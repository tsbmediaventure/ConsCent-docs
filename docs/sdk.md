## Functions

### Get User Details from SDK

    Get ConsCent user details by initialising the CSC 'user-details' function and passing a callback function in the arguments where the user details will be passed by ConsCent:

       ```
       const csc = window._csc;
       csc('user-details', {
         userDetailsCallback: yourUserDetailsCallbackFunction,
       })
       ```

       Parameters explained:

       - 'userDetailsCallback' this parameter takes a function which received the ConsCent user details as an input arguments. The argument contains a field called 'userDetailsMatch' which is set to true if the user details (user name - phone number or email of the user) match the default details passed by the client whilst initalising the CSC paywall.

    Example userDetailsCallback argument for Logged In User:

        {
            "address": {
                "apartment": "",
                "area": "",
                "pincode": "",
                "landmark": "",
                "city": "",
                "state": "",
                "country": ""
            },
            "wallet": {
                "balance": {
                    "$numberDecimal": "200.00"
                },
                "currency": "INR"
            },
            "name": "",
            "_id": "61b9cefbf5d1f54797aaf149",
            "phoneNumber": "8945793793",
            "country": "IN",
            "promotionalOptIn": true,
            "lastPurchasedOn": "2021-12-15T11:19:30.942Z"
            "userDetailsMatch": true
        }

    Example userDetailsCallback argument for Logged In User:

        {
            "message": "User not logged in",
            "userDetailsMatch": false
        }