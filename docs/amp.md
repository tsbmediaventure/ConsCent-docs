## Integration on AMP Pages

Since custom javascript isn't allowed on AMP Pages, and you cannot directly include the web-sdk on AMP pages, there is a slightly different integration process for AMP Pages.
This involves adding a few tags to your AMP pages based on your method of integration.

_As of now AMP integration only works with the content registration method_

### AMP Integration methods

1. Tag based
2. Dynamic

Both methods are very similar except the dynamic method requires you to register your premium content with ConsCent and only works with text content. The trade-off in tag based integration is that the content is present in the DOM, only invisible. This might be a plus point if you are worried about losing out on SEO when the content is completely not present.

### How to Integrate

**Please check the [amp-example.html](./amp/amp-example.html) and [amp-example-dynamic.html](./amp/amp-example-dynamic.html) to view full html pages**

0. **(Dynamic mode only)** When registering content on ConsCent via API calls, include the premium html of your content in the 'ampContent' field.

1. Include the amp access tag in your AMP page

```
    <script id="amp-access" type="application/json">
      {
        "authorization": "{API_URL}/api/v1/content/amp?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)",
        "login": "{FRONTEND_URL}/overlay?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)&returnUrl=RETURN_URL",
        "pingback": "https://pub.com/amp-ping?rid=READER_ID&url=SOURCE_URL",
        "authorizationFallbackResponse": { "granted": true },
        "noPingback": true
      }
    </script>
    <script
      async
      custom-element="amp-access"
      src="https://cdn.ampproject.org/v0/amp-access-0.1.js"
    ></script>
```

Please get the value or API_URL and FRONTEND_URL from the urls section of the Readme. ClientId is your unique clientId available on your dashboard and clientContentId is Id of the content you have registered on ConsCent.

2. Add a paywall for users who do not have access

````
    <div amp-access="NOT granted" amp-access-hide>
      <div
        on="tap:amp-access.login"
        style="
          color: green;
          display: flex;
          align-items: center;
          justify-content: center;
          background: black;
          color: white;
          font-size: 23px;
          font-family: Verdana, Geneva, Tahoma, sans-serif;
          margin: 4px;
          padding: 8px;
          cursor: pointer;
        "
      >
        <a>Unlock the full article now!</a>
      </div>
    </div>
    ```
````

Please note that only the outer div is important, you should design your own 'unlock / read more' tag within the outer div. A placeholder design has been included in the above code.

3. Place your premium content within the following tag

```
    <div amp-access="granted" amp-access-hide> THIS IS PREMIUM CONTENT </div>
```

_For dynamic mode, your content will not be present within the tags, use the following code instead -_

```
      <div amp-access="granted" amp-access-hide>
        <template amp-access-template type="amp-mustache">
          {{{cscContent}}}
        </template>
      </div>
```
