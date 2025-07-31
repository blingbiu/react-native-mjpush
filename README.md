# React-Native-mJpush

[![npm version](https://badge.fury.io/js/react-native-mjpush.svg)](https://badge.fury.io/js/react-native-mjpush)

iOS Version: 5.7.0

Android Version: 5.8.0

## 此项目基于[https://github.com/jpush/jpush-react-native](https://github.com/jpush/jpush-react-native)

## ChangeLog

1. 从RN-JPush2.7.5开始，重新支持TypeScript
2. 由于RN-JCore1.6.0存在编译问题，从RN-JCore1.7.0开始，还是需要在AndroidManifest.xml中添加配置代码，具体参考 配置-2.1 Android

## 1. 安装

```sh
npm install react-native-mjpush --save
```

* 注意：如果项目里没有react-native-mjcore，需要安装

  ```sh
  npm install react-native-mjcore --save
  ```

安装完成后连接原生库

进入到根目录执行

```sh
react-native link
```

或

```sh
react-native link react-native-mjpush
react-native link react-native-mjcore
```

## 2. 配置

### 2.1 Android

* build.gradle

  ```gradle
  android {
        defaultConfig {
            applicationId "yourApplicationId"           //在此替换你的应用包名
            ...
            manifestPlaceholders = [
                    JPUSH_APPKEY: "yourAppKey",         //在此替换你的APPKey
                    JPUSH_CHANNEL: "yourChannel"        //在此替换你的channel
            ]
        }
    }
  ```

  ```gradle
  dependencies {
        ...
        implementation project(':react-native-mjpush')  // 添加 jpush 依赖
        implementation project(':react-native-mjcore')  // 添加 jcore 依赖
    }
  ```

* setting.gradle

  ```gradle
  include ':react-native-mjpush'
  project(':react-native-mjpush').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-mjpush/android')
  include ':react-native-mjcore'
  project(':react-native-mjcore').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-mjcore/android')
  ```

* AndroidManifest.xml

  ```xml
  <meta-data
    android:name="JPUSH_CHANNEL"
    android:value="${JPUSH_CHANNEL}" />
  <meta-data
    android:name="JPUSH_APPKEY"
    android:value="${JPUSH_APPKEY}" />    
  ```

### 2.2 iOS

注意：您需要打开ios目录下的.xcworkspace文件修改您的包名

### 2.2.1 pod

```sh
pod install
```

* 注意：如果项目里使用pod安装过，请先执行命令

  ```sh
  pod deintegrate
  ```

### 2.2.2 手动方式

* Libraries

  ```txt
  Add Files to "your project name"
  node_modules/react-native-mjcore/ios/RCTJCoreModule.xcodeproj
  node_modules/react-native-mjpush/ios/RCTJPushModule.xcodeproj
  ```

* Capabilities

  ```txt
  Push Notification --- ON
  ```

* Build Settings

  ```txt
  All --- Search Paths --- Header Search Paths --- +
  $(SRCROOT)/../node_modules/react-native-mjcore/ios/RCTJCoreModule/
  $(SRCROOT)/../node_modules/react-native-mjpush/ios/RCTJPushModule/
  ```

* Build Phases

  ```txt
  libz.tbd
  libresolv.tbd
  UserNotifications.framework
  libRCTJCoreModule.a
  libRCTJPushModule.a
  ```

## 3. 引用

### 3.1 Android

参考：[MainApplication.java](https://github.com/bashen1/react-native-mjpush/tree/master/example/android/app/src/main/java/com/example/MainApplication.java)

### 3.2 iOS

参考：[AppDelegate.m](https://github.com/bashen1/react-native-mjpush/tree/master/example/ios/example/AppDelegate.m) 

### 3.3 js

参考：[App.js](https://github.com/bashen1/react-native-mjpush/blob/dev/example/App.js) 

## 4. API

详见：[index.js](https://github.com/bashen1/react-native-mjpush/blob/master/index.js)

## 5.  其他

* 集成前务必将example工程跑通
* 如有紧急需求请前往[极光社区](https://community.jiguang.cn/c/question)
* 上报问题还麻烦先调用JPush.setLoggerEnable(true}，拿到debug日志
