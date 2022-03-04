## Before you begin

All integration processes are divided in 2 segments, one segment is in your backend/CMS and the other is on your frontend. Your frontend can be a website, a mobile application or an AMP page. The AMP, and mobile integrations are covered in their respective pages and the web initialization is covered in the concepts section on this page.

If only want to use the passes feature, you do not need to use hashcode method or content registration. You can directly skip to the web / frontend integration. You will however have to configure a pass in the integration section of your client dashboard. [Check out passes here](passes.md)

Additionally, if you want to microprice pdf downloads or unlock a group of contents together check out [downloads](features/downloads.md) and [bundling](features/bundling.md)

At this point, you must also have access to your client id, api key and api secret (it is obtained by going to your your client dashboard > Integration > SDK)

## Content Registration

1. Modify your CMS and backend -

   1. Your content should have a paid / unpaid toggle (for your own purposes and to tell your frontend whether it should initialize ConsCent or not)
   1. Your CMS should only return partial content or no content when a paid content is requested.
   1. Your CMS must make a create / update call when paid content is created/edited as outlined here: https://tsbmediaventure.github.io/developer-docs/#create-content
   1. Modify your backend to return premium content only when a valid conscent consumption Id is provided by your frontend site. This consumption Id must be verified with conscent's backend as shown as here: https://tsbmediaventure.github.io/developer-docs/#validate-content-consumption

