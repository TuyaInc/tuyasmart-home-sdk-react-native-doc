### 移除分享
### 调用API
#### `import TuyaShareApi from './api/TuyaShareApi'`

通过调用TuyaShareApi里的方法完成相应操作

#### (1)删除共享关系

##### 【描述】

分享者通过memberId 删除与这个关系用户的所有共享关系（用户维度删除）

##### 【方法调用】

```js
@param memberId 用户成员Id 
removeUserShare({
	 memberId:'',
 }).
```

##### 【代码范例】

```js
TuyaShareApi.removeUserShare({
	 memberId:'',
 }).then(data=>{}).catch(err=>{})
```

#### (2)删除收到的共享关系

##### 【描述】

被分享者通过memberId 删除与这个关系用户的所有共享关系（用户维度删除）

##### 【方法调用】

```js
@param memberId 用户成员Id 
removeReceivedUserShare({
	 memberId:'',
 })
```

##### 【代码范例】

```js
  TuyaShareApi.removeReceivedUserShare({
	 memberId:'',
 }).then(data=>{}).catch(err=>{})
```

#### (3)删除某个设备共享

##### 【描述】

分享者删除指定关系用户下的某个共享的设备

##### 【方法调用】

```java
@param devId 设备Id
@param memberId 用户成员Id 
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

#### (4)移除收到的分享设备

##### 【描述】

被分享者删除某个共享的设备

##### 【方法调用】

```js
@param devId 设备Id
 removeReceivedDevShare({
		devId:'',
	})
```

##### 【代码范例】

```js
  TuyaShareApi.removeReceivedDevShare({
		devId:'',
	}).then(data=>{}).catch(err=>{})
```

### 