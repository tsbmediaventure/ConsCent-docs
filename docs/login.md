# Login

Integrating ConsCent on your Website is a simple and direct process. The following steps explain how to create credentials for your project. Your applications can then use the credentials to access APIs that you have enabled for that project. You start by copying the code on the right hand side within the script tags - and adding it to the header section of your Route Index file.
You can get your ConsCent Client Id from the Client Integration Page ​​of the ConsCent Client Dashboard - as mentioned in the Registration Section.
Including this regular script in the header section allows the ConsCent Login to be initalised and further used whenever user requires to login.
Finally, In order to ensure that the ConsCent Login appears on your site. You need to implement the 'csc_init' function on the content page - included on the right hand side of the ConsCent Login and enables a user to login through ConsCent on your website. Please ensure that you call this function anytime you want the ConsCent Login to show up on your content page.
We import the initalisation script using the unique '_csc' identifier and run the 'csc_init' function by passing a number of parameters.

##   Add this code to the head section of your website

### Login script :

This script can be called anywhere as you already have the SDK script to your header section. 

``````jsx
const csc = window._csc as any;
    csc('conscent-login', {
      debug: true,
      clientId: clientId,
      defaultEmail: defaultEmail || '',
      defaultName: defaultName || '',
      defaultPhone: defaultPhone || '',
      wrappingElementId: 'embed',
      successCallback: async (userDetailsObject: any) => {
        console.log('Success callback received from conscent login', userDetailsObject);
        setUserDetails(userDetailsObject);
        props.setShowLoginModal(false)
      },
      onCrossBtnClickSuccess: async () => {
        console.log('cross btn click successfully');
        props.setShowLoginModal(false)
      },
      unauthorizedCallback: () => {
        console.log('unauthorized callback called');
      },
    });
    
``````

### Logout Script :

``````jsx
//call this method on login button click
const callLogoutBtn = () => {
    const csc = window._csc as any;
    csc('logout', {
      debug: true,
      clientId: clientId,
      wrappingElementId: 'logout',
      logoutCallback: async () => {
        console.log('yyy');
      },
      unauthorizedCallback: () => {
        console.log('unauthorized callback called');
      },
    });
  };

```
