# SDK管理

### 1.方法
* SDK生产环境初始化方法

```
ID3Sdk.getInstance().init(this)

参数: context
返回: 无

```


* 用户登录

```
doRequestRegist(email,pass)

参数: email 用户名
      pass 密码
返回: 回调登录结果

```

* 用户登出

```
 doRequestLogout(String loginName)

参数: loginName 用户名
返回: 无

```

* 用户是否已登陆

```
isLoginedIn()

参数: 无
返回: Yes-已登陆 NO-未登陆

```

* 上传日志

```
 doRequestUploadLog()

参数: 无
返回: 回调上报结果

```

### 2.代理
* 通知设备状态变化的代理

```
didDeviceOffline(String mac, String deviceType)

参数: mac 设备mac码
	 deviceType 设备类型

```

* 设备详情

```
didDeviceStatusReceive(mac: String?, deviceType: String?,
                                        cmdList: java.util.ArrayList<Cmd.DataCmd<Any>>?)

参数:  mac 设备mac码
	 deviceType 设备类型
	cmdList 所有在线状态发生变化的设备列表

```


* 网络连接

```
didMqConnectionStateChanged(isConnect: Boolean)

参数: isConnect  网络连接的状态

```


* 登录Token失效,App需要退出重新登录

```
didNeedReLogin()

参数: 无

```
