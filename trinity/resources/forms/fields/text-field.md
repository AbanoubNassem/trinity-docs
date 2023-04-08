---
title: TextField
---
# TextField

The text input allows you to interact with a string:

```csharp
Make<TextField>("first_name")
```

## Length

You may limit the length of the input by setting the `SetMinLength`() and `SetMaxLength`() methods. These methods add both frontend validation only:

```csharp
Make<TextField>("last_name")
    .SetMinLength(4)
    .SetMaxLength(32)
```

