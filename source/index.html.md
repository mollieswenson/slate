---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript  

toc_footers:
  - <a href='https://github.com/mollieswenson'>API source code on Github</a>
  - <a href='http://mswenson.com'>See my portfolio</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the FoodTruck API! You can use this API to access FoodTruck API endpoints, which you can use to get and modify information about local foodtrucks.

You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> Use this code to authenticate:

```shell
#Pass your JWT token in the Authorization header when
#making requests that require authentication
curl "api_endpoint_goes_here" -H "Authorization: Bearer token_goes_here"
```

```javascript
const foodtruck = require('foodtruck');

let api = foodtruck.authorize('token_goes_here');
```
> Make sure to replace `token_goes_here` with your token.

FoodTruck uses JSON Web Tokens (JWT) to allow POST, PUT, and DELETE access to the API. FoodTruck expects a JWT token to be included in all POST, PUT, and DELETE API requests to the server.

For the purposes of demonstrating this API, include the below header and JWT token to authenticate with the server for POST (except registration), PUT, and DELETE requests.

`Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVhMTYxNDZlMTNkZjNlMTUxYWEzZjQyZSIsImlhdCI6MTUxMTM5NjY5NywiZXhwIjoxNTEzOTg4Njk3fQ.0YB9WlPxTdfMb5ysZO1qKRjrOgeHKmLVqVxfbkb4gTo`

<aside class="notice">
FoodTruck JWT tokens expire after 30 days.
</aside>

# FoodTrucks

## Get all trucks

```shell
curl -X GET "https://mollieswenson.com/api/v1/foodtruck"
```

```javascript
const foodtruck = require('foodtruck');

let trucks = api.trucks.get();
```
> The above command returns JSON structured like this:

```json
[
    {
        "_id": "5a170b72e843ef23f66b4c38",
        "avgcost": 7.99,
        "foodtype": "Breakfast",
        "name": "Pancake Hut",
        "reviews": [],
        "geometry": {
            "coordinates": [10.7, 20.5],
            "type": "Point"
        }
    },
    {
        "_id": "5a17129cfde1be05c23eb00e",
        "avgcost": 2.99,
        "foodtype": "Aemrican",
        "name": "Funk Dave's Diner",
        "reviews": [],
        "geometry": {
            "coordinates": [10.9, 44.8],
            "type": "Point"
        }
    }
]
```

This endpoint retrieves all trucks.

### HTTP Request

`GET https://mollieswenson.com/api/v1/foodtruck`

<aside class="success">
GET requests don't require authentication!
</aside>






## Get a specific truck

```shell
curl -X GET "https://mollieswenson.com/api/v1/foodtruck/5a170b72e843ef23f66b4c38"
```

```javascript
const foodtruck = require('foodtruck');

let max = api.trucks.post('');
{"name": "Jen's Juice Shoppe", "foodtype": "Juice", "avgcost": 9.99, "geometry": {"coordinates": [55.89,41.24]}}
```

This endpoint retreivews a specific truck

### HTTP Request

`GET https://mollieswenson.com/api/v1/foodtruck/[id]`

### URL Parameters

Parameter | Description
--------- | -----------
ID (required) | The ID of the truck to retrieve






## Get trucks by food type

```shell
curl -X GET "https://mollieswenson.com/api/v1/foodtruck/foodtype/breakfast"
```

```javascript
const foodtruck = require('foodtruck');

let max = api.trucks.get('foodtype=breakfast');
```

> The above command returns JSON structured like this:

```json
{
    "_id": "5a170b72e843ef23f66b4c38",
    "avgcost": 7.99,
    "foodtype": "Breakfast",
    "name": "Pancake Hut",
    "reviews": [],
    "geometry": {
        "coordinates": [10.7, 20.5],
        "type": "Point"
    },
    "_id": "9s174b43e843ef23f66b4d55",
    "avgcost": 7.99,
    "foodtype": "Breakfast",
    "name": "Waffle Way",
    "reviews": [],
    "geometry": {
        "coordinates": [15.7, 42.5],
        "type": "Point"
    }
}
```

This endpoint retrieves a list of trucks by food type.

### HTTP Request

`GET https://mollieswenson.com/api/v1/foodtruck/foodtype/[foodtype]`

### URL Parameters

Parameter | Description
--------- | -----------
foodtype (required) | The food type to retrieve






## Add a food truck

```shell
curl -X POST "https://mollieswenson.com/api/v1/foodtruck/add"
-H "Authorization: Bearer token_goes_here"
-d "name": "Jen's Juice Shoppe"
-d "foodtype": "Juice"
-d "avgcost": 9.99
-d "geometry": {"coordinates": [55.89,41.24]
```

