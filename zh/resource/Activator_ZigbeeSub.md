## ZigBee子设备配网
ZigBee子设备配网需要ZigBee网关设备云在线的情况下才能发起,且子设备处于配网状态。

【方法调用】

```js
TuyaActivatorApi.newGwSubDevActivator({
	devId:'',
	time:,//超时时间
}).then(data=>{}).catch(e=>{})
//开始配置
mTuyaActivator.start();
//停止配置
mTuyaActivator.stop();
//退出页面销毁一些缓存和监听
mTuyaActivator.onDestroy();

```
【代码范例】

```js
TuyaActivatorApi.newGwSubDevActivator({
	devId:'',
	time:100,//超时时间
}).then(data=>{}).catch(e=>{})
//开始配网
mTuyaActivatorApi.start();
//停止配网
TuyaActivatorApi.stop();
//销毁
TuyaActivatorApi.onDestory();

```