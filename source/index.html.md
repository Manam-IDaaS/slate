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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email|mobile" -H "Accept-Language":"en-ca,en;q=0.8,en-us;" https://api.apieco.ir/manam/auth/register -d '{"confirm_url":"https://tenant.com/confirm","firstname": "myyfirstname","lastname":"mylastname","email": "myemail@gmail.com","password":"12345","confirm_password":"12345","national_code":"12907652",birthday:"1370-01-03"}'

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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email|mobile" https://api.apieco.ir/manam/auth/send_confirm_email -d {"email":"user@test.com","tenant_email":"info@tenant.com",confirm_url:"tenant.com/confirm"}
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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email|mobile" https://api.apieco.ir/manam/auth/login -d '{"email": "myemail@mail.com","password":"password"}'

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


## One Time Passwords (OTP) (Enable) [IDaaS]

One time passwords can be useful if users require a backup password in case they lose theirs, or they're logging in on an untrusted computer. This module allows users to add one time passwords, clear them, or log in with them.

### step1 :Login:
```shell
curl -X POST -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/otp/login -d '{"email":"test@test.com","password":"88e69f31-70da285e-ebc276ee-e0b0f929"}'
```

> The above return this output for Login: (use this cookie for the next step)

```shell
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/login HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Content-Type: application/json
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 63
> 
* upload completely sent off: 63 out of 63 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=nnDh5GdXsqe8WO/zzghf4/x8gpChDliLKaEBcXIE698=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0MzY2MHxEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18JzpeVTJkDDLhaFhd32c9JU2j3ZTRSV4sc8Byg954PVQ=; Path=/; Expires=Sun, 29 Sep 2019 19:54:20 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 07:54:20 GMT
< Content-Length: 344
< 
* Connection #0 to host localhost left intact
{"access_token":"","birthday":"","custome_fields":"\u003cinvalid Value\u003e","email":"test16@gmail.com","firstname":"ali","lastname":"lastname","location":"/","mobile":"\u003cinvalid Value\u003e","mobile_seed":"\u003cinvalid Value\u003e","national_code":"","role":"","status":"success","tenant_confirm_url":"","tenant_email":"","type":"email"}
```
### step2 :Display qr code 
```shell
http -p BHbh GET  localhost:3000/auth/otp/add  Cookie:"ab_blog=MTU3MTI4OTI4MXxEdi1CQkFFQ180SUFBUkFCRUFBQUx2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUV3QVJkR1Z6ZEc5MGNEVkFkR1Z6ZEM1amIyMD18aZXlqtfTBLoYX3jmZ1G1oAssiGOCUOtEoji8pcpda7k=" "apieco_key":"<apieco_key>"  "user_type":"email"
```

### step3 :send qr code 
```shell
curl -X POST -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/otp/add --cookie  "ab_blog=MTU3MTI4OTI4MXxEdi1CQkFFQ180SUFBUkFCRUFBQUx2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUV3QVJkR1Z6ZEc5MGNEVkFkR1Z6ZEM1amIyMD18aZXlqtfTBLoYX3jmZ1G1oAssiGOCUOtEoji8pcpda7k=" -d {"code":"953502"}
```
> The above return this output: (use this cookie for the next step)

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/otp/add HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU3MTI4OTI4MXxEdi1CQkFFQ180SUFBUkFCRUFBQUx2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUV3QVJkR1Z6ZEc5MGNEVkFkR1Z6ZEM1amIyMD18aZXlqtfTBLoYX3jmZ1G1oAssiGOCUOtEoji8pcpda7k=
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 13
> Content-Type: application/x-www-form-urlencoded
> 
* upload completely sent off: 13 out of 13 bytes
< HTTP/1.1 200 OK
< Content-Type: application/json
< Set-Cookie: csrf_token=abTY0+5pHK0o3i085bnWijoflsmD1bOFWOaspolvQ6c=; Max-Age=31536000
< Vary: Origin
< Vary: Cookie
< Date: Thu, 17 Oct 2019 05:16:31 GMT
< Content-Length: 444
< 
* Connection #0 to host localhost left intact
{"csrf_token":"hIE14Y7tEKJZiD3xRvj7/Xz0WkhiPsMWjEt5ZEaq4HDtNe0yYIQMD3FWEM2jQS13RuvMgeHrcJPUrdXCz8Wj1w==","current_user_name":"","flash_error":"","flash_success":"","loggedin":true,"modules":{"auth":true,"auth-custom":true,"confirm":true,"lock":true,"logout":true,"oauth2":true,"otp":true,"recover":true,"recover-custom":true,"register":true,"register-custom":true,"remember":true},"otp":"a8632d34-037bf456-6b8216b8-16fa0b96","status":"success"}

