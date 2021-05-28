http://swift.gg/2016/12/30/how-to-read-the-swift-standard-libray-source/
按照以上步骤，在所有库下载完成后，使用命令 ./swift/utils/build-script --release-debuginfo --xcode 编译为xcode可以打开项目
期间遇到的错误
1.xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance
https://www.jianshu.com/p/07a281ff57d3 按照篇文章解决了
2.xcodebuild: error: 'cmark.xcodeproj' does not exist.
查看swift-source/build 下是否已经有此Xcode-RelWithDebInfoAssert 文件夹，有则删除，再尝试编译
