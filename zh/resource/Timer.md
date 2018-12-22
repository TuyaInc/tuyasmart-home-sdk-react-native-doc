## 定时任务
### 调用API
import TuyaTimerApi from './api/TuyaTimerApi'


涂鸦智能提供了基本的定时能力，支持设备（包括WiFi设备，蓝牙mesh子设备，zigbee子设备）和群组。并封装了针对设备dp点的定时器信息的增删改查接口。APP通过定时接口设置好定时器信息后，硬件模块会自动根据定时要求进行预订的操作。每个定时任务下可以包含多个定时器。如下图所示：
![timer](./images/ios-sdk-timer.jpg)

定时相关的所有方法都在`TuyaRnTimerApi`中

以下多个接口用到了taskName这个参数，具体可描述为一个分组，一个分组可以有多个定时器。每个定时属于或不属于一个分组，分组目前仅用于展示

### 增加定时器

##### 【 描述】

增加一个定时器

##### 【方法调用】

```js
/**
 * [addTimer description]
 * @param {[type]} category [description]
 * @param {[type]} loops    [7位字符串，每一位表示星期几，第一位表示星期日，第二位表示星期一，依次类推，表示在哪些天启用定时。0表示未选中，1表示选中.格式例如只选中星期一 星期二："0110000"。如果都未选中，则表示定时只执行一次，格式："0000000"]
 * @param {[type]} instruct [instruct包含一个dp点的集合和时间]
 * @param {[type]} groupId [这个是群组id]
 * 添加定时
 * 支持群组定时
 */

默认dpValue为true

   TuyaTimerApi.addTimerWithTask({
        taskName: "timer",
        loops: ,
        devId: ,
        dpId: "0",
        time: d
      })
 如果最后一个参数不传则说明表示为devId，支持设备和群组定时
 
   /**
     * 增加定时器         支持子设备新接口
     * 其他参数值释义同上
     * @param dps    dp点键值对，key是dpId，value是dpValue,仅支持单dp点
     * @param callback 回调
     */
 addTimerWithTaskDps({
  taskName: "timer",
        loops: ,
        devId: ,
        dpId: "0",
        time: d,
        dps:,
 })
        
```

##### 【代码范例】

```js
     设备定时
     /**
       * 设备定时
       */
     var instruct = [];
     instruct.push({ dps: { 0: true }, time: d });
     loops=[0,0,0,0,0,0,1];
      TuyaTimerApi.addTimerWithTask({
        taskName: "timer",
        loops: this.state.repeat.join(""),
        devId: this.state.devInfo.devId,
        dpId: "0",
        time: d
      })
      
      /**
       * 设备定时 带有自己定义dp点
       */
       TuyaTimerApi.addTimerWithTaskDps({
         taskName: "timer",
        loops: ,
        devId: ,
        dpId: "0",
        time: d,
        dps:'{'1':true}',
 })
```

### 获取某设备下的所有定时任务状态

##### 【描述】

获取某设备下的所有定时任务状态

##### 【方法调用】

```java
* 获取定时任务下所有定时器
* @param taskName 定时任务名称
* @param devId    设备Id或群组Id
* @param callback 回调
getTimerTaskStatusWithDeviceId({devid:''})
```

##### 【代码范例】

```js
    TuyaTimerApi.getTimerTaskStatusWithDeviceId({devid:''})
      .then(data => {
    
        }
      })
      .catch(err => {
        console.log("--err", err);
      });
```


### 控制定时任务中所有定时器的开关状态

##### 【描述】

控制定时任务中所有定时器的开关状态

##### 【方法调用】

```js
* 获取某设备下的所有定时任务状态
*
* @param devId    设备Id

TuyaTimerApi.updateTimerTaskStatusWithTask({taskName:'',devId:'',status:''})
```

##### 【代码范例】