```

use otp param as password in login for this sample a8632d34-037bf456-6b8216b8-16fa0b96

## One Time Passwords (OTP) (Login) [IDaaS]
```shell
http -p BHbh POST  localhost:3000/auth/otp/login  email="testotp5@test.com" password="a8632d34-037bf456-6b8216b8-16fa0b96" "apieco_key":"<apieco_key>"  "user_type":"email"
```
> The above return this output
```shell
POST /auth/otp/login HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 81
Content-Type: application/json
Host: localhost:3000
User-Agent: HTTPie/0.9.8
X-Consumer-ID: <X-Consumer-ID>
user_type: email

{
    "email": "testotp5@test.com",
    "password": "a8632d34-037bf456-6b8216b8-16fa0b96"
}

HTTP/1.1 307 Temporary Redirect
Content-Length: 35
Content-Type: application/json
Date: Thu, 17 Oct 2019 05:37:41 GMT
Set-Cookie: csrf_token=wXxv3/JLBeADQanAi41lhBG9oBiI2QW+WAjBuUhTkaw=; Max-Age=31536000
Set-Cookie: ab_blog=MTU3MTI5MDY2MXxEdi1CQkFFQ180SUFBUkFCRUFBQUx2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUV3QVJkR1Z6ZEc5MGNEVkFkR1Z6ZEM1amIyMD189TdMJ4anx1kPWoKjyHbP74pVFCNxGRHIfERWzm4OVhY=; Path=/; Expires=Thu, 17 Oct 2019 17:37:41 GMT; Max-Age=43200
Vary: Origin
Vary: Cookie

{
    "location": "/",
    "status": "success"
}
```

## One Time Passwords (OTP) (Clear) [IDaaS]

Have to be login and use cookie

```shell
 http -p BHbh POST  localhost:3000/auth/otp/clear  email="testotp5@test.com" Cookie:"ab_blog=MTU3MTI4OTI4MXxEdi1CQkFFQ180SUFBUkFCRUFBQUx2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUV3QVJkR1Z6ZEc5MGNEVkFkR1Z6ZEM1amIyMD18aZXlqtfTBLoYX3jmZ1G1oAssiGOCUOtEoji8pcpda7k=" "apieco_key":"<apieco_key>"  "user_type":"email"
 ```
> The above return this output.

```shell
POST /auth/otp/clear HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 30
Content-Type: application/json
Cookie: ab_blog=MTU3MTI4OTI4MXxEdi1CQkFFQ180SUFBUkFCRUFBQUx2LUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUV3QVJkR1Z6ZEc5MGNEVkFkR1Z6ZEM1amIyMD18aZXlqtfTBLoYX3jmZ1G1oAssiGOCUOtEoji8pcpda7k=
Host: localhost:3000
User-Agent: HTTPie/0.9.8
X-Consumer-ID: <X-Consumer-ID>
user_type: email

{
    "email": "testotp5@test.com"
}

HTTP/1.1 200 OK
Content-Length: 416
Content-Type: application/json
Date: Thu, 17 Oct 2019 05:46:49 GMT
Set-Cookie: csrf_token=vqf+qB/xr4nMXC3iQUkkdJdnf69UTW8OeCtDtxBO05Y=; Max-Age=31536000
Vary: Origin
Vary: Cookie

