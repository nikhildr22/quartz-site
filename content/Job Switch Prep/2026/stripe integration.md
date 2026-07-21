# Stripe API Integration Reference


---

## Table of Contents

1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Configuration](#configuration)
4. [Domain Layer](#domain-layer)
5. [Application Layer](#application-layer)
6. [API Layer (Controller)](#api-layer-controller)
7. [Frontend (Angular)](#frontend-angular)
8. [Webhook Flow](#webhook-flow)
9. [Key Patterns & Notes](#key-patterns--notes)

---

## Overview

The integration uses **Stripe Checkout** (hosted payment page). The flow is:

```
User clicks "Pay"
    → Angular calls POST /api/Payment/CreateCheckoutSession
    → Backend builds Stripe Checkout Session (line items, metadata, URLs)
    → Backend returns session ID
    → Angular uses @stripe/stripe-js to redirect user to Stripe's hosted page
    → User pays on Stripe
    → Stripe calls POST /api/Payment/WebHook
    → Backend validates webhook signature, reads metadata, completes booking
```

---

## Dependencies

### Backend — NuGet

```xml
<!-- OBRP.Application.csproj -->
<PackageReference Include="Stripe.net" Version="45.10.0" />
```

### Frontend — NPM

```json
"@stripe/stripe-js": "^3.0.0"
```

---

## Configuration

### appsettings.json

```json
"StripeConfig": {
  "PublicApiKey": "",
  "SecretApiKey": "",
  "WebHookSecret": ""
}
```

- **PublicApiKey** — exposed to the frontend (used to load Stripe.js)
- **SecretApiKey** — backend only (used to create sessions, set on `StripeConfiguration.ApiKey`)
- **WebHookSecret** — backend only (used to verify webhook signatures via `EventUtility.ConstructEvent`)

### Frontend config.json

```json
{
  "stripePublicKey": ""
}
```

The Angular app reads this at runtime and passes `stripePublicKey` to the helper that calls `loadStripe()`.

### Domain Interface

```csharp
// IStripeConfig.cs
public interface IStripeConfig
{
    string PublicApiKey { get; set; }
    string SecretApiKey { get; set; }
    string WebHookSecret { get; set; }
}
```

### Infrastructure Implementation

```csharp
// StripeConfig.cs
public class StripeConfig : IStripeConfig
{
    public string PublicApiKey { get; set; } = null!;
    public string SecretApiKey { get; set; } = null!;
    public string WebHookSecret { get; set; } = null!;
}
```

### Dependency Injection (Autofac)

```csharp
// ApiModule.cs
StripeConfig stripeConfig = configurationRoot
    .GetSection(typeof(StripeConfig).Name)
    .Get<StripeConfig>();

builder.Register(x => stripeConfig!).As<IStripeConfig>();
```

### Program.cs — Set Global API Key

```csharp
// Must run at startup before any Stripe calls
StripeConfiguration.ApiKey = stripeConfig.SecretApiKey;
```

---

## Domain Layer

### Constants

```csharp
// StripeConstants.cs
public static class StripeConstants
{
    // Metadata keys attached to every Checkout Session
    public const string BookingGroupIdMetaDataName = "BookingGroupId";
    public const string UserIdMetaDataName = "UserId";
    public const string PersonIdMetaDataName = "PersonId";
    public const string SystemMetaDataName = "System";
    public const string BookingTriggerSourceKey = "BookingTriggerSourceKey";

    // Payment settings
    public const string Currency = "CHF";          // adapt to your currency
    public const string TaxBehavior = "inclusive";
    public const string PaymentMode = "payment";
    public const int PriceConversion = 100;         // multiply CHF by 100 → Rappen (like cents)

    // Purchase type labels (stored in metadata)
    public const string VoucherPurchase = "VoucherPurchase";
    public const string GuestPurchase = "GuestPurchase";
    public const string ShopPurchase = "ShopPurchase";
    public const string SchoolPurchase = "SchoolPurchase";
    public const string MixedPurchase = "MixedPurchase";

    // Checkout locale
    public const string GermanLocale = "de";
    public const string EnglishLocale = "en";

    // Statement descriptor (appears on customer's bank statement)
    public const string StatementDescriptorSuffix = "OBRP";

    // Success / Cancel redirect URLs (one set per checkout source)
    public const string GuestRideSuccessUrl = "...";
    public const string GuestRideCancelUrl  = "...";
    public const string ShopSuccessUrl      = "...";
    public const string ShopCancelUrl       = "...";
    public const string SchoolSuccessUrl    = "...";
    public const string SchoolCancelUrl     = "...";
}
```

### Enums

```csharp
public enum PaymentType
{
    Order = 0,    // paid online via Stripe
    Invoice = 1   // paid by invoice (skip Stripe)
}

public enum PaymentCheckoutSources
{
    GuestRideBooking  = 0,
    Shop              = 1,
    SchoolEventBooking = 2,
}
```

### Service Interface

```csharp
// IPaymentService.cs
public interface IPaymentService
{
    Task<string> CreateCheckoutSessionAsync(
        BookingGroupRegisteredUserModel model,
        CancellationToken cancellationToken = default);
}
```

### Model

```csharp
// BookingGroupRegisteredUserModel.cs
public class BookingGroupRegisteredUserModel
{
    public Guid CartId { get; set; }
    public Guid? RegisteredUserId { get; set; }
    public Guid? PersonId { get; set; }
    public Guid SeasonId { get; set; }
    public bool IsCartPaidByVouchers { get; set; } = false;
    public string? PaymentIntentId = null;
    public PaymentCheckoutSources? PaymentCheckoutSource { get; set; }
}
```

---

## Application Layer

### PaymentService — CreateCheckoutSessionAsync

The core method that builds the Stripe `Session`. Adapt this to your own line-item logic.

```csharp
// PaymentService.cs
public async Task<string> CreateCheckoutSessionAsync(
    BookingGroupRegisteredUserModel model,
    CancellationToken cancellationToken = default)
{
    // 1. Load your data (bookings, products, etc.) from DB
    var lineItems = new List<SessionLineItemOptions>();

    // 2. Build line items — see projections below
    lineItems.Add(new SessionLineItemOptions
    {
        PriceData = new SessionLineItemPriceDataOptions
        {
            Currency = StripeConstants.Currency,
            UnitAmount = (long)(price * StripeConstants.PriceConversion), // convert to cents
            TaxBehavior = StripeConstants.TaxBehavior,
            ProductData = new SessionLineItemPriceDataProductDataOptions
            {
                Name = "Product Name",
                Description = "Optional description",
            },
        },
        Quantity = 1,
    });

    // 3. Configure session options
    var options = new SessionCreateOptions
    {
        LineItems = lineItems,
        Mode = StripeConstants.PaymentMode,       // "payment"
        Currency = StripeConstants.Currency,
        Locale = StripeConstants.GermanLocale,
        SuccessUrl = StripeConstants.ShopSuccessUrl,
        CancelUrl  = StripeConstants.ShopCancelUrl,
        PaymentIntentData = new SessionPaymentIntentDataOptions
        {
            StatementDescriptorSuffix = StripeConstants.StatementDescriptorSuffix,
        },
        Metadata = new Dictionary<string, string>
        {
            // IMPORTANT: attach all IDs you need in the webhook
            { StripeConstants.BookingGroupIdMetaDataName, model.CartId.ToString() },
            { StripeConstants.UserIdMetaDataName,          model.RegisteredUserId?.ToString() ?? "" },
            { StripeConstants.PersonIdMetaDataName,        model.PersonId?.ToString() ?? "" },
            { StripeConstants.BookingTriggerSourceKey,     StripeConstants.ShopPurchase },
        },
    };

    // 4. Create session via Stripe API
    var service = new SessionService();
    var session = await service.CreateAsync(options, cancellationToken: cancellationToken);

    // 5. Return session ID to frontend
    return session.Id;
}
```

### Line Item Projections (helper pattern)

Each entity type has a projection method that converts it to `SessionLineItemOptions`:

```csharp
// BookingEntityProjections.cs — example for a shipping cost line item
public static SessionLineItemOptions ToStripeShippingLineItem(this BookingEntity booking)
{
    return new SessionLineItemOptions
    {
        PriceData = new SessionLineItemPriceDataOptions
        {
            Currency = StripeConstants.Currency,
            UnitAmount = (long)(booking.ShippingCost * StripeConstants.PriceConversion),
            TaxBehavior = StripeConstants.TaxBehavior,
            ProductData = new SessionLineItemPriceDataProductDataOptions
            {
                Name = "Shipping",
            },
        },
        Quantity = 1,
    };
}

// VoucherEntityProjections.cs — example for a voucher
public static SessionLineItemOptions ToStripeLineItem(this VoucherEntity voucher)
{
    return new SessionLineItemOptions
    {
        PriceData = new SessionLineItemPriceDataOptions
        {
            Currency = StripeConstants.Currency,
            UnitAmount = (long)(voucher.Price * StripeConstants.PriceConversion),
            TaxBehavior = StripeConstants.TaxBehavior,
            ProductData = new SessionLineItemPriceDataProductDataOptions
            {
                Name = voucher.Name,
                Description = voucher.Description,
            },
        },
        Quantity = 1,
    };
}
```

### Stripe Metadata Extensions

Safe helpers to read webhook metadata without throwing:

```csharp
// StripeExtensions.cs
public static class StripeExtensions
{
    public static bool TryGetMetadataValue(
        this Session session, string key, out string? value)
    {
        value = null;
        if (session.Metadata == null) return false;
        return session.Metadata.TryGetValue(key, out value);
    }

    public static bool TryGetMetadataGuidValue(
        this Session session, string key, out Guid? value)
    {
        value = null;
        if (!session.TryGetMetadataValue(key, out var raw)) return false;
        if (Guid.TryParse(raw, out var guid))
        {
            value = guid;
            return true;
        }
        return false;
    }

    public static bool TryGetMetadataBoolValue(
        this Session session, string key, out bool value)
    {
        value = false;
        if (!session.TryGetMetadataValue(key, out var raw)) return false;
        return bool.TryParse(raw, out value);
    }
}
```

---

## API Layer (Controller)

```csharp
// PaymentController.cs
[ApiController]
[Route("api/[controller]")]
public class PaymentController : ControllerBase
{
    private readonly IPaymentService _paymentService;
    private readonly IStripeConfig _stripeConfig;
    // ... inject other booking services

    // ─── Create Checkout Session ──────────────────────────────────────────────

    [HttpPost("CreateCheckoutSession")]
    [Authorize]  // protect this endpoint
    public async Task<IActionResult> CreateCheckoutSessionAsync(
        [FromBody] BookingGroupRegisteredUserModel model)
    {
        var sessionId = await _paymentService.CreateCheckoutSessionAsync(model);
        return Ok(sessionId);
    }

    // ─── Webhook ─────────────────────────────────────────────────────────────

    [HttpPost("WebHook")]
    [AllowAnonymous]  // Stripe calls this — no auth header
    public async Task<IActionResult> WebHookAsync()
    {
        var json = await new StreamReader(HttpContext.Request.Body).ReadToEndAsync();
        var stripeSignature = Request.Headers["Stripe-Signature"];

        Event stripeEvent;
        try
        {
            // Validate the webhook signature — NEVER skip this
            stripeEvent = EventUtility.ConstructEvent(
                json,
                stripeSignature,
                _stripeConfig.WebHookSecret);
        }
        catch (StripeException)
        {
            return BadRequest();
        }

        if (stripeEvent.Type == EventTypes.CheckoutSessionCompleted)
        {
            var session = stripeEvent.Data.Object as Session;
            if (session == null) return BadRequest();

            // Read metadata that was attached when creating the session
            session.TryGetMetadataGuidValue(StripeConstants.UserIdMetaDataName,          out var userId);
            session.TryGetMetadataGuidValue(StripeConstants.PersonIdMetaDataName,        out var personId);
            session.TryGetMetadataGuidValue(StripeConstants.BookingGroupIdMetaDataName,  out var groupId);
            session.TryGetMetadataValue    (StripeConstants.BookingTriggerSourceKey,     out var source);

            // Route to the correct domain service based on purchase type
            switch (source)
            {
                case StripeConstants.GuestPurchase:
                    await _guestBookingService.CompleteBookingAsync(
                        groupId!.Value, session.PaymentIntentId);
                    break;

                case StripeConstants.ShopPurchase:
                    await _shopService.CompleteBookingAsync(
                        groupId!.Value, session.PaymentIntentId);
                    break;

                case StripeConstants.SchoolPurchase:
                    await _schoolEventBookingService.CompleteBookingAsync(
                        groupId!.Value, session.PaymentIntentId);
                    break;
            }
        }

        return Ok();
    }
}
```

> **Important**: Stripe expects a `200 OK` even if you do nothing with the event. If you return a non-2xx, Stripe will retry.

---

## Frontend (Angular)

### Stripe Helper

```typescript
// stripe.helper.ts
import { loadStripe, StripeError } from '@stripe/stripe-js';
import { MessageService } from 'primeng/api';

export default class StripeHelper {
    /**
     * Redirects the user to Stripe's hosted checkout page.
     * @param stripePublicKey  from config.json / environment
     * @param sessionId        returned by POST /api/Payment/CreateCheckoutSession
     */
    public static redirectToCheckOut(
        messageService: MessageService,
        stripePublicKey: string,
        sessionId: string
    ): Promise<any> {
        return loadStripe(stripePublicKey).then(stripe => {
            return stripe?.redirectToCheckout({ sessionId })
                .catch((stripeError: StripeError) => {
                    messageService.add({
                        severity: 'error',
                        summary: 'Payment Error',
                        detail: stripeError.message,
                    });
                });
        });
    }
}
```

### Angular API Service (generated by NSwag)

```typescript
// api-services.ts — PaymentService
export class PaymentService {
    constructor(
        private http: HttpClient,
        @Inject(API_BASE_URL) private baseUrl: string
    ) {}

    createCheckoutSession(model: BookingGroupRegisteredUserModel): Observable<string> {
        const url = this.baseUrl + '/api/Payment/CreateCheckoutSession';
        return this.http.post<string>(url, JSON.stringify(model), {
            headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
        });
    }
}
```

### TypeScript Models

```typescript
export interface BookingGroupRegisteredUserModel {
    cartId: string;
    registeredUserId?: string | null;
    personId?: string | null;
    seasonId: string;
    isCartPaidByVouchers: boolean;
    paymentCheckoutSource?: PaymentCheckoutSources | null;
}

export enum PaymentCheckoutSources {
    GuestRideBooking   = 0,
    Shop               = 1,
    SchoolEventBooking = 2,
}
```

### Typical Component Usage

```typescript
// booking-payment.component.ts
async pay(): Promise<void> {
    const model: BookingGroupRegisteredUserModel = {
        cartId: this.cartId,
        registeredUserId: this.userId,
        personId: this.personId,
        seasonId: this.seasonId,
        isCartPaidByVouchers: false,
        paymentCheckoutSource: PaymentCheckoutSources.Shop,
    };

    const sessionId = await firstValueFrom(this.paymentService.createCheckoutSession(model));

    await StripeHelper.redirectToCheckOut(
        this.messageService,
        this.config.stripePublicKey,
        sessionId
    );
}
```

---

## Webhook Flow

```
Stripe → POST /api/Payment/WebHook
           │
           ├─ Read raw request body (before any model binding!)
           ├─ Read "Stripe-Signature" header
           ├─ EventUtility.ConstructEvent(body, sig, webhookSecret)
           │     └─ throws StripeException if invalid → return 400
           │
           └─ if event.Type == "checkout.session.completed"
                 ├─ cast Data.Object → Session
                 ├─ read Metadata["BookingGroupId"]
                 ├─ read Metadata["BookingTriggerSourceKey"]
                 └─ route to appropriate CompleteBookingAsync()
                       └─ store session.PaymentIntentId on entity
```

### Registering the Webhook in Stripe Dashboard

1. Go to **Stripe Dashboard → Developers → Webhooks → Add endpoint**
2. URL: `https://yourdomain.com/api/Payment/WebHook`
3. Events to listen for: `checkout.session.completed`
4. Copy the **Signing secret** → paste as `WebHookSecret` in `appsettings.json`

---

## Key Patterns & Notes

| Pattern | Detail |
|---|---|
| **Raw body in webhook** | Do not use `[FromBody]` on the webhook action — read `HttpContext.Request.Body` as a raw string so Stripe's signature check works |
| **Metadata for routing** | Attach all domain IDs and the purchase type to `Session.Metadata` at creation time; read them back in the webhook |
| **Price conversion** | Stripe amounts are in the smallest currency unit (cents/Rappen). Multiply `decimal` prices by `100` before sending |
| **Idempotency** | Stripe may deliver a webhook more than once. Make `CompleteBookingAsync` idempotent (check if already completed) |
| **Locale** | Pass `Locale = "de"` or `"en"` to `SessionCreateOptions` for a localised checkout page |
| **Tax behaviour** | `TaxBehavior = "inclusive"` means displayed prices already include tax |
| **Statement descriptor** | `StatementDescriptorSuffix` (≤ 22 chars) appears on the customer's bank statement |
| **AllowAnonymous on webhook** | Stripe does not send auth headers — mark the webhook endpoint `[AllowAnonymous]` but validate via signature |
| **Frontend public key** | Never use the secret key on the frontend. Only `PublicApiKey` is passed to `loadStripe()` |
| **NSwag** | The Angular `PaymentService` is auto-generated from the OpenAPI spec via NSwag — edit `nswag.json` to regenerate |
