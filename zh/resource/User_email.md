# 用户邮箱账号体系
涂鸦智能提供邮箱密码登陆体系。
### 调用API
import TuyaUserApi from './api/TuyaUserApi'

## 一、用户邮箱密码注册
**接口描述**

用户邮箱密码注册。支持国内外邮箱注册。
```js
/**
//邮箱注册获取验证码
/**
 * 注册获取邮箱验证码
 * @param email
 */
 getRegisterEmailValidateCode

 //邮箱密码注册
* @param countryCode 国家区号
* @param email       邮箱账户
* @param passwd      登陆密码
registerAccountWithEmail
```
**代码范例**

```js
//注册获取邮箱验证码
 TuyaUserApi.getRegisterEmailValidateCode({
	 email:'',
 }).then(data=>{}).catch(err=>{})

//邮箱密码注册
 TuyaUserApi.registerAccountWithEmail({
	 email:'',
	 passwd:'',
 }).then(data=>{}).catch(err=>{})
```
> 注意事项   账户一旦注册到一个国家，目前数据无法迁移其他国家。

## 二、用户邮箱密码登陆
**接口描述**

用户邮箱密码登陆

```js
//邮箱密码登陆
* @param email  邮箱账户
* @param passwd 登陆密码
loginWithEmail
```
**代码范例**

```java
//邮箱密码登陆
//邮箱密码登陆
TuyaUserApi.loginWithEmail({
	email:'',
	passwd:'',
}).then(data=>{}).catch(err=>{})
```
## 三、 用户邮箱重置密码
**接口描述**

用户邮箱重置密码
```js
//邮箱找回密码，获取验证码
* @param countryCode 国家区号
* @param email       邮箱账户

getEmailValidateCode

//邮箱重置密码
* @param email     用户账户
* @param emailCode 邮箱验证码
* @param passwd    新密码
resetEmailPassword
```
**代码范例**

```js
//获取邮箱验证码
TuyaUserApi.getEmailValidateCode({
	countryCode:'',
	email:'',
}).then(data=>{}).catch(err=>{})

//重置密码
TuyaUserApi.resetEmailPassword({
	email:'',
	emailCode:'',
	passwd:'',
}).then(data=>{}).catch(err=>{})

```