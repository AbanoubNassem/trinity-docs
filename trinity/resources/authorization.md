---
title: Authorization
---
# Authorization

To limit which users may view, create, update, or delete resources, `Trinity` uses `CanView`,`CanCreate`,`CanUpdate`, and `CanDelete`, to determine if the user can or can't do that action.
> [!NOTE]
> by default all the authorization properties will return true if the user logged-in with role `admin` or `administrator`.

```csharp
    public static bool IsTrinityAdmin(this ClaimsPrincipal user)
    {
        return user.IsInRole("admin") || user.IsInRole("administrator");
    }
    
    public virtual bool CanView => User.IsTrinityAdmin();

    public virtual bool CanCreate => User.IsTrinityAdmin();

    public virtual bool CanUpdate => User.IsTrinityAdmin();

    public virtual bool CanDelete => User.IsTrinityAdmin();
```