# Telnyx Video SDK for iOS
This repository contains releases of Telnyx's Video SDK for iOS. Currently a release is installed through CocoaPods.


## Cocoapods

If your xcode project is not using [Cocoapods](https://cocoapods.org/) yet, you will need to configure it. 

From your project directory in a terminal do:
```bash
pod init
```
Like the on screen instructions mention, this will create two files: a `Podfile` and a `.xcworkspace` file in the directory. You'll want to use that to open your project moving forward.


### Adding the sdk to your project
1\. Open your podfile and add the TelnyxVideoSdk

target 'TARGET_NAME' do
		pod 'TelnyxVideoSdk', '~> 0.3.0'
end
```

2\. Add the `post_install` script to your Podfile

**Why is this needed?**  
We distribute our SDK binary as an XCFramework. When our XCFramework is generated, it must have the `BUILD_LIBRARY_FOR_DISTRIBUTION` flag set to `YES`. In order to distribute it via Cocoapods, all of XCFramework's dependencies need to also have `BUILD_LIBRARY_FOR_DISTRIBUTION` set to `YES`.Doing this avoids a  `dyld: Symbol not found` runtime error.

To achieve this, the following `post_install` script must be added to your Podfile:

```swift
post_install do |installer|
    installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
      end
    end
end
```

Your podfile should look something like this: 

```swift
platform :ios, '12.0'

target 'YOUR_APP_TARGET' do
  use_frameworks!

  # Pods for YOUR_APP_TARGET
  pod 'TelnyxVideoSdk'

  post_install do |installer|
    installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
      end
    end
  end
end
```

3\. Install your pods

```bash
pod install
```
4\. Open your `.xcworkspace`

5\. Import TelnyVideoSdk at the top level of your class**

```swift
import TelnyxVideoSdk
```

6\. Disable BITCODE: Go to the Build Settings tab of your `Target`, search for `bitcode` keyword and set it to `NO`.

7\. You are all set! 🚀
</br>
