# Blazor UI Development Guide for Angular Developers

> A comprehensive guide to understanding Blazor UI development in the Benobix project for developers transitioning from Angular development.

## Table of Contents
- [Introduction](#introduction)
- [What is MudBlazor?](#what-is-mudblazor)
- [Quick Comparison: Angular vs Blazor](#quick-comparison-angular-vs-blazor)
- [Component Structure](#component-structure)
- [Data Binding](#data-binding)
- [Component Communication](#component-communication)
- [Forms and Validation](#forms-and-validation)
- [Routing and Navigation](#routing-and-navigation)
- [Lifecycle Hooks](#lifecycle-hooks)
- [Dependency Injection](#dependency-injection)
- [State Management](#state-management)
- [Dialogs and Modals](#dialogs-and-modals)
- [Tables and Data Grids](#tables-and-data-grids)
- [Layout and Responsive Design](#layout-and-responsive-design)
- [Authorization and Security](#authorization-and-security)
- [Common MudBlazor Components](#common-mudblazor-components)
- [Best Practices](#best-practices)

---

## Introduction

Blazor is a .NET web framework that lets you build interactive web UIs using C# instead of JavaScript. This project uses **Blazor Server**, which means:
- Your component logic runs on the server
- UI updates are sent to the browser via SignalR
- Think of it like Angular Universal, but real-time

---

## What is MudBlazor?

**MudBlazor** is the Material Design component library for Blazor - think of it as **Angular Material** for Blazor.

When you see components like:
```razor
<MudButton>
<MudTextField>
<MudAppBar>
<MudTable>
```

These are all from the MudBlazor library, similar to how you'd use:
```html
<!-- Angular Material -->
<mat-button>
<mat-form-field>
<mat-toolbar>
<mat-table>
```

**Key Difference**: In Blazor, you compose components directly in markup with PascalCase naming, not kebab-case.

---

## Quick Comparison: Angular vs Blazor

| Feature | Angular | Blazor |
|---------|---------|--------|
| **Components** | `*.component.ts` + `*.component.html` | `*.razor` + `*.razor.cs` (optional) |
| **Template Syntax** | `{{ value }}` | `@value` |
| **Input Properties** | `@Input() name: string` | `[Parameter] public string Name { get; set; }` |
| **Output Events** | `@Output() clicked = new EventEmitter()` | `[Parameter] public EventCallback OnClick { get; set; }` |
| **Two-way Binding** | `[(ngModel)]="name"` | `@bind-Value="Name"` |
| **Event Binding** | `(click)="onClick()"` | `@onclick="OnClick"` |
| **Structural Directives** | `*ngIf`, `*ngFor` | `@if`, `@foreach` |
| **Services** | Injected via constructor | `[Inject] public IService Service { get; set; }` |
| **Lifecycle Hooks** | `ngOnInit()` | `OnInitializedAsync()` |
| **Routing** | `RouterModule.forRoot()` | `@attribute [Route("/path")]` |
| **HTTP Calls** | `HttpClient` | `HttpClient` (same!) |
| **Material Library** | Angular Material | MudBlazor |

---

## Component Structure

### Basic Component (without code-behind)

**Angular:**
```typescript
// person-card.component.ts
@Component({
  selector: 'app-person-card',
  templateUrl: './person-card.component.html'
})
export class PersonCardComponent {
  @Input() person: Person;
  
  showDetails() {
    console.log(this.person);
  }
}
```

**Blazor Equivalent:**
```razor
@* PersonCard.razor *@

<MudCard>
  <MudCardContent>
    <MudText>@Person.FirstName @Person.LastName</MudText>
    <MudButton OnClick="ShowDetails">Show Details</MudButton>
  </MudCardContent>
</MudCard>

@code {
    [Parameter] public Person Person { get; set; } = null!;
    
    private void ShowDetails()
    {
        Console.WriteLine(Person);
    }
}
```

### Component with Code-Behind (Recommended for Complex Components)

**Blazor:**
```razor
@* PersonCard.razor *@
@inherits BenobixComponentBase

<MudCard>
  <MudCardContent>
    <MudText>@Person.FirstName @Person.LastName</MudText>
    <MudButton OnClick="ShowDetails">Show Details</MudButton>
  </MudCardContent>
</MudCard>
```

```csharp
// PersonCard.razor.cs
namespace Benobix.Personnel.Presentation.Components;

public partial class PersonCard : BenobixComponentBase
{
    [Parameter] public Person Person { get; set; } = null!;
    
    [Inject] private ILogger<PersonCard> Logger { get; set; } = null!;
    
    private void ShowDetails()
    {
        Logger.LogInformation("Showing details for {PersonName}", Person.GetFullName());
    }
}
```

**Key Points:**
- The class name must match the file name
- Use `partial class` keyword
- No need to repeat the markup in the `.cs` file

---

## Data Binding

### One-Way Binding

**Angular:**
```html
<input [value]="username" />
<div>{{ username }}</div>
```

**Blazor:**
```razor
<MudTextField Value="@Username" />
<MudText>@Username</MudText>
```

### Two-Way Binding

**Angular:**
```html
<input [(ngModel)]="username" />
```

**Blazor:**
```razor
<MudTextField @bind-Value="Username" />
```

### Two-Way Binding with Change Detection

**Angular:**
```html
<input [(ngModel)]="username" (ngModelChange)="onUsernameChanged($event)" />
```

**Blazor:**
```razor
<MudTextField @bind-Value="Username" 
              @bind-Value:after="OnUsernameChanged" />

@code {
    private string Username { get; set; } = "";
    
    private void OnUsernameChanged()
    {
        // Called after Username is updated
        Console.WriteLine($"Username changed to: {Username}");
    }
}
```

### Event Binding

**Angular:**
```html
<button (click)="save()">Save</button>
<input (keyup)="onKeyUp($event)" />
```

**Blazor:**
```razor
<MudButton OnClick="Save">Save</MudButton>
<MudTextField @onkeyup="OnKeyUp" />

@code {
    private void Save()
    {
        // Save logic
    }
    
    private void OnKeyUp(KeyboardEventArgs e)
    {
        if (e.Key == "Enter")
        {
            Save();
        }
    }
}
```

### Real Example from Codebase

From `InboundApiConnectionAddEditForm.razor`:
```razor
@* Simple two-way binding *@
<MudCheckBox @bind-Value="@InboundApiConnection.Active"
             For="@(() => InboundApiConnection.Active)"
             Label="@InboundApiLocalization.FieldConnectionActiveLabel" />

@* Two-way binding with post-change action *@
<BenobixSelect T="@(Domain.InboundApi)"
               For="@(() => InboundApiConnection.InboundApi)"
               @bind-Value="@InboundApiConnection.InboundApi"
               @bind-Value:after="() => InboundApiChanged()"
               Label="@InboundApiLocalization.FieldApiLabel"
               ToStringFunc="inboundApi => inboundApi?.Name"
               Clearable="false">
    @foreach (var inboundApi in _inboundApis)
    {
        <MudSelectItem T="@(Domain.InboundApi)" Value="@inboundApi">
            @(inboundApi.Name)
        </MudSelectItem>
    }
</BenobixSelect>
```

---

## Component Communication

### Parent to Child (Props/Input)

**Angular:**
```typescript
// Child
@Input() title: string;
```
```html
<!-- Parent -->
<app-child [title]="pageTitle"></app-child>
```

**Blazor:**
```csharp
// Child
[Parameter] public string Title { get; set; } = "";
```
```razor
<!-- Parent -->
<ChildComponent Title="@PageTitle" />
```

### Child to Parent (Events/Output)

**Angular:**
```typescript
// Child
@Output() saved = new EventEmitter<Person>();

save() {
  this.saved.emit(this.person);
}
```
```html
<!-- Parent -->
<app-child (saved)="onPersonSaved($event)"></app-child>
```

**Blazor:**
```csharp
// Child Component
[Parameter] public EventCallback<Person> OnSaved { get; set; }

private async Task Save()
{
    await OnSaved.InvokeAsync(Person);
}
```
```razor
<!-- Parent -->
<ChildComponent OnSaved="@HandlePersonSaved" />

@code {
    private async Task HandlePersonSaved(Person person)
    {
        // Handle the saved person
        await SaveToDatabase(person);
    }
}
```

### Real Example - Form Submission

From `BenobixForm.razor.cs`:
```csharp
public partial class BenobixForm : MudForm
{
    [Parameter] public EventCallback OnSubmit { get; set; }
    [Parameter] public EventCallback OnValidSubmit { get; set; }
    [Parameter] public EventCallback OnCanceled { get; set; }
    
    private async Task Submit()
    {
        if (OnSubmit.HasDelegate)
        {
            await OnSubmit.InvokeAsync();
            return;
        }

        if (Validator is not null)
        {
            await Validate();
        }

        if (IsValid || Validator is null)
        {
            await OnValidSubmit.InvokeAsync();
        }
    }
}
```

Usage:
```razor
<BenobixForm Model="@Person" 
             Validator="_validator"
             OnValidSubmit="SavePerson"
             OnCanceled="Cancel">
    <!-- Form fields -->
</BenobixForm>
```

### Cascading Parameters (Similar to Provider/Context in Angular)

**Angular (with Services):**
```typescript
// In parent component
providers: [CurrentUserService]

// In child component
constructor(private currentUser: CurrentUserService) {}
```

**Blazor:**
```razor
@* Parent/Layout *@
<CascadingValue Value="LoggedInPerson" Name="LoggedInPerson">
    <CascadingValue Value="CurrentPrincipal" Name="CurrentPrincipal">
        @Body
    </CascadingValue>
</CascadingValue>
```

```csharp
// Any child component can receive it
[CascadingParameter(Name = "LoggedInPerson")] 
protected Person? LoggedInPerson { get; set; }

[CascadingParameter(Name = "CurrentPrincipal")] 
protected ClaimsPrincipal CurrentPrincipal { get; set; } = null!;
```

This is implemented in `MainLayoutBase.razor` and consumed by `BenobixComponentBase.cs`.

---

## Forms and Validation

### Form Structure

**Angular (Reactive Forms):**
```typescript
// Component
form = this.fb.group({
  firstName: ['', Validators.required],
  email: ['', [Validators.required, Validators.email]]
});

submit() {
  if (this.form.valid) {
    this.save(this.form.value);
  }
}
```
```html
<form [formGroup]="form" (ngSubmit)="submit()">
  <mat-form-field>
    <input matInput formControlName="firstName">
    <mat-error *ngIf="form.get('firstName').hasError('required')">
      Required
    </mat-error>
  </mat-form-field>
</form>
```

**Blazor (with FluentValidation):**
```csharp
// Validator (separate class)
public class PersonValidator : AbstractValidator<Person>
{
    public PersonValidator()
    {
        RuleFor(x => x.FirstName).NotEmpty();
        RuleFor(x => x.Email).NotEmpty().EmailAddress();
    }
}
```

```razor
@* Component *@
<BenobixForm Model="@Person" 
             Validator="_personValidator"
             OnValidSubmit="Submit">
    <MudGrid>
        <MudItem xs="12">
            <MudTextField @bind-Value="@Person.FirstName" 
                         For="@(() => Person.FirstName)"
                         Label="First Name" />
        </MudItem>
        <MudItem xs="12">
            <MudTextField @bind-Value="@Person.Email" 
                         For="@(() => Person.Email)"
                         Label="Email" />
        </MudItem>
    </MudGrid>
</BenobixForm>

@code {
    private Person Person { get; set; } = new();
    private PersonValidator _personValidator = new();
    
    private async Task Submit()
    {
        await SavePerson(Person);
    }
}
```

### Real Example - Role Add/Edit Dialog

From `RoleAddEditDialog.razor`:
```razor
<MudDialog Class="p-3">
    <TitleContent>
        <MudText Typo="Typo.h2">@MudDialog.Title</MudText>
    </TitleContent>
    <DialogContent>
        <BenobixForm Model="Role" 
                     ShowButtons="true"
                     Validator="_validator"
                     SubmitButtonText="@ApplyButtonText"
                     CancelButtonText="@CancelButtonText"
                     OnValidSubmit="Apply"
                     OnCanceled="Cancel"
                     @ref="_formRef">
            <MudGrid xs="12" Spacing="3">
                <MudItem xs="12">
                    <MudTextField Label="@AccountLocalization.AddEditRoleDialogRoleNameLabel" 
                                 @bind-Value="@Role.Name" 
                                 Placeholder="@AccountLocalization.RoleName" 
                                 For="@(() => Role.Name)" />
                </MudItem>
            </MudGrid>
        </BenobixForm>
    </DialogContent>
</MudDialog>
```

```csharp
public partial class RoleAddEditDialog : BenobixComponentBase
{
    private BenobixRoleValidator _validator = new();
    private BenobixForm _formRef = null!;
    
    [Parameter] public required BenobixRole Role { get; set; } = null!;
    [Parameter] public required string ApplyButtonText { get; set; } = null!;
    [CascadingParameter] private IMudDialogInstance MudDialog { get; set; } = null!;

    private void Apply()
    {
        if (_formRef.IsValid)
        {
            MudDialog.Close(DialogResult.Ok(Role));
        }
    }

    private void Cancel()
    {
        MudDialog.Cancel();
    }
}
```

**Key Differences:**
- Blazor uses FluentValidation instead of Angular's built-in validators
- `For` parameter connects the field to the validation context
- Validation errors are automatically displayed by MudBlazor components
- `BenobixForm` is a custom wrapper around `MudForm` with extra features

---

## Routing and Navigation

### Basic Routing

**Angular:**
```typescript
const routes: Routes = [
  { path: 'users', component: UsersComponent },
  { path: 'users/:id', component: UserDetailsComponent }
];
```

**Blazor:**
```razor
@* UsersPage.razor *@
@attribute [Route("/users")]

<h1>Users Page</h1>

@code {
    // Component code
}
```

```razor
@* UserDetailsPage.razor *@
@attribute [Route("/users/{UserId}")]

<h1>User Details: @UserId</h1>

@code {
    [Parameter] public Guid UserId { get; set; }
}
```

### Multiple Routes for Same Component

**Blazor:**
```razor
@attribute [Route("/reviews/new")]
@attribute [Route("/reviews/edit/{ReviewId}")]

@code {
    [Parameter] public Guid? ReviewId { get; set; }
    
    protected override async Task OnParametersSetAsync()
    {
        if (ReviewId.HasValue)
        {
            // Edit mode
            Review = await LoadReview(ReviewId.Value);
        }
        else
        {
            // Create mode
            Review = new Review();
        }
    }
}
```

### Real Example - Person Details

From `PersonDetails.razor`:
```razor
@attribute [Route(Routes.PersonDetailsTab)]
@attribute [Route(Routes.PersonDetailsForRegistryTab)]

@code {
    private const string PersonDetailsTab = "/personnel/{PersonId}/details";
    private const string PersonDetailsForRegistryTab = "/personnel/{PersonId}/details/registry/{RegistryId}";
    
    [Parameter] public Guid PersonId { get; set; }
    [Parameter] public Guid? RegistryId { get; set; }
}
```

### Navigation

**Angular:**
```typescript
// In component
constructor(private router: Router) {}

goToUser(id: string) {
  this.router.navigate(['/users', id]);
}
```

**Blazor:**
```csharp
[Inject] private NavigationManager Navigation { get; set; } = null!;

private void GoToUser(Guid id)
{
    Navigation.NavigateTo($"/users/{id}");
}
```

Or using links:
```razor
<MudButton Href="@($"/users/{userId}")">View User</MudButton>
```

### Route Constants

This project uses a nice pattern with route constants:

```csharp
// Routes.cs
public static class Routes
{
    public const string Person = "/personnel/{PersonId}";
    
    public static string WithParameters(Guid personId) 
        => Person.Replace("{PersonId}", personId.ToString());
}
```

Usage:
```razor
<MudButton Href="@Routes.Person.WithParameters(person.Id)">
    View Person
</MudButton>
```

---

## Lifecycle Hooks

### Angular Lifecycle Hooks
```typescript
export class MyComponent implements OnInit, OnDestroy, AfterViewInit {
  ngOnInit() {
    // Called once after component initialized
  }
  
  ngOnChanges(changes: SimpleChanges) {
    // Called when @Input properties change
  }
  
  ngAfterViewInit() {
    // Called after view initialized
  }
  
  ngOnDestroy() {
    // Called before component destroyed
  }
}
```

### Blazor Lifecycle Methods

```csharp
public class MyComponent : ComponentBase
{
    protected override async Task OnInitializedAsync()
    {
        // Called once after component initialized
        // Similar to ngOnInit
        await LoadData();
    }
    
    protected override async Task OnParametersSetAsync()
    {
        // Called when parameters are set/changed
        // Similar to ngOnChanges
        if (PersonId != Guid.Empty)
        {
            await LoadPerson(PersonId);
        }
    }
    
    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        // Called after component rendered
        // Similar to ngAfterViewInit
        if (firstRender)
        {
            // Only on first render
            await JSRuntime.InvokeVoidAsync("initializeMap");
        }
    }
    
    public void Dispose()
    {
        // Called when component is destroyed
        // Similar to ngOnDestroy
        _cancellationTokenSource?.Cancel();
    }
}
```

### Order of Execution

1. Constructor
2. `SetParametersAsync` (sets [Parameter] properties)
3. `OnInitialized` / `OnInitializedAsync` (once)
4. `OnParametersSet` / `OnParametersSetAsync` (every time parameters change)
5. `OnAfterRender` / `OnAfterRenderAsync` (after every render)

### Real Example - Person Details

```csharp
protected override async Task OnParametersSetAsync()
{
    if (PersonId == Guid.Empty)
    {
        return;
    }
    
    if (_person is null || _person.Id != PersonId)
    {
        _person = await MediatR.Send(new GetPersonInformationQuery(PersonId));
        _departmentIdsOfPerson = _person.PersonDepartments
            .Select(pd => pd.DepartmentId).ToList();
    }
}

protected override async Task OnAfterRenderAsync(bool firstRender)
{
    if (firstRender)
    {
        IsSmallScreen = await BrowserViewportService
            .GetCurrentBreakpointAsync() <= Breakpoint.Sm;
        StateHasChanged(); // Trigger re-render
    }
}
```

---

## Dependency Injection

### Angular DI
```typescript
@Component({...})
export class MyComponent {
  constructor(
    private http: HttpClient,
    private userService: UserService,
    private dialog: MatDialog
  ) {}
}
```

### Blazor DI
```csharp
public partial class MyComponent : ComponentBase
{
    [Inject] private HttpClient Http { get; set; } = null!;
    [Inject] private IUserService UserService { get; set; } = null!;
    [Inject] private IDialogService DialogService { get; set; } = null!;
}
```

### Service Registration

**Angular:**
```typescript
// In module
providers: [
  UserService,
  { provide: ILogger, useClass: ConsoleLogger }
]
```

**Blazor (Program.cs):**
```csharp
builder.Services.AddScoped<IUserService, UserService>();
builder.Services.AddSingleton<ILogger, ConsoleLogger>();
```

### Service Lifetimes

| Angular | Blazor | Description |
|---------|--------|-------------|
| `providedIn: 'root'` | `AddSingleton<T>()` | One instance for entire app |
| Default provider | `AddScoped<T>()` | One instance per connection (Blazor Server) |
| N/A | `AddTransient<T>()` | New instance every time |

### Base Component with Common Dependencies

The project uses `BenobixComponentBase` to provide common dependencies:

```csharp
public class BenobixComponentBase : ComponentBase
{
    [Inject] private ISnackbar Snackbar { get; set; } = null!;
    [Inject] private ILogger<BenobixComponentBase> Logger { get; set; } = null!;
    [Inject] private ILoadingService LoadingService { get; set; } = null!;
    
    protected void ShowError(string message, Exception? ex = null)
    {
        Snackbar.Add<SnackbarMessage>(
            new Dictionary<string, object>
            {
                { "Message", message },
                { "Details", ex?.Message ?? string.Empty },
            },
            Severity.Error);
    }
    
    protected async Task<bool> TryAndShowError(Func<Task> task, string message)
    {
        try
        {
            await task.Invoke();
            return true;
        }
        catch (Exception ex)
        {
            Logger.LogError(ex, ex.Message);
            ShowError(message, ex);
            return false;
        }
    }
}
```

All components inherit from this base class:
```csharp
public partial class MyComponent : BenobixComponentBase
{
    // Automatically has access to Logger, Snackbar, ShowError, etc.
}
```

---

## State Management

### Component State

**Both Angular and Blazor:**
- Component has private fields/properties for local state
- State changes trigger re-render

**Angular:**
```typescript
export class MyComponent {
  private users: User[] = [];
  private isLoading = false;
  
  async loadUsers() {
    this.isLoading = true;
    this.users = await this.api.getUsers();
    this.isLoading = false;
  }
}
```

**Blazor:**
```csharp
public partial class MyComponent : ComponentBase
{
    private List<User> _users = new();
    private bool _isLoading = false;
    
    private async Task LoadUsers()
    {
        _isLoading = true;
        StateHasChanged(); // Force UI update
        
        _users = await Api.GetUsers();
        _isLoading = false;
        StateHasChanged(); // Force UI update
    }
}
```

**Key Difference**: Blazor sometimes needs explicit `StateHasChanged()` calls, especially after async operations.

### Shared State (Services)

**Angular:**
```typescript
@Injectable({ providedIn: 'root' })
export class UserStateService {
  private userSubject = new BehaviorSubject<User | null>(null);
  user$ = this.userSubject.asObservable();
  
  setUser(user: User) {
    this.userSubject.next(user);
  }
}
```

**Blazor:**
```csharp
public interface IUserStateService
{
    User? CurrentUser { get; set; }
    event EventHandler UserChanged;
}

public class UserStateService : IUserStateService
{
    private User? _currentUser;
    
    public User? CurrentUser
    {
        get => _currentUser;
        set
        {
            _currentUser = value;
            UserChanged?.Invoke(this, EventArgs.Empty);
        }
    }
    
    public event EventHandler? UserChanged;
}
```

### MediatR for Commands/Queries (CQRS Pattern)

This project uses **MediatR** for command/query separation - similar to NgRx actions/effects in Angular:

**Angular (with NgRx):**
```typescript
// Dispatch action
this.store.dispatch(createUser({ user }));

// Select from store
this.users$ = this.store.select(selectAllUsers);
```

**Blazor (with MediatR):**
```csharp
// Send command
var result = await MediatR.Send(new CreateUserCommand(user));

// Send query
var users = await MediatR.Send(new GetAllUsersQuery());
```

**Command Example:**
```csharp
// Command
public record CreateUserAccountCommand(string Email, Person Person) 
    : IRequest<CreateUserResult>;

// Handler
public class CreateUserAccountHandler 
    : IRequestHandler<CreateUserAccountCommand, CreateUserResult>
{
    public async Task<CreateUserResult> Handle(
        CreateUserAccountCommand request, 
        CancellationToken cancellationToken)
    {
        // Business logic here
        var user = await _userRepository.Create(request.Email, request.Person);
        return new CreateUserResult { Success = true, User = user };
    }
}

// Usage in component
private async Task CreateAccount()
{
    var result = await MediatR.Send(
        new CreateUserAccountCommand(email, person));
    
    if (result.Success)
    {
        ShowSuccessSnackbar("Account created!");
    }
}
```

---

## Dialogs and Modals

### Opening a Dialog

**Angular Material:**
```typescript
const dialogRef = this.dialog.open(UserDialogComponent, {
  width: '500px',
  data: { userId: user.id }
});

dialogRef.afterClosed().subscribe(result => {
  if (result) {
    this.saveUser(result);
  }
});
```

**MudBlazor:**
```csharp
var parameters = new DialogParameters
{
    [nameof(UserDialog.UserId)] = user.Id
};

var dialogOptions = new DialogOptions
{
    MaxWidth = MaxWidth.Small,
    FullWidth = true,
    CloseOnEscapeKey = true,
    BackdropClick = false
};

var dialog = await DialogService.ShowAsync<UserDialog>(
    "Edit User", parameters, dialogOptions);
    
var result = await dialog.Result;

if (result is not null && !result.Canceled)
{
    await SaveUser((User)result.Data);
}
```

### Dialog Component Structure

**Angular:**
```typescript
@Component({
  selector: 'app-user-dialog',
  template: `
    <h2 mat-dialog-title>{{ data.title }}</h2>
    <mat-dialog-content>
      <form [formGroup]="form">
        <!-- Form fields -->
      </form>
    </mat-dialog-content>
    <mat-dialog-actions>
      <button mat-button (click)="cancel()">Cancel</button>
      <button mat-button (click)="save()">Save</button>
    </mat-dialog-actions>
  `
})
export class UserDialogComponent {
  constructor(
    public dialogRef: MatDialogRef<UserDialogComponent>,
    @Inject(MAT_DIALOG_DATA) public data: any
  ) {}
  
  cancel() {
    this.dialogRef.close();
  }
  
  save() {
    this.dialogRef.close(this.form.value);
  }
}
```

**Blazor:**
```razor
@* UserDialog.razor *@
@inherits BenobixComponentBase

<MudDialog Class="p-3">
    <TitleContent>
        <MudText Typo="Typo.h2">@MudDialog.Title</MudText>
    </TitleContent>
    
    <DialogContent>
        <BenobixForm Model="@User" 
                     Validator="_validator"
                     OnValidSubmit="Save"
                     OnCanceled="Cancel">
            <!-- Form fields -->
        </BenobixForm>
    </DialogContent>
</MudDialog>

@code {
    [Parameter] public Guid UserId { get; set; }
    [CascadingParameter] private IMudDialogInstance MudDialog { get; set; } = null!;
    
    private User User { get; set; } = new();
    
    private void Save()
    {
        MudDialog.Close(DialogResult.Ok(User));
    }
    
    private void Cancel()
    {
        MudDialog.Cancel();
    }
}
```

### Real Example - Delete Confirmation Dialog

From `DeleteDocumentDialog.razor`:
```razor
<MudDialog Class="p-3">
    <TitleContent>
        <MudText Typo="Typo.h2">@Title</MudText>
    </TitleContent>

    <DialogContent>
        <MudText>@CommonLocalization.DeleteDocumentDialogText : @DocumentName</MudText>
    </DialogContent>

    <DialogActions>
        <BenobixButton OnClick="@Cancel"
                      StartIcon="@Icons.Material.Filled.Cancel"
                      Color="Color.Secondary">
            @CommonLocalization.ButtonCancel
        </BenobixButton>
        <BenobixButton OnClick="@Apply"
                      StartIcon="@Icons.Material.Filled.Delete"
                      ButtonType="ButtonType.Submit">
            @CommonLocalization.ButtonDeleteDocument
        </BenobixButton>
    </DialogActions>
</MudDialog>
```

Usage:
```csharp
private async Task DeleteDocument(Document doc)
{
    var parameters = new DialogParameters
    {
        [nameof(DeleteDocumentDialog.DocumentName)] = doc.Name,
        [nameof(DeleteDocumentDialog.Title)] = "Delete Document"
    };
    
    var dialog = await DialogService.ShowAsync<DeleteDocumentDialog>(
        "Confirm Delete", parameters);
    var result = await dialog.Result;
    
    if (!result.Canceled)
    {
        await _documentService.Delete(doc.Id);
    }
}
```

---

## Tables and Data Grids

### Basic Table

**Angular Material:**
```typescript
export class UsersComponent {
  dataSource: MatTableDataSource<User>;
  displayedColumns = ['name', 'email', 'actions'];
  
  constructor(private api: UserService) {
    this.dataSource = new MatTableDataSource();
  }
  
  ngOnInit() {
    this.api.getUsers().subscribe(users => {
      this.dataSource.data = users;
    });
  }
}
```
```html
<table mat-table [dataSource]="dataSource">
  <ng-container matColumnDef="name">
    <th mat-header-cell *matHeaderCellDef>Name</th>
    <td mat-cell *matCellDef="let user">{{ user.name }}</td>
  </ng-container>
  
  <tr mat-header-row *matHeaderRowDef="displayedColumns"></tr>
  <tr mat-row *matRowDef="let row; columns: displayedColumns;"></tr>
</table>
```

**MudBlazor:**
```razor
<MudTable Items="@Users" Hover="true" Breakpoint="Breakpoint.Sm">
    <HeaderContent>
        <MudTh>Name</MudTh>
        <MudTh>Email</MudTh>
        <MudTh>Actions</MudTh>
    </HeaderContent>
    <RowTemplate Context="user">
        <MudTd>@user.Name</MudTd>
        <MudTd>@user.Email</MudTd>
        <MudTd>
            <MudIconButton Icon="@Icons.Material.Filled.Edit" 
                          OnClick="@(() => EditUser(user))" />
        </MudTd>
    </RowTemplate>
</MudTable>

@code {
    private List<User> Users { get; set; } = new();
    
    protected override async Task OnInitializedAsync()
    {
        Users = await UserService.GetAllUsers();
    }
}
```

### Server-Side Table with Pagination, Sorting, and Search

This project uses a custom `BenobixTable` component that wraps `MudTable`:

```razor
<BenobixTable T="UserIncludingPerson"
              LoadServerData="@LoadServerData"
              SearchField="true"
              RowClass="cursor-pointer"
              OnRowClick="@(e => OpenUserDetails(e.Item))"
              @ref="_table">
    <HeaderContent>
        <MudTh>
            <MudTableSortLabel SortLabel="@($"{nameof(UserIncludingPerson.Person)}.{nameof(Person.FirstName)}")" 
                               T="UserIncludingPerson">
                Name
            </MudTableSortLabel>
        </MudTh>
        <MudTh>
            <MudTableSortLabel SortLabel="@($"{nameof(UserIncludingPerson.User)}.{nameof(User.Email)}")" 
                               T="UserIncludingPerson">
                Email
            </MudTableSortLabel>
        </MudTh>
    </HeaderContent>
    <RowTemplate Context="user">
        <MudTd>@user.Person.GetFullName()</MudTd>
        <MudTd>@user.User?.Email</MudTd>
    </RowTemplate>
</BenobixTable>

@code {
    private BenobixTable<UserIncludingPerson> _table = null!;
    
    private async Task<TableData<UserIncludingPerson>> LoadServerData(
        TableState state, CancellationToken cancellationToken)
    {
        var query = new GetUsersWithFilterOptions
        {
            PageNumber = state.Page + 1,
            PageSize = state.PageSize,
            SortBy = state.SortLabel,
            SortDirection = state.SortDirection,
        };

        var result = await MediatR.Send(query, cancellationToken);
        
        return new TableData<UserIncludingPerson> 
        { 
            Items = result.Items, 
            TotalItems = result.TotalCount 
        };
    }
    
    private async Task RefreshTable()
    {
        await _table.ReloadServerData();
    }
}
```

**Key Features:**
- `LoadServerData`: Async function that loads data based on current table state
- `TableState`: Contains page, pageSize, sortLabel, sortDirection
- `SearchField="true"`: Adds search box
- `OnRowClick`: Row click handler
- `@ref="_table"`: Reference to reload data programmatically

**Angular Equivalent:**
```typescript
export class UsersComponent {
  dataSource: MatTableDataSource<User>;
  @ViewChild(MatPaginator) paginator: MatPaginator;
  @ViewChild(MatSort) sort: MatSort;
  
  ngAfterViewInit() {
    this.dataSource.paginator = this.paginator;
    this.dataSource.sort = this.sort;
    this.dataSource.filterPredicate = ...;
  }
}
```

---

## Layout and Responsive Design

### Grid System

**Angular Material:**
```html
<div fxLayout="row" fxLayout.xs="column">
  <div fxFlex="50" fxFlex.xs="100">Column 1</div>
  <div fxFlex="50" fxFlex.xs="100">Column 2</div>
</div>
```

**MudBlazor:**
```razor
<MudGrid>
    <MudItem xs="12" md="6">Column 1</MudItem>
    <MudItem xs="12" md="6">Column 2</MudItem>
</MudGrid>
```

**Grid Breakpoints:**
- `xs`: Extra small (< 600px)
- `sm`: Small (≥ 600px)
- `md`: Medium (≥ 960px)
- `lg`: Large (≥ 1264px)
- `xl`: Extra large (≥ 1904px)

### Responsive Visibility

**Angular Material:**
```html
<div fxHide.xs fxShow.gt-xs>
  Hidden on mobile
</div>
```

**MudBlazor:**
```razor
<MudHidden Breakpoint="Breakpoint.SmAndDown">
    Hidden on mobile
</MudHidden>

<MudHidden Breakpoint="Breakpoint.MdAndUp">
    Only on mobile
</MudHidden>
```

### Real Example - Responsive TopBar

From `TopBar.razor`:
```razor
<MudAppBar Elevation="0" Fixed="true" Dense="true">
    @if (LoggedInPerson is not null)
    {
        <!-- Desktop View -->
        <MudHidden Breakpoint="Breakpoint.SmAndDown">
            <MudIconButton Icon="@Icons.Material.Filled.Menu" OnClick="OnMenuClick" />
            <BenobixCompanyLogo Width="200" Height="45" />
            <MudSpacer />
            <MudButton Href="@($"/personnel/{LoggedInPerson.Id}")">
                <AvatarProfilePicture Person="LoggedInPerson" />
                <MudText>@LoggedInPerson.FirstName @LoggedInPerson.LastName</MudText>
            </MudButton>
            <LanguageSelectionMenu />
            <MudButton Href="@Routes.LogOut" StartIcon="@Icons.Material.Filled.Logout">
                Logout
            </MudButton>
        </MudHidden>
        
        <!-- Mobile View (Hamburger Menu) -->
        <MudHidden Breakpoint="Breakpoint.MdAndUp">
            <MudIconButton Icon="@Icons.Material.Filled.Menu" OnClick="OnMenuClick" />
            <MudSpacer />
            <BenobixCompanyLogo Height="45" />
            <MudSpacer />
            <MudMenu Icon="@Icons.Material.Filled.MoreVert">
                <MudMenuItem Href="@($"/personnel/{LoggedInPerson.Id}")">
                    <AvatarProfilePicture Person="LoggedInPerson" />
                    @LoggedInPerson.FirstName @LoggedInPerson.LastName
                </MudMenuItem>
                <LanguageSelectionMenu />
                <MudDivider />
                <MudMenuItem Href="@Routes.LogOut" Icon="@Icons.Material.Filled.Logout">
                    Logout
                </MudMenuItem>
            </MudMenu>
        </MudHidden>
    }
</MudAppBar>
```

### Main Layout Structure

**Angular:**
```html
<!-- app.component.html -->
<mat-sidenav-container>
  <mat-sidenav #sidenav mode="side">
    <app-sidebar></app-sidebar>
  </mat-sidenav>
  <mat-sidenav-content>
    <app-toolbar></app-toolbar>
    <router-outlet></router-outlet>
  </mat-sidenav-content>
</mat-sidenav-container>
```

**Blazor:**
```razor
@* MainLayout.razor *@
@inherits LayoutComponentBase

<MudThemeProvider />
<MudDialogProvider />
<MudSnackbarProvider />

<MudLayout>
    <MudAppBar>
        <TopBar OnMenuClick="ToggleSideBar" />
    </MudAppBar>
    
    <MudDrawer @bind-Open="_drawerOpen">
        <NavMenu />
    </MudDrawer>
    
    <MudMainContent>
        @Body
    </MudMainContent>
</MudLayout>

@code {
    private bool _drawerOpen = true;
    
    private void ToggleSideBar()
    {
        _drawerOpen = !_drawerOpen;
    }
}
```

**Key Points:**
- `@Body` is where routed component content renders (like `<router-outlet>`)
- `@inherits LayoutComponentBase` makes it a layout
- Pages specify their layout with `@layout MainLayout`

---

## Authorization and Security

### Page-Level Authorization

**Angular:**
```typescript
const routes: Routes = [
  {
    path: 'admin',
    component: AdminComponent,
    canActivate: [AuthGuard],
    data: { roles: ['Admin'] }
  }
];
```

**Blazor:**
```razor
@* AdminPage.razor *@
@attribute [Route("/admin")]
@attribute [Authorize(Roles = "Admin")]

<h1>Admin Page</h1>
```

For anonymous pages:
```razor
@attribute [AllowAnonymous]
```

### Authorization Views

**Angular:**
```html
<div *ngIf="hasPermission('read')">
  <p>You can read this</p>
</div>
```

**Blazor:**
```razor
<AuthorizeView Policy="@RequiredPolicy">
    <Authorized>
        <p>You can read this</p>
    </Authorized>
    <NotAuthorized>
        <p>Access Denied</p>
    </NotAuthorized>
</AuthorizeView>
```

### Real Example - Custom Authorization Component

From `BenobixAuthorizePage.razor`:
```razor
<BenobixAuthorizePage Policy="@(AuthorizationPolicyHelper.Policy<PersonnelAccessRole>(PermissionType.Read, departmentIds, subjectAreaIds, [personId]))">
    <Authorized>
        <MudPaper>
            <!-- Content user can access -->
        </MudPaper>
    </Authorized>
    <NotAuthorized>
        <MudAlert Severity="Severity.Error">
            You don't have permission to view this page.
        </MudAlert>
    </NotAuthorized>
</BenobixAuthorizePage>
```

---

## Common MudBlazor Components

### Buttons

```razor
<!-- Basic button -->
<MudButton Variant="Variant.Filled" Color="Color.Primary">
    Click Me
</MudButton>

<!-- Button with icon -->
<MudButton StartIcon="@Icons.Material.Filled.Save" OnClick="Save">
    Save
</MudButton>

<!-- Icon-only button -->
<MudIconButton Icon="@Icons.Material.Filled.Edit" OnClick="Edit" />

<!-- Loading button -->
<MudButton Disabled="@IsLoading">
    @if (IsLoading)
    {
        <MudProgressCircular Size="Size.Small" Indeterminate="true" />
    }
    else
    {
        <span>Submit</span>
    }
</MudButton>
```

**Variants:**
- `Variant.Filled` (default, solid color)
- `Variant.Outlined` (border only)
- `Variant.Text` (no background/border)

**Colors:**
- `Color.Primary` (blue)
- `Color.Secondary` (purple)
- `Color.Success` (green)
- `Color.Error` (red)
- `Color.Warning` (orange)
- `Color.Info` (light blue)

### Text Fields

```razor
<!-- Basic text field -->
<MudTextField @bind-Value="@Name" Label="Name" />

<!-- With validation -->
<MudTextField @bind-Value="@Email" 
              Label="Email" 
              For="@(() => Email)"
              Required="true"
              RequiredError="Email is required" />

<!-- Numeric field -->
<MudNumericField @bind-Value="@Age" Label="Age" Min="0" Max="120" />

<!-- Text area -->
<MudTextField @bind-Value="@Description" 
              Label="Description" 
              Lines="5" 
              AutoGrow="true" />

<!-- Password field -->
<MudTextField @bind-Value="@Password" 
              Label="Password" 
              InputType="InputType.Password" />
```

### Select Dropdowns

```razor
<MudSelect @bind-Value="@SelectedCountry" Label="Country">
    @foreach (var country in Countries)
    {
        <MudSelectItem Value="@country">@country.Name</MudSelectItem>
    }
</MudSelect>

<!-- Multi-select -->
<MudSelect @bind-Value="@SelectedRoles" 
           Label="Roles" 
           MultiSelection="true">
    @foreach (var role in Roles)
    {
        <MudSelectItem Value="@role">@role.Name</MudSelectItem>
    }
</MudSelect>
```

### Checkboxes and Switches

```razor
<!-- Checkbox -->
<MudCheckBox @bind-Value="@IsActive" Label="Active" />

<!-- Switch -->
<MudSwitch @bind-Value="@IsEnabled" Label="Enabled" Color="Color.Primary" />

<!-- Radio buttons -->
<MudRadioGroup @bind-Value="@SelectedOption">
    <MudRadio Value="@("option1")">Option 1</MudRadio>
    <MudRadio Value="@("option2")">Option 2</MudRadio>
</MudRadioGroup>
```

### Date and Time Pickers

```razor
<!-- Date picker -->
<MudDatePicker @bind-Date="@BirthDate" Label="Birth Date" />

<!-- Date range picker -->
<MudDateRangePicker @bind-DateRange="@DateRange" Label="Date Range" />

<!-- Time picker -->
<MudTimePicker @bind-Time="@MeetingTime" Label="Meeting Time" />
```

### Cards

```razor
<MudCard>
    <MudCardHeader>
        <MudText Typo="Typo.h6">Card Title</MudText>
    </MudCardHeader>
    <MudCardContent>
        <MudText>Card content goes here</MudText>
    </MudCardContent>
    <MudCardActions>
        <MudButton Variant="Variant.Text" Color="Color.Primary">Action</MudButton>
    </MudCardActions>
</MudCard>
```

### Alerts and Snackbars

```razor
<!-- Alert -->
<MudAlert Severity="Severity.Success">Operation completed successfully!</MudAlert>
<MudAlert Severity="Severity.Error" Dense="true">An error occurred!</MudAlert>

<!-- Snackbar (from code) -->
@code {
    [Inject] private ISnackbar Snackbar { get; set; } = null!;
    
    private void ShowNotification()
    {
        Snackbar.Add("User saved successfully!", Severity.Success);
        Snackbar.Add("Error saving user", Severity.Error);
    }
}
```

### Progress Indicators

```razor
<!-- Linear progress -->
<MudProgressLinear Value="@Progress" Color="Color.Primary" />

<!-- Circular progress -->
<MudProgressCircular Color="Color.Primary" Indeterminate="true" />

<!-- Loading overlay (custom in this project) -->
@if (IsLoading)
{
    <MudOverlay Visible="true" ZIndex="9999">
        <MudProgressCircular Color="Color.Primary" Indeterminate="true" />
    </MudOverlay>
}
```

### Tabs

```razor
<MudTabs>
    <MudTabPanel Text="Tab 1">
        <p>Content of Tab 1</p>
    </MudTabPanel>
    <MudTabPanel Text="Tab 2">
        <p>Content of Tab 2</p>
    </MudTabPanel>
</MudTabs>
```

### Menus

```razor
<MudMenu Icon="@Icons.Material.Filled.MoreVert">
    <MudMenuItem Icon="@Icons.Material.Filled.Edit" OnClick="Edit">
        Edit
    </MudMenuItem>
    <MudMenuItem Icon="@Icons.Material.Filled.Delete" OnClick="Delete">
        Delete
    </MudMenuItem>
    <MudDivider />
    <MudMenuItem OnClick="Archive">Archive</MudMenuItem>
</MudMenu>
```

### Typography

```razor
<MudText Typo="Typo.h1">Heading 1</MudText>
<MudText Typo="Typo.h2">Heading 2</MudText>
<MudText Typo="Typo.h3">Heading 3</MudText>
<MudText Typo="Typo.body1">Body text</MudText>
<MudText Typo="Typo.body2">Secondary body text</MudText>
<MudText Typo="Typo.caption">Caption text</MudText>
```

---

## Best Practices

### 1. Use Code-Behind for Complex Components

✅ **Good:**
```csharp
// PersonCard.razor.cs
public partial class PersonCard : BenobixComponentBase
{
    [Parameter] public Person Person { get; set; } = null!;
    [Inject] private IPersonService PersonService { get; set; } = null!;
    
    private async Task LoadDetails()
    {
        // Complex logic here
    }
}
```

❌ **Avoid:**
```razor
@code {
    // 200+ lines of code in @code block
}
```

### 2. Use Base Component for Common Functionality

All components should inherit from `BenobixComponentBase`:

```csharp
public partial class MyComponent : BenobixComponentBase
{
    // Gets access to:
    // - LoggedInPerson
    // - CurrentPrincipal
    // - Logger
    // - Snackbar
    // - LoadingService
    // - ShowError() helper
    // - TryAndShowError() helper
}
```

### 3. Use MediatR for Business Logic

✅ **Good:**
```csharp
// In component
var result = await MediatR.Send(new CreatePersonCommand(person));

// Business logic in handler
public class CreatePersonHandler : IRequestHandler<CreatePersonCommand, Person>
{
    public async Task<Person> Handle(CreatePersonCommand request, CancellationToken ct)
    {
        // Validation, business rules, database access
    }
}
```

❌ **Avoid:**
```csharp
// Don't put business logic directly in components
private async Task CreatePerson()
{
    // 50 lines of business logic, validation, DB access
}
```

### 4. Use Strongly-Typed Route Constants

✅ **Good:**
```csharp
public static class Routes
{
    public const string Person = "/personnel/{PersonId}";
    
    public static string WithParameters(Guid personId) 
        => Person.Replace("{PersonId}", personId.ToString());
}

// Usage
<MudButton Href="@Routes.Person.WithParameters(person.Id)">View</MudButton>
```

❌ **Avoid:**
```razor
<MudButton Href="@($"/personnel/{person.Id}")">View</MudButton>
```

### 5. Handle Async Operations Properly

✅ **Good:**
```csharp
private async Task LoadData()
{
    try
    {
        IsLoading = true;
        StateHasChanged();
        
        _data = await DataService.GetData();
    }
    catch (Exception ex)
    {
        Logger.LogError(ex, "Error loading data");
        ShowError("Failed to load data", ex);
    }
    finally
    {
        IsLoading = false;
        StateHasChanged();
    }
}
```

Or use the helper:
```csharp
await TryAndShowError(
    async () => {
        _data = await DataService.GetData();
    },
    "Failed to load data"
);
```

### 6. Use Proper Component Parameters

✅ **Good:**
```csharp
[Parameter, EditorRequired] 
public Person Person { get; set; } = null!;

[Parameter] 
public EventCallback<Person> OnPersonSaved { get; set; }
```

❌ **Avoid:**
```csharp
public Person? Person; // Not a parameter
```

### 7. Dispose of Resources

```csharp
public partial class MyComponent : BenobixComponentBase, IDisposable
{
    private CancellationTokenSource _cts = new();
    private Timer? _timer;
    
    public void Dispose()
    {
        _cts?.Cancel();
        _cts?.Dispose();
        _timer?.Dispose();
    }
}
```

### 8. Use Validation Properly

✅ **Good:**
```razor
<BenobixForm Model="@Person" Validator="_validator">
    <MudTextField @bind-Value="@Person.Email" 
                 For="@(() => Person.Email)"
                 Label="Email" />
</BenobixForm>

@code {
    private PersonValidator _validator = new();
}
```

The `For` parameter connects the field to validation.

### 9. Use Custom Components for Reusable UI

The project has many custom components:
- `BenobixForm` - Form with built-in buttons and validation
- `BenobixTable` - Table with server-side data
- `BenobixButton` - Custom styled button
- `BenobixTextField` - Custom text field
- `AvatarProfilePicture` - Display user avatar
- `BenobixCompanyLogo` - Display company logo

Use these instead of raw MudBlazor components for consistency.

### 10. Use `_Imports.razor` for Common Imports

```razor
@* _Imports.razor *@
@using MudBlazor
@using Benobix.Common.Application.Resources
@using Benobix.Common.Presentation.Components.Core
@using Microsoft.AspNetCore.Authorization

@* Now you don't need to import these in every file *@
```

---

## Quick Reference Cheat Sheet

| Task | Angular | Blazor |
|------|---------|--------|
| **Interpolation** | `{{ name }}` | `@Name` |
| **Property Binding** | `[disabled]="isDisabled"` | `Disabled="@IsDisabled"` |
| **Event Binding** | `(click)="save()"` | `@onclick="Save"` |
| **Two-way Binding** | `[(ngModel)]="name"` | `@bind-Value="Name"` |
| **If Condition** | `*ngIf="show"` | `@if (Show) { }` |
| **For Loop** | `*ngFor="let item of items"` | `@foreach (var item in Items) { }` |
| **Component Input** | `@Input() title` | `[Parameter] public string Title` |
| **Component Output** | `@Output() saved = new EventEmitter()` | `[Parameter] public EventCallback OnSaved` |
| **Service Injection** | Constructor injection | `[Inject] private IService Service` |
| **Router Navigation** | `router.navigate(['/path'])` | `Navigation.NavigateTo("/path")` |
| **Route Parameter** | `route.params.subscribe()` | `[Parameter] public Guid Id { get; set; }` |
| **HTTP GET** | `http.get<T>(url)` | `await Http.GetFromJsonAsync<T>(url)` |
| **Show Dialog** | `dialog.open(Component)` | `await DialogService.ShowAsync<Component>()` |
| **Show Toast** | `snackBar.open(message)` | `Snackbar.Add(message)` |
| **Template Reference** | `#myElement`, `@ViewChild` | `@ref _element` |

---

## Summary

Coming from Angular, the main conceptual shifts for Blazor are:

1. **C# instead of TypeScript** - You write component logic in C#, not TypeScript
2. **Razor syntax** - Use `@` for C# expressions instead of `{{ }}` brackets
3. **Component files** - `.razor` + `.razor.cs` instead of `.ts` + `.html`
4. **Server-side rendering** - Components run on the server, not in the browser
5. **MudBlazor** - Material Design component library (like Angular Material)
6. **Parameters** - Use `[Parameter]` attribute instead of `@Input()` decorator
7. **EventCallback** - Use `EventCallback<T>` instead of `EventEmitter<T>`
8. **Dependency Injection** - Use property injection with `[Inject]` instead of constructor
9. **No RxJS** - Use async/await instead of Observables
10. **StateHasChanged()** - Sometimes needs to be called explicitly to re-render

**The good news**: The concepts are very similar! If you understand Angular components, data binding, dependency injection, and routing, you'll pick up Blazor quickly.

---

## Additional Resources

- **MudBlazor Documentation**: https://mudblazor.com/
- **Blazor Documentation**: https://learn.microsoft.com/en-us/aspnet/core/blazor/
- **FluentValidation**: https://docs.fluentvalidation.net/
- **MediatR**: https://github.com/jbogard/MediatR

---

*This guide was created by analyzing the Benobix codebase and identifying common patterns used throughout the project.*
