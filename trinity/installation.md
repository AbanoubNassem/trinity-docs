---
title: Installation
---
## Requirements

Trinity requires .Net-Core 6+ to run.


## Installation

To get started with the admin panel, you can install it using the command:

Trinity is available on [NuGet](https://www.nuget.org/packages/Trinity/) , [GitHub](https://github.com/AbanoubNassem/Trinity)

```bash
dotnet add package AbanoubNassem.Trinity
```

Then add the following to your `Program.cs`

```csharp
using AbanoubNassem.Trinity.Extensions;

[...]

builder.Services.AddTrinity();

[...]

app.UseTrinity();
```