{
    "csrf_token": "N93wFyUWLnjraXPY9TxmFDcaEy/3/sZzUdj3aAv6H6uJeg6/OueB8Sc1Xjq0dUJgoH1sgKOzqX0p87TfG7TMPQ==",
    "current_user_name": "",
    "flash_error": "",
    "flash_success": "",
    "loggedin": true,
    "modules": {
        "auth": true,
        "auth-custom": true,
        "confirm": true,
        "lock": true,
        "logout": true,
        "oauth2": true,
        "otp": true,
        "recover": true,
        "recover-custom": true,
        "register": true,
        "register-custom": true,
        "remember": true
    },
    "otp_count": "0",
    "status": "success"
}
 ```


## Register two factor authentication via Time-Based One Time Passwords(totp) (Enable) [IDaaS]

You should use two factor authentication in your application if you want additional security beyond that of just simple passwords. Each 2fa module supports a different mechanism for verifying a second factor of authentication from a user.

Tip:
* You have to be login to enable 2fa (two factor authentication)

### step1 :Login:
```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/login -d '{"email": "test16@gmail.com","password":"12345","type":"email"}'

```

> The above return this output for Login: (use this cookie for the next step)
```shell
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/login HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Content-Type: application/json
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 63
> 
* upload completely sent off: 63 out of 63 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=nnDh5GdXsqe8WO/zzghf4/x8gpChDliLKaEBcXIE698=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0MzY2MHxEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18JzpeVTJkDDLhaFhd32c9JU2j3ZTRSV4sc8Byg954PVQ=; Path=/; Expires=Sun, 29 Sep 2019 19:54:20 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 07:54:20 GMT
< Content-Length: 344
< 
* Connection #0 to host localhost left intact
{"access_token":"","birthday":"","custome_fields":"\u003cinvalid Value\u003e","email":"test16@gmail.com","firstname":"ali","lastname":"lastname","location":"/","mobile":"\u003cinvalid Value\u003e","mobile_seed":"\u003cinvalid Value\u003e","national_code":"","role":"","status":"success","tenant_confirm_url":"","tenant_email":"","type":"email"}
```

### step 2: Verify Email
This step use cookie from previous step and set code param with email.

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/email/verify -d {"code":"test16@gmail.com"} --cookie "ab_blog=MTU2OTc0MzY2MHxEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18JzpeVTJkDDLhaFhd32c9JU2j3ZTRSV4sc8Byg954PVQ="


```
> The above return this output and send verify link to email.

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/totp/email/verify HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0MzY2MHxEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18JzpeVTJkDDLhaFhd32c9JU2j3ZTRSV4sc8Byg954PVQ=
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 23
> 
* upload completely sent off: 23 out of 23 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=/e9voyv6i1J6GbxKtttIIwqnOpyV5tIHd4QPNfzCF8w=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0Mzc0MnxEdi1CQkFFQ180SUFBUkFCRUFBQWJfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUZnQVVkSGR2Wm1GamRHOXlYMkYxZEdoZmRHOXJaVzRHYzNSeWFXNW5EQm9BR0U1V1RVTllhbWRxVFdGMVdtUkJlalZuWkZGaVUxRTlQUT09fMxv1mxHUSDH6Yn83cD4RodGuaXOWYHbhP438UicbuKA; Path=/; Expires=Sun, 29 Sep 2019 19:55:42 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 07:55:42 GMT
< Content-Length: 98
< 
* Connection #0 to host localhost left intact
{"location":"/","message":"An e-mail has been sent to confirm 2FA activation.","status":"success"}

```

### step 3: Verify Email by Link

This step verfy link that be send to email. (use cookie from previous step )

```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/email/verify/end -d '{"token":"NVMCXjgjMauZdAz5gdQbSQ=="}'  --cookie "ab_blog=MTU2OTc0Mzc0MnxEdi1CQkFFQ180SUFBUkFCRUFBQWJfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUZnQVVkSGR2Wm1GamRHOXlYMkYxZEdoZmRHOXJaVzRHYzNSeWFXNW5EQm9BR0U1V1RVTllhbWRxVFdGMVdtUkJlalZuWkZGaVUxRTlQUT09fMxv1mxHUSDH6Yn83cD4RodGuaXOWYHbhP438UicbuKA;"

