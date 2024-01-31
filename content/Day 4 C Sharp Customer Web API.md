---
title: Day 4 C Sharp Customer Web API
tags:
  - CSharp
  - DotNet
---
Today we will try to make our customized data for web API and push our project on GitHub

Under the project, create a folder call "Entities".
Right click on "Entities" folder, "Add" -> "new item", create a new file call `Customer.cs`

![[Pasted image 20240130225140.png]]

In `Customer.cs`, we can define the data field for our customer data.
like this

```
namespace CustomerAPI.Entities
{
    public class Customer
    {
        public int Id { get; set; }
        public required string Name { get; set; }
        public required string Email { get; set; }
        public string? Phone { get; set; }
        public string? Address { get; set; }
        public string? City { get; set; }

    }
}

```

Next, we need to create a controller file for customer entity

Right click on "Controllers" folder, "Add" -> "Controller"

![[Pasted image 20240130225140.png]]

Then, a pop up window will show up.
Select "API" -> "API Controller - Empty" -> click "Add" button ![[Pasted image 20240130230501.png]]

Select "API Controller - Empty" -> rename the file to `CustomerController.cs` -> click "Add" button 
![[Pasted image 20240130231216.png]]

Visual Studio code will create a empty controller for us

```
`CustomerController.cs`

using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;

namespace CustomerAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ValuesController : ControllerBase
    {
    }
}
```

We can create a get method on it and create a test data for respones.
```
`CustomerController.cs`

using CustomerAPI.Entities;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;

namespace CustomerAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class CustomerController : ControllerBase
    {
        [HttpGet]
        public async Task<IActionResult> GetCustomers() 
        {
            var customers = new List<Customer>
            {
                new Customer
                {
                    Id = 1,
                    Name = "Tony",
                    Email = "tony@gmail.com",
                    Phone = "12345678",
                    Address = "123 home Ave E",
                    City = "Torondo"
                }
            };
            return Ok(customers);
        }
    }
}

```

Ok = status 200

Let see the result on Postman
![[Pasted image 20240130235153.png]]

Yes, we did it.

Assume that we need to push the program on GitHub

Click "Git" on the top left menu -> create a Git repository 
-> login GitHub account -> click "Create and Push" button
![[擷取.jpg]]

Wait for the process ...

![[擷取2.jpg]]

Done.

![[擷取3.jpg]]

![[擷取4.jpg]]