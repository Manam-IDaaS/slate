---
title: Manam API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Manam API! You can use our API to access Manam API endpoints, which is a IDaaS and can register, login, conform, recover, Google Login oauth2.

We have language bindings in Shell (for shell use httpie (https://httpie.org/) ), and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Manam

Manam is IDaaS (Identity as a service).

## Register [IDaaS]


```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "Accept-Language":"en-ca,en;q=0.8,en-us;" https://api.apieco.ir/manam/auth/register -d '{"type":"[email|mobile]","confirm_url":"https://tenant.com/confirm","firstname": "myyfirstname","lastname":"mylastname","email": "myemail@gmail.com","password":"12345","confirm_password":"12345","national_code":"12907652",birthday:"1370-01-03"}'

```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/auth/register",
    headers: {
                'apieco_key': '<apieco_key>',
                "Accept-Language":"en-ca,en;q=0.8,en-us;"
         
            },
    dataType: "json",
    type : "POST",
    data: {
    "type":"[email|mobile]",
    "tenant_confirm_url": "https://tenant.com/confirm",
    "tenant_email": "info@tenant.com" // obliging when userType is "email"
    "firstname":"firstname",
    "lastname":"lastname"
    "email":"myemail@mail.com",// obliging when userType is "email"
    "mobile":"09111087815", // obliging when userType is "mobile"
    "mobile_seed":"+98"
    "password":"password",
    "confirm_password":"password", 
    "national_code":"12907652", 
    "bithday":"1370-01-03",
    "role":"admin"
    "custome_fields":[{"phone":"887219031":"address":"Tehran"}]
     }
    success : function(r) {
      console.log(r);
    }
  });
```

> The above command returns JSON structured like this:

```json

{
    "access_token": "...",    
    "email":"myemail@mail.com",// required when type is "email"
    "tenant_email": "info@tenant.com" // required when type is "email"
    "tenant_confirm_url":"tenant.com/tenant" //required
    "mobile":"09111087815", // required when type is "mobile"
    "mobile_seed":"+98",        
    "firstname":"firstname",
    "lastname":"lastname",    
    "national_code":"12907652", 
    "birthday":"1990-04-05",
    "role": "",
    "custome_fields":[{"phone":"887219031":"address":"Tehran"}]
    "oauth2_provider":"",
    "oauth2_user_info":[]
}

```

This endpoint register user in Manam.

### HTTP Request

`POST https://api.apieco.ir/manam/auth/register`

### Query Parameters
None.


### Data Params

Parameter | Type    | Description
--------- | ------- | ---------------
type* | string | email or mobile
email+ |[string] | required when type is "email"
mobile+|[number] | required when type is "mobile"
mobile_seed+|[number] | required when type is "mobile"
tenant_email+| [string] |  required when type is "email"
tenant_confirm_url* | string | 
password* | [string] | 
confirm_password* | string |
firstname| string |
lastname | string |
birthday | date |
custome_fields | string |
oauth2_provider | string | example : google , facebook, github , ...
oauth2_user_info | string |


## Confirm Email  [IDaaS]

```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" , -H "Accept-Language":"en-ca,en;q=0.8,en-us;" https://api.apieco.ir/manam/auth/confirm_email -d {cnf:"h-A1iPysWfQ9Mj5EYuCKZo9KJ5UccHTjqABqfL-8bw48fkUQAOhBB-Bbwo2V7AE5TKYYYE9QXpDLrCvImQ57Tw=="}
```

```javascript
$.ajax({
    url: "  https://api.apieco.ir/manam/auth/confirm_email?cnf=FFL5QDOYTXJZcO3SdcDgd8Kv-_euyLqVwm-eFagHZG_KCBLgtyhUkjFAeeDXvMFVVame3vXKyiWbnpNAVxQI8A==,
    headers: {
                "apieco_key":"<apieco_key>",
                "Accept-Language":"en-ca,en;q=0.8,en-us;"
            },
    dataType: "json",
    type : "GET",
    success : function(r) {
      console.log(r);
    }
  });
```

> The above command returns JSON structured like this:

if status code is 200:
```json
{
"location": "/",
"message": "You have successfully confirmed your account.",
"status": "success"
}
```
if status code is 401:

```json
{
"location": "/",
"message": "Your confirmation is unsuccess",
"status": "unsuccess"
}
```

This endpoint confirm users on Manam.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.apieco.ir/manam/auth/confirm_email/<cnf>`

### URL Parameters

Parameter | Description
--------- | -----------
cnf | The string that confirm registartion



## Confirm SMS  [IDaaS]

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/confirm_sms -d {cnf:"1237hsak"}
```

```javascript
$.ajax({
    url: "  https://api.apieco.ir/manam/auth/confirm_sms
    headers: {
                "apieco_key":"<apieco_key>"
            },
    dataType: "json",
    type : "POST",
    data:{cnf:"1237hsak"}
    success : function(r) {
      console.log(r);
    }
  });
```

> The above command returns JSON structured like this:

```json
{
"location": "/",
"message": "You have successfully confirmed your account.",
"status": "success"
}
```

This endpoint confirm users on Manam.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.apieco.ir/manam/auth/confirm_email/<cnf>`

### URL Parameters

Parameter | Description
--------- | -----------
cnf | The string that confirm registartion



## Send Confirm Email  [IDaaS]

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/send_confirm_email -d {userTpe:"email","email":"user@test.com","tenant_email":"info@tenant.com",confirm_url:"tenant.com/confirm"}
```

```javascript
  
  //user type email
$.ajax({
    url: "  https://api.apieco.ir/manam/auth/send_confirm_email
    headers: {
                "apieco_key":"<apieco_key>"
            },
    dataType: "json",
    type : "POST",
    data:{"email":"user@test.com","tenant_email":"info@tenan.com",tenant_confirm_url:"tenant.com/confirm"}
    success : function(r) {
      console.log(r);
    }
  });

  
  
```

> The above command returns JSON structured like this:

if status code is 200:
```json
{
"location": "/",
"message": "You have successfully confirmed your account.",
"status": "success"
}
```
if status code is 401:
```json
{
"location": "/",
"message": "Your confirmation is unsuccess.",
"status": "unsuccess"
}
```

This endpoint send new confirmation for mobile users on Manam.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.apieco.ir/manam/auth/new_confirm_sms/<cnf>`

### URL Parameters

Parameter | Description
--------- | -----------
mobile* | string
confirm_url*| string



## Send Confirm SMS  [IDaaS]

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/send_confirm_sms -d {"mobile":"09171929716",confirm_url:"tenant.com/confirm"}
```

```javascript
//user type mobile
$.ajax({
    url: "  https://api.apieco.ir/manam/auth/send_confirm_sms
    headers: {
                "apieco_key":"<apieco_key>",
                "Accept-Language":"en-ca,en;q=0.8,en-us;"
            },
    dataType: "json",
    type : "POST",
    data:{"mobile":"09171929716",confirm_url:"tenant.com/confirm"}
    success : function(r) {
      console.log(r);
    }
  }); 
  
```