```

> The above return this output.

```shell
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> GET /auth/2fa/totp/email/verify/end HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0Mzc0MnxEdi1CQkFFQ180SUFBUkFCRUFBQWJfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUZnQVVkSGR2Wm1GamRHOXlYMkYxZEdoZmRHOXJaVzRHYzNSeWFXNW5EQm9BR0U1V1RVTllhbWRxVFdGMVdtUkJlalZuWkZGaVUxRTlQUT09fMxv1mxHUSDH6Yn83cD4RodGuaXOWYHbhP438UicbuKA;
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> Content-Length: 36
> 
* upload completely sent off: 36 out of 36 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=mWPcLe6P2qo0Pk2QHcNBoJJqBbiSK8goIQ7kVXJwvNw=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NDA3MXxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXxwyK9CAuxaZOhOe_dxxdhuwjxmHgdOrAMwsglg5g64-g==; Path=/; Expires=Sun, 29 Sep 2019 20:01:11 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:01:11 GMT
< Content-Length: 54
< 
* Connection #0 to host localhost left intact
{"location":"/auth/2fa/totp/setup","status":"success"}
```

### step 4: Set up with Get

This step and the next step are the background for preparation and display QR code. (use cookie from previous step )

```shell
curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/setup --cookie "ab_blog=MTU2OTc0NDA3MXxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXxwyK9CAuxaZOhOe_dxxdhuwjxmHgdOrAMwsglg5g64-g=="

```

> The above return this output.

```shell
Note: Unnecessary use of -X or --request, GET is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> GET /auth/2fa/totp/setup HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0NDA3MXxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXxwyK9CAuxaZOhOe_dxxdhuwjxmHgdOrAMwsglg5g64-g==
> Content-Type: application/json
> X-Consumer-ID:kiss_customer
> user_type:email
> 
< HTTP/1.1 200 OK
< Content-Type: application/json
< Set-Cookie: csrf_token=67pbX3sg+VRU93hw0vQTmmhGOFFUTjwr+pR6Myzn6fQ=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NDE4MHxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXzTigFKYnQo_iEVpF4n9OXJXJiV84Jx8sm9YWQNaOnqYw==; Path=/; Expires=Sun, 29 Sep 2019 20:03:00 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:03:00 GMT
< Content-Length: 389
< 
* Connection #0 to host localhost left intact
{"csrf_token":"W18D1fFt8KmHayO80yDUAi5zhnq/itsHJhswOoGgM9aw5ViKik0J/dOcW8wB1MeYRjW+K+vE5yzcj0oJrUfaIg==","current_user_name":"","flash_error":"","flash_success":"","loggedin":true,"modules":{"auth":true,"auth-custom":true,"confirm":true,"lock":true,"logout":true,"oauth2":true,"recover":true,"recover-custom":true,"register":true,"register-custom":true,"remember":true},"status":"success"}

```

### step 5: Set up with POST

This step and the previous step are the background for preparation and display QR code. (use cookie from previous step )

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/setup --cookie "ab_blog=MTU2OTc0NDE4MHxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXzTigFKYnQo_iEVpF4n9OXJXJiV84Jx8sm9YWQNaOnqYw==;"

```

> The above return this output.

```shell
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/totp/setup HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0NDE4MHxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXzTigFKYnQo_iEVpF4n9OXJXJiV84Jx8sm9YWQNaOnqYw==;
> Content-Type: application/json
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> 
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=P8KNpXyIeQi+jqn0a10jhOMpgCUVV43hqiq6wby1Bd0=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NDI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV81al9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVk5HVFZKQk4wbFNRbFpVV2xoV1JWZFROa2hGVVRSWlRGcE1ValpSUmxJR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01FZ0FRZEdWemRERTJRR2R0WVdsc0xtTnZiUVp6ZEhKcGJtY01FZ0FRZEhkdlptRmpkRzl5WDJGMWRHaGxaQVp6ZEhKcGJtY01CZ0FFZEhKMVpRPT18oYFsxLdUi7weJmG7F1I7dUkZtjdTNSbtHY8IJhObza4=; Path=/; Expires=Sun, 29 Sep 2019 20:04:26 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:04:26 GMT
< Content-Length: 56
< 
* Connection #0 to host localhost left intact
{"location":"/auth/2fa/totp/confirm","status":"success"}
```


