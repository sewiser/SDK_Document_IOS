# Wiser Smart iOS SDK

---


## Features Overview

Wiser Smart APP SDK provides the interface package for the communication with hardware and accelerate the application development process, including the following features:

- Hardware functions (network configuration, control, status reporting, groups, firmware upgrades, sharing)
- Account system (phone number, email registration, login, password reset and other general account functions)
- Home system (home management, room management)

## Fast Integration

### Using CocoaPods

Add the following content in file `Podfile`:

```ruby
  pod 'WiserSmartBaseKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartUtil', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartActivatorCoreKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartActivatorKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartDeviceCoreKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartDeviceKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartFeedbackKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartMessageKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartMQTTChannelKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartSocketChannelKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartSceneKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
  pod 'WiserSmartTimerKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.26.5'
```

Execute command `pod update` in the project's root directory to begin integration.

For the instructions of CocoaPods, please refer to: [CocoaPods Guides](https://guides.cocoapods.org/)

## Initializing SDK

1. Open project setting, `Target => General`, edit `Bundle Identifier` to the value.

2. Import security image to the project and rename as `t_s.bmp`, then add it into `Project Setting => Target => Build Phases => Copy Bundle Resources`.

3. Add the following to the project file `PrefixHeader.pch`：

```objc
#import <WiserSmartHomeKit/WiserSmartKit.h>
```

Swift project add the following to the `xxx_Bridging-Header.h` file:

```swift
#import <WiserSmartHomeKit/WiserSmartKit.h>
```

4. Open file `AppDelegate.m`，and use the `App Key` and `App Secret` obtained from the development platform in the `[AppDelegate application:didFinishLaunchingWithOptions:]`method to initialize SDK:

Objc:

```objc
[[WiserSmartSDK sharedInstance] startWithAppKey:<#your_app_key#> secretKey:<#your_secret_key#>];
```

Swift:

```swift
 WiserSmartSDK.sharedInstance()?.start(withAppKey: <#your_app_key#>, secretKey: <#your_secret_key#>)
```

Now all the prepare work has been completed. You can use the sdk to develop your application now.



### Debug Mode

During the development we can open debug mode, print the log to analyze some problem.

Objc:

```objc
#ifdef DEBUG
    [[WiserSmartSDK sharedInstance] setDebugMode:YES];
#else
#endif
```

Swift:

```swift
#if DEBUG
   WiserSmartSDK.sharedInstance()?.debugMode = true
#else
#endif
```

