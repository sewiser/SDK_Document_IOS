## Integrated SDK

### Use CocoaPods for quick integration (SDK basically supports system version 8.0)

Add the following content in the `Podfile` file.

```ruby
platform :ios, '8.0'

target 'Your_Project_Name' do
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
end
```

Then run the `pod update` command in the root directory of project.
For use of CocoaPods, please refer to the [CocoaPods Guides](https://guides.cocoapods.org/) It is recommended to update the CocoaPods to the latest version.