```js
TuyaTimerApi.updateTimerTaskStatusWithTask({taskName:'',devId:'',status:''}).then(data=>{
}).catch(err=>{
})
```

### 控制某个定时器的开关状态

##### 【描述】

控制某个定时器的开关状态

##### 【方法调用】

```js
* 控制定时任务中所有定时器的开关状态
/**
* 控制某个定时器的开关状态
* @param taskName 定时任务名称
* @param devId    设备Id或群组Id
* @param timerId  定时钟Id
* @param isOpen   开关 Boolean
 */
 
updateTimerStatusWithTask({taskName:'',devId:'',timeId:'',isOpen:true})
```

##### 【代码范例】

```java
TuyaTimerApi.updateTimerStatusWithTask({taskName:'',devId:'',timeId:'',isOpen:true}).then(data=>{}).catch(err=>{})
```


### 删除定时器

##### 【描述】

删除定时器

##### 【方法调用】

```java
* 删除定时器
* @param taskName 定时任务名称
* @param devId    设备Id或群组Id
* @param timerId  定时钟Id String
* @param callback 回调
  TuyaTimerApi.removeTimerWithTask({devId:'', taskName:'', timeId:''})
```

##### 【代码范例】

```js
  TuyaTimerApi.removeTimerWithTask({devId:'',taskName:'',timeId})
              .then(data => {

              })
              .catch(err => {
                console.log("--->err", err);
              });
```




### 更新定时器的状态

##### 【描述】

更新定时器的状态

##### 【方法调用】

```js
/**
* 更新定时器的状态
* @param taskName 定时任务名称
* @param loops    循环次数 如每周每天传”1111111”
* @param devId    设备Id或群组Id
* @param timerId  定时钟Id
* @param dpId     dp点id
* @param time     定时时间
* @param isOpen      是否开启 
 */
updateTimerWithTask({taskName:'',loops:'',devId:'',timerId:'',dpId:'',time:'',isOpen:true})


/**
 * 更新定时器的状态
 * @param taskName 定时任务名称
 * @param devId    设备Id或群组id
 * @param timerId  定时钟Id
 * @param loops    循环次数
 * @param instruct 定时dp点数据,只支持单dp点 json格式 如:   [{
 *                 "time": "20:00",
 *                 "dps": {
 *                 "1": true
 *                 }]
 */
updateTimerWithTaskInstruct({taskName:'',loops:'',devId:'',timerId:'',instruct:''})


```

##### 【代码范例】

```js
TuyaTimerApi.updateTimerWithTask({taskName:'',loops:'',devId:'',timerId:'',dpId:'',time:'',isOpen:true}).then(data=>{
}).catch(err=>{})



TuyaTimerApi.updateTimerWithTaskInstruct({taskName:'',loops:'',devId:'',timerId:'',instruct: "[{"time": "20:00", "dps": { "1": true},{"time": "22:00","dps": {"2": true}]"})

```

### 获取定时任务下所有定时器

##### 【描述】

获取定时任务下所有定时器

##### 【方法调用】

```js
* 获取定时任务下所有定时器
* @param taskName 定时任务名称
* @param devId    设备Id或群组Id
  TuyaTimerApi.getTimerWithTask({devId:'', taskName:''})
```

##### 【代码范例】

```js
 TuyaTimerApi.getTimerWithTask({devId:'', taskName:''})
              .then(data => {

              })
              .catch(err => {
                console.log("--->err", err);
              });
```

### 获取设备所有定时任务下所有定时器

##### 【描述】

获取设备所有定时任务下所有定时器

##### 【方法调用】

```js
* 获取定时任务下所有定时器
* @param devId    设备Id或群组Id
  TuyaTimerApi.getAllTimerWithDeviceId({devId:''})
```

##### 【代码范例】

```js
  TuyaTimerApi.getAllTimerWithDeviceId({devId:''})
              .then(data => {

              })
              .catch(err => {
                console.log("--->err", err);
              });
```

## 