## 群组管理

### 调用API
#### `import TuyaGroupApi from './api/TuyaGroupApi'`

涂鸦云支持群组管理体系：可以创建群组，修改群组名称，管理群组设备，通过群组管理多个设备，解散群组。


### 创建群组

##### 【描述】

涂鸦智能提供一些设备群组控制的接口。这里的群组控制是指WiFi群组，目前只有群控的功能。群组功能默认关闭，如果需要开通群组功能，联系我们业务人员

##### 【方法调用】

```js
TuyaGroupApi.createGroup({
	homeId:'',
	productId:'',
	name:'',
	devIds:[]
})

```

##### 【代码范例】

```js
//创建群组
TuyaGroupApi.createGroup({
	homeId:123123,
	productId:'adfsfwefsdf',
	name:'aaaa',
	devIds:[]
}).then(data=>{}).catch(e=>{})
```

##### 【注意事项】

群组默认不支持创建，如果你的产品需要这个功能，那么请联系我们对产品进行开启这项功能。

### 群组列表获取

##### 【描述】

此接口主要是从云端拉取最新群组列表。

##### 【方法调用】

```js
TuyaGroupApi.queryDeviceListToAddGroup({
	homeId:, --Number
	productId:'',  ---string
})
(此接口主要是从云端拉取最新群组列表 根据产品ID)
```

##### 【代码范例】

```js
//云端获取群组列表
TuyaGroupApi.queryDeviceListToAddGroup({
	homeId:200032,
	productId:'213123d12s', 
}).then(data=>{}).catch(e=>{})
```

### 群组操作

##### 【描述】

涂鸦智能群组操作，主要是基于对主设备的操作，主设备是指当前群组在线的第一个设备。在线和离线状态、数据上报都是依赖于主设备的变更。发送控制命令是面对群组的所有设备。



#### (1) 群组修改名称

##### 【描述】

群组修改名称

##### 【方法调用】

```js
* 群组修改名称
* @param groupId    群组id
* @param callback 回调
updateGroupName({groupID:, //Number
name:''})
```

##### 【代码范例】

```js
//群组重命名
TuyaGroupApi.updateGroupName({groupID:123123,name:'hah'})
```


#### (1) 解散群组

##### 【描述】

 dismissGroup 解散群组

##### 【方法调用】

```js
* 解散群组
* @param groupId    群组id
* @param callback 回调
TuyaGroupApi.dismissGroup({
	groupId:'',
})
```

##### 【代码范例】

```js
//删除群组
TuyaGroupApi.dismissGroup({
	groupId:123456,
}).then(data=>{}).catch(e=>{})
```

#### (2) 群组回调事件

##### 【描述】

群组回调事件

##### 【方法调用】

```java
* 注册群组回调事件
* @param listener 回调
TuyaGroupApi.registerGroupListener({
   groupId:'',
},onDpUpdate,onGroupInfoUpdate,onGroupRemoved)

* 注销群组回调事件
TuyaGatewayApi.unregisterGroupListener({
	groupId:'',
},sub)
```

##### 【代码范例】

```js
//注册群组回调事件
TuyaGroupApi.registerGroupListener({
   groupId:'',
},onDpUpdate,onGroupInfoUpdate,onGroupRemoved).then(data=>{
}).catch(err=>{
})
//注销群组回调事件
TuyaGatewayApi.unregisterGroupListener({
	groupId:'',
},sub).(data=>{
}).catch(err=>{
})

```

#### （3）发送群组控制命令

##### 【描述】

发送群组控制命令

##### 【方法调用】

```js
* 发送群组控制命令
* @param command 控制命令
* @param listener 回调
TuyaGroupApi.publishDps({
	groupId:'',
	command:{}
})

```

##### 【代码范例】

```js
//command 参考设备篇
TuyaGroupApi.publishDps({
	groupId:'',
	command:'{'1':true}'
}).then(data=>{}).catch(e=>{})

```

##### 【注意事项】

群组的发送命令返回结果，是指发送给云端成功，并不是指实际控制设备成功。 



#### （5）群组数据销毁

```js
//群组数据销毁，建议退出群组控制页面的时候调用。
TuyaGroupApi.onDestroy({
	groupId:'',
})
```

## 