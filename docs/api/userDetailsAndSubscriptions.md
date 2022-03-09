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
        "secondaryEmail": "",
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
    "userSubscriptions": [
        {
            "_id": "62273ffbd5c69afcd7c05349",
            "client": "Outlook",
            "price": 1000,
            "purchasedOn": "2022-03-08T11:37:31.537Z",
            "subscriptionTitle": "Subscription test physical",
            "expiryDate": "2022-04-08T11:37:31.518Z",
            "subscriptionType": {
                "physical": true,
                "digital": false
            },
            "benefits": "Easy access to contents",
            "logoUrl": "https://conscent-public.s3.ap-south-1.amazonaws.com/stage/Outlook/banners/Outlook%20-%20brandLogo",
            "rzpSubscriptionId": "sub_J4a4NYpUc0qDMU",
            "status": "ACTIVE",
            "freeTrial": false,
            "tierId": "61a49984fabe8d7705a2cabd",
            "clientId": "5f92a62013332e0f667794dc",
            "gstComponents": {
                "physical": 0,
                "digital": 0
            },
            "subscriptionDurationInMonths": 1,
            "subscriptionPriceInInr": 1000,
            "allowCancellation": true,
            "cancellationUrl": "http://localhost:3000/consumption?subscription=62273ffbd5c69afcd7c05349",
            "allowRenewal": false,
            "renewalUrl": ""
        }
    ]
}
```
