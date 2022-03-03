# Purchased Subscriptions endpoint

Get the details of previously purchased subscriptions

**URL** : `{API_URL}/client/purchases/subscriptions`

**Method** : `GET`

**Auth required** : YES

Please pass your api key as username and api secret as password as basic auth to access the endpoint

## Query Parameters

**from**: ISODateString, to filter via a starting datetime

**to**: ISODateString, to filter via an ending datetime

**userId**: Pass conscent's user Id to filter purchases for one particular user

**pageSize**: Max Number of records returned per page - defaults to 500. Max possible value is 2000

**pageNumber**: The page number

## Success Response

**Code** : `200 OK`

**Content examples**

```json
{
  "purchases": [
    {
      "manuallyRenewed": false,
      "renewSubscription": false,
      "availedOffers": ["617ba48ec3b5066393988f22"],
      "promotional": false,
      "categories": [],
      "freeTrial": false,
      "migrated": false,
      "clientId": "5f92a62013332e0f667794dc",
      "clientContentId": "Client Story Id 1",
      "contentId": "5fbe46efbee15f1cebc81515",
      "buyingPrice": 100.36,
      "price": 104,
      "priceDetails": {
        "price": 104,
        "currency": "INR"
      },
      "subscriptionDetails": {
        "inrPrice": 104,
        "duration": 1
      },
      "expiryDate": "2022-03-28T12:49:02.844Z",
      "subscriptionId": "61a49855fabe8d7705a2cab4",
      "tierId": "61a49855fabe8d7705a2cab6",
      "userId": "613720ec6a14e1100bdfb9f5",
      "userEmail": "asdf@sdf.co",
      "userPhoneNumber": "129347792",
      "userName": "asdf",
      "userAddress": {
        "apartment": "",
        "area": "",
        "pincode": "",
        "landmark": "",
        "city": "",
        "state": "",
        "country": ""
      },
      "clientSpecificUserId": "234234612"
    },
    {
      "manuallyRenewed": false,
      "renewSubscription": false,
      "availedOffers": [],
      "promotional": false,
      "categories": [],
      "freeTrial": false,
      "migrated": false,
      "clientId": "5f92a62013332e0f667794dc",
      "clientContentId": "Client Story Id 1",
      "contentId": "5fbe46efbee15f1cebc81515",
      "buyingPrice": 193.97,
      "price": 201,
      "priceDetails": {
        "price": 201,
        "currency": "INR"
      },
      "subscriptionDetails": {
        "inrPrice": 201,
        "duration": 2
      },
      "expiryDate": "2022-04-25T08:00:12.714Z",
      "subscriptionId": "617a718d04ab353a12d84d30",
      "tierId": "6180db518634ae0b03c136b5",
      "userId": "5fca03a52185f150382ff144",
      "userEmail": "test+stagetest@test.com",
      "userPhoneNumber": "9999999999",
      "userName": "test name",
      "userAddress": {
        "apartment": "India",
        "area": "India",
        "pincode": "123423",
        "landmark": "India",
        "city": "test",
        "state": "ANDHRA PRADESH",
        "country": "IN"
      },
      "clientSpecificUserId": "234234612"
    }
  ],
  "paginationInfo": {
    "pageNumber": 1,
    "pageSize": 2,
    "recordsReturned": 2
  }
}
```
