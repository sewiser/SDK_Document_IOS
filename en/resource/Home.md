## Home management

After login, user shall use the `WiserSmartHomeManager to obtain` information of home list and initiate one home `WiserSmartHome` and attain details of a home and manage and control devices in the home.

### Callback of information in the home list

After the `WiserSmartHomeManagerDelegate` delegate protocol is realized, user can proceed operations in the home list change.

Objc:

```objc
#pragma mark - WiserSmartHomeManagerDelegate


// Add a home
- (void)homeManager:(WiserSmartHomeManager *)manager didAddHome:(WiserSmartHomeModel *)home {

}

// Delete a home
- (void)homeManager:(WiserSmartHomeManager *)manager didRemoveHome:(long long)homeId {

}

// The MQTT connection succeeds.
- (void)serviceConnectedSuccess {
    // Update the current home UI
}
```

Swift:

```swift
extension ViewController: WiserSmartHomeManagerDelegate {
    
    // Add a home
    func homeManager(_ manager: WiserSmartHomeManager!, didAddHome home: WiserSmartHomeModel!) {
        
    }
    
    // Delete a home
    func homeManager(_ manager: WiserSmartHomeManager!, didRemoveHome homeId: Int64) {
        
    }
    
    // The MQTT connection succeeds.
    func serviceConnectedSuccess() {
        // Update the current home UI
    }
    
}
```


### Obtain the home list.

Objc:

```objc
- (void)getHomeList {

	[self.homeManager getHomeListWithSuccess:^(NSArray<WiserSmartHomeModel *> *homes) {
        // home list
    } failure:^(NSError *error) {
        NSLog(@"get home list failure: %@", error);
    }];
}
```

Swift:

```swift
let homeManager: WiserSmartHomeManager = WiserSmartHomeManager()

func getHomeList() {
    homeManager.getHomeList(success: { (homes) in
        // home list
    }) { (error) in
        if let e = error {
            print("get home list failure: \(e)")
        }
    }
}
```

### Add home

Objc:

```objc
- (void)addHome {

    [self.homeManager addHomeWithName:@"you_home_name"
                          geoName:@"city_name"
                            rooms:@[@"room_name"]
                         latitude:lat
                        longitude:lon
                          success:^(double homeId) {

        NSLog(@"add home success");
    } failure:^(NSError *error) {
        NSLog(@"add home failure: %@", error);
    }];
}
```

Swift:

```swift
 func addHome() {
    homeManager.addHome(withName: "you_home_name", geoName: "city_name", rooms: ["room_name"], latitude: lat, longitude: lon, success: { (homeId) in
        print("add home success")
    }) { (error) in
        if let e = error {
            print("add home failure: \(e)")
        }
    }
}
```


## Home information management

Main function: it is used to obtain, change and dismiss a home. Obtain, add and delete member of a home. Add, dismiss and remove room.
The home ID needs to be used to initiate all WiserSmartHome classes related to all functions for home information management. Wrong home ID may cause initiation failure, and the nil will be returned.

### Callback of information change of home

After the `WiserSmartHomeDelegate` delegate protocol is realized, user can proceed operations in the home information change.

