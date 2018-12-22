### 设备数据流通道
### 调用API
import TuyaSingleTransferApi from './api/TuyaSingleTransferApi'


主要用于扫地机地图数据等大量实时上报的场景

```js
const TuyaSingleTransferApi = {
	/**
	 * 开始连接
	 */
    startConnect();

	/**
	 * 是否在线
	 */
    isOnline();

	/**
	 * 订阅设备数据，订阅设备之后，设备如果有数据上报上来，便可以通过 registerTransferDataListener 回调上来。需要注意的是，每次通道连接成功都需要重新订阅设备数据
	 */ 
  subscribeDevice(devId) 

	/**
	 * 取消订阅设备信息，则设备数据不在收到
	 *
	 */
  unSubscribeDevice(devId)

/**
 * 注册设备数据流，SDK不做数据解析，具体格式需要和硬件上报方协商一致，然后解析。
 */
  registerTransferDataListener({
		onSuccess(),
		onError(),
	})

    /** 取消注册
    */
   unRegisterTransferDataListener

    /**
    	断开数据流通道
    */
    stopConnect();
}

```



### 数据模型

#### DeviceBean

- iconUrl 设备图标链接地址
- devId 设备唯一标示id
- isOnline 设备是否在线（局域网或者云端在线） 
- name 设备名称
- schema 用来描述设备dp点属性
- productId 产品唯一标示id
- pv  网关通信协议版本 用x.x来表示 。
- bv  网关通用固件版本 用x.x来表示。
- time 设备添加时间
- isShare 设备是否被分享
- schemaMap Map类型 key 表示dpId， value 表示Schema 数据。
- dps  设备当前数据信息。key 是 dpId ，value 是值。
- lon、lat用来标示经纬度信息，需要用户使用sdk前，调用TuyaSdk.setLatAndLong 设置经纬度信息。
- isZigBeeWifi 是否是ZigBee网关设备
- hasZigBee 是否包含ZigBee能力（网关设备或者子设备）