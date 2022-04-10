---
title: Unicorn API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - http

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - category
  - brand
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Unicorn API
---

# Introduction

Welcome to the Unicorn API! You can use our API to access Unicorn API endpoints, which can get information on the e-commerce store.

# Response Format

The `data` field can return a single JSON object or an array of JSON objects.

The [error code reference](#errors) explains the message for each error code.

> The response from the API returns JSON structured like this.

```json
{
  "data": {
    "foo": "bar"
  },
  "message": "success message or error code reference"
}
```

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint" \
  --header "Authorization: Bearer meowmeowmeow"
```

> Make sure to replace `pinkfluffyunicorns` with your API key.

Unicorn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer pinkfluffyunicorns`

<aside class="notice">
You must replace <code>pinkfluffyunicorns</code> with your personal API key.
</aside>

# Identity

## Register User

```shell
curl --header "Content-Type: application/json" \
  --request POST \
  --data  $body \
  "http://api.unicorn.com/user/register"
```

```json
  body = {
    "first_name":"Sergio",
    "last_name": "Verstappen",
    "email": "per@ver.rb",
    "password":"pinkfluffypassword"
  }
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "name": "Sergio Verstappen",
    "email": "per@ver.rb",
    "accessToken": "eyJ1c2VySWQiOiI2MjQ1NDE4NDliOTM1ODI1NDNjZjNkYjMiLCJl",
    "refreshToken": null
  },
  "message": "Created"
}
```

> or

```json
{ "data": null, "message": "User already exists" }
```

This endpoint registers a new user.

### HTTP Request

`POST http://api.unicorn.com/user/register`

### Body

| Parameter  | Description                                                                |
| ---------- | -------------------------------------------------------------------------- |
| first_name | User's first name. Minimum 3 characters. No numbers or special characters. |
| last_name  | User's last name. Minimum 3 characters. No numbers or special characters.  |
| email      | User's valid email.                                                        |
| password   | User's password. Minimum 12 characters. Atleast one number.                |

### Response

| Parameter    | Description                              |
| ------------ | ---------------------------------------- |
| name         | User's full name.                        |
| email        | User's registered email.                 |
| accessToken  | Authentication token for registerd user. |
| refreshToken | `null`                                   |

## Login User

```shell
curl --header "Content-Type: application/json" \
  --request POST \
  --data  $body \
  "http://api.unicorn.com/user/login"
```

```json
  body = {
    "email": "per@ver.rb",
    "password":"pinkfluffypassword"
  }
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "accessToken": "eyJ1c2VySWQiOiI2MjQ1NDE4NDliOTM1ODI1NDNjZjNkYjMiLCJl",
    "refreshToken": null
  },
  "message": "OK"
}
```

> or

```json
{ "data": null, "message": "Incorrect credentials" }
```

This endpoint verifies the entered credentials and issues an access token to authenticated users.

### HTTP Request

`POST http://api.unicorn.com/user/login`

### Body

| Parameter | Description              |
| --------- | ------------------------ |
| email     | User's registered email. |
| password  | User's password.         |

### Response

| Parameter    | Description                              |
| ------------ | ---------------------------------------- |
| accessToken  | Authentication token for registerd user. |
| refreshToken | `null`                                   |

<aside class="success">
Remember — a happy unicorn is an authenticated unicorn!
</aside>

# Products

## Add Product

```shell
curl --header "Content-Type: application/json" \
  --request POST \
  --data  $body \
  "http://api.unicorn.com/product/add"
```

```json
  body = {
    "name": "Fresh Milk",
    "category": "DAIRY",
    "brand": "Nelson",
    "description": "500mL fresh cow milk from Ontario",
    "price": 5.99,
    "stock": 100
    }
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "name": "Fresh Milk",
    "category": "DAIRY",
    "brand": "Nelson",
    "description": "500mL fresh cow milk from Ontario",
    "price": 5.99,
    "stock": 100
  },
  "message": "Created"
}
```

> or

```json
{ "data": null, "message": "Product already exists" }
```

This endpoint adds a new product to the store catalog.

### HTTP Request

`POST http://api.unicorn.com/product/add`

### Body

| Parameter   | Description                                                      |
| ----------- | ---------------------------------------------------------------- |
| name        | Product name.                                                    |
| category    | Product category. Value should be in [CATEGORY](#category) list. |
| brand       | Product brand. Value should be in [BRAND](#brand) list.          |
| description | Product description.                                             |
| price       | Product price in CAD.                                            |
| stock       | Available stock of product.                                      |

### Response

| Parameter   | Description                    |
| ----------- | ------------------------------ |
| name        | Product name.                  |
| category    | Product [category](#category). |
| brand       | Product [brand](#brand).       |
| description | Product description.           |
| price       | Product price in CAD.          |
| stock       | Available stock of product.    |

## Get All Products

```shell
curl "http://api.unicorn.com/product/getAll"
```

> The above command returns JSON structured like this:

```json
{
  "data": [{
    "short_id": "Pmkfy5",
    "name": "Fresh Milk",
    "category": "DAIRY",
    "brand": "Nelson",
    "description": "500mL fresh cow milk from Ontario",
    "price": 5.99,
    "stock": 100
  },...],
  "message": "OK"
}
```

This endpoint retrieves all the products from the store catalog.

### HTTP Request

`POST http://api.unicorn.com/product/getAll`

### Response

The endpoint responds with an array of products with the following fields.

| Parameter   | Description                    |
| ----------- | ------------------------------ |
| name        | Product name.                  |
| category    | Product [category](#category). |
| brand       | Product [brand](#brand).       |
| description | Product description.           |
| price       | Product price in CAD.          |
| stock       | Available stock of product.    |

## Filter Products

```shell
curl "http://api.unicorn.com/product?brand=Nelson&category=DAIRY"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "short_id": "Pmkfy5",
      "name": "Fresh Milk",
      "category": "DAIRY",
      "brand": "Nelson",
      "description": "500mL fresh cow milk from Ontario",
      "price": 5.99,
      "stock": 100
    },
    {
      "short_id": "UmDfz9",
      "name": "Swiss Cheese",
      "category": "DAIRY",
      "brand": "Nelson",
      "description": "500g fresh swiss cheese",
      "price": 7.25,
      "stock": 120
    }
  ],
  "message": "OK"
}
```

This endpoint filters products by category and/or brand.

### HTTP Request

`POST http://api.unicorn.com/product`

### Query Parameters

| Parameter | Description                                                           |
| --------- | --------------------------------------------------------------------- |
| brand     | Brand to filter by. Value should be in [BRAND](#brand) list.          |
| category  | Category to filter by. Value should be in [CATEGORY](#category) list. |

### Response

The endpoint responds with an array of products with the following fields.

| Parameter   | Description                    |
| ----------- | ------------------------------ |
| name        | Product name.                  |
| category    | Product [category](#category). |
| brand       | Product [brand](#brand).       |
| description | Product description.           |
| price       | Product price in CAD.          |
| stock       | Available stock of product.    |
