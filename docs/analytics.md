# Analytics

## Pixel Events

You can register your pixels with their corresponding tracking IDs and configured events - for particular contents using the [Create Content](https://tsbmediaventure.github.io/developer-docs/#create-content) and [Edit Content](https://tsbmediaventure.github.io/developer-docs/#create-content) APIs. You can pass a 'pixels' object in the request body for either of the APIs - which can contain facebook and/or google pixel data - to ensure that the client's pixel events are fired on particular occurences relating to the content (Page View or Purchase of the Content). The pixel object must be passed in accordance with the format provided in the sample requests. 
Please note that the pixels are NOT fired when a user has blocked 3rd party cookies.

### Request Body

| Parameter | Default  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pixels    | optional | A nested object with the optional keys being "facebook" and "google". With the "google" object only requiring the trackingId - to include the gtag throughout the platform. However, for the "facebook" object the "pixelId" must be passed along with an "events" array - containing the event name (as configured on the facebook events manager), the eventType (which is an ENUM to be chosen from ["VIEW", "CONVERSION"]) as well as any data/values associated with the particular event. |

> The pixel object must passed as a JSON in the request body - structured like this:

```json
{
    "pixels": {
      "facebook": {
        "pixelId": "98357934724994",
        "events": [
          {
            "eventType": "VIEW",
            "name": "PageView"
          },
          {
            "eventType": "CONVERSION",
            "name": "Purchase",
            "data": {
              "value": "dataValue"
            }
          }
        ]
      },
      "google": {
        "trackingId": "G-RJDY8493"
      }
    }
  }
}
```

<aside class="notice">
Remember — if you're including events for the content - you must ensure that no two events in the events array can have the same eventType field.
</aside>
