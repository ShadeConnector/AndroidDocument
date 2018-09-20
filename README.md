# Connector IOS SDK 说明文档

### 1. 接入必读
* 及时关注最新SDK发布
* 智能网关[设备指示灯状态](Other/PilotLight_CN.md)

### 2. 简介
本文档用于说明Connecotor开放平台SDK iOS版本接口之间的关系及接口调用顺序,对开放平台SDK iOS版本主要流程都有详细说明和代码示例。主要有名称解释、项目环境、权限配置和主要流程介绍。

### 3. 名称解释
| 名词 | 说明 |
| ------ |-------|
| 智能网关 |  | 
| 双向电机 |  |
| 单向电机 |  |
| WiFi电机 |  |
| 场景 |  |
| 定时器 |  |
| [成品帘类型](CurtainType/CurtainType_CN.md) |  |
| [设备数据点](DataPoint/DataPoint_CN.md) |  |

### 4. 项目环境配置
* 创建新的XCode工程，然后导入Bridge.framework:
* sdk倒入libs文件夹,如下图所示
![](Pic/sdk.png)
* Build gradle添加依赖。如下图所示
![](Pic/build.png)
* 配置完成

### 5. 主要流程
##### 5.1 初始化流程
* 在Application中初始化SDK。参考代码 

```
 ID3Sdk.getInstance().init(this)
```

##### 5.2 检查网络是否连接
* 参考代码

```
 id3Sdk.doRequestSyncData().success {
        }.error { t ->
            this?.toast(t?.message)
            if ("Http connection exception".equals(t?.message)) {
               //提示错误信息
            }
```

##### 5.2.1 选择location。默认为Myhouse，可不选
* 参考代码

```
	//获取location列表
	id3Sdk.homeList
 	//选择
	id3Sdk.setCurrentHome(item?.code)
```

##### 5.3 网关、WiFi设备配网配网流程
* 将[网关](Class/DeviceInfo_CN.md)或WiFi[设备](Class/DeviceInfo_CN.md)处于配网状态
* 手机连上[网关](Class/DeviceInfo_CN.md)或WiFi[设备](Class/DeviceInfo_CN.md) AP热点
* 调用[网关](Class/DeviceInfo_CN.md)或WiFi[设备](Class/DeviceInfo_CN.md)配网API，将[网关](Class/DeviceInfo_CN.md)或WiFi[设备](Class/DeviceInfo_CN.md)配网添加到系统中。参考代码

```
//(String) wifi, (String) password, (String) deviceType) 
 id3Sdk.doRequestDeviceApConfig(wifi,password,deviceType)
```


* 将上一步配网得到的[网关](Class/DeviceInfo_CN.md)，绑定到指定Hoom下。参考方法

```
//String mac, String deviceType, String deviceAlias,
//String logo, String homeCode
id3Sdk.doRequestDeviceUpdateInHome(hub?.mac, 	hub?.deviceType, name,
                        null, homeCode).success {
                    //success
                }.error { e ->
                   //e?.message 
                }
```




* [网关](Class/DeviceInfo_CN.md)或WiFi[设备](Class/DeviceInfo_CN.md)添加完成，接下来您可以给[网关](Class/DeviceInfo_CN.md)或WiFi[设备](Class/DeviceInfo_CN.md)做些个性化设置，例如修改名称。


##### 5.3 单向、双向电机配对流程

* 第一步[设备](Class/DeviceInfo_CN.md)绑定[网关类](Class/DeviceInfo_CN)配对设备接口。参考代码

```
//String parentMac, String parentType, String childMac, String childType, int cmdDataType
id3Sdk.doRequestDeviceAddChild(hostDevice.mac, hostDevice.deviceType, "",
                Constants.DeviceType.SubSet,
                cmdDataType).success { }.error {  }
```

* 第二步将配对成功的[设备](Class/DeviceInfo_CN.md)绑定到房间或者Home下，参考代码
* 
//String mac, String deviceType, String deviceAlias, String logo, String romeCode
```
id3Sdk.doRequestDeviceUpdateInRoom(device?.mac, device?.deviceType,
                name, device?.deviceLogo,
                room?.code).success {
            //success
        }.error { e ->
            //e?.message
        }
```

//默认都绑到home下。防止在setting页由于异常没有添加到room导致找不到该设备的情况
String homeCode, String mac, String deviceType


        id3Sdk.doRequestBindDeviceToHome(id3Sdk.currentHome?.code, mac,
                deviceType).success {}.error {}


* [设备](Class/DeviceInfo_CN.md)添加完成，接下来您可以给[设备](Class/DeviceInfo_CN.md)做些个性化设置，例如修改名称。

##### 5.4 控制流程

* 第一步,根据[数据点文档](DataPoint/DataPoint_CN.md)，组设备控制命令。以双向电机为例,开、关、停止、调行程到50%、调角度到90°数据点分别为

```
	//开   
ArrayList<DataCmd> cmdList = 
arrayListOf( Cmd.Factory.createCmd("operation", 1))                   
```

```
//关
ArrayList<DataCmd> cmdList = 
arrayListOf( Cmd.Factory.createCmd("operation", 0))                  
```

```
//停止
ArrayList<DataCmd> cmdList = 
arrayListOf( Cmd.Factory.createCmd("operation", 2))                 
```

```
//调行程到50%
ArrayList<DataCmd> cmdList = 
arrayListOf( Cmd.Factory.createCmd("targetPosition", 50))               
```

```
//调角度到90°
ArrayList<DataCmd> cmdList = 
arrayListOf( Cmd.Factory.createCmd("targetPosition", 90))                
```


* 第二步,将上一步组好的数据点数据通过[设备](Class/DeviceInfo_CN.md)控制接口下发

```
	//String mac, String deviceType, ArrayList<DataCmd> cmdList
  id3Sdk.doRequestDeviceExecuteInLan(device?.mac, 	device?.deviceType, cmdList)                      
```

* 第三步,设备数据点数据下发成功之后，设备会按照数据点设置运行，运行成功之后。设备会上报设备最新数据点数据信息。

##### 5.5 设备信息(属性或数据点)更新上报

[设备](Class/DeviceInfo_CN.md)的数据点或属性发生变化以后，SDK会通过[SDK管理类](Class/BridgeManager_CN.md)代理方法回调设备最新信息。方法为

```
//String mac,String deviceType,ArrayList<Cmd.DataCmd<Any>> cmdList
- (void)didDeviceDataReceive(mac: String?, deviceType: String?,
                                      cmdList: ArrayList<Cmd.DataCmd<Any>>?)               
```

### 6. API DOC
#####  6.1 [类族](Class/Class_CN.md)
#####  6.2 [错误码](ErrorCode/ErrorCode_CN.md)
#####  6.3 [其他常量](Constant/Constant_CN.md)

### 7. App下载
* [AppStore](https://itunes.apple.com/cn/app/connector/id1344058317?mt=8)

![](Pic/AppStore.png)


* [GooglePlay](https://play.google.com/store/apps/details?id=com.smarthome.app.connector)

![](Pic/GooglePlay.png)


### 8. 技术支持
* 邮件: <smarthome.app.developer@gmail.com>
* Skype: <549819728@qq.com>
* 微信: wt_870529
