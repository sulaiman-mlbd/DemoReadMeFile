# GeneLife

GeneLife is a client app of Genesis Healthcare Asia ltd for better serving our clients

[![Platform](https://img.shields.io/cocoapods/p/LFAlertController.svg?style=flat)](http://cocoapods.org/pods/LFAlertController)
[![Swift Version][swift-image]][swift-url]
[![CocoaPods Compatible][cocoapods-image]][cocoapods-image] 


GeneLife shows user about thier analysis report and guide themselves for a better health 

![](genesis.jpeg)

## Requirements

- iOS 11.0+
- Xcode 10.0+

## Project Setup 

Clone the repository: 

```shell 
git clone https://github.com/genesis-healthcare/External-GeneLifeApp-iOS.git
```
Open directory in `terminal`

```shell 
  cd path/External-GeneLifeApp-iOS/
```
Install `bundler` if not installed 

Run the following command in `terminal` on our project to install the dependencies 

```shell
  sh setup.sh
```

or

```shell 
  bundle install --path vendor/bundle
  bundle exec pod install
  Pods/SwiftGen/bin/swiftgen
```

Now, our project is ready to run on `Xcode`. 
Open `project-name.xcworkspace` file for using this project

## Project Structure
```
/<Project Name>
	/Common				# Common loader, error message view etc.
		/Name 1
		/Name 2
	/Data
 		/PersistanceManager 	# Core data, file base data storage manager here
		/Network		# Networking module for this project , handle all networking operation from here
			/Parameter	# Models - From which data will be passed to server from different CRUD operation
			/Response	# Models - Response from server will be parsed as Response type model and will be 						passed to upper layer
	/Dev 				# Dev environmet specific contents
	/Features 			# Contains all screen with ViewController, ViewModel, Storyboard files
		/Feature A		# Contains ViewController, ViewModel, Storyboard for Feature A
		/Feature B
		.....
	/Flows 				# Handle App Navigation with many flow using Coordinator pattern (uses RxFlow) 
	/Model 				# Contains model files 
	/Prod 				# Production environmet specific contents
	/Protocols			# Protocols used in different classes
	/Resources			# Contains assets + some other resources for this project
	/Services			# Contains Services used by different ViewControllers of this 
	/Stg				# Staging environmet specific contents
	/Utility 			# Hold some utility classes like Keymanager etc.
		

```

## Note

### Storyboard
* set colors with sRGB

<img src="https://user-images.githubusercontent.com/4714421/53492287-d65a4600-3adb-11e9-9a63-767d90556cb5.png" width="300">

### RxSwift
* use onNext instead of onError on Subject

```
func requestSomething() -> Observable<Result<ResponseType, ErrorType>> {
    let subject = PublishSubject<Result<ResponseType, ErrorType>>

    someRequest() { response, error in
        if let error = error {
            subject.onNext(Result.failure(error))
            return
        }

        subject.onSuccess(Result.success(response))
    }

    return subject
}
```

[swift-image]:https://img.shields.io/badge/swift-4.2-orange.svg
[swift-url]: https://swift.org/
[cocoapods-image]: https://img.shields.io/badge/pod-v1.5.3-blue.svg
