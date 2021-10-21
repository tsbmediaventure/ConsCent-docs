### Using ConsCent to only display the paywall for users who have their adblock enabled

This guide covers a quick and simple integration process with no backend or CMS changes to enables passes for users who use an ad-blocker.

We assume you have access to the client dashboard - if you do not, please contact team ConsCent.

The first step is to sign in to your dashboard, go to the manage passes section, add a pass with a duration (in hours) and the price you decide, e.g. 10 rs for 24 hours.

Second step is to include the sdk in the header of your html page.

```
    <script>
    const clientId = '{replace_with_clientId}';
    (function (w, d, s, o, f, cid) {
        if (!w[o]) {
        w[o] = function () {
            w[o].q.push(arguments);
        };
        w[o].q = [];
        }
        (js = d.createElement(s)), (fjs = d.getElementsByTagName(s)[0]);
        js.id = o;
        js.src = f;
        js.async = 1;
        js.title = cid;
        fjs.parentNode.insertBefore(js, fjs);
    })(window, document, 'script', '_csc', '{replace_with_sdk_url}', clientId);
    </script>
```

- Replace {replace_with_sdk_url} with

  - 'https://sandbox-sdk.conscent.in' for sandbox (test mode)
  - 'https://sdk.conscent.in' for production

- Replace {replace_with_clientId} with your clientId which can be found in your client dashboard

### Third step is to show the paywall in premium articles.

- You need to wrap your premium content (premium portion of your article) in a div with a CSS property of display:none

- Insert a blank div on your page with the id 'csc-paywall', where you would like the paywall to render.

- Initialize the conscent paywall. If the ad blocker is not present, the paywall will automatically unhide your premium content.

Run the following code in the page of your premium article.

```
       const csc = window._csc;
       csc('init', {
         contentId: {contentId}, // substitute with a unique id for the current content / story
         clientId: {clientId}, // substitute with client id available on your dashboard
         title: {contentTitle}, // substitute with the title of the content
         successCallback: () => {},
         debug: true,
         wrappingElementId: 'csc-paywall',
         // Following fields are optional
         accentColor: '#red'
         buttonMode: false,
         fullScreenMode: 'false',
       })
```

Make sure you substitute the contentId, clientId and title!

An explanation of these parameters is outlined in [integrations](integration.md#Concepts). If you would like to use other parameters you can review them too.
