---
title: Navigation
---
# Navigation

By default, Trinity will register navigation items for each of your resources and custom pages. These classes contain properties and methods that you can override, to configure that navigation item:

```csharp
public override string Icon => "pi pi-user";
public override string Label => "The Customer";
public override string PluralLabel => "The Customers";
```
> [!TIP]
>Find a list of icons here: [Icons](https://primereact.org/icons/#list)