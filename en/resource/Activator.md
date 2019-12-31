

## Network Configuration

The network configuration modes supported by Wiser hardware module including:

- quick connection mode (TLink, it is referred to as the EZ mode) 
-  hotspot mode (AP mode). 
-  wired network configuration (Wired gateway use, no wifi configuration information required)
- sub-device configuration 
- bluetooth-wifi configuration

The quick connection mode features convenient operation. It is recommended to use the hotspot mode as the backup in case the quick connection mode fails. 

All functions related to the network configuration are realized by using the `WiserSmartActivator` Class (singleton).


### EZ mode

**Process of EZ mode network configuration:**

```sequence

Title: EZ Mode

participant APP
participant SDK
participant Device
participant Service

Note over APP: Connect to the Wifi of router
Note over Device: Switch to the EZ mode

APP->SDK: Get Token
SDK->Service: Get Token
Service-->SDK: Response Token
SDK-->APP: Response Token

APP->SDK: Start network configuration (send configuration data)
Note over SDK: broadcast configuration data
Device->Device: Get configuration data

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Device-->SDK: Network configuration succeeds
SDK-->APP: Network configuration succeeds

```

#### Get Token

Before the EZ/AP mode network configuration, the SDK needs to obtain the network configuration Token . The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds. A new Token has to be obtained if you have to reconfigure network.

Objc:

```
- (void)getToken {
	[[WiserSmartActivator sharedInstance] getTokenWithHomeId:homeId success:^(NSString *token) {
		NSLog(@"getToken success: %@", token);
		// TODO: startConfigWiFi
	} failure:^(NSError *error) {
		NSLog(@"getToken failure: %@", error.localizedDescription);
	}];
}
```

Swift:

```swift
func getToken() {
    WiserSmartActivator.sharedInstance()?.getTokenWithHomeId(homeId, success: { (token) in
        print("getToken success: \(token)")
        // TODO: startConfigWiFi
    }, failure: { (error) in
        if let e = error {
            print("getToken failure: \(e)")
        }
    })
}
```

#### Start network configuration.

EZ mode network configuration:

Objc:

```objc
- (void)startConfigWiFi:(NSString *)ssid password:(NSString *)password token:(NSString *)token {
	// Set WiserSmartActivator delegate，impl delegate method
	[WiserSmartActivator sharedInstance].delegate = self;

	// start activator
	[[WiserSmartActivator sharedInstance] startConfigWiFi:TYActivatorModeEZ ssid:ssid password:password token:token timeout:100];
}

#pragma mark - WiserSmartActivatorDelegate
- (void)activator:(WiserSmartActivator *)activator didReceiveDevice:(WiserSmartDeviceModel *)deviceModel error:(NSError *)error {

	if (!error && deviceModel) {
		//active success
    }

    if (error) {
        //active failure
    }
}

```

Swift:

```swift
func startConfigWiFi(withSsid ssid: String, password: String, token: String) {
    // Set WiserSmartActivator delegate，impl delegate method
    WiserSmartActivator.sharedInstance()?.delegate = self
    
    // start activator
    WiserSmartActivator.sharedInstance()?.startConfigWiFi(TYActivatorModeEZ, ssid: ssid, password: password, token: token, timeout: 100)
}

#pragma mark - WiserSmartActivatorDelegate
func activator(_ activator: WiserSmartActivator!, didReceiveDevice deviceModel: WiserSmartDeviceModel!, error: Error!) {
    if deviceModel != nil && error == nil {
        //active success
    }
        
    if let e = error {
        //active failure
        print("\(e)")
    }
}
```

The AP mode network configuration is the same to the EZ mode network configuration. You just need to change the first parameter of the `[WiserSmartActivator startConfigWiFi:ssid:password:token:timeout:]` to TYActivatorModeAP. But the `ssid` and `password` needs to be the name and password of router hotspot instead of the device hotspot.

#### Stop network configuration.

The App will continuously broadcast the network configuration information until the network configuration succeeds or the timeout is reached once the network configuration starts. The `[WiserSmartActivator stopConfigWiFi]` method has to be invoked if you need to cancel the network configuration or the network configuration is completed.

Objc:

```objc
- (void)stopConfigWifi {
	[WiserSmartActivator sharedInstance].delegate = nil;
	[[WiserSmartActivator sharedInstance] stopConfigWiFi];
}
```

Swift:

```swift
func stopConfigWifi() {
    WiserSmartActivator.sharedInstance()?.delegate = nil
    WiserSmartActivator.sharedInstance()?.stopConfigWiFi()
}
```


## AP mode

**Process of AP mode network configuration**

```sequence

Title: AP Mode

participant APP
participant SDK
participant Device
participant Service

Note over Device: Switch to the AP mode
APP->SDK: Get Token
SDK->Service: Get Token
Service-->SDK: Response Token
SDK-->APP: Response Token

Note over APP: Connect the hotspot device

APP->SDK: Start network configuration (send configuration data)
SDK->Device: send configuration data
Note over Device: Device turns off hotspot automatically

Note over Device: The device is connected to the Wifi of router

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Device-->SDK: Network configuration succeeds
SDK-->APP: Network configuration succeeds

```

