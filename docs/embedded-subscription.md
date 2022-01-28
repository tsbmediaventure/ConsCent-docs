## Embedded Subscriptions Integration

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

    Please replace {replace_with_clientId} with your client id (found in the integration section of your ConsCent client dashboard) and {replace_with_sdk_url} with the corresponding sdk_url as mentioned in [the urls section](Readme.md#URLs)

2.  On the page where you would like to display the Subscriptions widget-

    1. Create a blank div element, position it where you want the conscent paywall to render and give it an id attribute. This element must have space of a minimum width of 320 pixels and a minimum height of 550 pixels for the subscriptions' details to fit properly.

    2. Initialize the paywall with the following code:

       ```
       const csc = window._csc;
       csc('subs', {
         contentId: {contentId},
         clientId: {clientId},
         title: {contentTitle},
         url: {urlOfThePremiumContent},
         successCallback: yourSuccessCallbackFunction,
         debug: true,
         wrappingElementId: 'csc-paywall',
         // Following fields are optional
         contentUrl: {contentUrl},
         defaultPhone: '9898989898',
         defaultEmail: 'test@email.com',
         internalUserId: '10000000000'
       })
       ```

    Parameters explained:

    - The 'contentId' which can be the ID of the content that led the user to purchase a subscription on your platform

    - The 'clientId' which is retrieved from the Client Integrations Page of the ConsCent Client Dashboard.

    - The 'title' which should be the Content Title by which the particular content is registered with in the Client CMS.

    - The 'contentUrl' which should be the URL of the particular content that led the user to purchase a subscription - where the user will be redirected to on a successfull purchase

    - 'successCallback' this parameter takes a function which is discussed in step 3

    - 'debug' takes 'true' or 'false' (boolean) and a false flag disables non-error conscent log output.

    - 'wrappingElementId' is a mandatory string which is the id of an element created in step one.

    - 'defaultPhone' of the user, if available with the client, can be passed to ConsCent to be pre-filled in the required places

    - 'defaultEmail' of the user, if available with the client, can be passed to ConsCent to be pre-filled in the required places

     - 'internalUserId' of the user, from the client CMS/Database which will be passed back in the login/signup/purchase webhooks, allowing the client to keep track of the user's activities

    3. successCallback and validation

    1. If the user has bought or has access to the clients platform via subscriptions, your successCallback will be called with payload as the first argument (shown below)

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

    ```

    ```