Objc:
```objc
- (void)initHome {
    self.home = [WiserSmartHome homeWithHomeId:homeId];
    self.home.delegate = self;
}

#pragma mark - WiserSmartHomeDelegate

//Update information of home, such as name.
- (void)homeDidUpdateInfo:(WiserSmartHome *)home {
    [self reload];
}

// Received change of shared device list.
- (void)homeDidUpdateSharedInfo:(WiserSmartHome *)home {
    [self reload];
}

// the delegate when a new room is added.
- (void)home:(WiserSmartHome *)home didAddRoom:(WiserSmartRoomModel *)room {
  	[self reload];
}

// the delegate when an existing room is removed.
- (void)home:(WiserSmartHome *)home didRemoveRoom:(long long)roomId {
  	[self reload];
}

// room information change, such as name.
- (void)home:(WiserSmartHome *)home roomInfoUpdate:(WiserSmartRoomModel *)room {
    [self reload];
}

// The change of relation between  room and devices and group.
- (void)home:(WiserSmartHome *)home roomRelationUpdate:(WiserSmartRoomModel *)room {
    [self reload];
}

//Add device
- (void)home:(WiserSmartHome *)home didAddDeivice:(WiserSmartDeviceModel *)device {
    [self reload];
}

//Remove Device
- (void)home:(WiserSmartHome *)home didRemoveDeivice:(NSString *)devId {
    [self reload];
}

//Update information of device, such as name.
- (void)home:(WiserSmartHome *)home deviceInfoUpdate:(WiserSmartDeviceModel *)device {
    [self reload];
}

// the delegate of device dps update.
- (void)home:(WiserSmartHome *)home device:(WiserSmartDeviceModel *)device dpsUpdate:(NSDictionary *)dps {
    [self reload];
}

// Add group.
- (void)home:(WiserSmartHome *)home didAddGroup:(WiserSmartGroupModel *)group {
    [self reload];
}

// Remove group.
- (void)home:(WiserSmartHome *)home didRemoveGroup:(NSString *)groupId {
    [self reload];
}

//Update information of group, such as name.
- (void)home:(WiserSmartHome *)home groupInfoUpdate:(WiserSmartGroupModel *)group {
    [self reload];
}

// the delegate of group dps update.
- (void)home:(WiserSmartHome *)home group:(WiserSmartGroupModel *)group dpsUpdate:(NSDictionary *)dps {
    [self reload];
}

// the delegate of warning information update
- (void)home:(WiserSmartHome *)home device:(WiserSmartDeviceModel *)device warningInfoUpdate:(NSDictionary *)warningInfo {
	//...  
}

// the delegate of device firmware upgrade status update
- (void)home:(WiserSmartHome *)home device:(WiserSmartDeviceModel *)device upgradeStatus:(WiserSmartDeviceUpgradeStatus)upgradeStatus {
  	//...
}
```
Swift:

```swift
var home: WiserSmartHome?

extension ViewController: WiserSmartHomeDelegate {
    
    func initHome() {
        home = WiserSmartHome(homeId: homeId)
        home?.delegate = self
    }
    
    // Update information of home, such as name.
    func homeDidUpdateInfo(_ home: WiserSmartHome!) {
//        reload()
    }

    // Received change of shared device list.
    func homeDidUpdateSharedInfo(_ home: WiserSmartHome!) {
        
    }
    
    // the delegate when a new room is added.
    func home(_ home: WiserSmartHome!, didAddRoom room: WiserSmartRoomModel!) {
          //...
    }

    // the delegate when an existing room is removed.
    func home(_ home: WiserSmartHome!, didRemoveRoom roomId: int32!) {
       //...
    }

    // room information change, such as name.
    func home(_ home: WiserSmartHome!, roomInfoUpdate room: WiserSmartRoomModel!) {
//        reload()/
    }
    
    // The change of relation between  room and devices and group.
    func home(_ home: WiserSmartHome!, roomRelationUpdate room: WiserSmartRoomModel!) {
        
    }
    
    // Add device
    func home(_ home: WiserSmartHome!, didAddDeivice device: WiserSmartDeviceModel!) {
        
    }
    
    // Remove Device
    func home(_ home: WiserSmartHome!, didRemoveDeivice devId: String!) {
        
    }
    
    // Update information of device, such as name.
    func home(_ home: WiserSmartHome!, deviceInfoUpdate device: WiserSmartDeviceModel!) {
        
    }
    
    // the delegate of device dps update.
    func home(_ home: WiserSmartHome!, device: WiserSmartDeviceModel!, dpsUpdate dps: [AnyHashable : Any]!) {
         //...
    }

    // Add group.
    func home(_ home: WiserSmartHome!, didAddGroup group: WiserSmartGroupModel!) {
        
    }
    
    // Remove group.
    func home(_ home: WiserSmartHome!, didRemoveGroup groupId: String!) {
        
    }
    
    // Update information of group, such as name.
    func home(_ home: WiserSmartHome!, groupInfoUpdate group: WiserSmartGroupModel!) {
        
    }

    // he delegate of group dps update.
    func home(_ home: WiserSmartHome!, group: WiserSmartGroupModel!, dpsUpdate dps: [AnyHashable : Any]!) {
        
    }

      // the delegate of warning information update
    func home(_ home: WiserSmartHome!, device: WiserSmartDeviceModel!, warningInfoUpdate warningInfo: [AnyHashable : Any]!) {
    	//...
    }
  
    //  the delegate of device firmware upgrade status update
    func home(_ home: WiserSmartHome!, device: WiserSmartDeviceModel!, upgradeStatus status WiserSmartDeviceUpgradeStatus) {
    	//....
    }
    
}
```

