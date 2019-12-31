## User management

Supports various kinds of user systems such as mobile phone, email. Mobile phone supports verification code login and password login. The registration and login of each user system will be separately described later.

The `countryCode` parameter (country code) needs to be provided in the registration and login method for region selection. Data of all available regions is independent. The Chinese Mainland account `(country code: 86)` cannot be used in the `USA (country code: 1)`. The Chinese Mainland account does not exist in the USA region.

All functions of user are realized by using the `WiserSmartUser` Class (singleton).

### Use Mobile Phone for Login

Wiser Smart provides the mobile phone verification code login system.

#### Use Mobile Phone Password for Registration

1.Obtain mobile phone verification code.

Objc:

```objective-c
/**
 *  Send verification code. Used for mobile phone verification code login, register, password reset.
 *  @param type         0: mobile phone verification code login, 1: mobile phone verification code register, 2: mobile phone password reset.
 */
[[WiserSmartUser sharedInstance] sendVerifyCode:@"your_country_code" phoneNumber:@"your_phone_number" type:1 success:^{
    NSLog(@"sendVerifyCode success");
} failure:^(NSError *error) {
    NSLog(@"sendVerifyCode failure: %@", error);
}];
```

Swift:

```swift
/**
 *  Send verification code. Used for mobile phone verification code login, register, password reset.
 *  @param type         0: mobile phone verification code login, 1: mobile phone verification code register, 2: mobile phone password reset.
 */
WiserSmartUser.sharedInstance()?.sendVerifyCode("your_country_code", phoneNumber: "your_phone_number", type: 1, success: {
    print("sendVerifyCode success")
}, failure: { (error) in
    if let e = error {
        print("sendVerifyCode failure: \(e)")
    }
})
```



2.Use your mobile phone and password to registration.

Objc:

```objective-c
[[WiserSmartUser sharedInstance] registerByPhone:@"your_country_code" phoneNumber:@"your_phone_number" password:@"your_password" code:@"verify_code" success:^{
    NSLog(@"register success");
} failure:^(NSError *error) {
    NSLog(@"register failure: %@", error);
}];
```

Swift:

```swift
WiserSmartUser.sharedInstance()?.register(byPhone: "your_country_code", phoneNumber: "your_phone_number", password: "your_password", code: "verify_code", success: {
    print("register success")
}, failure: { (error) in
    if let e = error {
        print("register failure: \(e)")
    }
})
```



#### Use Mobile Phone Verification Code for Login

#### 1.Obtain mobile phone verification code.

Objc:

```objective-c
/**
 *  Send verification code. Used for mobile phone verification code login, register, password reset.
 *  @param type         0: mobile phone verification code login, 1: mobile phone verification code register, 2: mobile phone password reset.
 */
[[WiserSmartUser sharedInstance] sendVerifyCode:@"your_country_code" phoneNumber:@"your_phone_number" type:0 success:^{
    NSLog(@"sendVerifyCode success");
} failure:^(NSError *error) {
    NSLog(@"sendVerifyCode failure: %@", error);
}];
```

Swift:

```swift
/**
 *  Send verification code. Used for mobile phone verification code login, register, password reset.
 *  @param type         0: mobile phone verification code login, 1: mobile phone verification code register, 2: mobile phone password reset.
 */
WiserSmartUser.sharedInstance()?.sendVerifyCode("your_country_code", phoneNumber: "your_phone_number", type: 1, success: {
    print("sendVerifyCode success")
}, failure: { (error) in
    if let e = error {
        print("sendVerifyCode failure: \(e)")
    }
})
```



#### 2.Use mobile phone verification code for login

Objc:

```objective-c
[[WiserSmartUser sharedInstance] loginWithMobile:@"your_phone_number" countryCode:@"your_country_code" code:@"verify_code" success:^{
		NSLog(@"login success");
} failure:^(NSError *error) {
    NSLog(@"login failure: %@", error);
}];
```

Swift:

