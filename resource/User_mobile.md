# 手机账号体系

### 调用API

####  `import {TuyaUserApi} from 'tuyasmart-home-sdk'`

涂鸦智能提供手机验证码登陆体系。
通过TuyaUserApi来获取相应接口
## 一、手机验证码登陆

手机验证码登录功能，需要先调用验证码发送接口，发送验证码。再调用手机验证码验证接口。将收到的验证码填入对应的参数中。

**接口描述**

```js
//获取手机验证码
* @param countryCode   国家区号
* @param phoneNumber   手机号码
 getValidateCode({
	 countryCode: '',
	 phoneNumber: '')}

//手机验证码登陆
* @param countryCode 国家区号
* @param phone       电话
* @param code        验证码
 loginWithValidateCode({
	 countryCode:'',
	 phone:'',
 }).then(data=>{}).catch(err=>{})
```

**代码范例**

```java

//获取手机验证码
* @param countryCode   国家区号
* @param phoneNumber   手机号码
 TuyaUserApi.getValidateCode({
	 countryCode: '86',
	 phoneNumber: '123123'}).then(data=>{}).catch(err=>{})

//手机验证码登陆
* @param countryCode 国家区号
* @param phone       电话
* @param code        验证码
 TuyaUserApi.loginWithValidateCode({
	 countryCode:'86',
	 phone:'123123',
 }).then(data=>{}).catch(err=>{})
```
## 二、用户手机密码登陆

涂鸦智能提供手机密码登陆体系。
### 1. 手机密码注册
手机密码注册。支持国内外手机注册。

**接口描述：**

```java
/**
//获取手机验证码
* @param countryCode   国家区号
* @param phoneNumber   手机号码
getValidateCode()

//注册手机密码账户
* @param countryCode 国家区号
* @param phone       手机密码
* @param passwd      登陆密码

registerAccountWithPhone()

```

**代码范例**

```js
//获取手机验证码
TuyaUserApi.getValidateCode({
	countryCode:'',
	phoneNumber:'',
}).then(data=>{}).catch(err=>{})
//注册手机密码账户
TuyaUserApi.registerAccountWithPhone({
	countryCode:'',
	phone:'',
	passwd:'',
}).then(data=>{}).catch(err=>{})
```
### 2. 手机密码登陆
**接口描述**

使用手机号码和密码登陆。
```js
//手机密码登陆
* @param countryCode 国家区号
* @param phone       手机密码
* @param passwd      登陆密码
loginWithPhonePassword()
```
**代码范例**

```js
//手机密码登陆
* @param countryCode 国家区号
* @param phone       手机密码
* @param passwd      登陆密码
TuyaUserApi.loginWithPhonePassword({
	countryCode:'',
	phone:'',
	passwd:'',
}).then(data=>{}).catch(err=>{})
```
### 3. 手机重置密码
**接口描述**

手机账号重置密码。
```js
//获取手机验证码
* @param countryCode   国家区号
* @param phoneNumber   手机号码
getValidateCode

//重置密码
* @param countryCode 国家区号
* @param phone       手机号码
* @param code        手机验证码
* @param newPasswd   新密码
resetPhonePassword

```
**代码范例**

```java
//手机获取验证码
TuyaUserApi.getValidateCode({
countryCode:'',
	phone:'',
}).then(data=>{
}).catch(err=>{
})

//重置手机密码
TuyaUserApi.resetPhonePassword({
	countryCode:'',
	phone:'',
	code:'',
	newPasswd:'',
}).then(data=>{}).catch(err=>{})
```