### Obtain information of home.

Objc:

```objc
- (void)getHomeDetailInfo {

	[self.home getHomeDetailWithSuccess:^(WiserSmartHomeModel *homeModel) {
        // homeModel home information
        NSLog(@"get home detail success");
    } failure:^(NSError *error) {
        NSLog(@"get home detail failure: %@", error);
    }];
}
```

Swift:

```swift
func getHomeDetailInfo() {
    home?.getDetailWithSuccess({ (homeModel) in
        print("get home detail success")
    }, failure: { (error) in
        if let e = error {
            print("get home detail failure: \(e)")
        }
    })
}
```

### Update home information

Objc:

```objc
- (void)updateHomeInfo {
    [self.home updateHomeInfoWithName:@"new_home_name" geoName:@"city_name" latitude:lat longitude:lon success:^{
        NSLog(@"update home info success");
    } failure:^(NSError *error) {
        NSLog(@"update home info failure: %@", error);
    }];
}

```

Swift:

```swift
func updateHomeInfo() {
    home?.updateInfo(withName: "new_home_name", geoName: "city_name", latitude: lat, longitude: lon, success: {
        print("update home info success")
    }, failure: { (error) in
        if let e = error {
            print("update home info failure: \(e)")
        }
    })
}
```

###Sort device and groups 

Objc:

```objc
// orderList: [@{@"bizId": @"XXX", @"bizType": @"XXX"},@{@"bizId": @"XXX",@"bizType": @"XXX"}] bizId is devId or groupId, device's bizType = @"6" group's bizType = @"5"
- (void)sortDeviceOrGroupWithOrderList:(NSArray<NSDictionary *> *)orderList {
	[self.home sortDeviceOrGroupWithOrderList:orderList success:^ {
        NSLog(@"sort device or group success");
    } failure:^(NSError *error) {
        NSLog(@"sort device or group failure: %@", error);
    }];
}
```

Swift:

```swift
func sortDeviceOrGroup(withOrderList orderList: [[AnyHashable : Any]]?) {
    home.sortDeviceOrGroup(withOrderList: orderList, success: {
        print("sort device or group success")
    }, failure: { error in
        if let error = error {
            print("sort device or group failure: \(error)")
        }
    })
}
```

### Dismiss home

Objc:

```objc
- (void)dismissHome {

	[self.home dismissHomeWithSuccess:^() {
        NSLog(@"dismiss home success");
    } failure:^(NSError *error) {
        NSLog(@"dismiss home failure: %@", error);
    }];
}
```

Swift:

```swift
func dismissHome() {
    home?.dismiss(success: {
        print("dismiss home success")
    }, failure: { (error) in
        if let e = error {
            print("dismiss home failure: \(e)")
        }
    })
}
```

### Add room

Objc:

```objc
- (void)addHomeRoom {
    [self.home addHomeRoomWithName:@"room_name" success:^{
        NSLog(@"add room success");
    } failure:^(NSError *error) {
        NSLog(@"add room failure: %@", error);
    }];
}
```

Swift:

```swift
func addHomeRoom() {
    home?.addRoom(withName: "room_name", success: {
        print("add room success")
    }, failure: { (error) in
        if let e = error {
            print("add room failure: \(e)")
        }
    })
}
```

### Remove room

Objc:

```objc
- (void)removeHomeRoom {
    [self.home removeHomeRoomWithRoomId:roomId success:^{
        NSLog(@"remove room success");
    } failure:^(NSError *error) {
        NSLog(@"remove room failure: %@", error);
    }];
}
```

Swift:

```swift
func removeHomeRoom() {
    home?.removeRoom(withRoomId: roomId, success: {
        print("remove room success")
    }, failure: { (error) in
        if let e = error {
            print("remove room failure: \(e)")
        }
    })
}
```

### Sort room

Objc:

```objc
- (void)sortHomeRoom {
    [self.home sortRoomList:(NSArray<WiserSmartRoomModel *> *) success:^{
        NSLog(@"sort room success");
    } failure:^(NSError *error) {
        NSLog(@"sort room failure: %@", error);
    }];
}
```

Swift:

```swift
func sortHomeRoom() {
    home?.sortRoomList([WiserSmartRoomModel]!, success: {
        print("sort room success")
    }, failure: { (error) in
        if let e = error {
            print("sort room failure: \(e)")
        }
    })
}
```
### Home member management

All functions related to home member management correspond to`WiserSmartHome` and `WiserSmartHomeMember`classes, member role type is `TYHomeRoleType`

#### Add Home Member

Objc:

```objc
- (void)addShare {
  //	_home = [WiserSmartHome homeWithHomeId:homeId];
    [_home addHomeMemberWithName:@"name" headPic:image countryCode:@"your_country_code" userAccount:@"account" role:TYHomeRoleType_Admin success:^(NSDictionary *dict) {
        NSLog(@"addNewMember success");
    } failure:^(NSError *error) {
        NSLog(@"addNewMember failure: %@", error);
    }];
}
```

Swift:

```swift
func addShare() {
    home?.addHomeMember(withName:@"name", headPic:image, countryCode: "your_country_code", account: "account", role: TYHomeRoleType_Admin, success: {
        print("addNewMember success")
    }, failure: { (error) in
        if let e = error {
            print("addNewMember failure: \(e)")
        }
    })
}
```



#### Get a list of Home members

Objc:

```objc
- (void)initMemberList {
  //	_home = [WiserSmartHome homeWithHomeId:homeId];
    [_home getHomeMemberListWithSuccess:^(NSArray<WiserSmartHomeMemberModel *> *memberList) {
        NSLog(@"getMemberList success: %@", memberList);
    } failure:^(NSError *error) {
        NSLog(@"getMemberList failure");
    }];
}
```

Swift:

```swift
func initMemberList() {
    home.getHomeMemberList(withSuccess: { memberList in
        print("getMemberList success: \(memberList)")
    }, failure: { (error) in
        if let e = error {
            print("getMemberList failure: \(e)")
        }
    })
}
```



#### Modify the home member's comment name and whether it's an administrator

Objc:

```objc
- (void)modifyMemberName:(WiserSmartHomeMemberModel *)memberModel name:(NSString *)name {
	// self.homeMember = [[WiserSmartHomeMember alloc] init];

	WiserSmartHomeMemberRequestModel *requestModel = [[WiserSmartHomeMemberRequestModel alloc] init];
	[self.homeMember updateHomeMemberInfoWithMemberRequestModel:requestModel  success:^{
        NSLog(@"modifyMemberName success");
    } failure:^(NSError *error) {
        NSLog(@"modifyMemberName failure: %@", error);
    }];
}
```

Swift:

```swift
func modifyMember(_ memberModel: WiserSmartHomeMemberModel, name: String) {
    homeMember?.updateHomeMemberName(withMemberRequestModel:requestModel, success: {
        print("modifyMemberName success")
    }, failure: { (error) in
        if let e = error {
            print("modifyMemberName failure: \(e)")
        }
    })
}
```



#### Delete home members

Objc: 

```objc
- (void)removeMember:(WiserSmartHomeMemberModel *)memberModel {
	// self.homeMember = [[WiserSmartHomeMember alloc] init];

	[self.homeMember removeHomeMemberWithMemberId:memberModel.memberId success:^{
        NSLog(@"removeMember success");
    } failure:^(NSError *error) {
        NSLog(@"removeMember failure: %@", error);
    }];
}
```

Swift:

```swift
func removeMember(_ memberModel: WiserSmartHomeMemberModel) {
    homeMember?.removeHomeMember(withMemberId: memberModel.memberId, success: {
        print("removeMember success")
    }, failure: { (error) in
        if let e = error {
            print("removeMember failure: \(e)")
        }
    })
}
```



####  Accept or reject home invitations

Whether the member accepts the home‘s invitation corresponds to the dealStatus in WiserSmartHomeModel, The invited state will correspond to TYHomeStatusPending、TYHomeStatusAccept、TYHomeStatusReject.

