---
title: Belongs To column
---

## Displaying data from relationships

you can use the simple constructor:
```csharp
new BelongsToColumn(
        columnName: "language_id", 
        foreignColumnToSelect: "name", 
        foreignTable: "language"
    )
```

In this example, `Trinity` will assume that the foreign column is `language_id`, and it will select the column `name` from the table `language` based on the `language_id`

more controlled example:

```csharp
new BelongsToColumn(
        localColumnName: "language_id",
        relationTable: "language",
        foreignColumnName: "language_id",
        foreignColumnToSelect: "name",
        relationshipName: "languages"
    )
```

In this example, `Trinity` won't assume anything rather will use your input, which will give the same result.

## Nested Relationship

You may use "dot syntax" to access nested columns within relationships. 

Assuming we have a `warehouse` table , that has a relation with `store` table on `store_id`, and the `store` table has relationship with `staff` table,  we can select the `store` manager's `first_name`. 

```csharp
new BelongsToColumn(
        localColumnNames: "store_id.manager_staff_id",
        relationTables: "store.staff",
        foreignColumnName: "store_id.staff_id",
        foreignColumnToSelect: "first_name",
        relationshipName: "store_staff"
    )
```

In this example, `Trinity` will select the `first_name` of the manager from `staff.manager_staff_id` where the `staff.store_id` equals to the `warehouse.store_id`.