

Auto Login functionality

Defination: Auto login is a functionalty in conscent system in which client can get his user loggedin in conscent system. After that client can have all the functionality for the user. That are provided by conscent.

Now how does it work,
 client Need to get a user loggedin in there system. After user is loggedin in the client system. Client needs to follow these steps.

 1: client need to take a token which will be provided by conscent's backend that is called "tempAuthToken";
  To get tempAuthToken 
  Hit this URL
  URL : {API_URL}/client/purchases/subscriptions

  Method : GET

  Auth required : YES

  Please pass your api key as username and api secret as password as basic auth to access the endpoint

In Body you need to pass either email or phoneNumber 
example:        {
                    "phoneNumber": "9859099340",
                    "email": ""
                }

Success Response
Code : 200 OK

{
    "tempAuthToken": "644a2c13ce90df4882d1787a"
}


Now client has recieved the token now to get the user logged in the conscent System.

client needs to call this function 
  csc('auto-login', {
      clientId: clientId,
      token: tokenEntered,
      phone: data?.phoneNumber,
      email: data?.email,
      successCallbackFunction: async (userDetailsObject: any) => {
        setShowLoginDetails(true);
        console.log('Success callback received from conscent auto Login', userDetailsObject);
        alert('login successfull');
      },
      errorCallbackFunction: (errorObject: any) => {
        console.error(errorObject);
        alert('login unsuccessfull');
      },
      unauthorizedCallback: () => {
        console.log('unauthorized callback called');
      },
    });

 

