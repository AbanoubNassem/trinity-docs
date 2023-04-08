---
title: IdColumn
---

IdColumn displays an identifier value:

usually it's:

```csharp
 Make<IdColumn>(PrimaryKeyColumn)
```

but it can be any column:
```csharp
 Make<IdColumn>("some_id")
```

IdColumn is toggleable by default , which means it's hidden by default.