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
Date: Sun, 22 Sep 2019 18:31:12 GMT
Set-Cookie: csrf_token=eQ0is6UU4EfPrbz0fw+dJMbjVDzGTbrcJYje+in9Ris=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3NzA3MnxEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXylqzElrdJiQoa9pZTPKBbOSEfUklZPvAtvFPiv9s73Lg==; Path=/; Expires=Mon, 23 Sep 2019 06:31:12 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/",
    "status": "success"
}
```

### step2: verify code by email
This command send and email to verify email.

```shell
http -p BHbh POST localhost:3000/auth/2fa/sms/email/verify Code="test@test.com" Cookie:"ab_blog=MTU2OTE3NzA3MnxEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXylqzElrdJiQoa9pZTPKBbOSEfUklZPvAtvFPiv9s73Lg=="

```

> The above return this output and send email to verify.

```shell
POST /auth/2fa/sms/email/verify HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 25
Content-Type: application/json
Cookie: ab_blog=MTU2OTE3NzA3MnxEdi1CQkFFQ180SUFBUkFCRUFBQUt2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlE9PXylqzElrdJiQoa9pZTPKBbOSEfUklZPvAtvFPiv9s73Lg==
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "Code": "test@test.com"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 98
Content-Type: application/json
Date: Sun, 22 Sep 2019 18:31:57 GMT
Set-Cookie: csrf_token=NZCRMSrTv3i7n0gWjccCDfGzl3XQb1CnmXWxgsKqHcU=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3NzExN3xEdi1CQkFFQ180SUFBUkFCRUFBQWJQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRmdBVWRIZHZabUZqZEc5eVgyRjFkR2hmZEc5clpXNEdjM1J5YVc1bkRCb0FHR0pSVFRZMk1qUkJURFp3YVcwNGNXbG1XSGhXVFdjOVBRPT18lGYXCegj1Bh3eCL6bIFoKkNYV-OVTpckS0WBzBrk-Ms=; Path=/; Expires=Mon, 23 Sep 2019 06:31:57 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/",
    "message": "An e-mail has been sent to confirm 2FA activation.",
    "status": "success"
}
```


### step3: verify email by token

This command check token to verify email. (set cookie from previouse step)

```shell
http -p BHbh GET localhost:3000/auth/2fa/sms/email/verify/end token="bQM6624AL6pim8qifXxVMg==" Cookie:"ab_blog=MTU2OTE3NzExN3xEdi1CQkFFQ180SUFBUkFCRUFBQWJQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRmdBVWRIZHZabUZqZEc5eVgyRjFkR2hmZEc5clpXNEdjM1J5YVc1bkRCb0FHR0pSVFRZMk1qUkJURFp3YVcwNGNXbG1XSGhXVFdjOVBRPT18lGYXCegj1Bh3eCL6bIFoKkNYV-OVTpckS0WBzBrk-Ms=;"

```

> The above return this output.

```shell
GET /auth/2fa/sms/email/verify/end HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 37
Content-Type: application/json
Cookie: ab_blog=MTU2OTE3NzExN3xEdi1CQkFFQ180SUFBUkFCRUFBQWJQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNRmdBVWRIZHZabUZqZEc5eVgyRjFkR2hmZEc5clpXNEdjM1J5YVc1bkRCb0FHR0pSVFRZMk1qUkJURFp3YVcwNGNXbG1XSGhXVFdjOVBRPT18lGYXCegj1Bh3eCL6bIFoKkNYV-OVTpckS0WBzBrk-Ms=;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "token": "bQM6624AL6pim8qifXxVMg=="
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 53
Content-Type: application/json
Date: Sun, 22 Sep 2019 18:34:28 GMT
Set-Cookie: csrf_token=RzcsypX+RdWZugosWmeubsF6EKsDOltxf3/7IZdp85E=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3NzI2OHxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQklBRUhSM2IyWmhZM1J2Y2w5aGRYUm9aV1FHYzNSeWFXNW5EQVlBQkhSeWRXVUdjM1J5YVc1bkRBVUFBM1ZwWkFaemRISnBibWNNRHdBTmRHVnpkRUIwWlhOMExtTnZiUT09fPGM70_UMvWNhAm0ZKRMi9JrYO_eVOKDma0QGPkOciTY; Path=/; Expires=Mon, 23 Sep 2019 06:34:28 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/auth/2fa/sms/setup",
    "status": "success"
}

