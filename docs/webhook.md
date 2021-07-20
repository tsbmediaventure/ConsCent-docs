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
