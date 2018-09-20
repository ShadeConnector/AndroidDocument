# 区域类

### 1.属性

| 属性 | 说明 |
| ------ | ------ |
| code | 区域识别码，标识区域的唯一性 |
| name | 区域名称 |
| homeCode | 区域所在Home的识别码 |
| logo | 区域个性化图片url |
| isDefault | 区域是否是默认生成的,YES时则该区域不允许删除 |
| isShared | 区域是否是他人分享得到 |
| sharedBy | 区域分享者账户，isShared为YES有效 |
| devices | 区域下的设备列表 |

### 2.方法

* 获取区域对象

```
getZone(String zoneCode)

参数: zoneCode 区域识别码,唯一标识
返回: 区域对象详情

```

* 获取区域下房间列表

```
 getZoneListInHome(String homeCode)

参数: homeCode Home唯一标识
返回: 房间列表

```

* 删除区域

```
 doRequestDeleteZone(String zoneCode)

参数: zoneCode 区域识别码,唯一标识
返回: 回调删除结果

```

* 更新区域信息

```
doRequestUpdateZone(String zoneCode, String name, String logo)

参数: zoneCode 区域识别码,唯一标识
      name 区域名称
      logo 区域个性化图片数据
返回: 回调修改结果

```

* 当前区域下添加房间

```
doRequestAddRoom(String name, String logo, String zoneCode)

参数: name 房间名称
      logo 房间个性化图片(选填)
      zoneCode 区域识别码,唯一标识
返回: 回调添加结果

```
