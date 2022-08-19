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
In your activity class's onCreate, pass yourClientId, Environment Mode and app mode to be used in your app as below sample:
Conscent.configure(yourApplicationContext, "yourClientId", MODE, APP_MODE)
Remember to set configuration before you call further callbacks.

1. yourApplicationContext: Pass your application context here.
2. yourClientId: Pass your clientId received from Conscent.
3. Mode can be set as 
ConscentConfiguration.MODE.STAGE
ConscentConfiguration.MODE.SANDBOX
ConscentConfiguration.MODE.PRODUCTION

Mode is used for configuration testing of different environments available.

4. APP_MODE can be set as 
ConsCentConfiguration.APP_MODE.DEBUG
ConsCentConfiguration.APP_MODE.PROD

APP_MODE is used for checking debug and production environment of app where if APP_MODE is debug, then all errors will be shown as Toast messages and Logs. For PROD mode, only logs will be available for critical errors like Network unavailability, wrong client_id and wrong content_id.

## Step-4
To check if an article/content is free/paid or a payment needs to be done, in your class, use as below sample:
Parameters detail can be checked below for more information.

* Kotlin

Conscent.checkContentAccess(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        successCallback,
        errorCallback,
        subscribeCallback,
        buyPassCallback,
        signInCallback,
        contentTitle,
        subscriptionUrl,
        canSubscribe,
        showClose
    )

OR

Conscent.checkContentAccess(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        onConscentListener,
        contentTitle,
        subscriptionUrl,
        canSubscribe,
        showClose
    )


* Java

Conscent.Companion.checkContentAccess(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        successCallback,
        errorCallback,
        subscribeCallback,
        buyPassCallback,
        signInCallback,
        contentTitle,
        subscriptionUrl,
        canSubscribe,
        showClose
    );

OR

Conscent.Companion.checkContentAccess(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        onConscentListener,
        contentTitle,
        subscriptionUrl,
        canSubscribe,
        showClose
    );


To get all the subscription packages available, in your class, use as below sample:
Parameters detail can be checked below for more information.

* Kotlin

Conscent.checkSubscriptions(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        successCallback,
        errorCallback,
        subscribeCallback,
        signInCallback,
        showClose
    )

OR

Conscent.checkSubscriptions(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        onConscentListener,,
        showClose
    )


* Java

Conscent.Companion.checkContentAccess(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        successCallback,
        errorCallback,
        subscribeCallback,
        signInCallback,
        showClose
   );

OR

Conscent.Companion.checkContentAccess(
        yourActivityContext,
        parent,
        frameLayout,
        colorAccent,
        contentId,
        onConscentListener,
        showClose
    );


Parameters detail
* yourActivityContext: This is your activity content which is calling the methods and where callback will be received.
* parent: This will be the parent of your layout. Please keep ConstraintLayout as your root view in your activity xml file. Pass the reference of your root view in checkContent function.
* frameLayout: This will be a FrameLayout where payment page will be inflated. Create a frameLayout in your xml and pass here as a reference. 
for eg: 
<FrameLayout
        android:id="@+id/frame"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
* colorAccent: Color object to be passed to make payment flow layout accent color match as per your color.
  Eg: Color.parseColor("#0087ca") or ContextCompat.getColor(context, color_from_colors.xml) like ContextCompat.getColor(this, R.color.red)
* article/content id: This will be your article or content id for which detail needs to be checked.
* onConscentListener: You can pass a listener which will get called after success or failure in processing. If you pass a listener, after successful processing, the success reference will be called and for failed event, failure event will be called. You can implement OnConscentListener in your activity and then pass it as a reference.
* successCallback: This is the success callback which will get called for every successful processing. You can pass your method as a reference or an lambda expression which will get called in case of success.
* errorCallback: This is optional. You can pass it as null. This is the failure callback which will get called for every failed processing. You can pass your method as a reference or an lambda expression and it'll get called for failed cases. You can implement your code in it for failed cases.
* subscribeCallback: This is optional callback. If you want to inflate subscribe layout, pass a subscribe function which will be called when subscribe button will be clicked inside payment flow. Passing null will not inflate subscribe layout.
* buyPassCallback: This is optional callback. It will be called when buy-pass button will be clicked inside payment flow.
* signInCallback: This is the callback function which will be called when a user click on signIn button in payment flow. This will be only visible if subscribe layout has been inflated.
* contentTitle: Type string, title of the content for display purposes.
* subscriptionUrl: Type string, url to be used when subscribe button is clicked.
* canSubscribe: Type boolean, pass this as "true" to show subscribe layout else "false".
* showClose: Type boolean, pass this as "true" to show close button on the paywall/subscriptions, default is "false".

## Step-5
In you onActivityResult method, pass below line of code:
Conscent.handledIntent()

## Note:
In production mode, please enable the synchronized lock put in Conscent.configure() function to achieve one-time setup


To get logged in user details

* Kotlin
  
Conscent.getUserDetails()
  
* Java

Conscent.Companion.getUserDetails();


To get subscription details

* Kotlin

Conscent.getSubscriptionDetails()

* Java

Conscent.Companion.getSubscriptionDetails();


To get pass details

* Kotlin

Conscent.getPassDetails()

* Java

Conscent.Companion.getPassDetails();


To logout the user

* Kotlin

Conscent.logoutUser()

* Java

Conscent.Companion.logoutUser();

======================End======================