```swift
WiserSmartUser.sharedInstance()?.login(withMobile: "your_phone_number", countryCode: "your_country_code", code: "verify_code", success: {
    print("login success")
}, failure: { (error) in
    if let e = error {
        print("login failure: \(e)")
    }
})
```



#### Use Mobile Phone Password for Login

Objc:

```objective-c
[[WiserSmartUser sharedInstance] loginByPhone:@"your_country_code" phoneNumber:@"your_phone_number" password:@"your_password" success:^{
		NSLog(@"login success");
} failure:^(NSError *error) {
		NSLog(@"login failure: %@", error);
}];
```

Swift:

```swift
WiserSmartUser.sharedInstance()?.login(byPhone: "your_country_code", phoneNumber: "your_phone_number", password: "your_password", success: {
    print("login success")
}, failure: { (error) in
    if let e = error {
        print("login failure: \(e)")
    }
})
```
#### Resetting Password by Using Mobile Phone

The process of resetting password by using mobile phone is similar to that of registration with mobile phone.

- #### Send verification code:

Objc:

```objc
- (void)sendVerifyCode {
	[WiserSmartUser sharedInstance] sendVerifyCode:@"your_country_code" phoneNumber:@"your_phone_number" type:2 success:^{
		NSLog(@"sendVerifyCode success");
	} failure:^(NSError *error) {
		NSLog(@"sendVerifyCode failure: %@", error);
	}];
}
```

Swift:

```swift
func sendVerifyCode() {
    WiserSmartUser.sharedInstance()?.sendVerifyCode("your_country_code", phoneNumber: "your_phone_number", type: 2, success: {
        print("sendVerifyCode success")
    }, failure: { (error) in
        if let e = error {
            print("sendVerifyCode failure: \(e)")
        }
    })
}
```

- #### Reset password:

Objc:

```objc
- (void)resetPasswordByPhone {
	[WiserSmartUser sharedInstance] resetPasswordByPhone:@"your_country_code" phoneNumber:@"your_phone_number" newPassword:@"your_password" code:@"verify_code" success:^{
		NSLog(@"resetPasswordByPhone success");
	} failure:^(NSError *error) {
		NSLog(@"resetPasswordByPhone failure: %@", error);
	}];
}
```

Swift:

```swift
func resetPasswordByPhone() {
    WiserSmartUser.sharedInstance()?.resetPassword(byPhone: "your_country_code", phoneNumber: "your_phone_number", newPassword: "your_password", code: "verify_code", success: {
        print("resetPasswordByPhone success")
    }, failure: { (error) in
        if let e = error {
            print("resetPasswordByPhone failure: \(e)")
        }
    })
}
```


### Use Email for Login

Wiser Smart provides the email password login system.

#### User Email Password Registration

1.Register your email and obtain the verification code received in the email.

Objc:

```objective-c
[[WiserSmartUser sharedInstance] sendVerifyCodeByRegisterEmail:@"your_country_code" email:@"your_email" success:^{
  	NSLog(@"sendVerifyCode success");
} failure:^(NSError *error) {
    NSLog(@"sendVerifyCode failure: %@", error);
}];
```

Swift:

```swift
WiserSmartUser.sharedInstance()?.sendVerifyCode(byRegisterEmail: "your_country_code", email: "your_email", success: {
    print("sendVerifyCode success")
}, failure: { (error) in
    if let e = error {
        print("sendVerifyCode failure: \(e)")
    }
})
```



2.Select a password for your email.

Objc:

```objective-c
[[WiserSmartUser sharedInstance] registerByEmail:@"your_country_code" email:@"your_email" password:@"your_password" code:@"verify_code" success:^{
    NSLog(@"register success");
} failure:^(NSError *error) {
    NSLog(@"register failure: %@", error);
}];
```

Swift:

```swift
WiserSmartUser.sharedInstance()?.register(byEmail: "your_country_code", email: "your_email", password: "your_password", code: "verify_code", success: {
    print("register success")
}, failure: { (error) in
    if let e = error {
        print("register failure: \(e)")
    }
})
```



#### Use Email Password for Login

Objc:

```objective-c
[[WiserSmartUser sharedInstance] loginByEmail:@"your_country_code" email:@"your_email" password:@"your_password" success:^{
    NSLog(@"login success");
} failure:^(NSError *error) {
    NSLog(@"login failure: %@", error);
}];
```

Swift:

```swift
WiserSmartUser.sharedInstance()?.login(byEmail: "your_country_code", email: "your_email", password: "your_password", success: {
    print("login success")
}, failure: { (error) in
    if let e = error {
        print("login failure: \(e)")
    }
})
```

#### Reset email password

Resetting password by using email takes two steps:

- Send the verification code to an email.

Objc:

```objc
- (void)sendVerifyCodeByEmail {
	[WiserSmartUser sharedInstance] sendVerifyCodeByEmail:@"your_country_code" email:@"your_email" success:^{
		NSLog(@"sendVerifyCodeByEmail success");
	} failure:^(NSError *error) {
		NSLog(@"sendVerifyCodeByEmail failure: %@", error);
	}];
}
```

Swift:

```swift
func sendVerifyCodeByEmail() {
    WiserSmartUser.sharedInstance()?.sendVerifyCode(byEmail: "your_country_code", email: "your_email", success: {
        print("sendVerifyCodeByEmail success")
    }, failure: { (error) in
        if let e = error {
            print("sendVerifyCodeByEmail failure: \(e)")
        }
    })
}
```

- Use the verification code to reset password after the verification code is received.

Objc:

```objc
- (void)resetPasswordByEmail {
	[WiserSmartUser sharedInstance] resetPasswordByEmail:@"your_country_code" email:@"your_email" newPassword:@"your_password" code:@"verify_code" success:^{
		NSLog(@"resetPasswordByEmail success");
	} failure:^(NSError *error) {
		NSLog(@"resetPasswordByEmail failure: %@", error);
	}];
}
```

Swift:

```swift
func resetPasswordByEmail() {
    WiserSmartUser.sharedInstance()?.resetPassword(byEmail: "your_country_code", email: "your_email", newPassword: "your_password", code: "verify_code", success: {
        print("resetPasswordByEmail success")
    }, failure: { (error) in
        if let e = error {
            print("resetPasswordByEmail failure: \(e)")
        }
    })
}
```


### Modify User Avatar

**Interface description**

Used to upload user-defined avatars.

Objc:

```objc
- (void)updateHeadIcon:(UIImage *)headIcon {
	[[WiserSmartUser sharedInstance] updateHeadIcon:headIcon success:^{
		NSLog(@"update head icon success");
	} failure:^(NSError *error) {
		NSLog(@"update head icon failure: %@", error);
	}];
}
```

Swift:

```swift
func updateHeadIcon(_ headIcon: UIImage) {
    WiserSmartUser.sharedInstance()?.updateHeadIcon(headIcon, success: {
        print("update head icon success")
    }, failure: { (error) in
        if let e = error {
            print("update head icon failure: \(e)")
        }
    })
}
```

### Set the Unit of Temperature

**Interface description**

Set the temperature in Celsius or Fahrenheit

```objc
- (void)updateTempUnitWithTempUnit:(NSInteger)tempUnit {
	[[WiserSmartUser sharedInstance] updateTempUnitWithTempUnit:tempUnit success:^{
		NSLog(@"update temp unit success");
	} failure:^(NSError *error) {
		NSLog(@"update temp unit failure: %@", error);
	}];
}
```

Swift:

```swift
func updateTempUnit(withTempUnit tempUnit: Int) {
    WiserSmartUser.sharedInstance().updateTempUnit(withTempUnit: tempUnit, success: {
        print("update temp unit success")
    }, failure: { error in
        if let error = error {
            print("update temp unit failure: \(error)")
        }
    })
}
```

### Modify nickname

Objc:

```objc
- (void)modifyNickname:(NSString *)nickname {
	[[WiserSmartUser sharedInstance] updateNickname:nickname success:^{
		NSLog(@"updateNickname success");
	} failure:^(NSError *error) {
		NSLog(@"updateNickname failure: %@", error);
	}];
}
```

Swift:

```swift
func modifyNickname(_ nickName: String) {
    WiserSmartUser.sharedInstance()?.updateNickname(nickName, success: {
        print("updateNickname success")
    }, failure: { (error) in
        if let e = error {
            print("updateNickname failure: \(e)")
        }
    })
}
```

### Update timezone

Objc:

```objc
- (void)updateTimeZoneId:(NSString *)timeZoneId {
	[[WiserSmartUser sharedInstance] updateTimeZoneWithTimeZoneId:timeZoneId success:^{
		NSLog(@"update timeZoneId success");
	} failure:^(NSError *error) {
		NSLog(@"update timeZoneId failure: %@", error);
	}];
}
```

Swift:

```swift
func updateTimeZoneId(_ timeZoneId: String) {
    WiserSmartUser.sharedInstance()?.updateTimeZone(withTimeZoneId: timeZoneId, success: {
        print("update timeZoneId success")
    }, failure: { (error) in
        if let e = error {
            print("update timeZoneId failure: \(e)")
        }
    })
}
```



### Update location

If need, location can be reported through this api:

Objc:

```objc
- (void)updateLocation {
  double latitude = 30.000;
  double longitude = 120.000;
  [[WiserSmartSDK sharedInstance] updateLatitude:latitude longitude:longitude];
}
```

Swift:

```swift
func updateLocation() {
  WiserSmartSDK.sharedInstance()?.updataLatitude(latitude, longitude: longitude);
}
```



### Logout

Objc:

```objc
- (void)loginOut {
	[WiserSmartUser sharedInstance] loginOut:^{
		NSLog(@"logOut success");
	} failure:^(NSError *error) {
		NSLog(@"logOut failure: %@", error);
	}];
}
```

Swift:

```swift
func loginOut() {
    WiserSmartUser.sharedInstance()?.loginOut({
        print("logOut success")
    }, failure: { (error) in
        if let e = error {
            print("logOut failure: \(e)")
        }
    })
}
```

### Disable account (deregister user)
After one week, the account will be permanently disabled, and all information in the account will be deleted. If you log in to the account again before it is permanently disabled, your deregistration will be canceled.


Objc:

```objc
- (void)cancelAccount {
	[WiserSmartUser sharedInstance] cancelAccount:^{
		NSLog(@"cancel account success");
	} failure:^(NSError *error) {
		NSLog(@"cancel account failure: %@", error);
	}];
}
```

Swift:

```swift
func cancelAccount() {
    WiserSmartUser.sharedInstance()?.cancelAccount({
        print("cancel account success")
    }, failure: { (error) in
        if let e = error {
            print("cancel account failure: \(e)")
        }
    })
}
```

### Handling of Expired Session

If you have not logged in to your account for a long time, the session expiration error will be returned when you access the server interface. You have to monitor the notification of the 	`WiserSmartUserNotificationUserSessionInvalid` and log in to the account again after the login page is displayed.


Objc:

```objc

- (void)loadNotification {
	[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(sessionInvalid) name:WiserSmartUserNotificationUserSessionInvalid object:nil];
}

- (void)sessionInvalid {
	if ([[WiserSmartUser sharedInstance] isLogin]) {
		NSLog(@"sessionInvalid");
		// Log out
		[[WiserSmartUser sharedInstance] loginOut:nil failure:nil];

		// Go to login page
		MyLoginViewController *vc = [[MyLoginViewController alloc] init];
		self.window.rootViewController = vc;
	    [self.window makeKeyAndVisible];
	}
}
```

Swift:

```swift
func loadNotification() {
    NotificationCenter.default.addObserver(self, selector: #selector(sessionInvalid), name: NSNotification.Name(rawValue: "WiserSmartUserNotificationUserSessionInvalid"), object: nil)
}
    
@objc func sessionInvalid() {
    guard WiserSmartUser.sharedInstance()?.isLogin == true else {
        return
    }
        
    print("sessionInvalid")
    // Log out
    WiserSmartUser.sharedInstance()?.loginOut(nil, failure: nil)
    // Go to login page
}
```