### step 6: Display QR code

This step display QR code and user have to scan QR code and use code from that that change every minutues. (use cookie from previous step )

```shell
 curl -X GET -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/qr --cookie "ab_blog=MTU2OTc0NDI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV81al9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVk5HVFZKQk4wbFNRbFpVV2xoV1JWZFROa2hGVVRSWlRGcE1ValpSUmxJR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01FZ0FRZEdWemRERTJRR2R0WVdsc0xtTnZiUVp6ZEhKcGJtY01FZ0FRZEhkdlptRmpkRzl5WDJGMWRHaGxaQVp6ZEhKcGJtY01CZ0FFZEhKMVpRPT18oYFsxLdUi7weJmG7F1I7dUkZtjdTNSbtHY8IJhObza4=;"
```

> The above return this output.

```shell
Note: Unnecessary use of -X or --request, GET is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> GET /auth/2fa/totp/qr HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0NDI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV81al9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVk5HVFZKQk4wbFNRbFpVV2xoV1JWZFROa2hGVVRSWlRGcE1ValpSUmxJR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01FZ0FRZEdWemRERTJRR2R0WVdsc0xtTnZiUVp6ZEhKcGJtY01FZ0FRZEhkdlptRmpkRzl5WDJGMWRHaGxaQVp6ZEhKcGJtY01CZ0FFZEhKMVpRPT18oYFsxLdUi7weJmG7F1I7dUkZtjdTNSbtHY8IJhObza4=;
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> 
< HTTP/1.1 200 OK
< Content-Type: image/png
< Set-Cookie: csrf_token=A9Ibs6rcQJkJQ7auCxWxlDQZG6dsXH+wMA3QMplgVoQ=; Max-Age=31536000
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:07:35 GMT
< Content-Length: 1411
< 
Warning: Binary output can mess up your terminal. Use "--output -" to tell 
Warning: curl to output it to your terminal anyway, or consider "--output 
Warning: <FILE>" to save to a file.
* Failed writing body (0 != 1411)
* stopped the pause stream!
* Closing connection 0
```

Note : In shell can not show birnay data use browser or other tools like POSTMAN.


### step 8: Confirm and get recovery Code

This step use code from QR code that setup in mobile app or other ways from previous step and get recovery code. (use cookie from previous step )

```shell

curl -X POST -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/confirm  -d '{"code":"404870"}' --cookie "ab_blog=MTU2OTc0NDI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV81al9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVk5HVFZKQk4wbFNRbFpVV2xoV1JWZFROa2hGVVRSWlRGcE1ValpSUmxJR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01FZ0FRZEdWemRERTJRR2R0WVdsc0xtTnZiUVp6ZEhKcGJtY01FZ0FRZEhkdlptRmpkRzl5WDJGMWRHaGxaQVp6ZEhKcGJtY01CZ0FFZEhKMVpRPT18oYFsxLdUi7weJmG7F1I7dUkZtjdTNSbtHY8IJhObza4=;"


```