> The above command returns JSON structured like this:

if status code is 200:
```json
{
"location": "/",
"message": "You have successfully confirmed your account.",
"status": "success"
}
```
if status code is 401:
```json
{
"location": "/",
"message": "Your confirmation is unsuccess.",
"status": "unsuccess"
}
```

This endpoint send new confirmation for mobile users on Manam.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.apieco.ir/manam/auth/new_confirm_sms/<cnf>`

### URL Parameters

Parameter | Description
--------- | -----------
mobile* | string
confirm_url*| string


## Login [IDaaS]



```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/login -d '{"type":"[email|mobile]","email": "myemail@mail.com","password":"password"}'

```

```javascript
 $.ajax({
    url: "https://api.apieco.ir/manam/auth/login",
    headers: {                
                "apieco_key":"<apieco_key>",
                "Accept-Language":"en-ca,en;q=0.8,en-us;"
            },
    dataType: "json",
    type : "POST",
    data: { "type":"email",email:"myemail@mail.com", password:"password"}
    success : function(r) {
      console.log(r);
    }
  });
```

> The above command returns JSON structured like this:

```json
{
    
    "access_token": "...",    
    "email":"myemail@mail.com",// required when type is "email"
    "tenant_email": "info@tenant.com" // required when type is "email"
    "tenant_confirm_url":"tenant.com/tenant" //required
    "mobile":"09111087815", // required when type is "mobile"
    "mobile_seed":"+98",        
    "firstname":"firstname",
    "lastname":"lastname",    
    "national_code":"12907652", 
    "birthday":"1990-04-05",
    "roles": [],
    "custome_fields":[{"phone":"887219031":"address":"Tehran"}]
    "oauth2_provider":"",
    "oauth2_user_info":[]
}


```

This endpoint login user on Manam.

### HTTP Request

`POST https://api.apieco.ir/manam/auth/login`

### URL Parameters

None.


### Data Parameters

Parameter | Description
--------- | -----------
type | email or mobile
email | The email that register 
password | The password to login


## Register two factor authentication via Time-Based One Time Passwords(totp) (Enable) [IDaaS]

You should use two factor authentication in your application if you want additional security beyond that of just simple passwords. Each 2fa module supports a different mechanism for verifying a second factor of authentication from a user.

Tip:
* You have to be login to enable 2fa (two factor authentication)

### step1 :Login:
```shell
http -p BHbh POST localhost:3000/auth/login -H "apieco_key:<apieco_key>" email="test@test.com" password="1234"

```

> The above return this output for Login: (use this cookie for the next step)
```shell
POST /auth/login HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 46
Content-Type: application/json
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "email": "test@test.com",
    "password": "1234"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 35
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:44:45 GMT
Set-Cookie: csrf_token=2FL0EDK4UIN5lDaidm8GzoYvim0QCHoi4iF/ZdMF6S0=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTQ4NXxEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXw43TZdnSFlWDi8BNoOHAUmbk7WnKt-jnml5Vgmn5bpuA==; Path=/; Expires=Mon, 23 Sep 2019 22:44:45 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/",
    "status": "success"
}
```

### step 2: Verify Email
This step use cookie from previous step and set code param with email.

```shell
http -p BHbh POST  localhost:3000/auth/2fa/totp/email/verify code="test@test.com" Cookie:"ab_blog=MTU2OTIzNTQ4NXxEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXw43TZdnSFlWDi8BNoOHAUmbk7WnKt-jnml5Vgmn5bpuA==;"
```
> The above return this output and send verify link to email.

```shell
POST /auth/2fa/totp/email/verify HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 25
Content-Type: application/json
Cookie: ab_blog=MTU2OTIzNTQ4NXxEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXw43TZdnSFlWDi8BNoOHAUmbk7WnKt-jnml5Vgmn5bpuA==;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "test@test.com"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 98
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:45:39 GMT
Set-Cookie: csrf_token=jiK/MlwuO87gfl8f5Wb6bAs14L4+Wn4BVsyXefFZswo=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTUzOXxEdi1CQkFFQ180SUFBUkFCRUFBQWJQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRmdBVWRIZHZabUZqZEc5eVgyRjFkR2hmZEc5clpXNEdjM1J5YVc1bkRCb0FHRlY1WlZwSWVXRTJVVVU1YVdWeVRreFNORkpMVDNjOVBRPT18IKd27uBfVMg8-MnO6VVlUVVD3uky5cqg7j27N_oVerE=; Path=/; Expires=Mon, 23 Sep 2019 22:45:39 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/",
    "message": "An e-mail has been sent to confirm 2FA activation.",
    "status": "success"
}

```

### step 3: Verify Email by Link

This step verfy link that be send to email. (use cookie from previous step )

```shell
http -p BHbh GET  localhost:3000/auth/2fa/totp/email/verify/end token="UyeZHya6QE9ierNLR4RKOw=="  Cookie:"ab_blog=MTU2OTIzNTUzOXxEdi1CQkFFQ180SUFBUkFCRUFBQWJQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRmdBVWRIZHZabUZqZEc5eVgyRjFkR2hmZEc5clpXNEdjM1J5YVc1bkRCb0FHRlY1WlZwSWVXRTJVVVU1YVdWeVRreFNORkpMVDNjOVBRPT18IKd27uBfVMg8-MnO6VVlUVVD3uky5cqg7j27N_oVerE=;"
```

> The above return this output.

```shell
GET /auth/2fa/totp/email/verify/end HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 37
Content-Type: application/json
Cookie: ab_blog=MTU2OTIzNTUzOXxEdi1CQkFFQ180SUFBUkFCRUFBQWJQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRmdBVWRIZHZabUZqZEc5eVgyRjFkR2hmZEc5clpXNEdjM1J5YVc1bkRCb0FHRlY1WlZwSWVXRTJVVVU1YVdWeVRreFNORkpMVDNjOVBRPT18IKd27uBfVMg8-MnO6VVlUVVD3uky5cqg7j27N_oVerE=;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "token": "UyeZHya6QE9ierNLR4RKOw=="
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 54
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:46:58 GMT
Set-Cookie: csrf_token=ZeFOZQUXU1XnGWLVIQ4eBAVXQeVz3oKojUIihZyvfnQ=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTYxOHxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fMwDt2Jx4Bgb9hMDwaaukcbwaJ0l83nwIpeko8z9FD3s; Path=/; Expires=Mon, 23 Sep 2019 22:46:58 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/auth/2fa/totp/setup",
    "status": "success"
}

```

### step 4: Set up with Get

This step and the next step are the background for preparation and display QR code. (use cookie from previous step )

```shell
http -p BHbh GET  localhost:3000/auth/2fa/totp/setup Cookie:"ab_blog=MTU2OTIzNTYxOHxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fMwDt2Jx4Bgb9hMDwaaukcbwaJ0l83nwIpeko8z9FD3s;"
```

