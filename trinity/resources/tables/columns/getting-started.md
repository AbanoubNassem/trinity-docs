---
title: Getting started
---
> [!NOTE]
> `Trinity` aliases the table it's querying as `t`, therefore any custom query you apply, prepend `t.` to the local columns you are querying.

Column classes can be found in the [`AbanoubNassem.Trinity.Columns`](~/api/AbanoubNassem.Trinity.Columns.yml) namespace.

- [AggregateColumn](./aggregate-column.md)
- [BadgeColumn](./badge-column.md)
- [BelongsToColumn](./belongs-to-column.md)
- [ColorColumn](./color-column.md)
- [IconColumn](./icon-column.md)
- [IdColumn](./id-column.md)
- [ImageColumn](./image-column.md)
- [TextColumn](./text-column.md)

## Setting a label

By default, the label of the column, which is displayed in the header of the table, is generated from the name of the column. You may customize this using the `SetLabel()` method:

```csharp
new TextColumn("title")
    .SetLabel("this Is Title")
```

## Sorting

Columns may be sortable, by clicking on the column label. To make a column sortable, you must use the `SetAsSortable()` method:

```csharp
new TextColumn("rental_rate")
    .SetAsSortable()
```

You may customize how the sorting is applied to the query using a callback:

```csharp
new TextColumn("full_name")
    .SetAsSortable(true, (query, _) =>
    {
        query.OrderBy("t.last_name", "t.first_name");
    })
```

## Searching

Columns may be searchable, by using the text input in the top right of the table. To make a column searchable, you must use the `SetAsSearchable()` method:

```csharp
new TextColumn("title")
    .SetAsSearchable()  
```

You may customize how the search is applied to the query using a callback:

```csharp
new TextColumn("title")
    .SetAsSearchable(
        searchCallback: (query, str) =>
        {
            query.WhereLike("t.title", str);
        }
    )
```

### Searching individually

You can choose to enable a per-column search input using the `isIndividuallySearchable` parameter:

```csharp
new TextColumn("title")
    .SetAsSearchable(
        isIndividuallySearchable: true
    )
```

If you use the `isIndividuallySearchable` parameter, you may still search that column using the main "global" search input for the entire table.

To disable that functionality while still preserving the individual search functionality, you need the `globallySearchable` parameter:

```csharp
new TextColumn("title")
    .SetAsSearchable(
        isIndividuallySearchable: true,
        globallySearchable : false
    )
```

### Opening URLs

To open a URL, you may use the `SetAsUrl()` method, passing a callback to open. Callbacks accept a `record` parameter which you may use to customize the URL:

```csharp
new TextColumn("title")
    .SetAsUrl(record =>
    {
        return record["url"];
    }),
```

You may also choose to open the URL in a new tab:

```csharp
new TextColumn("title")
    .SetAsUrl(record =>
    {
        return record["url"];
    }, openUrlInNewTab : true),
```


## Hiding columns

To hide a column conditionally, you may use the `SetAsHidden()` and `SetAsVisible()` methods, whichever you prefer:

```csharp
new TextColumn("first_name")
    .SetAsVisible(User.IsTrinityAdmin()),
    
    //or
    
new TextColumn("first_name")
    .SetAsHidden(!User.IsTrinityAdmin()),
```

### Toggling column visibility

Users may hide or show columns themselves in the table. To make a column toggleable, use the `SetAsToggleable()` method:

```csharp
new TextColumn("first_name")
    .SetAsToggleable(),
```

By default, toggleable columns are hidden. To make them visible instead:

```csharp
new TextColumn("first_name")
    .SetAsToggleable(isToggledHiddenByDefault : false),
```

## Tooltips

You may specify a tooltip to display when you hover over a cell:

```csharp
new TextColumn("title")
    .SetTooltip("tooltip for title column!"),
```

This method also accepts a closure that can access the current table record:

```csharp
new TextColumn("title")
    .SetTooltip(record => $"tooltip for ${record["title"]}"),
```

## Custom attributes

The HTML of columns can be customized, by passing an `Dictionary` of attributes to `SetExtraAttributes()`:

```csharp
new TextColumn("title")
    .SetExtraAttributes(record => new Dictionary<string, string>()
    {
        { "class", "bg-gray-200" }
    })
```

These get merged onto the outer `<div>` element in the column.