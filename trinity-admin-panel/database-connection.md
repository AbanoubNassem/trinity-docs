
## Database Connection

`Trinity` uses [Dapper](https://github.com/DapperLib/Dapper) for manging database connections, and [SQLKata](https://github.com/sqlkata/querybuilder) for handling queries,
therefore `Trinity` is Database agnostic, you can use it with any database provider supported by `Dapper` and `SQLKata`. 


## Configurations

To configure `Trinity` with your database connection provider , add the connection factory :- 

```csharp
var conn = builder.Configuration.GetConnectionString("DefaultConnection");

builder.Services.AddTrinity(configs =>
    {
        configs.ConnectionFactory = () => new MySqlConnection(conn);
    });
```