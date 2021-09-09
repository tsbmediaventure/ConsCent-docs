## Content bundles

If you want to sell different pieces of micro-priced premium content in a bundled

1. Create a content bundle with contentids of all stories you want to bundle together. You will assign this contentBundle a unique contentBundleId. You will also include other params like price, url, etc.
   (all parameters and exact API details are available in the API documentation website)
   https://tsbmediaventure.github.io/developer-docs/#client-content-bundles

2. When initializing the paywall on your webpage [as outlined here](../integration.md#Concepts), instead of contentId, pass the contentBundleId of the bundle you created.
