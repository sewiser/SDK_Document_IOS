## Device data channel

Data channel mainly used for big data real-time upload such as sweeper map data, See `WiserSmartSingleTransfer` class.

### Initialize

```objective-c
WiserSmartSingleTransfer *transfer = [[WiserSmartSingleTransfer alloc] init];
// Set delegate. status changed or data received event will be received through callback.
transfer.delegate = #<WiserSmartTransferDelegateInstance>;
```

### Start connecting data channel

```objective-c
[self.transfer startConnect];
```


### Close data channel

```objective-c
[self.transfer close];
```


### Subscribe device

```objective-c
[self.transfer subscribeDeviceWithDevId:#<DevId>];
```

> Device can't be subscribed before channel connected. Please subscribe device in the channel status callback method.


### Unsubscribe device

```objective-c
[self.transfer unsubscribeDeviceWithDevId:#<DevId>];
```


### Get data channel connect status

```objective-c
BOOL isConnected = [self.transfer isConnected];
```



### WiserSmartTransferDelegate

```objective-c
/**
 Connect status changed

 When data channel connected/disconnected, this method will be called.

 @param transfer
 @param state Current state，`WiserSmartTransferState`
 */
- (void)transfer:(WiserSmartSingleTransfer *)transfer didUpdateConnectState:(WiserSmartTransferState)state;


/**
 New data received

 @param transfer
 @param devId Device id
 @param data Received data
 */
- (void)transfer:(WiserSmartSingleTransfer *)transfer didReciveDataWithDevId:(NSString *)devId data:(NSData *)data;

```
