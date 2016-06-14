---
title: TXODDS Mobile API Reference

language_tabs:
  - shell
  - java
  - ObjectiveC
  - javascript

toc_footers:
  - <a href='https://txodds.com/registers'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the TXODDS Mobile API! You can use this API to access our unique match information data including Previews, OCI Reports and Team News.

API endpoints include support for authentication; new account registration; loading user information and updating user preferences.


# Authentication

## Login

```shell
curl -X POST -d \
     'login=demo-user&password=opensesame&device_id=device-123&device_type=ios' \
     https://txodds.com/api/login
```

```java

```

```ObjectiveC

```

```javascript

```

> The above command returns JSON structured like this:

```json
{
   "resp_status":{
      "message":"OK",
      "code":0,
      "errors":null
   },
   "user_details":{
      "login":"demo-user",
      "email":"demo-user@txodds.com",
      "first_name":"Demo",
      "last_name":"User",
      "country":"GB",
      "locale":"en",
      "subscriptions":[
         {
            "name":"TRADER",
            "expiry":1502535462.0
         }
      ],
      "user_token":"1234abcd-1234-abcd-1234-1234abcd1234",
      "permissions":[
         "g:pro",
         "g:moves"
      ],
      "settings":{
         "notifications":true,
         "language":"en"
      },
      "profile_url":"http://txodds.com/profiles/demo-user"
   }
}
```

This endpoint authenticates an existing user and returns all account information. 

Each user is only permitted to have 2 active registered devices for TXODDS mobile applications, this requires that when a login request is made the unique device Id of the user's handset is submitted.

### HTTP Request

`POST https://txodds.com/api/login`

### Query Parameters

Parameter | Required | Description | Options
--------- | -------- | ----------- | -------
login | true | The user's unique login name. | 
password | true | The user's password |
device_id | true | The unique device Id that the user is using. |
device_type | true | The device operating system. | android, ios
language | false | The language to choose upon login. | en, it, zh

<aside class="notice">
Remember — a user may only have 2 active registered devices. Do deactivate a device the user must log into their profile on the website https://txodds.com/
</aside>

## Register

```shell
curl -X POST -d \
     'login=demo-user&email=demo-user@txodds.com&firstname=Demo&lastname=User&password=opensesame&device_id=device-123&device_type=ios' \
     https://txodds.com/api/register
```

```java

```

```ObjectiveC

```

```javascript

```

> The above command returns JSON structured like this:

```json
{
   "resp_status":{
      "message":"OK",
      "code":0,
      "errors":null
   },
   "user_details":{
      "login":"demo-user",
      "email":"demo-user@txodds.com",
      "first_name":"Demo",
      "last_name":"User",
      "country":"GB",
      "locale":"en",
      "subscriptions":[
         {
            "name":"TRADER",
            "expiry":1502535462.0
         }
      ],
      "user_token":"1234abcd-1234-abcd-1234-1234abcd1234",
      "permissions":[
         "g:pro",
         "g:moves"
      ],
      "settings":{
         "notifications":true,
         "language":"en"
      },
      "profile_url":"http://txodds.com/profiles/demo-user"
   }
}
```

This endpoint will create a new user account at TXODDS. The user will be able to use this account to access all of TXODDS services.

<aside class="notice">TXODDS users various product subscriptions to control access to certain data and products. By default a new user account without a subscription will be able to access the mobile app but will only have access to Previews data.</aside>

### HTTP Request

`POST https://txodds.com/api/register`

### URL Parameters

Parameter | Required | Description | Options
--------- | -------- | ----------- | -------
login | true | The user's unique login name. | 
email | true | The user's email address |
firstname | true | The user's first name |
lastname | true | The user's last name or surname |
password | true | The user's password |
tel | false | The user's telephone number |
country | false | 2 letter country code |
device_id | true | The unique device Id that the user is using. |
device_type | true | The device operating system. | android, ios


## Subscribe Device

```shell
curl -X POST -d \
     'user_token=1234abcd-1234-abcd-1234-1234abcd1234&device_token=ABCZXY42492384092&device_id=device-123&device_type=ios' \
     https://txodds.com/api/subscribe-device
```

