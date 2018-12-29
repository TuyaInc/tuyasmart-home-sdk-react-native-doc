# 集成TuyaRnSDK
## 集成准备
## 开发环境准备
1. 配置相关react-native 环境 [react-native环境搭建](https://reactnative.cn/docs/getting-started.html)  请采用react-native 0.57版本
2. 首先找一个文件夹 执行react-native init 项目名
（例如 react-native init TuyaSdkTest）

## Android 篇介绍

### 一、安装
#### 1. Run `npm install tuyasmart-home-sdk --save`
#### 2. `react-native link tuyasmart-home-sdk`

### 二、使用
#### 例如 `import {TuyaCoreApi} from 'tuyasmart-home-sdk'`

### 三、混淆配置

在proguard-rules.pro文件配置相应混淆配置

```shell
#fastJson
-keep class com.alibaba.fastjson.**{*;}
-dontwarn com.alibaba.fastjson.**

#netty
-keep class io.netty.** { *; }
-dontwarn io.netty.**

#mqtt
-keep class org.eclipse.paho.client.mqttv3.** { *; }
-dontwarn org.eclipse.paho.client.mqttv3.**

-dontwarn okio.**
-dontwarn rx.**
-dontwarn javax.annotation.**
-keep class com.squareup.okhttp.** { *; }
-keep interface com.squareup.okhttp.** { *; }
-keep class okio.** { *; }
-dontwarn com.squareup.okhttp.**

-keep class com.tuya.**{*;}
-dontwarn com.tuya.**
```

### 四、注意事项
在app的build.gradle中加入以下代码

```
repositories {
    flatDir {
        dirs project(':tuyasmart-home-sdk').file('libs')
    }
}
```

## 在代码中使用SDK功能

TuyaRNSdk 是一切全屋智能API对外的接口，包含：配网、初始化、控制、房间、群组、ZigBee等一系列的操作。




