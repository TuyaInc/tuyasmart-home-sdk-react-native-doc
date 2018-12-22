### ZigBee网关配网

### 调用API
#### `import TuyaActivatorApi from './api/TuyaActivatorApi'`

```
这里的ZigBee网关配网是指有线配网
```

#### ZigBee网关有线配网

ZigBee网关配网前，请确保ZigBee网关设备连接上外网联通的路由器，并使ZigBee网关设备处于配网状态

##### 【方法调用】

```js
//配置相应参数
 TuyaActivatorApi.initActivator({
        //配网
        homeId:this.state.homeId,
        ssid: this.state.ssid,
        password: this.state.wifipassword,
        time: this.state.maxTime,
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

##### 【代码范例】

```java
//初始化监听
ITuyaSmartActivatorListener  listener =new ITuyaSmartActivatorListener() {
                @Override
                public void onError(String errorCode, String errorMsg) {
						
                }

                @Override
                public void onActiveSuccess(DeviceBean deviceBean) {
                	
                }

                @Override
                public void onStep(String step, Object data) {

                }
            })
ITuyaActivator mITuyaActivator = TuyaHomeSdk.getActivatorInstance().newGwActivator(new TuyaGwActivatorBuilder()
            .setToken(token)
            .setTimeOut(100)
            .setContext(this)
            .setListener(listener);
            
//开始配网
TuyaActivatorApi.start();
//停止配网
TuyaActivatorApi.stop()
//退出页面清理
TuyaActivatorApi.onDestroy()
```


