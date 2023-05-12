Conscent Plugin for developers
======================

This is a step by step guide to include Conscent Plugin in your app. This plugin is developed in Kotlin and supports both Java and Kotlin languages. 

### Step-1
Copy plugin aar file to your libs folder and add it in your app level build gradle file.

### Step-2
In your application build.gradle file, include dependency as below with latest versions:

* Retrofit and GSON converter
implementation 'com.squareup.retrofit2:retrofit:(insert latest version)'
implementation 'com.squareup.retrofit2:converter-gson:(insert latest version)'
Example:
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'

* Coroutines
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:(insert latest version)'
Example:
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.4.2'

* Browser
implementation 'androidx.browser:browser:(insert latest version)'
Example:
implementation 'androidx.browser:browser:1.3.0'

Note: 
1. In case of error for Kotlin not enabled, please enable Kotlin for project.
2. In case of error in Manifest merging, please merge Manifest as per Android Studio support or include line tools:replace="android:icon,android:roundIcon" inside your application tag in Android Manifest file.

## Step-3
In your application (recommended) or root activity class's onCreate, pass applicationContext, yourClientId, accentColor, Environment Mode and App Mode to be used in your app as below sample:
ConscentWrapper.configure(yourApplicationContext, yourClientId, yourAccentColor, MODE, APP_MODE)
Remember to set configuration before you call further callbacks.

1. yourApplicationContext: Pass your application context here.
2. yourClientId: Pass your clientId received from Conscent.
3. yourAccentColor: Pass your accentColor for the app.
4. Mode can be set as 
ConscentConfiguration.MODE.STAGE
ConscentConfiguration.MODE.SANDBOX
ConscentConfiguration.MODE.PRODUCTION

Mode is used for configuration testing of different environments available.

5. APP_MODE can be set as 
ConsCentConfiguration.APP_MODE.DEBUG
ConsCentConfiguration.APP_MODE.PROD

APP_MODE is used for checking debug and production environment of app where if APP_MODE is debug, then all errors will be shown as Toast messages and Logs. For PROD mode, only logs will be available for critical errors like Network unavailability, wrong client_id and wrong content_id.

You can later change your clientId also, by calling the following function:
ConscentWrapper.changeClientId(yourClientId), throws "Configure ConscentWrapper first!" if not configured already!

## Step-4
Create an instance of the Conscent class for each unique contentId (recommended) for more control over your content flow. Use the below described method:

*Kotlin

val instance = ConscentWrapper.getConscentInstance(
        yourCallingActivity,
        yourParentView,
        yourContainerView,
        contentId,
        onConscentListener
)

*Java

Conscent instance = ConscentWrapper.Companion.getConscentInstance(
        yourCallingActivity,
        yourParentView,
        yourContainerView,
        contentId,
        onConscentListener
);

*All parameter details are given at the bottom.

## Step-5
To check if an article/content is free/paid or a payment needs to be done, in your class, use as below sample:
Parameters detail can be checked below for more information.

* Kotlin

instance.checkContentAccess(
        yourContentTitle,
        yourSubsUrl,
        canSubscribe,
        showClose
    )

* Java

instance.checkContentAccess(
        yourContentTitle,
        yourSubsUrl,
        canSubscribe,
        showClose
    );


To get all the subscription packages available, in your class, use as below sample:
Parameters detail can be checked below for more information.

* Kotlin

instance.checkSubscriptions(
        yourContentTitle,
        yourSubsUrl,
        showClose
    )

* Java

instance.checkSubscriptions(
        yourContentTitle,
        yourSubsUrl,
        showClose
   );


Parameters detail
* yourCallingActivity (Activity): This is your activity content which is calling the methods and where callback will be received.
* yourParentView (ConstraintLayout): This will be the parent of your layout. Please keep ConstraintLayout as your root view in your activity xml file. Pass the reference of your root view in checkContent function.
* yourContainerView (FrameLayout): This will be a FrameLayout where payment page will be inflated. Create a frameLayout in your xml and pass here as a reference. 
for eg: 
<FrameLayout
        android:id="@+id/frame"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
  Eg: Color.parseColor("#0087ca") or ContextCompat.getColor(context, color_from_colors.xml) like ContextCompat.getColor(this, R.color.red)
* contentTd (String): This will be your article or content id for which detail needs to be checked.
* onConscentListener (OnConscentListener): You can pass a listener which will get called after success or failure in processing. If you pass a listener, after successful processing, the success reference will be called and for failed event, failure event will be called. You can implement OnConscentListener in your activity and then pass it as a reference.
  * onSuccess: This is the success callback which will get called for every successful processing. You can pass your method as a reference or an lambda expression which will get called in case of success.
  * onError: This is optional. You can pass it as null. This is the failure callback which will get called for every failed processing. You can pass your method as a reference or an lambda expression and it'll get called for failed cases. You can implement your code in it for failed cases.
  * onSubscribe: This is optional callback. If you want to inflate subscribe layout, pass a subscribe function which will be called when subscribe button will be clicked inside payment flow. Passing null will not inflate subscribe layout.
  * onBuyPass: This is optional callback. It will be called when buy-pass button will be clicked inside payment flow.
  * onSignIn: This is the callback function which will be called when a user click on signIn button in payment flow. This will be only visible if subscribe layout has been inflated.
  * onAdFree: This is the callback function which will be called when a user click on adfree subscription.
* yourContentTitle (String - Optional): Type string, title of the content for display purposes.
* yourSubsUrl (String - Optional): Type string, url to be used when subscribe button is clicked.
* canSubscribe (Boolean - Optional): Type boolean, pass this as "true" to show subscribe layout else "false".
* showClose (Boolean - Optional): Type boolean, pass this as "true" to show close button on the paywall/subscriptions, default is "false".

## Step-6
In you onActivityResult method, pass below line of code:
instance.handledIntent()


To get logged in user details

* Kotlin

ConscentWrapper.INSTANCE?.getUserDetails()
  
* Java

ConscentWrapper.Companion.getUserDetails();


To get subscription details

* Kotlin

ConscentWrapper.INSTANCE?.getSubscriptionDetails()

* Java

ConscentWrapper.Companion.INSTANCE?.getSubscriptionDetails();


To get pass details

* Kotlin

ConscentWrapper.INSTANCE?.getPassDetails()

* Java

ConscentWrapper.Companion.INSTANCE?.getPassDetails();


To logout the user

* Kotlin

ConscentWrapper.INSTANCE?.logoutUser()

* Java

ConscentWrapper.Companion.INSTANCE?.logoutUser();

======================End======================
