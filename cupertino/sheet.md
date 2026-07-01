# showCupertinoSheet()

```dart
Future<T?> showCupertinoSheet<T>({required BuildContext context, WidgetBuilder? pageBuilder, WidgetBuilder? builder, ScrollableWidgetBuilder? scrollableBuilder, bool useNestedNavigation = false, bool enableDrag = true, RouteSettings? settings, double? topGap, bool showDragHandle = false})
```

Shows a Cupertino-style sheet widget that slides up from the bottom of the screen and stacks the previous route behind the new sheet.

{@youtube 560 315 https://www.youtube.com/watch?v=5H-WvH5O29I}

This is a convenience method for displaying [CupertinoSheetRoute] for most use cases. The Widget returned from `scrollableBuilder` will be used to display the content on the [CupertinoSheetRoute]. If the content of the sheet has a scrollable view, the [ScrollController] provided by `scrollableBuilder` can be used to enable the drag-to-dimiss gesture to work with the scrolling of the content. See [CupertinoSheetRoute.scrollableBuilder] for an example.

`useNestedNavigation` allows new routes to be pushed inside of a [CupertinoSheetRoute] by adding a new [Navigator] inside of the [CupertinoSheetRoute].

When `useNestedNavigation` is set to `true`, any route pushed to the stack from within the context of the [CupertinoSheetRoute] will display within that sheet. System back gestures and programmatic pops on the initial route in a sheet will also be intercepted to pop the whole [CupertinoSheetRoute]. If a custom [Navigator] setup is needed, like for example to enable named routes or the pages API, then it is recommended to directly push a [CupertinoSheetRoute] to the stack with whatever configuration needed. See [CupertinoSheetRoute] for an example that manually sets up nested navigation.

The whole sheet can be popped at once by either dragging down on the sheet, or calling [CupertinoSheetRoute.popSheet].

When `enableDrag` is set to `true` (the default), users can dismiss the sheet by dragging it down or by calling [CupertinoSheetRoute.popSheet]. When `enableDrag` is `false`, users cannot dismiss the sheet by dragging, and it can only be closed by calling [CupertinoSheetRoute.popSheet].

The `topGap` parameter can be used to customize the gap between the top of the screen and the top of the sheet as a ratio of the screen height. It should be a value between 0.0 and 0.9, where 0.0 means no gap and 0.9 means the sheet takes up only the bottom 10% of the screen. If not provided, defaults to 0.08 (8% of screen height).

When `showDragHandle` is set to `true`, then a drag handle will be placed at the top of the sheet. This flag will default to false.

iOS sheet widgets are generally designed to be tightly coupled to the context of the widget that opened the sheet. As such, it is not recommended to push a non-sheet route that covers the sheet without first popping the sheet. If necessary however, it can be done by pushing to the root [Navigator].

If `useNestedNavigation` is `false` (the default), then a [CupertinoSheetRoute] will be shown with no [Navigator] widget. Multiple calls to `showCupertinoSheet` can still be made to show multiple stacked sheets, if desired.

`showCupertinoSheet` always pushes the [CupertinoSheetRoute] to the root [Navigator]. This is to ensure the previous route animates correctly.

Returns a [Future] that resolves to the value (if any) that was passed to [Navigator.pop] when the sheet was closed.

{@tool dartpad} This example shows how to navigate to use [showCupertinoSheet] to display a Cupertino sheet widget with nested navigation.

** See code in examples/api/lib/cupertino/sheet/cupertino_sheet.1.dart ** {@end-tool}

See also:

- [CupertinoSheetRoute] the basic route version of the sheet view.
- [showCupertinoDialog] which displays an iOS-styled dialog.
- <https://developer.apple.com/design/human-interface-guidelines/sheets>

# CupertinoSheetTransition

```dart
class CupertinoSheetTransition extends StatefulWidget {}
```

Provides an iOS-style sheet transition.

The page slides up and stops below the top of the screen. When covered by another sheet view, it will slide slightly up and scale down to appear stacked behind the new sheet.

### CupertinoSheetTransition()

```dart
CupertinoSheetTransition({dynamic key, required Animation<double> primaryRouteAnimation, required Animation<double> secondaryRouteAnimation, required Widget child, required bool linearTransition, double topGap = _kTopGapRatio})
```

Creates an iOS style sheet transition.

### primaryRouteAnimation

```dart
Animation<double> primaryRouteAnimation
```

`primaryRouteAnimation` is a linear route animation from 0.0 to 1.0 when this screen is being pushed.

### secondaryRouteAnimation

```dart
Animation<double> secondaryRouteAnimation
```

`secondaryRouteAnimation` is a linear route animation from 0.0 to 1.0 when another screen is being pushed on top of this one.

### child

```dart
Widget child
```

The widget below this widget in the tree.

### linearTransition

```dart
bool linearTransition
```

Whether to perform the transition linearly.

Used to respond to a drag gesture.

### topGap

```dart
double topGap
```

The gap between the top of the screen and the top of the sheet as a ratio of the screen height.

{@template flutter.cupertino.CupertinoSheetTransition.topGap} This value should be between 0.0 and 0.9, where 0.0 means no gap (sheet extends to the top of the screen) and 0.9 means the sheet covers only the bottom 10% of the screen. A value of 0.08 represents 8% of the screen height.

If not provided, defaults to a value of 0.08. {@endtemplate}

### delegateTransition()

```dart
Widget delegateTransition(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, bool allowSnapshotting, Widget? child)
```

The primary delegated transition. Will slide a non [CupertinoSheetRoute] page down.

Provided to the previous route to coordinate transitions between routes.

If a [CupertinoSheetRoute] already exists in the stack, then it will slide the previous sheet upwards instead.

### createState()

```dart
State<CupertinoSheetTransition> createState()
```

# CupertinoSheetRoute

```dart
class CupertinoSheetRoute<T> extends PageRoute<T> with _CupertinoSheetRouteTransitionMixin<T> {}
```

Route for displaying an iOS sheet styled page.

{@youtube 560 315 https://www.youtube.com/watch?v=5H-WvH5O29I}

The `CupertinoSheetRoute` will slide up from the bottom of the screen and stop below the top of the screen. If the previous route is a non-sheet route, then it will animate downwards to stack behind the new sheet. If the previous route is a sheet route, then it will animate slightly upwards to look like it is laying on top of the previous stack of sheets.

Typically called by [showCupertinoSheet], which provides some boilerplate for pushing the `CupertinoSheetRoute` to the root navigator and providing simple nested navigation.

The sheet will be dismissed by dragging downwards on the screen, or a call to [CupertinoSheetRoute.popSheet].

Any time a CupertinoSheetRoute contains a large scrollable that might conflict with the dismiss drag gesture, pass the provided [ScrollController] from `scrollableBuilder` to the scrollable. A scrollable widget used within the sheet that does not use this [ScrollController] will still scroll in response to user gestures, but the drag to dismiss behavior of the sheet will not trigger. If there is no scrollable area within the sheet, this parameter can be ignored. See below for an example.

{@tool dartpad} This example shows how to navigate to [CupertinoSheetRoute] by using it the same as a regular route.

** See code in examples/api/lib/cupertino/sheet/cupertino_sheet.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to show a Cupertino Sheet with nested navigation manually set up in order to enable restorable state.

** See code in examples/api/lib/cupertino/sheet/cupertino_sheet.2.dart ** {@end-tool}

{@tool dartpad} This example shows how to show a Cupertino Sheet with scrollable content.

** See code in examples/api/lib/cupertino/sheet/cupertino_sheet.3.dart ** {@end-tool}

See also:

- [showCupertinoSheet], which is a convenience method for pushing a `CupertinoSheetRoute`, with optional nested navigation built in.

### CupertinoSheetRoute()

```dart
CupertinoSheetRoute({dynamic settings, WidgetBuilder? builder, ScrollableWidgetBuilder? scrollableBuilder, bool enableDrag = true, bool showDragHandle = false, double? topGap})
```

Creates a page route that displays an iOS styled sheet.

### builder

```dart
WidgetBuilder? builder
```

Builds the primary contents of the sheet route.

### scrollableBuilder

```dart
ScrollableWidgetBuilder? scrollableBuilder
```

Builds the primary contents of the sheet route with a provided [ScrollController].

If the scrollable content built by this builder uses the provided [ScrollController], then when a downward drag is applied to the scrollable area while the content is scrolled to the top, the drag to dismiss behavior of the sheet will be triggered.

{@tool dartpad} This example shows how to show a Cupertino Sheet with scrollable content.

** See code in examples/api/lib/cupertino/sheet/cupertino_sheet.3.dart ** {@end-tool}

### enableDrag

```dart
bool enableDrag
```

### topGap

```dart
double get topGap
```

### showDragHandle

```dart
bool showDragHandle
```

Shows a drag handle at the top of the sheet.

Defaults to false.

### buildContent()

```dart
Widget buildContent(BuildContext context)
```

### hasParentSheet()

```dart
bool hasParentSheet(BuildContext context)
```

Checks if a Cupertino sheet view exists in the widget tree above the current context.

### popSheet()

```dart
void popSheet(BuildContext context)
```

Pops the entire [CupertinoSheetRoute], if a sheet route exists in the stack.

Used if to pop an entire sheet at once, if there is nested navigation within that sheet.

### barrierColor

```dart
Color? get barrierColor
```

### barrierDismissible

```dart
bool get barrierDismissible
```

### barrierLabel

```dart
String? get barrierLabel
```

### maintainState

```dart
bool get maintainState
```

### opaque

```dart
bool get opaque
```
