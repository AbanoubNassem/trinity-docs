---
title: Authentication
---
# Authentication

Since `Trinity` is database agnostic , and doesn't follow a specific implementation for `Authentaction`,
the authentication has to be done manually based on your project implementation.

> [!TIP]
> `Trinity` uses `Cookies` for authentication.

```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.AuthenticateUser = (httpContext, email, password) =>
            Task.FromResult(
                new TrinityUser(
                    "123456", //identifier
                    "Abanoub", //name
                    email, // email
                    email == "admin@admin.com" ? "admin" : "user", // role
                    "https://yourprojectuser.com/avatar" // avatar
                )
            )!;

    })
```
You can use the `httpContext` to access the `ServiceProvider` and get the `DatabaseContext` or any services.

for example:

```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.AuthenticateUser = (httpContext, email, password) => {
        
          var db = httpContext.RequestServices.GetRequiredService<DatabaseContext>();
          var user = db.Users.SingleOrDefaultAsync(x => x.Email == email);
          
          //check if exist or return null
          //verfiy the password based on your implementation
        
          return  Task.FromResult(
                new TrinityUser(
                    user.Id, //identifier
                    user.Name, //name
                    user.Email, // email
                    user.Role.Name, // role
                    user.avatar // avatar
                )
            )!;
        };

    })
```

## CSRF protection

> [!NOTE]
> `Trinity` automatically includes the proper CSRF protection when making requests.