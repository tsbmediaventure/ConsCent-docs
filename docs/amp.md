## Integration on AMP Pages

Since custom javascript isn't allowed on AMP Pages, and you cannot directly include the web-sdk on AMP pages, there is a slightly different integration process for AMP Pages.
This involves adding a few tags to your AMP pages based on your method of integration.

_AMP integration works with subscription and passes also now_

### AMP Integration methods

1. Tag based
2. Dynamic

Both methods are very similar except the dynamic method requires you to register your premium content with ConsCent (content-registration method) and only works with text content. The trade-off in tag based integration is that the content is present in the DOM, only invisible. This might be a plus point if you are worried about losing out on SEO when the content is completely not present.

### How to Integrate

**Please check the [amp-example.html](./amp/amp-example.html) and [amp-example-dynamic.html](./amp/amp-example-dynamic.html) to view full html pages**

0. **(Dynamic mode only)** When registering content on ConsCent via API calls, include the premium html of your content in the 'ampContent' field.

1. Include the amp access tag in your AMP page. Information about the urls and query params is given after the code block

```
    <script id="amp-access" type="application/json">
      {
        "authorization": "{API_URL}/api/v1/content/amp?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)&title=QUERY_PARAM(title)&subTitle=QUERY_PARAM(clientId)&url=QUERY_PARAM(URL)",
        "login": "{FRONTEND_URL}/overlay?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)&returnUrl=RETURN_URL",
        "login": {
          "micropricing": "{FRONTEND_URL}/overlay?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)returnUrl=RETURN_URL",
          "pass": "{FRONTEND_URL}/overlay?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)&returnUrl=RETURN_URL&purchaseMode=PASS",
          "subscription": "{SUBS_URL}?rid=READER_ID&_=RANDOM&clientContentId=QUERY_PARAM(clientContentId)&clientId=QUERY_PARAM(clientId)"
        },
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

Please get the value for API_URL, SUBS_URL and FRONTEND_URL from the urls section of the Readme. ClientId is your unique clientId available on your dashboard and clientContentId is Id of the content you have registered on ConsCent.
- QUERY_PARAM(clientContentId) should be replaced with your unique content's id
- QUERY_PARAM(clientId) should be replaced with your clientId
- QUERY_PARAM(title) should be replaced with the title of the content
- QUERY_PARAM(url) should be replaced with the url of the non-amp content page of the current content
- QUERY_PARAM(subTitle) is optional, and should be replaced with your content's subtitle or  removed from the url

2. Add a paywall for users who do not have access

````
    
    <div amp-access="NOT granted" amp-access-hide>
      <template amp-access-template type="amp-mustache">
        <div class="csc-wrapper">
          <div class='csc-container'>
            <div class='csc-header-main'>
              Now pay only for what you want!
            </div>
            <div class="wrap-top-bottom-container">
              <div class='csc-content'>
                {{#micropricingExists}}
                <div class='csc-left-col'>
                  <div class='csc-heading-wrap'>
                    <div class='csc-small-sub-heading'>
                      This is a Premium Story
                    </div>
                    <div class='csc-heading'>
                      Pay {{contentPrice}} to Read now
                    </div>
                    <div>
                      {{#userBalance}}
                      <div class='csc-balance'>ConsCent Balance: {{userBalance}}</div>
                      {{/userBalance}}
                      {{^userBalance}}
                      <div class='csc-balance'></div>
                      {{/userBalance}}
                    </div>
                  </div>
                  <div style='display: flex ;justify-content:center'>
                    <button class="csc-button" on="tap:amp-access.login-micropricing">Read Now </button>
                  </div>
                  <span class='csc-powered-by'>
                    Pay with
                    <amp-img src='https://conscent-static-assets.s3.ap-south-1.amazonaws.com/conscentLogoMono.png'
                      height="10" width="63.33" />
                  </span>
                  <div style="margin-top: 16px;">
                    Once paid, this story is free for {{duration}} days
                  </div>
                </div>

                {{#passExists}}
                <div class='csc-middle-col'>
                  <div class='csc-vertical-line'>
                    <div class='csc-or-write'>OR</div>
                  </div>
                </div>
                {{/passExists}}
                {{/micropricingExists}}
                {{#passExists}}
                <div class='csc-right-col'>
                  <div class="csc-subscribe-title-container">
                    <div class="csc-subscribe-title" style="font-size: 23px;">
                      {{passDuration}}-hr unlimited access to premium content for {{passPrice}}
                    </div>
                  </div>

                  <div style='display: flex ;justify-content:center'>
                    <button class="csc-button" on="tap:amp-access.login-pass" style="margin-top: 0px;">Buy Pass</button>
                  </div>

                  {{^micropricingExists}}
                  {{^subscriptionExists}}
                  <span class='csc-powered-by'>
                    Pay with
                    <amp-img src='https://conscent-static-assets.s3.ap-south-1.amazonaws.com/conscentLogoMono.png'
                      height="10" width="63.33" />
                  </span>
                  {{/subscriptionExists}}
                  {{/micropricingExists}}
                </div>
                {{/passExists}}
              </div>
              {{#subscriptionExists}}
              <div class="csc-bottom-container">
                <div>
                  <div class="csc-subscribe-title-container">
                    <div class="csc-subscribe-title">
                      For unlimited access to all the articles
                    </div>
                  </div>

                  <div style='display: flex ;justify-content:center'>
                    <button class="csc-subscribe-button">Subscribe Now </button>
                  </div>
                  {{^micropricingExists}}
                  {{^passExists}}
                  <span class='csc-powered-by'>
                    Pay with
                    <amp-img src='https://conscent-static-assets.s3.ap-south-1.amazonaws.com/conscentLogoMono.png'
                      height="10" width="63.33" />
                  </span>
                  {{/passExists}}
                  {{/micropricingExists}}
                </div>
              </div>
              {{/subscriptionExists}}
            </div>
          </div>
        </div>
      </template>
    </div>
````

Please note that  if you do not use ConsCent's subscription, and have your own system, you can modify the on-click tap of the amp button manually after removing the templating condition.
**You must also include CSS for the above ConsCent paywall on your amp page.** Include the following CSS block in a separate index.css file and make sure you include it in your main page, or add the styles in your main page.

```
      
    .csc-wrapper {
      width: 750px;
      margin: auto;
    }
    
    .csc-container {
      font-family: Lato;
      font-weight: normal;
      color: #222;
      background-color: #fff;
      border-radius: 10px;
      box-shadow: rgba(50, 50, 93, 0.25) 0 2px 5px -1px, rgba(0, 0, 0, 0.3) 0 1px 3px -1px;
      margin: 0 2px -2px 2px;
    }
    
    .csc-header-main {
      width: 100%;
      height: 42px;
      border-top-left-radius: 10px;
      border-top-right-radius: 10px;
      background-color: rgb(204, 51, 51);
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 18px;
    }
    
    .csc-content {
      display: flex;
      justify-content: center;
      text-align: center;
    }
    
    .csc-left-col {
      width: 50%;
      padding-top: 16px;
      padding-bottom: 16px;
    }
    
    .csc-heading-wrap {
      line-height: 1.4;
    }
    
    .csc-button {
      margin-top: 24px;
      margin-bottom: 5px;
      letter-spacing: 1px;
      background-color: #3c465c;
      border-radius: 14px;
      width: 264px;
      height: 50px;
      padding: 0;
      font-family: Roboto, sans-serif;
      font-weight: 500;
      font-size: 20px;
      color: #fff;
      border: none;
      cursor: pointer;
    }
    
    .csc-subscribe-button {
      background-color: transparent;
      color: rgb(204, 51, 51);
      letter-spacing: 1px;
      margin-bottom: 32px;
      border: 1px solid rgb(204, 51, 51);
      border-radius: 14px;
      width: 264px;
      height: 50px;
      padding: 0;
      font-family: Roboto, sans-serif;
      font-weight: 500;
      font-size: 20px;
    }
    
    .csc-subscribe-title {
      font-size: 18px;
      margin: auto;
      word-break: break-word;
      line-height: 1.3;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    
    .csc-subscribe-title-container {
      margin-bottom: 24px;
      margin-top: 36px;
    }
    
    .csc-powered-by {
      margin-bottom: 16px;
      font-size: 12px;
      opacity: .8;
    }
    
    .csc-already-container {
      margin-top: 16px;
    }
    
    .csc-conscent-login-write {
      color: rgb(60, 70, 92);
      cursor: pointer;
      font-size: 16px;
      color: rgb(204, 51, 51);
    }
    
    .csc-right-col {
      width: 50%;
      padding-top: 16px;
      padding-bottom: 16px;
      padding-left: 30px;
    }
    
    .csc-middle-col {
      display: contents;
    }
    
    .csc-heading {
      font-size: 26px;
      font-weight: 600;
    }
    
    .csc-small-sub-heading {
      font-size: 16px;
      line-height: 1.5;
    }
    
    .csc-sub-heading {
      font-size: 18px;
    }
    
   .wrap-top-bottom-container{
      padding: 24px;
    }
    .csc-vertical-line {
      border-right: 1px dashed lightgrey;
      display: flex;
      align-items: center;
      justify-content: center;
    }


    .csc-bottom-container {
      border: 1px dashed lightgrey;
      margin-top: 16px;
    }

    .csc-or-write {
      background-color: #fff;
      width: 20px;
      height: 25px;
      position: relative;
      left: 10px;
      font-size: 16px;
      font-weight: 600;
      top: 5px;
    }
    .csc-balance {
      color: #222;
      opacity: 0.6;
    }
    
    @media (max-width: 678px) {
      .csc-wrapper {
        width: 100%;
      }
      .csc-content {
        display: block;
      }
      .csc-header-main {
        font-size: 16px;
      }
      .csc-left-col {
        width: 100%;
        padding-top: 10px;
        padding-bottom: 0;
      }
      .csc-right-col {
        width: 100%;
        padding-top: 16px;
        padding: 0;
      }
      .csc-heading {
        font-size: 26px;
      }
      .csc-small-sub-heading {
        font-size: 16px;
      }
      .csc-vertical-line {
        border-right: none;
        border-bottom: 1px dashed lightgrey;
      }
      .csc-or-write {
        width: 50px;
        left: 0;
        top: 16px;
      }
      .csc-subscribe-already-container {
        margin-bottom: 32px;
      }
      .csc-subscribe-title-container {
        margin-top: 16px;
      }
      .csc-subscribe-title {
        padding-top: 24px;
      }
    }
```


Sample code for including a index.css file - 

```
  <style amp-custom>
    @import url('index.css');
  </style>
```



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
