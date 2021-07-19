Technical Instructions for using the Android plugin

---

This is a step by step guide to include Conscent Plugin in your app. This plugin is developed in Kotlin and supports both Java and Kotlin languages.

### Step-1

Copy plugin aar file to your libs folder and add it in your app level build gradle file.
Please contact the ConsCent team if you do not have your plugin AAR file.

### Step-2

In your application build.gradle file, include dependency as below with latest versions:

- Retrofit and GSON converter
  implementation 'com.squareup.retrofit2:retrofit:(insert latest version)'
  implementation 'com.squareup.retrofit2:converter-gson:(insert latest version)'
  Example:
  implementation 'com.squareup.retrofit2:retrofit:2.9.0'
  implementation 'com.squareup.retrofit2:converter-gson:2.9.0'

- Coroutines
  implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:(insert latest version)'
  Example:
  implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.4.2'

- Browser
  implementation 'androidx.browser:browser:(insert latest version)'
  Example:
  implementation 'androidx.browser:browser:1.3.0'

Note:

1. In case of error for Kotlin not enabled, please enable Kotlin for project.
2. In case of error in Manifest merging, please merge Manifest as per Android Studio support or include line tools:replace="android:icon,android:roundIcon" inside your application tag in Android Manifest file.

## Step-3

In your application class, pass client_id, Environment Mode and app mode to be used in your app as below sample:

Conscent.configure(yourApplicationContext, "your_client_id", MODE, APP_MODE)

1. yourApplicationContext: Pass your application context here.
2. Client ID: Pass your client_id received from Conscent.
3. Mode can be set as
   ConscentConfiguration.MODE.SANDBOX
   ConscentConfiguration.MODE.PRODUCTION

Mode is used for configuration testing of different environments available.

4. APP_MODE can be set as
   ConsCentConfiguration.APP_MODE.DEBUG
   ConsCentConfiguration.APP_MODE.PROD

APP_MODE is used for checking debug and production enviroment of app where if APP_MODE is debug, then all errors will be shown as Toast messages and Logs. For PROD mode, only logs will be available for critical errors like Network unavailability, wrong client_id and wrong content_id.

## Step-4

To display the paywall for a particular content, in your class, use as checkContent function as shown in below sample:
Parameters detail can be checked below for more information.

- Kotlin

Conscent.checkContent(
"your_article/content_id",
parent,
frameLayout,
yourActivityContext,
success,
failure,
subscribe,
signIn,
colorAccent
)

OR

Conscent.checkContent(
"your_article/content_id",
parent,
frameLayout,
yourActivityContext,
conscentCallBackReference,
showSubscribe,
colorAccent
);

- Java

Conscent.Companion.checkContent(
"your_article/content_id",
parent,
frameLayout,
yourActivityContext,
success,
failure,
subscribe,
signIn,
colorAccent
);

OR

Conscent.Companion.checkContent(
"your_article/content_id",
parent,
frameLayout,
yourActivityContext,
conscentCallBackReference,
showSubscribe,
colorAccent
);

Parameters detail

- article/content id: This will be your article or content id for which detail needs to be checked.
- parent: This will be the parent of your layout. Please keep ConstraintLayout as your root view in your activity xml file. Pass the reference of your root view in checkContent function.
- frameLayout: This will be a FrameLayout where payment page will be inflated. Create a frameLayout in your xml and pass here as a reference.
  for eg:
  <FrameLayout
          android:id="@+id/frame"
          android:layout_width="match_parent"
          android:layout_height="wrap_content" />

- yourActivityContext: This is your activity content which is calling the methods and where callback will be received.
- conscentCallBackReference: You can pass a callbackReference which will get called after success or failure in processing. If you pass a callbackReference, after successfull processing, the success reference will be called and for failed event, failure event will be called. You can implement ConscentCallBack in your activity and then pass it as a reference.
- success: This is the success callback which will get called for every successfull processing. You can pass your method as a reference or an lambda expression which will get called in case of success.
- failure: This is optional. You can pass it as null. This is the failure callback which will get called for every failed processing. You can pass your method as a reference or an lambda expression and it'll get called for failed cases. You can implement your code in it for failed cases.
- subscribe: This is optional callback. If you want to inflate subscribe layout, pass a subcribe function which will be called when subscribe button will be clicked inside payment flow. Passing null will not inflate subscribe layout.
- signIn: This is the callback function which will be called when a user click on signIn button in payment flow. This will be only visible if subscribe layout has been inflated.
- colorAccent: Color object to be passed to make payment flow layout accent color match as per your color.
  Eg: Color.parseColor("#0087ca") or ContextCompat.getColor(context, color_from_colors.xml) like ContextCompat.getColor(this, R.color.red)
- showSubscribe: Type boolean, pass this as "true" to show subscribe layout else "false".

## Step-5

In you onActivityResult method, pass below line of code:
Conscent.handledIntent()

======================End======================
