# 定时器类

### 1.常量值
* 定时器类型 

* 定时器循环方式 

| 属性 | 说明 |
| ------ | ------ |
| REPEAT_MONTH | 按月循环 |
| REPEAT_WEEK | 按周循环 |
| REPEAT_ONCE | 不循环 |

* 定时器时间值类型 

| 属性 | 说明 |
| ------ | ------ |
| SUNSET | 日落 |
| SUNRISE | 日出 |

### 2.属性

| 属性 | 说明 |
| ------ | ------ |
| timerCode | 定时器识别码,标识定时器的唯一性 |
| timerAlias | 定时器名称 |
| logoValue | 定时器个性化图标索引值 |
| timeOffset | 定时器是否使能 |
| cycleType | 定时器循环方式 |
| timeZone | 时区。例如Asia/Shanghai|
| timeType | 定时器状态 |
| timeOffset | 定时器触发时间偏移量(±60min) 仅对日出日落类型定时器有效|
| order | 定时器索引值 |
| rules | 定时器控制的设备动作，仅当timer的rule的Type为Device有效|
| rules | 定时器控制的场景，仅当timerrule的的Type为Scene有效|
| repeat | 定时器重复状态 |
| areaCode | 定时器所在的Home|
| days | 定时器重复天数 |
| time | 定时器时间 |



### 3.方法

* 获取定时器对象

```
Timer getTimer(String timerCode）

参数: timerCode 定时器识别码
返回: 定时器对象详情

```

* 获取指定Home下的定时器列表

```
getTimerList()

参数: 无
返回: 回调定时器列表

```

* 删除定时器

```
doRequestDeleteTimer(String timerCode)

参数: timerCode 定时器识别码
返回: 回调删除结果

```


* 新增或者修改定时器信息(直接对成员属性修改之后，调用此方法)

```
doRequestAddOrUpdateTimer(Timer timer)

参数: timer Timer类
返回: 回调修改结果

```

* 修改定时器的使能状态

```
doRequestChangeTimerStatus(String timerCode, int timerStatus)

参数: timerCode 定时器识别码
	  timerStatus 1-open 0-close
返回: 回调修改结果

```