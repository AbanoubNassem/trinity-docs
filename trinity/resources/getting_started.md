---
title: Resources
---
# Resources
Resources are classes that are used to build CRUD interfaces for your models. They describe how administrators should be
able to interact with data from your app - using tables and forms.

## Creating a resource

To create a resource for the `Customer` model/table:

In your project create `Resources/CustomerResource.cs` class:

```csharp
public class CustomerResource : TrinityResource
{
}
```

by default `TrinityResource` will assume that, the `CustomerResource` table is `customers` and the primary key is `id` ,
where the `id` is `int`.

to override the table name and the primary key:

```csharp
public class CustomerResource : TrinityResource<Guid>
{
    public override string PrimaryKeyColumn => "customer_id";
    protected override string Table => "customer";
}
```

## ShowGridlines :
Displays borders between Table cells, `false` by default. 

```csharp
public override bool ShowGridlines => true;
```

## StripedRows :
Alternating rows are displayed, `false` by default.

```csharp
public override bool StripedRows => true;
```