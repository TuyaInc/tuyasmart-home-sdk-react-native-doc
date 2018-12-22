## 设备控制
### 调用API
#### `import TuyaHomeApi from './api/TuyaHomeApi'`

### 设备信息获取

##### 【描述】

涂鸦智能提供了丰富的接口供开发者实现设备信息的获取和管理能力(移除等)。设备相关的返回数据都采用异步消息的方式通知接受者.

##### 【注意事项】

- 设备控制必须先初始化数据，即先调用
  
  TuyaHomeApi.getHomeDetail({
	homeId:'',
}).then(data=>{}).catch(e=>{})
- schema dp数据相关介绍[详见功能点相关概念][3]

------

### 设备操作控制

ITuyaDevice类提供了设备状态通知能力，通过注册回调函数，开发者可以方便的获取设备数据接受、设备移除、设备上下线、手机网络变化的通知。同时也提供了控制指令下发，设备固件升级的接口。

`

#### 设备功能点

DeviceBean 类 dps 属性定义了设备的状态，称作数据点（DP点）或功能点。`dps`字典里的每个`key`对应一个功能点的`dpId`，`dpValue`为该功能点的值。各自产品功能点定义参见[涂鸦开发者平台](https://developer.tuya.com/)的产品功能。
功能点具体参见[快速入门-功能点相关概念](https://docs.tuya.com/cn/creatproduct/#_7)

##### 【指令格式】

发送控制指令按照以下格式：
{"(dpId)":"(dpValue)"}

##### 【功能点示例】

开发平台可以看到一个产品这样的界面
![功能点](./images/ios_dp_sample.jpeg)

根据后台该产品的功能点定义，示例代码如下:

```java
//设置dpId为1的布尔型功能点示例 作用:开关打开 
dps = {"1": true};

//设置dpId为4的字符串型功能点示例 作用:设置RGB颜色为ff5500
dps = {"4": "ff5500"};

//设置dpId为5的枚举型功能点示例 作用:设置档位为2档
dps = {"5": "2"};

//设置dpId为6的数值型功能点示例 用:设置温度为20°
dps = {"6": 20};

//设置dpId为15的透传型(byte数组)功能点示例 作用:透传红外数据为1122
dps = {"15": "1122"};

//多个功能合并发送
dps = {"1": true, "4": "ff5500"};

  TuyaDeviceApi.send({
                  devId: this.state.devId,
                  command: command
                }).then(data => {
                    console.warn("--->data", data);
                  })
                  .catch(err => {
                    console.warn("--->err", err);
                  });
```

##### 【注意事项】

- 控制命令的发送需要特别注意数据类型。<br />
	比如功能点的数据类型是数值型（value），那控制命令发送的应该是 `{"2": 25}`  而不是  `{"2": "25"}`<br />
- 透传类型传输的byte数组是字符串格式并且必须是偶数位。<br />
	比如正确的格式是: `{"1": "0110"}` 而不是 `{"1": "110"}`

#### 初始化数据监听

##### 【描述】

TuyaDeviceApi提供设备相关信息（dp数据、设备名称、设备在线状态和设备移除）的监听，会实时同步到这里。 这边要按照一定顺序传递参数

##### 【实现回调】

```js
 TuyaDeviceApi.registerDevListener(
      { devId: this.state.devId },
      data => {
        console.log("onDpUpdate", data);
      },
      data => {
        console.warn("onRemoved", data);
      },
      data => {
        console.warn("onStatusChanged", data);
      },
      data => {
        console.warn("onNetworkStatusChanged", data);
      },
      data => {
        console.warn("onDevInfoUpdate", data);
      }
    );
```

#### 数据下发

##### 【描述】

通过局域网或者云端这两种方式发送控制指令给设备。send(通过局域网或者云端这两种方式发送控制指令给设备。)

##### 【方法调用】

```js
//发送控制命令给硬件
command的格式应符合{key:value} 例如 {"1":true}
      TuyaDeviceApi.send({
                  devId: this.state.devId,
                  command: command
                })
                  .then(data => {
                    console.warn("--->data", data);
                  })
                  .catch(err => {
                    console.warn("--->err", err);
                  });
