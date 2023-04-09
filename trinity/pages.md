---
title: Pages
---

# Pages

`Trinity` allows you to create completely custom pages for the admin panel.

## Creating a page

To create a new page, you can inherit from `TrinityPage`:

```csharp
public class Settings : TrinityPage
{
}
```

this will register a new item in the side navigation.

## Customization

`Trinity` will automatically generate a title, navigation label and URL (slug) for your page based on its name. You may override it using the properties of your page class:

```csharp
public class Settings : TrinityPage
{
    public override string Slug => "abanoub-nassem";

    public override string Label => "Settings";

    public override string Icon => "pi pi-apple";
}
```

## Widgets

`Trinity` allows you to display widgets inside pages.

To add a widget to a page, use the `GetSchema()` method:

```csharp
protected override List<ITrinityWidget> GetSchema()
{
    return new List<ITrinityWidget>()
    {
        Make<BarChartWidget>()
            .SetLabel("Sales")
            .SetChart(("Q1", 540), ("Q2", 325), ("Q3", 702), ("Q4", 620)),
    };
}
```

