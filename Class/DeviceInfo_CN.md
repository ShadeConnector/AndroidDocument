# 设备类/网关类

### 1.属性

| 属性 | 说明 |
| ------ | ------ |
| mac | 设备Mac地址，标识设备的唯一性 |
| deviceAlias | 设备名称 |
| deviceLogo | 设备个性化图片url |
| sharedBy | 设备分享者账户，isShared为YES有效 |
| isShared | 设备是否是他人分享得到 |
| battery | 设备电池电量(对锂电池电机有效) |
| modelCode | 设备模板Code |
| deviceSignCode | 设备特征码 |
| serialNo | 设备序列号 |
| status | 设备状态(1:激活 2:冻结) |
| deviceOnline | 设备在线标识 |
| deviceData | 设备数据点数据 |
| fwVersion | 设备固件(对单双向设备无效) |
| isCorTimers | 设备是否已关联添加了定时器 |
| deviceType | 设备类型 |
| curatinType | 窗帘类型 (对单双向设备有效)|
| ssid | 设备所连接网络的SSID，仅对Wifi设备有效 |
| order | 设备所在位置|
| orderInRoom | 设备所在房间信息 |




### 2.方法

* 获取设备对象列表

```
id3Sdk.getDevice(device?.mac)

参数: mac 设备mac
返回: 设备对象列表                
```

* 设备控制

```
doRequestDeviceControl(String mac, String deviceType, ArrayList<DataCmd> cmdList)

参数: mac 设备mac
	  deviceType 设备类型
	  cmdList 设备数据集合
返回: 回调控制数据下发结果
```

* 绑定设备到指定Home下

```
 doRequestBindDeviceToHome(String homeCode, String mac, String deviceType) 

参数: homeCode Home识别码
	  mac 设备mac
	  deviceType 设备类型
返回: 绑定结果

```

* 更新设备到指定区域下

```
doRequestDeviceUpdateInZone(String mac, String deviceType, String deviceAlias, String logo, String zoneCode)

参数: 	mac 设备mac
	 	deviceType 设备类型
		deviceAlias 设备名字
		logo 设备图标
		zoneCode 区域识别码
返回: 绑定结果

```

* 绑定设备到指定房间下

```
doRequestBindDeviceToRoom(String roomCode, String mac, String deviceType) 

参数: 	roomCode 房间识别码
		mac 设备mac
	 	deviceType 设备类型
返回: 绑定结果

```

* 删除设备

```
 doRequestDeviceDelete(Device device) 

参数: device Device类
返回: 回调删除结果

```

* 修改设备详情

```
doRequestDeviceUpdateInRoom(String mac, String deviceType, String deviceAlias, String logo, String romeCode)

参数: 	mac 设备mac
		deviceType 设备类型
		deviceAlias 设备名称
		logo 设备个性化图标
      	roomCode 设备所属房间	
返回: 回调修改结果

```

* 移动设备到Home层级下

```
- (void)moveDeviceToHomeWithHomeCode:(NSString*)homeCode
                            completion:(BridgeBlock)completion

参数: homeCode 设备待移动到的Home识别码
返回: 回调移动结果

```

* 校验设备名称是否已经存在

```
device.deviceAlias == name

参数: deviceName 设备名称
返回: YES-存在  NO-不存在

```

* 获取指定设备最新版本号(仅对WiFi设备有效)

```
doRequestDeviceVersion(String productLineCode, String deviceType)

参数: 	productLineCode  ""
		deviceType 设备类型
返回: 回调设备版本信息

```


* 设备升级

```
doRequestDeviceVersionUpdate(String mac, String deviceType, String versionCode)

参数: 	mac 设备mac
		deviceType 设备类型
		versionCode 版本唯一标识
返回: 回调升级命令下发结果，升级进度请关注BridgeManagerDelegate

```

* 设备行程值设置保存

```
-(void)savePointWithData:(NSDictionary*)data
              completion:(BridgeBlock) completion
参数: data 数据点控制数据
返回: 回调设置结果

```

* WiFi设备配网，更新网络

```
doRequestDeviceWifiSet(String wifi, String password, String mac, String deviceType)
参数: wifi 需要连接网络的名字
      password 需要连接网络的密码
      mac 设备mac
      deviceType 所配置设备类型
返回: 回调配置结果。如若成功，则会回调配网成功的设备对象

```


* 获取设备关联的定时器列表

```
id3Sdk.getDeviceTimerList(device?.mac))
参数: mac 设备mac
返回: 定时器列表

```