```

### Step 4 : Set up Phone number to get Code
This command send a code to phone number this code is one of the factors in 2fa to login. (set cookie from previouse step)

```shell
http -p BHbh POST localhost:3000/auth/2fa/sms/setup phone_number="935631589" Cookie:"ab_blog=MTU2OTE3NzI2OHxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQklBRUhSM2IyWmhZM1J2Y2w5aGRYUm9aV1FHYzNSeWFXNW5EQVlBQkhSeWRXVUdjM1J5YVc1bkRBVUFBM1ZwWkFaemRISnBibWNNRHdBTmRHVnpkRUIwWlhOMExtTnZiUT09fPGM70_UMvWNhAm0ZKRMi9JrYO_eVOKDma0QGPkOciTY"
```

> The above return this output.

```shell
POST /auth/2fa/sms/setup HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 29
Content-Type: application/json
Cookie: ab_blog=MTU2OTE3NzI2OHxEdi1CQkFFQ180SUFBUkFCRUFBQVZQLUNBQUlHYzNSeWFXNW5EQklBRUhSM2IyWmhZM1J2Y2w5aGRYUm9aV1FHYzNSeWFXNW5EQVlBQkhSeWRXVUdjM1J5YVc1bkRBVUFBM1ZwWkFaemRISnBibWNNRHdBTmRHVnpkRUIwWlhOMExtTnZiUT09fPGM70_UMvWNhAm0ZKRMi9JrYO_eVOKDma0QGPkOciTY
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "phone_number": "935631589"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 55
Content-Type: application/json
Date: Sun, 22 Sep 2019 18:36:37 GMT
Set-Cookie: csrf_token=Tt3kZR6dukMj7sgjtLIPg4RZg15sR97fNNTP1o0pkcU=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3NzM5N3xEdi1CQkFFQ180SUFBUkFCRUFBQV84dl9nZ0FGQm5OMGNtbHVad3dNQUFwemJYTmZjMlZqY21WMEJuTjBjbWx1Wnd3SUFBWTROREV4TlRjR2MzUnlhVzVuREJJQUVIUjNiMlpoWTNSdmNsOWhkWFJvWldRR2MzUnlhVzVuREFZQUJIUnlkV1VHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNREFBS2MyMXpYMjUxYldKbGNnWnpkSEpwYm1jTUN3QUpPVE0xTmpNeE5UZzVCbk4wY21sdVp3d0tBQWh6YlhOZmJHRnpkQVp6ZEhKcGJtY01EQUFLTVRVMk9URTNOek01Tnc9PXyK6GBrkST81vsvmX2mf-wqDspeZUCFnsbtmvbyBwi80A==; Path=/; Expires=Mon, 23 Sep 2019 06:36:37 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/auth/2fa/sms/confirm",
    "status": "success"
}

```

### Step5: Confirm Code and get recovery code 

This command get recovery code. This is another factors in 2fa to login. (set cookie from previouse step)
Param code send in phone number.

```shell
http -p BHbh POST localhost:3000/auth/2fa/sms/confirm  code="841157" Cookie:"ab_blog=MTU2OTE3NzM5N3xEdi1CQkFFQ180SUFBUkFCRUFBQV84dl9nZ0FGQm5OMGNtbHVad3dNQUFwemJYTmZjMlZqY21WMEJuTjBjbWx1Wnd3SUFBWTROREV4TlRjR2MzUnlhVzVuREJJQUVIUjNiMlpoWTNSdmNsOWhkWFJvWldRR2MzUnlhVzVuREFZQUJIUnlkV1VHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNREFBS2MyMXpYMjUxYldKbGNnWnpkSEpwYm1jTUN3QUpPVE0xTmpNeE5UZzVCbk4wY21sdVp3d0tBQWh6YlhOZmJHRnpkQVp6ZEhKcGJtY01EQUFLTVRVMk9URTNOek01Tnc9PXyK6GBrkST81vsvmX2mf-wqDspeZUCFnsbtmvbyBwi80A==;"
```

> The above return this output.

```shell
POST /auth/2fa/sms/confirm HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 18
Content-Type: application/json
Cookie: ab_blog=MTU2OTE3NzM5N3xEdi1CQkFFQ180SUFBUkFCRUFBQV84dl9nZ0FGQm5OMGNtbHVad3dNQUFwemJYTmZjMlZqY21WMEJuTjBjbWx1Wnd3SUFBWTROREV4TlRjR2MzUnlhVzVuREJJQUVIUjNiMlpoWTNSdmNsOWhkWFJvWldRR2MzUnlhVzVuREFZQUJIUnlkV1VHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNREFBS2MyMXpYMjUxYldKbGNnWnpkSEpwYm1jTUN3QUpPVE0xTmpNeE5UZzVCbk4wY21sdVp3d0tBQWh6YlhOZmJHRnpkQVp6ZEhKcGJtY01EQUFLTVRVMk9URTNOek01Tnc9PXyK6GBrkST81vsvmX2mf-wqDspeZUCFnsbtmvbyBwi80A==;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "841157"
}

HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
Date: Sun, 22 Sep 2019 18:38:33 GMT
Set-Cookie: csrf_token=BNkGKqOTe1UAsTSd4bYPgBi9T120xsv6LvLDO21cDQE=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3NzUxM3xEdi1CQkFFQ180SUFBUkFCRUFBQWZQLUNBQU1HYzNSeWFXNW5EQklBRUhSM2IyWmhZM1J2Y2w5aGRYUm9aV1FHYzNSeWFXNW5EQVlBQkhSeWRXVUdjM1J5YVc1bkRBVUFBM1ZwWkFaemRISnBibWNNRHdBTmRHVnpkRUIwWlhOMExtTnZiUVp6ZEhKcGJtY01DZ0FJYzIxelgyeGhjM1FHYzNSeWFXNW5EQXdBQ2pFMU5qa3hOemN6T1RjPXzL6AqZWnuZrPlKIaxxDpccQegrKS9lDzN-A-4_KcfGeQ==; Path=/; Expires=Mon, 23 Sep 2019 06:38:33 GMT; Max-Age=43200
Vary: Cookie

{
    "csrf_token": "NSEXBNn+56N9SThaLZbGpOaRmr+eoEmY4CXjeEvI1box+BEuem2c9n34DMfMIMkk/izV4ipmgmLO1yBDJpTYuw==",
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
        "3ts27-y1mpd",
        "egmiy-y61ta",
        "596md-64s5z",
        "rmyg2-ghkqg",
        "kwgc8-qjafz",
        "gfr4m-dtybg",
        "digih-7473p",
        "phyn6-q3bub",
        "bzd98-7j1mg",
        "tw8zd-toxef"
    ],
    "status": "success"
}

```


## Login two factor authentication via SMS [IDaaS]

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
Content-Length: 56
Content-Type: application/json
Date: Sun, 22 Sep 2019 16:54:26 GMT
Set-Cookie: csrf_token=6LbxhECYsWf/FjlhqwoWs+9zReKOxWYufQ2ZEIUwL50=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3MTI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV80RF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNQ2dBSWMyMXpYMnhoYzNRR2MzUnlhVzVuREF3QUNqRTFOamt4TnpFeU5qWUdjM1J5YVc1bkRBd0FDbk50YzE5elpXTnlaWFFHYzNSeWFXNW5EQWdBQmpZNE16SXhNdz09fAx01VIvXP9AijVXuGSJbZr62cqy_pKlj_2RvxACOW_1; Path=/; Expires=Mon, 23 Sep 2019 04:54:26 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/auth/2fa/sms/validate",
    "status": "success"
}
```

### step2: validate with code and verify code
This command use to authenticate in 2fa visa SMS. (set cookie from previouse step)
code and recovery_code params are described in previous part (code comes from sms and recovery_code comes from confirm step).

```shell
http -p BHbh POST localhost:3000/auth/2fa/sms/validate  code="155638" recovery_code="jutyg-iyjm0" Cookie:"ab_blog=MTU2OTE3MTI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV80RF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNQ2dBSWMyMXpYMnhoYzNRR2MzUnlhVzVuREF3QUNqRTFOamt4TnpFeU5qWUdjM1J5YVc1bkRBd0FDbk50YzE5elpXTnlaWFFHYzNSeWFXNW5EQWdBQmpZNE16SXhNdz09fAx01VIvXP9AijVXuGSJbZr62cqy_pKlj_2RvxACOW_1;"

```

> The above return this output.

