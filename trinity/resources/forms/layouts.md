---
title: Layouts
---

# Layouts

Layouts may be created using the `Make<>` method. You will then define the `schema` in the first parameter to be displayed inside the layout:

```csharp
Make<GridLayout>(new List<IFormComponent>
    {
        Make<TextField>("title"),
        
        Make<EditorField>("description")
    }
)
```

## Columns

You may create multiple columns within each layout component using the `SetColumns()` method:

```csharp
Make<GridLayout>(new List<IFormComponent>
    {
        Make<TextField>("title"),
        
        Make<EditorField>("description")
    }
)
    .SetColumns(3)
```

## Controlling field column span

You may specify the number of columns that any component may span in the parent grid:

```csharp
Make<GridLayout>(new List<IFormComponent>
    {
        Make<TextField>("title")
            ,
        
        Make<EditorField>("description")
    }
)
    .SetColumnSpan(3)
```

## GridLayout

Generally, form fields are stacked on top of each other in one column. To change this, you may use a grid layout:

```csharp
Make<GridLayout>(new List<IFormComponent>
        {
            Make<TextField>("first_name")
                

            Make<TextField>("last_name")
        }),
```

By default, grid components will create a two column grid for the [PrimeFlex](https://www.primefaces.org/primeflex/gridsystem) `md` breakpoint and higher.

You may pass a different number of columns to the grid's md breakpoint:

```csharp
Make<GridLayout>(new List<IFormComponent>
    {
        Make<TextField>("title"),
        
        Make<EditorField>("description")
    }
)
    .SetColumns(3)
```


## FieldsetLayout

You may want to group fields into a Fieldset. Each fieldset has a label, a border, and a two-column grid by default:

```csharp
Make<GridLayout>(new List<IFormComponent>
        {
            Make<TextField>("first_name")
                

            Make<TextField>("last_name")
        })
        .SetLabel("Some Label"),
```



## TabsLayout

Some forms can be long and complex. You may want to use tabs to reduce the number of components that are visible at once:

```csharp
Make<TabsLayout>(new List<Tab>()
        {
            Make<Tab>("Test1", new List<IFormComponent>()).SetAsDisabled(),
            Make<Tab>("Test2", new List<IFormComponent>()
            {
                
            }),
            Make<Tab>("Test3", new List<IFormComponent>()
            {
                
            }),
        })
        .SetActiveTabIndex(2)
```


## CardLayout

The card layout may be used to render the form components inside a card:

```csharp
 Make<CardLayout>(new List<IFormComponent>
        {

        }
    )
    .SetLabel("Some Title")
```

## PanelLayout

The card layout may be used to render the form components inside a panel container component with an optional content toggle feature:

```csharp
 Make<PanelLayout>(new List<IFormComponent>
        {

        }
    )
    .SetHeader("Some Title")
    .SetAsToggleable()
```