> The above return this output.

```shell
GET /auth/2fa/totp/setup HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Cookie: ab_blog=MTU2OTIzNTYxOHxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fMwDt2Jx4Bgb9hMDwaaukcbwaJ0l83nwIpeko8z9FD3s;
Host: localhost:3000
User-Agent: HTTPie/0.9.8



HTTP/1.1 200 OK
Content-Length: 343
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:48:16 GMT
Set-Cookie: csrf_token=GddII5bFs+aXE8zrX4RQaF2VexgV/7tRqqqrt0X9sD4=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTY5NnxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fNm_r3aZEXm8OWkG6TLLQHnv5HXfbH7phcmZBq2sjDC1; Path=/; Expires=Mon, 23 Sep 2019 22:48:16 GMT; Max-Age=43200
Vary: Cookie

{
    "csrf_token": "KCIeoVA3ZFmKIpdO4GmGebpFezo7njGYd3Hx22wWxKUx9VaCxvLXvx0xW6W/7dYR59AAIi5hisnd21psKet0mw==",
    "current_user_name": "myyname",
    "flash_error": "",
    "flash_success": "",
    "loggedin": true,
    "modules": {
        "auth": true,
        "confirm": true,
        "lock": true,
        "logout": true,
        "oauth2": true,
        "otp": true,
        "recover": true,
        "register": true,
        "remember": true
    },
    "status": "success"
}

```

### step 5: Set up with POST

This step and the previous step are the background for preparation and display QR code. (use cookie from previous step )

```shell
http -p BHbh POST  localhost:3000/auth/2fa/totp/setup Cookie:"ab_blog=MTU2OTIzNTY5NnxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fNm_r3aZEXm8OWkG6TLLQHnv5HXfbH7phcmZBq2sjDC1;"
```

> The above return this output.

```shell
POST /auth/2fa/totp/setup HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 0
Cookie: ab_blog=MTU2OTIzNTY5NnxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fNm_r3aZEXm8OWkG6TLLQHnv5HXfbH7phcmZBq2sjDC1;
Host: localhost:3000
User-Agent: HTTPie/0.9.8



HTTP/1.1 302 Found
Content-Length: 0
Date: Mon, 23 Sep 2019 10:48:56 GMT
Location: /auth/2fa/totp/confirm
Set-Cookie: csrf_token=2u4T82qTkXUJyI04Gp/X0fQYLiKFVUqQelVI2g4JXOs=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTczNnxEdi1CQkFFQ180SUFBUkFCRUFBQV81WF9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVTFHUzFFelJVVlpWRW8zVnpKRFdVTlBWMWhEVjFWWVdqSkNRMUpTVjBrR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01Ed0FOZEdWemRFQjBaWE4wTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXyhpO-zAeTtkJ6Fes8_LNLJG5dtsYSBuwCKlmR9k3EQdw==; Path=/; Expires=Mon, 23 Sep 2019 22:48:56 GMT; Max-Age=43200
Vary: Cookie

```

### step 6: Set up with POST

This step and the previous step are the background for preparation and display QR code. (use cookie from previous step )

```shell
http -p BHbh POST  localhost:3000/auth/2fa/totp/setup Cookie:"ab_blog=MTU2OTIzNTY5NnxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fNm_r3aZEXm8OWkG6TLLQHnv5HXfbH7phcmZBq2sjDC1;"
```

> The above return this output.

```shell
POST /auth/2fa/totp/setup HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 0
Cookie: ab_blog=MTU2OTIzNTY5NnxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fNm_r3aZEXm8OWkG6TLLQHnv5HXfbH7phcmZBq2sjDC1;
Host: localhost:3000
User-Agent: HTTPie/0.9.8



HTTP/1.1 302 Found
Content-Length: 0
Date: Mon, 23 Sep 2019 10:48:56 GMT
Location: /auth/2fa/totp/confirm
Set-Cookie: csrf_token=2u4T82qTkXUJyI04Gp/X0fQYLiKFVUqQelVI2g4JXOs=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTczNnxEdi1CQkFFQ180SUFBUkFCRUFBQV81WF9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVTFHUzFFelJVVlpWRW8zVnpKRFdVTlBWMWhEVjFWWVdqSkNRMUpTVjBrR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01Ed0FOZEdWemRFQjBaWE4wTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXyhpO-zAeTtkJ6Fes8_LNLJG5dtsYSBuwCKlmR9k3EQdw==; Path=/; Expires=Mon, 23 Sep 2019 22:48:56 GMT; Max-Age=43200
Vary: Cookie


```


### step 7: Display QR code

This step display QR code and user have to scan QR code and use code from that that change every minutues. (use cookie from previous step )

```shell
http -p BHbh GET  localhost:3000/auth/2fa/totp/qr Cookie:"ab_blog=MTU2OTIzNTczNnxEdi1CQkFFQ180SUFBUkFCRUFBQV81WF9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVTFHUzFFelJVVlpWRW8zVnpKRFdVTlBWMWhEVjFWWVdqSkNRMUpTVjBrR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01Ed0FOZEdWemRFQjBaWE4wTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXyhpO-zAeTtkJ6Fes8_LNLJG5dtsYSBuwCKlmR9k3EQdw==;"
```

> The above return this output.

```shell
GET /auth/2fa/totp/qr HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Cookie: ab_blog=MTU2OTIzNTczNnxEdi1CQkFFQ180SUFBUkFCRUFBQV81WF9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVTFHUzFFelJVVlpWRW8zVnpKRFdVTlBWMWhEVjFWWVdqSkNRMUpTVjBrR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01Ed0FOZEdWemRFQjBaWE4wTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXyhpO-zAeTtkJ6Fes8_LNLJG5dtsYSBuwCKlmR9k3EQdw==;
Host: localhost:3000
User-Agent: HTTPie/0.9.8



HTTP/1.1 200 OK
Content-Length: 1390
Content-Type: image/png
Date: Mon, 23 Sep 2019 10:50:07 GMT
Set-Cookie: csrf_token=b3GLiRKaeE6quSYoJtn9+qozPwQDGXUkdRR1eGNKs0k=; Max-Age=31536000
Vary: Cookie



+-----------------------------------------+
| NOTE: binary data not shown in terminal |
+-----------------------------------------+


```

Note : In shell can not show birnay data use browser or other tools like POSTMAN.


### step 8: Confirm and get recovery Code

This step use code from QR code that setup in mobile app or other ways from previous step and get recovery code. (use cookie from previous step )

```shell
http -p BHbh POST  localhost:3000/auth/2fa/totp/confirm code="396259" Cookie:"ab_blog=MTU2OTIzNTczNnxEdi1CQkFFQ180SUFBUkFCRUFBQV81WF9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVTFHUzFFelJVVlpWRW8zVnpKRFdVTlBWMWhEVjFWWVdqSkNRMUpTVjBrR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01Ed0FOZEdWemRFQjBaWE4wTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXyhpO-zAeTtkJ6Fes8_LNLJG5dtsYSBuwCKlmR9k3EQdw=="
```

