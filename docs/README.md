# ConsCent Docs

### Before you begin

You must have contacted or been contacted by the ConsCent team and have access to your ConsCent Dashboard.

Your clientId, API_KEY and API_SECRET are available in the dashboard in the SDK integration section. (Present on the sidebar)

NEVER expose your API_SECRET. Do NOT use it in the frontend-side of your website.

If you are only interested in receiving donations from users, you can read about [accepting donations here](donations.md)

_Please note that this is the developer documentation, for information on making requests to ConsCent APIs, please consult the [API documentation](https://tsbmediaventure.github.io/developer-docs/)_

### Table of Contents

- Getting started
- Sandbox and Production
  - Making fake payments in sandbox
- URLs list
- Working with APIs
- Understanding ConsCent flow
- Which integration to choose?
- Integration Methods
  - Content registration
  - Blanket pricing
  - Hashcode based integration
- [AMP Support](amp.md)
- Pricing strategies
  - International Pricing
  - Different price in India and abroad
  - Category based pricing
- Customizing the paywall
  - Screen type
  - Subscription
  - Sign-in
  - Translucency
  - Button Mode
- [Webhooks](webhook.md)
- [Analytics](analytics.md)
- [Donations](donations.md)
- [Tagging](tagging.md)

### Getting Started

If you are unsure on which integration is for you, please read which integration to choose. Once satisfied, you can read up on how your desired integration flow works and then dabble in customizing the paywall.

### Sandbox and Production

Sandbox and production are two separate ConsCent environments that you will work with while integrating ConsCent. The difference between the two is that sandbox lets you make fake payments that you can make to test out your integration.
The typical customer users sandbox in their staging servers and production on their live deployment.
Switching environments is a matter of using separate keys / conscent urls.

##### Making fake payments in sandbox

Depending on your country/currency you will get Paytm or Razorpay prompts

###### Paytm

The easiest way to make a fake payment is to choose netbanking, any bank and proceed.

###### Razorpay

https://razorpay.com/docs/payment-gateway/test-card-upi-details/

### URLs

API_URL is the base for all API requests to ConsCent.
SDK_URL is the URL of the web SDK usually included in your website
FRONTEND_URL is the URL of the ConsCent user dashboard (only used in some cases)

These differ according to your environment.

##### Sandbox:

API_URL: https://sandbox-api.conscent.in  
SDK_URL: https://sandbox-sdk.conscent.in  
FRONTEND_URL: https://sandbox-user.conscent.in

##### Production:

API_URL: https://api.conscent.in  
SDK_URL: https://sdk.conscent.in  
FRONTEND_URL: https://user.conscent.in

### Working with APIs

The API Specification can be found here:  
https://tsbmediaventure.github.io/developer-docs

It outlines all the APIs available to you and how to authenticate for the same.
The authentication is as follows -
Client API Key and Secret must be passed in Authorization Headers using Basic Auth. With API Key as the Username and API Secret as the password.
If you are unsure how to generate the header, [please use this](https://www.blitter.se/utils/basic-authentication-header-generator/)

### Understanding ConsCent web flow

The general ConsCent web flow consists of:-

1. The ConsCent SDK being included in your website
2. The ConsCent SDK being initialized to show the paywall
3. The user interacting with the paywall and completing the conscent flow which means they either-

- signed up and paid for the story
- were logged in and only paid for the story, or
- had already recently paid for the story

4. Your frontend website is notified that it has to show the content premium content

The implementation of the steps depend on the the integration method of your choosing.

### Which Integration method to choose?

There are three main ways to integrate ConsCent.

1. Content registration - This method gives you control over the price for each content. For this to work, your CMS needs to make API calls to register metadata on each priced content to ConsCent's backend servers.
2. Blanket pricing - This method is useful for a quick proof of concept or if you have very limited control over your backend/cms
3. Hashcode registration - Similar to content registration flow, useful if you are not able to make API calls from your backend/CMS. Content meta-data is securely hashed before-hand and then the hashed code is used to initialize the paywall client side. This method is not currently supported on Android/iOS and AMP pages.

You can find detailed instructions in integration page for each method.