```

##### 【代码范例】

以灯类产品作为示例

1、定义灯开关dp点

```js
var STHEME_LAMP_DPID_1 = "1"; //灯开关 
```

2、关于灯开关的数据结构：

```js
    let command ={}
    dpValue 可以为enum bool number
    command[STHEME_LAMP_DPID_1] = dpValue
```

3、对设备进行初始化

```js
/**
 * 设备对象。该设备的所有dp变化都会通过callback返回。
 *
 * 初始化设备之前，请确保已经初始化连接服务端，否则无法获取到服务端返回信息
 */
 registerDevListener(监听设备变化)

  TuyaDeviceApi.registerDevListener(
      { devId: this.state.devId },
      data => {

      },
      data => {
        console.warn("onRemoved", data);
      },
      data => {
        console.warn("onStatusChanged", data);
      },
      data => {
        console.warn("onNetworkStatusChanged", data);
      },
      data => {
        console.warn("onDevInfoUpdate", data);
      }
    );
```

4、开灯的代码片段

```js
  let command ={}
  command[dpId] = !!!dpValue
 TuyaDeviceApi.send({
  devId: this.state.devId,
  command: command
  })
  .then(data => {
   console.warn("--->data", data);
   })
   .catch(err => {
   console.warn("--->err", err);
    });
```

5、注销设备监听事件

```js
TuyaDeviceApi.unRegisterDevListener({ devId: this.state.devId,});
```

6、设备资源销毁

```js
TuyaDeviceApi.onDestroy({ devId: this.state.devId,});
```

##### 【注意事项】

- 指令下发成功并不是指设备真正操作成功，只是意味着指令成功发送出去。操作成功会有dp数据信息上报上来 ，且通过`onDpUpdate`接口返回。
- command 命令字符串 是以`{dpId,dpValue}` 数据格式转成JsonString。
- command 命令可以一次发送多个dp数据。



#### 设备信息查询

##### 【描述】

查询单个dp数据 从设备上查询dp最新数据 会经过 onDpUpdate 接口回调。

##### 【方法调用】

```js
TuyaDeviceApi.getDp({dpId:''}).then((data)=>{
}).catch((err)=>{
})
```

##### 【代码范例】

```js
1、通过调用TuyaDeviceApi.getDp方法。

2、数据会通过dp数据更新监听上报上来。
onDpUpdate(String devId,String dpStr)
```

##### 【注意事项】 

- 该接口主要是针对那些数据不主动去上报的dp点。 常规查询dp数据值可以通过 DeviceBean里面 getDps()去获取。

#### 设备重命名

##### 【描述】

设备重命名，支持多设备同步。

##### 【方法调用】

```js
//重命名
       TuyaDeviceApi.renameDevice({
              devId: this.state.devId,
              name: this.state.nameValue
            })
```

##### 【代码范例】

```js
       TuyaDeviceApi.renameDevice({
              devId: this.state.devId,
              name: this.state.nameValue
            })
              .then(data => {
                console.log("--->data", data);
              })
              .catch(err => {
                console.warn("-->err", err);
              });
```

成功之后 ，`onDevInfoUpdate()` 会收到通知。



#### 移除设备

##### 【描述】

用于从用户设备列表中移除设备

##### 【方法调用】

```js
/**
 * 移除设备
 *
 * @param callback
 */
     TuyaDeviceApi.removeDevice({
              devId: this.state.devId,
            })
```

##### 【代码范例】

```js
    TuyaDeviceApi.removeDevice({
              devId: this.state.devId,
            }).then(data => {
                console.log("--->data", data);
              })
              .catch(err => {
                console.warn("-->err", err);
              });
```