> The above return this output.

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/totp/confirm HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0NDI2NnxEdi1CQkFFQ180SUFBUkFCRUFBQV81al9nZ0FEQm5OMGNtbHVad3dOQUF0MGIzUndYM05sWTNKbGRBWnpkSEpwYm1jTUlnQWdVVk5HVFZKQk4wbFNRbFpVV2xoV1JWZFROa2hGVVRSWlRGcE1ValpSUmxJR2MzUnlhVzVuREFVQUEzVnBaQVp6ZEhKcGJtY01FZ0FRZEdWemRERTJRR2R0WVdsc0xtTnZiUVp6ZEhKcGJtY01FZ0FRZEhkdlptRmpkRzl5WDJGMWRHaGxaQVp6ZEhKcGJtY01CZ0FFZEhKMVpRPT18oYFsxLdUi7weJmG7F1I7dUkZtjdTNSbtHY8IJhObza4=;
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 17
> Content-Type: application/x-www-form-urlencoded
> 
* upload completely sent off: 17 out of 17 bytes
< HTTP/1.1 200 OK
< Content-Type: application/json
< Set-Cookie: csrf_token=hX0/dMNBh25+TgZZLabjO0xsFKfl7tTg9Xr8C10wAz0=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NDY3MHxEdi1CQkFFQ180SUFBUkFCRUFBQVZfLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUVnQVFkSGR2Wm1GamRHOXlYMkYxZEdobFpBWnpkSEpwYm1jTUJnQUVkSEoxWlE9PXzyx9MERC3HTgSedqPlmfRCDI3RyHgAgtPb8XMNJwwnvA==; Path=/; Expires=Sun, 29 Sep 2019 20:11:10 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:11:10 GMT
< Content-Length: 548
< 
* Connection #0 to host localhost left intact
{"csrf_token":"OICZ97by/Z84KRXjG2MZRUJRJIRYpAxnQa006r98hQa9/aaDdbN68UZnE7o2xfp+Dj0wI71K2Ie018jh4kyGOw==","current_user_name":"","flash_error":"","flash_success":"","loggedin":true,"modules":{"auth":true,"auth-custom":true,"confirm":true,"lock":true,"logout":true,"oauth2":true,"recover":true,"recover-custom":true,"register":true,"register-custom":true,"remember":true},"recovery_codes":["ee1zb-91jy1","qfc7q-ukd1d","hhdcj-q99w1","he8dg-jn9vf","86nqh-00ru6","egir1-u4cut","i1228-gntn5","xe4vz-af6i6","qzdcr-2756b","k1ujj-v5mty"],"status":"success"}

```

## Login two factor authentication via Time-Based One Time Passwords (totp) [IDaaS]

You should use two factor authentication in your application if you want additional security beyond that of just simple passwords. Each 2fa module supports a different mechanism for verifying a second factor of authentication from a user.

### step1 : Login via password
```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/login -d '{"email": "test16@gmail.com","password":"12345","type":"email"}'

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
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 63
> 
* upload completely sent off: 63 out of 63 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=28bMalNpc8GkE15ROqCiIcqYMD7Zp5Qe2OHpLMkvUng=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NTQ5NnxEdi1CQkFFQ180SUFBUkFCRUFBQU52LUNBQUVHYzNSeWFXNW5EQTRBREhSdmRIQmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18-RcNmidjCGEPnSWLXxHg4n6TdTpa8gCLQU47-K3UxAA=; Path=/; Expires=Sun, 29 Sep 2019 20:24:56 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:24:56 GMT
< Content-Length: 366
< 
* Connection #0 to host localhost left intact
{"access_token":"","birthday":"","custome_fields":"\u003cinvalid Value\u003e","email":"test16@gmail.com","firstname":"ali","lastname":"lastname","location":"/auth/2fa/totp/validate","mobile":"\u003cinvalid Value\u003e","mobile_seed":"\u003cinvalid Value\u003e","national_code":"","role":"","status":"success","tenant_confirm_url":"","tenant_email":"","type":"email"}

```

### step2: validate with code and verify code
This command use to authenticate in 2fa visa toyp. (set cookie from previouse step)
code and recovery_code params are described in previous part (code comes from sms and recovery_code comes from confirm step).

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/validate -d '{"code": "326019","recovery_code":"hhdcj-q99w1"}' --cookie "ab_blog=MTU2OTc0NTQ5NnxEdi1CQkFFQ180SUFBUkFCRUFBQU52LUNBQUVHYzNSeWFXNW5EQTRBREhSdmRIQmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18-RcNmidjCGEPnSWLXxHg4n6TdTpa8gCLQU47-K3UxAA="

```

> The above return this output.

