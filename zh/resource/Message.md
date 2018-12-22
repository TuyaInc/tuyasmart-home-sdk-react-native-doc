## 消息中心
### 调用API
import TuyaMessageApi from './api/TuyaMessageApi'


### 获取消息列表

##### 【描述】

用于获取全部消息列表。

##### 【方法原型】

```js
/**
 *  获取消息列表
 *
 * @param callback 回调
 */
TuyaMessageApi.getMessageList().then(data=>{}).catch(e=>{})
```

其中， 返回值提供一下key：

```js
/**
 * 获取日期和时间 格式: 2017-09-08 17:12:45
 *
 * @return 日期和时间
 */
dateTime
/**
 * 获取消息图标URL
 *
 * @return 消息图标URL
 */
icon

/**
 * 获取消息类型名称(如果是告警类型消息则为dp点名称)
 *
 * @return 消息类型名称
 */
msgTypeContent

/**
 *  获取消息内容, 可用于界面展示
 *
 * @return 消息内容
 */
msgContent

/**
 * 获取消息类型
 * 0: 系统消息
 * 1: 有新的设备
 * 2: 有新的好友
 * 4: 设备告警
 *
 * @return 消息类型
 */
msgType

/**
 * 获取设备id
 * 注： 只有告警类型消息才会有该字段
 *
 * @return 设备ID
 */
msgSrcId

/**
 *  获取消息id
 *
 * @return 消息id
 */
id
```

##### 【代码范例】

```js
TuyaMessageApi.getMessageList().then(data=>{}).catch(e=>{})
```

### 删除消息

##### 【描述】

用于批量删除消息。

##### 【方法原型】

```js
/**
 *  删除消息
 *
 * @param mIds 要删除的消息的id列表
 * @param callback 回调
 */
TuyaMessageApi.deleteMessage({
	ids:[]//要删除的消息的id列表
})
```

##### 【代码范例】

```js
TuyaMessageApi.deleteMessage({
	ids:[]//要删除的消息的id列表
}).then(data=>{}).catch(e=>{})
```

## 