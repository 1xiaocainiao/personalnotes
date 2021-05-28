#iOS 原生主动调用flutter并返回数据到原生
iOS 原生  swift
```
final Channel = FlutterMethodChannel(name: "callBackImUserInfo",
                                                     binaryMessenger: binaryMessenger)
        }
        
        imUserInfoChannel.invokeMethod("getImUser", arguments: userId) { (result) in
            print("结果")
        }
```

flutter
```
const callBackImUserInfoChannel = MethodChannel('callBackImUserInfo');
callBackImUserInfoChannel.setMethodCallHandler(handelCall);
```

```
Future<dynamic> handelCall(MethodCall methodCall) async {
    print(methodCall.toString());
    print("原生主动调用flutter");
    Map<String, String> map = {};
    if (methodCall.method == "getImUser") {
      final value = await UserInfoDataSource.getUserInfo(methodCall.arguments);
      if (value != null) {
        map = {
          "user_id": value.userId,
          "realname": value.realname,
          "avatar": value.avatar
        };
      }
    }
    return Future.value(map);
  }
```
注意setMethodCallHandler设置监听，重点通过调用  Future.value(backResult)  返回原生结果

[原文地址](https://www.jianshu.com/p/ca0e47ffef71)

#flutter 调用 iOS 代码
flutter 代码
```
const channel = MethodChannel('videoCallChannel');
        final toUserMap = {
          'id': id,
        };
        final meUserMap = {
          'id': id,
        };
        channel.invokeMethod(
            'videoCall', {"toUserMap": toUserMap, "meUserMap": meUserMap});
```

iOS 代码
```
let videoCallChannel = FlutterMethodChannel(name: "videoCallChannel",
                                                    binaryMessenger: controller.binaryMessenger)
        videoCallChannel.setMethodCallHandler({
            (call: FlutterMethodCall, result: @escaping FlutterResult) -> Void in
            guard call.method == "videoCall", let userMap = call.arguments as? Dictionary<String, Dictionary<String, String>>,
            let otherUserMap = userMap["toUserMap"],
            let meUserMap = userMap["meUserMap"] else {
                result(FlutterMethodNotImplemented)
                return
            }
            
            RCIMClient.shared()?.currentUserInfo = RCUserInfo(userId: meUserMap["id"], name: meUserMap["name"], portrait: meUserMap["avatar"])
            RCCall.shared().startSingleCall(otherUserMap["id"], mediaType: RCCallMediaType.video)
        })
```
