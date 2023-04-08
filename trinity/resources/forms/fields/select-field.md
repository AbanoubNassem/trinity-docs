---
title: SelectField
---

# SelectField

The select component allows you to select from a list of predefined options:

```csharp
Make<SelectField>("status")
    .SetOptions(new List<KeyValuePair<string, string>>
    {
        new("draft", "Draft"), 
        new("reviewing", "Reviewing"), 
        new("published", "Published")
    })
```

In the `SetOptions()` list, the keys are saved, and the values will be the label of each option in the dropdown.

## Search

You may enable a search input to allow easier access to many options, using the `SetAsSearchable()` method:

```csharp
Make<SelectField>("status")
    .SetOptions(new List<KeyValuePair<string, string>>
    {
        new("draft", "Draft"), 
        new("reviewing", "Reviewing"), 
        new("published", "Published")
    })
    .SetAsSearchable()
```