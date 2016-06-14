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

## Set User Preferences

```shell
curl -X POST -d \
     'user_token=1234abcd-1234-abcd-1234-1234abcd1234&language=en&notifications=true' \
     https://txodds.com/api/set-preferences
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
   "message": "changed: 2", 
   "success": true
}
```

### HTTP Request

`POST https://txodds.com/api/set-preferences`

### URL Parameters


Parameter | Required | Description | Options
--------- | -------- | ----------- | -------
user_token | true | The user session token. |
language | false | The user's selected language. | en, it, zh
notifications | false | Whether to receive push notifications | true, false


## Get User Profiles

```shell
curl -X POST -d \
     'user_token=1234abcd-1234-abcd-1234-1234abcd1234' \
     https://txodds.com/api/get-user-profiles
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


## Get User Profile

```shell
curl -X POST -d \
     'user_token=1234abcd-1234-abcd-1234-1234abcd1234&profile_id=20277' \
     https://txodds.com/api/get-user-profile
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


# Application Data

## Loading Initial App Data

```shell
curl -X POST -d \
     'user_token=d5be71fe-96dd-4af1-95e3-77e49face214' \
     https://txodds.com/api/initial-data
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
   "previews":[
      {
         "body":"<p>Lionel Messi has just returned to training, training with the ball and there is a chance that he will play against Chile. It is up to Messi himself, according to their coach. Messi has endured back problems and he is tired after some hectic travelling lately.  As the other two teams in this group are Bolivia and Panama this game between the Copa America finalists last time around is not that important. L Biglia will miss this game and N Gaitan is the one likely to replace Messi, if necessary. Over the years it has become quite clear that Messi does not reach the same heights playing for Argentina,  as he does playing for Barcelona.</p><p>M Fernandez is injured and he has been replaced by M Gonzalez in the Chilean squad. Key players as always for Chile are of course A Sanchez and A Vidal.</p><p>G Higuain, Kun Aguero, Di Maria, yes,  Argentina have some outstanding offensive players in their team even without L Messi and their midfield line is also top class with E Banega, Mascherano and J Pastore likely starters.</p><p>I would back the Argentinian win.</p>",
         "updated":1465201480.0,
         "event_date":1465264800.0,
         "match_link":"https://txodds.com/odds+comparison/html?peid=3530854",
         "id":29397,
         "description":"Preview for Argentina v Chile",
         "league":"FBINT Copa America-16",
         "title":"Argentina v Chile",
         "url":"https://txodds.com/match-info/29397/argentina-v-chile",
         "created":1465201480.0,
         "created_by":"jamespunt"
      }
   ],
   "moves":[
      {
         "body":"<h2><strong>OCI Report</strong></h2><p><strong>Market Move on Panama ( 137.75% OCI )</strong></p><p><strong><em>Reason: &nbsp;QUALITY / TEAM NEWS</em></strong></p><p><strong>Panama</strong> are a defensive side and don't concede many goals. And held their won against bigger teams Brazil, Mexico and Uruguay in the last year. They are missing Torres (df 98/8).</p><p><strong>Bolivia</strong> look very poor and have lost 9 of their last 10 games! They are also missing key players and their top scorer. Bolivia without Vaca (gk 14/0), Morales (df 10/0), Cardoza (mf 37/5), Chumacero (mf 31/2), Bejarano (mf 16/0), Pedriel (att 20/3) and Moreno (att 54/14 top scorer).</p><p><strong><em>Panama 1.72 &nbsp;Draw 3.39 &nbsp;Bolivia 5.47</em></strong></p><p><a href=\"https://txodds.com/odds+comparison/html?peid=3530853&ot=0\">https://txodds.com/odds+comparison/html?peid=35308...</a></p>",
         "updated":1465202850.0,
         "event_date":1465254000.0,
         "match_link":"https://txodds.com/odds+comparison/html?peid=3530853",
         "id":29398,
         "description":"OCI Report for Panama v Bolivia",
         "league":"Copa America",
         "title":"Panama v Bolivia",
         "url":"https://txodds.com/match-info/29398/panama-v-bolivia",
         "created":1465202850.0,
         "created_by":"kellyeden"
      }
   ],
   "news":[
      {
         "body":"<h2><strong>Market Information</strong></h2><p><strong>France</strong>&nbsp;missing Varane (df 29/2), Sakho (df 28/2), Debuchy (df 27/2), Diarra (mf 34/0), Valbuena (mf 52/8), Lacazette (att 10/1), Gameiro (att 8/1) and Benzema (att 81/27 top scorer).</p><p><strong>Romania</strong>&nbsp;are without Papp (df 18/3), Goian (df 59/5), Tamas (df 65/3), Gardos (df 13/0), Maxim (mf 28/2) and Rusescu (att 10/1).</p><p><strong><em>Possible Line-ups:</em></strong></p><p><strong>France:</strong> Lloris, Sagna, Rami, Koscielny, Evra, Pogba, Kante, Matuidi, Payet, Griezmann, Giroud.</p><p><strong>Romania:&nbsp;</strong>Tatarusanu, Sapunaru, Chiriches, Grigore, Rat, Pintilii, Hoban, Popa, Stanciu, Stancu, Andone.</p><p><strong><em>Info: &nbsp;</em></strong>France are unbeaten in their last 10 games against Romania (W5, D5). However, four of their last five encounters have ended in draws.&nbsp;Romania's last victory against France was a 2-0 friendly win in Bucharest in April 1972.&nbsp;Romania have kept a clean sheet in 7 of their last 8 matches</p><p><strong><em><br></em></strong></p><p><strong><em>France 1.33 &nbsp;Draw 4.81 &nbsp;Romania 10.73</em></strong></p><p><a href=\"https://txodds.com/odds+comparison/html?peid=3453592\">https://txodds.com/odds+comparison/html?peid=34535...</a></p>",
         "updated":1465538977.0,
         "event_date":1465585200.0,
         "match_link":"https://txodds.com/odds+comparison/html?peid=3453592",
         "id":29423,
         "description":"Team News for France v Romania",
         "league":"Euro 2016 - Group A",
         "title":"France v Romania",
         "url":"https://txodds.com/match-info/29423/france-v-romania",
         "created":1465538977.0,
         "created_by":"kellyeden"
      }
   ]
}
```

### HTTP Request

`POST https://txodds.com/api/initial-data`

### URL Parameters

Parameter | Required | Description
--------- | -------- | -----------
user_token | true | The user session token.


## Previews Data

## OCI Reports Data

## Team News Data



