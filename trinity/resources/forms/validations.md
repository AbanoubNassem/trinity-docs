---
title: Validations
---

# Form Validation

`Trinity` uses [FluentValidation](https://docs.fluentvalidation.net/) under the hood.
So basically use `FluentValidation` on any `TrinityField`.

```csharp
Make<TextField>("first_name")
    .SetValidationRules(rules =>
        rules.NotEmpty()
            .NotNull()
            .MinimumLength(6)
    ),
```
You may use the [Built-in Validators](https://docs.fluentvalidation.net/en/latest/built-in-validators.html) or create your own [Custom Validators](https://docs.fluentvalidation.net/en/latest/custom-validators.html)