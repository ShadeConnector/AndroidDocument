# Home类

### 1.属性

| 属性 | 说明 |
| ------ | ------ |
| Code | Home识别码,标识Home的唯一性 |
| Name | Home名称 |
| Logo | Home个性化图片url |
| devices | Home所在设备列表 |
| isDefault | Home是否是默认生成的,YES时则该home不允许删除 |
| isShared | Home是否是他人分享得到 |
| sharedBy | Home分享者账户，isShared为YES有效 |
| lat | Home所在的纬度 |
| lng | Home所在的经度 |


### 2.方法
##### 2.1 Home相关操作
* 获取Home唯一标识

```
  public String getCode() {
        return this.code;
    }

参数: 无
返回: Home的唯一标识

```

* 获取账号下所有Home设备列表

```
public ArrayList<Device> getDevices() {
        return this.devices;
    }

参数: 无
返回: Home下设备列表

```

* 获取home列表(默认排序方式)

```
getHomeList

参数: 无
返回: 回调Home列表

```

* 添加Home

```
doRequestAddHome(String name, String logo, double lng, double lng)

参数: name Home名称
      logo home个性化图片(选填)
      lng home所在位置经度
      lat home所在位置纬度
返回: 回调Home添加结果

```

* 删除Home

```
doRequestDeleteHome(String homeCode)

参数: homeCode home唯一标识code
返回: 回调删除结果

```


* 修改Home信息

```
doRequestUpdateHome(String code, String name, String logo, double lng, double lat)

参数: code Home唯一标识code
	  name Home名称
      logo home个性化图片
      lng home所在位置经度
      lat home所在位置纬度
返回: 回调修改结果

```

  
##### 2.2 区域相关操作

* 在当前Home下添加区域  


```
 doRequestAddZone(String name, String logo, String homeCode)

参数: name 区域名称
      logo 区域个性化图片
      homeCode home唯一标识code
返回: 回调添加结果

```

* 获取当前Home下的所有缓存的区域列表

```
getZoneListInHome(String homeCode)

参数:  homeCode home唯一标识code
返回: 区域列表

```

##### 2.3 房间相关操作

* 获取当前home里面的所有房间列表

```
getRoomListInHome（）

参数: 无
返回: 回调房间列表

```



* 对当前Home下房间进行排序

```
orderRoomList(ArrayList<Room> list)

参数: roomList 排序后的房间列表
返回: 无

```

##### 2.4 设备相关操作

* 获取当前Home下所有缓存的设备

```
//首先获取房间列表
 val roomList = id3Sdk.getRoomListInHome()
//遍历房间列表
 for (room in roomList) {
            val deviceListInRoom = id3Sdk.getDeviceListInRoom(room.code)}
参数: 无
返回: 设备

```




* 对当前Home下设备进行排序

```
orderRoomDeviceList(ArrayList<Device> list)

参数: deviceList 排序后的设备列表
返回: 无

```

##### 2.5 场景相关操作

* 获取当前Home下所有场景列表

```
id3Sdk.getSceneList（）

参数: 无
返回: 回调场景列表

```


* 对当前Home下的场景排序

```
orderSceneList(ArrayList<Scene> list)

参数: list 排序后的场景列表
返回: 无

```

* 场景添加设备

```
doRequestUpdateSceneWithDevices(String sceneCode, String sceneName, String logo, String homeCode, ArrayList<Rule> ruleList)

参数: sceneCode 场景code
	  sceneName 场景名称
      logo 场景个性化图片数据 
      homeCode home唯一标识code
      ruleList 场景控制的设备动作列表
返回: 回调添加结果

```

* 当前Home下添加场景并给场景添加定时器

```
doRequestAddSceneWithDevicesAndTimers(String sceneName, String logo, String homeCode, ArrayList<Rule> ruleList, ArrayList<Timer> timerList)

参数: sceneName 场景名称
     logo 场景个性化图片数据 (选填。如设置，则sceneIcon失效)
     homeCode home唯一标识code
     ruleList 场景控制的设备动作列表
     timerList 场景关联的定时器列表
返回: 回调添加结果

```
##### 2.6 定时器相关操作
* 新增定时器

```
doRequestAddOrUpdateTimer(Timer timer)

参数: timer 待添加的定时器对象，注意action属性和scene属性不能同时设置
返回: 回调添加结果

```

* 获取当前Home下所有定时器列表

```
id3Sdk.getTimerList（）

参数:无
返回: 回调定时器列表

```



* 对当前Home的定时器排序

```
orderTimerList(ArrayList<Timer> timerList)

参数: timerList 排序后的定时器列表
返回: 无

```

##### 2.7 分享功能相关操作

* 获取当前Home已分享的账户列表

```
doRequestGetHomeAuthorized(String homeCode)

参数: homecode Home唯一标识code
返回: 回调分享账号列表

```

* 将当前Home分享给指定账户

```
doRequestShareHomeAuthority(String destAccount, ArrayList<Home> homeList)
参数: destAccount 账户名
	  homelist home列表
返回: 回调分享结果

```

* 取消当前Home对指定用户的分享

```
doRequestCancelRoomAuthority(String destAccount, ArrayList<Home> homeList)

参数: destAccount email
      homeList home列表
返回: 回调取消分享结果

```

##### 2.8 网关相关操作

* 获取当前Home下的网关列表

```
getHostList(String homeCode)

参数: homecode Home唯一标识code
返回: 回调网关列表

```





