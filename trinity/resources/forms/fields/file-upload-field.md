---
title: FileUploadField
---

# FileUploadField

## File upload

The file upload field is based on [Filepond](https://pqina.nl/filepond).

```csharp
Make<FileUploadField>("image")
```

![](../../../../images/file-upload.png)

By default, files will be uploaded publicly to `wwwroot/trinity_public`.

## Upload location/directory

To change the directory that files are saved in, use the `SetUploadDirectory()` method:

```csharp
Make<FileUploadField>("image")
    .SetUploadDirectory("somewhere")
```

## Multiple files

You may also upload multiple files. This stores URLs in text seperated by `,`:

```csharp
Make<FileUploadField>("attachments")
    .SetAsMultiple()
```

> [!CAUTION]
> Please note, it is the responsibility of the developer to delete these files from the disk if they are removed,
> as `Trinity` is unaware if they are depended on elsewhere.

## File types

You may restrict the types of files that may be uploaded using the `SetFileTypes()` method, and passing an array of MIME
types. You may also use the `SetAsImage()` method as shorthand to allow all image MIME types.

```csharp
Make<FileUploadField>("document")
    .SetFileTypes("application/pdf" , "text")
    
Make<FileUploadField>("image")
    .SetAsImage()
```

## File size

You may also restrict the size of uploaded files, in bytes:

```csharp
Make<FileUploadField>("image")
    .SetAsImage()
    .SetMinimumFileSize(512000) // 512kb
    .SetMaximumFileSize(1024000) // 1024kb
```

## Image resizing

Filepond allows you to crop and resize images before they are uploaded. You can customize this behaviour using
the [`SetImageResizeMode(ImageResizeModeType.Contain)`](~/api/AbanoubNassem.Trinity.Fields.ImageResizeModeType.yml), `SetImageCropAspectRatio()`, `SetImageResizeTargetHeight()`
and `SetImageResizeTargetWidth()` methods.

```csharp
Make<FileUploadField>("image")
    .SetAsImage()
    .SetMinimumFileSize(512000) // 512kb
    .SetMaximumFileSize(1024000) // 1024kb
    .SetImageResizeMode(ImageResizeModeType.Cover)
    .SetImageCropAspectRatio("16:9")
    .SetImageResizeTargetWidth(1920)
    .SetImageResizeTargetHeight(1080)
```

## Style

You may also alter the general appearance of the Filepond component. Available options for these methods are available on the [Filepond website](https://pqina.nl/filepond/docs/api/instance/properties/#styles).

```csharp
use Filament\Forms\Components\FileUpload;

Make<FileUploadField>('attachment')
    .SetImagePreviewHeight('250')
    .SetLoadIndicatorPosition('left')
    .SetPanelAspectRatio('2:1')
    .SetPanelLayout(PanelLayoutType.Integrated)
    .SetRemoveUploadedFileButtonPosition('right')
    .SetButtonProcessItemPosition('left')
    .SetUploadProgressIndicatorPosition('left')
```

## Download

If you wish to add a download button to each file, you can use the `SetCanDownload()` method:

```csharp
Make<FileUploadField>("image")
    .SetAsImage()
    .SetCanDownload()
```