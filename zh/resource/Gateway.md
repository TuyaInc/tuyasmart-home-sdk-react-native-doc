## 网关

### 调用API

####  `import {TuyaGatewayApi} from 'tuyasmart-home-sdk'`

网关类封装了ZigBee网关的相关操作，包括控制，查询子设备，监听子设备状态等。
可以通过GatewayNativeApi提供的相应方法去完成相关操作。
`const GatewayNativeApi = require('react-native').NativeModules.TuyaGatewayModule`

- publishDps 发送命令
- broadcastDps(广播控制设备)
- multicastDps 组播控制设备
- getSubDevList 获取网关子设备
- registerSubDevListener 注册子设备信息变更
- unRegisterSubDevListener 注销子设备信息变更

```javascript
TuyaGatewayApi.publishDps({
	devId:'',
	localId:'',
	dps:''
}).then(data=>{}).catch(e=>{})

TuyaGatewayApi.broadcastDps({
	devId:'',
	dps:''
}).then(data=>{}).catch(e=>{})

TuyaGatewayApi.multicastDps({
	devId:'',
	localId:'',
	dps:''
}).then(data=>{}).catch(e=>{})


TuyaGatewayApi.registerSubDevListener({
	devId:'',
},onSubDevDpUpdate,onSubDevRemoved,onSubDevAdded,onSubDevInfoUpdate,onSubDevStatusChanged)

TuyaGatewayApi.unRegisterSubDevListener({
	devId:'',
},sub)

```

------

