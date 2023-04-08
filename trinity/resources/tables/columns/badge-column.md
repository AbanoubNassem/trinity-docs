---
title: Badge column
---

Badge columns render a colored badge with the cell's contents:

```csharp
Make<BadgeColumn>('status')
    .SetOptions(
        ("draft", "Draft"),
        ("reviewing", "Reviewing"),
        ("published", "Published"),
    )
```

## Customizing the color

Badges may have a color. It can be one of [BadgeSeverityType](~/api/AbanoubNassem.Trinity.Columns.BadgeSeverityType.yml):

```csharp
Make<BadgeColumn>('status')   
    .SetOptions(
        ("draft", "Draft", BadgeSeverityType.Info),
        ("reviewing", "Reviewing", BadgeSeverityType.Success),
        ("published", "Published", BadgeSeverityType.Danger)
    )
```

## Adding an icon

Badges may also have an icon:

```csharp
Make<BadgeColumn>('status')   
    .SetOptions(
         ("draft", "Draft", BadgeSeverityType.Info, ""),
         ("reviewing", "Reviewing", BadgeSeverityType.Success, "pi pi-refresh"),
         ("published", "Published", BadgeSeverityType.Danger, "pi pi-truck")
    )
```

## Customizing the size

you may change the badge size. It can be one of [BadgeSizeType](~/api/AbanoubNassem.Trinity.Columns.BadgeSizeType.yml):

```csharp
Make<BadgeColumn>('status')   
    .SetSize(BadgeSizeType.XLarge)
```