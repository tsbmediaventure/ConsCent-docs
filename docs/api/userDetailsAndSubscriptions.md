# Get UserDetials and Subscriptions endpoint

Get the user Details and subscriptions

**URL** : `{API_URL}/user/user-and-subscription-details`

**Method** : `GET`

**Auth required** : NO

## Query Parameters

**clientId**: Pass clientId of the client

**userId**: Pass conscent's user Id to get the user details


## Success Response

**Code** : `200 OK`

**Content examples**

```json
{
    "userdetails": {
        "name": "AKHIL",
        "email": "testmail51@gmail.com",
        "secondaryPhoneNumber": "9832748888",
        "secondaryEmail":"",
        "dateOfBirth": "1999-01-01T09:50:21.951Z",
        "address": {
            "apartment": "ouy",
            "area": "029384kdsjf",
            "pincode": "530009",
            "landmark": "fj",
            "city": "8732489",
            "state": "",
            "country": "IN"
        },
        "country": "IN",
        "promotionalOptIn": true,
        "lastPurchasedOn": "2022-03-08T11:37:31.667Z",
        "wallet": {
            "balance": {
                "$numberDecimal": "50.00"
            },
            "currency": "INR"
        }
    },
    "subscriptionDetails": {
        "location": {
            "latitude": 13.0411,
            "longitude": 77.5702,
            "postcode": "560056"
        },
        "gstComponents": {
            "physical": 0,
            "digital": 0
        },
        "inrGstComponents": {
            "physical": 0,
            "digital": 0
        },
        "manuallyRenewed": false,
        "renewSubscription": true,
        "availedOffers": [],
        "promotional": false,
        "categories": [],
        "bundle": false,
        "bundleContentIds": [],
        "paymentType": [
            "NEW"
        ],
        "freeTrial": false,
        "migrated": false,
        "_id": "62273ffbd5c69afcd7c05349",
        "userAccount": "622726d267e3aa84a68ed0f7",
        "clientId": "5f92a62013332e0f667794dc",
        "clientContentId": "Client Story Id 3",
        "contentId": "5fbe46efbee15f1cebc81517",
        "buyingPrice": 965,
        "price": 1000,
        "country": "IN",
        "city": "bengaluru (nagashettyhalli)",
        "userCountry": "IN",
        "expiryDate": "2022-04-08T11:37:31.518Z",
        "priceDetails": {
            "price": 1000,
            "currency": "INR"
        },
        "type": "SUBSCRIPTION",
        "subscriptionTitle": "Subscription test physical",
        "operatingSystem": "Mac OS",
        "device": "desktop",
        "subscriptionType": {
            "physical": true,
            "digital": false
        },
        "subscriptionId": "61a49984fabe8d7705a2cabb",
        "tierId": "61a49984fabe8d7705a2cabd",
        "renewalId": "62273fe8d5c69afcd7c05347",
        "renewalDetails": {
            "price": 1000,
            "currency": "INR"
        },
        "subscriptionDetails": {
            "inrPrice": 1000,
            "duration": 1
        },
    }
}
```