> The above return this output.

```shell
POST /auth/2fa/totp/confirm HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 18
Content-Type: application/json
Cookie: ab_blog=MTU2OTIzNTczNnxEdi1CQkFFQ180SUFBUkFCRUFBQV81WF9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVTFHUzFFelJVVlpWRW8zVnpKRFdVTlBWMWhEVjFWWVdqSkNRMUpTVjBrR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01Ed0FOZEdWemRFQjBaWE4wTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXyhpO-zAeTtkJ6Fes8_LNLJG5dtsYSBuwCKlmR9k3EQdw==
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "396259"
}

HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:52:53 GMT
Set-Cookie: csrf_token=cOZlegLkkp2P3eBkoy1WPc43x6CjMk2tRO3JagRZxqU=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTk3M3xEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRWdBUWRIZHZabUZqZEc5eVgyRjFkR2hsWkFaemRISnBibWNNQmdBRWRISjFaUT09fFaWSRTIhAEDaUUMCQWkvh_h7DzheUMIXythE_yEhrpV; Path=/; Expires=Mon, 23 Sep 2019 22:52:53 GMT; Max-Age=43200
Vary: Cookie

{
    "csrf_token": "PJAr2TFAiuCChIODd2C+P8CZLJm+Mjg1sBQRXUOY3GNMdk6jM6QYfQ1ZY+fUTegCDq7rOR0AdZj0+dg3R8Eaxg==",
    "current_user_name": "myyname",
    "flash_error": "",
    "flash_success": "",
    "loggedin": true,
    "modules": {
        "auth": true,
        "confirm": true,
        "lock": true,
        "logout": true,
        "oauth2": true,
        "otp": true,
        "recover": true,
        "register": true,
        "remember": true
    },
    "recovery_codes": [
        "qh7eg-78iii",
        "2i56t-26sma",
        "ipnjp-hoa7r",
        "ohkmj-uamj3",
        "q51ut-tb9n5",
        "jvacz-vd21u",
        "5gf63-7x7dc",
        "khb8f-6wucy",
        "ue647-9vqqk",
        "9k8mu-f62gs"
    ],
    "status": "success"
}

```

## Login two factor authentication via Time-Based One Time Passwords (totp) [IDaaS]

You should use two factor authentication in your application if you want additional security beyond that of just simple passwords. Each 2fa module supports a different mechanism for verifying a second factor of authentication from a user.

### step1 : Login via password
```shell
http -p BHbh POST localhost:3000/auth/login -H "apieco_key:<apieco_key>" email="test@test.com" password="1234"

```

> The above return this output for Login: (use this cookie for the next step)

```shell
POST /auth/login HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 46
Content-Type: application/json
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "email": "test@test.com",
    "password": "1234"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 57
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:53:13 GMT
Set-Cookie: csrf_token=jmmT9/4pPYwSKslwmrV5t6SRZBlmM7hSWvh4hLs7csM=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNTk5M3xEdi1CQkFFQ180SUFBUkFCRUFBQU1fLUNBQUVHYzNSeWFXNW5EQTRBREhSdmRIQmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXwG4MkM6K4ldMpRxUE8mSfBWRCt_pxcHTt8TTqamXaCSA==; Path=/; Expires=Mon, 23 Sep 2019 22:53:13 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/auth/2fa/totp/validate",
    "status": "success"
}

```

### step2: validate with code and verify code
This command use to authenticate in 2fa visa toyp. (set cookie from previouse step)
code and recovery_code params are described in previous part (code comes from sms and recovery_code comes from confirm step).

```shell
http -p BHbh POST  localhost:3000/auth/2fa/totp/validate code="622153" recovery_code="qh7eg-78iii" Cookie:"ab_blog=MTU2OTIzNTk5M3xEdi1CQkFFQ180SUFBUkFCRUFBQU1fLUNBQUVHYzNSeWFXNW5EQTRBREhSdmRIQmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXwG4MkM6K4ldMpRxUE8mSfBWRCt_pxcHTt8TTqamXaCSA==;"
```

> The above return this output.

```shell
POST /auth/2fa/totp/validate HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 50
Content-Type: application/json
Cookie: ab_blog=MTU2OTIzNTk5M3xEdi1CQkFFQ180SUFBUkFCRUFBQU1fLUNBQUVHYzNSeWFXNW5EQTRBREhSdmRIQmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXwG4MkM6K4ldMpRxUE8mSfBWRCt_pxcHTt8TTqamXaCSA==;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "622153",
    "recovery_code": "qh7eg-78iii"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 74
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:56:16 GMT
Set-Cookie: csrf_token=8iFQbRUx6q8n8l4UrCyHtGZYakTNBfPd74PK1236/+g=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNjE3NnxEdi1CQkFFQ180SUFBUkFCRUFBQVRmLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNQ3dBSmRIZHZabUZqZEc5eUJuTjBjbWx1Wnd3R0FBUjBiM1J3fC2Q-SnGpsB5B-Spyo1tRtrhJokNfxxBpvPKdB_59zaJ; Path=/; Expires=Mon, 23 Sep 2019 22:56:16 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/",
    "message": "Successfully Authenticated",
    "status": "success"
}
```


## Remove two factor authentication via totp (Disable) [IDaaS]

User can remove 2fa.
Tips:
1. set cookie from Login step
2.code and recovery_code params are described in previous part (code comes from QR code scanner that change every minutes and recovery_code comes from confirm step).


```shell

http -p BHbh POST localhost:3000/auth/2fa/totp/remove code="114381" recovery_code="2i56t-26sma" Cookie:"ab_blog=MTU2OTIzNjE3NnxEdi1CQkFFQ180SUFBUkFCRUFBQVRmLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNQ3dBSmRIZHZabUZqZEc5eUJuTjBjbWx1Wnd3R0FBUjBiM1J3fC2Q-SnGpsB5B-Spyo1tRtrhJokNfxxBpvPKdB_59zaJ;"
```

> The above return this output.

