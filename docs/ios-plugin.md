# csc-ios-plugin

Conscent Plugin for developers
This is a step by step guide to include Conscent Plugin in your app. This plugin is developed in Swift and supports IOS 13.0 and above.

# Conscent Plugin

This is a step-by-step guide to include Conscent Plugin in your app. This plugin is developed in Swift and supports IOS 13.0 and above.

### Files Information:

- CCPluginStatusVC.swift
  This file contains the paywall View controller and its methods

\*CCPlugin.swift
This file contains the total flow and all the functionality of the framework

\*Constants.swift
This file is storing and managing the login challenge and session in user's device

- Model.swift
  This File contains all data classes used inside app i.e. used in API calling request, response handling and internal to plug-in functionality.

- Helper.swift
  This file is contains all the Helper methods such as fixing the view controller in view , rendering the dashed line and some other functionality that helps at various places at code.

CCPluginStoryboard.storyboard
This file contains the view file for paywall

NetworkProperties.swift
This file contains all information for all APIs end-point, API method used and parameters to be passed.

NetworkClient.swift
This file manages all the networking in the framework

CommonClass.swift
This file has methods to check internet connection and some other network helper functions

## Internal functions

handleFreeConsumption
This is the function used to check if content is free or not

handleContentID
This is the funcion used to get details about the content like it's price etc.

openBrowser
This is the function used to redirect the user to browser to make the payment

handleRelaunchApp
This is the function to handle the relaunch of the app when it's redirected from the browser

handlePostLoginChallenge
This is the function for creating login challenge.

handleLoginChallenge
This is the function for checking user's login challenge.

handleSessionID
This function is used for checking user's session for a particular content.

showPayWall
This function is the second public function and starts the flow of checking the content and displaying the paywall and also stores various properties supplied by the user

Images.bundle
This file contains all the images used at various places in the framework

configure.swift
This function sets the client id and environment and is the first public function that the user will call

======================End======================

<h1>How to use the plugin folder in ./plugins/CCPlugin.xcframework.zip</h1>

Step-1 Setup-1

1.Drag the xcframework folder in the your projects under framework and add it to your project. 2.Select your target and go into Frameworks,Libraries and Embedded Content section ,and in CCPlugin.xcframework change embed mode to embed and sign 3.First Clean and then Build your project.


Step-2 Setup-2

First Import the Framework CCPlugin
In your View Controller class, pass client_id and Environment Mode to be used in your app as below sample: CCplugin.shared.configure(mode: .stage, clientID: clientID)
Mode can be set as CCplugin.shared.mode.stage CCplugin.shared.mode.sandbox CCplugin.shared.mode.production by Default the Mode is stage
You can pass the accent color by using CCplugin.shared.accent color and modify the accent color in the paywall
There is a also a property named debug mode CCplugin.shared.debugMode which can be set true or false to show toasts if the contentID or clientID entered is wrong it is only for development purposes

Step-3 Functions

To check if an article/content is free/paid or a payment needs to be done, in your class, use as below sample: Parameters detail can be checked below for more information.

CCplugin.shared.showPayWall(contentID: contentID!, viewLayout: ViewLayoutInfo(vc: self, view: webView), delegate: self,,subscriberDelegate:CCPluginSubscribeBtnTapDelegate? = nil,signInDelegate:CCPluginSignBtnTapDelegate? = nil)

Parameters detail:- *contentID: This will be your article or content id for which detail needs to be checked.

ViewLayoutInfo : This is a struct which has 2 values VC and view , pass the view on which you are going to show your content and VC(View controller) in which the view is present *delegate: This will be used handle the success and failure cases , pass the class as the delegate where you want to handle success or Failure ,this delegate is of the protocol CCPluginCompletionHandlerDelegate which has 2 methods success and failure which will be triggered in case of success and failure of the process
success: This is the success callback which will get called for every successful processing.The method success will be triggered in this case in your delegate class
failure: This is the failure callback which will get called for every failed processing. The method failure will be triggered in this case in the your delegate class *subscriberDelegate This is a optional callback which will be called if you pass your class as its delegate ,It will be triggred When the subscription button is taped but if you don't pass in your delegate it will not show the subscription view *signInDelegate This is a optional callback which will be called if you pass your class as its delegate ,It will be triggered When the sign in button is taped , but if you don't pass in your delegate it will not show the Sign-in view

Step-4 Final Touches

In your Project go to your target and in the URL types add a new one with URL schemes "conscent" This is important to handle redirection or app launches from the browser Then in the Scene delegate add the function func scene(_ scene: UIScene, openURLContexts URLContexts: Set) add call this function CCplugin.shared.handleRelaunchApp(url: url)

Step-5 Important Points

Keep in mind there is only instance of the CCPlugin so a new function call will override the last function call
Please show or load your content only after the success callback to avoid showing paid content for free in case of server or internet issue
Don't forget step 4 otherwise you will have to refresh the content screen everytime you make a payment for a paid content
The blocker View supports both portrait and landscape orientation
Make sure the height of the paywall view is more than 600 in portrait and 336 in landscape to avoid any view obstruction , alternatively if you're not passing the subscriber view you can have the paywall height of 313 in portrait , 336 in landscape
If you don't have a valid session ID the logIn with Conscent button will not show
if you have valid session you will se the user's account balance in the paywall
The view automatically centers all of its content so it's fine if you don't want the subscription view
Please look at the Sample Project for more Details

======================End======================
