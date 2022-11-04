---
title: Carton Caps API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Carton Caps API
---

# Carton Caps API Reference

Welcome to the official Carton Caps API reference page! You can use the Carton Caps API to access Carton Caps user information including referral records.

# Documention

For information regarding API endpoints and example requests/responses, you're in the right spot.
Scroll down to see which endpoints are available, and be sure to checkout the `curl` examples on the right-hand side as well.

For additional documention, please see the following:

- [Project repository](https://github.com/sephraim/carton_caps_api) - Get up and running locally with the Carton Caps API
- [API design documentation](design-docs.pdf) - Discover how the Carton Caps mobile app interacts with the API

# Requirements

In order to use this API, you must be running the Carton Caps API application on your local machine.
See [here](https://github.com/sephraim/carton_caps_api) for how to do that.


# Users

## Get All Users

```shell
curl -LX GET 'http://localhost:3000/api/v1/users'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "first_name": "Lisa",
    "last_name": "Simpson",
    "birthdate": "1981-05-09",
    "zip_code": 62629,
    "referral_code": "V3GAN5",
    "links": {
      "self": "http://localhost:3000/api/v1/users/1",
      "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/1/referrer",
          "referees": "http://localhost:3000/api/v1/users/1/referees"
      }
    }
  },
  {
    "id": 2,
    "first_name": "Marge",
    "last_name": "Simpson",
    "birthdate": "1956-10-01",
    "zip_code": 62629,
    "referral_code": "BLU3RR",
    "links": {
      "self": "http://localhost:3000/api/v1/users/2",
      "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/2/referrer",
          "referees": "http://localhost:3000/api/v1/users/2/referees"
      }
    }
  }
]
```

This endpoint retrieves all users.

### HTTP Request

`GET http://localhost:3000/api/v1/users`

## Get A Specific User

```shell
curl -LX GET 'http://localhost:3000/api/v1/users/1'
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "first_name": "Lisa",
  "last_name": "Simpson",
  "birthdate": "1981-05-09",
  "zip_code": 62629,
  "referral_code": "V3GAN5",
  "links": {
    "self": "http://localhost:3000/api/v1/users/1",
    "referrals": {
        "referred_by": "http://localhost:3000/api/v1/users/1/referrer",
        "referees": "http://localhost:3000/api/v1/users/1/referees"
    }
  }
}
```

This endpoint retrieves a specific user.

### HTTP Request

`GET http://localhost:3000/api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | User ID

## Create A New User

```shell
curl -LX POST 'http://localhost:3000/api/v1/users' \
-H 'Content-Type: application/json' \
--data-raw '
  {
    "first_name": "Maggie",
    "last_name": "Simpson",
    "birthdate": "1989-01-01",
    "zip_code": 62629,
    "referral_code_used": "V3GAN5"
  }'
```

> The above command returns JSON of the newly created user structured like this:

```json
{
  "id": 5,
  "first_name": "Maggie",
  "last_name": "Simpson",
  "birthdate": "1989-01-01",
  "zip_code": 62629,
  "referral_code": "P4CIFR",
  "links": {
    "self": "http://localhost:3000/api/v1/users/5",
    "referrals": {
      "referred_by": "http://localhost:3000/api/v1/users/5/referrer",
      "referees": "http://localhost:3000/api/v1/users/5/referees"
    }
  }
}
```

This endpoint creates a new user. If a valid referral code is passed in then a new referral record will be created as well.

### HTTP Request

`POST http://localhost:3000/api/v1/users`

### Request Body

Parameter | Required?   | Type | Description
--------- | ----------- | ----------- | -----------
first_name    | Yes | string | First name
last_name     | Yes | string | Last name
birthdate     | Yes | string | Date of birth, e.g. "1989-01-01"
zip_code      | Yes | number | Zip code, e.g. 62629
referral_code | No  | string | Existing user's referral code, e.g. "V3GAN5"

## Delete a Specific User

```shell
curl -LX DELETE 'http://localhost:3000/api/v1/users/4' --data-raw ''
```

> The above command will return HTTP Status Code 204 (No Content) on successful deletion.


This endpoint deletes a specific user.

### HTTP Request

`DELETE http://localhost:3000/api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | User ID

# Referrals

## Get All Referrals

```shell
curl -LX GET 'http://localhost:3000/api/v1/referrals'
```

> The above command returns JSON structured like this:

```json
[
  {
    "completed_at": "2022-11-04T05:19:34.330Z",
    "referrer": {
      "id": 2,
      "first_name": "Marge",
      "last_name": "Simpson",
      "birthdate": "1956-10-01",
      "zip_code": 62629,
      "referral_code": "BLU3RR",
      "links": {
        "self": "http://localhost:3000/api/v1/users/2",
        "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/2/referrer",
          "referees": "http://localhost:3000/api/v1/users/2/referees"
        }
      }
    },
    "referee": {
      "id": 4,
      "first_name": "Homer",
      "last_name": "Simpson",
      "birthdate": "1956-05-12",
      "zip_code": 62629,
      "referral_code": "DFB33R",
      "links": {
        "self": "http://localhost:3000/api/v1/users/4",
        "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/4/referrer",
          "referees": "http://localhost:3000/api/v1/users/4/referees"
        }
      }
    }
  }
]
```

This endpoint retrieves all referrals by all users unless filtering using the query parameters below.

### HTTP Request

`GET http://localhost:3000/api/v1/referrals`

