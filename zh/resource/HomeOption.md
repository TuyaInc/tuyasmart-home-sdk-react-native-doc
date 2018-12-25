### 家庭操作类
### 调用API
#### `import TuyaHomeApi from './api/TuyaHomeApi'`


TuyaHomeApi 提供了家庭相关的操作类，负责处理家庭的数据和信息的更新。

#### 初始化家庭下的所有数据

```js 
    TuyaHomeApi.getHomeDetail({
	homeId:'',
}).then(data=>{}).catch(e=>{})

```

#### 获取本地缓存中的数据信息 


```js
	
	获取家庭下面的本地cache
   TuyaHomeApi.getHomeLocalCache({
	homeId:'',
}).then(data=>{}).catch(e=>{})

```
#### 更新家庭信息

```java

    /**
     * 更新家庭信息
     *
     * @param name     家庭名称
     * @param lon      当前家庭的经度
     * @param lat      当前家庭的纬度
     * @param geoName  地理位置的地址
     * @param callback
     */
TuyaHomeApi.updateHome({
	homeId:'',
	name:'',
	lon:'',
	lat:'',
	geoName:''//家庭地理位置名称
}).then(data=>{}).catch(e=>{})
```

#### 解散家庭

```js
	/**
     * 解散家庭
     *
     * @param callback
     */
    TuyaHomeApi.dismissHome({
	homeId:'',
}).then(data=>{}).catch(e=>{})

```

#### 排序

```java

    /**
     * 排序
     *
     * @param idList homeId list 
     * @param callback
     */
  TuyaHomeApi.sortHome({
	idList: Arrry,
}).then(data=>{}).catch(e=>{})
```

#### 添加房间

```java
   /**
     * 添加房间
     *
     * @param name
     * @param callback
     */
    void addRoom(String name, ITuyaRoomResultCallback callback);
```

#### 移除家庭下面的房间

```
 /**
   * 移除房间
   *
   * @param roomId
   * @param callback
   */
TuyaHomeApi.removeRoom({
	homeId:'',
	roomId:'',
}).then(data=>{}).catch(e=>{})

```

#### 排序家庭下面的房间

```java

 /**
   * 排序房间
   *
   * @param idList   房间id的list
   * @param callback
   */
TuyaHomeApi.sortRoom({
	homeId:'',
	idList:[],//房间id的list
}).then(data=>{}).catch(e=>{})

```

#### 查询房间列表

```java
   /**
    * 查询房间列表
    *
    * @param homeId
    */
TuyaHomeApi.queryRoomList({
	homeId:'',
}).then(data=>{}).catch(e=>{})

```
