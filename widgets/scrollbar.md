@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

@docImport 'editable_text.dart'; @docImport 'list_wheel_scroll_view.dart'; @docImport 'nested_scroll_view.dart'; @docImport 'page_view.dart'; @docImport 'scroll_view.dart'; @docImport 'widget_state.dart';

# ScrollbarOrientation

```dart
enum ScrollbarOrientation {}
```

An orientation along either the horizontal or vertical [Axis].

Place towards the left of the screen.

Place towards the right of the screen.

Place on top of the screen.

Place on the bottom of the screen.

# ScrollbarPainter

```dart
class ScrollbarPainter extends ChangeNotifier implements CustomPainter {}
```

Paints a scrollbar's track and thumb.

The size of the scrollbar along its scroll direction is typically proportional to the percentage of content completely visible on screen, as long as its size isn't less than [minLength] and it isn't overscrolling.

If [padding] is an [EdgeInsetsDirectional], a non-null [textDirection] must be provided to properly resolve the padding values.

Unlike [CustomPainter]s that subclasses [CustomPainter] and only repaint when [shouldRepaint] returns true (which requires this [CustomPainter] to be rebuilt), this painter has the added optimization of repainting and not rebuilding when:

- the scroll position changes; and
- when the scrollbar fades away.

Calling [update] with the new [ScrollMetrics] will repaint the new scrollbar position.

Updating the value on the provided [fadeoutOpacityAnimation] will repaint with the new opacity.

You must call [dispose] on this [ScrollbarPainter] when it's no longer used.

See also:

- [Scrollbar] for a widget showing a scrollbar around a [Scrollable] in the Material Design style.
- [CupertinoScrollbar] for a widget showing a scrollbar around a [Scrollable] in the iOS style.

### ScrollbarPainter()

```dart
ScrollbarPainter({required Color color, required Animation<double> fadeoutOpacityAnimation, Color trackColor = const Color(0x00000000), Color trackBorderColor = const Color(0x00000000), TextDirection? textDirection, double thickness = _kScrollbarThickness, EdgeInsetsGeometry padding = EdgeInsets.zero, double mainAxisMargin = 0.0, double crossAxisMargin = 0.0, Radius? radius, Radius? trackRadius, OutlinedBorder? shape, double minLength = _kMinThumbExtent, double? minOverscrollLength, ScrollbarOrientation? scrollbarOrientation, bool ignorePointer = false})
```

Creates a scrollbar with customizations given by construction arguments.

### color

```dart
Color get color
```

[Color] of the thumb. Mustn't be null.

### color

```dart
set color(Color value)
```

### trackColor

```dart
Color get trackColor
```

[Color] of the track. Mustn't be null.

### trackColor

```dart
set trackColor(Color value)
```

### trackBorderColor

```dart
Color get trackBorderColor
```

[Color] of the track border. Mustn't be null.

### trackBorderColor

```dart
set trackBorderColor(Color value)
```

### trackRadius

```dart
Radius? get trackRadius
```

[Radius] of corners of the Scrollbar's track.

Scrollbar's track will be rectangular if [trackRadius] is null.

### trackRadius

```dart
set trackRadius(Radius? value)
```

### textDirection

```dart
TextDirection? get textDirection
```

[TextDirection] of the [BuildContext] which dictates the side of the screen the scrollbar appears in (the trailing side). Must be set prior to calling paint.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### thickness

```dart
double get thickness
```

Thickness of the scrollbar in its cross-axis in logical pixels. Mustn't be null.

### thickness

```dart
set thickness(double value)
```

### fadeoutOpacityAnimation

```dart
Animation<double> fadeoutOpacityAnimation
```

An opacity [Animation] that dictates the opacity of the thumb. Changes in value of this [Listenable] will automatically trigger repaints. Mustn't be null.

### mainAxisMargin

```dart
double get mainAxisMargin
```

Distance from the scrollbar thumb's start and end to the edge of the viewport in logical pixels. It affects the amount of available paint area.

