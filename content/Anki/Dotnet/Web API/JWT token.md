STARTanki
Basic

 What are the three parts of a JWT?

Back:
A JWT consists of three parts separated by dots:

1. Header
2. Payload
3. Signature

```text
Header.Payload.Signature
```
<!--ID: 1783329693807-->
ENDanki

STARTanki
Basic

 What is stored in the JWT Header?

Back:
The Header contains metadata about the token.

Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

- `alg` → Signing algorithm
- `typ` → Token type (JWT)
<!--ID: 1783329693813-->
ENDanki

STARTanki
Basic

 What is stored in the JWT Payload?

Back:
The Payload contains **claims** about the user or token.

Example:

```json
{
  "sub": "123",
  "name": "Nikhil",
  "email": "nikhil@example.com",
  "role": "Admin"
}
```
<!--ID: 1783329693817-->
ENDanki

STARTanki
Basic

 What is the purpose of the JWT Signature?

Back:
The Signature ensures the token has **not been tampered with**.

It is generated from:
- Header
- Payload
- Secret key (HS256) or Private key (RS256)
<!--ID: 1783329693821-->
ENDanki

STARTanki
Basic

 What are JWT claims?

Back:
Claims are pieces of information stored in the JWT Payload.

Examples:
- User ID
- Username
- Email
- Role
- Expiration time
<!--ID: 1783329693823-->
ENDanki

STARTanki
Basic

 What are the common registered JWT claims?

Back:
| Claim | Purpose |
|-------|---------|
| sub | Subject (User ID) |
| name | User name |
| email | Email |
| role | User role |
| iss | Issuer |
| aud | Audience |
| exp | Expiration time |
| nbf | Not valid before |
| iat | Issued at |
| jti | Unique token ID |
<!--ID: 1783329693826-->
ENDanki

STARTanki
Basic
Can a JWT contain custom claims?

Back:
Yes.

Example:

```json
{
  "EmployeeId": "101",
  "Department": "IT",
  "Permission": "CanApprove"
}
```

Applications can add any custom claims they need.
<!--ID: 1783329693829-->
ENDanki

STARTanki
Basic

How do you add claims when creating a JWT in ASP.NET Core?

Back:

```csharp
var claims = new[]
{
    new Claim(JwtRegisteredClaimNames.Sub, user.Id.ToString()),
    new Claim(ClaimTypes.Email, user.Email),
    new Claim(ClaimTypes.Name, user.Name),
    new Claim(ClaimTypes.Role, "Admin")
};
```
<!--ID: 1783329693833-->
ENDanki

STARTanki
Basic

 How do you create a JWT in ASP.NET Core?

Back:

```csharp
var token = new JwtSecurityToken(
    issuer: "MyApi",
    audience: "MyClient",
    claims: claims,
    expires: DateTime.UtcNow.AddHours(1),
    signingCredentials: credentials
);

string jwt = new JwtSecurityTokenHandler().WriteToken(token);
```
<!--ID: 1783329693837-->
ENDanki

STARTanki
Basic

How do you read JWT claims inside an ASP.NET Core controller?

Back:

```csharp
string? email =
    User.FindFirst(ClaimTypes.Email)?.Value;

string? role =
    User.FindFirst(ClaimTypes.Role)?.Value;
```
<!--ID: 1783329693839-->
ENDanki

STARTanki
Basic

How do you enumerate all JWT claims in ASP.NET Core?

Back:

```cs
foreach (var claim in User.Claims)
{
    Console.WriteLine($"{claim.Type}: {claim.Value}");
}
```
<!--ID: 1783329693842-->
ENDanki

STARTanki
Basic

Is a JWT encrypted?

Back:
No.

A JWT is **Base64Url encoded**, not encrypted.

Anyone can decode the Header and Payload.

Only the Signature protects against tampering.
<!--ID: 1783329693845-->
ENDanki

STARTanki
Basic

What information should NOT be stored in a JWT?

Back:
Never store sensitive information such as:

- Passwords
- Credit card numbers
- OTPs
- Secret keys
- Refresh tokens

JWTs can be easily decoded.
<!--ID: 1783329693847-->
ENDanki

STARTanki
Basic

 What is the purpose of the `iss` claim in a JWT?

Back:
`iss` (Issuer) identifies the server or application that issued the JWT.

Example:

```json
{
  "iss": "MyApi"
}
```
<!--ID: 1783329693849-->
ENDanki

STARTanki
Basic

 What is the purpose of the `aud` claim in a JWT?

Back:
`aud` (Audience) identifies the intended recipient of the JWT.

Example:

```json
{
  "aud": "MyAngularApp"
}
```
<!--ID: 1783329693850-->
ENDanki

STARTanki
Basic

 What is the purpose of the `exp` claim in a JWT?

Back:
`exp` specifies when the token expires.

After this time, the token is considered invalid.

Example:

```json
{
  "exp": 1751900000
}
```
<!--ID: 1783329693852-->
ENDanki

STARTanki
Basic

 What is the purpose of the `sub` claim in a JWT?

Back:
`sub` (Subject) uniquely identifies the user or entity the token represents.

Example:

```json
{
  "sub": "123"
}
```
<!--ID: 1783329693854-->
ENDanki

STARTanki
Basic

 What is the purpose of the `jti` claim in a JWT?

Back:
`jti` (JWT ID) uniquely identifies a token.

It is commonly used to:
- Prevent replay attacks
- Revoke specific tokens
- Track issued tokens
<!--ID: 1783329693856-->
ENDanki

STARTanki
Basic

 Why does ASP.NET Core populate `User.Claims`?

Back:
After successful JWT validation, ASP.NET Core extracts the claims from the token and populates the authenticated user's `ClaimsPrincipal`.

This allows access to claims like:

```csharp
User.Identity?.Name
User.Claims
User.FindFirst(ClaimTypes.Role)
```
<!--ID: 1783329693857-->
ENDanki

STARTanki
Basic

 Interview answer: Explain the contents of a JWT.

Back:
A JWT consists of three parts:

1. **Header** – contains the signing algorithm and token type.
2. **Payload** – contains claims such as user ID, email, roles, issuer, audience, and expiration.
3. **Signature** – verifies the integrity of the token and ensures it hasn't been modified.

ASP.NET Core validates the signature and exposes the claims through `User.Claims`.
<!--ID: 1783329693859-->
ENDanki