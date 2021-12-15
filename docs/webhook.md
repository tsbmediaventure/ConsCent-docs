# Webhooks

## User Data Webhook

You can register your webhook endpoint for receiving ConsCent user data by logging in to your ConsCent Client Dashboard and navigating to the [Webhook Page](https://client.conscent.in/dashboard/webhook). You will be able to enable/disable and edit your webhook url from this section. Once the webhook URL is registered and the webhook is in the enabled state - the endpoint will recieve user data (name, email & country of the user) anytime the user logins in for the first time on the client's website or application via ConsCent.

> The webhook returns a JSON in the request body - structured like this:

```json
{
  "phoneNumber": "9818329028",
  "email": "test-email@webhook.com",
  "country": "IN"
}
```

Do note that you will receive either the phoneNumber or the email depending on what the user chooses to log in with.

## Login Webhook

You can register your webhook endpoint for receiving ConsCent user data by logging in to your ConsCent Client Dashboard and navigating to the [Webhook Page](https://client.conscent.in/dashboard/webhook). You will be able to enable/disable and edit your webhook url from this section. Once the webhook URL is registered and the webhook is in the enabled state - the endpoint will recieve user data (name, email, phone number, hashed email & phone number, city, location, address & country of the user) anytime the user logins in on the client's website or application via ConsCent.

> The webhook returns a JSON in the request body - structured like this:

```json
{
  "phoneNumber": "9818329028",
  "email": "test-email@webhook.com",
  "country": "IN",
  "hashedPhoneNumber": "7942mey829mxe1238z2ym9zy39my29zy2z9dy24793msy29z2z",
  "hashedEmail": "8392mx30mx2mu8034x02mx802ry2480nyd249yx420xfn20w4y04xm2024",
  "name": "Test Name",
  "city": "London",
  "location": {
    "latitude": 8359893,
    "longitude": 7438734,
    "postcode": 221993
  },
  "address": {
    "apartment": "7923492 Apartment1",
    "area": "Test Area",
    "pincode": "389023",
    "landmark": "test landmark",
    "city": "New York City",
    "state": "New York",
    "country": "US"
  }
}
```

## Subscription Payment Webhook

You can register your webhook endpoint for receiving ConsCent purchased subscription data by logging in to your ConsCent Client Dashboard and navigating to the [Webhook Page](https://client.conscent.in/dashboard/webhook). You will be able to enable/disable and edit your webhook url from this section. Once the webhook URL is registered and the webhook is in the enabled state - the endpoint will recieve user's purchased subscription data anytime the user purchases a subscription on the client's platform or application via ConsCent. Moreover, the webhook is secured by basic auth using the Clients API Key and API Secret provided by ConsCent on the SDK Integration section of the client dashboard - [ConsCent Client Integration](https://client.conscent.in/dashboard/integration). You can optionally choose to keep the endpoint as protected and authenticate using the provided credentials which are passed in the headers of the POST request to the configured webhook endpoint. 

> The webhook returns a JSON in the request body - structured like this:

```json
{
  "_id": "61b9cf42f5d1f54797aaf14f",
  "renewSubscription": false,
  "availedOffers": [],
  "promotional": false,
  "tags": [],
  "bundle": false,
  "bundleContentIds": [],
  "paymentType": ["NETWORK"],
  "freeTrial": false,
  "migrated": false,
  "userAccount": "61b9cefbf5d1f54797aaf149",
  "clientId": "601a8ea4f2149f089782814f",
  "buyingPrice": 289.5,
  "price": 300,
  "country": "IN",
  "city": "bengaluru (nagashettyhalli)",
  "location": {
    "latitude": 13.0411,
    "longitude": 77.5702,
    "postcode": "560056"
  },
  "userCountry": "IN",
  "expiryDate": "2022-05-15T11:19:30.897Z",
  "priceDetails": {
    "price": 300,
    "currency": "INR"
  },
  "type": "SUBSCRIPTION",
  "subscriptionTitle": "Subscription 5",
  "device": "desktop",
  "subscriptionType": {
    "physical": false,
    "digital": true
  },
  "subscriptionId": "616ffd76621d69c5ee43c044",
  "createdAt": "2021-12-15T11:19:30.914Z",
  "updatedAt": "2021-12-15T11:19:30.914Z",
  "chosenTier": {
    "clientTierId": "Test Tier ID",
    "_id": "616ffd76621d69c5ee437485",
    "price": 300,
    "duration": 5,
    "currency": "INR"
  }
}
```
