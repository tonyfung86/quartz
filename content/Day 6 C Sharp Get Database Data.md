---
title: Day 6 C Sharp Get Database Data
tags:
  - CSharp
  - DotNet
---
In Day5, we successed to connect Microsoft Sql server and created a `CustomerDB`.

Naturally, we will try to get the data from database and use it for API.

Open `SQL Server Management Studio (SSMS)`.

Expand `Database Diagrams`>expand `Table`>right click on `dbo.Customer` >`Edit Top 200 Rows`

![[Pasted image 20240202231935.png]]

Create 2 record

![[Pasted image 20240202232342.png]]

Go back to `Visual Studio`.

Open `CustomerController.cs`
![[Pasted image 20240202232644.png]]

```
CustomerController.cs

using CustomerAPI.Data;
using CustomerAPI.Entities;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace CustomerAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class CustomerController : ControllerBase
    {
        private readonly DataContext _context;
        
        public CustomerController(DataContext context) {
            
            _context = context;
            
        }

        [HttpGet]
        public async Task<IActionResult> GetCustomers() 
        {
            
            var customers = await _context.Customers.ToListAsync();
	        
            return Ok(customers);
        }
        
    }
}
```

We can test it on `Postman`

Success!

![[Pasted image 20240202233549.png]]

What if we just want to get 1 specific record only?

We can specify a `id` in the Route.

```
CustomerController.cs

using CustomerAPI.Data;
using CustomerAPI.Entities;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;

namespace CustomerAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class CustomerController : ControllerBase
    {
        private readonly DataContext _context;

        public CustomerController(DataContext context) {
            
            _context = context;

        }

        [HttpGet]
        public async Task<IActionResult> GetCustomers() 
        {

            var customers = await _context.Customers.ToListAsync();
            
            return Ok(customers);
        }

        [HttpGet("{id}")]
        public async Task<IActionResult> GetCustomerById(int id)
        {
            var customers = await _context.Customers.FindAsync(id);
            if(customers == null)
            {
                return BadRequest("Customer not found");
            }

            return Ok(customers);
        }
    }
}

```

We use `[HttpGet("{id}")]` to retrieve the id from the URL and to get the record from `CustomerDB` by the id.

And we also have to checking if the record if valid or not.

If the record is not found, return a `BadRequest(400)` or `NotFound(404)`.

Let test it on `Postman`.

Success!

![[Pasted image 20240202234736.png]]

Also the not found respond.

![[Pasted image 20240202234916.png]]