# Pricing strategies

Prices can be set in three ways while registering content.

1. No Price overrides, only the price and the currency. (see create content api)
2. Geolocation based price overrides along with price.
3. No pricing information, only category information.

Blanket integration uses the default price which can have overrides -- which can be set from your dashboard. (Changing the price will change the price of all your contents)

### International Pricing

Every content can be priced at different prices/currencies for different countries.
The amount will be dynamically converted to the user's preferred currency.

For e.g. you can set a price of Rs.5 for India and Rs.20 for the US.
Users from the US will see the price as $0.27 (20 INR converted to USD) (based on conversion rates)
Alternatively you can set a price of Rs.5 for India and $0.15 for the US and all users from the US will see the price as $0.15. (No conversion happens)

For blanket pricing, you can set different default prices for different countries from the dashboard.
For content registration, you can set this while creating/editing contents.

### Different price in India and abroad

One common use case is to have one price (X INR) in India and  (Y INR) everywhere else in the world.

To achieve this, you will set the price as Y INR, and set the price override value of India to X INR.

### Category based pricing

When using content registration flow or hashcode flow, this