---
title: Day 5 C Database Connection
tags:
  - CSharp
  - DotNet
---
Today we will try to get connection to **Microsoft SQL Server** and **create a CustomerDB** for our API data.

First, we need to create a `DataContext.cs` file under `Data` Folder.
![[Pasted image 20240202003830.png]]

```
`DataContext.cs`

using CustomerAPI.Entities;
using Microsoft.EntityFrameworkCore;

namespace CustomerAPI.Data
{
    public class DataContext:DbContext
    {
        public DataContext(DbContextOptions<DataContext> options) : base(options)
        {
            
        }

        public DbSet<Customer> Customers { get; set; }
    }
}

```

Before using the class `DbContext`, we need to install a package called `Microsoft.EntityFrameworkCore`.

To install it, we select `Tools` from the top right bar.

Select `NuGet Package Manager` > `Manage NuGet Packages for Solution...`
![[Pasted image 20240202004242.png]]

A NuGet Solution window will show up.
Select `Microsoft.EntityFrameworkCore` > select your project > click install.
![[Pasted image 20240202004928.png]]

Actually, we have 2 more package to install, there are `Microsoft.EntityFrameworkCore.SqlServer` and `Microsoft.EntityFrameworkCore.Tools`.

Follow the above step to install them.
![[Pasted image 20240202005544.png]]

Move on to set the connection String, open `appsettings.json` under the project.

Add "ConnectionStrings" item on top of it and type the Server and Database informaion base on your case.
```
`appsettings.json`

{
  "ConnectionStrings": {
    "DefaultConnection" : "Server=.;Database=CustomerDB;Trusted_Connection=true;TrustServerCertificate=true;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}

```

After that, go to `Program.cs`. 

Add the code to connect `SQL server` by the `ConnectionStrings` we just added.

```
.
.
.

builder.Services.AddDbContext<DataContext>(options =>
{
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"));
});

.
.
.

```

![[Pasted image 20240202010724.png]]

Open `Package Manager Console`.
![[Pasted image 20240202010948.png]]

Type `Add-Migration initial` in the console to create a Migration file.

![[Pasted image 20240202011338.png]]

`Migrations` folder we be created automatically.

![[Pasted image 20240202011519.png]]

At this point, all the stuff we need to connect to the SQL server is ready.

Before we connect, make sure you have already install the 
`Microsoft SQP Server` and `SQL Server Management Studio (SSMS)`.

You can choose to download the lastest version of these software and find the installation guide online.

Finally, we can use the migration file to update the Database.

Go back to `Package Manager Console`.

Type `Update-Database`.

If success to connect, it will show something like this.
![[Pasted image 20240202012408.png]]

If you facing this error
`Only the invariant culture is supported in globalization-invariant mode. See https://aka.ms/GlobalizationInvariantMode for more information. (Parameter 'name')`
`en-us is an invalid culture identifier.`

![[Pasted image 20240202012500.png]]

You can go to InvariantGlobalization to **false** under this file.
![[Pasted image 20240202012628.png]]

Now, we can check if the `CustomerDB` is built or not.
Open `SQL Server Management Studio (SSMS)` and connect to the `Microsoft SQP Server`.

![[Pasted image 20240202013001.png]]

We did it!!