## iOS native
```
import Foundation
import UIKit

extension UIImage {
    func compressToCacheSandbox(_ maxFileSize: Int = 524_288, targetPath: String, compressionQuality: Int) -> String? {
        if FileManager.default.fileExists(atPath: targetPath) {
            do {
                try FileManager.default.removeItem(atPath: targetPath)
            } catch  {
                
            }
        }
        
        let imageData = self.jpegData(compressionQuality: CGFloat(compressionQuality) / 100.0)
        
        if let tempData = imageData {
            do {
                try  tempData.write(to: URL(fileURLWithPath: targetPath), options: Data.WritingOptions.atomic)
            } catch   {
                print(error.localizedDescription)
                return nil
            }
        }
        
        return targetPath
    }
}
```

```
import Flutter

public class FlutterIOSImageCompressPlugin: NSObject, FlutterPlugin {
    /// Public register method for Flutter plugin registrar.
    public static func register(with registrar: FlutterPluginRegistrar) {
        let channel = FlutterMethodChannel(name: "flutterImageCompress",
                                           binaryMessenger: registrar.messenger())
        let instance = FlutterIOSImageCompressPlugin()
        registrar.addMethodCallDelegate(instance, channel: channel)
    }
    
    /// Public handler method for managing method channel calls.
    public func handle(_ call: FlutterMethodCall, result: @escaping FlutterResult) {
        if call.method == "imageCompress",
           let arguments = call.arguments as? Dictionary<String, String>,
           let filePath = arguments["filePath"],
           let image = UIImage(contentsOfFile: filePath),
           let maxFileSizeString = arguments["maxFileSize"],
           let maxFileSize = Int(maxFileSizeString),
           let targetPath = arguments["targetPath"],
           let compressionQuality = arguments["quality"] {
            result(image.compressToCacheSandbox(maxFileSize, targetPath: targetPath, compressionQuality: Int(compressionQuality) ?? 1))
        } else {
            result(FlutterError(code: "-1",
                                message: "compress image failed", details: "compress image failed"))
        }
    }
}
```
以上为插件原型，下面是Appdelegate中的代码
```
let registrarCompressImage = self.registrar(forPlugin: "flutterImageCompress")
        FlutterIOSImageCompressPlugin.register(with: registrarCompressImage!)
```
## flutter native
flutter plugin
```
import 'package:flutter/services.dart';

class FlutterImageCompressIos {
  static const MethodChannel _channel =
      const MethodChannel('flutterImageCompress');

  static Future<String> get platformVersion async {
    final String version = await _channel.invokeMethod('getPlatformVersion');
    return version;
  }

  static final FlutterImageCompressIos instance = FlutterImageCompressIos();

  static Future<File> compressImage(
    String filePath,
    String targetPath, {
    int maxFileSize = 524288,
    int quality = 95,
  }) async {
    var file = await _channel.invokeMethod("imageCompress", {
      'filePath': filePath,
      "targetPath": targetPath,
      'maxFileSize': "$maxFileSize",
      'quality': "$quality",
    });

    return new File(file);
  }
}
```

使用
```
await FlutterImageCompressIos.compressImage("", "")
```
