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

curl -X POST -H "Content-Type: application/json" -H "customer_token:cus-token"  https://api.manam.ir/auth/register -d '{"name": "myyname","email": "myemail@mail.com","password":"password","confirm_password":"password"}'

```

```javascript
$.ajax({
    url: "https://api.manam.ir/auth/register",
    headers: {
                'customer_token': 'cus_token',
         
            },
    dataType: "json",
    type : "POST",
    data: {name:"myname", email:"myemail@mail.com", password:"password", confirm_password:"password", "customer_token":"cus_token"}
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

`POST https://api.manam.ir/auth/register`

### Query Parameters
None.


### Data Params

Parameter | Type 
--------- | ------- 
name | string
email | [string] 
password | [string]
confirm_password | string




## Confirm

```shell

curl -X GET -H "Content-Type: application/json" -H "customer_token:cus-token" https://api.manam.ir/auth/confirm -d {cnf:h-A1iPysWfQ9Mj5EYuCKZo9KJ5UccHTjqABqfL-8bw48fkUQAOhBB-Bbwo2V7AE5TKYYYE9QXpDLrCvImQ57Tw==}
```

```javascript
$.ajax({
    url: "https://api.manam.ir/auth/confirm?cnf=FFL5QDOYTXJZcO3SdcDgd8Kv-_euyLqVwm-eFagHZG_KCBLgtyhUkjFAeeDXvMFVVame3vXKyiWbnpNAVxQI8A==,
    headers: {
                'customer_token': 'cus_token',
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

`GET https://api.manam.ir/auth/confirm/<cnf>/<customer_token>`

### URL Parameters

Parameter | Description
--------- | -----------
cnf | The string that confirm registartion
customer_token | The token that specific for each customer

## Login



```shell

curl -X POST -H "Content-Type: application/json" -H "customer_token:cus_token" https://api.manam.ir/auth/login -d '{"email": "myemail@mail.com","password":"password"}'

```

```javascript
 $.ajax({
    url: "https://api.manam.ir/auth/login",
    headers: {
                'customer_token': 'cus_token',
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

`POST https://api.manam.ir/auth/login`

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

curl -X POST -H "Content-Type: application/json" -H "customer_token:cus_token" https://api.manam.ir/auth/recover -d '{"email": "myemail@mail.com"}'


```

```javascript
$.ajax({
    url: "https://api.manam.ir/auth/recover",
    headers: {
                'customer_token': 'cus_token',
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

`POST https://api.manam.ir/auth/recover`

### URL Parameters

None.

### Data Parameters

Parameter | Description
--------- | -----------
email | The email that register 
customer_token | The token is specific for customer


## Refresh Token


```shell

curl -X POST -H "Content-Type: application/json" -H "customer_token:cus_token" -H "auth_token:eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiVlx1MDAxNcKbwoNUwoonbFPCu8KhwrYiLCJpYXQiOjE0NDQyNjI4NjYsImV4cCI6MTQ0NDI2Mjg4Nn0.Dww7TC-d0teDAgsmKHw7bhF2THNichsE6rVJq9xu_2s" -H "refresh_token:fdb8fdbecf1d03ce5e6125c067733c0d51de209c" https://api.manam.ir/auth/refreshToken 


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


## Google Login (oauth2)
Use this link `<a href="https://api.manam.ir/googlelogin/[customer-token]">Google Log In</a>`

Contact to admin for give customer-token