#### Get Token

Before the EZ/AP mode network configuration, the SDK needs to obtain the network configuration Token. The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds. A new Token has to be obtained if you have to reconfigure network.

Objc:

```
- (void)getToken {
	[[WiserSmartActivator sharedInstance] getTokenWithHomeId:homeId success:^(NSString *token) {
		NSLog(@"getToken success: %@", token);
		// TODO: startConfigWiFi
	} failure:^(NSError *error) {
		NSLog(@"getToken failure: %@", error.localizedDescription);
	}];
}
```

Swift:

```swift
func getToken() {
    WiserSmartActivator.sharedInstance()?.getTokenWithHomeId(homeId, success: { (token) in
        print("getToken success: \(token)")
        // TODO: startConfigWiFi
    }, failure: { (error) in
        if let e = error {
            print("getToken failure: \(e)")
        }
    })
}
```

#### Start network configuration.

AP mode network configuration:

Objc:

```objc
- (void)startConfigWiFi:(NSString *)ssid password:(NSString *)password token:(NSString *)token {
	// Set WiserSmartActivator delegate，impl delegate method
	[WiserSmartActivator sharedInstance].delegate = self;

	// Start activator
	[[WiserSmartActivator sharedInstance] startConfigWiFi:TYActivatorModeAP ssid:ssid password:password token:token timeout:100];
}

#pragma mark - WiserSmartActivatorDelegate
- (void)activator:(WiserSmartActivator *)activator didReceiveDevice:(WiserSmartDeviceModel *)deviceModel error:(NSError *)error {

	if (!error && deviceModel) {
		//active success
    }

    if (error) {
        //active failure
    }
}

```

Swift:

```swift
func startConfigWiFi(withSsid ssid: String, password: String, token: String) {
    // Set WiserSmartActivator delegate，impl delegate method
    WiserSmartActivator.sharedInstance()?.delegate = self
    
    // Start activator
    WiserSmartActivator.sharedInstance()?.startConfigWiFi(TYActivatorModeAP, ssid: ssid, password: password, token: token, timeout: 100)
}

#pragma mark - WiserSmartActivatorDelegate
func activator(_ activator: WiserSmartActivator!, didReceiveDevice deviceModel: WiserSmartDeviceModel!, error: Error!) {
    if deviceModel != nil && error == nil {
        //active success
    }
        
    if let e = error {
        //active failure
        print("\(e)")
    }
}
```

The AP mode network configuration is the same to the EZ mode network configuration. You just need to change the first parameter of the `[WiserSmartActivator startConfigWiFi:ssid:password:token:timeout:]` to TYActivatorModeAP. But the `ssid` and `password` needs to be the name and password of router hotspot instead of the device hotspot.

#### Stop network configuration.

The App will continuously broadcast the network configuration information until the network configuration succeeds or the timeout is reached once the network configuration starts. The `[WiserSmartActivator stopConfigWiFi]` method has to be invoked if you need to cancel the network configuration or the network configuration is completed.

Objc:

```objc
- (void)stopConfigWifi {
	[WiserSmartActivator sharedInstance].delegate = nil;
	[[WiserSmartActivator sharedInstance] stopConfigWiFi];
}
```

Swift:

```swift
func stopConfigWifi() {
    WiserSmartActivator.sharedInstance()?.delegate = nil
    WiserSmartActivator.sharedInstance()?.stopConfigWiFi()
}
```


#### Wired network configuration 

```sequence

Title: Zigbee Gateway configuration

participant APP
participant SDK
participant Zigbee Gateway
participant Service

Note over Zigbee Gateway: Reset zigbee gateway
APP->SDK: Get Token
SDK->Service: Get Token
Service-->SDK: Response Token
SDK-->APP: Response Token

APP->APP: connect mobile phone to the same hotspot of the gateway

APP->SDK: sends the activation instruction
SDK->Zigbee Gateway: sends the activation instruction
Note over Zigbee Gateway: device receives the activation data

Zigbee Gateway->Service: activate the device
Service-->Zigbee Gateway: network configuration succeeds

Zigbee Gateway-->SDK: network configuration succeeds
SDK-->APP: network configuration succeeds

```

#### Get Token

Before the EZ/AP mode network configuration, the SDK needs to obtain the network configuration Token. The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds. A new Token has to be obtained if you have to reconfigure network.

Objc:

```
- (void)getToken {
	[[WiserSmartActivator sharedInstance] getTokenWithHomeId:homeId success:^(NSString *token) {
		NSLog(@"getToken success: %@", token);
		// TODO: startConfigWiFi
	} failure:^(NSError *error) {
		NSLog(@"getToken failure: %@", error.localizedDescription);
	}];
}
```