The scrollbar track consumes this space.

Mustn't be null and defaults to 0.

### mainAxisMargin

```dart
set mainAxisMargin(double value)
```

### crossAxisMargin

```dart
double get crossAxisMargin
```

Distance from the scrollbar thumb to the nearest cross axis edge in logical pixels.

The scrollbar track consumes this space.

Defaults to zero.

### crossAxisMargin

```dart
set crossAxisMargin(double value)
```

### radius

```dart
Radius? get radius
```

[Radius] of corners if the scrollbar should have rounded corners.

Scrollbar will be rectangular if [radius] is null.

### radius

```dart
set radius(Radius? value)
```

### shape

```dart
OutlinedBorder? get shape
```

The [OutlinedBorder] of the scrollbar's thumb.

Only one of [radius] and [shape] may be specified. For a rounded rectangle, it's simplest to just specify [radius]. By default, the scrollbar thumb's shape is a simple rectangle.

If [shape] is specified, the thumb will take the shape of the passed [OutlinedBorder] and fill itself with [color] (or grey if it is unspecified).

### shape

```dart
set shape(OutlinedBorder? value)
```

### padding

```dart
EdgeInsetsGeometry get padding
```

The amount of space by which to inset the scrollbar's start and end, as well as its side to the nearest edge, in logical pixels.

This is typically set to the current [MediaQueryData.padding] to avoid partial obstructions such as display notches. If you only want additional margins around the scrollbar, see [mainAxisMargin].

Defaults to [EdgeInsets.zero]. Offsets from all four directions must be greater than or equal to zero.

For RTL (right-to-left) support, you can provide [EdgeInsetsDirectional], but you must also provide a non-null [textDirection] to properly resolve the padding values. The scrollbar will automatically adjust the padding based on the text direction.

### padding

```dart
set padding(EdgeInsetsGeometry value)
```

### minLength

```dart
double get minLength
```

The preferred smallest size the scrollbar thumb can shrink to when the total scrollable extent is large, the current visible viewport is small, and the viewport is not overscrolled.

The size of the scrollbar may shrink to a smaller size than [minLength] to fit in the available paint area. E.g., when [minLength] is `double.infinity`, it will not be respected if [ScrollMetrics.viewportDimension] and [mainAxisMargin] are finite.

Mustn't be null and the value has to be greater or equal to [minOverscrollLength], which in turn is >= 0. Defaults to 18.0.

### minLength

```dart
set minLength(double value)
```

### minOverscrollLength

```dart
double get minOverscrollLength
```

The preferred smallest size the scrollbar thumb can shrink to when viewport is overscrolled.

When overscrolling, the size of the scrollbar may shrink to a smaller size than [minOverscrollLength] to fit in the available paint area. E.g., when [minOverscrollLength] is `double.infinity`, it will not be respected if the [ScrollMetrics.viewportDimension] and [mainAxisMargin] are finite.

The value is less than or equal to [minLength] and greater than or equal to 0. When null, it will default to the value of [minLength].

### minOverscrollLength

```dart
set minOverscrollLength(double value)
```

### scrollbarOrientation

```dart
ScrollbarOrientation? get scrollbarOrientation
```

{@template flutter.widgets.Scrollbar.scrollbarOrientation} Dictates the orientation of the scrollbar.

[ScrollbarOrientation.top] places the scrollbar on top of the screen. [ScrollbarOrientation.bottom] places the scrollbar on the bottom of the screen. [ScrollbarOrientation.left] places the scrollbar on the left of the screen. [ScrollbarOrientation.right] places the scrollbar on the right of the screen.

[ScrollbarOrientation.top] and [ScrollbarOrientation.bottom] can only be used with a vertical scroll. [ScrollbarOrientation.left] and [ScrollbarOrientation.right] can only be used with a horizontal scroll.

