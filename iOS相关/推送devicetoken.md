Swift
```
let token = deviceToken.reduce("") { $0 + String(format: "%02x", $1) }
```

OC
```
NSString *token = [[[[deviceToken description] stringByReplacingOccurrencesOfString:@"<"
                                                                             withString:@""]
                        stringByReplacingOccurrencesOfString:@">"
                        withString:@""]
                       stringByReplacingOccurrencesOfString:@" "
                       withString:@""];
```
