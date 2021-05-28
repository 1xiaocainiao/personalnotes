当column嵌套column时，内部column必须要能确定高度
如
```
Column(
                        mainAxisAlignment: MainAxisAlignment.start,
                        crossAxisAlignment: CrossAxisAlignment.start,
                        mainAxisSize: MainAxisSize.min,
                        children: [
                          phraseBar(),
                        ],
                      )
```
```
Widget phraseBar() {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        _tipsText(),
        Container(
          height: itemHeight + vPadding * 2,
          child: _phraseList(),
        )
      ],
    );
  }
```
上面第二个column中高度必须要能够确定，否则会出错

