#### 固件升级
### 调用API

####  `import {TuyaOTAApi} from 'tuyasmart-home-sdk'`

##### 【描述】
我们通过上面调用api拿到TuyaOTAPi进行相关操作
固件升级主要用于修复设备bug和增加设备新功能。固件升级主要分两种，第一种是设备升级，第二种是MCU升级。升级的接口位于TuyaOTAApi中。

#### 查询固件升级信息


##### 【方法调用】

```js
//获取固件升级信息
TuyaOTAApi.getOtaInfo({devId:''}).then(data=>{}).catch(e=>{})

```

返回固件升级的json信息，提供以下信息

```js
	 upgradeStatus;//升级状态，0:无新版本 1:有新版本 2:在升级中
    version;//最新版本
    currentVersion;//当前版本
    timeout;//超时时间，单位：秒
    upgradeType;//0:app提醒升级 2-app强制升级 3-检测升级
    type;//0:wifi设备 1:蓝牙设备 2:GPRS设备 3:zigbee设备（目前只支持zigbee网关）9:MCU
    typeDesc;//模块描述
    astUpgradeTime;//上次升级时间，单位：毫秒
```

##### 【代码范例】

```js
TuyaOTAApi.getOtaInfo({devId:''}).then(data=>{
//处理相应数据
}).catch(e=>{})
```

#### 设置升级状态回调

##### 【描述】

ota之前需要注册监听，以实时获取升级状态
onSuccess,onFailure,onProgress 相应的funtion传进去，处理相应的回调

##### 【方法调用】

```js
//otaType 升级的设备类型，同`UpgradeInfoBean`的type字段
TuyaOTAApi.startOta({
	devId:''
},onSuccess,onFailure,onProgress).then(data=>{}).catch(e=>{})
```

#### 开始升级

##### 【描述】

 调用以开始升级,调用后注册的ota监听会把升级状态返回回来，以便开发者构建UI

##### 【方法调用】

```js
TuyaOTAApi.startOta({
	devId:''
},onSuccess,onFailure,onProgress).then(data=>{}).catch(e=>{})
```

#### 销毁

##### 【描述】

 离开升级页面后要销毁，回收内存。

##### 【方法调用】

```js
TuyaOTAApi.onDestory()
```

#### 