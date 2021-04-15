# 前端VUE项目打包成安卓APP



## 1.打包vue项目，在项目的根目录执行命令 npm run build,直至项目打包完成

## 2.新建cordova项目

### 	1.安装cordova，命令行执行 npm install -g cordova

### 	2.利用cordova创建一个新项目，命令行执行 cordova create folkmusic com.music.folkmusic musicapp

## 3.打包cordova项目，在根目录执行命令 cordova platforms add android --save

## 4.在根目录下执行 cordova build android生成apk文件

## 5.检查环境是否已经准备就绪，执行命令 cordova requirements

## 6.打包apk

1. 生成签名证书

   在命令行执行

```
keytool -genkey -v -keystore folkmusic.keystore -alias flokmusic -keyalg RSA -validity 36500
```

其中folkmusic.keystore代表所生成的证书文件名的所在目录（直接写名字代表当前目录），folkmusic代表别名，不写默认为mykey，RSA代表才用RSA算法，36500代表证书的有效期天数

然后根据提示输入所需录入的信息

成功之后会在目录下面生成一个证书文件

## 7.apk签名

签名的方式有两种：

### 1.生成未签名的debug版本的apk，然后再用命令进行签名

在根目录执行命令 cordova build android --release

成功之后会在release目录下面生成一个app-release-unsigned.apk的文件

将签名所生成的证书文件复制到该目录之下执行命令 

```
jarsigner -verbose -sigalg SHA1withRSA  -digestalg SHA1 -keystore VoiceCare.keystore app-release-unsigned.apk VoiceCare
```



### 2.直接生产签名的apk文件

在命令行执行

```
cordova build android --release --keystore="VoiceCare.keystore" --alias=VoiceCare --storePassword=123456 --password=123456
```

同样会在release目录下面生成一个apk文件，并且是已经签名了的文件。

在我们的项目开发中，如果每次都输入这样一长串的命令未免太过麻烦，在cordova项目中，我们可以通过配置来快速生成带签名的apk文件

在项目的根目录下面新建一个build.json文件，在里面配置证书的一些配置信息

```json
{
  "android": {
    "release": {
    "keystore": "VoiceCare.keystore",
    "alias": "VoiceCare",
    "storePassword": "123456",
    "password": "123456"
    }
  }
}
```

配置好之后以后打包就可以直接执行打包命令 cordova build android --release生成一个代签名的apk文件了

-----

## 问题：

### 1.无法联网

出现这种原因是因为我安装的android sdk是属于高版本的，在高版本的android sdk中默认开启了对非加密的明文传输的保护，我们无法通过http网络请求的方式获取数据。

解决方案如下（取一即可）：

1. android sdk27及以上有这种限制，可以将android sdk降低到26版本。降低android版本可以通过命令cordova platform remove android 再 cordova platform add  android@6.3.0,当我们打包时候就会自动给我们下载安装对应版本。

2. 在目录project\platforms\android\res\xml添加文件`network-security-config.xml,插入内容如下`

```
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true">
        <trust-anchors>
            <certificates src="system" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

在project\platforms\android\app\src\main\AndroidManifest.xml文件中修改，修改内容如下

```
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <application android:networkSecurityConfig="@xml/network_security_config">
    </application>
</manifest>
```

3. 可以使用https调用数据接口
4. 在AnroidManifest.xml中的application添加设置项：

```xml
<application android:usesCleartextTraffic="true">
```

此上方法任选一个应该可以解决这个问题。

---

## 2.打包无法获取权限问题

1.安装插件

`cordova plugin add cordova-plugin-media`

`cordova plugin add cordova-plugin-media-capture`

`cordova plugin add cordova-plugin-android-permissions`

`cordova plugin add cordova-plugin-camera`

2.在项目的index.html添加如下：

```html
<script src="cordova.js"></script>
<script>
	
	var permissions = cordova.plugins.permissions;
//校验app是否有安卓写入权限
permissions.checkPermission(permissions.RECORD_AUDIO, function(s) {
//hasPermission 验证是否成功
if (!s.hasPermission) {
    //没有权限
    //app申请写入权限
    permissions.requestPermission(permissions.RECORD_AUDIO, function(s) {
if (s.hasPermission) {
    //申请成功
}
else {
    //申请失败
}
}, function(error) {
});
} else {
    //拥有权限
}
}, function(error) {
});
</script>
```