Swift:

```swift
func getToken() {
    WiserSmartActivator.sharedInstance()?.getTokenWithHomeId(homeId, success: { (token) in
        print("getToken success: \(token)")
        // TODO: startConfigWiFi
    }, failure: { (error) in
        if let e = error {
            print("getToken failure: \(e)")
        }
    })
}
```

##### Wired network configuration of zigbee

Objc:

```objc
- (void)startConfigWiFiToken:(NSString *)token {
	// Set WiserSmartActivator delegate，impl delegate method
	[WiserSmartActivator sharedInstance].delegate = self;

	// Start activator
	[[WiserSmartActivator sharedInstance] startConfigWiFiWithToken:token timeout:100];
}

#pragma mark - WiserSmartActivatorDelegate
- (void)activator:(WiserSmartActivator *)activator didReceiveDevice:(WiserSmartDeviceModel *)deviceModel error:(NSError *)error {

	if (!error && deviceModel) {
		//active success
    }

    if (error) {
        //active failure
    }

}

```

Swift:

```swift
func startConfigWifiToken(_ token: String) {
    // Set WiserSmartActivator delegate，impl delegate method
    WiserSmartActivator.sharedInstance()?.delegate = self
    
    // Start activator
    WiserSmartActivator.sharedInstance()?.startConfigWiFi(withToken: token, timeout: 100)
}

#pragma mark - WiserSmartActivatorDelegate
func activator(_ activator: WiserSmartActivator!, didReceiveDevice deviceModel: WiserSmartDeviceModel!, error: Error!) {
    if deviceModel != nil && error == nil {
        //active success
    }
        
    if let e = error {
        //active failure
        print("\(e)")
    }
}
```

#### Stop network configuration.

The App will continuously broadcast the network configuration information until the network configuration succeeds or the timeout is reached once the network configuration starts. The `[WiserSmartActivator stopConfigWiFi]` method has to be invoked if you need to cancel the network configuration or the network configuration is completed.

Objc:

```objc
- (void)stopConfigWifi {
	[WiserSmartActivator sharedInstance].delegate = nil;
	[[WiserSmartActivator sharedInstance] stopConfigWiFi];
}
```

Swift:

```swift
func stopConfigWifi() {
    WiserSmartActivator.sharedInstance()?.delegate = nil
    WiserSmartActivator.sharedInstance()?.stopConfigWiFi()
}
```


### Activate the  sub-device

```sequence

Title: Zigbee sub-device configuration

participant APP
participant SDK
participant Zigbee Gateway
participant Service

Note over Zigbee Gateway: Reset zigbee sub device
APP->SDK: sends the subdevice activation instruction
SDK->Zigbee Gateway: sends the activation instruction

Note over Zigbee Gateway: zigbee gateway receives the activation data

Zigbee Gateway->Service: activate the sub device
Service-->Zigbee Gateway: network configuration succeeds

Zigbee Gateway-->SDK: network configuration succeeds
SDK-->APP: network configuration succeeds

```

The `stopActiveSubDeviceWithGwId` method has to be invoked if you need to cancel the network configuration or the network configuration is completed.

```objc
- (void)activeSubDevice {
    // Set WiserSmartActivator delegate，impl delegate method
	[WiserSmartActivator sharedInstance].delegate = self;

	[[WiserSmartActivator sharedInstance] activeSubDeviceWithGwId:@"your_device_id" timeout:100];
}

#pragma mark - WiserSmartActivatorDelegate
- (void)activator:(WiserSmartActivator *)activator didReceiveDevice:(WiserSmartDeviceModel *)deviceModel error:(NSError *)error {

    if (!error && deviceModel) {
		//active success
    }

    if (error) {
        //active failure
    }
}
```

Swift:

```swift
func activeSubDevice() {
    // Set WiserSmartActivator delegate，impl delegate method
    WiserSmartActivator.sharedInstance()?.delegate = self
    
    WiserSmartActivator.sharedInstance()?.activeSubDevice(withGwId: "your_device_id", timeout: 100)
}

#pragma mark - WiserSmartActivatorDelegate
func activator(_ activator: WiserSmartActivator!, didReceiveDevice deviceModel: WiserSmartDeviceModel!, error: Error!) {
    if deviceModel != nil && error == nil {
        //active success
    }
        
    if let e = error {
        //active failure
        print("\(e)")
    }
}
```

#### Stop activating the sub-device

Objc:

```objc
- (void)stopActiveSubDevice {
  [WiserSmartActivator sharedInstance].delegate = nil;
	[[WiserSmartActivator sharedInstance] stopActiveSubDeviceWithGwId:@"your_device_id"];
}
```

Swift:

```swift
func stopActiveSubDevice() {
  	WiserSmartActivator.sharedInstance()?.delegate = nil
    WiserSmartActivator.sharedInstance()?.stopActiveSubDevice(withGwId: "your_device_id")
}
```

