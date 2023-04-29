# Deep link for flutter

A deep link is a URL that navigates to a specific destination in your mobile app. 
Think of deep links like a URL address you enter into a web browser to go to a 
specific page of a website rather than the home page.
Deep links help with user engagement and business marketing. For example, if 
you’re running a sale, you can direct the user to a specific product page in your app 
instead of making them search for it

## Types of Deep Links
There are three types of deep links:
• URI schemes: An app’s own URI scheme. fooderlich://raywenderlich.com/home
is an example of Fooderlich’s URI scheme. This form of deep link only works if the 
user has installed your app.
• iOS Universal Links: In the root of your web domain, you place a file that points 
to a specific app ID to say whether to open your app or to direct the user to the 
App Store. You must register that specific app ID with Apple to handle links from 
that domain.
• Android App Links: Like iOS Universal Links for the Android platform, Android 
App Links take users to a link’s specific content directly in your app. They leverage 
HTTP URLs and are associated with a website. For users that don’t have your app 
installed, these links go directly to the content of your website.

## Overview of Fooderlich’s Paths
Fooderlich has many screens you can deep link to.
### Path: /
The app initializes and checks the app cache to see if the user is logged in and has 
completed the onboarding guide.
• /login: Redirects to the Login screen if the user isn’t logged in yet.
• /onboarding: Redirects to the Onboarding screen if the user hasn’t completed the 
onboarding
![image](https://user-images.githubusercontent.com/20933055/235304669-9e17cc7f-5ab7-4365-9b04-0d0d60ad3d82.png)
 
 ### Path: /:tab
 Once the user logs in and completes onboarding, they’re redirected to /:tab. It 
contains one parameter, tab, which directs to a tab index. The screenshots below 
show that the tab index is 0, 1 or 2, respectively.
![image](https://user-images.githubusercontent.com/20933055/235304688-38f68d3a-6b2f-43b1-994d-1798a988fa0f.png)

### Path: /:tab/profile
The profile route is actually a sub route of home. From the home screen, the user can 
open their user profile from each of the three tabs.
![image](https://user-images.githubusercontent.com/20933055/235304708-b0e33eac-1a8a-4a20-8535-b729268ae316.png)


## How to use?
When you deep link on mobile, you’ll use the following URI scheme:
fooderlich://raywenderlich.com/<path>
On the web, the URI scheme is like any web browser URL:
http://localhost:60738/#/<path>

##  Router API
![image](https://user-images.githubusercontent.com/20933055/235304744-f47c8ea9-6a6a-4325-867a-6d240f6cb94a.png)

Router is a widget that extends RouterDelegate. The router ensures that the 
messages pass to RouterDelegate.
• Navigator defines a stack of MaterialPages in a declarative way. It also handles 
any onPopPage() events.
• BackButtonDispatcher handles platform-specific system back button presses. It 
listens to requests by the OS and tells the router delegate to pop a route.

Next we’ll look at RouteInformationProvider and RouteInformationParser:
![image](https://user-images.githubusercontent.com/20933055/235304790-01cf7bda-c3d4-4e77-bcec-856c3058b003.png)
RouteInformationProvider: Provides the route information to the router. It 
informs the router about the initial route and notifies it of new intents.
• RouteInformationParser: Gets the route string from 
RouteInformationProvider, then parses the URL string to a generic user-defined 
data type. This data type is a navigation configuration.


## Testing
### Testing Deep Links on iOS
Enter the following in your terminal:
`xcrun simctl openurl booted 'fooderlich://raywenderlich.com/1'`
### Testing Deep Links on Android
Enter the following in your terminal:
`
~/Library/Android/sdk/platform-tools/adb shell am start -a 
android.intent.action.VIEW \
 -c android.intent.category.BROWSABLE \
 -d 'fooderlich://raywenderlich.com/1'
 `
### Running the Web App
Go through the Fooderlich UI flow, and you’ll see that the web browser’s address bar 
changes:
![image](https://user-images.githubusercontent.com/20933055/235304924-cfcb5bd1-77d4-42ba-aeeb-8f056a2c340c.png)
If we change the tab query parameter’s value to 0, 1 or 2, the app automatically 
switches to that tab.
![image](https://user-images.githubusercontent.com/20933055/235304944-18ff1dda-52ae-4cd4-927f-6d893e11f0f0.png)


## Notes to take:
• The app notifies RouteInformationProvider when there’s a new route.
• The provider passes the route information to RouteInformationParser to parse 
the URL string.
• The parser converts route information state to and from a URL string.
• GoRouter converts route information state to and from a RouteMatchList.
