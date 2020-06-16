# 施耐德智能iOS SDK

---

## 功能概述

施耐德智能APP SDK提供了与硬件设备、接口封装，加速应用开发过程，主要包括了以下功能：

- 硬件设备相关（配网、控制、状态上报、群组、固件升级、共享）
- 账户体系（手机号、邮箱的注册、登录、重置密码等通用的账户功能）
- 家庭体系 （家庭管理，房间管理等功能）

## 快速集成

### 使用Cocoapods集成

在`Podfile`文件中添加以下内容：

```ruby
  pod 'WiserSmartBaseKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.14.2'
  pod 'WiserSmartUtil', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.14.2'
  pod 'WiserSmartMQTTChannelKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.14.2'
  pod 'WiserSmartSocketChannelKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.14.2'
  pod 'WiserSmartActivatorKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.14.2'
  pod 'WiserSmartDeviceKit', :git => 'https://github.com/sewiser/WiserSDK_IOS.git', :tag => '3.14.2'
```

然后在项目根目录下执行`pod update`命令，集成第三方库。

CocoaPods的使用请参考：[CocoaPods Guides](https://guides.cocoapods.org/)

## 初始化SDK

1. 打开项目设置，Target => General，修改`Bundle Identifier`对应的iOS包名

2. 导入安全图片到工程根目录，重命名为`t_s.bmp`，并加入「项目设置 => Target => Build Phases => Copy Bundle Resources」中。

3. 在项目的`PrefixHeader.pch`文件添加以下内容：

```objc
#import <WiserSmartHomeKit/WiserSmartKit.h>
```

Swift 项目可以添加在 `xxx_Bridging-Header.h` 桥接文件中添加以下内容

```
#import <WiserSmartHomeKit/WiserSmartKit.h>
```

4. 打开`AppDelegate.m`文件，在`[AppDelegate application:didFinishLaunchingWithOptions:]`方法中初始化SDK：

Objc:

```objc
[[WiserSmartSDK sharedInstance] startWithAppKey:<#your_app_key#> secretKey:<#your_secret_key#>];
```

Swift:

```swift
 WiserSmartSDK.sharedInstance()?.start(withAppKey: <#your_app_key#>, secretKey: <#your_secret_key#>)
```



至此，准备工作已经全部完毕，可以开始App开发啦。

### Debug 模式

在开发的过程中可以开启 Debug 模式，打印一些日志用于分析问题。

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

