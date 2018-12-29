## 意见反馈
### 调用API

####  `import {FeedBackNativeApi} from 'tuyasmart-home-sdk'`

用于在用户和企业或开发者之间提供一种沟通通道。

FeedBackNativeApi是反馈的管理API，提供了新增反馈、获取反馈列表等接口，调用方式：
`const FeedBackNativeApi = require('react-native').NativeModules
  .TuyaFeedBackModule`

ITuyaFeedbackMag是针对某一会话的反馈管理类，也提供了新增反馈、获取当前会话的消息列表，
### 获取反馈列表

#### 【描述】

获取该用户所有的反馈。

##### 【方法原型】

```js
/**
 * 获取反馈列表
 *
 * 
 */
TuyaFeedBackApi.getFeedbackList().then(data=>{}).catch(e=>{})
```



### 获取反馈类型列表

##### 【描述】

获取可选择的反馈类型列表，用于创建反馈之前选择。

##### 【方法原型】

```js
/**
 * 获取反馈类型列表
 *
 * @param callback 回调
 */
TuyaFeedBackApi.getFeedbackType().then(data=>{}).catch(e=>{})
```

### 新增反馈

##### 【描述】

新增一条反馈信息。

##### 【方法原型】

```js
/**
 * 添加反馈
 *
 * @param message  反馈内容
 * @param contact  联系方式（电话或邮箱）
 * @param hdId     反馈类目id
 * @param hdType   反馈类型
 * @param callback 回调
 */
TuyaFeedBackApi.addFeedback({
	message:'',//反馈内容
	contact:'',// 联系方式（电话或邮箱）
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
}).then(data=>{}).catch(e=>{})
```

注 `hdId`, `hdType`变量可以从[获取反馈类型列表]()接口返回的`FeedbackTypeBean`类中获取。

##### 【代码范例】

```js
TuyaFeedBackApi.addFeedback({
	message:'',//反馈内容
	contact:'',// 联系方式（电话或邮箱）
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
}).then(data=>{
//做数据处理
}).catch(e=>{
//异常的一些处理
})
```

### 反馈消息管理

由[获取反馈列表](###)接口返回的反馈列表中，每个反馈对象都对应者一组消息(对话)。`TuyaFeedBackApi.getMsgList({
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
})`方法来初始化消息管理类。

例:

```js
TuyaFeedBackApi.getMsgList({
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
}).then(data=>{}).catch(e=>{})
```

#### 获取反馈消息列表

##### 【描述】

用于获取当前反馈话题（会话场景）的消息列表。

##### 【方法原型】

```java
/**
 * 获取反馈消息列表
 *
 *  @param callback 回调
 */
TuyaFeedBackApi.getMsgList({
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
}).then(data=>{}).catch(e=>{})
```


##### 【代码范例】

```js
TuyaFeedBackApi.getMsgList({
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
}).then(data=>{
//数据处理
}).catch(e=>{})
```

#### 添加新反馈

##### 【描述】

用于在当前对话中添加新的反馈消息。

##### 【方法原型】

```java
/**
 * 添加新反馈
 *
 * @param msg      反馈内容
 * @param contact  联系方式
 * @param hdId 反馈类目id
 * @param hdType 反馈类型
 */
TuyaFeedBackApi.addMsg({
	message:'',//反馈内容
	contact:'',// 联系方式（电话或邮箱）
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
})
```

##### 【代码范例】

```java
TuyaFeedBackApi.addMsg({
	message:'',//反馈内容
	contact:'',// 联系方式（电话或邮箱）
	hdId:'',// 反馈类目id
	hdType:''// 反馈类型
}).then(data=>{}).catch(e=>{})
```

## 