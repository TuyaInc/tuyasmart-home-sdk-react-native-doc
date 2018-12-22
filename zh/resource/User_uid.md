# 用户uid登陆体系

### 调用API
import TuyaUserApi from './api/TuyaUserApi'

涂鸦智能提供uid登陆体系。如果客户自有用户体系，那么可以通过uid登陆体系，接入我们的sdk。
## 一、用户uid注册

**接口描述**

用户uid注册
```js
//用户uid注册
* @param countryCode 国家号码
* @param uid         用户uid
* @param password    用户密码

registerAccountWithUid
```
**代码范例**

```js
//uid注册
TuyaUserApi.registerAccountWithUid.({
	countryCode:'',
	uid:'',
	password:'',
}).then(data=>{}).catch(err=>{})
```
## 二、用户uid登陆
**接口描述**

用户uid登陆

```js
//uid 登陆
* @param countryCode 国家号码
* @param uid         用户uid
* @param passwd      用户密码

loginWithUid
```
**代码范例**

```js
//uid登陆
TuyaUserApi.loginWithUid.({
	countryCode:'',
	uid:'',
	passwd:'',
}).then(data=>{}).catch(err=>{})
```
## 三、用户uid重置密码
用户uid重置密码，需要通过云云对接的方式进行重置密码。详看云端API文档



## 四、用户uid登陆注册接口
**接口描述**

用户UID 登陆注册合成一个接口。

```js
//uid 登陆
* @param countryCode 国家号码
* @param uid         用户uid
* @param passwd      用户密码

loginOrRegisterWithUid
```
**代码范例**

```js
//uid登陆
TuyaUserApi.loginOrRegisterWithUid({
	countryCode:'',
	uid:'',
	passwd:'',
}).then(data=>{

}).catch(err=>{})
```