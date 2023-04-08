---
title: TextAreaField
---

# TextAreaField

`TextAreaField` allows you to interact with a multi-line string:

```csharp
Make<TextAreaField>("description")
```

## Properties

You can use `SetTextAreaProperties` method to customize the properties :

```csharp
Make<TextAreaField>("description")
    .SetTextAreaProperties(
    autoResize : true, 
    rows : 5, 
    cols : 30
 )
```