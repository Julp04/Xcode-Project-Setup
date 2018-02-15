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
  * (To-Do) Using Result.swift file on completion handler

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

### Fastlane🚀
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

### CocoaPods


### Crashlytics

#### Install Crashlytics via CocoaPods
```
use_frameworks!
pod 'Fabric'
pod 'Crashlytics'
```

Run command 
`pod install`

#### Add a run script build phase

### Firebase

### Sketch

## Common Practices

### Constants
