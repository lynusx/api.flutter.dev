@docImport 'package:flutter/material.dart';

@docImport 'single_child_scroll_view.dart'; @docImport 'text.dart';

# PageController

```dart
class PageController extends ScrollController {}
```

A controller for [PageView].

A page controller lets you manipulate which page is visible in a [PageView]. In addition to being able to control the pixel offset of the content inside the [PageView], a [PageController] also lets you control the offset in terms of pages, which are increments of the viewport size.

See also:

- [PageView], which is the widget this object controls.

{@tool snippet}

This widget introduces a [MaterialApp], [Scaffold] and [PageView] with two pages using the default constructor. Both pages contain an [ElevatedButton] allowing you to animate the [PageView] using a [PageController].

```dart
class MyPageView extends StatefulWidget {
  const MyPageView({super.key});

  @override
  State<MyPageView> createState() => _MyPageViewState();
}

class _MyPageViewState extends State<MyPageView> {
  final PageController _pageController = PageController();

  @override
  void dispose() {
    _pageController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: PageView(
          controller: _pageController,
          children: <Widget>[
            ColoredBox(
              color: Colors.red,
              child: Center(
                child: ElevatedButton(
                  onPressed: () {
                    if (_pageController.hasClients) {
                      _pageController.animateToPage(
                        1,
                        duration: const Duration(milliseconds: 400),
                        curve: Curves.easeInOut,
                      );
                    }
                  },
                  child: const Text('Next'),
                ),
              ),
            ),
            ColoredBox(
              color: Colors.blue,
              child: Center(
                child: ElevatedButton(
                  onPressed: () {
                    if (_pageController.hasClients) {
                      _pageController.animateToPage(
                        0,
                        duration: const Duration(milliseconds: 400),
                        curve: Curves.easeInOut,
                      );
                    }
                  },
                  child: const Text('Previous'),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

{@end-tool}

### PageController()

```dart
PageController({int initialPage = 0, bool keepPage = true, double viewportFraction = 1.0, void Function(ScrollPosition)? onAttach, void Function(ScrollPosition)? onDetach})
```

Creates a page controller.

### initialPage

```dart
int initialPage
```

The page to show when first creating the [PageView].

### keepPage

```dart
bool keepPage
```

Save the current [page] with [PageStorage] and restore it if this controller's scrollable is recreated.

If this property is set to false, the current [page] is never saved and [initialPage] is always used to initialize the scroll offset. If true (the default), the initial page is used the first time the controller's scrollable is created, since there's isn't a page to restore yet. Subsequently the saved page is restored and [initialPage] is ignored.

See also:

- [PageStorageKey], which should be used when more than one scrollable appears in the same route, to distinguish the [PageStorage] locations used to save scroll offsets.

### viewportFraction

```dart
double viewportFraction
```

{@template flutter.widgets.pageview.viewportFraction} The fraction of the viewport that each page should occupy.

Defaults to 1.0, which means each page fills the viewport in the scrolling direction. {@endtemplate}

### page

```dart
double? get page
```

The current page displayed in the controlled [PageView].

There are circumstances that this [PageController] can't know the current page. Reading [page] will throw an [AssertionError] in the following cases:

1.  No [PageView] is currently using this [PageController]. Once a [PageView] starts using this [PageController], the new [page] position will be derived:

- First, based on the attached [PageView]'s [BuildContext] and the position saved at that context's [PageStorage] if [keepPage] is true.
- Second, from the [PageController]'s [initialPage].

2.  More than one [PageView] using the same [PageController].

The [hasClients] property can be used to check if a [PageView] is attached prior to accessing [page].

### animateToPage()

```dart
Future<void> animateToPage(int page, {required Duration duration, required Curve curve})
```

Animates the controlled [PageView] from the current page to the given page.

The animation lasts for the given duration and follows the given curve. The returned [Future] resolves when the animation completes.

### jumpToPage()

```dart
void jumpToPage(int page)
```

Changes which page is displayed in the controlled [PageView].

Jumps the page position from its current value to the given value, without animation, and without checking if the new value is in range.

### nextPage()

```dart
Future<void> nextPage({required Duration duration, required Curve curve})
```

Animates the controlled [PageView] to the next page.

The animation lasts for the given duration and follows the given curve. The returned [Future] resolves when the animation completes.

### previousPage()

```dart
Future<void> previousPage({required Duration duration, required Curve curve})
```

Animates the controlled [PageView] to the previous page.

The animation lasts for the given duration and follows the given curve. The returned [Future] resolves when the animation completes.

### createScrollPosition()

```dart
ScrollPosition createScrollPosition(ScrollPhysics physics, ScrollContext context, ScrollPosition? oldPosition)
```

### attach()

```dart
void attach(ScrollPosition position)
```

# PageMetrics

```dart
class PageMetrics extends FixedScrollMetrics {}
```

Metrics for a [PageView].

The metrics are available on [ScrollNotification]s generated from [PageView]s.

### PageMetrics()

```dart
PageMetrics({required double? minScrollExtent, required double? maxScrollExtent, required double? pixels, required double? viewportDimension, required dynamic axisDirection, required double viewportFraction, required double devicePixelRatio})
```

Creates an immutable snapshot of values associated with a [PageView].

### copyWith()

```dart
PageMetrics copyWith({double? minScrollExtent, double? maxScrollExtent, double? pixels, double? viewportDimension, AxisDirection? axisDirection, double? viewportFraction, double? devicePixelRatio})
```

### page

```dart
double? get page
```

The current page displayed in the [PageView].

### viewportFraction

```dart
double viewportFraction
```

The fraction of the viewport that each page occupies.

Used to compute [page] from the current [pixels].

# PageScrollPhysics

```dart
class PageScrollPhysics extends ScrollPhysics {}
```

Scroll physics used by a [PageView].

These physics cause the page view to snap to page boundaries.

See also:

- [ScrollPhysics], the base class which defines the API for scrolling physics.
- [PageView.physics], which can override the physics used by a page view.

### PageScrollPhysics()

```dart
PageScrollPhysics({ScrollPhysics? parent})
```

Creates physics for a [PageView].

### applyTo()

```dart
PageScrollPhysics applyTo(ScrollPhysics? ancestor)
```

### createBallisticSimulation()

```dart
Simulation? createBallisticSimulation(ScrollMetrics position, double velocity)
```

### allowImplicitScrolling

```dart
bool get allowImplicitScrolling
```

# PageView

```dart
class PageView extends StatefulWidget {}
```

A scrollable list that works page by page.

Each child of a page view is forced to be the same size as the viewport.

You can use a [PageController] to control which page is visible in the view. In addition to being able to control the pixel offset of the content inside the [PageView], a [PageController] also lets you control the offset in terms of pages, which are increments of the viewport size.

The [PageController] can also be used to control the [PageController.initialPage], which determines which page is shown when the [PageView] is first constructed, and the [PageController.viewportFraction], which determines the size of the pages as a fraction of the viewport size.

{@youtube 560 315 https://www.youtube.com/watch?v=J1gE9xvph-A}

{@tool dartpad} Here is an example of [PageView]. It creates a centered [Text] in each of the three pages which scroll horizontally.

** See code in examples/api/lib/widgets/page_view/page_view.0.dart ** {@end-tool}

## Persisting the scroll position during a session

Scroll views attempt to persist their scroll position using [PageStorage]. For a [PageView], this can be disabled by setting [PageController.keepPage] to false on the [controller]. If it is enabled, using a [PageStorageKey] for the [key] of this widget is recommended to help disambiguate different scroll views from each other.

See also:

- [PageController], which controls which page is visible in the view.
- [SingleChildScrollView], when you need to make a single child scrollable.
- [ListView], for a scrollable list of boxes.
- [GridView], for a scrollable grid of boxes.
- [ScrollNotification] and [NotificationListener], which can be used to watch the scroll position without using a [ScrollController].

### PageView()

```dart
PageView({dynamic key, Axis scrollDirection = Axis.horizontal, bool reverse = false, PageController? controller, ScrollPhysics? physics, bool pageSnapping = true, ValueChanged<int>? onPageChanged, List<Widget> children = const <Widget>[], DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool allowImplicitScrolling = false, ScrollCacheExtent? scrollCacheExtent, String? restorationId, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, ScrollBehavior? scrollBehavior, bool padEnds = true})
```

Creates a scrollable list that works page by page from an explicit [List] of widgets.

This constructor is appropriate for page views with a small number of children because constructing the [List] requires doing work for every child that could possibly be displayed in the page view, instead of just those children that are actually visible.

Like other widgets in the framework, this widget expects that the [children] list will not be mutated after it has been passed in here. See the documentation at [SliverChildListDelegate.children] for more details.

{@template flutter.widgets.PageView.allowImplicitScrolling} If [allowImplicitScrolling] is true, the [PageView] will participate in accessibility scrolling more like a [ListView], where implicit scroll actions will move to the next page rather than into the contents of the [PageView]. {@endtemplate}

### PageView.builder()

```dart
PageView.builder({dynamic key, Axis scrollDirection = Axis.horizontal, bool reverse = false, PageController? controller, ScrollPhysics? physics, bool pageSnapping = true, ValueChanged<int>? onPageChanged, required NullableIndexedWidgetBuilder itemBuilder, ChildIndexGetter? findChildIndexCallback, int? itemCount, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool allowImplicitScrolling = false, ScrollCacheExtent? scrollCacheExtent, String? restorationId, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, ScrollBehavior? scrollBehavior, bool padEnds = true})
```

Creates a scrollable list that works page by page using widgets that are created on demand.

This constructor is appropriate for page views with a large (or infinite) number of children because the builder is called only for those children that are actually visible.

Providing a non-null [itemCount] lets the [PageView] compute the maximum scroll extent.

[itemBuilder] will be called only with indices greater than or equal to zero and less than [itemCount].

{@macro flutter.widgets.ListView.builder.itemBuilder}

{@template flutter.widgets.PageView.findChildIndexCallback} The [findChildIndexCallback] corresponds to the [SliverChildBuilderDelegate.findChildIndexCallback] property. If null, a child widget may not map to its existing [RenderObject] when the order of children returned from the children builder changes. This may result in state-loss. This callback needs to be implemented if the order of the children may change at a later time. {@endtemplate}

{@macro flutter.widgets.PageView.allowImplicitScrolling}

### PageView.custom()

```dart
PageView.custom({dynamic key, Axis scrollDirection = Axis.horizontal, bool reverse = false, PageController? controller, ScrollPhysics? physics, bool pageSnapping = true, ValueChanged<int>? onPageChanged, required SliverChildDelegate childrenDelegate, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool allowImplicitScrolling = false, ScrollCacheExtent? scrollCacheExtent, String? restorationId, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, ScrollBehavior? scrollBehavior, bool padEnds = true})
```

Creates a scrollable list that works page by page with a custom child model.

{@tool dartpad} This example shows a [PageView] that uses a custom [SliverChildBuilderDelegate] to support child reordering.

** See code in examples/api/lib/widgets/page_view/page_view.1.dart ** {@end-tool}

{@macro flutter.widgets.PageView.allowImplicitScrolling}

### allowImplicitScrolling

```dart
bool allowImplicitScrolling
```

{@template flutter.widgets.PageView.allowImplicitScrolling} Controls whether the widget's pages will respond to [RenderObject.showOnScreen], which will allow for implicit accessibility scrolling.

With this flag set to false, when accessibility focus reaches the end of the current page and the user attempts to move it to the next element, the focus will traverse to the next widget outside of the page view.

With this flag set to true, when accessibility focus reaches the end of the current page and user attempts to move it to the next element, focus will traverse to the next page in the page view. {@endtemplate}

### scrollCacheExtent

```dart
ScrollCacheExtent scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