```shell
POST /auth/2fa/totp/remove HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 50
Content-Type: application/json
Cookie: ab_blog=MTU2OTIzNjE3NnxEdi1CQkFFQ180SUFBUkFCRUFBQVRmLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNQ3dBSmRIZHZabUZqZEc5eUJuTjBjbWx1Wnd3R0FBUjBiM1J3fC2Q-SnGpsB5B-Spyo1tRtrhJokNfxxBpvPKdB_59zaJ;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "114381",
    "recovery_code": "2i56t-26sma"
}

HTTP/1.1 200 OK
Content-Length: 343
Content-Type: application/json
Date: Mon, 23 Sep 2019 10:58:57 GMT
Set-Cookie: csrf_token=QuZTwCF8KTTdaVXEmUS21MVC6DfOzJvOfQsxO2Ev0pE=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTIzNjMzN3xEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXx7_OwN5f_ZuxcTnCXg033zd0_LbNUBoBDI6vrpjpRQ5w==; Path=/; Expires=Mon, 23 Sep 2019 22:58:57 GMT; Max-Age=43200
Vary: Cookie

{
    "csrf_token": "T2EapDfZeQ1wZxNjNcjJVJ2tgNsTajPDMbhzYnOSWHYNh0lkFqVQOa0ORqesjH+AWO9o7N2mqA1Ms0JZEr2K5w==",
    "current_user_name": "myyname",
    "flash_error": "",
    "flash_success": "",
    "loggedin": true,
    "modules": {
        "auth": true,
        "confirm": true,
        "lock": true,
        "logout": true,
        "oauth2": true,
        "otp": true,
        "recover": true,
        "register": true,
        "remember": true
    },
    "status": "success"
}

```





## Register two factor authentication via SMS (Enable) [IDaaS]

You should use two factor authentication in your application if you want additional security beyond that of just simple passwords. Each 2fa module supports a different mechanism for verifying a second factor of authentication from a user.

Tip:
* You have to be login to enable 2fa (two factor authentication)


### step1 :Login:
```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/login -d '{"email": "test@gmail.com","password":"12345","type":"email"}'

```

> The above return this output for Login: (use this cookie for the next step)

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/login HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 63
> 
* upload completely sent off: 63 out of 63 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=aiHP5mKPv3t8ufveaE2isuc7vr8teZuzMc+S3tfOCTQ=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTY5ODcxN3xEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRPT18q0sHMSHjZt7ADMGIlJBxWcj24xtY2bm6AMoYYkREuFI=; Path=/; Expires=Sun, 29 Sep 2019 07:25:17 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 19:25:17 GMT
< Content-Length: 344
< 
* Connection #0 to host localhost left intact
{"access_token":"","birthday":"","custome_fields":"\u003cinvalid Value\u003e","email":"test15@gmail.com","firstname":"ali","lastname":"lastname","location":"/","mobile":"\u003cinvalid Value\u003e","mobile_seed":"\u003cinvalid Value\u003e","national_code":"","role":"","status":"success","tenant_confirm_url":"","tenant_email":"","type":"email"}
```

### step2: verify code by email
This command send and email to verify email.

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v --cookie "ab_blog=MTU2OTY5ODcxN3xEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRPT18q0sHMSHjZt7ADMGIlJBxWcj24xtY2bm6AMoYYkREuFI=;" localhost:3000/auth/2fa/sms/email/verify -d '{"Code":"test@gmail.com"}'

```

> The above return this output and send email to verify.

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/sms/email/verify HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTY5ODcxN3xEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRPT18q0sHMSHjZt7ADMGIlJBxWcj24xtY2bm6AMoYYkREuFI=;
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 27
> 
* upload completely sent off: 27 out of 27 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=IAkehPBhXxjm2QZvqVv4x6z+QwljsfpffeKquvxYxkw=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTY5ODgyMHxEdi1CQkFFQ180SUFBUkFCRUFBQWJfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUZnQVVkSGR2Wm1GamRHOXlYMkYxZEdoZmRHOXJaVzRHYzNSeWFXNW5EQm9BR0ZoT1JFWXlRVk50VFc1c1ZtcFlibUZJUVhWM04xRTlQUT09fNk_hWEgtbU5b66gDIb5zgxHevAeTmQTp-PGcQxEyruC; Path=/; Expires=Sun, 29 Sep 2019 07:27:00 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 19:27:00 GMT
< Content-Length: 98
< 
* Connection #0 to host localhost left intact
{"location":"/","message":"An e-mail has been sent to confirm 2FA activation.","status":"success"}
```


### step3: verify email by token

This command check token to verify email. (set cookie from previouse step)

```shell
curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v --cookie "ab_blog=MTU2OTY5ODgyMHxEdi1CQkFFQ180SUFBUkFCRUFBQWJfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUZnQVVkSGR2Wm1GamRHOXlYMkYxZEdoZmRHOXJaVzRHYzNSeWFXNW5EQm9BR0ZoT1JFWXlRVk50VFc1c1ZtcFlibUZJUVhWM04xRTlQUT09fNk_hWEgtbU5b66gDIb5zgxHevAeTmQTp-PGcQxEyruC;" localhost:3000/auth/2fa/sms/email/verify/end -d '{"token":"XNDF2ASmMnlVjXnaHAuw7Q=="}'

```

> The above return this output.

```shell
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> GET /auth/2fa/sms/email/verify/end HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTY5ODgyMHxEdi1CQkFFQ180SUFBUkFCRUFBQWJfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUZnQVVkSGR2Wm1GamRHOXlYMkYxZEdoZmRHOXJaVzRHYzNSeWFXNW5EQm9BR0ZoT1JFWXlRVk50VFc1c1ZtcFlibUZJUVhWM04xRTlQUT09fNk_hWEgtbU5b66gDIb5zgxHevAeTmQTp-PGcQxEyruC;
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 36
> 
* upload completely sent off: 36 out of 36 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=cNV9KGod3ARjt4tMafKyQcliH8lMrsxPvkTad74OTac=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTY5ODkyNnxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXw7Di416VQ-kG3rd-t1cYEr4ht6KNIUDduvud4Se2YfcA==; Path=/; Expires=Sun, 29 Sep 2019 07:28:46 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 19:28:46 GMT
< Content-Length: 53
< 
* Connection #0 to host localhost left intact
{"location":"/auth/2fa/sms/setup","status":"success"}

```

### Step 4 : Set up Phone number to get Code
This command send a code to phone number this code is one of the factors in 2fa to login. (set cookie from previouse step)

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v --cookie "ab_blog=MTU2OTY5ODkyNnxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXw7Di416VQ-kG3rd-t1cYEr4ht6KNIUDduvud4Se2YfcA==" localhost:3000/auth/2fa/sms/setup -d '{"phone_number":"93562717380"}'
```

