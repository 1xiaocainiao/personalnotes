NSData 推送Devicetoken 在Xcode11 的处理

NSData* theToken = ...
NSString* stringWithFormat = [NSString stringWithFormat"@"%@", theToken];
NSString* description = [theToken description];

Xcode 10 打印
result = 
@"<44154da7 32345001 53106883 ffc1071f a59c0d24 a70871e5 aa8dbb41>"

Xcode 11 iOS 13 打印
@"{length =32, bytes = 0x44154da7 32345001 53106883 ffc1071f ... a70871e5 aa8dbb41}"

NSData to hex NSString 
Xcode 10 以及之前
```
-(NSString *)hexStringFormData:(NSData *)data
{
    return [[[[NSString stringWithFormat:@"%@",data]
            stringByReplacingOccurrencesOfString:@"<" withString:@""]
            stringByReplacingOccurrencesOfString:@">" withString:@""]
            stringByReplacingOccurrencesOfString:@" " withString:@""];
}
```
Xcode 11 iOS 13 之后
```
NSMutableString *valueString = [NSMutableString string];
                    const char *bytes = valueData.bytes;
                    NSInteger count = valueData.length;
                    for (int i = 0; i < count; i++) {
                        [valueString appendFormat:@"%02x", bytes[i]&0x000000FF];
                    }
```
另一种 未测试是否正确
```
NSMutableString *string = [[NSMutableString alloc] initWithCapacity:[data length]];
    [data enumerateByteRangesUsingBlock:^(const void *bytes, NSRange byteRange, BOOL *stop) {
        unsigned char *dataBytes = (unsigned char*)bytes;
        for (NSInteger i = 0; i < byteRange.length; i++) {
            NSString *hexStr = [NSString stringWithFormat:@"%x", (dataBytes[i]) & 0xff];
            if ([hexStr length] == 2) {
                [string appendString:hexStr];
            } else {
                [string appendFormat:@"0%@", hexStr];
            }
        }
    }];
```

hex NSString to NSData
```
- (NSData *)convertDataBaseStoredStringToData:(NSString *)command
{
    if (![command isKindOfClass:[NSString class]]) {
        return [NSData data];
    }
    command = [command stringByReplacingOccurrencesOfString:@">" withString:@""];
    command = [command stringByReplacingOccurrencesOfString:@"<" withString:@""];
    command = [command stringByReplacingOccurrencesOfString:@" " withString:@""];
    NSMutableData *commandToSend= [[NSMutableData alloc] init];
    unsigned char whole_byte;
    char byte_chars[3] = {'\0','\0','\0'};
    int i;
    for (i=0; i < [command length]/2; i++) {
        byte_chars[0] = [command characterAtIndex:i*2];
        byte_chars[1] = [command characterAtIndex:i*2+1];
        whole_byte = strtol(byte_chars, NULL, 16);
        [commandToSend appendBytes:&whole_byte length:1];
    }
    return commandToSend;
}
```
另一种
```
- (NSData *)convertHexStrToData:(NSString *)str
{
    if (!str || [str length] == 0) {
        return nil;
    }
    
    NSMutableData *hexData = [[NSMutableData alloc] initWithCapacity:20];
    NSRange range;
    if ([str length] % 2 == 0) {
        range = NSMakeRange(0, 2);
    } else {
        range = NSMakeRange(0, 1);
    }
    for (NSInteger i = range.location; i < [str length]; i += 2) {
        unsigned int anInt;
        NSString *hexCharStr = [str substringWithRange:range];
        NSScanner *scanner = [[NSScanner alloc] initWithString:hexCharStr];
        
        [scanner scanHexInt:&anInt];
        NSData *entity = [[NSData alloc] initWithBytes:&anInt length:1];
        [hexData appendData:entity];
        
        range.location += range.length;
        range.length = 2;
    }
    return hexData;
}
```
