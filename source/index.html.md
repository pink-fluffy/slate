---
title: Unicorn API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - http

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
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
Remember — a happy kitten is an authenticated kitten!
</aside>