1. Modify your frontend as show in [Concepts](#Concepts) if its a website, or visit the relevant android / ios / amp pages.

## Hashcode Method

Follow all steps in the Content Registration flow, except you do not need to make a create / update call when paid content is created or modified. Instead, you must generate a hash on the fly and pass it to your frontend website. This hash will contain all information about the content in a signed format. (JWT)
This method avoids the trouble of having to register all your existing premium content.

Integration steps: -

1. Include all details of the post request body that is used for creating the content (as shown here https://tsbmediaventure.github.io/developer-docs/#create-content) in a an object (POJO-like object), lets say the object is named contentDetails.

2. Use any jwt library and sign the contentDetails object with your client secret. The generated hash is the hashcode required by conscent. **Make sure you never leak your client secret to your frontend website**

3. Pass the hashcode to your frontend website

4. Your frontend website must pass the hashCode to the conscent init function, described in the web initialization section below.

## Blanket Method

1. Set a default price, default duration & optionally international price overrides in your integration section.
2. Follow frontend initialization instructions to render the paywall

## Concepts

### Web initialization of SDK

1.  Add this code to the head section of your website

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

    Please replace {replace_with_clientId} with your client id and {replace_with_sdk_url} with the corresponding sdk_url as mentioned in [the urls section](Readme.md#URLs)

2.  On the premium content page -

    1. Create a blank div element, position it where you want the conscent paywall to render and give it an id attribute. This element must have space of a minimum width of 320 pixels and a minimum height of 550 pixels for the conscent paywall to fit properly.

    2. Initialize the paywall with the following code:

       ```
       const csc = window._csc;
       csc('init', {
         contentId: {contentId},
         clientId: {clientId},
         title: {contentTitle},
         categories=['category1', 'category2', 'category3']
         subTitle: {contentSubtitle},
         category:{contentCategory},
         successCallback: yourSuccessCallbackFunction,
         debug: true,
         wrappingElementId: 'csc-paywall',
         // Following fields are optional
         accentColor: '#bbaaff'
         subscriptionUrl: {subscriptionUrl},
         signInUrl: {clientSignInUrl},
         buttonMode: false,
         fullScreenMode: 'false',
         translucencyId:'id-translucency',
         CSCIconPosition: 'right',
         CSCIconOffset: '72%',
         hashCode: 'your-hashcode', // mandatory if using hashcode flow
         adBlockOnly: false,
         hiddenElemId: '',
         defaultPhone: '9898989898',
         defaultEmail: 'test@email.com',
         defaultname: 'John Doe',
         internalUserId: '10000000000'
       })
       ```

       Parameters explained:

       - The 'contentId' which should be identical to the Content Id by which the particular content is registered with - in your CMS. This allows us to identify each piece of unique premium content that you have.

       - The 'clientId' which is retrieved from the Client Integrations Page of the ConsCent Client Dashboard.

       - The 'title' which should be the Content Title by which the particular content is registered with in the Client CMS.

       - The 'categories' which is an optiona parameters - it must be an array of string of all the categories that you would like to be associated with the content.

       - The 'subTitle' which should be the Content Subtitle. This is a optional parameter.

       - The 'category' which should be the Content Category. This is a opitonal parameter.

       - 'successCallback' this parameter takes a function which is discussed in step 3

       - 'debug' takes 'true' or 'false' (boolean) and a false flag disables non-error conscent log output.

       - 'wrappingElementId' is a mandatory string which is the id of an element created in step one.

       - 'accentColor' sets the theme color of the paywall, it can take a css color or a css color hexcode.

       - The 'subscriptionUrl' which is the link to the Subscription page of your website - if this parameter is empty, the subscription section of the paywall does not appear.

       - You can optionally provide the 'signInUrl' which is the link to the login page for already subscribed users on the clients platform - Doing this will add a "Sign in here" text to be displayed below the "Subscribe" button.

       - 'buttonMode' can be set to 'true' or 'false' (boolean) -- if true, the paywall will appear only as a button. This may be useful for content such as videos, songs and podcasts. Moreover, the 'button' paywall can be styled from the client dashboard directly - by passing the required CSS there.

       - 'fullScreenMode' can be set to 'true' or 'false' (strings) -- if true, the first screen of the paywall will cover the entire webpage. This is useful if you don't want the premium content page to be visible at all once the user proceeds with the payment.

       - 'translucencyId' if you would like ConsCent to hide/unhide an element on your page with a translucent overlay (frontend-only). Set the id of that element as the value of translucencyId

       - 'CSCIconPosition' positions the icon to the right or to the bottom of the browser, the possible values for this variable are 'bottom' or 'right'.

       - 'CSCIconOffset's value can be any valid css value (e.g. '10px' or '50%') which will set the distance of the icon from the edge of the browser window.

       - 'hashCode' if using hashcode method of registration you need to pass your generated and signed hash in this field.

       - 'adBlockOnly' works exclusively with the hiddenElemId field, if true, the paywall will only load when the user has enabled his ad-blocker

       - 'hiddenElemId' If you want ConsCent to unhide a DOM element with display: none property on it when the user unlocks the content, you can pass the 'id' of the DOM element in this property.

       - 'defaultPhone' of the user, if available with the client, can be passed to ConsCent to be pre-filled in the required places

       - 'defaultEmail' of the user, if available with the client, can be passed to ConsCent to be pre-filled in the required places

       - 'defaultName' of the user, if available with the client, can be passed to ConsCent to be pre-filled in the required places

       - 'internalUserId' of the user, from the client CMS/Database which will be passed back in the login/signup/purchase webhooks, allowing the client to keep track of the user's activities

    3. successCallback and validation

       1. If the user has bought or has access to premium content, your successCallback will be called with payload as the first argument (shown below)

       ```
         { "message": "Content Purchased Successfully", "payload": { "clientId": "5fbb40b07dd98b0e89d90a25", "contentId": "Client Content Id 5", "createdAt": "2020-12-29T05:51:31.116Z" }, "consumptionId": "a0c433af-a413-49e1-9f40-ce1fbd63f568", "signature": "74h9xm2479m7x792nxx247998975393x08y9hubrufyfy3348oqpqqpyg78fhfurifr3", }
       ```

       2. Your successCallback function is a javascript function responsible for taking the payload, and displaying the premium content to the user. For completely secure validation, make sure your successCallback function calls a specific route on your backend meant for returning premium content that accepts the a conscent consumption id (present in the argument passed to successCallback). The validation flow will be something like this:-
          1. Frontend passes ConsCent consumption Id to your backend via an API call
          1. Backend must verify that the consumption Id is valid and is valid for the contentId requested. This validation is done by checking with ConsCent's API, as shown here: https://tsbmediaventure.github.io/developer-docs/#validate-content-consumption
          1. If the validation is successful, the backend must return the premium content -- or a way to unlock it, to your frontend website.
          1. The frontend must retrieve the content/ way to access content retrieved from backend and display the premium content to the user.

    Example successCallback for an article:

         ```


         async function yourSuccessCallbackFunction(validationObject) {
            // Function to show the premium content to the User since they have paid for it via ConsCent
            // Here you should verify the validationObject with our backend
            // And then you must provide access to the user for the complete content
            // example verification code:

            console.log('Initiating verification with backend via consumption Id');
            const xhttp = new XMLHttpRequest(); // using vanilla javascript to make a post request
            const url = `${your-backend-url}/api/get-premium-content/${validationObject.consumptionId}`;
            xhttp.open('POST', url, true);
            // e is the response event
            xhttp.onload = (e) => {
            const premiumDataFromBackend = JSON.parse(e.target.response);
                // Validation successful
                console.log('successful validation');
                // sample code that takes an HTML element and populates it with data returned from the backend call
                // this will work in case of articles
                document.getElementById('premium-content').innerHTML = premiumDataFromBackend.content;
            };
            xhttp.send();
         }


         ```
