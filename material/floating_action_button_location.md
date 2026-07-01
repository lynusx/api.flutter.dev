@docImport 'app_bar.dart'; @docImport 'bottom_app_bar.dart'; @docImport 'bottom_navigation_bar.dart'; @docImport 'circle_avatar.dart'; @docImport 'floating_action_button.dart'; @docImport 'list_tile.dart';

# kFloatingActionButtonMargin

```dart
double kFloatingActionButtonMargin
```

The margin that a [FloatingActionButton] should leave between it and the edge of the screen.

[FloatingActionButtonLocation.endFloat] uses this to set the appropriate margin between the [FloatingActionButton] and the end of the screen.

# kFloatingActionButtonSegue

```dart
Duration kFloatingActionButtonSegue
```

The amount of time the [FloatingActionButton] takes to transition in or out.

The [Scaffold] uses this to set the duration of [FloatingActionButton] motion, entrance, and exit animations.

# kFloatingActionButtonTurnInterval

```dart
double kFloatingActionButtonTurnInterval
```

The fraction of a circle the [FloatingActionButton] should turn when it enters.

Its value corresponds to 0.125 of a full circle, equivalent to 45 degrees or pi/4 radians.

# kMiniButtonOffsetAdjustment

```dart
double kMiniButtonOffsetAdjustment
```

If a [FloatingActionButton] is used on a [Scaffold] in certain positions, it is moved [kMiniButtonOffsetAdjustment] pixels closer to the edge of the screen.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.leading] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

More specifically:

- In the following positions, the [FloatingActionButton] is moved _horizontally_ closer to the edge of the screen:
- [FloatingActionButtonLocation.miniStartTop]
- [FloatingActionButtonLocation.miniStartFloat]
- [FloatingActionButtonLocation.miniStartDocked]
- [FloatingActionButtonLocation.miniEndTop]
- [FloatingActionButtonLocation.miniEndFloat]
- [FloatingActionButtonLocation.miniEndDocked]
- In the following positions, the [FloatingActionButton] is moved _vertically_ closer to the bottom of the screen:
- [FloatingActionButtonLocation.miniStartFloat]
- [FloatingActionButtonLocation.miniCenterFloat]
- [FloatingActionButtonLocation.miniEndFloat]

# FloatingActionButtonLocation

```dart
abstract class FloatingActionButtonLocation {}
```

An object that defines a position for the [FloatingActionButton] based on the [Scaffold]'s [ScaffoldPrelayoutGeometry].

Flutter provides [FloatingActionButtonLocation]s for the common [FloatingActionButton] placements in Material Design applications. These locations are available as static members of this class.

## Floating Action Button placements

The following diagrams show the available placement locations for the FloatingActionButton.

- [FloatingActionButtonLocation.centerDocked]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_center_docked.png)

- [FloatingActionButtonLocation.centerFloat]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_center_float.png)

- [FloatingActionButtonLocation.centerTop]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_center_top.png)

- [FloatingActionButtonLocation.endDocked]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_docked.png)

- [FloatingActionButtonLocation.endFloat]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_float.png)

- [FloatingActionButtonLocation.endTop]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_top.png)

- [FloatingActionButtonLocation.startDocked]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_start_docked.png)

- [FloatingActionButtonLocation.startFloat]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_start_float.png)

- [FloatingActionButtonLocation.startTop]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_start_top.png)

- [FloatingActionButtonLocation.miniCenterDocked]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_center_docked.png)

- [FloatingActionButtonLocation.miniCenterFloat]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_center_float.png)

- [FloatingActionButtonLocation.miniCenterTop]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_center_top.png)

- [FloatingActionButtonLocation.miniEndDocked]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_end_docked.png)

- [FloatingActionButtonLocation.miniEndFloat]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_end_float.png)

- [FloatingActionButtonLocation.miniEndTop]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_end_top.png)

- [FloatingActionButtonLocation.miniStartDocked]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_start_docked.png)

