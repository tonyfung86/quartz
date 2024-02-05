---
title: Day 8 C Sharp Put & Delete Database Data
tags:
  - CSharp
  - DotNet
---
After **Get and Post method**, we will learn the last two method, they are **Put and Delete method**.

**Put method**

Open `CustomerController.cs`.

```
`CustomerController.cs`.
.
.
.
[HttpPut]
public async Task<ActionResult<Customer>> PutCustomer(int id, Customer customer)
{
    if (id != customer.Id)
    {
        return BadRequest();
    }

    _context.Entry(customer).State = EntityState.Modified;

    try
    {
        await _context.SaveChangesAsync();
    }
    catch (DbUpdateConcurrencyException) 
    {
        if (!CustomerExists(id)) { return NotFound(); }
        else { throw; }
    }

    return NoContent();
}

private bool CustomerExists(int id)
{
    return (_context.Customers?.Any(customer => customer.Id == id)).GetValueOrDefault();
}
```

Open `Postman`.

`Put method` means to edit the data, it required am id from the request **URL** and the data from **request body**. According to the **HTTP** specification, a **PUT** request the client to submit the complete updated entity, which is mandatory, but not only the data to be modified.

![[Pasted image 20240205015432.png]]

![[Pasted image 20240205015642.png]]

The response for this is **204** **(No Content).**

**Delete method**

Open `CustomerController.cs`.

```
`CustomerController.cs`.
.
.
.
[HttpDelete("{id}")]
public async Task<ActionResult<Customer>> DeleteCustomer(int id)
{
    if(_context.Customers == null)
    {
        return NotFound();
    }
    var customer = await _context.Customers.FindAsync(id);
    if (customer == null) 
    {
        return NotFound();
    }
    _context.Customers.Remove(customer);
    await _context.SaveChangesAsync();
    return NoContent();
}
```

Open `Postman`.

![[Pasted image 20240205015905.png]]

![[Pasted image 20240205020323.png]]