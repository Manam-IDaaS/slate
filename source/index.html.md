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

## Register


```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:1234" https://api.apieco.ir/manam/auth/register -d '{"name": "myyname","email": "jik.jeek2018@gmail.com","password":"12345","confirm_password":"12345","meli_code":"12907652", "picture":"butypic","address":"Tehran, saadat Abad", "postal_code":"postal_code","birthday":"1990-02-01","marital_status":"single","facebook_id":"facebook_id","instagram_id":"instagram_id","twitter_id":"twitter_id","linkedIn_id":"linkedIn_id","document":"document","mobile":"09111087815","telephone":"88828919"}'

```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/auth/register",
    headers: {
                'apieco_key': '1234',
         
            },
    dataType: "json",
    type : "POST",
    data: {name:"myname",
    email:"myemail@mail.com",
    password:"password",
    confirm_password:"password", 
    "meli_code":"12907652", 
    "picture":"butypic",
    "address":"Tehran, saadat Abad",
    "postal_code":"postal_code",
    "birthday":"1990-02-1",
    "marital_status":"single",
    "facebook_id":"facebook_id"
    "instagram_id":"instagram_id",
    "twitter_id":"twitter_id",
    "linkedIn_id":"linkedIn_id",
    "document":"document",
    "mobile":"09111087815",
    "telephone":"88828919"
     }
    success : function(r) {
      console.log(r);
    }
  });
```

> The above command returns JSON structured like this:

```json

{
    "auth_token": "...",
    "refresh_token": "...",
    "username": "",
    "fullname": "",
    "email": "",
    "roles": [],
    "permissions": []
}

```

This endpoint register user in Manam.

### HTTP Request

`POST https://api.apieco.ir/manam/auth/register`

### Query Parameters
None.


### Data Params

Parameter | Type 
--------- | ------- 
name | string
email | [string] *
password | [string]*
confirm_password | string*
meli_code | string
picture | string
address | string
birthday | date
marital_status | string
facebook_id | string
instagram_id | string
twitter_id | string
linkedIn_id | string
document | string
mobile | string
telephone | string


## Confirm  

```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:1234" https://api.apieco.ir/manam/auth/confirm -d {cnf:h-A1iPysWfQ9Mj5EYuCKZo9KJ5UccHTjqABqfL-8bw48fkUQAOhBB-Bbwo2V7AE5TKYYYE9QXpDLrCvImQ57Tw==}
```

```javascript
$.ajax({
    url: "  https://api.apieco.ir/manam/auth/confirm?cnf=FFL5QDOYTXJZcO3SdcDgd8Kv-_euyLqVwm-eFagHZG_KCBLgtyhUkjFAeeDXvMFVVame3vXKyiWbnpNAVxQI8A==,
    headers: {
                "apieco_key":"1234"
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
"location": "/",
"message": "You have successfully confirmed your account.",
"status": "success"
}
```

This endpoint confirm users on Manam.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.apieco.ir/manam/auth/confirm/<cnf>`

### URL Parameters

Parameter | Description
--------- | -----------
cnf | The string that confirm registartion

## Login



```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:1234" https://api.apieco.ir/manam/auth/login -d '{"email": "myemail@mail.com","password":"password"}'

```

```javascript
 $.ajax({
    url: "https://api.apieco.ir/manam/auth/login",
    headers: {                
                "apieco_key":"1234"
            },
    dataType: "json",
    type : "POST",
    data: { email:"myemail@mail.com", password:"password"}
    success : function(r) {
      console.log(r);
    }
  });
```

> The above command returns JSON structured like this:

```json
{
    "auth_token": "...",
    "refresh_token": "...",
    "username": "",
    "fullname": "",
    "email": "",
    "roles": [],
    "permissions": []
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
email | The email that register 
password | The password to login
customer_token | The token is specific for customer



## Recover

```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:1234" https://api.apieco.ir/manam/auth/recover -d '{"email": "myemail@mail.com"}'


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/auth/recover",
    headers: {
                "apieco_key":"1234"
                'auth_token':"..."
              
            },
    dataType: "json",
    type : "POST",
    data: { email:"myemail@mail.com"}
    success : function(r) {
      console.log(r);
    }
  });
  ```

> The above command returns JSON structured like this:

```json
{
"location": "/",
"message": "An email has been sent to you with further instructions on how to reset your password.",
"status": "success"
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
email | The email that register 


## Refresh Token


```shell

curl -X POST -H "Content-Type: application/json" -H "apieco_key:1234" -H "auth_token:eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI4NjYsImV4cCI6MTQ0NDI2Mjg4Nn0.Dww7TC-d0teDAgsmKHw7bhF2THNichsE6rVJq9xu_2s" -H "refresh_token:fdb8fdbecf1d03ce5e6125c067733c0d51de209c" https://api.apieco.ir/manam/auth/refreshToken 


```

> The above command returns JSON structured like this:

```json
{
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI4NjYsImV4cCI6MTQ0NDI2Mjg4Nn0.Dww7TC-d0teDAgsmKHw7bhF2THNichsE6rVJq9xu_2s",
    "expires_in":20,
    "refresh_token":"7fd15938c823cf58e78019bea2af142f9449696a"
}
```

This endpoint RefreshToken create new refresh token for users.

## View User

```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:1234"  https://api.apieco.ir/manam/view_user/<email>


```

```javascript
$.ajax({
    url: "https://api.apieco.ir/manam/view_user",
    headers: {
                "apieco_key":"1234"
                
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
'{"email":"...",
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



## Get Manam User Info


```shell

curl -X GET -H "Content-Type: application/json" -H "apieco_key:1234"  https://api.apieco.ir/manam/get_manam_user_info/<email>

```

> The above command returns JSON structured like this:

```json
{
   
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



## Google Login (oauth2)
Use this link `<a href="https://api.apieco.ir/manam/googlelogin/[apieco_key]">Google Log In</a>`

Contact to admin for give customer-token


