---
title: Widgets
---

# Widgets

`Trinity` allows you to display widgets inside pages, and below or above the resource table.

## Displaying a widget on a resource page

To display a widget on a resource page, use the `SetTopWidgets()` or `SetBottomWidgets()` methods:

```csharp
protected override TrinityTable GetTrinityTable()
    {
        return Make<TrinityTable>()
            //[...]
            .SetTopWidgets(new List<ITrinityWidget>()
            {
                // ...
            })
            .SetBottomWidgets(new List<ITrinityWidget>()
            {
                // ...
            })
            //[...]
    }
```

`SetTopWidgets()` returns a list of widgets to display above the table content, whereas `SetBottomWidgets()` are displayed below.

## Pages

To show widgets in [Pages](../pages.md#widgets). 

## Available widgets

`Trinity` ships with a few pre-built widgets, as well as the ability to create custom widgets:

- [Stats](./stats-widget.md) widgets display any data, often numeric data, within cards in a row.
- [ChartWidgets](./chart-widgets.md) widgets display numeric data in a visual chart.


## Generating Widget data from database

Assuming you are using `Entity Framework` , this can be done on pages or resources:

```csharp
//belwo is a Pseudocode
private DatabaseContext _databaseContext = null!;

public override Task Setup()
{
    _databaseContext = ServiceProvider.GetRequiredService<DatabaseContext>();
    return base.Setup();
}

protected override List<ITrinityWidget> GetSchema()
{
    var sales = _databaseContext.Sales.ToList();
    var data = sales.Select(x => Tuple.Create(x.quarter, x.value));
    
    return new List<ITrinityWidget>()
    {
        // static data
        //Make<BarChartWidget>()
            //.SetLabel("Sales")
            //.SetChart(("Q1", 540), ("Q2", 325), ("Q3", 702), ("Q4", 620)),
 
        // database data
        Make<BarChartWidget>()
            .SetLabel("Sales")
            .SetChart(data),
    };
}

```

## Authorization

You may conditionally show or hide widgets for certain users using either the `SetAsVisible()` or `SetAsHidden()` methods:

```csharp
Make<BarChartWidget>()
    .SetLabel("Sales")
    .SetChart(("Q1", 540), ("Q2", 325), ("Q3", 702), ("Q4", 620)),
    .SetAsHidden(!User.IsTrinityAdmin())
```