> The above return this output.

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/sms/setup HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTY5ODkyNnxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXw7Di416VQ-kG3rd-t1cYEr4ht6KNIUDduvud4Se2YfcA==
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 30
> 
* upload completely sent off: 30 out of 30 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=e7bbc7/0ZRVJNKPKux9c3PBeklRTWd6Cipa6WoZ6kTE=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTY5OTAzMnxEdi1CQkFFQ180SUFBUkFCRUFBQV85RF9nZ0FGQm5OMGNtbHVad3dGQUFOMWFXUUdjM1J5YVc1bkRCSUFFSFJsYzNReE5VQm5iV0ZwYkM1amIyMEdjM1J5YVc1bkRCSUFFSFIzYjJaaFkzUnZjbDloZFhSb1pXUUdjM1J5YVc1bkRBWUFCSFJ5ZFdVR2MzUnlhVzVuREF3QUNuTnRjMTl1ZFcxaVpYSUdjM1J5YVc1bkRBMEFDemt6TlRZeU56RTNNemd3Qm5OMGNtbHVad3dLQUFoemJYTmZiR0Z6ZEFaemRISnBibWNNREFBS01UVTJPVFk1T1RBek1nWnpkSEpwYm1jTURBQUtjMjF6WDNObFkzSmxkQVp6ZEhKcGJtY01DQUFHTWpJME16Z3d8ycJy0h7IEVRfA3UycamPYNpfevSiGekXrbtHpMrB7kI=; Path=/; Expires=Sun, 29 Sep 2019 07:30:32 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 19:30:32 GMT
< Content-Length: 55
< 
* Connection #0 to host localhost left intact
{"location":"/auth/2fa/sms/confirm","status":"success"}
```

### Step5: Confirm Code and get recovery code 

This command get recovery code. This is another factors in 2fa to login. (set cookie from previouse step)
Param code send in phone number.

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v --cookie "ab_blog=MTU2OTY5OTAzMnxEdi1CQkFFQ180SUFBUkFCRUFBQV85RF9nZ0FGQm5OMGNtbHVad3dGQUFOMWFXUUdjM1J5YVc1bkRCSUFFSFJsYzNReE5VQm5iV0ZwYkM1amIyMEdjM1J5YVc1bkRCSUFFSFIzYjJaaFkzUnZjbDloZFhSb1pXUUdjM1J5YVc1bkRBWUFCSFJ5ZFdVR2MzUnlhVzVuREF3QUNuTnRjMTl1ZFcxaVpYSUdjM1J5YVc1bkRBMEFDemt6TlRZeU56RTNNemd3Qm5OMGNtbHVad3dLQUFoemJYTmZiR0Z6ZEFaemRISnBibWNNREFBS01UVTJPVFk1T1RBek1nWnpkSEpwYm1jTURBQUtjMjF6WDNObFkzSmxkQVp6ZEhKcGJtY01DQUFHTWpJME16Z3d8ycJy0h7IEVRfA3UycamPYNpfevSiGekXrbtHpMrB7kI=" localhost:3000/auth/2fa/sms/confirm -d '{"code":"224380"}'
```

> The above return this output.

```shellNote: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/sms/confirm HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTY5OTAzMnxEdi1CQkFFQ180SUFBUkFCRUFBQV85RF9nZ0FGQm5OMGNtbHVad3dGQUFOMWFXUUdjM1J5YVc1bkRCSUFFSFJsYzNReE5VQm5iV0ZwYkM1amIyMEdjM1J5YVc1bkRCSUFFSFIzYjJaaFkzUnZjbDloZFhSb1pXUUdjM1J5YVc1bkRBWUFCSFJ5ZFdVR2MzUnlhVzVuREF3QUNuTnRjMTl1ZFcxaVpYSUdjM1J5YVc1bkRBMEFDemt6TlRZeU56RTNNemd3Qm5OMGNtbHVad3dLQUFoemJYTmZiR0Z6ZEFaemRISnBibWNNREFBS01UVTJPVFk1T1RBek1nWnpkSEpwYm1jTURBQUtjMjF6WDNObFkzSmxkQVp6ZEhKcGJtY01DQUFHTWpJME16Z3d8ycJy0h7IEVRfA3UycamPYNpfevSiGekXrbtHpMrB7kI=
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 17
> 
* upload completely sent off: 17 out of 17 bytes
< HTTP/1.1 200 OK
< Content-Type: application/json
< Set-Cookie: csrf_token=BqPUBoT/7WAxcWLRyp6DMoOpf3IA0juviUw2FmN2owI=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTY5OTQ2OHxEdi1CQkFFQ180SUFBUkFCRUFBQWZfLUNBQU1HYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlFaemRISnBibWNNQ2dBSWMyMXpYMnhoYzNRR2MzUnlhVzVuREF3QUNqRTFOamsyT1Rrd016ST187es9m_dP25911C7XvnONBZBMstQ-sq6EzvbAjmAl0Rc=; Path=/; Expires=Sun, 29 Sep 2019 07:37:48 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 19:37:48 GMT
< Content-Length: 548
< 
* Connection #0 to host localhost left intact
{"csrf_token":"LzAXe82z9C6YEgkLLQ/I1HG6EozqNZlEod0cALaF0Fopk8N9SUwZTqlja9rnkUvm8hNt/urnousokSoW1fNzWA==","current_user_name":"","flash_error":"","flash_success":"","loggedin":true,"modules":{"auth":true,"auth-custom":true,"confirm":true,"lock":true,"logout":true,"oauth2":true,"recover":true,"recover-custom":true,"register":true,"register-custom":true,"remember":true},"recovery_codes":["i5sr9-r8f27","svu0c-tu0jm","wbjsn-jxn4n","m0yyt-c0un9","uiadp-mhznb","9m8in-vuwdk","h41cv-xp4ca","khfmr-gfzti","4cvtc-9kf2g","d364p-h71mz"],"status":"success"}

```


## Login two factor authentication via SMS [IDaaS]

You should use two factor authentication in your application if you want additional security beyond that of just simple passwords. Each 2fa module supports a different mechanism for verifying a second factor of authentication from a user.


### step1 : Login via password
```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/login -d '{"email": "test@gmail.com","password":"12345","type":"email"}'
```

> The above return this output for Login: (use this cookie for the next step)

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/login HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 63
> 
* upload completely sent off: 63 out of 63 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=JpirzjYRGTjJSWgY3iaiykWpGBfYC2JHeTZW6MKVg90=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTcwMzcxNXxEdi1CQkFFQ180SUFBUkFCRUFBQV80UF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUNnQUljMjF6WDJ4aGMzUUdjM1J5YVc1bkRBd0FDakUxTmprM01ETTNNVFVHYzNSeWFXNW5EQXdBQ25OdGMxOXpaV055WlhRR2MzUnlhVzVuREFnQUJqUTJORFkxTlE9PXxkXEBe1CwJ62xrTiTmvWGNQKB4Irbc8nV7Nx9ZIepWBA==; Path=/; Expires=Sun, 29 Sep 2019 08:48:35 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 20:48:35 GMT
< Content-Length: 365
< 
* Connection #0 to host localhost left intact
{"access_token":"","birthday":"","custome_fields":"\u003cinvalid Value\u003e","email":"test@gmail.com","firstname":"ali","lastname":"lastname","location":"/auth/2fa/sms/validate","mobile":"\u003cinvalid Value\u003e","mobile_seed":"\u003cinvalid Value\u003e","national_code":"","role":"","status":"success","tenant_confirm_url":"","tenant_email":"","type":"email"}
```

### step2: validate with code and verify code
This command use to authenticate in 2fa visa SMS. (set cookie from previouse step)
code and recovery_code params are described in previous part (code comes from sms and recovery_code comes from confirm step).

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -v --cookie "ab_blog=MTU2OTcwMzcxNXxEdi1CQkFFQ180SUFBUkFCRUFBQV80UF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUNnQUljMjF6WDJ4aGMzUUdjM1J5YVc1bkRBd0FDakUxTmprM01ETTNNVFVHYzNSeWFXNW5EQXdBQ25OdGMxOXpaV055WlhRR2MzUnlhVzVuREFnQUJqUTJORFkxTlE9PXxkXEBe1CwJ62xrTiTmvWGNQKB4Irbc8nV7Nx9ZIepWBA==;" localhost:3000/auth/2fa/sms/validate -d '{"code":"224380","recovery_code":"i5sr9-r8f27"}'
```

