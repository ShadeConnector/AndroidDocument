# 用户类

### 1.属性

| 属性 | 说明 |
| ------ | ------ |
| userCode | 用户识别码，标识用户的唯一性 |
| email | 用户邮箱 |
| mobileNo | 用户手机号 |
| nickName | 用户呢称 |
| logo | 用户头像url |
| sex | 性别 |
| realName | 用户真实姓名 |
| birthday | 用户生日 |
| location | 用户联系地址 |
| securityNum | 用户身份证号码 |
| remark | 用户备注 |
| accessToken | 访问令牌 |
| refreshToken | 刷新令牌 |

### 2.方法

* 获取当前登录用户信息

```
getCurUser()

参数: 无
返回: 用户对象详情

```


* 校验用户是否存在

```
doRequestAccountExist(String loginName)

参数: loginName 用户名
返回: 回调responsobject返回为布尔值 TRUE-存在 FALSE-不存在

```


* 注册账户

```
doRequestRegist(String loginName, String password)

参数: loginName 用户名(邮箱)
      password 用户设置的密码
返回: 回调注册结果

```

* 邮箱用户忘记密码

```
doRequestApplyRestPwdByEmail(String email)

参数: email 用户名(邮箱)
返回: 回调操作结果

```
* 登出账户

```
doRequestLogout(String loginName)

参数: loginName 用户名    
返回: 回调操作结果

```


* 更新用户头像

```
doRequestUploadUserLogo(File file)

参数: file 用户头像图片
返回: 回调操作结果

```

* 修改用户头像及昵称

```
doRequestUpdateUserInfo(String nickName, String email, String mobileNo, String sex, String realName, String birthday, String location, String securityNum, String remark)
参数: 	nickName 用户昵称
      	email 用户邮箱
		mobileNo 用户手机号
		sex 用户性别
		realName 用户真实姓名
		birthday 用户生日
		location 用户联系地址
		securityNum 用户身份证号
		remark 备注
返回: 回调操作结果

```

* 登陆后修改用户密码

```
doRequestUpdatePwd(String password, String oldPwd)

参数: password 用户设置的新密码
      oldPwd 用户原来密码
返回: 回调操作结果

```