- [FloatingActionButtonLocation.miniStartFloat]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_start_float.png)

- [FloatingActionButtonLocation.miniStartTop]:

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_start_top.png)

See also:

- [FloatingActionButton], which is a circular button typically shown in the bottom right corner of the app.
- [FloatingActionButtonAnimator], which is used to animate the [Scaffold.floatingActionButton] from one [FloatingActionButtonLocation] to another.
- [ScaffoldPrelayoutGeometry], the geometry that [FloatingActionButtonLocation]s use to position the [FloatingActionButton].

### FloatingActionButtonLocation()

```dart
FloatingActionButtonLocation()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### startTop

```dart
FloatingActionButtonLocation startTop
```

Start-aligned [FloatingActionButton], floating over the transition between the [Scaffold.appBar] and the [Scaffold.body].

To align a floating action button with [CircleAvatar]s in the [ListTile.leading] slots of [ListTile]s in a [ListView] in the [Scaffold.body], use [miniStartTop] and set [FloatingActionButton.mini] to true.

This is unlikely to be a useful location for apps that lack a top [AppBar] or that use a [SliverAppBar] in the scaffold body itself.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_start_top.png)

### miniStartTop

```dart
FloatingActionButtonLocation miniStartTop
```

Start-aligned [FloatingActionButton], floating over the transition between the [Scaffold.appBar] and the [Scaffold.body], optimized for mini floating action buttons.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.leading] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

This is unlikely to be a useful location for apps that lack a top [AppBar] or that use a [SliverAppBar] in the scaffold body itself.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_start_top.png)

### centerTop

```dart
FloatingActionButtonLocation centerTop
```

Centered [FloatingActionButton], floating over the transition between the [Scaffold.appBar] and the [Scaffold.body].

This is unlikely to be a useful location for apps that lack a top [AppBar] or that use a [SliverAppBar] in the scaffold body itself.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_center_top.png)

### miniCenterTop

```dart
FloatingActionButtonLocation miniCenterTop
```

Centered [FloatingActionButton], floating over the transition between the [Scaffold.appBar] and the [Scaffold.body], intended to be used with [FloatingActionButton.mini] set to true.

This is unlikely to be a useful location for apps that lack a top [AppBar] or that use a [SliverAppBar] in the scaffold body itself.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_center_top.png)

### endTop

```dart
FloatingActionButtonLocation endTop
```

End-aligned [FloatingActionButton], floating over the transition between the [Scaffold.appBar] and the [Scaffold.body].

To align a floating action button with [CircleAvatar]s in the [ListTile.trailing] slots of [ListTile]s in a [ListView] in the [Scaffold.body], use [miniEndTop] and set [FloatingActionButton.mini] to true.

This is unlikely to be a useful location for apps that lack a top [AppBar] or that use a [SliverAppBar] in the scaffold body itself.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_top.png)

### miniEndTop

```dart
FloatingActionButtonLocation miniEndTop
```

End-aligned [FloatingActionButton], floating over the transition between the [Scaffold.appBar] and the [Scaffold.body], optimized for mini floating action buttons.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.trailing] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

This is unlikely to be a useful location for apps that lack a top [AppBar] or that use a [SliverAppBar] in the scaffold body itself.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_end_top.png)

### startFloat

```dart
FloatingActionButtonLocation startFloat
```

Start-aligned [FloatingActionButton], floating at the bottom of the screen.

To align a floating action button with [CircleAvatar]s in the [ListTile.leading] slots of [ListTile]s in a [ListView] in the [Scaffold.body], use [miniStartFloat] and set [FloatingActionButton.mini] to true.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_start_float.png)

### miniStartFloat

```dart
FloatingActionButtonLocation miniStartFloat
```

Start-aligned [FloatingActionButton], floating at the bottom of the screen, optimized for mini floating action buttons.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.leading] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

Compared to [FloatingActionButtonLocation.startFloat], floating action buttons using this location will move horizontally _and_ vertically closer to the edges, by [kMiniButtonOffsetAdjustment] each.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_start_float.png)

### centerFloat

```dart
FloatingActionButtonLocation centerFloat
```

Centered [FloatingActionButton], floating at the bottom of the screen.

To position a mini floating action button, use [miniCenterFloat] and set [FloatingActionButton.mini] to true.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_center_float.png)

### miniCenterFloat

```dart
FloatingActionButtonLocation miniCenterFloat
```

Centered [FloatingActionButton], floating at the bottom of the screen, optimized for mini floating action buttons.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align horizontally with the locations [FloatingActionButtonLocation.miniStartFloat] and [FloatingActionButtonLocation.miniEndFloat].

Compared to [FloatingActionButtonLocation.centerFloat], floating action buttons using this location will move vertically down by [kMiniButtonOffsetAdjustment].

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_center_float.png)

### endFloat

```dart
FloatingActionButtonLocation endFloat
```

End-aligned [FloatingActionButton], floating at the bottom of the screen.

This is the default alignment of [FloatingActionButton]s in Material applications.

To align a floating action button with [CircleAvatar]s in the [ListTile.trailing] slots of [ListTile]s in a [ListView] in the [Scaffold.body], use [miniEndFloat] and set [FloatingActionButton.mini] to true.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_float.png)

### miniEndFloat

```dart
FloatingActionButtonLocation miniEndFloat
```

End-aligned [FloatingActionButton], floating at the bottom of the screen, optimized for mini floating action buttons.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.trailing] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

Compared to [FloatingActionButtonLocation.endFloat], floating action buttons using this location will move horizontally _and_ vertically closer to the edges, by [kMiniButtonOffsetAdjustment] each.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_end_float.png)

### startDocked

```dart
FloatingActionButtonLocation startDocked
```

Start-aligned [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar.

To align a floating action button with [CircleAvatar]s in the [ListTile.leading] slots of [ListTile]s in a [ListView] in the [Scaffold.body], use [miniStartDocked] and set [FloatingActionButton.mini] to true.

If the value of [Scaffold.bottomNavigationBar] is a [BottomAppBar], the bottom app bar can include a "notch" in its shape that accommodates the overlapping floating action button.

This is unlikely to be a useful location for apps that lack a bottom navigation bar.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_start_docked.png)

### miniStartDocked

```dart
FloatingActionButtonLocation miniStartDocked
```

Start-aligned [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar, optimized for mini floating action buttons.

If the value of [Scaffold.bottomNavigationBar] is a [BottomAppBar], the bottom app bar can include a "notch" in its shape that accommodates the overlapping floating action button.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.leading] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

This is unlikely to be a useful location for apps that lack a bottom navigation bar.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_start_docked.png)

### centerDocked

```dart
FloatingActionButtonLocation centerDocked
```

Centered [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar.

If the value of [Scaffold.bottomNavigationBar] is a [BottomAppBar], the bottom app bar can include a "notch" in its shape that accommodates the overlapping floating action button.

This is unlikely to be a useful location for apps that lack a bottom navigation bar.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_center_docked.png)

### miniCenterDocked

```dart
FloatingActionButtonLocation miniCenterDocked
```

Centered [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar; intended to be used with [FloatingActionButton.mini] set to true.

If the value of [Scaffold.bottomNavigationBar] is a [BottomAppBar], the bottom app bar can include a "notch" in its shape that accommodates the overlapping floating action button.

This is unlikely to be a useful location for apps that lack a bottom navigation bar.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_center_docked.png)

### endDocked

```dart
FloatingActionButtonLocation endDocked
```

End-aligned [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar.

If the value of [Scaffold.bottomNavigationBar] is a [BottomAppBar], the bottom app bar can include a "notch" in its shape that accommodates the overlapping floating action button.

This is unlikely to be a useful location for apps that lack a bottom navigation bar.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_docked.png)

### miniEndDocked

```dart
FloatingActionButtonLocation miniEndDocked
```

End-aligned [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar, optimized for mini floating action buttons.

To align a floating action button with [CircleAvatar]s in the [ListTile.trailing] slots of [ListTile]s in a [ListView] in the [Scaffold.body], use [miniEndDocked] and set [FloatingActionButton.mini] to true.

If the value of [Scaffold.bottomNavigationBar] is a [BottomAppBar], the bottom app bar can include a "notch" in its shape that accommodates the overlapping floating action button.

This is intended to be used with [FloatingActionButton.mini] set to true, so that the floating action button appears to align with [CircleAvatar]s in the [ListTile.trailing] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

This is unlikely to be a useful location for apps that lack a bottom navigation bar.

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_mini_end_docked.png)

### endContained

```dart
FloatingActionButtonLocation endContained
```

End-aligned [FloatingActionButton], floating over the [Scaffold.bottomNavigationBar] so that the floating action button lines up with the center of the bottom navigation bar.

This is unlikely to be a useful location for apps which has a [BottomNavigationBar] or a non material 3 [BottomAppBar].

![](https://flutter.github.io/assets-for-api-docs/assets/material/floating_action_button_location_end_contained.png)

### getOffset()

```dart
Offset getOffset(ScaffoldPrelayoutGeometry scaffoldGeometry)
```

Places the [FloatingActionButton] based on the [Scaffold]'s layout.

This uses a [ScaffoldPrelayoutGeometry], which the [Scaffold] constructs during its layout phase after it has laid out every widget it can lay out except the [FloatingActionButton]. The [Scaffold] uses the [Offset] returned from this method to position the [FloatingActionButton] and complete its layout.

### toString()

```dart
String toString()
```

# StandardFabLocation

```dart
abstract class StandardFabLocation extends FloatingActionButtonLocation {}
```

A base class that simplifies building [FloatingActionButtonLocation]s when used with mixins [FabTopOffsetY], [FabFloatOffsetY], [FabDockedOffsetY], [FabStartOffsetX], [FabCenterOffsetX], [FabEndOffsetX], and [FabMiniOffsetAdjustment].

A subclass of [FloatingActionButtonLocation] which implements its [getOffset] method using three other methods: [getOffsetX], [getOffsetY], and [isMini].

Different mixins on this class override different methods, so that combining a set of mixins creates a floating action button location.

For example: the location [FloatingActionButtonLocation.miniEndTop] is based on a class that extends [StandardFabLocation] with mixins [FabMiniOffsetAdjustment], [FabEndOffsetX], and [FabTopOffsetY].

You can create your own subclass of [StandardFabLocation] to implement a custom [FloatingActionButtonLocation].

{@tool dartpad} This is an example of a user-defined [FloatingActionButtonLocation].

The example shows a [Scaffold] with an [AppBar], a [BottomAppBar], and a [FloatingActionButton] using a custom [FloatingActionButtonLocation].

The new [FloatingActionButtonLocation] is defined by extending [StandardFabLocation] with two mixins, [FabEndOffsetX] and [FabFloatOffsetY], and overriding the [getOffsetX] method to adjust the FAB's x-coordinate, creating a [FloatingActionButtonLocation] slightly different from [FloatingActionButtonLocation.endFloat].

** See code in examples/api/lib/material/floating_action_button_location/standard_fab_location.0.dart ** {@end-tool}

### StandardFabLocation()

```dart
StandardFabLocation()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getOffsetX()

