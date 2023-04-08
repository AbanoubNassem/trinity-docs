---
title: BelongsToField
---
# BelongsToField

You may use the `BlenogsToField` to show html `<select/>` and configure a `BelongsTo` relationship to automatically retrieve and save options from:

```csharp
Make<BelongsToField>(
   columnName: "address_id", 
   foreignColumnToSelect: "address", 
   foreignTable: "address"
 )
```

In this example, `Trinity` will assume that the foreign column is `address_id`, and it will select the column `address` from the table `address` based on the `address_id`

more controlled example:

```csharp
Make<BelongsToField>(
        localColumnName: "address_id",
        relationTable: "address",
        foreignColumnName: "address_id",
        foreignColumnToSelect: "address",
        relationshipName: "addresses"
    )
```

In this example, `Trinity` won't assume anything rather will use your input, which will give the same result.

## Nested Relationship

You may use "dot syntax" to access nested columns within relationships.

Assuming we have a `warehouse` table , that has a relation with `store` table on `store_id`, and the `store` table has relationship with `staff` table,  we can select the `store` manager's `first_name`.

```csharp
Make<BelongsToField>(
        localColumnNames: "store_id.manager_staff_id",
        relationTables: "store.staff",
        foreignColumnName: "store_id.staff_id",
        foreignColumnToSelect: "first_name",
        relationshipName: "store_staff"
    )
```

In this example, `Trinity` will show html `<select/>` of the `first_name` of the manager from `staff.manager_staff_id` where the `staff.store_id` equals to the `warehouse.store_id`.