### 家庭管理类
### 调用API
#### `import TuyaHomeManagerApi from './api/TuyaHomeManagerApi'`

TuyaHomeManagerApi 提供了创建家庭、获取家庭列表以及监听家庭相关的变更

可以通过TuyaHomeManagerApi来获取

#### 创建家庭

```javascript
 /**
   *
   * @param name     家庭名称
   * @param lon      经度
   * @param lat      纬度
   * @param geoName  家庭地理位置名称
   * @param rooms    房间列表
   * @param callback
   */
  TuyaHomeManagerApi.createHome({
	name:'',//家庭名称
	lon:'',
	lat:'',
	geoName:'',// 家庭地理位置名称
    rooms:[]//房间列表
}).then(data=>{}).catch(e=>{})


```


#### 获取家庭列表

```javascript

/**
  * @param callback
  */
    void queryHomeList(ITuyaGetHomeListCallback callback);
```

#### 家庭信息的变更

```javascript

   /**
     * 注册家庭信息的变更
     * 有：家庭的增加、删除、信息变更、分享列表的变更和服务器连接成功的监听
     *
     * @param listener
     */
TuyaHomeManagerApi.registerTuyaHomeChangeListener(
	onHomeAdded,//庭添加成功,用于多设备数据同步
    onHomeRemoved,//家庭删除成功
    onHomeInfoChanged,// 家庭信息变更,用于多设备数据同步
    onSharedDeviceList,//分享设备列表变更 用于多设备数据同步
    onSharedGroupList,//分享群组列表变更 用于多设备数据同步
    onServerConnectSuccess//手机连接涂鸦云服务器成功，特别注意接收到此通知，在一些情况下，本地数据与服务端数据可能会不一致，可以调用Home下面getHomeDetail接口重新刷新数据。
	)
    
    
    /**
     * 注销家庭信息的变更
     *
     * @param listener
     */
  TuyaHomeManagerApi.unregisterTuyaHomeChangeListener(sub);
    
    
```



### 对家庭的缓存数据操作

```javascript

获取此数据前，应该调用家庭的初始化接口 getHomeDetail、或者getHomeLocalCache 之后才会有
  TuyaHomeApi.getHomeDetail({
      homeId: this.state.homeId
    })
      .then(data => {}).catch(err=>{
      })

```

