ITuyaActivator 集成了WiFi配网、ZigBee配网、蓝牙mesh配网等。

### WiFi配网  
### 调用API
#### `import TuyaActivatorApi from './api/TuyaActivatorApi'`

##### 【描述】

```
WiFi配网主要有EZ模式和AP模式两种
```

##### 【初始化参数配置】

```js
TuyaActivatorApi.initActivator({
	homeId:'',
	ssid:'',
	password:'',
	time:'',//超时时间
	type:'',//配网模式TY_AP,TY_EZ,TY_QR
}).then(data=>{}).catch(e=>{})
```

##### 【参数说明】

###### 【入参】

```java
/**
* @param homeId  当前用户的homeId
* @param ssid   配网之后，设备工作WiFi的名称。（家庭网络）
* @param password   配网之后，设备工作WiFi的密码。（家庭网络）
* @param activatorModel:	现在给设备配网有以下两种方式:
ActivatorModelEnum.TY_EZ: 传入该参数则进行EZ配网
ActivatorModelEnum.TY_AP: 传入该参数则进行AP配网
* @param timeout     配网的超时时间设置，默认是100s.
*/
```



##### 【方法调用】

```js
//getActivator  初始化
 TuyaActivatorApi.initActivator({
        //配网
        homeId:,         //Number
        ssid: ,          //String
        password: ,      //String
        time: ,          //Number
        type: "TY_EZ". //"TY_AP"
      })
        .then(data => {
        .catch(error => {
        });
//开始配置
TuyaActivatorApi.startConfig();
//停止配置
TuyaActivatorApi.stopConfig();
//退出页面销毁一些缓存和监听
TuyaActivatorApi.onDestroy();
```

##### 【代码范例】

```js
//配置相应参数
 TuyaActivatorApi.initActivator({
        //配网
        homeId:232132,   
        ssid: "wsdesfsde",
        password: "12345678",
        time: 100,
        type: "TY_EZ". //"TY_AP"
      })
        .then(data => {
          console.log('----->data',data)
          console.warn("PEIWANGCGON");
        })
        .catch(error => {
          console.log('---config err',error)

        });
//开始配置
TuyaActivatorApi.start();
//停止配置
TuyaActivatorApi.stop();
//回调销毁
TuyaActivatorApi.onDestroy();
```

#### 【配网问题汇总】

##### 配网超时，此时设备一直处于连不上网络的状态。有以下几种原因。

- 获取WiFi Ssid 错误，导致配网失败
	安卓系统API里面获取到ssid，通常前后会有“”。
	建议使用Tuya Sdk里面自带的WiFiUtil.getCurrentSSID()去获取
- WiFi密码包含空格
	用户在输入密码的时候，由于输入法联想的功能很容易在密码中输入空格。建议密码输入的时候直接显示出来，另外在判断密码含有空格的时候，弹窗提醒用户。
- 用户不输入WiFi密码
	用户在首次使用智能设备产品的过程中，很容易不输入密码就进行后续操作
	建议判断密码输入为空且WiFi加密类型不为NONE时，弹窗提醒用户。
- 用户在AP配网时选择了设备的热点名称，用户首次使用智能产品的过程中，很容易出现此问题。
	建议在判别AP配网时用户选择了设备的热点名称，弹窗提醒给用户。
- 获取WiFi的Ssid为"0x","\<unknown ssid\>"
	目前发现在一些国产手机会出现此问题。并不是用户选择的WiFi名称。这是由于定位权限没开启导致的，建议用户可以手动输入WiFi的Ssid，或者给出弹窗提醒，让用户开启相应权限。

##### 配网超时，此时设备已经激活成功。可能原因有：

- APP没有连接到正常的网络，导致无法获取设备的状态。