### Query Parameters

Parameter  | Description
---------- | ------------
referrer_id | Filter referrals by a specific user ID where they are the referrer
referee_id  | Filter referrals by a specific user ID where they are the referee

## Get A Specific User's Referees

```shell
curl -LX GET 'http://localhost:3000/api/v1/users/2/referees'
```

> The above command returns JSON structured like this:

```json
{
  "referrer": {
    "id": 2,
    "first_name": "Marge",
    "last_name": "Simpson",
    "birthdate": "1956-10-01",
    "zip_code": 62629,
    "referral_code": "BLU3RR",
    "links": {
      "self": "http://localhost:3000/api/v1/users/2",
      "referrals": {
        "referred_by": "http://localhost:3000/api/v1/users/2/referrer",
        "referees": "http://localhost:3000/api/v1/users/2/referees"
      }
    }
  },
  "referees": [
    {
      "id": 4,
      "first_name": "Homer",
      "last_name": "Simpson",
      "birthdate": "1956-05-12",
      "zip_code": 62629,
      "referral_code": "DFB33R",
      "links": {
        "self": "http://localhost:3000/api/v1/users/4",
        "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/4/referrer",
          "referees": "http://localhost:3000/api/v1/users/4/referees"
        }
      }
    }
  ]
}
```

This endpoint retrieves a specific user's completed referrals (referees).

### HTTP Request

`GET http://localhost:3000/api/v1/users/<ID>/referees`

### URL Parameters

Parameter | Description
--------- | -----------
ID | User ID

## Get A Specific User's Referrer

```shell
curl -LX GET 'http://localhost:3000/api/v1/users/2/referrer'
```

> The above command returns JSON structured like this:

```json
{
  "referrer": {
  "id": 1,
  "first_name": "Lisa",
  "last_name": "Simpson",
  "birthdate": "1981-05-09",
  "zip_code": 62629,
  "referral_code": "V3GAN5",
  "links": {
    "self": "http://localhost:3000/api/v1/users/1",
    "referrals": {
      "referred_by": "http://localhost:3000/api/v1/users/1/referrer",
      "referees": "http://localhost:3000/api/v1/users/1/referees"
    }
  }
  },
  "referees": [
    {
      "id": 2,
      "first_name": "Marge",
      "last_name": "Simpson",
      "birthdate": "1956-10-01",
      "zip_code": 62629,
      "referral_code": "BLU3RR",
      "links": {
        "self": "http://localhost:3000/api/v1/users/2",
        "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/2/referrer",
          "referees": "http://localhost:3000/api/v1/users/2/referees"
        }
      }
    },
    {
      "id": 3,
      "first_name": "Bart",
      "last_name": "Simpson",
      "birthdate": "1979-02-23",
      "zip_code": 62629,
      "referral_code": "G3TBNT",
      "links": {
        "self": "http://localhost:3000/api/v1/users/3",
        "referrals": {
          "referred_by": "http://localhost:3000/api/v1/users/3/referrer",
          "referees": "http://localhost:3000/api/v1/users/3/referees"
        }
      }
    }
  ]
}
```

This endpoint retrieves a specific user's referrer as well as all of the referrer's completed referrals (referees).

### HTTP Request

`GET http://localhost:3000/api/v1/users/<ID>/referrer`

### URL Parameters

Parameter | Description
--------- | -----------
ID | User ID