> The above return this output for Login: (use this cookie for the next step)

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/sms/validate HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTcwMzcxNXxEdi1CQkFFQ180SUFBUkFCRUFBQV80UF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUNnQUljMjF6WDJ4aGMzUUdjM1J5YVc1bkRBd0FDakUxTmprM01ETTNNVFVHYzNSeWFXNW5EQXdBQ25OdGMxOXpaV055WlhRR2MzUnlhVzVuREFnQUJqUTJORFkxTlE9PXxkXEBe1CwJ62xrTiTmvWGNQKB4Irbc8nV7Nx9ZIepWBA==;
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> Content-Length: 47
> 
* upload completely sent off: 47 out of 47 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=oNgdwQKLrGhC+A5iSLRSmZMheKK9/U508czNt62aa7Y=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTcwMzg3NnxEdi1CQkFFQ180SUFBUkFCRUFBQWRfLUNBQU1HYzNSeWFXNW5EQW9BQ0hOdGMxOXNZWE4wQm5OMGNtbHVad3dNQUFveE5UWTVOekF6TnpFMUJuTjBjbWx1Wnd3RkFBTjFhV1FHYzNSeWFXNW5EQklBRUhSbGMzUXhOVUJuYldGcGJDNWpiMjBHYzNSeWFXNW5EQXNBQ1hSM2IyWmhZM1J2Y2daemRISnBibWNNQlFBRGMyMXp8xbl_yMOkW10ponO4hLDZ3zo18YCMl_GM_7wIPUrKgfg=; Path=/; Expires=Sun, 29 Sep 2019 08:51:16 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sat, 28 Sep 2019 20:51:16 GMT
< Content-Length: 74
< 
* Connection #0 to host localhost left intact
{"location":"/","message":"Successfully Authenticated","status":"success"}
```

## Remove two factor authentication via SMS (Disable) [IDaaS]

User can remove 2fa.
Tips:
1. set cookie from Login step
2.code and recovery_code params are described in previous part (code comes from sms and recovery_code comes from confirm step).


```shell

curl -X POST -H "Content-Type: application/json" -H "X-Consumer-ID:kiss_customer" -H "user_type:email" -v --cookie ""ab_blog=MTU2OTcwMzcxNXxEdi1CQkFFQ180SUFBUkFCRUFBQV80UF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUNnQUljMjF6WDJ4aGMzUUdjM1J5YVc1bkRBd0FDakUxTmprM01ETTNNVFVHYzNSeWFXNW5EQXdBQ25OdGMxOXpaV055WlhRR2MzUnlhVzVuREFnQUJqUTJORFkxTlE9PXxkXEBe1CwJ62xrTiTmvWGNQKB4Irbc8nV7Nx9ZIepWBA==;" localhost:3000/auth/2fa/sms/remove -d '{"code":"224380","recovery_code":"h41cv-xp4ca"}'

```

> The above return this output.

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/sms/remove HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTczNzAzNHxEdi1CQkFFQ180SUFBUkFCRUFBQWRfLUNBQU1HYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUN3QUpkSGR2Wm1GamRHOXlCbk4wY21sdVp3d0ZBQU56YlhNR2MzUnlhVzVuREFvQUNITnRjMTlzWVhOMEJuTjBjbWx1Wnd3TUFBb3hOVFk1TnpNMk9UWTN88eZJP4-UKCFdIUsOvrpFQkV1QsWkH1_6t1x_ePBwkh8=;
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 47
> 
* upload completely sent off: 47 out of 47 bytes
< HTTP/1.1 200 OK
< Content-Type: application/json
< Set-Cookie: csrf_token=5jzL8V/RILT4kZrwrHgzYGYLQjzlehK6EHzAB/x+F/o=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTczNzA5MnxEdi1CQkFFQ180SUFBUkFCRUFBQVZmLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUNnQUljMjF6WDJ4aGMzUUdjM1J5YVc1bkRBd0FDakUxTmprM016WTVOamM9fMx0mVj8uNfqUjiFEz55Owmk1tCTQO9ifz35PKjmxES2; Path=/; Expires=Sun, 29 Sep 2019 18:04:52 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 06:04:52 GMT
< Content-Length: 389
< 
* Connection #0 to host localhost left intact
{"csrf_token":"Ow8w6jDD9J3KBsKN4MYOpPxBpY7BG2AlSLpTxo85OLndM/sbbxLUKTKXWH1Mvj3EmkrnsiRhcp9YxpPBc0cvQw==","current_user_name":"","flash_error":"","flash_success":"","loggedin":true,"modules":{"auth":true,"auth-custom":true,"confirm":true,"lock":true,"logout":true,"oauth2":true,"recover":true,"recover-custom":true,"register":true,"register-custom":trueH "user_type:email" -v  localhost:3000/auth/login -d '{"email": "test15@gmail.com","password":"12345","type":"email"}'

```






## Recover [IDaaS]

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/recover -d '{"type":"[email|mobile]","email": "myemail@mail.com"}'


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/auth/recover",
    headers: {
                "apieco_key":"<apieco_key>",
                
            
              
            },
    dataType: "json",
    type : "POST",
    data: { "type":"email","email":"myemail@mail.com"}
    success : function(r) {
      console.log(r);
    }
  });
  ```

> The above command returns JSON structured like this:

if status code is 200:
```json
{"location":"/",
"message":"An email has been sent to you with further instructions on how to reset your password.",
"status":"success"
}
```
if status code is 401:
```json
{
"location": "/",
"message": "There is an error here to recover password.",
"status": "unsuccess"
}
```


This endpoint recover user on Manam.

### HTTP Request

`POST https://api.apieco.ir/manam/auth/recover`

### URL Parameters

None.

### Data Parameters

Parameter | Description
--------- | -----------
type | email or mobile
email | The email that register 



