---
title: TextColumn
---
# TextColumn

Text columns display simple text from your database:

```csharp
new TextField(columnName: "first_name"),
```

## Displaying a description

Descriptions may be used to easily render additional text above or below the column contents.

You can display a description below the contents of a text column using the `SetDescription()` method:

```csharp
new TextColumn("first_name")
    .SetDescription(record => $"{record["first_name"]} has a description"),
```

By default, the description is displayed below the main text, but you can move it above using the second parameter:
```csharp
new TextColumn("first_name")
    .SetDescription(record => $"{record["first_name"]} has a description", DescriptionPositionTypes.Above),
```


## Date formatting

You may use the `SetAsDateTime` method to format the column:

```csharp
new TextColumn("last_update")
    .SetAsDateTime("yyyy-MM-dd HH:mm:ss")
```

You may use the `SetAsTimeAgo()` method to format the column to be a string showing how long ago a DateTime was, for example `4 minutes ago`:

```csharp
new TextColumn("last_update")
    .SetAsDateTime()
    .SetAsTimeAgo()
```

## Currency formatting

The `SetAsCurrency` method allows you to easily format monetary values, in any currency.:

```csharp
new TextColumn("rental_rate")
    .SetAsCurrency("eur")
```

## Limiting text length

You may `SetLimit()` the length of the cell's value:

```csharp
new TextColumn("description")
    .SetLimit(50)
```

## Limiting word count

You may limit the number of `SetWordsCount()` displayed in the cell:

```csharp
new TextColumn("description")
    .SetLimit(10)
```

## Rendering HTML

If your column value is HTML, you may render it using `SetAsHtml()`:

```csharp
new TextColumn("description")
    .SetAsHtml()
```

## Custom formatting

You may instead pass a custom formatting callback to `SetFormatUsing()`, which accepts the `record` of the cell:

```csharp
new TextColumn("description")
    .SetFormatUsing(record => $"<p class='text-gray-500'>{record["description"]}</p>")
```

## Customizing the color

You may set a color for the text, either `primary`, `secondary`, `success`, `warning` or `danger`:

```csharp
new TextColumn("status")
    .SetColor("primary")
```

## Adding an icon

Text columns may also have an icon, You may set the position of an icon using:

```csharp
new TextColumn("email")
    .SetIcon("pi pi-mail", "after"), // after or before
```

## Customizing the text size

You may make the text smaller or bigger using [`SetSize(SizeTypes)`](~/api/AbanoubNassem.Trinity.Components.TrinityColumn.SizeTypes.yml):

```csharp
new TextColumn("title")
    SetSize(SizeTypes.Xl)
```

## Customizing the font weight

Text columns have regular font weight by default but you may change this to any of the the following options: `font-light`, `font-normal`, `font-medium`, `font-semibold`,or `font-bold`.

For instance, you may make the font bold using `SetWeight("font-bold")`:

```csharp
new TextColumn("title")
    SetWeight("font-bold")
```

## Customizing the font family

You can change the text font family.

For instance, you may make the font mono using `SetFontFamily("mono")`:

```csharp
new TextColumn("title")
    SetFontFamily("mono")
```