读取设备方法

### 方法

*  读取行程值

```
  Cmd.DataCmd dataCmd = device.getCmd(String name)
        int current = dataCmd.data 

参数: cmdName
返回: 回调设备最新行程值

```

* 读取角度值

```
 Cmd.DataCmd dataCmd = device.getCmd(String name)
	int current = dataCmd.data 
参数: cmdName
返回: 回调设备最新角度值

```

* 读取设备最新信息

```
 
didDeviceDataReceive(String mac, String deviceType,
                                     ArrayList<Cmd.DataCmd<Object>> arrayList)

参数: 无
返回: 回调设备最新对象详情

```
