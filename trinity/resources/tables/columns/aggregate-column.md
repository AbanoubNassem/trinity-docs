---
title: AggregateColumn
---
# AggregateColumn

## Counting relationships

If you wish to count the number of related records in a column, you may use the `Counts()` method:

```csharp
Make<AggregateColumn>("user_id")
    .Counts(
        foreignKeyColumn: "id", 
        foreignTable: "users" 
    )
```

In this example, `users` is the name of the table to count from. where the `users`.`id` equals the column `user_id`

## Aggregating relationships

`Trinity` provides several methods for aggregating a relationship column, including `Average()`, `Max()`, `Min()` and `Sum()`. For instance, if you wish to show the average of a column on all related records in a table, you may use the `Average()` method:

```csharp
Make<AggregateColumn>("user_id")
    .Average(
        foreignKeyColumn: "id", 
        foreignTable: "users",
        foreignColumnToAverage : "age"
    )
```

In this example, `users` is the name of the table to `Average` the `age` from. where the `users`.`id` equals the column `user_id`
