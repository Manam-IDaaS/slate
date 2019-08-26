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
{
"location": "/",
"message": "An email has been sent to you with further instructions on how to reset your password.",
"status": "success"
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

curl -X GET -H "Content-Type: application/json" -H "apieco_key:<apieco_key>" https://api.apieco.ir/manam/auth/changepassword -d '{"cnf":"....","new_password": "...","re_new_password":"..."}'


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/auth/changepassword",
    headers: {
                "apieco_key":"<apieco_key>",
                
            
              
            },
    dataType: "json",
    type : "GET",
    data: { "cnf":"...","new_password":"...","re_new_password":""}
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
{
"location": "/",
"message": "There is an error here to change password.",
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


