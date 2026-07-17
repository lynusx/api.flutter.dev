# WindowPositionerAnchor

```dart
enum WindowPositionerAnchor {}
```

Defines how a child window will be placed relative to the anchor rectangle of its parent.

The specified anchor is used to derive an anchor point on the anchor rectangle that the child [BaseWindowController] will be positioned relative to. If a corner anchor is set (e.g. [topLeft] or [bottomRight]), the anchor point will be at the specified corner; otherwise, the derived anchor point will be centered on the specified edge, or in the center of the anchor rectangle if no edge is specified.

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [center], then the child window will be positioned relative to the center of the parent window.

If [WindowPositioner.childAnchor] is set to [center], then the middle of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [top], then the child window will be positioned relative to the top of the parent window.

If [WindowPositioner.childAnchor] is set to [top], then the top of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [bottom], then the child window will be positioned relative to the bottom of the parent window.

If [WindowPositioner.childAnchor] is set to [bottom], then the bottom of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [left], then the child window will be positioned relative to the left of the parent window.

If [WindowPositioner.childAnchor] is set to [left], then the left of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [right], then the child window will be positioned relative to the right of the parent window.

If [WindowPositioner.childAnchor] is set to [right], then the right of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [topLeft], then the child window will be positioned relative to the top left of the parent window.

If [WindowPositioner.childAnchor] is set to [topLeft], then the top left of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [bottomLeft], then the child window will be positioned relative to the bottom left of the parent window.

If [WindowPositioner.childAnchor] is set to [bottomLeft], then the bottom left of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [topRight], then the child window will be positioned relative to the top right of the parent window.

If [WindowPositioner.childAnchor] is set to [topRight], then the top right of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

If the [WindowPositioner.parentAnchor] is set to [bottomRight], then the child window will be positioned relative to the bottom right of the parent window.

If [WindowPositioner.childAnchor] is set to [bottomRight], then the bottom right of the child window will be positioned relative to [WindowPositioner.parentAnchor].

{@macro flutter.widgets.windowing.experimental}

# WindowPositionerConstraintAdjustment

```dart
class WindowPositionerConstraintAdjustment {}
```

The [WindowPositionerConstraintAdjustment] describes how a window will adjust its position when it would be partly constrained by the platform.

{@template flutter.widgets.window_positioner.constraint_adjustment} Whether a window is considered "constrained" is left to the platform to determine. For example, the window may be partly outside the output's 'work area', thus necessitating the child window's position be adjusted until it is entirely inside the work area.

The adjustments can be combined, according to a defined precedence:

1.  [WindowPositionerConstraintAdjustment.flipX] and [WindowPositionerConstraintAdjustment.flipY]
2.  [WindowPositionerConstraintAdjustment.slideX] and [WindowPositionerConstraintAdjustment.slideY]
3.  [WindowPositionerConstraintAdjustment.resizeX] and [WindowPositionerConstraintAdjustment.resizeY]

The first adjustment that results in the child window being entirely inside the work area will be picked. {@endtemplate}

{@macro flutter.widgets.windowing.experimental}

### WindowPositionerConstraintAdjustment()

```dart
WindowPositionerConstraintAdjustment({bool flipX = false, bool flipY = false, bool slideX = false, bool slideY = false, bool resizeX = false, bool resizeY = false})
```

### slideX

```dart
bool slideX
```

If [slideX] is `true` and the window would be displayed off the screen in the X-axis,then it will be translated in the X-direction (either negative or positive) in order to best display the window on screen.

{@macro flutter.widgets.windowing.experimental}

### slideY

```dart
bool slideY
```

If [slideY] is `true` and the window would be displayed off the screen in the Y-axis, then it will be translated in the Y-direction (either negative or positive) in order to best display the window on screen.

{@macro flutter.widgets.windowing.experimental}

### flipX

```dart
bool flipX
```

If [flipX] is `true` and the window would be displayed off the screen in the X-axis in one direction, then it will be flipped to the opposite side of its parent in order to best display the window on screen.

{@macro flutter.widgets.windowing.experimental}

### flipY

```dart
bool flipY
```

If [flipY] is `true` and the window would be displayed off the screen in the Y-axis in one direction, then it will be flipped to the opposite side of its parent in order to best display the window on screen.

{@macro flutter.widgets.windowing.experimental}

### resizeX

```dart
bool resizeX
```

If [resizeX] is `true` and the window would be displayed off the screen in the X-axis, then its width will be reduced such that it fits on screen.

{@macro flutter.widgets.windowing.experimental}

### resizeY

```dart
bool resizeY
```