For a vertical scroll the orientation defaults to [ScrollbarOrientation.right] for [TextDirection.ltr] and [ScrollbarOrientation.left] for [TextDirection.rtl]. For a horizontal scroll the orientation defaults to [ScrollbarOrientation.bottom]. {@endtemplate}

### scrollbarOrientation

```dart
set scrollbarOrientation(ScrollbarOrientation? value)
```

### ignorePointer

```dart
bool get ignorePointer
```

Whether the painter will be ignored during hit testing.

### ignorePointer

```dart
set ignorePointer(bool value)
```

### update()

```dart
void update(ScrollMetrics metrics, AxisDirection axisDirection)
```

Update with new [ScrollMetrics]. If the metrics change, the scrollbar will show and redraw itself based on these new metrics.

The scrollbar will remain on screen.

### updateThickness()

```dart
void updateThickness(double nextThickness, Radius nextRadius)
```

Update and redraw with new scrollbar thickness and radius.

### paint()

```dart
void paint(Canvas canvas, Size size)
```

### getTrackToScroll()

```dart
double getTrackToScroll(double thumbOffsetLocal)
```

Convert between a thumb track position and the corresponding scroll position.

The `thumbOffsetLocal` argument is a position in the thumb track.

### getThumbScrollOffset()

```dart
double getThumbScrollOffset()
```

The thumb's corresponding scroll offset in the track.

### hitTest()

```dart
bool? hitTest(Offset? position)
```

### hitTestInteractive()

```dart
bool hitTestInteractive(Offset position, PointerDeviceKind kind, {bool forHover = false})
```

Same as hitTest, but includes some padding when the [PointerEvent] is caused by [PointerDeviceKind.touch] to make sure that the region isn't too small to be interacted with by the user.

The hit test area for hovering with [PointerDeviceKind.mouse] over the scrollbar also uses this extra padding. This is to make it easier to interact with the scrollbar by presenting it to the mouse for interaction based on proximity. When `forHover` is true, the larger hit test area will be used.

### hitTestOnlyThumbInteractive()

```dart
bool hitTestOnlyThumbInteractive(Offset position, PointerDeviceKind kind)
```

Same as hitTestInteractive, but excludes the track portion of the scrollbar. Used to evaluate interactions with only the scrollbar thumb.

### shouldRepaint()

```dart
bool shouldRepaint(ScrollbarPainter oldDelegate)
```

### shouldRebuildSemantics()

```dart
bool shouldRebuildSemantics(CustomPainter oldDelegate)
```

### semanticsBuilder

```dart
SemanticsBuilderCallback? get semanticsBuilder
```

### toString()

```dart
String toString()
```

### dispose()

```dart
void dispose()
```

# RawScrollbar

```dart
class RawScrollbar extends StatefulWidget {}
```

An extendable base class for building scrollbars that fade in and out.

To add a scrollbar to a [ScrollView], like a [ListView] or a [CustomScrollView], wrap the scroll view widget in a [RawScrollbar] widget.