```shell

Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/totp/validate HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0NTQ5NnxEdi1CQkFFQ180SUFBUkFCRUFBQU52LUNBQUVHYzNSeWFXNW5EQTRBREhSdmRIQmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18-RcNmidjCGEPnSWLXxHg4n6TdTpa8gCLQU47-K3UxAA=
> Content-Type: application/json
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 48
> 
* upload completely sent off: 48 out of 48 bytes
< HTTP/1.1 307 Temporary Redirect
< Content-Type: application/json
< Set-Cookie: csrf_token=RSg9qBoFlUvlH5UlJY8FMsj9VIWlXXHOPVcQPDnCMEU=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NTYwMnxEdi1CQkFFQ180SUFBUkFCRUFBQVVQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUN3QUpkSGR2Wm1GamRHOXlCbk4wY21sdVp3d0dBQVIwYjNSd3yRxbe0gnzqbmD2pbgqx8KkviJxktBCpWQ1otm2rccKxw==; Path=/; Expires=Sun, 29 Sep 2019 20:26:42 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:26:42 GMT
< Content-Length: 74
< 
* Connection #0 to host localhost left intact
{"location":"/","message":"Successfully Authenticated","status":"success"}

```


## Remove two factor authentication via totp (Disable) [IDaaS]

User can remove 2fa.
Tips:
1. set cookie from Login step
2.code and recovery_code params are described in previous part (code comes from QR code scanner that change every minutes and recovery_code comes from confirm step).


```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/auth/2fa/totp/remove -d '{"code": "302922","recovery_code":"egir1-u4cut"}' --cookie "ab_blog=MTU2OTc0NTYwMnxEdi1CQkFFQ180SUFBUkFCRUFBQVVQLUNBQUlHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUN3QUpkSGR2Wm1GamRHOXlCbk4wY21sdVp3d0dBQVIwYjNSd3yRxbe0gnzqbmD2pbgqx8KkviJxktBCpWQ1otm2rccKxw==; "


```

> The above return this output.

```shell
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
> POST /auth/2fa/totp/remove HTTP/1.1
> Host: localhost:3000
> User-Agent: curl/7.58.0
> Accept: */*
> Cookie: ab_blog=MTU2OTc0NjAwM3xEdi1CQkFFQ180SUFBUkFCRUFBQVVQLUNBQUlHYzNSeWFXNW5EQXNBQ1hSM2IyWmhZM1J2Y2daemRISnBibWNNQmdBRWRHOTBjQVp6ZEhKcGJtY01CUUFEZFdsa0JuTjBjbWx1Wnd3U0FCQjBaWE4wTVRaQVoyMWhhV3d1WTI5dHzlVBe7ocaPKr5q65XrOGra3K8nO92zliUulloeLx-bfw==
> Content-Type: application/json
> X-Consumer-ID:<X-Consumer-ID>
> user_type:email
> Content-Length: 48
> 
* upload completely sent off: 48 out of 48 bytes
< HTTP/1.1 200 OK
< Content-Type: application/json
< Set-Cookie: csrf_token=VzJ9Qui3oWfwGI7CPJV5yXB4rH5Ei/UKK640zZpnrJY=; Max-Age=31536000
< Set-Cookie: ab_blog=MTU2OTc0NjA3OXxEdi1CQkFFQ180SUFBUkFCRUFBQUxmLUNBQUVHYzNSeWFXNW5EQVVBQTNWcFpBWnpkSEpwYm1jTUVnQVFkR1Z6ZERFMlFHZHRZV2xzTG1OdmJRPT18MtycnV81wGKxoMhh576pKnaWamRpk-4WfkCPgwuZ020=; Path=/; Expires=Sun, 29 Sep 2019 20:34:39 GMT; Max-Age=43200
< Vary: Origin
< Vary: Cookie
< Date: Sun, 29 Sep 2019 08:34:39 GMT
< Content-Length: 389
< 
* Connection #0 to host localhost left intact
{"csrf_token":"cuaFkoXH2IyDsF5Jps5ZAkCSkhWsRqgOx4nMp0tgST0l1PjQbXB563Oo0IuaWyDLMOo+a+jNXQTsJ/hq0Qflqw==","current_user_name":"","flash_error":"","flash_success":"","loggedin":true,"modules":{"auth":true,"auth-custom":true,"confirm":true,"lock":true,"logout":true,"oauth2":true,"recover":true,"recover-custom":true,"register":true,"register-custom":true,"remember":true},"status":"success"}

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
> X-Consumer-ID:<X-Consumer-ID>
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
> X-Consumer-ID:<X-Consumer-ID>
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
> X-Consumer-ID:<X-Consumer-ID>
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
> X-Consumer-ID:<X-Consumer-ID>
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
> X-Consumer-ID:<X-Consumer-ID>
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
> X-Consumer-ID:<X-Consumer-ID>
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
> X-Consumer-ID:<X-Consumer-ID>
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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v --cookie ""ab_blog=MTU2OTcwMzcxNXxEdi1CQkFFQ180SUFBUkFCRUFBQV80UF9nZ0FEQm5OMGNtbHVad3dOQUF0emJYTmZjR1Z1WkdsdVp3WnpkSEpwYm1jTUVnQVFkR1Z6ZERFMVFHZHRZV2xzTG1OdmJRWnpkSEpwYm1jTUNnQUljMjF6WDJ4aGMzUUdjM1J5YVc1bkRBd0FDakUxTmprM01ETTNNVFVHYzNSeWFXNW5EQXdBQ25OdGMxOXpaV055WlhRR2MzUnlhVzVuREFnQUJqUTJORFkxTlE9PXxkXEBe1CwJ62xrTiTmvWGNQKB4Irbc8nV7Nx9ZIepWBA==;" localhost:3000/auth/2fa/sms/remove -d '{"code":"224380","recovery_code":"h41cv-xp4ca"}'

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
> X-Consumer-ID:<X-Consumer-ID>
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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/view_user -d {"email":"<email>","type":"email"}


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/view_user",
    headers: {
                "apieco_key":"<apieco_key>"
                
            },
    dataType: "json",
    type : "POST",
    success : function(r) {
      console.log(r);
    }
  });
  ```