If `true` and the window would be displayed off the screen in the Y-axis, then its height will be reduced such that it fits on screen.

{@macro flutter.widgets.windowing.experimental}

### toString()

```dart
String toString()
```

# WindowPositioner

```dart
class WindowPositioner {}
```

The [WindowPositioner] defines how child windows are placed relative to their parent window.

For example, the rules may be defined such that the child window remains within the visible area's borders, and to specify how the child window changes its position, such as sliding along an axis, or flipping around a rectangle.

See also:

- [TooltipWindowController], a subclass of [BaseWindowController] that uses [WindowPositioner] to position tooltip windows.
- [WindowPositionerAnchor], which defines anchor points for positioning windows.
- [WindowPositionerConstraintAdjustment], which defines how windows adjust their position when they would be partly constrained by the platform.

{@macro flutter.widgets.windowing.experimental}

### WindowPositioner()

```dart
WindowPositioner({WindowPositionerAnchor parentAnchor = WindowPositionerAnchor.center, WindowPositionerAnchor childAnchor = WindowPositionerAnchor.center, Offset offset = Offset.zero, WindowPositionerConstraintAdjustment constraintAdjustment = const WindowPositionerConstraintAdjustment()})
```

Const constructor for [WindowPositioner].

### copyWith()

```dart
WindowPositioner copyWith({WindowPositionerAnchor? parentAnchor, WindowPositionerAnchor? childAnchor, Offset? offset, WindowPositionerConstraintAdjustment? constraintAdjustment})
```

Copy a [WindowPositioner] with some fields replaced.

### parentAnchor

```dart
WindowPositionerAnchor parentAnchor
```

Defines the point on the parent from which to position the child.

The specified anchor is used to derive an anchor point that the child window will be positioned relative to. If a corner anchor is set (e.g. [WindowPositionerAnchor.topLeft] or [WindowPositionerAnchor.bottomRight]), the anchor point will be at the specified corner; otherwise, the derived anchor point will be centered on the specified edge, or in the center of the anchor rectangle if no edge is specified.

The child is positioned by placing [childAnchor] on top of [parentAnchor] and then translating by [offset].

Defaults to [WindowPositionerAnchor.center].

{@macro flutter.widgets.windowing.experimental}

### childAnchor

```dart
WindowPositionerAnchor childAnchor
```

Defines the point on the child that is positioned relative to the parent.

The specified anchor is used to derive an anchor point that will be positioned relative to the [parentAnchor]. If a corner anchor is set (e.g. [WindowPositionerAnchor.topLeft] or [WindowPositionerAnchor.bottomRight]), the anchor point will be at the specified corner; otherwise, the derived anchor point will be centered on the specified edge, or in the center of the anchor rectangle if no edge is specified.

The child is positioned by placing [childAnchor] on top of [parentAnchor] and then translating by [offset].

Defaults to [WindowPositionerAnchor.center].

{@macro flutter.widgets.windowing.experimental}

### offset

```dart
Offset offset
```

The offset with which to place the child relative to the parent.

The child is positioned by placing [childAnchor] on top of [parentAnchor] and then translating by [offset].

For example if the anchor of the anchor rectangle is at (x, y), the window has a [childAnchor] of [WindowPositionerAnchor.topLeft], and the [offset] is (ox, oy), the calculated window position will be (x + ox, y + oy). The offset position of the window is the one used for constraint testing. See [constraintAdjustment].

An example use case is placing a popup menu on top of a user interface element, while aligning the user interface element of the parent window with some user interface element placed somewhere in the popup window.

Defaults to [Offset.zero].

{@macro flutter.widgets.windowing.experimental}

### constraintAdjustment

```dart
WindowPositionerConstraintAdjustment constraintAdjustment
```

Defines how Flutter will adjust the position of the window if the unadjusted position would result in the window being partly constrained by the platform.

{@macro flutter.widgets.window_positioner.constraint_adjustment}

The first adjustment that results in the child window being entirely inside the work area will be picked.

See also:

- [WindowPositionerConstraintAdjustment] for details on each adjustment type.

{@macro flutter.widgets.windowing.experimental}

### placeWindow()

```dart
Rect placeWindow({required Size childSize, required Rect anchorRect, required Rect parentRect, required Rect displayRect})
```

Computes the screen-space rectangle for a child window placed according to this [WindowPositioner].

[childSize] is the frame size of the child window.

[anchorRect] is the rectangle relative to which the child window is placed.

[parentRect] is the parent window's rectangle.

[displayRect] is the output display area where the child window will be placed.

All sizes and rectangles are in physical coordinates.

{@macro flutter.widgets.windowing.experimental}

### toString()

```dart
String toString()
```
