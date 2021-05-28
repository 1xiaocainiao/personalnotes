当需要popUntil 到首页的时候有两种方式
```
Navigator.of(context).popUntil((route) => route.isFirst);
```
以及
```
Navigator.popUntil(
          context,
          ModalRoute.withName(Navigator.defaultRouteName),
        );
```
我使用第二种方式时，出现了黑屏，原因是退出登录，以及登录的地方使用了pushNamedAndRemoveUntil，所以后面改为使用第一种方式返回首页，就不会黑屏了
