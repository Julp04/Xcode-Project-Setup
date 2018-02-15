# Xcode Project Practices
Common practices and tools to be implemented when starting a new Xcode project such as versioning, CI, setting up environements, etc 

* [Setup](#setup)
  * [Versioning](#versioning)
  * [Environments](#environments)
* [Tools](#tools)
  * [Fastlane](#fastlane)
  * [CocoaPods](#cocoapods)
  * [Fabric / Crashlytics](#crashlytics)
  * [Firebase](#firebase)
  * [Sketch](#sketch)
* [Common Practices](#common-practices)
  * [Constants](#constants)
  * [Result.swift](#result)
  
* To-Do
  - [ ] Result.swift
  - [ ] Sketch setup and script
  - [ ] Firebase setup and script
  - [ ] Fastlane example lanes
  - [ ] Finish Crashlytics setup

## Setup

### Versioning
Setup build and version numbers so that they can be auto incremented using [Fastlane](#fastlane)

![alt text](https://developer.apple.com/library/content/qa/qa1827/Art/QA1827_Versioning.png)

  Initially you are going to want to set: 

  Bundle versions string, short: `1.0.0`

  Bundle verison: `1`

![alt text](https://developer.apple.com/library/content/qa/qa1827/Art/QA1827_InfoPaneInXcode.png)

### Environments
When setting up a new Xcode project you are going to want have at least two different environements
#### Development
Environement that will talk to your dev database / api with dummy data

#### Production
So when you are making changes and your app has been shipped to the app store you are not messing with user data that is out in production

#### Setting it up in Xcode
In order too have two environments you will need to create two different targets in your project. 
Under build settings select your target for your app and duplicate it

![alt text](https://github.com/Julp04/Xcode-Project-Setup/blob/master/images/duplicate.png)

This will create a new target with named "appname copy" -> You should rename this to something like "appname-dev"

When you create this new target it will create another Info.plist for this specific target as well as give it a new BundleId

![alt text](https://github.com/Julp04/Xcode-Project-Setup/blob/master/images/dev-infoplist.png)

After you have setup your new target, you are most likely going to want to set a flag so that you can run certain code for specifics environment

To add a flag go to Build Settings and in the search bar type "other swift flags"

Here you are gonna want to add a flag to determine that this is the development target. See below

![alt text](https://github.com/Julp04/Xcode-Project-Setup/blob/master/images/swiftflags.png)

So now in your AppDelagate you can do something like this:

```swift
#if DEVELOPMENT
            let filePath = Bundle.main.path(forResource: "GoogleService-Info-DEV", ofType: "plist")!
            let options = FIROptions(contentsOfFile: filePath)
            FIRApp.configure(with: options!)
        #else
            let filePath = Bundle.main.path(forResource: "GoogleService-Info", ofType: "plist")!
            let options = FIROptions(contentsOfFile: filePath)
            FIRApp.configure(with: options!)
            Fabric.with([Crashlytics.self])
        #endif
```
Using [Firebase](#firebase) as backend service and configuring it up for dev and prod environments


## Tools

### [Fastlane](https://fastlane.tools/)<img src="https://avatars0.githubusercontent.com/u/11098337?s=400&v=4" width="30" height="30">
> fastlane is an open source platform aimed at simplifying Android and iOS deployment.

> fastlane lets you automate every aspect of your development and release workflow.

#### Installing
Make sure you have latest verison of Xcode command line tools installed:

`xcode-select --install`

Install fastlane using 

`sudo gem install -fastlane -NV` 

or

`brew cask install fastlane`

#### Setting it up in your project
Navigate to project directory and run

`fastlane init`

### [CocoaPods](https://cocoapods.org/)
CocoaPods are a very easy way to integreate different frameworks and packages into your project.
There are tons and tons of cocoapods out there that will save development hours for many different aspects of your project like:

* Custom Alert Views
* Custom Login Pages
* Setting up backend services like [Firebase](#firebase) or [Crashlytics](#crashlytics)
* Much, much more!

In order to use cocoapods in your project cd in your project directory and run

`pod init`

This will create a podfile that looks like this:

![alt text](https://github.com/Julp04/Xcode-Project-Setup/blob/master/images/podfile.png)

#### Install pods
cd into your project director and run

`pod install`

This will create a new .xcworkspace file in your directory which you should now use from now on instead of .xcproj


### [Crashlytics](https://fabric.io/kits/ios/crashlytics/install)<img src="https://a.slack-edge.com/7f1a0/plugins/crashlytics/assets/service_512.png" width="30" height="30">

#### Install Crashlytics via CocoaPods
```
use_frameworks!
pod 'Fabric'
pod 'Crashlytics'
```

Run command 
`pod install`

#### Add a run script build phase

### [Firebase](https://firebase.google.com/docs/ios/setup)<img src="https://firebase.google.com/_static/images/firebase/touchicon-180.png" width="30" height="30">

### [Sketch](https://sketchapp.com)<img src="https://www.sketchapp.com/images/press/sketch-press-kit/app-icons/sketch-mac-icon@2x.png" width="30" height="30">

## Common Practices

### Constants
