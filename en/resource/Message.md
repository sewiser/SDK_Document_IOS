## Message center

All functions related to the message center are realized by using the `WiserSmartMessage` class. Obtaining message list, deleting messages in batches and checking for message update are supported. 

### Obtain message list

Objc:

```objc
- (void)getMessageList {
//    self.smartMessage = [[WiserSmartMessage alloc] init];
	[self.smartMessage getMessageList:^(NSArray<WiserSmartMessageListModel *> *list) {
		NSLog(@"get message list success:%@", list);
	} failure:^(NSError *error) {
		NSLog(@"get message list failure:%@", error);
	}];
}
```
Swift:

```swift
func getMessageList() {
    smartMessage?.getList({ (list) in
        print("get message list success: \(list)")
    }, failure: { (error) in
        if let e = error {
            print("get message list failure: \(e)")
        }
    })
}
```

### Delete messages

Delete messages in batches. `messgeIdList` denotes the id group of messages to be deleted, and the message id can be attained from the message list. 

```objc
- (void)deleteMessage {
//    self.smartMessage = [[WiserSmartMessage alloc] init];
    [self.smartMessage deleteMessage:(NSArray <NSString *> *)messgeIdList success:^{
		NSLog(@"delete message success");
    } failure:^(NSError *error) {
    	NSLog(@"delete message failure:%@", error);
    }];
}
```
Swift:

```swift
func deleteMessage() {
    smartMessage?.delete(["messgeIdList"], success: {
        print("delete message success")
    }, failure: { (error) in
        if let e = error {
            print("delete message failure: \(e)")
        }
    })
}
```
### Obtain the timestamp of the latest news

The timestamp of the latest news can be compared with that of local latest message. If the former is bigger than the later, a red dot will be displayed to hint the new message. 

Objc:

```objc
- (void)getMessageMaxTime {
//    self.smartMessage = [[WiserSmartMessage alloc] init];
	[self.smartMessage getMessageMaxTime:^(int result) {
		NSLog(@"get message max time success:%d", result);
	} failure:^(NSError *error) {
		NSLog(@"get message max time failure:%@", error);
	}];
}
```

Swift:

```swift
func getMessageMaxTime() {
    smartMessage?.getMaxTime({ (result) in
        print("get message max time success :\(result)")
    }, failure: { (error) in
        if let e = error {
            print("get message max time failure: \(e)")
        }
    })
}
```



### Message push settings

#### Get message push status

The main control of all message push, including device alert, family message, notification message.

```objective-c
[[WiserSmartSDK sharedInstance] getPushStatusWithSuccess:^(BOOL result) {

} failure:^(NSError *error) {

}];
```

#### Switch message push on/off

```objective-c
BOOL enable = YES;
[[WiserSmartSDK sharedInstance] setPushStatusWithStatus:enable  success:^{

} failure:^(NSError *error) {

}];
```

#### Get status of device alert status

```objective-c
[[WiserSmartSDK sharedInstance] getDevicePushStatusWithSuccess:^(BOOL result) {

} failure:^(NSError *error) {

}];
```

#### Switch device alert on.off

```objective-c
BOOL enable = YES;
[[WiserSmartSDK sharedInstance] setDevicePushStatusWithStauts:enable  success:^{

} failure:^(NSError *error) {

}];
```

#### Get family message status

```objective-c
[[WiserSmartSDK sharedInstance] getFamilyPushStatusWithSuccess:^(BOOL result) {

} failure:^(NSError *error) {

}];
```

#### Switch family message on/off

```objective-c
BOOL enable = YES;
[[WiserSmartSDK sharedInstance] setFamilyPushStatusWithStauts:enable  success:^{

} failure:^(NSError *error) {

}];
```

#### Get notification message status

```objective-c
[[WiserSmartSDK sharedInstance] getNoticePushStatusWithSuccess:^(BOOL result) {

} failure:^(NSError *error) {

}];
```

#### Switch notification message on/off

```objective-c
BOOL enable = YES;
[[WiserSmartSDK sharedInstance] setNoticePushStatusWithStauts:enable  success:^{

} failure:^(NSError *error) {

}];
```
