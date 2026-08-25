# Brunner Mifflin (User)

**Author**: carax49<br>
**Date**: 2026-08-23

## Overview

- Category: Boot2Root
- Description:

```text
You have found the Brunner Mifflin HR system, and your curious nature makes you wonder if you can view all the monsters?
```

## Analysis

The challenge provides the file `UserController.cs`


```c#
using Microsoft.AspNetCore.Mvc;

namespace OrderingApi;

[Route("api/[controller]")]
[ApiController]
public class UserController : ControllerBase
{
    
    [HttpGet("{id}")]
    public IActionResult Get([FromRoute]int id)
    {
        var users = GetUsers();

        if (id < 0 || id > users.Length)
            return NotFound(new { Error = "User not found" });

        return Ok(users[id]);
    }
    
    [HttpGet("Admin/{role}")]
    public IActionResult Get([FromRoute]string role)
    {
        if(role.ToLower() == "itguy")
            return Ok("<REDACTED>");

        return Unauthorized("Only members of IT has access to this dashboard");
    }
}
```

I noticed the following section:

```c#
    [HttpGet("Admin/{role}")]
    public IActionResult Get([FromRoute]string role)
    {
        if(role.ToLower() == "itguy")
            return Ok("<REDACTED>");

        return Unauthorized("Only members of IT has access to this dashboard");
    }
```

So I tried:

```http
GET /api/User/Admin/itguy
```

And the response returned `200 OK`

## Solution

Access the endpoint `/api/User/Admin/itguy`

And I received

```text
To setup e-mail survailance I connect through the IT web terminal at /terminal with my username: itguy and my password: itguy321 <br /> brunner{1tGuyW111F1x}
```


## Flag

```text
brunner{1tGuyW111F1x}
```