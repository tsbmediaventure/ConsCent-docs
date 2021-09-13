## Working with infinite scrolling

If you have multiple premium content on the same page and want to put them all behind a paywall, follow the following steps.

1. When the first premium content comes into focus, initialize the paywall via the init method outlined in [integrations](integration.md#Concepts)
2. When a new premium content comes into focus, first de-initalize the paywall by running `window._csc('remove') `and then re-initalize it with the new details.