Objc:

```objc
- (void)initMemberList {
  //	_home = [WiserSmartHome homeWithHomeId:homeId];
  	[_home joinFamilyWithAccept:YES success:^(BOOL result) {
        NSLog(@"join success");
    } failure:^(NSError *error) {
        NSLog(@"join failure");
    }];
}
```



Swift:

```swift
func initMemberList(_ memberModel: WiserSmartHomeMemberModel) {
    home?.joinFamilyWithAccept(true, success: { (result: Bool) in
        print("join success")
    }, failure: { (error) in
        if let e = error {
            print("join failure: \(e)")
        }
    })
}
```



## Room information management

The roomId needs to be used to initiate all `WiserSmartRoom` classes related to all functions for room information management. Wrong roomId may cause initiation failure, and the `nil` will be returned.

### Update room name

Objc:

```objc
- (void)updateRoomName {
    [self.room updateRoomName:@"new_room_name" success:^{
        NSLog(@"update room name success");
    } failure:^(NSError *error) {
        NSLog(@"update room name failure: %@", error);
    }];
}
```

Swift:

```swift
func updateRoomName() {
    room?.updateName("new_room_name", success: {
        print("update room name success")
    }, failure: { (error) in
        if let e = error {
            print("update room name failure: \(e)")
        }
    })
}
```

### Add device to a room

Objc:

```objc
- (void)addDevice {
    [self.room addDeviceWithDeviceId:@"devId" success:^{
        NSLog(@"add device to room success");
    } failure:^(NSError *error) {
        NSLog(@"add device to room failure: %@", error);
    }];
}
```

Swift:

```swift
func addDevice() {
    room?.addDevice(withDeviceId: "your_devId", success: {
        print("add device to room success")
    }, failure: { (error) in
        if let e = error {
            print("add device to room failure: \(e)")
        }
    })
}
```

### Remove device from a room

Objc:

```objc
- (void)removeDevice {
    [self.room removeDeviceWithDeviceId:@"devId" success:^{
        NSLog(@"remove device from room success");
    } failure:^(NSError *error) {
        NSLog(@"remove device from room failure: %@", error);
    }];
}
```

Swift:

```swift
func removeDevice() {
    room?.removeDevice(withDeviceId: "your_devId", success: {
        print("remove device from room success")
    }, failure: { (error) in
        if let e = error {
            print("remove device from room failure: \(e)")
        }
    })
}
```

### Add group in a room

Objc:

```objc
- (void)addGroup {
    [self.room addGroupWithGroupId:@"groupId" success:^{
        NSLog(@"add group to room success");
    } failure:^(NSError *error) {
        NSLog(@"add group to room failure: %@", error);
    }];
}
```

Swift:

```swift
func addGroup() {
    room?.addGroup(withGroupId: "your_groupId", success: {
        print("add group to room success")
    }, failure: { (error) in
        if let e = error {
            print("add group to room failure: \(e)")
        }
    })
}
```

### Remove group in a room

Objc:

```objc
- (void)removeGroup {
    [self.room removeGroupWithGroupId:@"groupId" success:^{
        NSLog(@"remove group from room success");
    } failure:^(NSError *error) {
        NSLog(@"remove group from room failure: %@", error);
    }];
}
```

Swift:

```swift
func removeGroup() {
    room?.removeGroup(withDeviceId: "your_devId", success: {
        print("remove device from room success")
    }, failure: { (error) in
        if let e = error {
            print("remove device from room failure: \(e)")
        }
    })
}
```

### Change relation between room and group and devices in batches.

Objc:

```objc
- (void)saveBatchRoomRelation {
    [self.room saveBatchRoomRelationWithDeviceGroupList:(NSArray <NSString *> *)deviceGroupList success:^{
        NSLog(@"save batch room relation success");
    } failure:^(NSError *error) {
        NSLog(@"save batch room relation failure: %@", error);
    }];
}
```

Swift:

```swift
func saveBatchRoomRelation() {
    room?.saveBatchRoomRelation(withDeviceGroupList: [String]!, success: {
        print("save batch room relation success")
    }, failure: { (error) in
        if let e = error {
            print("save batch room relation failure: \(e)")
        }
    })
}
```