In [PageView], the default [scrollCacheExtent] uses [ScrollCacheExtent.viewport], where the value represents the number of viewport lengths to cache beyond the visible area.

When [PageController.viewportFraction] is 1.0 (the default), this is equivalent to the number of pages. For example, `ScrollCacheExtent.viewport(2.0)` caches 2 pages before and after the visible page.

When [PageController.viewportFraction] is less than 1.0, multiple pages may be visible in a single viewport, so `ScrollCacheExtent.viewport(1.0)` may cache more than one additional page in each direction.

[ScrollCacheExtent.pixels] can also be used to specify the cache extent in logical pixels instead of viewport sizes.

If [scrollCacheExtent] is specified, its value must be consistent with [allowImplicitScrolling]: the value must be greater than 0.0 when [allowImplicitScrolling] is true, and must be 0.0 when [allowImplicitScrolling] is false.

Defaults to `ScrollCacheExtent.viewport(1.0)` if [allowImplicitScrolling] is true, and `ScrollCacheExtent.viewport(0.0)` if [allowImplicitScrolling] is false.

### restorationId

```dart
String? restorationId
```

{@macro flutter.widgets.scrollable.restorationId}

### scrollDirection

```dart
Axis scrollDirection
```

The [Axis] along which the scroll view's offset increases with each page.

