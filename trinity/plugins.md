---
title: Plugins
---

# Plugins

Plugins can be used to extend `Trinity`'s default behaviour and create reusable modules for use in multiple applications.

To create a new plugin, extend the [TrinityPlugin](~/api/AbanoubNassem.Trinity.Plugins.TrinityPlugin.yml) class provided by `Trinity`:

> [!TIP]
> Use [TrinityPluginSample](https://github.com/AbanoubNassem/TrinityPluginSample) to quickly get you going.

```csharp
namespace TrinityPluginSample;

public class PluginSample : TrinityPlugin
{
    public override List<string> GetScriptSources()
    {
        return new List<string>()
        {
            "/main.js"
        };
    }

    public override List<string> GetStyleSources()
    {
        return new List<string>()
        {
            "/style.css"
        };
    }
}
```

## Registering plugins

You don't really need to do anything, `Trinity` will scan the referenced plugins and register it automatically.

> [!NOTE]
> To register any Resource, Page, Field, Column, Widget etc , you have to register the `Frontend` part as well.

## Pages

To register a custom page:-

- First the backend:-
  create a class that inherits [TrinityPage](~/api/AbanoubNassem.Trinity.Pages.TrinityPage.yml).

create a class that inherits [TrinityPage](~/api/AbanoubNassem.Trinity.Pages.TrinityPage.yml).

```csharp
public class CustomPage : TrinityPage
{
    public override string Slug => "custom-page";

    public override string PageView => "PLUGIN_NAME::CustomPage";

    public override object GetData()
    {
        return new List<string>()
        {
            "some",
            "data"
        };
    }
}
```

- Second the frontend, you have to register the `ReactJS` component with `Trinity`:-

```typescript jsx
window.trinityApp.serving((app) => {
    app.registerPage("PLUGIN_NAME::CustomPage", CustomPage);
});

```

> [!NOTE]
> The `PageName` or `ComponentName` -> `PLUGIN_NAME::CustomPage` must match on both backend and frontend , so `Trinity` knows how to serve the component.

### Slug

You can change the page `slug` by overriding the property `Slug`.

```csharp
 public override string Slug => "custom-page";
```

### Data

You can pass any data to the page `slug` by overriding the `GetData()` method.

```csharp
public override object GetData()
    {
        var conn = Configurations.ConnectionFactory();
        //make a query and get data
        var products = conn.Query("get products");
        return new
        {
            list = new List<string>() { "some", "data" },
            products
        };
    }
```

[Check Page Sample](https://github.com/AbanoubNassem/TrinityPluginSample/blob/4aac495d252082d4acb0f1a6976ad955795f3a47/_plugin-frontend/src/custom_page.tsx#L11)

## Field , Column, Widget , etc

- Same as `Page`, but instead of inheriting from `TrinityPage`, you would inherit from the appropriate base class, `TrinityField`, `TrinityColumn`, `TrinityWidget`, etc.
- Use the same `ComponentName` in backend and frontend.

```typescript jsx
window.trinityApp.serving((app) => {
  app.registerComponent: (name: string, component: (props: any) => JSX.Element) => void;
  app.registerLayout: (name: string, component: (props: LayoutProps<TrinityLayout | any>) => JSX.Element) => void;
  app.registerField: (name: string, component: (props: FieldProps<TrinityField | any>) => JSX.Element) => void;
  app.registerColumn: (name: string, component: (props: ColumnProps<TrinityColumn | any>) => JSX.Element) => void;
  app.registerWidget: (name: string, component: (props: WidgetProps<TrinityWidget | any>) => JSX.Element) => void;
  app.registerPage: (name: string, component: (props: PageProps<TrinityPage>) => JSX.Element) => void;
}
```


## Localizations

`Trinity` uses custom `JSON` `Localizer` , we add the localization in the backend, it will be available for the frontend.

> [!TIP]
> All `Trininty` backend components has `Localizer` property, and all the frontend components has `localize` method.

### Create Localizations 

Create a `Dirctory` called `Locale` , inside of it , a `Dirctory` with your plugin name , and there add the locale files, like `en.json`, [refer here for more info](https://github.com/AbanoubNassem/TrinityPluginSample/tree/main/Locales/trinity-sample-plugin)