## Change Password [IDaaS]

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/recover/end -d '{"token":"...","password":"...","confirm_password":"..."}'


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/auth/changepassword",
    headers: {
                "apieco_key":"<apieco_key>",
                
            
              
            },
    dataType: "json",
    type : "GET",
    data: { token":"...","password":"...","confirm_password":"..."}
    success : function(r) {
      console.log(r);
    }
  });
  ```

> The above command returns JSON structured like this:

if status code is 200:
```json
{
"location": "/",
"message": "Your password chaneg successfully",
"status": "success"
}
```
if status code is 401:
```json
{"csrf_token":"H0tNRAn1wDgtHOJKuoNOSwDtLAE2XgUiizt4aLukbRNuh8cnXbDr9HA9nB9kzpIRAcyRGsaroMCGw5L/jc6Icw==",
"current_user_name":"",
"errors":{"":["recovery token is invalid"]},"flash_error":"","flash_success":"","loggedin":false,"modules":{"auth":true,"auth-custom":true,"confirm":true,"confirm-custom":true,"lock":true,"logout":true,"oauth2":true,"recover":true,"recover-custom":true,"register":true,"register-custom":true,"remember":true},"status":"failure"}
```


This endpoint recover user on Manam.

### HTTP Request

`POST https://api.apieco.ir/manam/auth/recover`

### URL Parameters

None.

### Data Parameters

Parameter | Description
--------- | -----------
type | email or mobile
email | The email that register 





## Refresh Token [IDaaS]


```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "auth_token:eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI4NjYsImV4cCI6MTQ0NDI2Mjg4Nn0.Dww7TC-d0teDAgsmKHw7bhF2THNichsE6rVJq9xu_2s" -H "access_token:fdb8fdbecf1d03ce5e6125c067733c0d51de209c" https://api.apieco.ir/manam/auth/refreshToken 


```

> The above command returns JSON structured like this:

```json
{
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI4NjYsImV4cCI6MTQ0NDI2Mjg4Nn0.Dww7TC-d0teDAgsmKHw7bhF2THNichsE6rVJq9xu_2s",
    "expires_in":20,
    "access_token":"7fd15938c823cf58e78019bea2af142f9449696a"
}
```

This endpoint RefreshToken create new refresh token for users.

## View User [IDaaS]

```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/view_user/<email>


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/view_user",
    headers: {
                "apieco_key":"<apieco_key>"
                
            },
    dataType: "json",
    type : "GET",
    success : function(r) {
      console.log(r);
    }
  });
  ```

> The above command returns JSON structured like this:

```json
{
  {"email":"...",
  "meli_code":"...",
  "picture":"...",
  "address":"...",
  "postal_code":"...",
  "birthday":"...",
  "marital_status":"...",
  "facebook_id":"...",
  "instagram_id":"...",
  "twitter_id":"...",
  "linkedIn_id":"...",
  "document":"...",
  "mobile":"...",
  "telephone":"..."}'
}
```

This endpoint display user info user.

### HTTP Request

`POST https://api.apieco.ir/manam/auth/recover`

### URL Parameters

None.

### Data Parameters

Parameter | Description
--------- | -----------
email | The email that register 




## Edit User [IDaaS]

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/edit_user -d '{"userType":"[email|mobile]","email":"mytest@gmail.com","melicode":"12344", "picture":"butypic","address":"address", "postal_code":"posss","birthday":"1990-02-01","marital_status":"single","facebook_id":"facebook_id","instagram_id":"instagram_id","twitter_id":"twitter_id","linkedIn_id":"linkedIn_id","document":"document1","mobile":"091223423","telephone":"091383184"}'


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/edit_user",
    headers: {
                "apieco_key":"<apieco_key>"
                
            },
    dataType: "json",
    type : "POST",
    data: {
            "userType":"[email|mobile]",
            "email":"mytest@gmail.com",
           "melicode":"12344",
           "picture":"butypic",
           "address":"address",
           "postal_code":"posss",
           "birthday":"1990-01-02",
           "marital_status":"single",
           "facebook_id":"facebook_id",
           "instagram_id":"instagram_id",
           "twitter_id":"twitter_id",
           "linkedIn_id":"linkedIn_id",
           "document":"document1",
           "mobile":"091223423",
           "telephone":"091383184"}
    success : function(r) {
      console.log(r);
    }
  });
  ```

> The above command returns JSON structured like this:

```json
{
  {"email":"...","Name":"..."}'
}
```

This endpoint edit user information.

### HTTP Request

`POST https://api.apieco.ir/manam/edit_user`

### URL Parameters

None.

### Data Parameters

Parameter | Description
--------- | -----------
email* | The email that register 
userType*|[email|mobile]
melicode |
picture | 
address | 
postal_code | 
birthday | 
marital_status |
facebook_id | 
instagram_id |
twitter_id |
linkedIn_id | 
document | 
mobile | 
telephone | 


## Google Login (oauth2)[IDaaS]
Use this link `<a href="https://api.apieco.ir/manam/googlelogin/[apieco_key]">Google Log In</a>`

Contact to admin for give customer-token

> The above command returns JSON structured like this:

```json
{
    "access_token": "...",
    "username": "",
    "fullname": "",
    "email": "",
    "roles": [],
    "permissions": []
    //... other user info
}


```





## Get Manam User Info [Manam]


```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/get_manam_user_info/<email>

```

> The above command returns JSON structured like this:

```json

{
        "email":"...",
        "meli_code":"...",
        "picture":"...",
        "address":"...",
        "postal_code":"...",
        "birthday":"...",
        "marital_status":"...",
        "facebook_id":"...",
        "instagram_id":"...",
        "twitter_id":"...",
        "linkedIn_id":"...",
        "document":"...",
        "mobile":"...",
        "telephone":"..."
   
}

```
or for google users
```json
{
        "ageRanges":"",
				"CoverPhotos":""
				"Photos":"",
				"Locales":"",
	      //name
				"DisplayName":"",
				"FamilyName":"",
				"GivenName":"",
				"DisplayNameLastFirst":"",
				//birthday
				"BirthdayDay":"",
				"BirthdayMonth":"",
				"BirthdayYear":"",
				"Email":"",
   
}

```


This endpoint display Manam user information.

### HTTP Request

`GET https://api.apieco.ir/manam/auth/get_manam_user_info/<email>`


### Data Params
None.


### Query Parameters

Parameter | Type 
--------- | ------- 
email | [string] *


## Login with Manam [Manam]


```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/manamlogin

```

> The above command returns JSON structured like this:

```json

{
        "email":"...",
        "meli_code":"...",
        "picture":"...",
        "address":"...",
        "postal_code":"...",
        "birthday":"...",
        "marital_status":"...",
        "facebook_id":"...",
        "instagram_id":"...",
        "twitter_id":"...",
        "linkedIn_id":"...",
        "document":"...",
        "mobile":"...",
        "telephone":"..."
   
}

```
or for google users
```json
{
        "ageRanges":"",
				"CoverPhotos":""
				"Photos":"",
				"Locales":"",
	      //name
				"DisplayName":"",
				"FamilyName":"",
				"GivenName":"",
				"DisplayNameLastFirst":"",
				//birthday
				"BirthdayDay":"",
				"BirthdayMonth":"",
				"BirthdayYear":"",
				"Email":"",
   
}


