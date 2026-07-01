@docImport 'color_scheme.dart';

# RefreshCallback

```dart
typedef RefreshCallback = Future<void> Function()
```

The signature for a function that's called when the user has dragged a [RefreshIndicator] far enough to demonstrate that they want the app to refresh. The returned [Future] must complete when the refresh operation is finished.

Used by [RefreshIndicator.onRefresh].

# RefreshIndicatorStatus

```dart
enum RefreshIndicatorStatus {}
```

Indicates current status of Material `RefreshIndicator`.

Pointer is down.

Dragged far enough that an up event will run the onRefresh callback.

Animating to the indicator's final "displacement".

Running the refresh callback.

Animating the indicator's fade-out after refreshing.

Animating the indicator's fade-out after not arming.

# RefreshIndicatorTriggerMode

```dart
enum RefreshIndicatorTriggerMode {}
```

Used to configure how [RefreshIndicator] can be triggered.

The indicator can be triggered regardless of the scroll position of the [Scrollable] when the drag starts.

The indicator can only be triggered if the [Scrollable] is at the edge when the drag starts.

# RefreshIndicator

```dart
class RefreshIndicator extends StatefulWidget {}
```

A widget that supports the Material "swipe to refresh" idiom.

{@youtube 560 315 https://www.youtube.com/watch?v=ORApMlzwMdM}

When the child's [Scrollable] descendant overscrolls, an animated circular progress indicator is faded into view. When the scroll ends, if the indicator has been dragged far enough for it to become completely opaque, the [onRefresh] callback is called. The callback is expected to update the scrollable's contents and then complete the [Future] it returns. The refresh indicator disappears after the callback's [Future] has completed.

The trigger mode is configured by [RefreshIndicator.triggerMode].

{@tool dartpad} This example shows how [RefreshIndicator] can be triggered in different ways.

** See code in examples/api/lib/material/refresh_indicator/refresh_indicator.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to trigger [RefreshIndicator] in a nested scroll view using the [notificationPredicate] property.

** See code in examples/api/lib/material/refresh_indicator/refresh_indicator.1.dart ** {@end-tool}

{@tool dartpad} This example shows how to use [RefreshIndicator] without the spinner.

** See code in examples/api/lib/material/refresh_indicator/refresh_indicator.2.dart ** {@end-tool}

## Troubleshooting

### Refresh indicator does not show up

The [RefreshIndicator] will appear if its scrollable descendant can be overscrolled, i.e. if the scrollable's content is bigger than its viewport. To ensure that the [RefreshIndicator] will always appear, even if the scrollable's content fits within its viewport, set the scrollable's [Scrollable.physics] property to [AlwaysScrollableScrollPhysics]:

```dart
ListView(
  physics: const AlwaysScrollableScrollPhysics(),
  // ...
)
```

A [RefreshIndicator] can only be used with a vertical scroll view.

See also:

- <https://material.io/design/platform-guidance/android-swipe-to-refresh.html>
- [RefreshIndicatorState], can be used to programmatically show the refresh indicator.
- [RefreshProgressIndicator], widget used by [RefreshIndicator] to show the inner circular progress spinner during refreshes.
- [CupertinoSliverRefreshControl], an iOS equivalent of the pull-to-refresh pattern. Must be used as a sliver inside a [CustomScrollView] instead of wrapping around a [ScrollView] because it's a part of the scrollable instead of being overlaid on top of it.

### RefreshIndicator()

```dart
RefreshIndicator({dynamic key, double displacement = 40.0, double edgeOffset = 0.0, required RefreshCallback onRefresh, Color? color, Color? backgroundColor, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, String? semanticsLabel, String? semanticsValue, double strokeWidth = RefreshProgressIndicator.defaultStrokeWidth, RefreshIndicatorTriggerMode triggerMode = RefreshIndicatorTriggerMode.onEdge, double elevation = 2.0, required Widget child})
```

Creates a refresh indicator.

The [onRefresh], [child], and [notificationPredicate] arguments must be non-null. The default [displacement] is 40.0 logical pixels.

The [semanticsLabel] is used to specify an accessibility label for this widget. If it is null, it will be defaulted to [MaterialLocalizations.refreshIndicatorSemanticLabel]. An empty string may be passed to avoid having anything read by screen reading software. The [semanticsValue] may be used to specify progress on the widget.

### RefreshIndicator.adaptive()

```dart
RefreshIndicator.adaptive({dynamic key, double displacement = 40.0, double edgeOffset = 0.0, required RefreshCallback onRefresh, Color? color, Color? backgroundColor, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, String? semanticsLabel, String? semanticsValue, double strokeWidth = RefreshProgressIndicator.defaultStrokeWidth, RefreshIndicatorTriggerMode triggerMode = RefreshIndicatorTriggerMode.onEdge, double elevation = 2.0, required Widget child})
```

Creates an adaptive [RefreshIndicator] based on whether the target platform is iOS or macOS, following Material design's [Cross-platform guidelines](https://material.io/design/platform-guidance/cross-platform-adaptation.html).

When the descendant overscrolls, a different spinning progress indicator is shown depending on platform. On iOS and macOS, [CupertinoActivityIndicator] is shown, but on all other platforms, [CircularProgressIndicator] appears.

If a [CupertinoActivityIndicator] is shown, the following parameters are ignored: [backgroundColor], [semanticsLabel], [semanticsValue], [strokeWidth].

The target platform is based on the current [Theme]: [ThemeData.platform].

Notably the scrollable widget itself will have slightly different behavior from [CupertinoSliverRefreshControl], due to a difference in structure.

### RefreshIndicator.noSpinner()

```dart
RefreshIndicator.noSpinner({dynamic key, required RefreshCallback onRefresh, ValueChanged<RefreshIndicatorStatus?>? onStatusChange, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, String? semanticsLabel, String? semanticsValue, RefreshIndicatorTriggerMode triggerMode = RefreshIndicatorTriggerMode.onEdge, double elevation = 2.0, required Widget child})
```

Creates a [RefreshIndicator] with no spinner and calls `onRefresh` when successfully armed by a drag event.

Events can be optionally listened by using the `onStatusChange` callback.

### child

```dart
Widget child
```

The widget below this widget in the tree.

The refresh indicator will be stacked on top of this child. The indicator will appear when child's Scrollable descendant is over-scrolled.

Typically a [ListView] or [CustomScrollView].

### displacement

```dart
double displacement
```

The distance from the child's top or bottom [edgeOffset] where the refresh indicator will settle. During the drag that exposes the refresh indicator, its actual displacement may significantly exceed this value.

In most cases, [displacement] distance starts counting from the parent's edges. However, if [edgeOffset] is larger than zero then the [displacement] value is calculated from that offset instead of the parent's edge.

### edgeOffset

```dart
double edgeOffset
```

The offset where [RefreshProgressIndicator] starts to appear on drag start.

Depending whether the indicator is showing on the top or bottom, the value of this variable controls how far from the parent's edge the progress indicator starts to appear. This may come in handy when, for example, the UI contains a top [Widget] which covers the parent's edge where the progress indicator would otherwise appear.

By default, the edge offset is set to 0.

See also:

- [displacement], can be used to change the distance from the edge that the indicator settles.

### onRefresh

```dart
RefreshCallback onRefresh
```

A function that's called when the user has dragged the refresh indicator far enough to demonstrate that they want the app to refresh. The returned [Future] must complete when the refresh operation is finished.

### onStatusChange

```dart
ValueChanged<RefreshIndicatorStatus?>? onStatusChange
```

Called to get the current status of the [RefreshIndicator] to update the UI as needed. This is an optional parameter, used to fine tune app cases.

### color

```dart
Color? color
```

The progress indicator's foreground color. The current theme's [ColorScheme.primary] by default.

### backgroundColor

```dart
Color? backgroundColor
```

The progress indicator's background color. The current theme's [ThemeData.canvasColor] by default.

### notificationPredicate

```dart
ScrollNotificationPredicate notificationPredicate
```

A check that specifies whether a [ScrollNotification] should be handled by this widget.

By default, checks whether `notification.depth == 0`. Set it to something else for more complicated layouts.

### semanticsLabel

```dart
String? semanticsLabel
```

{@macro flutter.progress_indicator.ProgressIndicator.semanticsLabel}

This will be defaulted to [MaterialLocalizations.refreshIndicatorSemanticLabel] if it is null.

### semanticsValue

```dart
String? semanticsValue
```

{@macro flutter.progress_indicator.ProgressIndicator.semanticsValue}

### strokeWidth

```dart
double strokeWidth
```

Defines [strokeWidth] for `RefreshIndicator`.

By default, the value of [strokeWidth] is 2.0 pixels.

### triggerMode

```dart
RefreshIndicatorTriggerMode triggerMode
```

Defines how this [RefreshIndicator] can be triggered when users overscroll.

The [RefreshIndicator] can be pulled out in two cases, 1, Keep dragging if the scrollable widget at the edge with zero scroll position when the drag starts. 2, Keep dragging after overscroll occurs if the scrollable widget has a non-zero scroll position when the drag starts.

If this is [RefreshIndicatorTriggerMode.anywhere], both of the cases above can be triggered.

If this is [RefreshIndicatorTriggerMode.onEdge], only case 1 can be triggered.

Defaults to [RefreshIndicatorTriggerMode.onEdge].

### elevation

```dart
double elevation
```

Defines the elevation of the underlying [RefreshIndicator].

Defaults to 2.0.

### createState()

```dart
RefreshIndicatorState createState()
```

# RefreshIndicatorState

```dart
class RefreshIndicatorState extends State<RefreshIndicator> with TickerProviderStateMixin<RefreshIndicator> {}
```

Contains the state for a [RefreshIndicator]. This class can be used to programmatically show the refresh indicator, see the [show] method.

### initState()

```dart
void initState()
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(RefreshIndicator oldWidget)
```

### dispose()

```dart
void dispose()
```

### show()

```dart
Future<void> show({bool atTop = true})
```

Show the refresh indicator and run the refresh callback as if it had been started interactively. If this method is called while the refresh callback is running, it quietly does nothing.

Creating the [RefreshIndicator] with a [GlobalKey<RefreshIndicatorState>] makes it possible to refer to the [RefreshIndicatorState].

The future returned from this method completes when the [RefreshIndicator.onRefresh] callback's future completes.

If you await the future returned by this function from a [State], you should check that the state is still [mounted] before calling [setState].

When initiated in this manner, the refresh indicator is independent of any actual scroll view. It defaults to showing the indicator at the top. To show it at the bottom, set `atTop` to false.

### build()

```dart
Widget build(BuildContext context)
```
