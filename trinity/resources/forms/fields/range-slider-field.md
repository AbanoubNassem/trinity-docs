---
title: RangeSliderField
---

# RangeSliderField

> [!TIP]
> `RangeSliderField` inherits all `SliderField` functionalities.

When `RangeSliderField` is used, slider will provide two handles to define two values. In range mode, value should be an array instead of a single value.

```csharp 
Make<RangeSliderField>("length")
    .SetMin(20)
    .SetMax(90)
```
![](../../../../images/range-slider-field.png)