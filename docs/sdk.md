## Functions

### Get User Details from SDK

Get ConsCent user details by initialising the CSC 'user-details' function and passing a callback function in the arguments where the user details will be passed by ConsCent:

   ```
   const csc = window._csc;
   csc('user-details', {
     userDetailsCallback: yourUserDetailsCallbackFunction,
   })
   ```

example invokation: 
`window._csc('user-details', { userDetailsCallback: (e) => console.log(e)})`

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
        "userDetailsMatch": true,
        "loggedIn": true,
        "hashedEmail": "43983m220m7249y29yr2803y107924mx42r7x2rm80x4xm84mx7m27240m5742x2x924",
        "hashedPhoneNumber": "mx8x024mr4x03mxyx4802242mx04x7x42x724x024x84x84x",
        "previousSubscriber": true,
        "existingSubscriber": false
    }

Example userDetailsCallback argument for Not Logged In User:

    {
        "loggedIn": false,
        "userDetailsMatch": false
    }


### Log User out of ConsCent

Log the user out by calling the CSC 'logout' function and passing a callback function in the arguments where the logout result be passed by ConsCent:

   ```
   const csc = window._csc;
   csc('logout', {
     logoutCallback: yourUserDetailsCallbackFunction,
   })
   ```

example invokation: 
`window._csc('user-details', { logoutCallback: (e) => console.log(e)})`

Possible Responses:

Failure Case:
{ error: 'user-not-logged-in' }

Success Case:
{ message: 'Successfully logged out of all devices' }
