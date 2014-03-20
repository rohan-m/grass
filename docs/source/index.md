---
title: Identity API Specs

language_tabs:
  - shell

toc_footers:
 - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>
---

# Introduction

Welcome to the Grass APIs !!

This example API documentation page was created with [Slate](http://github.com/tripit/slate).

# Token Validation

## Create Token
> Request:

```shell
curl
  "http://api.example.com/v1/token/{type}/{identifier}"
  --verbose
  --request POST
  --header  "apikey: {client_id}"
  --header  "content-type: application/json"
  --data    "{"type":"alphanumeric / numeric etc","length":6,"text":"One time PIN: {token} has been generated for your request# 12346","expiry":300}"
```

> Response:

```http
HTTP/1.1 200 OK
```

This endpoint creates a Token, and sends it to the given identifier.

### HTTP Request

`POST http://api.example.com/v1/token/{type}/{identifier}`

### Path Parameters

Parameter | Required | Values | Description
--------- | -------- | ------ | -----------
type | true | sms, email | type of service
identifier | true | +919xxxx, xxx@gmail.com | identifier using the service

### Body
Parameter | Values | Description
--------- | ------ | -----------
type | alphanumeric, numeric | type of the token to be generated
length | 7 | generated token's length
text | One time PIN: {token} | sample text, with placeholder for token
expiry | 300 | in seconds

<aside class="success">
Body is of JSON type. Please look at the curl request, to learn more.
</aside>


<aside class="success">
Upon successful, Developer gets a 200 OK
</aside>

<aside class="warning">
Upon failure, Developer gets a 400 Bad Request
</aside>

## Validate Token
> Request:

```shell
curl
  "http://api.example.com/v1/token/{type}/{identifier}/{token}"
  --verbose
  --request GET
  --header  "apikey: {client_id}"
```

> Response:

```http
HTTP/1.1 200 OK
```

This endpoint validates a Token, with its identifier.

### HTTP Request

`GET http://api.example.com/v1/token/{type}/{identifier}/{token}`

### Path Parameters

Parameter | Required | Values | Description
--------- | -------- | ------ | -----------
type | true | sms, email | type of service
identifier | true | +919xxxx, xxx@gmail.com | identifier using the service
token | true | xd4f67^ | user submitted token, that he/she has received

<aside class="success">
If Token is valid for the given identifier, Developer gets a 200 OK
</aside>

<aside class="warning">
If Token is not valid for the given identifier, Developer gets a 400 Bad Request
</aside>

## Response Codes

The Token API uses the following status codes:

Status Code | Meaning
----------- | -------
200 | OK -- You are cool, dude !!
400 | Bad Request -- Your request sucks, go home man !!##@@



# User Management
This API is supposed to proxy the Usergrid API, and provide a SPI reference for
the other adapters. This will be invoked by the Identity API, and is a internal
facing API.

## Authorization
User Management API is an internal facing one, and thus requires only apikey
validation.

## Create User
> Request:

```shell
curl
  "http://api.example.com/v1/users"
  --verbose
  --request POST
  --header  "apikey: {client_id}"
  --header  "content-type: application/json"
  --data    "{"personal-info":{"name":{"surname":"Shell","given":"Ron","title":"Mr","complete":"Mr. Ron Shell"},"dob":"12-12-1980","gender":"male","image":"http://gravatar.com/avatar/d43903a7f1db7f4246ecdd6hj6ed54gh","secrets":{"what is your dob":"54431df57f827c3d38b49dd2bf9a29fa","what is your birthplace":"11d0c7bdbc6cade41f2b2fcb36ac6b90"}},"external-info":{"id":"rshell","crmid":1238347384728723700,"dept":"something"},"email":{"0":"xyz@some.com","1":"abc@another.com"},"phone":{"0":"+561234567890","1":"+561234567891","2":"+561234567892"},"address":{"house":"number something","street":"something","locality":"another","city":"some","state":"some","country":"another","postalcode":"4FCDG78","landmark":"near some market"},"social":{"twitter":"handle","google":"plusprofile","facebook":"faceid","live":"windowsliveid"},"groups":["somegroup1","somegroup2","somegroup3"]}"
```

> Response:

```http
HTTP/1.1 201 Created

{
    "id": "b1615ce7-0f73-464d-bb15-45f701015aa0",
    "metadata": {
        "type": "user",
        "created": 1394800072652,
        "modified": 1394800072652,
        "uri": "https://api.example.com/v1/users/b1615ce7-0f73-464d-bb15-45f701015aa0"
    },
    "personal-info": {
        "name": {
            "surname": "Shell",
            "given": "Ron",
            "title": "Mr",
            "complete": "Mr. Ron Shell"
        },
        "dob": "12-12-1980",
        "gender": "male",
        "image": "http://gravatar.com/image/id/1238347384728723839",
        "secrets": {
            "what is your dob": "54431df57f827c3d38b49dd2bf9a29fa",
            "what is your birthplace": "11d0c7bdbc6cade41f2b2fcb36ac6b90"
        }
    },
    "external-info": {
        "id": "rshell",
        "crmid": 1238347384728723700,
        "dept": "something",
        "custom": {
            "salaryindex": "150K"
        }
    },
    "username": "rshell",
    "email": {
        "0": "xyz@some.com",
        "1": "abc@another.com"
    },
    "phone": {
        "0": "+561234567890",
        "1": "+561234567891",
        "2": "+561234567892"
    },
    "address": {
        "house": "number something",
        "street": "something",
        "locality": "another",
        "city": "some",
        "state": "some",
        "country": "another",
        "postalcode": "4FCDG78",
        "landmark": "near some market"
    },
    "social": {
        "twitter": "handle",
        "google": "plusprofile",
        "facebook": "faceid",
        "live": "windowsliveid",
        "skype": "skypeid",
        "linkedin": "profileid",
        "personaluri": "bloguri"
    },
    "groups": [
        "somegroup1",
        "somegroup2",
        "somegroup3"
    ]
}
```

###Purpose
CREATE a User entity

### HTTP Request

`POST http://api.example.com/v1/users`


### Body
Body is self-explanatory. Please look at the curl request, to learn more


<aside class="success">
Upon successful, Developer gets a 201 Created
</aside>

<aside class="warning">
Upon failure, Developer gets a 400 Bad Request
</aside>

## Get User
> Request:

```shell
curl
  "http://api.example.com/v1/users/{userid/email/username}"
  --verbose
  --request GET
  --header  "apikey: {client_id}"
```

> Response:

```http
HTTP/1.1 200 OK

{
    "id": "b1615ce7-0f73-464d-bb15-45f701015aa0",
    "metadata": {
        "type": "user",
        "created": 1394800072652,
        "modified": 1394800072652,
        "uri": "https://api.example.com/v1/users/b1615ce7-0f73-464d-bb15-45f701015aa0"
    },
    "personal-info": {
        "name": {
            "surname": "Shell",
            "given": "Ron",
            "title": "Mr",
            "complete": "Mr. Ron Shell"
        },
        "dob": "12-12-1980",
        "gender": "male",
        "image": "http://gravatar.com/image/id/1238347384728723839",
        "secrets": {
            "what is your dob": "54431df57f827c3d38b49dd2bf9a29fa",
            "what is your birthplace": "11d0c7bdbc6cade41f2b2fcb36ac6b90"
        }
    },
    "external-info": {
        "id": "rshell",
        "crmid": 1238347384728723700,
        "dept": "something",
        "custom": {
            "salaryindex": "150K"
        }
    },
    "username": "rshell",
    "email": {
        "0": "xyz@some.com",
        "1": "abc@another.com"
    },
    "phone": {
        "0": "+561234567890",
        "1": "+561234567891",
        "2": "+561234567892"
    },
    "address": {
        "house": "number something",
        "street": "something",
        "locality": "another",
        "city": "some",
        "state": "some",
        "country": "another",
        "postalcode": "4FCDG78",
        "landmark": "near some market"
    },
    "social": {
        "twitter": "handle",
        "google": "plusprofile",
        "facebook": "faceid",
        "live": "windowsliveid",
        "skype": "skypeid",
        "linkedin": "profileid",
        "personaluri": "bloguri"
    },
    "groups": [
        "somegroup1",
        "somegroup2",
        "somegroup3"
    ]
}
```

###Purpose
GET a User entity

### HTTP Request

`GET http://api.example.com/v1/users/{userid/email/username}`


<aside class="success">
Upon successful, Developer gets a 200 OK
</aside>

<aside class="warning">
Upon failure, Developer gets a 400 Bad Request
</aside>

## Update User
> Request:

```shell
curl
  "http://api.example.com/v1/users/{userid/email/username}"
  --verbose
  --request PUT
  --header  "apikey: {client_id}"
  --header  "content-type: application/json"
  --data    "{"personal-info":{"name":{"surname":"Shell","given":"Ron","title":"Mr","complete":"Mr. Ron Shell"},"dob":"12-12-1980","gender":"male","image":"http://gravatar.com/avatar/d43903a7f1db7f4246ecdd6hj6ed54gh","secrets":{"what is your dob":"54431df57f827c3d38b49dd2bf9a29fa","what is your birthplace":"11d0c7bdbc6cade41f2b2fcb36ac6b90"}},"external-info":{"id":"rshell","crmid":1238347384728723700,"dept":"something"},"email":{"0":"xyz@some.com","1":"abc@another.com"},"phone":{"0":"+561234567890","1":"+561234567891","2":"+561234567892"},"address":{"house":"number something","street":"something","locality":"another","city":"some","state":"some","country":"another","postalcode":"4FCDG78","landmark":"near some market"},"social":{"twitter":"handle","google":"plusprofile","facebook":"faceid","live":"windowsliveid"},"groups":["somegroup1","somegroup2","somegroup3"]}"
```

> Response:

```http
HTTP/1.1 200 OK

{
    "id": "b1615ce7-0f73-464d-bb15-45f701015aa0",
    "metadata": {
        "type": "user",
        "created": 1394800072652,
        "modified": 1394800072652,
        "uri": "https://api.example.com/v1/users/b1615ce7-0f73-464d-bb15-45f701015aa0"
    },
    "personal-info": {
        "name": {
            "surname": "Shell",
            "given": "Ron",
            "title": "Mr",
            "complete": "Mr. Ron Shell"
        },
        "dob": "12-12-1980",
        "gender": "male",
        "image": "http://gravatar.com/image/id/1238347384728723839",
        "secrets": {
            "what is your dob": "54431df57f827c3d38b49dd2bf9a29fa",
            "what is your birthplace": "11d0c7bdbc6cade41f2b2fcb36ac6b90"
        }
    },
    "external-info": {
        "id": "rshell",
        "crmid": 1238347384728723700,
        "dept": "something",
        "custom": {
            "salaryindex": "150K"
        }
    },
    "username": "rshell",
    "email": {
        "0": "xyz@some.com",
        "1": "abc@another.com"
    },
    "phone": {
        "0": "+561234567890",
        "1": "+561234567891",
        "2": "+561234567892"
    },
    "address": {
        "house": "number something",
        "street": "something",
        "locality": "another",
        "city": "some",
        "state": "some",
        "country": "another",
        "postalcode": "4FCDG78",
        "landmark": "near some market"
    },
    "social": {
        "twitter": "handle",
        "google": "plusprofile",
        "facebook": "faceid",
        "live": "windowsliveid",
        "skype": "skypeid",
        "linkedin": "profileid",
        "personaluri": "bloguri"
    },
    "groups": [
        "somegroup1",
        "somegroup2",
        "somegroup3"
    ]
}
```

###Purpose
UPDATE a User entity

### HTTP Request

`PUT http://api.example.com/v1/users/{userid/email/username}`


### Body
Body is self-explanatory. Please look at the curl request, to learn more


<aside class="success">
Upon successful, Developer gets a 200 OK
</aside>

<aside class="warning">
Upon failure, Developer gets a 400 Bad Request
</aside>

## Delete User
> Request:

```shell
curl
  "http://api.example.com/v1/users/{userid/email/username}"
  --verbose
  --request DELETE
  --header  "apikey: {client_id}"
```

> Response:

```http
HTTP/1.1 200 OK
```

###Purpose
DELETE a User entity

### HTTP Request

`DELETE http://api.example.com/v1/users/{userid/email/username}`


<aside class="success">
Upon successful, Developer gets a 200 OK
</aside>

<aside class="warning">
Upon failure, Developer gets a 400 Bad Request
</aside>