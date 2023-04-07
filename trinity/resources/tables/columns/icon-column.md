---
title: IconColumn
---

Icon columns render an icon component representing their contents:

```csharp
new IconColumn("is_featured")
    .SetOptions(
        (null, "pi pi-circle-fill"),
        ("draft", "pi pi-pencil"),
        ("reviewing", "pi pi-clock"),
        ("published", "pi pi-check-circle")
    )
```

## Customizing the color

Icon columns may also have a set of icon colors, using the same syntax. They may be either `primary`, `secondary`, `success`, `warning` or `danger`:

```csharp
new IconColumn("is_featured")
    .SetOptions(
        (null, "pi pi-circle-fill", "secondary"),
        ("draft", "pi pi-pencil", "danger"),
        ("reviewing", "pi pi-clock", "warning"),
        ("published", "pi pi-check-circle", "success")
    )
```


## Handling booleans

Icon columns can display a check or cross icon based on the contents of the database column, either true or false, using the `SetAsBoolean()` method:

```csharp
new IconColumn("is_featured")
    .SetAsBoolean()
```

## Customizing the boolean icons and colors

You may customize the icon representing each state. By default, [PrimeIcons](https://primereact.org/icons/#list) are installed:

```csharp
new IconColumn("is_featured")
    .SetTrueIcon("pi pi-check-circle","green")
    .SetFalseIcon("pi pi-times-circle","red")
```


## Customizing the boolean values

You may customize what value is true and what value is false. 

```csharp
new IconColumn<string>("is_featured")
    .SetTrueValue("cool")
    .SetFalseValue("bad")
```