For the direction in which active scrolling may be occurring, see [ScrollDirection].

Defaults to [Axis.horizontal].

### reverse

```dart
bool reverse
```

Whether the page view scrolls in the reading direction.

For example, if the reading direction is left-to-right and [scrollDirection] is [Axis.horizontal], then the page view scrolls from left to right when [reverse] is false and from right to left when [reverse] is true.

Similarly, if [scrollDirection] is [Axis.vertical], then the page view scrolls from top to bottom when [reverse] is false and from bottom to top when [reverse] is true.

Defaults to false.

### controller

```dart
PageController? controller
```

An object that can be used to control the position to which this page view is scrolled.

### physics

```dart
ScrollPhysics? physics
```

How the page view should respond to user input.

For example, determines how the page view continues to animate after the user stops dragging the page view.

The physics are modified to snap to page boundaries using [PageScrollPhysics] prior to being used.

If an explicit [ScrollBehavior] is provided to [scrollBehavior], the [ScrollPhysics] provided by that behavior will take precedence after [physics].

Defaults to matching platform conventions.

### pageSnapping

```dart
bool pageSnapping
```

Set to false to disable page snapping, useful for custom scroll behavior.

If the [padEnds] is false and [PageController.viewportFraction] < 1.0, the page will snap to the beginning of the viewport; otherwise, the page will snap to the center of the viewport.

### onPageChanged

```dart
ValueChanged<int>? onPageChanged
```

Called whenever the page in the center of the viewport changes.

### childrenDelegate

```dart
SliverChildDelegate childrenDelegate
```

A delegate that provides the children for the [PageView].

The [PageView.custom] constructor lets you specify this delegate explicitly. The [PageView] and [PageView.builder] constructors create a [childrenDelegate] that wraps the given [List] and [IndexedWidgetBuilder], respectively.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.scrollable.hitTestBehavior}

Defaults to [HitTestBehavior.opaque].

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@macro flutter.widgets.scrollable.scrollBehavior}

The [ScrollBehavior] of the inherited [ScrollConfiguration] will be modified by default to not apply a [Scrollbar].

### padEnds

```dart
bool padEnds
```

Whether to add padding to both ends of the list.

If this is set to true and [PageController.viewportFraction] < 1.0, padding will be added such that the first and last child slivers will be in the center of the viewport when scrolled all the way to the start or end, respectively.

If [PageController.viewportFraction] >= 1.0, this property has no effect.

This property defaults to true.

### createState()

```dart
State<PageView> createState()
```
