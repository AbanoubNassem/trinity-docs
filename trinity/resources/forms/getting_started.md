---
title: Tables
---
# Tables

Resource classes contain a [TrinityTable](~/api/AbanoubNassem.Trinity.Components.TrinityTable.yml) property that is used to build the table on the listing page.

```csharp
protected override TrinityTable GetTrinityTable()
    {
        return new TrinityTable()
            .SetColumns(new List<ITrinityColumn>()
            {
                new AggregateColumn("store_id")
                    .Counts("store_id", "store")
                    .SetLabel("Abanoub"),

                new TextColumn("first_name"),

                new BelongsToColumn(
                        "store_id.manager_staff_id",
                        "store.staff",
                        "store_id.staff_id",
                        "store.staff",
                        "first_name"
                    )
                    .SetAsSearchable(),
            })
            .SetTopWidgets(new List<ITrinityWidget>()
            {
                new StatsWidget("orders", "100"),
                new StatsWidget("customers", "200")
            })
            .SetBottomWidgets(new List<ITrinityWidget>()
            {
                new StatsWidget("customers", "200")
            })
            .SetActions(new List<ITrinityAction>()
            {
                new TrinityAction("View")
                    .SetSeverity(ActionSeverity.Help)
                    .SetLabel("View")
                    .SetIcon("pi pi-eye")
                    .SetAsUrl("https://google.com", true)
                    .SetHandleActionUsing((_, _) => Task.FromResult(TrinityAction.Redirect("/")))
                    .SetRequiresConfirmation()
            })
            .SetBulkActions(new List<ITrinityAction>()
            {
                new TestAction()
                    .SetLabel("Download")
                    .SetSeverity(ActionSeverity.Info)
                    .SetIcon("pi pi-download")
                    .SetRequiresConfirmation()
                    .SetForm(new TrinityForm().SetSchema(new List<IFormComponent>()
                    {
                        new GridLayout(new List<IFormComponent>()
                        {
                            new TextField("first_name"),
                            new TextField("last_name"),
                        }),
                        new TextField("testing")
                            .SetValidationRules(v=> v.NotEmpty().NotNull())
                    }))
            });
    }
```