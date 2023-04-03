---
title: Listing records 
---

# Listing records

## Tables

Resource classes contain a [TrinityTable](~/api/AbanoubNassem.Trinity.Components.TrinityTable.yml) property that is used
to build the table on the listing page.

```csharp
protected override TrinityTable GetTrinityTable()
    {
        return new TrinityTable()
            .SetColumns(new List<ITrinityColumn>()
            {
                // ...
            })
            .SetTopWidgets(new List<ITrinityWidget>()
            {
                // ...
            })
            .SetBottomWidgets(new List<ITrinityWidget>()
            {
                // ...
            })
            .SetActions(new List<ITrinityAction>()
            {
                // ...
            })
            .SetBulkActions(new List<ITrinityAction>()
            {
                // ...
            });
    }
```

## Columns

The `TrinityTable.SetColumns` method is used to define the columns in your table. It is a list of column objects, in the
order they should appear in your table.

`Trinity` has many columns available for your tables, including:

- [AggregateColumn](./columns/aggregate-column.md)
- [BadgeColumn](./columns/badge-column.md)
- [BelongsToColumn](./columns/belongs-to-column.md)
- [ColorColumn](./columns/color-column.md)
- [IconColumn](./columns/icon-column.md)
- [IdColumn](./columns/id-column.md)
- [ImageColumn](./columns/image-column.md)
- [TextColumn](./columns/text-column.md)

You may also build your own completely custom table columns.

## Filters

`Trinity` filters are any form field that allow you to scope your `Trinity` index queries with custom conditions.

by Default the filter is - [TextField](../forms/fields/text-field.md) , when you set the column as searchable, however
you can simply change that:

> [!TIP]
> Setting any column as searchable , will make the `Column` filterable.

```csharp
new TextColumn("first_name")
        .SetAsSearchable() // default Text input field
        
new TextColumn("first_name")
        .SetCustomFilter(new EditorField("test"),
                (query, str) =>
                {
                    query.WhereStarts("t.first_name", str);
                }),
```

> [!TIP]
> Setting the custom filter of any Column, will make the `Column` filterable, and will allow you to alter the query.

## Actions

[Actions](../actions) are buttons that are rendered at the end of table rows. They allow the user to perform a task on a
record in the table.

To add actions to a table, use the `TrinityTable.SetActions()` method:


```csharp
protected override TrinityTable GetTrinityTable()
    {
        return new TrinityTable()
            .SetColumns(new List<ITrinityColumn>()
            {
                // ...
            })
            .SetActions(new List<ITrinityAction>()
            {
                new TrinityAction("View")
                    .SetSeverity(ActionSeverity.Help)
                    .SetLabel("View")
                    .SetIcon("pi pi-eye")
                    .SetAsUrl("https://google.com", true)
            });
    }
```

## Bulk actions

[Bulk actions](../actions#bulk-actions) are buttons that are rendered in the header of the table. They appear when you select records using the checkboxes at the start of each table row. They allow the user to perform a task on multiple records at once in the table.

To add bulk actions, use the `TrinityTable.SetBulkActions()` method:

```csharp
protected override TrinityTable GetTrinityTable()
    {
        return new TrinityTable()
            .SetColumns(new List<ITrinityColumn>()
            {
                // ...
            })
            .SetBulkActions(new List<ITrinityAction>()
            {
                new TrinityAction("download")
                    .SetLabel("Download")
                    .SetSeverity(ActionSeverity.Info)
                    .SetIcon("pi pi-download")
                    .SetRequiresConfirmation()
                    .SetHandleActionUsing((form, records) =>
                    {
                        var results = new List<TrinityActionResult>();
                        foreach (var record in records)
                        {
                            results.Add(TrinityAction.Download(record["file_url"], record["file_name"]));
                        }

                        return Task.FromResult(results);
                    })
            });
    }
```