```java

```

```ObjectiveC

```

```javascript

```

> The above command returns JSON structured like this:

```json
{"success": true}
```

This endpoint will subscribe the user's device for push notifications produced by the server. When new content is created for the app, users can receive notification of this.

It is recommended that this endpoint be called after each user login.

### HTTP Request

`POST https://txodds.com/api/subscribe-device`

### URL Parameters

Parameter | Required | Description | Options
--------- | -------- | ----------- | -------
user_token | true | The user session token. |
device_token | true | The device's publish token |
device_id | true | The unique device Id that the user is using. |
device_type | true | The device operating system. | android, ios

<aside class="notice">
You must replace `user_token` with the token value returned from login.
</aside>


# User Information

## Get User Details

```shell
curl -X POST -d \
     'user_token=1234abcd-1234-abcd-1234-1234abcd1234' \
     https://txodds.com/api/get-user-details
```

```java

```

```ObjectiveC

```

```javascript

```

> The above command returns JSON structured like this:

```json
{
   "resp_status":{
      "message":"OK",
      "code":0,
      "errors":null
   },
   "user_details":{
      "login":"demo-user",
      "email":"demo-user@txodds.com",
      "first_name":"Demo",
      "last_name":"User",
      "country":"GB",
      "locale":"en",
      "subscriptions":[
         {
            "name":"TRADER",
            "expiry":1502535462.0
         }
      ],
      "user_token":"1234abcd-1234-abcd-1234-1234abcd1234",
      "permissions":[
         "g:pro",
         "g:moves"
      ],
      "settings":{
         "notifications":true,
         "language":"en"
      },
      "profile_url":"http://txodds.com/profiles/demo-user"
   }
}
```

This endpoint returns the same user details information that is returned after a success login.


### HTTP Request

`POST https://txodds.com/api/get-user-details`

### URL Parameters

Parameter | Required | Description
--------- | -------- | -----------
user_token | true | The user session token.

<aside class="notice">
You must replace `user_token` with the token value returned from login.
</aside>


## Get User Profiles


> The above command returns JSON structured like this:

```json
{
    "resp_status": {
        "message": "OK",
        "code": 0,
        "errors": null
    },
    "profiles": [
        {
            "is_active": false,
            "id": 26,
            "name": "All Bookmakers"
        },
        {
            "is_active": true,
            "id": 20268,
            "name": "Good books"
        },
        {
            "is_active": false,
            "id": 20269,
            "name": "Arbs"
        },
        {
            "is_active": false,
            "id": 20271,
            "name": "default"
        },
        {
            "is_active": false,
            "id": 20272,
            "name": "tennis"
        },
        {
            "is_active": false,
            "id": 20276,
            "name": "Asian + Totals"
        },
        {
            "is_active": false,
            "id": 20277,
            "name": "Italian Books"
        }
    ]
}
```

### HTTP Request

`POST https://txodds.com/api/get-user-profiles`

### URL Parameters

Parameter | Required | Description
--------- | -------- | -----------
user_token | true | The user session token.

<aside class="warning">
Yet to be documented
</aside>


## Get User Profile

> The above command returns JSON structured like this:

```json

 {
    "profile": {
        "leagues": [],
        "is_active": false,
        "sort_order": null,
        "odds_types": [],
        "id": 20277,
        "vs_at": null,
        "name": "Italian Books",
        "sports": [],
        "books": [
            109,
            110,
            126,
            238,
            291,
            342,
            413,
            475,
            567,
            613
        ],
        "default_sport": "all",
        "default_day": "today",
        "widgets": [],
        "display_format": "euro"
    },
    "resp_status": {
        "message": "OK",
        "code": 0,
        "errors": null
    }
}
```


### HTTP Request

`POST https://txodds.com/api/get-user-profile`

### URL Parameters

Parameter | Required | Description
--------- | -------- | -----------
user_token | true | The user session token.
profile_id | true | The Id of the user profile to load.

<aside class="warning">
Yet to be documented
</aside>
