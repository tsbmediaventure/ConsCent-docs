## Functions

### Get User Details from SDK

Get ConsCent user details by initialising the CSC 'user-details' function and passing a callback function in the arguments where the user details will be passed by ConsCent:

```
const csc = window._csc;
csc('user-details', {
  userDetailsCallback: yourUserDetailsCallbackFunction,
})
```

example invokation:
`window._csc('user-details', { userDetailsCallback: (e) => console.log(e)})`

Parameters explained:

- 'userDetailsCallback' this parameter takes a function which receives the ConsCent user details as an input arguments. The argument contains a field called 'userDetailsMatch' which is set to true if the user details (user name - phone number or email of the user) match the default details passed by the client whilst initalising the CSC paywall.

Example userDetailsCallback argument for Logged In User:

    {
        "address": {
            "apartment": "",
            "area": "",
            "pincode": "",
            "landmark": "",
            "city": "",
            "state": "",
            "country": ""
        },
        "wallet": {
            "balance": {
                "$numberDecimal": "200.00"
            },
            "currency": "INR"
        },
        "name": "",
        "_id": "61b9cefbf5d1f54797aaf149",
        "phoneNumber": "8945793793",
        "country": "IN",
        "promotionalOptIn": true,
        "lastPurchasedOn": "2021-12-15T11:19:30.942Z"
        "userDetailsMatch": true,
        "loggedIn": true,
        "hashedEmail": "43983m220m7249y29yr2803y107924mx42r7x2rm80x4xm84mx7m27240m5742x2x924",
        "hashedPhoneNumber": "mx8x024mr4x03mxyx4802242mx04x7x42x724x024x84x84x",
        "previousSubscriber": true,
        "existingSubscriber": false
    }

Example userDetailsCallback argument for Not Logged In User:

    {
        "loggedIn": false,
        "userDetailsMatch": false
    }

### Get Subscription Details from SDK

Get ConsCent user details by initialising the CSC 'subscription-details' function and passing a callback function in the arguments where the user details will be passed by ConsCent:

```
const csc = window._csc;
csc('subscription-details', {
  callbackFunction: yourSubscriptionDetailsCallbackFUnction,
})
```

example invokation:
`window._csc('user-details', { callbackFunction: (e) => console.log(e)})`

Parameters explained:

- 'callbackFunction' this parameter takes a function which receives the ConsCent subscription details as an input arguments.

Example subscription details argument for Logged In User:
(the subscription details can contain more than one object if the user has purchased multiple subscriptions)

```

    {
        "loggedIn": true,
        "subscriptionDetails": [
            {
                "_id": "62188c8ceda7ab612d841230",
                "client": "clientName",
                "price": 201,
                "purchasedOn": "2022-02-25T08:00:12.719Z",
                "subscriptionTitle": "Physical and Dibital subscription",
                "expiryDate": "2022-04-25T08:00:12.714Z",
                "subscriptionType": {
                    "physical": true,
                    "digital": true
                },
                "benefits": "Unlimited access to premium digital content,Magazine delivered to your doorstep before they hit newsstands",
                "logoUrl": "https://conscent-public.s3.ap-south-1.amazonaws.com/stage/Outlook/banners/Outlook%20-%20brandLogo",
                "freeTrial": false,
                "tierId": "6180db518634ae0b03c136b5",
                "clientId": "5f92a62013332e0f667794dc",
                "gstComponents": {
                    "physical": 0,
                    "digital": 0
                },
                "subscriptionDurationInMonths": 2,
                "subscriptionPriceInInr": 201,
                "allowCancellation": false,
                "cancellationUrl": "",
                "allowRenewal": true,
                "renewalUrl": "http://localhost:3000/consumption?subscription=62188c8ceda7ab612d841230"
            }
        ]

    }

```

Example callback argument for Not Logged In User:
```
    {
        "loggedIn": false,
        "subscriptionDetails": false
    }

```

### Log User out of ConsCent

Log the user out by calling the CSC 'logout' function and passing a callback function in the arguments where the logout result be passed by ConsCent:

````

const csc = window.\_csc;
csc('logout', {
logoutCallback: yourUserDetailsCallbackFunction,
})

```

example invokation:
`window._csc('user-details', { logoutCallback: (e) => console.log(e)})`

Possible Responses:

Failure Case:
{ error: 'user-not-logged-in' }

Success Case:
{ message: 'Successfully logged out of all devices' }
```
