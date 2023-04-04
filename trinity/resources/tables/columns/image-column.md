---
title: ImageColumn
---

Images can be easily displayed within your table:

```csharp
new ImageColumn("image")
```

The column in the database can contain a relative path to the image, or a `URL`.

## Square image

You may display the image using a 1:1 aspect ratio:

```csharp
new ImageColumn("image")
    .SetAsSquare()
```

## Circular image

You may make the image fully rounded, which is useful for rendering avatars:

```csharp
new ImageColumn("image")
    .SetAsCircular()
```
## Customizing the size

You may customize the image size by passing a `SetWidth()` and `SetHeight()`:

```csharp
new ImageColumn("image")
    .SetWidth("200px")
    .SetHeight("50px")
```

## Previewable image

You may make the image previewable in a modal, to see the whole image:

```csharp
new ImageColumn("image")
    .SetAsPreviewable()
```

## Downloadable image

You may make the image Downloadable , so you can download the image:

```csharp
new ImageColumn("image")
    .SetAsDownloadable()
```

