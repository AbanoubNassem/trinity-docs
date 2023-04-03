---
title: Branding
---

# Branding

Although `Trinity`'s interface is intended to be an isolated part of your application that is managed by `Trinity`, you can make some small customizations to the branding logo and color used by `Trinity` to make the interface more cohesive with the rest of your application.

## Brand Title
To customize the title used in the `Trinity` interface:
```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.Title = "Trinity";
    });
```
## Brand Prefix
`Trinity` uses `/admin` to prefix all the routes by default , however you can change that:
```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.Prefix = "trinity";
    });
```

## Brand Logo
To customize the logo used at the top left of the `Trinity` interface, you may specify the logo within `Trinity` configurations. This configuration value should contain an absolute path to the image file of the logo you would like to use:

```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.DarkLogo = "url or path";
        configs.WhiteLogo = "url or path";
        configs.FavIcon = "url or path";
    });
```


## Customizing `Trinity`'s Footer
There are times you may wish to customize `Trinity`'s default footer text to include relevant information for your users, such as your application version, IP addresses, or other information. Using the [TrinityConfigurations.Footer](~/api/AbanoubNassem.Trinity.Configurations.TrinityConfigurations.yml#AbanoubNassem_Trinity_Configurations_TrinityConfigurations_Footer), you may customize the footer text of your `Trinity` installation.

```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.Footer = new HtmlString("<div>" +
                                        "This is my custom footer!" +
                                        "</div>");
    });
```


## Customizing `Trinity`'s Progress-indicator
You may want to change the progress indicator color, to match your brand colors, to do so use [TrinityConfigurations.ProgressSettings](~/api/AbanoubNassem.Trinity.Configurations.TrinityConfigurations.yml#AbanoubNassem_Trinity_Configurations_TrinityConfigurations_ProgressSettings):

```csharp
builder.Services
    .AddTrinity(configs =>
    {
        configs.ProgressSettings = new ProgressConfigurations()
        {
            Color = "red", //custom color
            Delay = 250, //custom delay before showing the progress indicator in milliseconds
            ShowSpinner = true,// whether to show a spinner or not
        };
    });
```