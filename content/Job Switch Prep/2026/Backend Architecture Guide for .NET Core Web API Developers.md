# Backend Architecture Guide for .NET Core Web API Developers

**For developers coming from Controller-Interface-Service pattern and .NET Core Web API background**

---

## Table of Contents
1. [Architecture Overview](#architecture-overview)
2. [Key Differences from Traditional Web API](#key-differences-from-traditional-web-api)
3. [Request Handling - Blazor Pages + MediatR](#request-handling---blazor-pages--mediatr)
4. [Service Layer - CQRS with MediatR](#service-layer---cqrs-with-mediatr)
5. [Interface Patterns](#interface-patterns)
6. [Dependency Injection](#dependency-injection)
7. [Data Access - Unit of Work Pattern](#data-access---unit-of-work-pattern)
8. [MediatR Pipeline & Behaviors](#mediatr-pipeline--behaviors)
9. [Validation with FluentValidation](#validation-with-fluentvalidation)
10. [Domain Models](#domain-models)
11. [Architecture Comparison](#architecture-comparison)
12. [Common Patterns](#common-patterns)

---

## Architecture Overview

### Pattern Used
This application uses **Clean Architecture** with **CQRS** (Command Query Responsibility Segregation) via **MediatR**, combined with **Domain-Driven Design** principles.

### Layer Organization

Each business domain (Account, Personnel, Organization, KnowHow, Object, etc.) is structured as a module:

```
Module/
├── *.Domain                  → Entities, Value Objects, Domain Logic
├── *.Application             → Commands, Queries, Handlers, Business Logic
├── *.Application.Interface   → Command/Query Contracts (IRequest<T>)
├── *.Infrastructure          → Data Access, EF Core, External Services
└── *.Presentation            → Blazor Components (.razor), UI Logic
```

**Statistics:**
- **304 Commands** (write operations)
- **485 Queries** (read operations)
- **No traditional Repository pattern** - uses Unit of Work with direct DbContext access

### Critical Difference

Unlike traditional .NET Core Web API where you have:
```
Angular Frontend → HTTP → API Controller → Service → Repository → Database
```

This application runs as a **single process**:
```
Blazor Component → MediatR.Send() → Handler → UnitOfWork → Database
```

**No HTTP layer** between UI and business logic for the main application (only for external InboundApi integration).

---

## Key Differences from Traditional Web API

| Aspect | Traditional Web API | **This Application** |
|--------|---------------------|---------------------|
| **Frontend** | Separate SPA (Angular/React) | Blazor Server (integrated) |
| **Request Handling** | Controllers with `[HttpPost]` | Blazor pages + `MediatR.Send()` |
| **Communication** | HTTP/REST APIs | In-process method calls |
| **Service Layer** | `IService` + `ServiceImpl` | Command/Query Handlers |
| **Service Granularity** | Coarse (UserService with many methods) | Fine-grained (one handler per operation) |
| **Data Access** | Repository + `IRepository<T>` | UnitOfWork with direct DbContext |
| **Transactions** | Manual or `[TransactionScope]` | Automatic via pipeline behavior |
| **Validation** | Model attributes + manual | FluentValidation in handlers |
| **Routing** | `[Route]` attributes | Blazor `@page` directive |
| **State Management** | Client-side (NgRx, Redux) | Server-side Blazor state |
| **Deployment** | Two apps (FE + BE) | Single application |

### Architecture Flow Comparison

**Traditional Web API:**
```
┌─────────────┐      HTTP      ┌────────────┐     ┌─────────┐     ┌────────────┐
│   Angular   │ ───────────→   │ Controller │ ──→ │ Service │ ──→ │ Repository │
│  Component  │                │            │     │         │     │            │
└─────────────┘                └────────────┘     └─────────┘     └────────────┘
  TypeScript                        C#                  C#              C#
```

**This Application (Blazor + CQRS):**
```
┌─────────────┐                ┌────────────┐     ┌───────────┐     ┌────────────┐
│   Blazor    │  MediatR.Send  │  Handler   │ ──→ │ UnitOfWork│ ──→ │  DbContext │
│  Component  │ ───────────→   │  (CQRS)    │     │           │     │            │
└─────────────┘                └────────────┘     └───────────┘     └────────────┘
     C#                              C#                 C#               C#
```

---

## Request Handling - Blazor Pages + MediatR

### What You're Used To: Controller Pattern

**Traditional .NET Core Web API:**

```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;
    
    public UsersController(IUserService userService)
    {
        _userService = userService;
    }
    
    [HttpPost]
    public async Task<IActionResult> CreateUser(CreateUserDto dto)
    {
        var result = await _userService.CreateUser(dto);
        return Ok(result);
    }
    
    [HttpGet("{id}")]
    public async Task<IActionResult> GetUser(Guid id)
    {
        var user = await _userService.GetUser(id);
        return Ok(user);
    }
}
```

**Angular Component:**
```typescript
createUser() {
  this.http.post('/api/users', this.userData).subscribe(
    result => console.log('Success'),
    error => console.error('Error')
  );
}
```

### How It Works Here: Blazor + MediatR

**Blazor Component (C# + Razor):**

**File:** `Benobix.Account.Presentation/Pages/Settings/SettingsUsersPage.razor.cs`
```csharp
public partial class SettingsUsersPage : SettingsPage
{
    [Inject] private ISender MediatR { get; set; } = null!;
    
    // Direct MediatR call - NO HTTP involved!
    private async Task AddAccount(Person p)
    {
        // Send command to MediatR
        var createResult = await MediatR.Send(
            new CreateUserAccountCommand(p.Email!, p));
            
        if (createResult.Success)
        {
            ShowSuccessSnackbar(AccountLocalization.SuccessAddAccount);
            await _table.ReloadServerData();
        }
        else
        {
            ShowErrorSnackbar(AccountLocalization.ErrorAddAccount);
        }
    }
    
    private async Task<TableData<UserIncludingPerson>> LoadServerData(
        TableState state, 
        CancellationToken cancellationToken)
    {
        // Query via MediatR
        var result = await MediatR.Send(
            new GetPaginatedUsersQuery(state.Page, state.PageSize), 
            cancellationToken);
            
        return new TableData<UserIncludingPerson>
        {
            Items = result.Items,
            TotalItems = result.TotalCount
        };
    }
}
```

**Razor Template:**
```razor
@page "/settings/users"
@attribute [Authorize(Policy = PolicyNames.AdminUser)]
@using Benobix.Account.Application.Interface.Commands

<BenobixTable T="UserIncludingPerson"
              LoadServerData="@LoadServerData"
              OnRowClick="@(e => OpenEditDialog(e.Item))">
    <!-- Table columns -->
</BenobixTable>
```

**Key Takeaway:**
- ✅ No `[ApiController]` needed
- ✅ No HTTP requests (`HttpClient`, `fetch`)
- ✅ Direct in-process method calls via MediatR
- ✅ Type-safe across entire stack (no JSON serialization)

### When Controllers ARE Used: External API Only

Controllers exist **only** for the **InboundApi** module (for external system integration):

**File:** `Benobix.InboundApi.Presentation/Controllers/PersonController.cs`
```csharp
[Route("inboundapi/person")]
[InboundApiAuthorize(InboundApiType.Person)]
public class PersonController(
    IMediator mediatR, 
    IInboundApiAuthorizationService authService)
    : BaseConnectInboundApiController<InboundApiPersonDto, Guid>(mediatR, authService)
{
    [HttpGet]
    public async Task<ActionResult<IPaginatedList<InboundApiPersonDto>>> GetPaginated(
        int pageIndex, int pageSize)
    {
        IPaginatedList<InboundApiPersonDto> result = null!;

        await Track(async () =>
        {
            ValidatePageSize(pageSize);
            // Still uses MediatR internally!
            result = await mediatR.Send(
                new GetPaginatedPersonsForInboundApiQuery(
                    GetInboundApiConnectionId()!.Value, pageIndex, pageSize));
        });

        return Ok(result);
    }
    
    [HttpPost]
    public async Task<ActionResult<InboundApiPersonDto>> Save(
        InboundApiPersonSaveDto person, 
        CancellationToken cancellationToken = default)
    {
        InboundApiPersonDto result = null!;
        
        await Track(async () =>
        {
            result = await mediatR.Send(
                new SavePersonForInboundApiCommand(person, GetInboundApiConnectionId()!.Value), 
                cancellationToken);
        }, person.Id);

        return result;
    }
}
```

**Pattern:** Even controllers delegate to MediatR handlers - they're just HTTP adapters for external systems.

---

## Service Layer - CQRS with MediatR

### Traditional Service Pattern

**What you're used to:**

```csharp
// Interface
public interface IUserService
{
    Task<UserDto> CreateUser(CreateUserDto dto);
    Task<UserDto> GetUser(Guid id);
    Task<List<UserDto>> GetAllUsers();
    Task UpdateUser(UpdateUserDto dto);
    Task DeleteUser(Guid id);
}

// Implementation
public class UserService : IUserService
{
    private readonly IUserRepository _repository;
    private readonly IEmailService _emailService;
    
    public UserService(IUserRepository repository, IEmailService emailService)
    {
        _repository = repository;
        _emailService = emailService;
    }
    
    public async Task<UserDto> CreateUser(CreateUserDto dto)
    {
        // Validation
        if (string.IsNullOrEmpty(dto.Email))
            throw new ValidationException("Email required");
            
        // Business logic
        var user = new User { Email = dto.Email, ... };
        await _repository.Add(user);
        await _repository.SaveChanges();
        
        // Send email
        await _emailService.SendWelcomeEmail(user.Email);
        
        return MapToDto(user);
    }
    
    public async Task<UserDto> GetUser(Guid id)
    {
        var user = await _repository.GetById(id);
        return MapToDto(user);
    }
    
    // ... more methods
}
```

### CQRS Pattern in This Application

Instead of one service with many methods, each **operation** gets its own **Command** or **Query** with a dedicated **Handler**.

#### Commands (Write Operations)

**Command Definition (Contract):**

**File:** `Benobix.Account.Application.Interface/Commands/CreateUserAccountCommand.cs`
```csharp
using MediatR;

namespace Benobix.Account.Application.Interface.Commands;

// Command = Data Transfer Object + Marker Interface
public record CreateUserAccountCommand(
    string Email, 
    Person Person, 
    bool CreatePerson = false) 
    : IRequest<(bool Success, SendEmailResult EmailResult)>;
    //  ^^^^^^^^ - MediatR marker interface
    //            return type ──────────────────────────┘
```

**Command Handler (Implementation):**

**File:** `Benobix.Account.Application/Commands/CreateUserAccountCommand.cs`
```csharp
namespace Benobix.Account.Application.Commands;

public class CreateUserAccountCommandHandler(
    IUnscopedSender mediatR,       // For nested MediatR calls
    IAccountService accountService  // Complex business logic service
) : IRequestHandler<CreateUserAccountCommand, (bool Success, SendEmailResult EmailResult)>
{
    public async Task<(bool Success, SendEmailResult EmailResult)> Handle(
        CreateUserAccountCommand request, 
        CancellationToken cancellationToken)
    {
        // 1. Validation (FluentValidation)
        if (request.CreatePerson)
        {
            var validationResult = await new UserValidator(mediatR)
                .ValidateAsync(request.Person, cancellationToken);
            
            if (!validationResult.IsValid)
            {
                throw new ValidationException(validationResult.Errors);
            }
        }

        // 2. Business logic via Service
        return await accountService.CreateUserAccount(
            request.Email, 
            request.Person, 
            request.CreatePerson, 
            cancellationToken);
    }
}
```

**Another Command Example:**

**File:** `Benobix.Account.Application/Commands/LogInCommand.cs`
```csharp
public record LogInCommand(string Email, string Password, bool RememberMe) 
    : IRequest<LoginResultWithLoggedInPerson>
{
    // Override ToString to hide password in logs
    public override string ToString()
        => $"{nameof(LogInCommand)} {{{nameof(Email)} = {Email}, " +
           $"{nameof(Password)} = ***, {nameof(RememberMe)} = {RememberMe}}}";
}

public class LogInCommandHandler(
    ILogInService logInService,
    IUnitOfWork unitOfWork,
    ILogger<LogInCommand> logger,
    ISettingsAccessService settingsAccessService,
    IAccountService accountService
) : IRequestHandler<LogInCommand, LoginResultWithLoggedInPerson>
{
    public async Task<LoginResultWithLoggedInPerson> Handle(
        LogInCommand request, 
        CancellationToken cancellationToken)
    {
        logger.Log(LogLevel.Information, "Log in attempt from {user}", request.Email);

        // 1. Authenticate via ASP.NET Core Identity
        var result = await logInService.PasswordSignInAsync(
            request.Email, 
            request.Password, 
            request.RememberMe, 
            lockoutOnFailure: true, 
            cancellationToken);

        if (result.Status == LogInResultStatus.Succeeded)
        {
            logger.Log(LogLevel.Information, 
                "Log in attempt from {user} was successful", request.Email);
        }

        // 2. Check if application is disabled (maintenance mode)
        var settings = await settingsAccessService
            .GetSettings<AccountModuleSettings>(cancellationToken);
            
        if (settings?.IsApplicationDisabled is true 
            && !accountService.IsAdmin(result.User.Id))
        {
            return new LoginResultWithLoggedInPerson(
                LogInResultStatus.ApplicationDeactivated);
        }

        // 3. Fetch full person data from database
        var loggedInPerson = await unitOfWork
            .CreateQuery<Person>()
            .Include(p => p.Settings)
            .SingleAsync(p => p.Id == result.User.PersonId, cancellationToken);

        return new LoginResultWithLoggedInPerson(result.Status, loggedInPerson);
    }
}
```

#### Queries (Read Operations)

**Query Definition:**

**File:** `Benobix.Account.Application.Interface/Queries/GetLoggedInPersonQuery.cs`
```csharp
using System.Security.Claims;
using MediatR;

namespace Benobix.Account.Application.Interface.Queries;

public record GetLoggedInPersonQuery(ClaimsPrincipal Principal) 
    : IRequest<Person>;
```

**Query Handler:**

**File:** `Benobix.Account.Application/Queries/GetLoggedInPersonQuery.cs`
```csharp
namespace Benobix.Account.Application.Queries;

public class GetLoggedInPersonQueryHandler(
    UserManager<BenobixUser> userManager,
    IUnitOfWork unitOfWork
) : IRequestHandler<GetLoggedInPersonQuery, Person>
{
    public async Task<Person> Handle(
        GetLoggedInPersonQuery request, 
        CancellationToken cancellationToken)
    {
        // 1. Get user ID from claims
        var userId = userManager.GetUserId(request.Principal);
        if (string.IsNullOrEmpty(userId))
        {
            throw new UnauthorizedAccessException();
        }

        // 2. Query database with UnitOfWork
        var user = await unitOfWork
            .CreateQuery<BenobixUser>()
            .Include(u => u.Person)
            .ThenInclude(p => p.Settings)
            .FirstOrDefaultAsync(u => u.Id == userId, cancellationToken);

        var person = user?.Person;
        if (person is null)
        {
            throw new UnauthorizedAccessException();
        }

        return person;
    }
}
```

#### Complex Update Command with Version Tracking

**File:** `Benobix.KnowHow.Application/Commands/UpdateQualificationCommand.cs`
```csharp
public record UpdateQualificationCommand(Qualification Qualification) 
    : IChangeDatabaseRequest;  // Marker for automatic transaction

public class UpdateQualificationCommandHandler(IUnitOfWork unitOfWork) 
    : IRequestHandler<UpdateQualificationCommand>
{
    public async Task Handle(
        UpdateQualificationCommand request, 
        CancellationToken cancellationToken)
    {
        var updatedQualification = request.Qualification;
        
        // 1. Validate
        var validator = new QualificationValidator();
        var validationResult = await validator.ValidateAsync(
            updatedQualification, cancellationToken);

        if (!validationResult.IsValid)
        {
            throw new ValidationException(validationResult.Errors);
        }

        // 2. Load existing entity with related data
        var unchangedQualification = await unitOfWork
            .CreateQuery<Qualification>()
            .Include(q => q.Scale)
            .ThenInclude(s => s!.ScaleItems)
            .SingleAsync(q => q.Id == updatedQualification.Id, cancellationToken);

        // 3. Create version history
        var historyCopy = CreateVersionHistory(unchangedQualification);
        
        // 4. Apply updates
        await UpdateEntity(updatedQualification, unchangedQualification, 
            historyCopy, cancellationToken);
            
        // SaveChanges automatically called by TransactionBehaviour
    }

    private Qualification CreateVersionHistory(Qualification original)
    {
        // Creates a copy for audit trail
        var copy = original with
        {
            Id = Guid.Empty,  // New ID
            IsActive = false,
            IsLastVersion = false,
            ScaleId = null,
            Scale = null,
        };

        // Deep copy related entities
        if (original.Scale != null)
        {
            copy.Scale = original.Scale with { Id = Guid.Empty };
            copy.Scale.ScaleItems = original.Scale.ScaleItems
                .Select(si => si with { Id = Guid.Empty, Scale = copy.Scale })
                .ToList();
        }

        unitOfWork.Add(copy);
        return copy;
    }
}
```

### Benefits of CQRS over Traditional Services

| Aspect | Traditional Service | CQRS Handlers |
|--------|---------------------|---------------|
| **Granularity** | Coarse (one service, many methods) | Fine-grained (one handler per operation) |
| **Dependencies** | All injected in constructor | Only what each handler needs |
| **Testing** | Mock entire service | Test handlers independently |
| **Single Responsibility** | Multiple operations in one class | One operation per handler |
| **Optimization** | One implementation for all | Optimize read vs write separately |
| **Cross-cutting** | Manual in each method | Automatic via behaviors |

---

## Interface Patterns

### Traditional Interface-Service Pattern

```csharp
// Interface defines contract
public interface IAccountService
{
    Task<UserDto> CreateUser(CreateUserDto dto);
    Task<UserDto> GetUser(Guid id);
}

// Implementation
public class AccountService : IAccountService
{
    // Implementation details
}

// Registration
services.AddScoped<IAccountService, AccountService>();
```

### How It Works Here

Some services still use traditional interface pattern for **complex domain logic**:

**Service Interface:**

**File:** `Benobix.Account.Application.Interface/Services/IAccountService.cs`
```csharp
namespace Benobix.Account.Application.Interface.Services;

public interface IAccountService
{
    Task<bool> HasUserAccount(Guid personId);
    Task<bool> HasUserAccount(string email);
    Task DeactivateAccount(Guid personId, CancellationToken cancellationToken);
    Task ActivateAccount(Guid personId, CancellationToken cancellationToken);
    
    Task<IEnumerable<Person>> GetPersonsWithPermission(
        Guid accessRoleIdentifier, 
        PermissionType permissionType, 
        AccessRolePermission accessRolePermission, 
        CancellationToken cancellationToken);
    
    Task<(bool Success, SendEmailResult EmailResult)> CreateUserAccount(
        string email, 
        Person person, 
        bool createPerson = false, 
        CancellationToken cancellationToken = default);
    
    Task<bool> ConfirmUserAccount(string id, string token);
    Task<SendEmailResult> SendChangeEmailNotification(
        Guid personId, string newEmail, CancellationToken cancellationToken = default);
    Task<bool> ChangeEmail(string id, string newEmail, string token);
    Task<bool> IsSetPasswordRequested(ClaimsPrincipal user);
    Task<string> GeneratePasswordResetTokenAsync(ClaimsPrincipal user);
    Task<bool> SetNewPassword(ClaimsPrincipal user, string currentPassword, string newPassword);
    Task<bool> ChangePassword(ClaimsPrincipal user, string newPassword, string code);
    Task<bool> ResetPassword(string email, CancellationToken cancellationToken = default);
    Task<string> IsPasswordValid(string password);
    Task<bool> IsTwoFactorEnabled(ClaimsPrincipal claimsPrincipal);
    Task<string?> GetTwoFactorAuthenticatorKey(ClaimsPrincipal claimsPrincipal);
    bool IsAdmin(ClaimsPrincipal? claimsPrincipal);
    Task<string> GenerateRandomPassword(int length = 12);
    string HashPassword(string username, string password);
}
```

**Service Implementation:**

**File:** `Benobix.Account.Application/Services/AccountService.cs`
```csharp
namespace Benobix.Account.Application.Services;

public class AccountService(
    UserManager<BenobixUser> userManager,
    IUnitOfWork unitOfWork,
    IApplicationSettings applicationSettings,
    IEmailSender emailSender,
    IEmailContentBuilder contentBuilder,
    IRouteProvider routeProvider
) : IAccountService
{
    public async Task<bool> HasUserAccount(Guid personId)
    {
        return await GetBenobixUser(personId, CancellationToken.None) is not null;
    }

    public async Task<bool> HasUserAccount(string email)
    {
        return await userManager.FindByEmailAsync(email) is not null;
    }

    public async Task DeactivateAccount(Guid personId, CancellationToken cancellationToken)
    {
        var user = await GetBenobixUser(personId, cancellationToken);
        if (user is not null)
        {
            await DeactivateUser(user);
        }
    }

    public async Task<(bool Success, SendEmailResult EmailResult)> CreateUserAccount(
        string email, 
        Person person, 
        bool createPerson = false, 
        CancellationToken cancellationToken = default)
    {
        // 1. Create user entity
        BenobixUser newUser = new()
        {
            Email = email,
            UserName = email,
            MustSetNewPassword = true,
            LockoutEnabled = true,
        };

        if (createPerson)
        {
            newUser.Person = person;
        }
        else
        {
            newUser.PersonId = person.Id;
        }

        // 2. Use ASP.NET Core Identity
        var generatedPassword = await GenerateRandomPassword();
        var result = await userManager.CreateAsync(newUser, generatedPassword);

        if (!result.Succeeded)
        {
            return (false, SendEmailResult.Failure);
        }

        // 3. Generate confirmation token
        var emailConfirmToken = Uri.EscapeDataString(
            await userManager.GenerateEmailConfirmationTokenAsync(newUser));
        
        var locale = person.Settings.Language;
        
        // 4. Send welcome email
        var sendEmailResult = await emailSender.SendEmail(
            [person],
            recipient => recipient.GetMailAddress(),
            LocalizationService.GetLocalizedText<AccountLocalization>(
                nameof(AccountLocalization.NewAccountNotificationSubject), locale),
            recipient => contentBuilder
                .Create(LocalizationService.GetLocalizedText<AccountLocalization>(
                    nameof(AccountLocalization.NewAccountNotificationSubject), locale))
                .AddTitle(LocalizationService.GetLocalizedText<AccountLocalization>(
                    nameof(AccountLocalization.NewAccountNotificationTitle), locale))
                .AddParagraph($"{LocalizationService.GetLocalizedText<AccountLocalization>(
                    nameof(AccountLocalization.AccountNotificationGreeting), locale)} {recipient.GetFullName()}")
                .AddParagraph($"{string.Format(
                    LocalizationService.GetLocalizedText<AccountLocalization>(
                        nameof(AccountLocalization.NewAccountNotificationInitialPassword), locale), 
                    generatedPassword)}")
                .AddLink(
                    LocalizationService.GetLocalizedText<AccountLocalization>(
                        nameof(AccountLocalization.NewAccountNotificationLink), locale), 
                    $"{applicationSettings.GetBaseUrl()}{routeProvider.GetConfirmEmailRoute(newUser.Id, emailConfirmToken)}")
                .Build(),
            cancellationToken);
            
        return (true, sendEmailResult);
    }

    public async Task<IEnumerable<Person>> GetPersonsWithPermission(
        Guid accessRoleIdentifier, 
        PermissionType permissionType, 
        AccessRolePermission accessRolePermission, 
        CancellationToken cancellationToken)
    {
        // Complex query logic
        var query = unitOfWork.CreateQuery<BenobixUserRole>()
            .Include(ur => ur.User)
            .ThenInclude(u => u!.Person);

        query = query.Where(ur => ur.Role!.Claims.Any(c => 
            c.AccessRoleIdentifier == accessRoleIdentifier
            && (permissionType == PermissionType.Read 
                ? c.Permission.ReadPermissions == accessRolePermission 
                : c.Permission.WritePermissions == accessRolePermission)));

        return await query.Select(ur => ur.User!.Person).ToListAsync(cancellationToken);
    }
}
```

### When to Use Services vs Handlers

| Use Service When | Use Handler When |
|------------------|------------------|
| Complex, reusable domain logic | Simple CRUD operation |
| Used by multiple handlers | One-time operation |
| Encapsulates ASP.NET Core Identity | Direct database query |
| Third-party integration | Straightforward validation |

**Pattern:** Handlers orchestrate, Services encapsulate complex logic.

---

## Dependency Injection

### Module-Based Registration

Each module registers its own dependencies using extension methods:

**File:** `Benobix.Account.Application/DependencyInjection.cs`
```csharp
namespace Benobix.Account.Application;

public static class DependencyInjection
{
    public static IServiceCollection AddAccountApplication(
        this IServiceCollection services)
    {
        // Auto-register all MediatR handlers from this assembly
        services.AddMediatR(cfg => 
        {
            cfg.RegisterServicesFromAssemblies(Assembly.GetExecutingAssembly());
        });
        
        // Register services
        services.AddScoped<IAccountService, AccountService>();
        services.AddScoped<ILocalization, AccountLocalization>();

        return services;
    }
}
```

**File:** `Benobix.Common.Application/DependencyInjection.cs`
```csharp
namespace Benobix.Common.Application;

public static class DependencyInjection
{
    public static IServiceCollection AddCommonApplication(
        this IServiceCollection services, 
        IConfiguration configuration)
    {
        services.AddScoped<ILocalization, CommonLocalization>();
        services.AddScoped<ILocalizationService, LocalizationService>();
        services.AddSingleton<IModuleRegistry, ModuleRegistry>();
        services.AddSingleton<IAccessRoleRegistry, AccessRoleRegistry>();
        services.AddScoped<IPictureService, PictureService>();
        services.AddScoped<IProfilePictureFileService, ProfilePictureFileService>();
        services.AddScoped<IUserInteractionLogger, UserInteractionLogger>();
        services.AddScoped<IReviewNotificationService, ReviewNotificationService>();

        services.AddStripe(configuration);
        services.AddMediatR(configuration, Assembly.GetExecutingAssembly());

        return services;
    }

    public static IServiceCollection AddMediatR(
        this IServiceCollection services, 
        params Assembly[] assemblies)
    {
        services.AddMediatR(cfg => 
        {
            cfg.RegisterServicesFromAssemblies(assemblies);
        });
        return services;
    }

    private static IServiceCollection AddMediatR(
        this IServiceCollection services, 
        IConfiguration configuration, 
        params Assembly[] assemblies)
    {
        services.AddMediatR(cfg =>
        {
            cfg.RegisterServicesFromAssemblies(assemblies);
            cfg.AddCommonBehaviours(configuration);  // Add pipeline behaviors
        });
        return services;
    }

    private static void AddCommonBehaviours(
        this MediatRServiceConfiguration cfg, 
        IConfiguration configuration)
    {
        // Optional performance logging
        if (configuration.GetValue<bool>("AdditionalLogging:Performance"))
        {
            cfg.AddBehavior(typeof(IPipelineBehavior<,>), 
                typeof(PerformanceLoggingBehaviour<,>));
        }

        // Global behaviors for ALL handlers
        cfg.AddBehavior(typeof(IPipelineBehavior<,>), 
            typeof(UnhandledExceptionBehaviour<,>));
        cfg.AddBehavior(typeof(IPipelineBehavior<,>), 
            typeof(TransactionBehaviour<,>));
    }
}
```

**File:** `Benobix.Common.Infrastructure/DependencyInjection.cs`
```csharp
namespace Benobix.Common.Infrastructure;

public static class DependencyInjection
{
    public static IServiceCollection AddCommonInfrastructure(
        this IServiceCollection services, 
        IConfiguration configuration)
    {
        // Register Unit of Work
        services.AddScoped<IUnitOfWork, UnitOfWork>();
        services.AddScoped<ISettingsAccessService, SettingsAccessService>();

        // Strategy Pattern: File storage based on configuration
        switch (configuration["FileStorage"])
        {
            case "AwsS3FileStorage":
                services.Configure<AwsS3FileStorageConfiguration>(
                    configuration.GetSection(nameof(AwsS3FileStorageConfiguration)));
                services.AddScoped<IFileStorageService, AwsS3FileStorageService>();
                break;
            case "LocalFileStorage":
                services.AddScoped<IFileStorageService, LocalFileStorageService>();
                break;
            case "DatabaseFileStorage":
                services.AddScoped<IFileStorageService, DatabaseFileStorageService>();
                break;
            default:
                throw new InvalidOperationException(
                    "Setting 'FileStorage' is not provided.");
        }

        services.AddScoped<PdfTypography>();
        services.AddDbContext(configuration);
        services.AddSmtpClient(configuration);
        services.AddApplicationSettings(configuration);
        services.AddSingleton<IAsyncMemoryCache, AsyncMemoryCache>();
        
        // Conditional registration
        if (configuration.GetValue<bool>("Stripe:DisableForDevelopment"))
        {
            services.AddScoped<IStripeCache, StripeNoOpCache>();
        }
        else
        {
            services.AddScoped<IStripeCache, StripeCache>();
        }

        return services;
    }

    private static IServiceCollection AddDbContext(
        this IServiceCollection services, 
        IConfiguration configuration)
    {
        var databaseConfiguration = configuration.GetSection("database")
            .Get<DatabaseConfiguration>()
            ?? throw new InvalidOperationException("'Database' section is not configured.");

        var postgresConnectionString = configuration
            .GetConnectionString("PostgresConnection");

        services.AddDbContext<BenobixDbContext>(options =>
        {
            switch (databaseConfiguration.Type)
            {
                case "Postgres" when postgresConnectionString is null:
                    throw new InvalidOperationException(
                        "Connection string 'PostgresConnection' not found.");
                case "Postgres":
                    DbTypeProvider.DbType = DbType.Postgres;
                    var assembly = VersionInformation.IsAdminApp
                        ? "Benobix.Common.Infrastructure.PostgresMigrationsAdminApp"
                        : "Benobix.Common.Infrastructure.PostgresMigrations";
                    
                    options.ReplaceService<IMigrationsSqlGenerator, 
                        CustomNpgsqlMigrationsSqlGenerator>();
                    options.ReplaceService<IMigrationsModelDiffer, 
                        CustomMigrationsModelDiffer>();
                    options.UseNpgsql(postgresConnectionString, 
                        builder => builder.MigrationsAssembly(assembly));
                    options.ConfigureWarnings(w => 
                        w.Ignore(RelationalEventId.PendingModelChangesWarning));
                    options.WithExpressionExpanding();
                    break;
                    
                case "InMemory":
                    DbTypeProvider.DbType = DbType.InMemory;
                    options.UseInMemoryDatabase(databaseName: "benobix");
                    options.ConfigureWarnings(builder => 
                        builder.Ignore(InMemoryEventId.TransactionIgnoredWarning));
                    break;
            }
        });

        return services;
    }
}
```

### Bootstrapping in Startup/Program

**File:** `Benobix.WebApp/DiBootstrap.cs`
```csharp
public static IServiceCollection AddBenobixServices(
    this IServiceCollection services, 
    IConfiguration configuration)
{
    services
        // Common infrastructure (DbContext, UnitOfWork, etc.)
        .AddCommonApplication(configuration)
        .AddCommonInfrastructure(configuration)
        
        // Module registrations
        .AddAccountApplication()
        .AddAccountInfrastructure()
        .AddAccountPresentation()
        
        .AddPersonnelApplication()
        .AddPersonnelInfrastructure()
        .AddPersonnelPresentation()
        
        .AddOrganizationApplication()
        .AddOrganizationInfrastructure()
        .AddOrganizationPresentation()
        
        .AddKnowHowApplication()
        .AddKnowHowInfrastructure()
        .AddKnowHowPresentation()
        
        .AddObjectApplication()
        .AddObjectInfrastructure()
        .AddObjectPresentation();
        
    // Replace default Mediator with scoped version
    services.AddScoped<IMediator, ScopedMediator>();
    services.AddScoped<IUnscopedSender, UnscopedMediator>();
    
    return services;
}
```

### Key Takeaways

- ✅ Each module has its own `DependencyInjection.cs`
- ✅ MediatR handlers are auto-discovered via assembly scanning
- ✅ No need to manually register each handler
- ✅ Extension methods chain for clean bootstrap

---

## Data Access - Unit of Work Pattern

### What You're Used To: Repository Pattern

**Traditional Repository:**

```csharp
// Interface
public interface IUserRepository
{
    Task<User> GetById(Guid id);
    Task<List<User>> GetAll();
    Task Add(User user);
    Task Update(User user);
    Task Delete(Guid id);
    Task SaveChanges();
}

// Implementation
public class UserRepository : IUserRepository
{
    private readonly DbContext _context;
    
    public async Task<User> GetById(Guid id)
    {
        return await _context.Users.FindAsync(id);
    }
    
    public async Task Add(User user)
    {
        await _context.Users.AddAsync(user);
    }
    
    public async Task SaveChanges()
    {
        await _context.SaveChangesAsync();
    }
}

// Registration
services.AddScoped<IUserRepository, UserRepository>();
```

### Unit of Work in This Application

**No Repository Pattern!** Instead, there's a single `IUnitOfWork` interface providing direct DbContext access:

**File:** `Benobix.Common.Application.Interface/Services/IUnitOfWork.cs`
```csharp
namespace Benobix.Common.Application.Interface.Services;

public interface IUnitOfWork : IDisposable
{
    // Direct DbSet access
    IQueryable<TEntity> Set<TEntity>() where TEntity : class;
    
    // Query builders (no tracking by default for performance)
    IQuery<TEntity> CreateQuery<TEntity>() where TEntity : class;
    IQuery<TEntity> CreateQueryAsTracking<TEntity>() where TEntity : class;
    
    // CRUD operations
    void Add<TEntity>(TEntity entity) where TEntity : class, IHasId;
    void AddRange<TEntity>(IEnumerable<TEntity> entity) where TEntity : class, IHasId;
    void Insert<TEntity>(TEntity entity) where TEntity : class, IHasId;
    void Update<TEntity>(TEntity entity) where TEntity : class, IHasId;
    void UpdateRange<TEntity>(IEnumerable<TEntity> entities) where TEntity : class, IHasId;
    
    Task Delete<TEntity>(Guid entityId, CancellationToken cancellationToken = default) 
        where TEntity : class, IHasId;
    void Delete<TEntity>(TEntity entity) where TEntity : class, IHasId;
    void DeleteRange<TEntity>(IEnumerable<TEntity> entities) where TEntity : class, IHasId;
    
    bool Exists<TEntity>(Expression<Func<TEntity, bool>> predicate) where TEntity : class;
    
    // Transaction management
    void SaveChanges();
    Task SaveChangesAsync(CancellationToken cancellationToken = default);
    void ClearChangeTracker();
    
    // Advanced operations
    Task RemoveAndDeleteItemsFromCollection<TEntity, TEnumerableItem>(
        TEntity entity, 
        Expression<Func<TEntity, ICollection<TEnumerableItem>>> propertyPath)
        where TEntity : ModelBase
        where TEnumerableItem : ModelBase;

    Task LoadPropertyAsync<TEntity, TProperty>(
        TEntity entity, 
        Expression<Func<TEntity, TProperty?>> getEnumerableToUpdate, 
        CancellationToken cancellationToken = default)
        where TEntity : class
        where TProperty : class;
}
```

**File:** `Benobix.Common.Infrastructure/Services/UnitOfWork.cs`
```csharp
namespace Benobix.Common.Infrastructure.Services;

public class UnitOfWork(BenobixDbContext dbContext, IAsyncMemoryCache cache) 
    : IUnitOfWork, IAsyncDisposable
{
    public BenobixDbContext DbContext { get => dbContext; }

    public IQueryable<TEntity> Set<TEntity>() where TEntity : class
    {
        return dbContext.Set<TEntity>();
    }

    public IQuery<TEntity> CreateQuery<TEntity>() where TEntity : class
    {
        var dbSet = dbContext.Set<TEntity>().AsNoTrackingWithIdentityResolution();
        return new Query<TEntity>(dbSet, false, cache);
    }

    public IQuery<TEntity> CreateQueryAsTracking<TEntity>() where TEntity : class
    {
        var dbSet = dbContext.Set<TEntity>().AsTracking();
        return new Query<TEntity>(dbSet, true, cache);
    }

    public void Add<TEntity>(TEntity entity) where TEntity : class, IHasId
    {
        Update(entity);  // Delegates to Update for smart tracking
    }

    public void Update<TEntity>(TEntity entity) where TEntity : class, IHasId
    {
        if (!IsEntityAlreadyTracked(entity))
        {
            dbContext.Update(entity);
        }
    }

    public void UpdateRange<TEntity>(IEnumerable<TEntity> entities) 
        where TEntity : class, IHasId
    {
        var untrackedEntities = GetUntrackedEntities(entities);
        if (untrackedEntities.Count > 0)
        {
            dbContext.UpdateRange(untrackedEntities);
        }
    }

    public async Task Delete<TEntity>(Guid entityId, CancellationToken cancellationToken = default) 
        where TEntity : class, IHasId
    {
        var entity = await CreateQuery<TEntity>()
            .SingleOrDefaultAsync(e => e.Id == entityId, cancellationToken);

        if (entity is not null)
        {
            dbContext.Remove(entity);
        }
    }

    public void Delete<TEntity>(TEntity entity) where TEntity : class, IHasId
    {
        dbContext.Remove(entity);
    }

    public bool Exists<TEntity>(Expression<Func<TEntity, bool>> predicate) 
        where TEntity : class
    {
        return dbContext.Set<TEntity>().Any(predicate);
    }

    public async Task SaveChangesAsync(CancellationToken cancellationToken = default)
    {
        await dbContext.SaveChangesAsync(cancellationToken);
    }
}
```

### Usage in Handlers

**Example: Query Handler**
```csharp
public class GetLoggedInPersonQueryHandler(
    UserManager<BenobixUser> userManager,
    IUnitOfWork unitOfWork
) : IRequestHandler<GetLoggedInPersonQuery, Person>
{
    public async Task<Person> Handle(
        GetLoggedInPersonQuery request, 
        CancellationToken cancellationToken)
    {
        var userId = userManager.GetUserId(request.Principal);

        // Direct LINQ query with UnitOfWork
        var user = await unitOfWork
            .CreateQuery<BenobixUser>()          // No tracking for better performance
            .Include(u => u.Person)               // EF Core navigation properties
            .ThenInclude(p => p.Settings)
            .FirstOrDefaultAsync(u => u.Id == userId, cancellationToken);

        return user?.Person ?? throw new UnauthorizedAccessException();
    }
}
```

**Example: Command Handler**
```csharp
public class UpdateUserRoleAssignmentsCommandHandler(IUnitOfWork unitOfWork) 
    : IRequestHandler<UpdateUserRoleAssignmentsCommand>
{
    public async Task Handle(
        UpdateUserRoleAssignmentsCommand request, 
        CancellationToken cancellationToken)
    {
        // 1. Query existing entities
        var existingUserRoleAssignments = await unitOfWork
            .CreateQuery<BenobixUserRole>()
            .Where(ur => ur.UserId == request.UserId)
            .ToListAsync(cancellationToken);

        // 2. Calculate what to remove
        var assignmentsToRemove = existingUserRoleAssignments
            .ExceptBy(request.UpdatedUserRoleAssignments.Select(ur => ur.RoleId), 
                ur => ur.RoleId);

        // 3. Apply changes
        unitOfWork.DeleteRange(assignmentsToRemove);
        unitOfWork.UpdateRange(request.UpdatedUserRoleAssignments);
        
        // SaveChanges automatically called by TransactionBehaviour pipeline
    }
}
```

### Why No Repository Pattern?

| Repository Pattern | Unit of Work Pattern |
|--------------------|----------------------|
| Abstraction over data access | Direct DbContext access |
| One repository per entity | Single UnitOfWork for all entities |
| Custom methods per entity | Generic LINQ queries |
| More code to maintain | Less boilerplate |
| Can hide EF Core features | Full access to EF Core |

**Rationale:**
- EF Core's `DbContext` already implements Unit of Work pattern
- `DbSet<T>` already implements Repository pattern
- Additional abstraction layers add complexity without value
- Direct LINQ access allows for optimized, ad-hoc queries

---

## MediatR Pipeline & Behaviors

### Pipeline Behaviors = Middleware for MediatR

Behaviors wrap handler execution like ASP.NET Core middleware:

```
Request → Behavior 1 → Behavior 2 → Handler → Behavior 2 → Behavior 1 → Response
```

### Transaction Behavior (Auto-Commit)

**File:** `Benobix.Common.Application/Behaviours/TransactionBehaviour.cs`
```csharp
namespace Benobix.Common.Application.Behaviours;

/// <summary>
/// Automatically wraps commands in database transactions
/// </summary>
public class TransactionBehaviour<TRequest, TResponse>(IUnitOfWork unitOfWork) 
    : IPipelineBehavior<TRequest, TResponse>
    where TRequest : IChangeDatabase  // Only applies to commands
{
    public async Task<TResponse> Handle(
        TRequest request, 
        RequestHandlerDelegate<TResponse> next, 
        CancellationToken cancellationToken)
    {
        // Start transaction
        await unitOfWork.BeginTransaction(cancellationToken);
        
        try
        {
            // Execute handler
            var response = await next();
            
            // Save changes
            await unitOfWork.SaveChangesAsync(cancellationToken);
            
            // Commit transaction
            await unitOfWork.CommitTransaction(cancellationToken);
            
            return response;
        }
        catch (Exception)
        {
            // Rollback on error
            await unitOfWork.RollbackTransaction(cancellationToken);
            throw;
        }
    }
}
```

**Marker Interface for Transactional Commands:**
```csharp
// Commands that modify database must implement this
public interface IChangeDatabase { }

// Base interfaces that inherit from IChangeDatabase
public interface IChangeDatabaseRequest : IRequest, IChangeDatabase { }
public interface IChangeDatabaseRequest<T> : IRequest<T>, IChangeDatabase { }

// Usage in your command
public record UpdateQualificationCommand(Qualification Qualification) 
    : IChangeDatabaseRequest;  // ← Automatically gets transaction
```

### Exception Handling Behavior

**File:** `Benobix.Common.Application/Behaviours/UnhandledExceptionBehaviour.cs`
```csharp
namespace Benobix.Common.Application.Behaviours;

/// <summary>
/// Global exception handler for all MediatR requests
/// </summary>
public class UnhandledExceptionBehaviour<TRequest, TResponse>(
    ILogger<TRequest> logger) 
    : IPipelineBehavior<TRequest, TResponse>
    where TRequest : IRequest<TResponse>
{
    public async Task<TResponse> Handle(
        TRequest request,
        RequestHandlerDelegate<TResponse> next,
        CancellationToken cancellationToken)
    {
        try
        {
            return await next();
        }
        catch (Exception ex)
        {
            var requestName = typeof(TRequest).Name;

            logger.LogError(ex, 
                "Benobix Request: Unhandled Exception for Request {Name} {@Request}", 
                requestName, request);

            throw;
        }
    }
}
```

### Performance Logging Behavior (Optional)

**File:** `Benobix.Common.Application/Behaviours/PerformanceLoggingBehaviour.cs`
```csharp
namespace Benobix.Common.Application.Behaviours;

/// <summary>
/// Logs execution time for slow requests
/// Enabled via configuration: AdditionalLogging:Performance = true
/// </summary>
public class PerformanceLoggingBehaviour<TRequest, TResponse>(
    ILogger<TRequest> logger) 
    : IPipelineBehavior<TRequest, TResponse>
    where TRequest : IRequest<TResponse>
{
    private readonly Stopwatch _timer = new();

    public async Task<TResponse> Handle(
        TRequest request,
        RequestHandlerDelegate<TResponse> next,
        CancellationToken cancellationToken)
    {
        _timer.Start();

        var response = await next();

        _timer.Stop();

        var elapsedMilliseconds = _timer.ElapsedMilliseconds;

        // Log if request took longer than 500ms
        if (elapsedMilliseconds > 500)
        {
            var requestName = typeof(TRequest).Name;

            logger.LogWarning(
                "Benobix Long Running Request: {Name} ({ElapsedMilliseconds} ms) {@Request}",
                requestName,
                elapsedMilliseconds,
                request);
        }

        return response;
    }
}
```

### Behavior Registration

```csharp
services.AddMediatR(cfg =>
{
    cfg.RegisterServicesFromAssemblies(assemblies);
    
    // Add common behaviors (executed in order)
    cfg.AddBehavior(typeof(IPipelineBehavior<,>), 
        typeof(UnhandledExceptionBehaviour<,>));
    cfg.AddBehavior(typeof(IPipelineBehavior<,>), 
        typeof(TransactionBehaviour<,>));
    cfg.AddBehavior(typeof(IPipelineBehavior<,>), 
        typeof(PerformanceLoggingBehaviour<,>));
});
```

### Execution Order

```
1. UnhandledExceptionBehaviour (outer try-catch)
   2. TransactionBehaviour (begin transaction)
      3. PerformanceLoggingBehaviour (start timer)
         4. YOUR HANDLER (business logic)
      4. PerformanceLoggingBehaviour (stop timer, log if slow)
   3. TransactionBehaviour (commit/rollback)
4. UnhandledExceptionBehaviour (catch, log, rethrow)
```

---

## Validation with FluentValidation

### Validator Example

**File:** `Benobix.Account.Application/Validators/UserValidator.cs`
```csharp
namespace Benobix.Account.Application.Validators;

public class UserValidator : AbstractValidator<Person>
{
    private ISender _mediatR;

    public UserValidator(ISender mediatR)
    {
        _mediatR = mediatR;

        // Simple validation rules
        RuleFor(p => p.FirstName)
            .NotEmpty()
            .WithMessage(AccountLocalization.NewUserValidatorFirstNameIsEmpty);

        RuleFor(p => p.LastName)
            .NotEmpty()
            .WithMessage(AccountLocalization.NewUserValidatorLastNameIsEmpty);

        RuleFor(p => p.Email)
            .NotEmpty()
            .WithMessage(AccountLocalization.NewUserValidatorEmailIsEmpty);

        // Async validation with database query
        RuleFor(p => p.Email)
            .MustAsync(async (value, cancellationToken) => 
                await IsEmailUniqueAsync(value!, cancellationToken))
            .WithMessage(AccountLocalization.NewUserValidatorUserWithEmailAlreadyExists)
            .When(p => !string.IsNullOrEmpty(p.Email));
    }

    private async Task<bool> IsEmailUniqueAsync(
        string email, 
        CancellationToken cancellationToken = default)
    {
        // Query via MediatR to check uniqueness
        return !await _mediatR.Send(
            new ExistsUserWithEmailQuery(email), cancellationToken);
    }
}
```

### Validation in Handler

```csharp
public class CreateUserAccountCommandHandler(
    IUnscopedSender mediatR, 
    IAccountService accountService) 
    : IRequestHandler<CreateUserAccountCommand, (bool Success, SendEmailResult EmailResult)>
{
    public async Task<(bool Success, SendEmailResult EmailResult)> Handle(
        CreateUserAccountCommand request, 
        CancellationToken cancellationToken)
    {
        // Validate before processing
        if (request.CreatePerson)
        {
            var validator = new UserValidator(mediatR);
            var validationResult = await validator.ValidateAsync(
                request.Person, cancellationToken);
            
            if (!validationResult.IsValid)
            {
                // Throws ValidationException with detailed errors
                throw new ValidationException(validationResult.Errors);
            }
        }

        return await accountService.CreateUserAccount(
            request.Email, request.Person, request.CreatePerson, cancellationToken);
    }
}
```

### Complex Validator with Dependencies

**File:** `Benobix.KnowHow.Application/Validators/QualificationValidator.cs`
```csharp
public class QualificationValidator : AbstractValidator<Qualification>
{
    public QualificationValidator()
    {
        RuleFor(q => q.Title)
            .NotEmpty()
            .WithMessage(KnowHowLocalization.QualificationValidatorTitleIsEmpty);

        RuleFor(q => q.Scale)
            .NotNull()
            .When(q => q.ScaleRequired)
            .WithMessage(KnowHowLocalization.QualificationValidatorScaleIsRequired);

        RuleFor(q => q.Scale)
            .Must(HaveAtLeastTwoScaleItems)
            .When(q => q.Scale != null)
            .WithMessage(KnowHowLocalization.QualificationValidatorScaleMustHaveAtLeastTwoItems);

        RuleFor(q => q.Scale)
            .Must(HaveUniqueScaleValues)
            .When(q => q.Scale?.ScaleItems?.Count > 0)
            .WithMessage(KnowHowLocalization.QualificationValidatorScaleValuesMustBeUnique);
    }

    private bool HaveAtLeastTwoScaleItems(Qualification qualification, Scale? scale)
    {
        return scale?.ScaleItems?.Count >= 2;
    }

    private bool HaveUniqueScaleValues(Qualification qualification, Scale? scale)
    {
        var values = scale?.ScaleItems.Select(si => si.Value).ToList();
        return values?.Count == values?.Distinct().Count();
    }
}
```

---

## Domain Models

### Base Entity

**File:** `Benobix.Common.Domain/ModelBase.cs`
```csharp
namespace Benobix.Common.Domain;

public interface IModelBase
{
    IModelBase CreateCopy();
    void CopyFrom(IModelBase source);
}

/// <summary>
/// Base entity for all domain models
/// Uses C# records for immutability and value-based equality
/// </summary>
public abstract record ModelBase<TId> : IModelBase, IHasId<TId>, ITimeMetaData
    where TId : struct
{
    [Required] public TId Id { get; set; }
    [Required] public DateTime CreatedAt { get; set; }
    [Required] public DateTime UpdatedAt { get; set; }

    /// <summary>
    /// Checks if object is new (not persisted yet)
    /// </summary>
    public virtual bool IsNewInstance()
    {
        return Id.Equals(default) 
               && CreatedAt == default
               && UpdatedAt == default;
    }

    /// <summary>
    /// Creates a shallow copy (references are shared)
    /// </summary>
    public virtual IModelBase CreateCopy() => this with { };

    /// <summary>
    /// Copies properties from another instance
    /// </summary>
    public virtual void CopyFrom(IModelBase source)
    {
        if (source.GetType() == GetType())
        {
            foreach (var property in GetType().GetProperties())
            {
                if (property.CanWrite)
                {
                    property.SetValue(this, property.GetValue(source));
                }
            }
        }
    }
}

// Default: Guid-based ID
public abstract record ModelBase : ModelBase<Guid>;
```

### Simple Entity Example

**File:** `Benobix.Common.Domain/Person.cs`
```csharp
namespace Benobix.Common.Domain;

public record Person : ModelBase
{
    [Required] public string FirstName { get; set; } = null!;
    [Required] public string LastName { get; set; } = null!;
    public string? Email { get; set; }
    public string? Initials { get; set; }
    public bool HasPicture { get; set; }
    public bool? Archived { get; set; }
    public PersonSettings Settings { get; set; } = new();
    
    // Computed properties
    public string GetFullName() => $"{FirstName} {LastName}";
    public string GetMailAddress() => Email ?? "";
}
```

### Entity with Identity

**File:** `Benobix.Account.Domain/BenobixUser.cs`
```csharp
namespace Benobix.Account.Domain;

/// <summary>
/// Extends ASP.NET Core Identity User
/// </summary>
public class BenobixUser : IdentityUser
{
    public Guid PersonId { get; set; }
    [Required] public Person Person { get; set; } = null!;
    public bool MustSetNewPassword { get; set; }
    public bool UserActive { get; set; } = true;
}
```

### Complex Entity with Navigation Properties

**File:** `Benobix.Organization.Domain/Position.cs`
```csharp
namespace Benobix.Organization.Domain;

public record Position : ArchivableModelBase
{
    // Primitive properties
    [Required] public string Title { get; set; } = null!;
    public string? Description { get; set; }
    [Required] public int Workload { get; set; }
    
    // Foreign keys
    public Guid? DepartmentId { get; set; }
    public Guid? SubjectAreaId { get; set; }
    public Guid? SupervisorDepartmentId { get; set; }
    public Guid? SupervisorSubjectAreaId { get; set; }
    public Guid? DeputyId { get; set; }
    
    // Navigation properties (EF Core)
    public Department? Department { get; set; }
    public SubjectArea? SubjectArea { get; set; }
    public Position? SupervisorDepartment { get; set; }
    public Position? SupervisorSubjectArea { get; set; }
    public Position? Deputy { get; set; }
    
    // Collections
    public List<PositionLocationAssignment> LocationAssignments { get; set; } = [];
    public List<PositionPersonAssignment> PersonAssignments { get; set; } = [];
    public List<PositionRoleProfileAssignment> RoleProfileAssignments { get; set; } = [];

    // Override HashCode for circular reference handling
    public override int GetHashCode() => HashCode.Combine(
        HashCode.Combine(
            base.GetHashCode(),
            Title,
            Description,
            Workload,
            DepartmentId,
            SubjectAreaId,
            SupervisorDepartmentId,
            SupervisorSubjectAreaId),
        DeputyId,
        LocationAssignments,
        PersonAssignments,
        RoleProfileAssignments);

    public virtual bool Equals(Position? other)
    {
        return base.Equals(other)
            && Title == other.Title
            && Description == other.Description
            && Workload == other.Workload
            && DepartmentId == other.DepartmentId
            && LocationAssignments.SequenceEqual(other.LocationAssignments)
            && PersonAssignments.SequenceEqual(other.PersonAssignments);
    }
}
```

### Entity with Self-Referencing (Tree Structure)

**File:** `Benobix.Organization.Domain/Department.cs`
```csharp
namespace Benobix.Organization.Domain;

/// <summary>
/// Department with hierarchical parent-child relationship
/// </summary>
public record Department : ArchivableModelBase, ITreeItem<Department>
{
    public bool StaffFunction { get; set; }
    [Required] public string Name { get; set; } = null!;
    
    // Self-referencing hierarchy
    public Guid? ParentId { get; set; }
    public Department? Parent { get; set; }
    public List<Department> Children { get; set; } = [];
    
    public int Level { get; set; } = 1;
    public bool Highlight => StaffFunction;

    public Guid? TemplateDashboardId { get; set; }
    public TemplateDashboard? TemplateDashboard { get; set; }

    /// <summary>
    /// Domain logic: Recalculate level based on hierarchy
    /// </summary>
    public void UpdateLevel()
    {
        Level = Parent?.Level + 1 ?? 1;
        
        // Recursively update children
        foreach (var child in Children)
        {
            child.UpdateLevel();
        }
    }
}
```

---

## Architecture Comparison

### Complete Flow Diagram

**Traditional .NET Core Web API:**
```
┌─────────────┐
│   Angular   │ (TypeScript)
│  Component  │
└──────┬──────┘
       │ HTTP POST /api/users
       │ JSON: { email: "...", firstName: "..." }
       ▼
┌──────────────────┐
│   API Gateway    │ (CORS, Auth, Rate Limiting)
└──────┬───────────┘
       ▼
┌──────────────────┐
│  UsersController │ (C#)
│  [HttpPost]      │
└──────┬───────────┘
       │ userService.CreateUser(dto)
       ▼
┌──────────────────┐
│   IUserService   │ (C#)
│   UserService    │
└──────┬───────────┘
       │ userRepo.Add(user)
       ▼
┌──────────────────┐
│ IUserRepository  │ (C#)
│  UserRepository  │
└──────┬───────────┘
       │ DbContext.Users.Add()
       ▼
┌──────────────────┐
│  EF Core Context │ (C#)
│    SaveChanges   │
└──────┬───────────┘
       │ SQL INSERT
       ▼
┌──────────────────┐
│   SQL Database   │
└──────────────────┘
```

**This Application (Blazor + CQRS):**
```
┌─────────────────┐
│ Blazor Component│ (C# Razor)
│  SettingsUsers  │
│  Page.razor.cs  │
└──────┬──────────┘
       │ MediatR.Send(new CreateUserAccountCommand(...))
       │ In-process method call (no HTTP!)
       ▼
┌─────────────────────────────────────────────┐
│         MediatR Pipeline (Behaviors)        │
│  1. UnhandledExceptionBehaviour             │
│  2. TransactionBehaviour (BeginTransaction) │
│  3. PerformanceLoggingBehaviour             │
└──────┬──────────────────────────────────────┘
       ▼
┌─────────────────┐
│ Command Handler │ (C#)
│ CreateUserAcc...│
│ CommandHandler  │
└──────┬──────────┘
       │ FluentValidation
       │ accountService.CreateUserAccount()
       ▼
┌─────────────────┐
│ IAccountService │ (C#)
│ AccountService  │ (if complex logic)
└──────┬──────────┘
       │ OR direct:
       │ unitOfWork.Add(user)
       ▼
┌─────────────────┐
│  IUnitOfWork    │ (C#)
│   UnitOfWork    │
└──────┬──────────┘
       │ dbContext.Users.Add()
       ▼
┌─────────────────┐
│ BenobixDbContext│ (EF Core)
└──────┬──────────┘
       │ SQL INSERT
       ▼
┌─────────────────┐
│PostgreSQL (DB)  │
└─────────────────┘
       │
       ▼ (Back through pipeline)
┌─────────────────┐
│TransactionBeh...|
│ SaveChanges()   │
│ CommitTransaction│
└──────┬──────────┘
       │ Response
       ▼
 Return to Blazor Component
```

### Trade-offs

#### **Pros of Blazor + CQRS:**
- ✅ **Performance:** No HTTP serialization overhead
- ✅ **Type Safety:** Full C# type system across entire stack
- ✅ **Code Reuse:** Share models, validators, services between UI and logic
- ✅ **Simplified Deployment:** Single application, no CORS issues
- ✅ **Fine-grained Handlers:** Each operation isolated for testing
- ✅ **Automatic Transactions:** Via MediatR behaviors
- ✅ **Clean Separation:** CQRS separates reads from writes

#### **Cons:**
- ❌ **Cannot scale independently:** Frontend and backend are coupled
- ❌ **Single technology stack:** Must use .NET for everything
- ❌ **Not suitable for mobile apps:** Would need separate API layer
- ❌ **Learning curve:** Different from traditional Web API
- ❌ **More classes:** One handler per operation (vs one service for many)

---

## Common Patterns

### 1. Command Query Separation

**Commands** (write):
```csharp
public record CreateUserCommand(string Email, string Name) 
    : IChangeDatabaseRequest<Guid>;  // Returns user ID
```

**Queries** (read):
```csharp
public record GetUserQuery(Guid UserId) 
    : IRequest<UserDto>;  // Returns DTO
```

### 2. Handler with Nested MediatR Call

```csharp
public class CreateOrderCommandHandler(IUnscopedSender mediatR) 
    : IRequestHandler<CreateOrderCommand, Order>
{
    public async Task<Order> Handle(
        CreateOrderCommand request, 
        CancellationToken cancellationToken)
    {
        // Nested query to check if customer exists
        var customerExists = await mediatR.Send(
            new CustomerExistsQuery(request.CustomerId), 
            cancellationToken);
            
        if (!customerExists)
            throw new ValidationException("Customer not found");
            
        // Create order...
    }
}
```

### 3. Optimistic Concurrency with Version Tracking

```csharp
public async Task Handle(
    UpdateEntityCommand request, 
    CancellationToken cancellationToken)
{
    // Load existing
    var existing = await unitOfWork
        .CreateQuery<Entity>()
        .SingleAsync(e => e.Id == request.Id, cancellationToken);
    
    // Create historical version
    var history = existing with 
    { 
        Id = Guid.Empty, 
        IsLastVersion = false 
    };
    unitOfWork.Add(history);
    
    // Update current
    existing.SomeProperty = request.NewValue;
    existing.IsLastVersion = true;
    unitOfWork.Update(existing);
}
```

### 4. Pagination Pattern

```csharp
public record GetPaginatedUsersQuery(int PageIndex, int PageSize) 
    : IRequest<IPaginatedList<UserDto>>;

public class GetPaginatedUsersQueryHandler(IUnitOfWork unitOfWork) 
    : IRequestHandler<GetPaginatedUsersQuery, IPaginatedList<UserDto>>
{
    public async Task<IPaginatedList<UserDto>> Handle(
        GetPaginatedUsersQuery request, 
        CancellationToken cancellationToken)
    {
        return await unitOfWork
            .CreateQuery<BenobixUser>()
            .Include(u => u.Person)
            .Select(u => new UserDto 
            { 
                Id = u.Id, 
                Email = u.Email,
                Name = u.Person.GetFullName()
            })
            .ToPaginatedListAsync(request.PageIndex, request.PageSize, cancellationToken);
    }
}
```

### 5. Caching Query Results

```csharp
public class GetSettingsQueryHandler(
    IUnitOfWork unitOfWork, 
    IAsyncMemoryCache cache) 
    : IRequestHandler<GetSettingsQuery, Settings>
{
    public async Task<Settings> Handle(
        GetSettingsQuery request, 
        CancellationToken cancellationToken)
    {
        var cacheKey = $"Settings_{request.SettingsType}";
        
        return await cache.GetOrAddAsync(
            cacheKey,
            async () => await unitOfWork
                .CreateQuery<Settings>()
                .FirstOrDefaultAsync(s => s.Type == request.SettingsType, cancellationToken),
            TimeSpan.FromMinutes(10));
    }
}
```

---

## Summary for .NET Core Web API Developers

### What's Different?
- **No Controllers** for main app (only for external API)
- **No Repository Pattern** - direct UnitOfWork/DbContext access
- **CQRS** - separate Commands (write) and Queries (read)
- **MediatR** - in-process messaging instead of HTTP
- **Blazor Server** - C# instead of TypeScript/Angular
- **Automatic Transactions** - via pipeline behaviors

### What's Similar?
- **Dependency Injection** - same pattern, module-based
- **EF Core** - same ORM, LINQ queries
- **ASP.NET Core Identity** - same authentication
- **FluentValidation** - same validation library
- **Clean Architecture** - same layering principles

### Mental Model Translation

| .NET Web API | This Application |
|--------------|------------------|
| `Controller` | Blazor Component |
| `IUserService.CreateUser()` | `CreateUserCommand` + Handler |
| `IUserRepository.GetById()` | `unitOfWork.CreateQuery<User>()` |
| `[HttpPost]` | `MediatR.Send(command)` |
| `return Ok(dto)` | `return dto` (no HTTP layer) |
| `services.AddScoped<IUserService, UserService>()` | `services.AddMediatR(assembly)` |

### Recommended Learning Path
1. ✅ Understand **MediatR** basics (IRequest, IRequestHandler)
2. ✅ Learn **CQRS** principles (Command vs Query)
3. ✅ Study **Unit of Work** pattern (no Repository)
4. ✅ Review **MediatR Behaviors** (pipeline middleware)
5. ✅ Explore **Blazor** components (if unfamiliar)
6. ✅ Read existing handlers in codebase as examples

---

## Quick Reference

### Creating a New Command

1. **Define Command (Interface layer):**
```csharp
// Benobix.YourModule.Application.Interface/Commands/YourCommand.cs
public record YourCommand(string Data) : IChangeDatabaseRequest<Guid>;
```

2. **Create Handler (Application layer):**
```csharp
// Benobix.YourModule.Application/Commands/YourCommand.cs
public class YourCommandHandler(IUnitOfWork unitOfWork) 
    : IRequestHandler<YourCommand, Guid>
{
    public async Task<Guid> Handle(
        YourCommand request, 
        CancellationToken cancellationToken)
    {
        // Your logic here
        var entity = new YourEntity { Data = request.Data };
        unitOfWork.Add(entity);
        // SaveChanges called automatically by TransactionBehaviour
        return entity.Id;
    }
}
```

3. **Call from Blazor:**
```csharp
var result = await MediatR.Send(new YourCommand("data"));
```

### Creating a New Query

1. **Define Query:**
```csharp
public record GetYourEntityQuery(Guid Id) : IRequest<YourEntity>;
```

2. **Create Handler:**
```csharp
public class GetYourEntityQueryHandler(IUnitOfWork unitOfWork) 
    : IRequestHandler<GetYourEntityQuery, YourEntity>
{
    public async Task<YourEntity> Handle(
        GetYourEntityQuery request, 
        CancellationToken cancellationToken)
    {
        return await unitOfWork
            .CreateQuery<YourEntity>()
            .FirstOrDefaultAsync(e => e.Id == request.Id, cancellationToken)
            ?? throw new NotFoundException();
    }
}
```

---

**Next Steps:** Review existing handlers in the codebase to see these patterns in action!