```shell
POST /auth/2fa/sms/validate HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 50
Content-Type: application/json
Cookie: ab_blog=MTU2OTE3MTI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV80RF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUR3QU5kR1Z6ZEVCMFpYTjBMbU52YlFaemRISnBibWNNQ2dBSWMyMXpYMnhoYzNRR2MzUnlhVzVuREF3QUNqRTFOamt4TnpFeU5qWUdjM1J5YVc1bkRBd0FDbk50YzE5elpXTnlaWFFHYzNSeWFXNW5EQWdBQmpZNE16SXhNdz09fAx01VIvXP9AijVXuGSJbZr62cqy_pKlj_2RvxACOW_1;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "155638",
    "recovery_code": "jutyg-iyjm0"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 74
Content-Type: application/json
Date: Sun, 22 Sep 2019 16:56:26 GMT
Set-Cookie: csrf_token=Xntl9G1O59aOKws9l8x1gHyI/pNbF2cN0l5Ygu5JJOQ=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3MTM4NnxEdi1CQkFFQ180SUFBUkFCRUFBQWRQLUNBQU1HYzNSeWFXNW5EQW9BQ0hOdGMxOXNZWE4wQm5OMGNtbHVad3dNQUFveE5UWTVNVGN4TWpZMkJuTjBjbWx1Wnd3RkFBTjFhV1FHYzNSeWFXNW5EQThBRFhSbGMzUkFkR1Z6ZEM1amIyMEdjM1J5YVc1bkRBc0FDWFIzYjJaaFkzUnZjZ1p6ZEhKcGJtY01CUUFEYzIxenykX1pbSrFB-Mt1uBJEWMaipMg5tzTMn81XJBuqS23CkQ==; Path=/; Expires=Mon, 23 Sep 2019 04:56:26 GMT; Max-Age=43200
Vary: Cookie

{
    "location": "/",
    "message": "Successfully Authenticated",
    "status": "success"
}
```

## Remove two factor authentication via SMS (Disable) [IDaaS]

User can remove 2fa.
Tips:
1. set cookie from Login step
2.code and recovery_code params are described in previous part (code comes from sms and recovery_code comes from confirm step).


```shell

http -p BHbh POST localhost:3000/auth/2fa/sms/remove  code="155638" recovery_code="nn4u9-gqs87" Cookie:"ab_blog=MTU2OTE3MTM4NnxEdi1CQkFFQ180SUFBUkFCRUFBQWRQLUNBQU1HYzNSeWFXNW5EQW9BQ0hOdGMxOXNZWE4wQm5OMGNtbHVad3dNQUFveE5UWTVNVGN4TWpZMkJuTjBjbWx1Wnd3RkFBTjFhV1FHYzNSeWFXNW5EQThBRFhSbGMzUkFkR1Z6ZEM1amIyMEdjM1J5YVc1bkRBc0FDWFIzYjJaaFkzUnZjZ1p6ZEhKcGJtY01CUUFEYzIxenykX1pbSrFB-Mt1uBJEWMaipMg5tzTMn81XJBuqS23CkQ==;"

```

> The above return this output.

```shell
POST /auth/2fa/sms/remove HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 50
Content-Type: application/json
Cookie: ab_blog=MTU2OTE3MTM4NnxEdi1CQkFFQ180SUFBUkFCRUFBQWRQLUNBQU1HYzNSeWFXNW5EQW9BQ0hOdGMxOXNZWE4wQm5OMGNtbHVad3dNQUFveE5UWTVNVGN4TWpZMkJuTjBjbWx1Wnd3RkFBTjFhV1FHYzNSeWFXNW5EQThBRFhSbGMzUkFkR1Z6ZEM1amIyMEdjM1J5YVc1bkRBc0FDWFIzYjJaaFkzUnZjZ1p6ZEhKcGJtY01CUUFEYzIxenykX1pbSrFB-Mt1uBJEWMaipMg5tzTMn81XJBuqS23CkQ==;
Host: localhost:3000
User-Agent: HTTPie/0.9.8

{
    "code": "155638",
    "recovery_code": "nn4u9-gqs87"
}

HTTP/1.1 200 OK
Content-Length: 343
Content-Type: application/json
Date: Sun, 22 Sep 2019 16:57:54 GMT
Set-Cookie: csrf_token=hXnVusD365PV01U3ZAeQa5FpmSVIfyYCjDIP7cvhpkA=; Max-Age=31536000
Set-Cookie: ab_blog=MTU2OTE3MTQ3NHxEdi1CQkFFQ180SUFBUkFCRUFBQVV2LUNBQUlHYzNSeWFXNW5EQW9BQ0hOdGMxOXNZWE4wQm5OMGNtbHVad3dNQUFveE5UWTVNVGN4TWpZMkJuTjBjbWx1Wnd3RkFBTjFhV1FHYzNSeWFXNW5EQThBRFhSbGMzUkFkR1Z6ZEM1amIyMD18XpHmS7hzPtGc94Gtiq6FED04wBPkexOM2M311D7igAY=; Path=/; Expires=Mon, 23 Sep 2019 04:57:54 GMT; Max-Age=43200
Vary: Cookie

{
    "csrf_token": "zvt64O5CSBaNJkziCVDwDiUeuplfqKFqZ2edxJg0r4BLgq9aLrWjhVj1GdVtV2BltHcjvBfXh2jrVZIpU9UJwA==",
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


