UITabbarItem push pop回来，title颜色会改为默认色
iOS 13 前可设置
```
UITabBarItem *item = [[UITabBarItem alloc] initWithTitle:tabBarItemTitles[index]
                                                           image:unselectedimage
                                                   selectedImage:selectedimage];
        
        [item setTitleTextAttributes:@{NSForegroundColorAttributeName : [UIColor]} forState:UIControlStateSelected];
        
        [item setTitleTextAttributes:@{NSForegroundColorAttributeName : [UIColor]} forState:UIControlStateNormal];
```
iOS 13 后 设置
```
tabBarController.tabBar.tintColor = [UIColor ];
    tabBarController.tabBar.unselectedItemTintColor = [UIColor];
```
UITabbar 去掉 shadowImage
iOS 13前
```
[tabBarController.tabBar setShadowImage:[[UIImage alloc]init]];
    [tabBarController.tabBar setBackgroundImage:[UIImage ] size: i]];
```
iOS 13 后
```
UITabBarAppearance *appearance = [self.tabBar.standardAppearance copy];
        appearance.backgroundImage = [UIImage new];
        appearance.shadowImage = [UIImage];
        appearance.shadowColor = [UIColor clearColor];
        self.tabBar.standardAppearance = appearance;
```
注意，iOS 13后用新的api去掉黑线, 我这里不能单独设置每个 tabbarItem badgeColor，所以我没有采用这种,
使用了古老的遍历查找remove, 以下代码使用时注意自己看下试图结构，适当修改,目前仅适合iOS 13 12, Swift未更新，自行根据oc修改，以后升级可能有改变，慎用
OC
```
for (UIView *tabbarSubView in self.tabBarController.tabBar.subviews) {
        NSString *name = NSStringFromClass([tabbarSubView class]);
        if ([name containsString:@"_UIBarBackground"]) { // 找到整个的背景
            for (UIView *tempView in tabbarSubView.subviews) {
              // 模拟器上只看到这个
                if ([tempView isKindOfClass:[UIImageView class]]) {
                    [tempView removeFromSuperview];
                }
              // 真机还看到这个
                NSString *tempName = NSStringFromClass([tempView class]);
                if ([tempName containsString:@"_UIBarBackgroundShadowView"]) {
                    [tempView removeFromSuperview];
                    break;
                }
            }
            break;
        }
    }
```
Swift
```
for tabbarSubView in tabBarController?.tabBar.subviews ?? [] {
            let name = NSStringFromClass(tabbarSubView.classForCoder)
            if name.contains("_UIBarBackground") {
                for tempView in tabbarSubView.subviews {
                    let tempName = NSStringFromClass(tempView.classForCoder)
                    if tempName.contains("_UIBarBackgroundShadowView") {
                        tempView.removeFromSuperview()
                        break
                    }
                }
                break
            }
        }
```
