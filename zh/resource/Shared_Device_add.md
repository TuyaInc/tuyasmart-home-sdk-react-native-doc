### 添加共享
### 调用API
import TuyaShareApi from './api/TuyaShareApi'

通过调用TuyaShareApi里的方法完成相应操作
#### (1)添加多个设备共享（覆盖）

##### 【描述】

分享多个设备给指定用户，会将指定用户的以前所有分享覆盖掉

##### 【方法调用】

```java
@param homeId	 家庭id
@param countryCode 手机区号码,例如中国是“86”
@param userAccount 账号
@param ShareIdBean 分享内容 目前支持 设备或者mesh


TuyaShareApi.addShareWithHomeId({
homeId:'',
countryCode:'',
userAccount:'',
devIds:'',
})

```

##### 【代码范例】

```java
TuyaShareApi.addShareWithHomeId({
homeId:'',
countryCode:'',
userAccount:'',
devIds:'',
}).then(data=>{}).catch(err=>{})
```

#### (2)添加多个设备共享（追加）

##### 【描述】

分享多个设备给指定用户，会将要分享的设备追加到指定用户的所有分享中

##### 【方法调用】

```java
@param homeId		分享者家庭id
@param countryCode   手机区号码,例如中国是“86”
@param userAccount   手机号码
@param devIds 		 分享的设备id列表

TuyaShareApi.addShareWithMemberId({
memberId:'',
	devIds:'',
})

```

##### 【代码范例】



```js
/**
 * 批量添加设备共享
 * @param memberId 分享目标用户id
 * @param devIds 设备id列表 要求string数组
 * @param callback
 */
 
TuyaShareApi.addShareWithMemberId({
	memberId:'',
	devIds:'',
}).then(data=>{}).catch(err=>{})

```



#### (3)单个设备取消共享

##### 【描述】

通过用户关系id取消单个设备分享

##### 【方法调用】

```java
/**
 * 用户下的设备分享关闭
 *
 * @param devId
 * @param memberId
 * @param callback
 */
disableDevShare({
	devId:'',
	memberId:'',
})

```

##### 【代码范例】

```js
TuyaShareApi.disableDevShare({
	devId:'',
	memberId:'',
}).then(data=>{}).catch(err=>{})
```

### 查询分享

#### (1)查询主动分享的关系列表

##### 【描述】

分享者获取主动分享的关系列表(分享给其他用户的用户信息列表)

##### 【方法调用】

```js
queryUserShareList({
	homeId:'',
})

```

##### 【代码范例】

```js
TuyaShareApi.queryUserShareList({
	homeId:'',
}).then(data=>{}).catch(err=>{})
```

#### (2)查询收到分享关系列表

##### 【描述】

被分享者获取收到的分享关系列表

##### 【方法调用】

```js
queryShareReceivedUserList()

```

##### 【代码范例】

```js
TuyaShareApi.queryShareReceivedUserList().then(data=>{
}).catch(err=>{
})

```

#### (3)查询指定设备的分享用户列表

##### 【描述】

分享者获取某个设备的共享用户列表

##### 【方法调用】

```js
@param devId 设备Id
queryDevShareUserList({
	devId:'',
})

```

##### 【代码范例】

```js
TuyaShareApi.queryDevShareUserList({
	devId:'',
}).then(data=>{}).catch(err=>{})
```

#### (4)查询指定设备是谁共享的

##### 【描述】

被分享者查找指定设备是谁共享过来的

##### 【方法调用】

```js
@param devId 设备Id
queryShareDevFromInfo({
	devId:'',
})

```

##### 【代码范例】

```js
TuyaShareApi.queryShareDevFromInfo().then(data=>{
}).catch(err=>{
})
```

#### (5)查询分享到指定用户的共享关系

##### 【描述】

分享者 通过memberId 获取分享给这个关系用户的所有共享设备信息

##### 【方法调用】

```
@param memberId 用户成员Id 从SharedUserInfoBean中获取
getUserShareInfo({
	memberId:'',
})

```

##### 【代码范例】

```java
TuyaShareApi.getUserShareInfo({
	memberId:'',
}).then(data=>{}).catch(err=>{})
```

#### (6)查询收到指定用户共享的信息

##### 【描述】

被分享者 通过memberId 获取收到这个关系用户的所有共享设备信息

##### 【方法调用】

```js
getReceivedShareInfo({
	memberId:'',
}).then(data=>{}).catch(err=>{})

```

##### 【代码范例】

```java
TuyaShareApi.getReceivedShareInfo({
	memberId:'',
}).then(data=>{}).catch(err=>{})
```


### 