# 场景类

### 1.属性

| 属性 | 说明 |
| ------ | ------ |
| sceneCode | 场景识别码，标识场景的唯一性 |
| sceneName | 场景名称 |
| sceneLogo | 场景个性化图片url |
| order | 场景个性化图标索引值|
| areaCode | 场景所在Home |
| rules | 操作类 |



### 2.方法

* 获取场景对象

```
getScene(String sceneCode)

参数: sceneCode 场景识别码
返回: 场景对象详情

```

* 获取场景列表

```
getSceneList（）

参数: 无
返回: 回调场景列表

```

* 对当前房间下的所有设备列表排序

```
orderSceneList(ArrayList<Room> SceneList)

参数: SceneList 排序后的设备列表
返回: 无

```

* 校验场景名称是否已经存在

```
scene.sceneName == name

参数: sceneName 场景名称
返回: YES-存在 NO-不存在

```

* 删除场景

```
doRequestDeleteScene(String sceneCode)

参数: sceneCode 场景识别码
返回: 回调删除结果

```


* 修改场景信息

```
doRequestUpdateSceneWithDevices(String sceneCode, String sceneName, String logo, String homeCode, ArrayList<Rule> ruleList)

参数: sceneCode 场景识别码
	  sceneName 场景名称称
      logo 场景图片数据(选填)
      homeCode home识别码
	  ruleList 操作类数据列表
返回: 回调修改结果

```

* 获取场景控制信息列表

```
scene.getSceneRuleList()

参数: 无
返回: 控制信息列表

```

* 场景执行

```
doRequestTriggerScene(String sceneCode) 

参数: sceneCode 场景识别码
返回: 回调控制结果

```

* 获取场景关联的定时器列表

```
getSceneTimerList(String sceneCode)

参数: sceneCode 场景识别码
返回: 定时器列表

```
