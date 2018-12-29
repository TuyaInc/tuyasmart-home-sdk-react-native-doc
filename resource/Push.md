# 集成Push

基于Tuya SDK开发的app，Tuya平台支持Push功能，支持给用户发送运营Push和产品的告警Push。

## 一、集成友盟

国内Push功能是基于友盟推送开发的，请先参考[友盟文档](https://developer.umeng.com/docs/66632/detail/66744)将友盟集成到项目中，涂鸦云支持友盟第三方通道，如果需要小米、华为、魅族通道，去各个平台申请，依照友盟文档初始化

### 设置用户别名

在确保友盟已经集成到项目中后，通过友盟SDK设置用户id，推送时会按照用户id向用户推送消息

```js
/**
* @param aliasId Alias		1.可以是你的应用为每个用户自动生成的唯一id，
* 2.也可以是用户采用第三方平台登录时从第三方平台获取到的用户id  具体参考友盟文档
* 3.也可以使用涂鸦SDK中的方法获取唯一的id，PhoneUtil.getDeviceID(context),PhoneUtil位于com.tuya.smart.android.common.utils包中
* @param ALIAS_TYPE		需要填"TUYA_SMART"
*/
mPushAgent.addAlias("zhangsan@sina.com", "TUYA_SMART", new UTrack.ICallBack() {
    @Override
    public void onMessage(boolean isSuccess, String message) {
    }
});
```

### Push涂鸦云注册

将aliasId注册到涂鸦云

```js
/**
* @param aliasId   用户别名 为第二步向友盟注册用户别名的alias
* @param pushProvider   注册push的类别  友盟填"umeng" 
*/		
TuyaPushApi.registerDevice({aliasId:'',pushProvider:''}).then(data=>{}).catch(e=>{})
```

### 第三方通道设置

如果使用了友盟第三方通道，弹窗的activity必须命名为SpecialPushActivity.
![push](../../../../SDK%E6%96%87%E6%A1%A3/tuyasmart_home_android_sdk-master/TuyaSmartHomeSdkDemo/doc/images/push_mi.png)
以小米为例，SpecialPushActivity继承自UmengNotifyClickActivity，并且完整的包名路径为`com.activity.SpecialPushActivity`.

### Push消息接收

继承 UmengMessageService, 实现自己的Service来完全控制达到消息的处理，参考友盟文档

```java
public class MyPushIntentService extends UmengMessageService {
    @Override
    public void onMessage(Context context, Intent intent) {
        try {
            String message = intent.getStringExtra(AgooConstants.MESSAGE_BODY);
            UMessage msg = new UMessage(new JSONObject(message);
            UmLog.d(TAG, "message=" + message);      //消息体
            UmLog.d(TAG, "custom=" + msg.custom);    //自定义消息的内容
            UmLog.d(TAG, "title=" + msg.title);      //通知标题
            UmLog.d(TAG, "text=" + msg.text);        //通知内容
            
            PushBean pushBean=PushBean.formatMessage(msg.custom)

        } catch (Exception e) {
            L.e(TAG, e.toString());
        }
}
```

>说明
> - msg.custom中的内容就是收到的推送信息
> - msg.custom的具体协议格式：
>	custom=tuya://message?a=view&ct=${title}&cc=​${content}&p=>{}&link=tuyaSmart%3A%2F%2Fbrowser%3Furl%3Dhttp%253A%252F%252Fwww.baidu.com;
>- 通过PushBean.formatMessage()来对数据进行解析得到PushBean

### 用户解绑

**接口说明**

在用户退出登录等需要解除应用和用户关系的操作下调用友盟的移除别名的方法

```java
/**
* @param aliasId Alias		用户自动生成的唯一id
* @param ALIAS_TYPE		需要填"TUYA_SMART"
*/ 
mPushAgent.deleteAlias(aliasId, "TUYA_SMART", new UTrack.ICallBack() {
    @Override
    public void onMessage(boolean isSuccess, String message) {
    }
});
```

### 发送Push

#### 新增运营Push

涂鸦开发者平台 - 用户运营 - 消息中心 - 新增消息

#### 新增告警Push

涂鸦开发者平台 - 对应产品 - 扩展功能 - 告警设置 - 新增告警规则(应用推送方式)

----

## 二、集成FCM Push

对于国外的用户，需要集成Google的FCM推送服务。先参照官方文档 [将 Firebase 添加到您的 Android 项目](https://firebase.google.com/docs/android/setup?hl=zh-cn),之后配置客户端，参考 [Android客户端配置Firebase](https://firebase.google.com/docs/cloud-messaging/android/client?hl=zh-cn)

### 将注册令牌注册到涂鸦云

在继承`FirebaseInstanceIdService`类的`onTokenRefresh`方法监控注册令牌的生成，并将令牌注册到涂鸦云。

```java
/**
* @param aliasId   用户别名 即fcm生成的token
* @param pushProvider   注册push的类别  fcm填"gcm"
*/		
TuyaHomeSdk.getInstance().registerDevice(String aliasId, String pushProvider, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }

    @Override
    public void onSuccess() {

    }
});
```

### 用户解绑

**说明**

在用户退出登录等需要解除应用和用户关系的操作下调用FCM的移除注册令牌的方法

```java
FirebaseInstanceId.getInstance().deleteInstanceId();
```

