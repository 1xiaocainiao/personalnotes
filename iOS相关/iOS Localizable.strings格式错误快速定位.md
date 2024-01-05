
iOS开发多语言，翻译过后的文字很多行有些总是会有各种各样的问题。导致运行失败，如何能快速找出出错的位置呢。

### 运行报错，这是Localizable.strings文件里内容格式不正确

`validation failed: Couldn't parse property list because the input data was in an invalid format`

1.先进入Localizable.strings对应目录下  
2.输入`pl < Localizable.strings`  
会定位到准确的某一行  
`tc@tcdeMacBook-Pro en.lproj % pl < Localizable.strings 2022-06-02 17:24:57.577 pl[10493:269738] *** Exception parsing ASCII property list: NSParseErrorException Error Domain=NSCocoaErrorDomain Code=3840 "Unexpected character " at line 1" UserInfo={NSDebugDescription=Unexpected character " at line 1, kCFPropertyListOldStyleParsingError=Error Domain=NSCocoaErrorDomain Code=3840 "Expected ';' or '=' after key at line 58" UserInfo={NSDebugDescription=Expected ';' or '=' after key at line 58}}`  