{@youtube 560 315 https://www.youtube.com/watch?v=DbkIQSvwnZc}

{@template flutter.widgets.Scrollbar} A scrollbar thumb indicates which portion of a [ScrollView] is actually visible.

By default, the thumb will fade in and out as the child scroll view scrolls. When [thumbVisibility] is true, the scrollbar thumb will remain visible without the fade animation. This requires that the [ScrollController] associated with the Scrollable widget is provided to [controller], or that the [PrimaryScrollController] is being used by that Scrollable widget.

If the scrollbar is wrapped around multiple [ScrollView]s, it only responds to the nearest ScrollView and shows the corresponding scrollbar thumb by default. The [notificationPredicate] allows the ability to customize which [ScrollNotification]s the Scrollbar should listen to.

If the child [ScrollView] is infinitely long, the [RawScrollbar] will not be painted. In this case, the scrollbar cannot accurately represent the relative location of the visible area, or calculate the accurate delta to apply when dragging on the thumb or tapping on the track.

### Interaction

Scrollbars are interactive and can use the [PrimaryScrollController] if a [controller] is not set. Interactive Scrollbar thumbs can be dragged along the main axis of the [ScrollView] to change the [ScrollPosition]. Tapping along the track exclusive of the thumb will trigger a [ScrollIncrementType.page] based on the relative position to the thumb.

When using the [PrimaryScrollController], it must not be attached to more than one [ScrollPosition]. [ScrollView]s that have not been provided a [ScrollController] and have a [ScrollView.scrollDirection] of [Axis.vertical] will automatically attach their ScrollPosition to the PrimaryScrollController. Provide a unique ScrollController to each [Scrollable] in this case to prevent having multiple ScrollPositions attached to the PrimaryScrollController.

{@tool dartpad} This sample shows an app with two scrollables in the same route. Since by default, there is one [PrimaryScrollController] per route, and they both have a scroll direction of [Axis.vertical], they would both try to attach to that controller on mobile platforms. The [Scrollbar] cannot support multiple positions attached to the same controller, so one [ListView], and its [Scrollbar] have been provided a unique [ScrollController]. Desktop platforms do not automatically attach to the PrimaryScrollController, requiring [ScrollView.primary] to be true instead in order to use the PrimaryScrollController.

Alternatively, a new PrimaryScrollController could be created above one of the [ListView]s.

** See code in examples/api/lib/widgets/scrollbar/raw_scrollbar.0.dart ** {@end-tool}

### Automatic Scrollbars on Desktop Platforms

Scrollbars are added to most [Scrollable] widgets by default on [TargetPlatformVariant.desktop] platforms. This is done through [ScrollBehavior.buildScrollbar] as part of an app's [ScrollConfiguration]. Scrollables that do not use the [PrimaryScrollController] or have a [ScrollController] provided to them will receive a unique ScrollController for use with the Scrollbar. In this case, only one Scrollable can be using the PrimaryScrollController, unless [interactive] is false. To prevent [Axis.vertical] Scrollables from using the PrimaryScrollController, set [ScrollView.primary] to false. Scrollable widgets that do not have automatically applied Scrollbars include

- [EditableText]
- [ListWheelScrollView]
- [PageView]
- [NestedScrollView]
- [DropdownButton]

Default Scrollbars can be disabled for the whole app by setting a [ScrollBehavior] with `scrollbars` set to false.

{@tool snippet}

```dart
MaterialApp(
  scrollBehavior: const MaterialScrollBehavior()
    .copyWith(scrollbars: false),
  home: Scaffold(
    appBar: AppBar(title: const Text('Home')),
  ),
)
```

{@end-tool}

{@tool dartpad} This sample shows how to disable the default Scrollbar for a [Scrollable] widget to avoid duplicate Scrollbars when running on desktop platforms.

** See code in examples/api/lib/widgets/scrollbar/raw_scrollbar.desktop.0.dart ** {@end-tool} {@endtemplate}

{@tool dartpad} This sample shows a [RawScrollbar] that executes a fade animation as scrolling occurs. The RawScrollbar will fade into view as the user scrolls, and fade out when scrolling stops. The [GridView] uses the [PrimaryScrollController] since it has an [Axis.vertical] scroll direction and has not been provided a [ScrollController].

** See code in examples/api/lib/widgets/scrollbar/raw_scrollbar.1.dart ** {@end-tool}

{@tool dartpad} When `thumbVisibility` is true, the scrollbar thumb will remain visible without the fade animation. This requires that a [ScrollController] is provided to `controller` for both the [RawScrollbar] and the [GridView]. Alternatively, the [PrimaryScrollController] can be used automatically so long as it is attached to the singular [ScrollPosition] associated with the GridView.

** See code in examples/api/lib/widgets/scrollbar/raw_scrollbar.2.dart ** {@end-tool}

See also:

- [ListView], which displays a linear, scrollable list of children.
- [GridView], which displays a 2 dimensional, scrollable array of children.

### RawScrollbar()

```dart
RawScrollbar({dynamic key, required Widget child, ScrollController? controller, bool? thumbVisibility, OutlinedBorder? shape, Radius? radius, double? thickness, Color? thumbColor, double minThumbLength = _kMinThumbExtent, double? minOverscrollLength, bool? trackVisibility, Radius? trackRadius, Color? trackColor, Color? trackBorderColor, Duration fadeDuration = _kScrollbarFadeDuration, Duration timeToFade = _kScrollbarTimeToFade, Duration pressDuration = Duration.zero, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, bool? interactive, ScrollbarOrientation? scrollbarOrientation, double mainAxisMargin = 0.0, double crossAxisMargin = 0.0, EdgeInsetsGeometry? padding})
```

Creates a basic raw scrollbar that wraps the given [child].

The [child], or a descendant of the [child], should be a source of [ScrollNotification] notifications, typically a [Scrollable] widget.

### child

```dart
Widget child
```

{@template flutter.widgets.Scrollbar.child} The widget below this widget in the tree.

The scrollbar will be stacked on top of this child. This child (and its subtree) should include a source of [ScrollNotification] notifications. Typically a [Scrollbar] is created on desktop platforms by a [ScrollBehavior.buildScrollbar] method, in which case the child is usually the one provided as an argument to that method.

Typically a [ListView] or [CustomScrollView]. {@endtemplate}

### controller

```dart
ScrollController? controller
```

{@template flutter.widgets.Scrollbar.controller} The [ScrollController] used to implement Scrollbar dragging.

If nothing is passed to controller, the default behavior is to automatically enable scrollbar dragging on the nearest ScrollController using [PrimaryScrollController.of].

If a ScrollController is passed, then dragging on the scrollbar thumb will update the [ScrollPosition] attached to the controller. A stateful ancestor of this widget needs to manage the ScrollController and either pass it to a scrollable descendant or use a PrimaryScrollController to share it.

{@tool snippet} Here is an example of using the [controller] attribute to enable scrollbar dragging for multiple independent ListViews:

```dart
// (e.g. in a stateful widget)

final ScrollController controllerOne = ScrollController();
final ScrollController controllerTwo = ScrollController();

@override
Widget build(BuildContext context) {
  return Column(
    children: <Widget>[
      SizedBox(
       height: 200,
       child: CupertinoScrollbar(
         controller: controllerOne,
         child: ListView.builder(
           controller: controllerOne,
           itemCount: 120,
           itemBuilder: (BuildContext context, int index) => Text('item $index'),
         ),
       ),
     ),
     SizedBox(
       height: 200,
       child: CupertinoScrollbar(
         controller: controllerTwo,
         child: ListView.builder(
           controller: controllerTwo,
           itemCount: 120,
           itemBuilder: (BuildContext context, int index) => Text('list 2 item $index'),
         ),
       ),
     ),
   ],
  );
}
```

{@end-tool} {@endtemplate}

### thumbVisibility

```dart
bool? thumbVisibility
```

{@template flutter.widgets.Scrollbar.thumbVisibility} Indicates that the scrollbar thumb should be visible, even when a scroll is not underway.

When false, the scrollbar will be shown during scrolling and will fade out otherwise.

When true, the scrollbar will always be visible and never fade out. This requires that the Scrollbar can access the [ScrollController] of the associated Scrollable widget. This can either be the provided [controller], or the [PrimaryScrollController] of the current context.

- When providing a controller, the same ScrollController must also be provided to the associated Scrollable widget.
- The [PrimaryScrollController] is used by default for a [ScrollView] that has not been provided a [ScrollController] and that has a [ScrollView.scrollDirection] of [Axis.vertical]. This automatic behavior does not apply to those with [Axis.horizontal]. To explicitly use the PrimaryScrollController, set [ScrollView.primary] to true.

Defaults to false when null.

{@tool snippet}

```dart
// (e.g. in a stateful widget)

final ScrollController controllerOne = ScrollController();
final ScrollController controllerTwo = ScrollController();

@override
Widget build(BuildContext context) {
return Column(
  children: <Widget>[
    SizedBox(
       height: 200,
       child: Scrollbar(
         thumbVisibility: true,
         controller: controllerOne,
         child: ListView.builder(
           controller: controllerOne,
           itemCount: 120,
           itemBuilder: (BuildContext context, int index) {
             return Text('item $index');
           },
         ),
       ),
     ),
     SizedBox(
       height: 200,
       child: CupertinoScrollbar(
         thumbVisibility: true,
         controller: controllerTwo,
         child: SingleChildScrollView(
           controller: controllerTwo,
           child: const SizedBox(
             height: 2000,
             width: 500,
             child: Placeholder(),
           ),
         ),
       ),
     ),
   ],
  );
}
```

{@end-tool}

See also:

- [RawScrollbarState.showScrollbar], an overridable getter which uses this value to override the default behavior.
- [ScrollView.primary], which indicates whether the ScrollView is the primary scroll view associated with the parent [PrimaryScrollController].
- [PrimaryScrollController], which associates a [ScrollController] with a subtree. {@endtemplate}

Subclass [Scrollbar] can hide and show the scrollbar thumb in response to [WidgetState]s by using [ScrollbarThemeData.thumbVisibility].

### shape

```dart
OutlinedBorder? shape
```

The [OutlinedBorder] of the scrollbar's thumb.

Only one of [radius] and [shape] may be specified. For a rounded rectangle, it's simplest to just specify [radius]. By default, the scrollbar thumb's shape is a simple rectangle.

If [shape] is specified, the thumb will take the shape of the passed [OutlinedBorder] and fill itself with [thumbColor] (or grey if it is unspecified).

{@tool dartpad} This is an example of using a [StadiumBorder] for drawing the [shape] of the thumb in a [RawScrollbar].

** See code in examples/api/lib/widgets/scrollbar/raw_scrollbar.shape.0.dart ** {@end-tool}

### radius

```dart
Radius? radius
```

The [Radius] of the scrollbar thumb's rounded rectangle corners.

Scrollbar will be rectangular if [radius] is null, which is the default behavior.

### thickness

```dart
double? thickness
```

The thickness of the scrollbar in the cross axis of the scrollable.

If null, will default to 6.0 pixels.

### thumbColor

```dart
Color? thumbColor
```

The color of the scrollbar thumb.

If null, defaults to Color(0x66BCBCBC).

### minThumbLength

```dart
double minThumbLength
```

The preferred smallest size the scrollbar thumb can shrink to when the total scrollable extent is large, the current visible viewport is small, and the viewport is not overscrolled.

The size of the scrollbar's thumb may shrink to a smaller size than [minThumbLength] to fit in the available paint area (e.g., when [minThumbLength] is greater than [ScrollMetrics.viewportDimension] and [mainAxisMargin] combined).

Mustn't be null and the value has to be greater or equal to [minOverscrollLength], which in turn is >= 0. Defaults to 18.0.

### minOverscrollLength

```dart
double? minOverscrollLength
```

The preferred smallest size the scrollbar thumb can shrink to when viewport is overscrolled.

When overscrolling, the size of the scrollbar's thumb may shrink to a smaller size than [minOverscrollLength] to fit in the available paint area (e.g., when [minOverscrollLength] is greater than [ScrollMetrics.viewportDimension] and [mainAxisMargin] combined).

Overscrolling can be made possible by setting the `physics` property of the `child` Widget to a `BouncingScrollPhysics`, which is a special `ScrollPhysics` that allows overscrolling.

The value is less than or equal to [minThumbLength] and greater than or equal to 0. When null, it will default to the value of [minThumbLength].

### trackVisibility

```dart
bool? trackVisibility
```

{@template flutter.widgets.Scrollbar.trackVisibility} Indicates that the scrollbar track should be visible.

When true, the scrollbar track will always be visible so long as the thumb is visible. If the scrollbar thumb is not visible, the track will not be visible either.

Defaults to false when null. {@endtemplate}

Subclass [Scrollbar] can hide and show the scrollbar thumb in response to [WidgetState]s by using [ScrollbarThemeData.trackVisibility].

### trackRadius

```dart
Radius? trackRadius
```

The [Radius] of the scrollbar track's rounded rectangle corners.

Scrollbar's track will be rectangular if [trackRadius] is null, which is the default behavior.

### trackColor

```dart
Color? trackColor
```

The color of the scrollbar track.

The scrollbar track will only be visible when [trackVisibility] and [thumbVisibility] are true.

If null, defaults to Color(0x08000000).

### trackBorderColor

```dart
Color? trackBorderColor
```

The color of the scrollbar track's border.

The scrollbar track will only be visible when [trackVisibility] and [thumbVisibility] are true.

If null, defaults to Color(0x1a000000).

### fadeDuration

```dart
Duration fadeDuration
```

The [Duration] of the fade animation.

Defaults to a [Duration] of 300 milliseconds.

### timeToFade

```dart
Duration timeToFade
```

The [Duration] of time until the fade animation begins.

Defaults to a [Duration] of 600 milliseconds.

### pressDuration

```dart
Duration pressDuration
```

The [Duration] of time that a LongPress will trigger the drag gesture of the scrollbar thumb.

Defaults to [Duration.zero].

### notificationPredicate

```dart
ScrollNotificationPredicate notificationPredicate
```

{@template flutter.widgets.Scrollbar.notificationPredicate} A check that specifies whether a [ScrollNotification] should be handled by this widget.

By default, checks whether `notification.depth == 0`. That means if the scrollbar is wrapped around multiple [ScrollView]s, it only responds to the nearest scrollView and shows the corresponding scrollbar thumb. {@endtemplate}

### interactive

```dart
bool? interactive
```

{@template flutter.widgets.Scrollbar.interactive} Whether the Scrollbar should be interactive and respond to dragging on the thumb, or tapping in the track area.

Does not apply to the [CupertinoScrollbar], which is always interactive to match native behavior. On Android, the scrollbar is not interactive by default.

When false, the scrollbar will not respond to gesture or hover events, and will allow to click through it.

Defaults to true when null, unless on Android, which will default to false when null.

See also:

- [RawScrollbarState.enableGestures], an overridable getter which uses this value to override the default behavior. {@endtemplate}

### scrollbarOrientation

```dart
ScrollbarOrientation? scrollbarOrientation
```

{@macro flutter.widgets.Scrollbar.scrollbarOrientation}

### mainAxisMargin

```dart
double mainAxisMargin
```

Distance from the scrollbar thumb's start or end to the nearest edge of the viewport in logical pixels. It affects the amount of available paint area.

The scrollbar track consumes this space.

Mustn't be null and defaults to 0.

### crossAxisMargin

```dart
double crossAxisMargin
```

Distance from the scrollbar thumb's side to the nearest cross axis edge in logical pixels.

The scrollbar track consumes this space.

Defaults to zero.

### padding

```dart
EdgeInsetsGeometry? padding
```

The insets by which the scrollbar thumb and track should be padded.

When null, the inherited [MediaQueryData.padding] is used.

Defaults to null.

### createState()

```dart
RawScrollbarState<RawScrollbar> createState()
```

# RawScrollbarState

```dart
class RawScrollbarState<T extends RawScrollbar> extends State<T> with TickerProviderStateMixin<T> {}
```

The state for a [RawScrollbar] widget, also shared by the [Scrollbar] and [CupertinoScrollbar] widgets.

Controls the animation that fades a scrollbar's thumb in and out of view.

Provides defaults gestures for dragging the scrollbar thumb and tapping on the scrollbar track.

### scrollbarPainter

```dart
ScrollbarPainter scrollbarPainter
```

Used to paint the scrollbar.

Can be customized by subclasses to change scrollbar behavior by overriding [updateScrollbarPainter].

### showScrollbar

```dart
bool get showScrollbar
```

Overridable getter to indicate that the scrollbar should be visible, even when a scroll is not underway.

Subclasses can override this getter to make its value depend on an inherited theme.

Defaults to false when [RawScrollbar.thumbVisibility] is null.

### enableGestures

```dart
bool get enableGestures
```

Overridable getter to indicate is gestures should be enabled on the scrollbar.

When false, the scrollbar will not respond to gesture or hover events, and will allow to click through it.

Subclasses can override this getter to make its value depend on an inherited theme.

Defaults to true when [RawScrollbar.interactive] is null.

See also:

- [RawScrollbar.interactive], which overrides the default behavior.

### initState()

```dart
void initState()
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### updateScrollbarPainter()

```dart
void updateScrollbarPainter()
```

This method is responsible for configuring the [scrollbarPainter] according to the [widget]'s properties and any inherited widgets the painter depends on, like [Directionality] and [MediaQuery].

Subclasses can override to configure the [scrollbarPainter].

### didUpdateWidget()

```dart
void didUpdateWidget(T oldWidget)
```

### getScrollbarDirection()

```dart
Axis? getScrollbarDirection()
```

Returns the [Axis] of the child scroll view, or null if the we haven't seen a ScrollMetrics notification yet.

### handleThumbPress()

```dart
void handleThumbPress()
```

Handler called when a press on the scrollbar thumb has been recognized.

Cancels the [Timer] associated with the fade animation of the scrollbar.

### handleThumbPressStart()

```dart
void handleThumbPressStart(Offset localPosition)
```

Handler called when a long press gesture has started.

Begins the fade out animation and creates the thumb's DragScrollController.

### handleThumbPressUpdate()

```dart
void handleThumbPressUpdate(Offset localPosition)
```

Handler called when a currently active long press gesture moves.

Updates the position of the child scrollable via the _drag ScrollDragController.

### handleThumbPressEnd()

```dart
void handleThumbPressEnd(Offset localPosition, Velocity velocity)
```

Handler called when a long press has ended.

### handleTrackTapDown()

```dart
void handleTrackTapDown(TapDownDetails details)
```

Handler called when the track is tapped in order to page in the tapped direction.

### isPointerOverTrack()

```dart
bool isPointerOverTrack(Offset position, PointerDeviceKind kind)
```

Returns true if the provided [Offset] is located over the track of the [RawScrollbar].

Excludes the [RawScrollbar] thumb.

### isPointerOverThumb()

```dart
bool isPointerOverThumb(Offset position, PointerDeviceKind kind)
```

Returns true if the provided [Offset] is located over the thumb of the [RawScrollbar].

### isPointerOverScrollbar()

```dart
bool isPointerOverScrollbar(Offset position, PointerDeviceKind kind, {bool forHover = false})
```

Returns true if the provided [Offset] is located over the track or thumb of the [RawScrollbar].

The hit test area for mouse hovering over the scrollbar is larger than regular hit testing. This is to make it easier to interact with the scrollbar and present it to the mouse for interaction based on proximity. When `forHover` is true, the larger hit test area will be used.

### handleHover()

```dart
void handleHover(PointerHoverEvent event)
```

Cancels the fade out animation so the scrollbar will remain visible for interaction.

Can be overridden by subclasses to respond to a [PointerHoverEvent].

Helper methods [isPointerOverScrollbar], [isPointerOverThumb], and [isPointerOverTrack] can be used to determine the location of the pointer relative to the painter scrollbar elements.

### handleHoverExit()

```dart
void handleHoverExit(PointerExitEvent event)
```

Initiates the fade out animation.

Can be overridden by subclasses to respond to a [PointerExitEvent].

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```
