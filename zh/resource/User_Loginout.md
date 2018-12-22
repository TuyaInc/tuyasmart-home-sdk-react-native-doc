## 一、上传用户头像
用户相关的我们可以使用TuyaUserApi来调用相关api

### 调用API
import TuyaUserApi from './api/TuyaUserApi'

**接口描述**

用于上传用户自定义的头像。

```js
/**
 * 上传用户头像
 *
 * @param file     用户头像图片文件
 */
TuyaUserApi.uploadUserAvatar
```
**代码范例**

```java
TuyaUserApi.uploadUserAvatar({
	file:''
}).then(data=>{

}).catch(err=>{})
```
## 二、设置温度单位
**接口描述**

设置温度单位是摄氏度还是华氏度

```js
/**
 * TempUnitEnum.Celsius是摄氏度,TempUnitEnum.Fahrenheit是华摄度
 *
 * @param unit
 */
  TuyaUserApi.setTempUnit({
	 unit:'',
 }).then(data=>{

 }).catch(err=>{})

```


## 三、退出登录接口

用户账号切换的时候需要调用退出登录接口

**代码范例**

```js
  TuyaUserApi.logout().then(data=>{

}).catch(err=>{})

```
## 四、注销账户

**接口描述**

一周后账号才会永久停用并删除以下你账户中的所有信息，在此之前重新登录，则你的停用请求将被取消

```java

/**
 * 注销账户
 * Account cancellation
 * @param callback
 */
cancelAccount()
    
```
**代码范例**

```js
  TuyaUserApi.cancelAccount().then(data=>{}).catch(err=>{});

```