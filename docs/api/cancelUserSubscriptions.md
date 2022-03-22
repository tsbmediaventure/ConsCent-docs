# Cancel Active Subscriptions for a Particular User

The client can cancel the active subscripptions for a user 

**URL** : `{API_URL}/client/cancel-subscriptions/{userId}`

**Method** : `POST`

**Auth required** : YES

Please pass your api key as username and api secret as password as basic auth to access the endpoint

## Success Response

**Code** : `200 OK`

**Content examples**

```json

{
    "message": "Subscriptions Cancelled Successfully"
}

```