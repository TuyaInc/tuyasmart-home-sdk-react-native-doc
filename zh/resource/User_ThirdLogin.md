#  第三方登陆
### 调用API
import TuyaUserApi from './api/TuyaUserApi'

## 一、Twitter登陆

**接口说明**

```js
* @param countryCode 国家区号
* @param key         twitter授权登录获取的key
* @param secret      twitter授权登录获取的secret
loginByTwitter({
	countryCode:'',
	key:'',
	secret:'',
}).catch(err=>{

})
```


## 二、QQ登陆

**接口说明**

```js
* @param countryCode 国家区号
* @param userId          QQ授权登录获取的userId
* @param accessToken      QQ授权登录获取的accessToken
loginByQQ({
	countryCode:'',
	userId:'',
	accessToken:'',
}).then(data=>{}).catch(err=>{})
```

## 三、微信登陆

**接口说明**

```js
* @param countryCode 国家区号
* @param code        微信授权登录获取的code
loginByWechat({
	countryCode:'',
	code:''
}).then(data=>{}).catch(err=>{})

```

## 四、Facebook 登陆
**接口说明**


```js
* @param countryCode 国家区号
* @param code      token facebook授权登录获取的token
loginByFacebook({
	countryCode:'',
	code:'',
}).then(data=>{

}).catch(err=>{})
```