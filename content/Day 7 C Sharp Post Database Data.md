---
title: Day 7 C Sharp Post Database Data
tags:
  - CSharp
  - DotNet
---
Following **Get Method**, as evident, we will have **Post Method**.

Same as **Get Method**, open `CustomerController.cs`.

Add a `[HttpPost]` route.

```
CustomerController.cs
.
.
.
[HttpPost]
public async Task<ActionResult<Customer>> PostCustomer(Customer customer)
{
    _context.Customers.Add(customer);
    await _context.SaveChangesAsync();
    return Ok(customer);

}


```

In above code, it retrieve a customer json object from **Request body** and return 200 status with that customer json object.

Let see how it work.

Open `Postman`.

![[Pasted image 20240204010953.png]]

Set **Type** to **Post**. 

Go to **Body** section.

Input 

```
{

  "id": 0,

  "name": "Goku",

  "email": "goku@gmail.com",

  "phone": "87654312",

  "address": "shinnjukku 123",

  "city": "Tokyo"

}
```

Column **id** can be igoned since the id will auto generated by the DB.

Result.

![[Pasted image 20240204010335.png]]

You may notice that the respone status is also `200 OK`, but there is a status can be used under this circumstances. Which is `201 Created`.

To do this, we have to modify the `return OK(customer)`.

Like this.

```
.
.
.
[HttpPost]
public async Task<ActionResult<Customer>> PostCustomer(Customer customer)
{
    _context.Customers.Add(customer);
    await _context.SaveChangesAsync();

    return CreatedAtAction(nameof(GetCustomerById), new { id = customer.Id }, customer);

}
```

`CreatedAtAction` is refer to `201 Created`.

Inside the `CreatedAtAction()`, it retrieve the new add record through the `GetCustomerById()` method with the `customer.Id`.

Let's take a look.

![[Pasted image 20240204011831.png]]

Also, the `CustomerDB`.

![[Pasted image 20240204012526.png]]