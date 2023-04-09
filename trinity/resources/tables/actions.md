---
title: Actions
---

# Actions

`Trinity` actions allow you to perform custom tasks on one or more records. For example, you might write an action that sends an email to a user containing account data they have requested. Or, you might write an action to transfer a group of records to another user.

## Single actions

Single action buttons are rendered at the end of each table row.


```csharp
protected override TrinityTable GetTrinityTable()
    {
        return Make<TrinityTable>()
            .SetActions(new List<ITrinityAction>()
            {
                // ...
            })
    }
```
Actions may be created using the `Make<TrinityAction>()` method, passing its name. The name of the action should be unique. You can then pass a callback to `SetHandleActionUsing()` which executes the task, or a callback to `SetAsUrl()` which generates a link URL:

> [!TIP]
> If you would like the URL to open in a new tab, you can use the `SetOpenUrlInNewTab()` method.

```csharp
Make<TrinityAction>("view")
    .SetAsUrl(record => $"/{Configurations.Prefix}/{Name}/edit/{record[PrimaryKeyColumn]}")
    .SetOpenUrlInNewTab()
```

## Bulk actions

Bulk action buttons are visible when the user selects at least one record.

```csharp
protected override TrinityTable GetTrinityTable()
    {
        return Make<TrinityTable>()
            .SetBulkActions(new List<ITrinityAction>()
            {
                // ...
            })
    }
```
> [!NOTE]
> `BulkActions` are basically `Actions` , both will receive :- a submitted form if any, and a list of records, however `BulkActions` will only be visible, if any record is selected.

```csharp
Make<TrinityAction>("download")
        .SetHandleActionUsing((form, record) =>
        {
            return TrinityAction.Download(record["file_url"], record["file_filename"]);
        })
```

## Action Responses

You can customize the response using a variety of methods available via the `TrinityAction` class. To display a custom "success" message, you may invoke the `TrinityAction.Notification` method from your handle method:

```csharp
Make<TrinityAction>("some_action")
        .SetHandleActionUsing((form, record) =>
        {
              //some-action work
            return TrinityAction.Notification(NotificationSeverity.Success, $"It worked!, ${record["name"]} was updated!");
        })
```

## Redirect Responses

```csharp
return TrinityAction::Redirect('https://example.com', openUrlInNewTab: false);
```

## Download Responses

To initiate a file download after the action is executed, you may use the Action::download method. The download method accepts the URL of the file to be downloaded as its first argument, and the desired name of the file as its second argument:

```csharp
return TrinityAction.Download(record["file_url"], record["file_filename"]);
```
## Setting a label

By default, the label of the action is generated from its name. You may customize this using the `SetLabel()` method:

> [!NOTE]
> `Actions` will show a rounded button , and when hovered will show the `Label`, where the `BulkActions` will show a rectangular button with the `Label` inside of it.

```csharp
Make<TrinityAction>("view")
    .SetAsUrl(record => $"/{Configurations.Prefix}/{Name}/edit/{record[PrimaryKeyColumn]}")
    .SetOpenUrlInNewTab()
    .SetLabel("View Record")
```

## Setting a color/severity

Actions may have a color to indicate their significance. use any of [ActionSeverity](~/api/AbanoubNassem.Trinity.Components.TrinityAction.ActionSeverity.yml) options:

```csharp
Make<TrinityAction>("view")
    .SetAsUrl(record => $"/{Configurations.Prefix}/{Name}/edit/{record[PrimaryKeyColumn]}")
    .SetOpenUrlInNewTab()
    .SetLabel("View Record")
    .SetSeverity(ActionSeverity.Primary)
```

## Setting an icon

Single actions may also render, [icons](https://primereact.org/icons/#list) to indicate their purpose:

```csharp
Make<TrinityAction>("view")
    .SetAsUrl(record => $"/{Configurations.Prefix}/{Name}/edit/{record[PrimaryKeyColumn]}")
    .SetOpenUrlInNewTab()
    .SetLabel("View Record")
    .SetSeverity(ActionSeverity.Primary)
    .SetIcon("pi pi-eye")
```

## Modals

Actions and bulk actions may require additional confirmation or form information before they run. You may open a modal before an action is executed to do this.

## Confirmation modals

You may require confirmation before an action is run using the `SetRequiresConfirmation()` method. This is useful for particularly destructive actions, such as those that delete records.

```csharp
Make<TrinityAction>("download")
        .SetHandleActionUsing((form, record) =>
        {
            return TrinityAction.Download(record["file_url"], record["file_filename"]);
        })
        .SetRequiresConfirmation()
```

## Action Modal Customization

By default, actions will ask the user for confirmation before running. You can customize the confirmation message, confirm button, and cancel button to give the user more context before running the action. This is done by calling the `SetConfirmText`, `SetConfirmButtonText`, and `SetCancelButtonText` methods when defining the action:

```csharp
Make<TrinityAction>("active_user")
        .SetHandleActionUsing((form, record) => { 
            //[...]
         })
        .SetRequiresConfirmation()
        .SetConfirmText("Are you sure you want to activate this user?" ,"pi pi-info-circle");
        .SetConfirmButtonText("Activate", "p-button-success");
        .SetCancelButtonText("Don't activate", "pi pi-times");
```

## Custom forms

You may also render a form in this modal to collect extra information from the user before the action runs.

```csharp
Make<TrinityAction>("download")
        .SetForm(new TrinityForm()
            .SetSchema(new List<IFormComponent>()
            {
                Make<GridLayout>(new List<IFormComponent>()
                {
                    Make<TextField>("first_name").SetAsRequired(),
                    Make<TextField>("last_name"),
                }),
                Make<TextField>("testing")
                    .SetValidationRules(v => v.NotEmpty().NotNull())
            })
        )
```

## Authorization

You may conditionally show or hide actions and bulk actions for certain users using either the `SetAsVisible()` or `SetAsHidden()` methods:

```csharp
Make<TrinityAction>("download")
        .SetHandleActionUsing((form, record) =>
        {
            return TrinityAction.Download(record["file_url"], record["file_filename"]);
        })
        .SetAsHidden(!User.IsTrinityAdmin())
```