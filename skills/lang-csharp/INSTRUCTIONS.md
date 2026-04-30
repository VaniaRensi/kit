---
name: lang-csharp
category: quality
description: >
  C# and .NET lens for core audit, refactor, and quality skills. Augments core-audit,
  core-refactor, and core-quality with language-specific naming conventions, .NET
  architecture patterns, dependency scanning, and security checks.
---

# C# Lens — Language-Specific Standards for .NET Projects

This skill does **not** replace `core-audit`, `core-refactor`, or `core-quality` — it augments them. Load this skill alongside the relevant core skill whenever the project is written in C#.

---

## 🔍 Detection Signals

Load this skill automatically when any of the following are found during the Exploration step:

- `*.csproj` or `*.sln` file in the project root
- `global.json` (SDK version pinning)
- `Program.cs`, `Startup.cs`, or `appsettings.json`

---

## 1. Naming Conventions (augments `core-naming`)

.NET naming is strict and enforced by Roslyn analyzers. Any deviation is a HIGH audit finding.

| Scope | Convention | Example |
|-------|-----------|---------|
| Classes, methods, properties, namespaces | `PascalCase` | `UserService`, `GetById` |
| Local variables, parameters | `camelCase` | `userId`, `requestBody` |
| Private fields | `_camelCase` | `_userRepository` |
| Constants | `PascalCase` | `MaxRetryCount` (not `MAX_RETRY_COUNT`) |
| Interfaces | `I` prefix + PascalCase | `IUserRepository` |
| Async methods | `Async` suffix | `GetByIdAsync` |
| Generic type parameters | `T` prefix | `TEntity`, `TResult` |

**Common violations to flag:**
- `getUserById` instead of `GetUserById` (camelCase on public method)
- `_UserService` or `userService` for private fields (wrong prefix or case)
- Async method missing `Async` suffix (silent breaking of await conventions)
- Interface not prefixed with `I`

---

## 2. Architecture Patterns (augments `core-architecture`)

### Dependency Injection (DI)
.NET has a built-in DI container. Services should never be instantiated with `new` inside a class — they must be injected via constructor.

```csharp
// ❌ Anti-pattern — tight coupling, untestable
public class OrderController {
    private readonly OrderService _service = new OrderService();
}

// ✅ Correct — constructor injection
public class OrderController {
    private readonly IOrderService _service;
    public OrderController(IOrderService service) => _service = service;
}
```

**Flag as HIGH**: direct `new` instantiation of services that should be injected.

### Repository Pattern
Data access must be behind an interface. EF Core DbContext should not be injected directly into controllers.

```csharp
// ❌ Controller should not reference DbContext directly
public class UserController(AppDbContext db) { ... }

// ✅ Controller references repository interface
public class UserController(IUserRepository users) { ... }
```

### Options Pattern
Configuration must use `IOptions<T>` — never read `IConfiguration` directly in services.

```csharp
// ❌ Direct config reads break testability
var timeout = _config["HttpClient:Timeout"];

// ✅ Strongly-typed options
public class ApiSettings { public int TimeoutSeconds { get; set; } }
// Injected as IOptions<ApiSettings>
```

### CQRS (when present)
If the project uses MediatR or similar, commands and queries must be separated. A handler that does both read and write is a MEDIUM finding.

---

## 3. Dependency Scanning (augments `core-audit` AUDIT-DEPS)

Run these commands and record the output in `AUDIT-DEPS.md`:

```bash
# Vulnerable packages (NuGet security advisories)
dotnet list package --vulnerable

# Outdated packages
dotnet list package --outdated

# Deprecated packages
dotnet list package --deprecated
```

**Flags:**
- Any `--vulnerable` output = CRITICAL finding.
- Packages >2 major versions behind = HIGH finding.
- No `global.json` = MEDIUM (SDK version not pinned, builds may differ across machines).
- Packages targeting `net5.0`, `net6.0`, or `netcoreapp*` (EOL targets) = HIGH.

---

## 4. Security Specifics (augments `core-audit` AUDIT-SECURITY)

### Entity Framework — Parameterization
Raw SQL in EF must always use parameterized queries.