```javascript
const foodtruck = require('foodtruck');

let max = api.trucks.get('foodtype=breakfast');
```

This endpoint adds a new food truck to the database.

### HTTP Request

`POST https://mollieswenson.com/api/v1/foodtruck/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
name (required) | The name of the food truck.
foodtype (required) | The type of food available at the food truck.
avgcost (required) | The average cost of meals at this food truck.
geometry (required) | Contains coordinates, an array with two numerical values.









## Modify a food truck

```shell
curl -X PUT "https://mollieswenson.com/api/v1/foodtruck/5a170b72e843ef23f66b4c38"
-H "Authorization: Bearer token_goes_here"
-d "name": "Jen's Juice and Bagels"
-d "foodtype": "Breakfast"
-d "avgcost": 10.99
-d "geometry": {"coordinates": [-32.65,99.24]
```

```javascript
TODO
```

This endpoint modifies an existing food truck.

### HTTP Request

`PUT https://mollieswenson.com/api/v1/foodtruck/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
name (optional) | The name of the food truck.
foodtype (optional) | The type of food available at the food truck.
avgcost (optional) | The average cost of meals at this food truck.
geometry (optional) | Contains coordinates, an array with two numerical values.







## Delete a truck

```shell
curl -X DELETE "https://mollieswenson.com/api/v1/foodtruck/5a170b72e843ef23f66b4c38"
-H "Authorization: Bearer token_goes_here"
```

```javascript
TODO
```

This endpoint deletes a food truck.

### HTTP Request

`DELETE https://mollieswenson.com/api/v1/foodtruck/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID (required) | The ID of the food truck to delete


#Reviews

##Add a review

```shell
curl -X POST "https://mollieswenson.com/api/v1/foodtruck/reviews/add/5a170b72e843ef23f66b4c38"
-H "Authorization: Bearer token_goes_here"
-d "title" : "title_here"
-d "text" : "text_here"
```

```javascript
TODO
```

This endpoint adds a review to a specific food truck.

### HTTP Request

`POST https://mollieswenson.com/api/v1/foodtruck/review/add/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
id (required) | The ID of the food truck to add the review to
title (required) | The title of the reviews
text (required) | The body text of the review


##Get reviews for a truck

```shell
curl -X GET "https://mollieswenson.com/api/v1/foodtruck/reviews/5a170b72e843ef23f66b4c38"
```

```javascript
TODO
```

This endpoint retrieves all reviews assigned to a specific food truck.

### HTTP Request

`GET https://mollieswenson.com/api/v1/foodtruck/review/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
id (required) | The ID of the food truck to retrieve reviews for


#Accounts

##Register a user account

> Use this code to register an account.

```shell
curl -X POST "https://mollieswenson.com/api/v1/account/register"
  -d "email": "example1@gmail.com"
	-d "password": "password12345"
```

```javascript
TODO
```

This endpoint registers new user accounts.

<aside class="notice">
Registration does not require authentication.
</aside>

### HTTP Request

`POST https://mollieswenson.com/api/v1/account/register`

### URL Parameters

Parameter | Description
--------- | -----------
email (required) | The registering user's email address
password (required) | The registering user's password






##Get a user's account details

> Use this code to get details of a user account.

```shell
curl -X POST "https://mollieswenson.com/api/v1/account/me"
  -H "Authorization: Bearer _token_goes_here"
```

```javascript
TODO
```
> The above command returns JSON structured like this:

```json
{
    "id": "5a16146e13df3e151aa3f42e",
    "iat": 1511396697,
    "exp": 1513988697
}
```

This endpoint retrieves a user's account details.

### HTTP Request

`GET https://mollieswenson.com/api/v1/account/me`

### URL Parameters

This endpoint does not require a parameter to identify the user. The user is identified by the JWT token.






##Log in to a user account

> Use this code to log in to an account.

```shell
curl -X POST "https://mollieswenson.com/api/v1/account/register"
  -d "email": "example1@gmail.com"
	-d "password": "password12345"
```

```javascript
TODO
```

This endpoint logs in a user account.

### HTTP Request

`POST https://mollieswenson.com/api/v1/account/login[id]`

### URL Parameters

Parameter | Description
--------- | -----------
email (required) | The user's email address
password (required) | The user's password







##Log out of a user account

> Use this code to log out of an account.

```shell
curl -X POST "https://mollieswenson.com/api/v1/account/logout"
  -d "id": "5a16146e13df3e151aa3f42e"
```

```javascript
TODO
```

This endpoint logs out a user account.

### HTTP Request

`POST https://mollieswenson.com/api/v1/account/logout/[id]`

### URL Parameters

Parameter | Description
--------- | -----------
id (required) | The user's id
