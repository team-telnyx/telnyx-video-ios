# Telnyx Video SDK for iOS
This repository contains releases of Telnyx's Video SDK for iOS. These releases can be installed as a CocoaPod or manually into your project.

## Adding Telnyx Video SDK to your iOS Client Application:
Currently the Video SDK is delivered through Cocoapods. 

### Cocoapods

If your xcode project is not using [cocoapods](https://cocoapods.org/) yet, you will need to configure it.

1. Open your podfile and add the TelnyxVideoSdk

```
pod 'TelnyxVideoSdk', '~> 0.0.1'
```

2. At the end of your podfile also add the following post_install sequence:

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
  pod 'TelnyxVideoSdk', '~> 0.0.1'

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

6. Disable BITCODE: Go to the Build Settings tab of your app target, search for “bitcode” and set it to “NO”

7. Go to your Info.plist file and add the “Privacy - Microphone Usage Description” key with a description that your app requires microphone. 
 
8. Go to your Info.plist file and add the “Privacy - Camera Usage Description” key with a description that your app requires access to cameras.

9. You are all set! 🚀
</br>
