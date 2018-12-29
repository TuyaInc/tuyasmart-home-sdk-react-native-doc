# session失效监听


**描述**

Session由于可能存在一些异常或者在一段时间不操作（45天）会失效掉，这时候需要退出应用，重新登陆获取Session。

**接口说明**

```js
//session失效监听 在js层我们监听事件 needLogin


```
**实现回调**

```js
this.needLoginListener = RCTDeviceEventEmitter.addListener("needLogin",()=>{
//处理相关逻辑
})
```
**代码范例**

```java
import RCTDeviceEventEmitter from "RCTDeviceEventEmitter";

componentWillMount(){
this.needLoginListener = RCTDeviceEventEmitter.addListener("needLogin",()=>{
//处理相关逻辑
})

}

componentWillUnmount(){
this.needLoginListener.remove();
}



```
>注意事项
>
> - 一旦出现此类回调，请跳转到登陆页面，让用户重新登陆。

---