ConsCent Plugin Integration Guide
=================================

This guide provides step-by-step instructions on how to include the ConsCent Plugin in your iOS app. The ConsCent Plugin is developed in Swift and supports iOS 13.0 and above.

### Step 1: Integration Setup

#### Step 1.1: Adding the Plugin Framework
1. Drag the CCPlugin.xcframework folder into your Xcode project.
2. Select your app target and go to the "Frameworks, Libraries, and Embedded Content" section.
3. Change the embed mode for CCPlugin.xcframework to "Embed & Sign".
4. Clean and build your project to ensure the framework is properly integrated.


### Step 2: Plugin Configuration

#### Step 2.1: Importing the Framework
Import the CCPlugin framework into your ViewController class.
~~~Swift
import CCPlugin
~~~~

#### Step 2.2: Configuring the Plugin
In your ViewController class, configure the plugin by providing the client ID and the desired environment mode.
~~~Swift
CCPlugin.shared.configure(mode: .sandbox, clientID: "your-client-id")
~~~~

Parameters:
* contentID: This will be your article or content ID for which details need to be checked.
* The mode parameter specifies the environment mode to be used in your app. You can choose one of the following modes:
~~~
Mode.stage (default)
Mode.sandbox
Mode.production
~~~

#### Step 2.3: Customizing Accent Color
You can set the accent color for the paywall by accessing the accentColor property of the CCPlugin.shared instance and modifying its value.
~~~Swift
CCPlugin.shared.accentColor = UIColor.red
~~~

#### Step 2.4: Enabling Debug Mode
The debugMode property of the CCPlugin.shared instance can be set to true or false to enable or disable debug mode. When debug mode is enabled, toasts will be shown if the content ID or client ID entered is incorrect. This is useful for development purposes.
~~~Swift
CCplugin.shared.debugMode = false
CCplugin.shared.accentColor = accentColor
~~~


### Step 3: Functions
To check if an article/content is free/paid or a payment needs to be done, in your class, use as below sample:
Parameters detail can be checked below for more information.

#### Step 3.1: PayWall Screen
1. This step is for PayWall Screen
~~~Swift
CCplugin.shared.showPayWall(contentID: contentID, viewLayout: ViewLayoutInfo(vc: self, view: self.view), completiondelegate: self, subscriberDelegate: self, signInDelegate: self)
~~~

2. This step is for Subscription Screen
~~~Swift
CCplugin.shared.initSubscriptions(contentID: contentID, viewLayout: ViewLayoutInfo(vc: self, view: self.view), completiondelegate: self)
~~~

#### Parameters Details:
* contentID: This will be your article or content ID for which details need to be checked.
* ViewLayoutInfo: This is a struct that has two values, vc (View Controller) and view. Pass the view on which you are going to show your content and the View Controller in which the view is present.
* delegate: This will be used to handle the success and failure cases. Pass the class as the delegate where you want to handle success or failure. This delegate is of the protocol CCPluginCompletionHandlerDelegate, which has two methods: success and failure that will be triggered in case of success and failure of the process.
* success: This is the success callback that will be called for every successful processing. The success method will be triggered in the delegate class.
* failure: This is the failure callback that will be called for every failed processing. The failure method will be triggered in the delegate class.
* subscriberDelegate: This is an optional callback that will be called if you pass your class as its delegate. It will be triggered when the subscription button is tapped. If you don't pass it in your delegate, it will not show the subscription view.
* signInDelegate: This is an optional callback that will be called if you pass your class as its delegate. It will be triggered when the sign-in button is tapped. If you don't pass it in your delegate, it will not show the sign-in view. 


### Step 4: Final Touches
* In your Project go to your target and in the URL types add a new one with URL schemes "conscent".
* This is important to handle redirection or app launches from the browser.
* call below function inside of `openURLContexts` scene delegate.
~~~Swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    if let url = URLContexts.first?.url {
       CCplugin.shared.handleRelaunchApp(url: url)
    }
}
~~~


### Step 5: Important Points
1. Keep in mind there is only instance of the `CCPlugin`. So a new function call will override the last function call.
2. Please show or load your content only after the success callback to avoid showing paid content for free in case of server or internet issue.
3. Don't forget step 4 otherwise you will have to refresh the content screen everytime you make a payment for a paid content
4. The blocker View supports both portrait and landscape orientation
5. Make sure the height of the paywall view is more than 600 in portrait and 336 in landscape to avoid any view obstruction, alternatively if you're not passing the subscriber view you can have the paywall height of 313 in portrait, 336 in landscape
6. If you don't have a valid session ID the logIn with Conscent button will not show
7. if you have valid session you will se the user's account balance in the paywall
8. The view automatically center all of its content so it's fine if you don't want the subscription view


Please look at the Sample Project for more Details


