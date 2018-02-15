# Xcode-Project-Setup
Common practices and tools to be implemented when starting a new Xcode project such as versioning, CI, setting up environements, etc 

* [Setup](#setup)
  * [Versioning](#versioning)
  * [Environments](#environments)
* [Tools](#tools)
  * [Fastlane](#fastlane)
  * [Fabric](#fabric) 
  * [Sketch](#sketch)
* [Common Practices](#common-practices)
  * [Constants](#constants)

## Setup

### Versioning
Setup build and version numbers so that they can be auto incremented using [Fastlane](#fastlane)

![alt text](https://developer.apple.com/library/content/qa/qa1827/Art/QA1827_Versioning.png)

  Initially you are going to want to set: 

  Bundle versions string, short: `1.0.0`

  Bundle verison: `1`

![alt text](https://developer.apple.com/library/content/qa/qa1827/Art/QA1827_InfoPaneInXcode.png)

### Environments


## Tools

### Fastlane
> fastlane is an open source platform aimed at simplifying Android and iOS deployment.

> fastlane lets you automate every aspect of your development and release workflow.

#### Installing
Make sure you have latest verison of Xcode command line tools installed:

`
  xcode-select --install
`

Install fastlane using 

`sudo gem install -fastlane -NV` 

or

`brew cask install fastlane`

#### Setting it up in your project
Navigate to project directory and run

`fastlane init`


### Fabric

### Sketch

## Common Practices

### Constants
