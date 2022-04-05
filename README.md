# Telnyx Video SDK for iOS
This repository contains releases of Telnyx's Video SDK for iOS. Currently a release is installed through CocoaPods.

## Adding Telnyx Video SDK to your iOS project:
Currently the Video SDK is delivered through Cocoapods. 

### Cocoapods

If your xcode project is not using [Cocoapods](https://cocoapods.org/) yet, you will need to configure it.

1. Open your podfile and add the TelnyxVideoSdk

```
pod 'TelnyxVideoSdk
```

2. When XCFramework is generated, it must have the `BUILD_LIBRARY_FOR_DISTRIBUTION` flag set to `YES`. When distributing the XCFramework through Cocoapods, the XCFramework's dependencies should also have `BUILD_LIBRARY_FOR_DISTRIBUTION` set to `YES` to avoid getting `dyld: Symbol not found` error in runtime.
To achieve this, the following `post_install` script must be added to your Podfile:

```
post_install do |installer|
    installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
      end
    end
end
```

Your podfile should look something like this: 

```
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

3. Install your pods. You can add the flag --repo-update to ensure your cocoapods has the specs updated.

```Bash
pod install --repo-update
```
4. Open your .xcworkspace 

5. Import TelnyVideoSdk at the top level of your class:

```Swift
import TelnyxVideoSdk
```

6. Disable BITCODE: Go to the Build Settings tab of your project target, search for “bitcode” and set it to “NO”

7. You are all set! 🚀
</br>
