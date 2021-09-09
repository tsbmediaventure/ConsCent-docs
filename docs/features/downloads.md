## Enabling PDF downloads

If you want to gate pdf downloads via micro-pricing, please follow the content-registration method.

Follow the content creation steps (API call) as outlined there and include the following download parameter

- download is an object containing the following fields
  - url: This is the url containing the static pdf file. If the request fails, make sure the url doesn't use redirects.
  - fileType: this must be set to 'PDF'
  - fileName: This is the name of the file that the user will download

Once the content has been registered, you can faciliate priced downloads by redirecting or linking users to this url:->

For Sandbox: https://user.conscent.in/overlay?clientId={your-client-id}&clientContentId={your-content-id}&download=true

For Production: https://sandbox-user.conscent.in/overlay?clientId={your-client-id}&clientContentId={your-content-id}&download=true

Please replace {your-client-id} with your client id and {your-content-id} with the contentId of the content you registered.

**At the moment only pdf downloads are supported, if you required any other file type please contact us**
