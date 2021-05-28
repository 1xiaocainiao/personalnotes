```
import 'package:flutter/material.dart' hide NestedScrollView;
import 'package:extended_nested_scroll_view/extended_nested_scroll_view.dart';


Widget _body(BuildContext context) {
    return BlocConsumer<LifeMomentContainerBloc, LifeMomentContainerState>(
        listener: (context, state) {},
        builder: (context, state) {
          return NestedScrollView(
            controller: _scrollController,
            headerSliverBuilder: (con, boxIsScrolled) {
              return _sliverBuilder(context, boxIsScrolled);
            },
            body: Column(
              children: [
                _childTabBody(context),
                Expanded(child: _scrollViewBody(context)),
              ],
            ),
            innerScrollPositionKeyBuilder: () {
              var index = "Tab";
              index += (_tabController.index.toString());
              return Key(index);
            },
          );
        });
  }


  List<Widget> _sliverBuilder(BuildContext context, bool boxIsScrolled) {
    final state = BlocProvider.of<LifeMomentContainerBloc>(context).state;

    final height = state.hotStroyIsEmpty ? 0.0 : HomeHotHorizontalHeight;

    return [
      SliverAppBar(
        pinned: false,
        floating: false,
        expandedHeight: height,
        toolbarHeight: height,
        flexibleSpace: StoryHorizontalPage(),
      ),
    ];
  }

  double _tabbarHeight() {
    return 67.0;
  }

  Widget _childTabBody(BuildContext context) {
    return PreferredSize(
        preferredSize: Size(MediaQuery.of(context).size.width, _tabbarHeight()),
        child: Column(
          children: [
            Container(height: 1.0, color: c4),
            Container(
              color: c1,
              // color: Colors.transparent,
              padding:
                  const EdgeInsets.only(top: 24.0, left: 16.0, bottom: 16.0),
              width: MediaQuery.of(context).size.width,
              child: _newOrNearbyButton(),
            ),
          ],
        ));
  }

//保持各自滚动,不会相互影响
  Widget _scrollViewBody(BuildContext context) {
    final state = BlocProvider.of<LifeMomentContainerBloc>(context).state;

    return TabBarView(
      controller: _tabController,
      physics: NeverScrollableScrollPhysics(),
      children: [
        NestedScrollViewInnerScrollPositionKeyWidget(
          const Key("Tab0"),
          NewMomentListPage(
            isNew: true,
          ),
        ),
        NestedScrollViewInnerScrollPositionKeyWidget(
          const Key("Tab1"),
          NewMomentListPage(
            isNew: false,
          ),
        ),
      ],
    );
  }
```
