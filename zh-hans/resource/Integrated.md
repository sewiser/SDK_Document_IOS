## 集成SDK

### 使用CocoaPods快速集成（SDK最低支持系统版本8.0）

在`Podfile`文件中添加以下内容：

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

然后在项目根目录下执行`pod update`命令进行集成。

_CocoaPods的使用请参考：[CocoaPods Guides](https://guides.cocoapods.org/)_
_CocoaPods建议更新至最新版本_

