# Xcode-Project-Setup
Common practices and tools to be implemented when starting a new Xcode project such as versioning, CI, setting up environements, etc 

## Fastlane 🚀
> fastlane is an open source platform aimed at simplifying Android and iOS deployment.

> fastlane lets you automate every aspect of your development and release workflow.

### Installing
Make sure you have latest verison of Xcode command line tools installed:

`
  xcode-select --install
`

Install fastlane using 

`sudo gem install -fastlane -NV` 

or

`brew cask install fastlane`

### Setting it up in pyour project
Navigate to project directory and run

`fastlane init`