> The above command returns JSON structured like this:

```json

{"access_token":"...",
 "birthday":"",
 "custome_fields":"",
 "email":"test15@gmail.com",
 "firstname":"ali",
 "lastname":"lastname",
 "location":"/",
 "mobile":"",
 "mobile_seed":"" ,
 "national_code":"",
 "role":"",
 "status":"success",
 "tenant_confirm_url":"",
 "tenant_email":"",
 "type":"email"}
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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/edit_user -d '{"type":"[email|mobile]","email":"mytest@gmail.com","national_code":"12344","birthday":"1990-02-01","mobile":"091223423","custom_field":"{"address":"..","postal_code":"..."}"}'


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
            "type":"[email|mobile]",
            "email":"mytest@gmail.com",
           "national_code":"12344",
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

curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>"  https://api.apieco.ir/manam/get_manam_user_info -d '{"email": "test@test.com","type":"email"}'

```

> The above command returns JSON structured like this:

```json

{"NationalCode":"66666",
"Birthday":"1930-03-01",
"Mobile":"9356315367",
"Firstname":"...",
"Lastname":"...",
"Role":"...",
"TenantEmail":"info@tenant.com",
"TenantConfirmURL":"tenant.com/confirm",
"CustomFields":"{\"name\": \"name\", \"address\": \"address\"}",
"Type":"email"}

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
```

## Google Login with Manam [Manam]
Consumer has a link in site to login user with manam and user want to login in manam with google ouath.
This proscess has two step first step to authorization from google and the second step to get user information.

### step 1: Authenticate user in google
when user click on a link in site and want login with google login go to this page to enter email and password.
for this step use this api.

Tip:
tenant_callback_url :  tenant define callback url.


```python

url = 'https://https://api.apieco.ir/oauth_google'
headers = {'apieco_key': '<apieco_key>',               
               'tenant_callback_url':'http://tenant.com/<tenant_google_callback>' # tenant confirm url
               }
r = requests.get(url, headers=headers).content


```
> The above command display google ouath for login user:



After login go to tenant url with to parameters code and state this parameter used for the next state.

### step 2: Display user information

```shell
curl -X POST -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" -H "user_type:email" -v  localhost:3000/user_google_info -d '{"code": "<code>","state":"pseudo-random"}'
```