```csharp
// ❌ SQL injection risk — CRITICAL
var users = db.Users.FromSqlRaw($"SELECT * FROM Users WHERE Name = '{name}'");

// ✅ Safe — parameterized
var users = db.Users.FromSqlRaw("SELECT * FROM Users WHERE Name = {0}", name);
// Or use LINQ — always safe
var users = db.Users.Where(u => u.Name == name);
```

### ASP.NET Middleware Order
In `Program.cs`, middleware must follow this order. Wrong order = security bypass.

```
1. UseExceptionHandler / UseDeveloperExceptionPage
2. UseHttpsRedirection
3. UseStaticFiles
4. UseRouting
5. UseCors
6. UseAuthentication   ← must come before UseAuthorization
7. UseAuthorization
8. MapControllers / MapRazorPages
```

**Flag as CRITICAL**: `UseAuthorization` before `UseAuthentication`.

### Secrets Management
Secrets must never appear in `appsettings.json` committed to source control. Use:
- Development: `dotnet user-secrets`
- Production: environment variables or Azure Key Vault / AWS Secrets Manager

**Flag as CRITICAL**: connection strings, API keys, or passwords in `appsettings.json`.

### Nullable Reference Types
If the project targets .NET 6+, `<Nullable>enable</Nullable>` should be in the `.csproj`. Disabled nullable = potential null reference exceptions at runtime.

**Flag as MEDIUM** if missing on a .NET 6+ project.

---

## 5. Code Quality Signals (augments `core-quality`)

| Pattern | Severity | Reason |
|---------|----------|--------|
| `async void` method (not an event handler) | HIGH | Exceptions are swallowed; cannot be awaited |
| `catch (Exception ex)` without re-throw or specific type | MEDIUM | Masks bugs, swallows recoverable errors |
| `IDisposable` implemented without `using` at call site | HIGH | Resource leaks (DbConnection, HttpClient, Stream) |
| `HttpClient` created with `new` per request | HIGH | Socket exhaustion — use `IHttpClientFactory` |
| Blocking `.Result` or `.Wait()` on async code | HIGH | Deadlock risk in ASP.NET context |
| Missing `CancellationToken` on async methods | MEDIUM | Long operations cannot be cancelled |
| `string` concatenation in loops | LOW | Use `StringBuilder` for performance |
| `DateTime.Now` instead of `DateTime.UtcNow` | MEDIUM | Timezone-sensitive bugs |

---

## 6. Testing Conventions (augments `core-quality`)

.NET testing follows Arrange-Act-Assert (AAA). The dominant frameworks are xUnit, NUnit, and MSTest.

```csharp
// xUnit example
public class UserServiceTests {
    [Fact]
    public async Task GetById_ReturnsUser_WhenExists() {
        // Arrange
        var repo = Substitute.For<IUserRepository>(); // NSubstitute
        repo.GetByIdAsync(1).Returns(new User { Id = 1 });
        var sut = new UserService(repo);

        // Act
        var result = await sut.GetByIdAsync(1);

        // Assert
        Assert.NotNull(result);
        Assert.Equal(1, result.Id);
    }
}
```

**Flags:**
- Tests without AAA structure = LOW (readability debt).
- No test project at all = HIGH (untestable production code by definition).
- Tests that use `Thread.Sleep` instead of `Task.Delay` = MEDIUM.
- Mocking concrete classes instead of interfaces = MEDIUM (signals missing abstraction).

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 3: CONTROL (augmenting **AUDIT** or **QUALITY** mode).
2. **Objective**: Apply C#/.NET standards on top of the core skill currently active.
3. **Recommended Next Step**:
   - During audit → return to `core-audit` and continue the 6-Report framework.
   - During refactor → return to `core-refactor` and apply fixes using this skill as the naming/architecture reference.
   - If architecture questions arise → load `core-architecture` alongside this skill.
4. **Where this skill sits in the flow**:
   ```
   core-audit (Exploration detects .csproj) → load lang-csharp → continue audit with C# lens
   core-refactor (Standards Reference: naming/arch fixes) → consult lang-csharp → apply fix → verify
   ```