```dart
double getOffsetX(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Obtains the x-offset to place the [FloatingActionButton] based on the [Scaffold]'s layout.

Used by [getOffset] to compute its x-coordinate.

### getOffsetY()

```dart
double getOffsetY(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Obtains the y-offset to place the [FloatingActionButton] based on the [Scaffold]'s layout.

Used by [getOffset] to compute its y-coordinate.

### isMini()

```dart
bool isMini()
```

A function returning whether this [StandardFabLocation] is optimized for mini [FloatingActionButton]s.

### getOffset()

```dart
Offset getOffset(ScaffoldPrelayoutGeometry scaffoldGeometry)
```

# FabTopOffsetY

```dart
mixin FabTopOffsetY on StandardFabLocation {}
```

Mixin for a "top" floating action button location, such as [FloatingActionButtonLocation.startTop].

The `adjustment`, typically [kMiniButtonOffsetAdjustment], is ignored in the Y axis of "top" positions. For "top" positions, the X offset is adjusted to move closer to the edge of the screen. This is so that a minified floating action button appears to align with [CircleAvatar]s in the [ListTile.leading] slot of a [ListTile] in a [ListView] in the [Scaffold.body].

### getOffsetY()

```dart
double getOffsetY(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates y-offset for [FloatingActionButtonLocation]s floating over the transition between the [Scaffold.appBar] and the [Scaffold.body].

# FabFloatOffsetY

```dart
mixin FabFloatOffsetY on StandardFabLocation {}
```

Mixin for a "float" floating action button location, such as [FloatingActionButtonLocation.centerFloat].

### getOffsetY()

```dart
double getOffsetY(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates y-offset for [FloatingActionButtonLocation]s floating at the bottom of the screen.

# FabDockedOffsetY

```dart
mixin FabDockedOffsetY on StandardFabLocation {}
```

Mixin for a "docked" floating action button location, such as [FloatingActionButtonLocation.endDocked].

### getOffsetY()

```dart
double getOffsetY(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates y-offset for [FloatingActionButtonLocation]s floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the top of the bottom navigation bar.

# FabContainedOffsetY

```dart
mixin FabContainedOffsetY on StandardFabLocation {}
```

Mixin for a "contained" floating action button location, such as [FloatingActionButtonLocation.endContained].

### getOffsetY()

```dart
double getOffsetY(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates y-offset for [FloatingActionButtonLocation]s floating over the [Scaffold.bottomNavigationBar] so that the center of the floating action button lines up with the center of the bottom navigation bar.

# FabStartOffsetX

```dart
mixin FabStartOffsetX on StandardFabLocation {}
```

Mixin for a "start" floating action button location, such as [FloatingActionButtonLocation.startTop].

### getOffsetX()

```dart
double getOffsetX(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates x-offset for start-aligned [FloatingActionButtonLocation]s.

# FabCenterOffsetX

```dart
mixin FabCenterOffsetX on StandardFabLocation {}
```

Mixin for a "center" floating action button location, such as [FloatingActionButtonLocation.centerFloat].

### getOffsetX()

```dart
double getOffsetX(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates x-offset for center-aligned [FloatingActionButtonLocation]s.

# FabEndOffsetX

```dart
mixin FabEndOffsetX on StandardFabLocation {}
```

Mixin for an "end" floating action button location, such as [FloatingActionButtonLocation.endDocked].

### getOffsetX()

```dart
double getOffsetX(ScaffoldPrelayoutGeometry scaffoldGeometry, double adjustment)
```

Calculates x-offset for end-aligned [FloatingActionButtonLocation]s.

# FabMiniOffsetAdjustment

```dart
mixin FabMiniOffsetAdjustment on StandardFabLocation {}
```

Mixin for a "mini" floating action button location, such as [FloatingActionButtonLocation.miniStartTop].

### isMini()

```dart
bool isMini()
```

# FloatingActionButtonAnimator

```dart
abstract class FloatingActionButtonAnimator {}
```

Provider of animations to move the [FloatingActionButton] between [FloatingActionButtonLocation]s.

The [Scaffold] uses [Scaffold.floatingActionButtonAnimator] to define:

- The [Offset] of the [FloatingActionButton] between the old and new [FloatingActionButtonLocation]s as part of the transition animation.
- An [Animation] to scale the [FloatingActionButton] during the transition.
- An [Animation] to rotate the [FloatingActionButton] during the transition.
- Where to start a new animation from if an animation is interrupted.

See also:

- [FloatingActionButton], which is a circular button typically shown in the bottom right corner of the app.
- [FloatingActionButtonLocation], which the [Scaffold] uses to place the [Scaffold.floatingActionButton] within the [Scaffold]'s layout.

### FloatingActionButtonAnimator()

```dart
FloatingActionButtonAnimator()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### scaling

```dart
FloatingActionButtonAnimator scaling
```

Moves the [FloatingActionButton] by scaling out and then in at a new [FloatingActionButtonLocation].

This animator shrinks the [FloatingActionButton] down until it disappears, then grows it back to full size at its new [FloatingActionButtonLocation].

This is the default [FloatingActionButton] motion animation.

### getOffset()

```dart
Offset getOffset({required Offset begin, required Offset end, required double progress})
```

Gets the [FloatingActionButton]'s position relative to the origin of the [Scaffold] based on [progress].

[begin] is the [Offset] provided by the previous [FloatingActionButtonLocation].

[end] is the [Offset] provided by the new [FloatingActionButtonLocation].

[progress] is the current progress of the transition animation. When [progress] is 0.0, the returned [Offset] should be equal to [begin]. when [progress] is 1.0, the returned [Offset] should be equal to [end].

### getScaleAnimation()

```dart
Animation<double> getScaleAnimation({required Animation<double> parent})
```

Animates the scale of the [FloatingActionButton].

The animation should both start and end with a value of 1.0.

For example, to create an animation that linearly scales out and then back in, you could join animations that pass each other:

```dart
  @override
  Animation<double> getScaleAnimation({required Animation<double> parent}) {
    // The animations will cross at value 0, and the train will return to 1.0.
    return TrainHoppingAnimation(
      Tween<double>(begin: 1.0, end: -1.0).animate(parent),
      Tween<double>(begin: -1.0, end: 1.0).animate(parent),
    );
  }
```

### getRotationAnimation()

```dart
Animation<double> getRotationAnimation({required Animation<double> parent})
```

Animates the rotation of [Scaffold.floatingActionButton].

The animation should both start and end with a value of 0.0 or 1.0.

The animation values are a fraction of a full circle, with 0.0 and 1.0 corresponding to 0 and 360 degrees, while 0.5 corresponds to 180 degrees.

For example, to create a rotation animation that rotates the [FloatingActionButton] through a full circle:

```dart
@override
Animation<double> getRotationAnimation({required Animation<double> parent}) {
  return Tween<double>(begin: 0.0, end: 1.0).animate(parent);
}
```

### getAnimationRestart()

```dart
double getAnimationRestart(double previousValue)
```

Gets the progress value to restart a motion animation from when the animation is interrupted.

[previousValue] is the value of the animation before it was interrupted.

The restart of the animation will affect all three parts of the motion animation: offset animation, scale animation, and rotation animation.

An interruption triggers if the [Scaffold] is given a new [FloatingActionButtonLocation] while it is still animating a transition between two previous [FloatingActionButtonLocation]s.

A sensible default is usually 0.0, which is the same as restarting the animation from the beginning, regardless of the original state of the animation.

### noAnimation

```dart
FloatingActionButtonAnimator noAnimation
```

Creates an instance of [FloatingActionButtonAnimator] where the [FloatingActionButton] does not animate on entrance and exit when [FloatingActionButtonLocation] is shown or hidden and when transitioning between [FloatingActionButtonLocation]s.

{@tool dartpad} This sample showcases how to override [FloatingActionButton] entrance and exit animations using [FloatingActionButtonAnimator.noAnimation] in [Scaffold.floatingActionButtonAnimator].

** See code in examples/api/lib/material/scaffold/scaffold.floating_action_button_animator.0.dart ** {@end-tool}

### toString()

```dart
String toString()
```
