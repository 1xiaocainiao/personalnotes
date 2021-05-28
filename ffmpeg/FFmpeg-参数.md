转码以及裁剪视频
```
var arg = [

“-i”,
this.widget.videoPath,
// “-ss”, //剪去1毫秒, 可以解决录制第一帧黑屏,但治标不治本
// “00:00:00.001”,
// “-t”,
// endTime(duration),
“-c:v”,
“h264”,
“-c:a”, // 音频直接copy
“copy”,
“-b:v”, //平均码率 不设置这个，默认用的25，视频压缩会很模糊
“3200k”,
“-bufsize”, // 码率控制缓冲大小
“3200k”,
/ “-maxrate”, // 最大码率 -minrate 最小码率
“3200k”, /
“-fs”, // 设置文件最大值
“${videoMaxSize}MB”,
targetVideoPath
];
```

获取视频首帧图
```
var coverArg = [
“-i”,
this.widget.videoPath,
“-vframes”,
“1”,
coverImagePath,
];
```

amr 转 mp3
```
final Directory extDir = await getTemporaryDirectory();
    final String dirPath = '${extDir.path}/$VoiceCacheFoldNameMP3';
    await Directory(dirPath).create(recursive: true);
    var fileName = mp3URL.split("/").last;
    var path = "$dirPath/$fileName";

var arg = [
      "-i",
      amrPath,
      path,
    ];
```
