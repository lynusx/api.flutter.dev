@docImport 'data_table.dart'; @docImport 'elevated_button.dart'; @docImport 'icon_button.dart'; @docImport 'ink_decoration.dart'; @docImport 'ink_ripple.dart'; @docImport 'ink_splash.dart'; @docImport 'text_button.dart';

# InteractiveInkFeature

```dart
abstract class InteractiveInkFeature extends InkFeature {}
```

An ink feature that displays a [color] "splash" in response to a user gesture that can be confirmed or canceled.

Subclasses call [confirm] when an input gesture is recognized. For example a press event might trigger an ink feature that's confirmed when the corresponding up event is seen.

Subclasses call [cancel] when an input gesture is aborted before it is recognized. For example a press event might trigger an ink feature that's canceled when the pointer is dragged out of the reference box.

The [InkWell] and [InkResponse] widgets generate instances of this class.

### InteractiveInkFeature()

```dart
InteractiveInkFeature({required MaterialInkController controller, required dynamic referenceBox, required Color color, ShapeBorder? customBorder, dynamic onRemoved})
```

Creates an InteractiveInkFeature.

### confirm()

```dart
void confirm()
```

Called when the user input that triggered this feature's appearance was confirmed.

Typically causes the ink to propagate faster across the material. By default this method does nothing.

### cancel()

```dart
void cancel()
```

Called when the user input that triggered this feature's appearance was canceled.

Typically causes the ink to gradually disappear. By default this method does nothing.

### color

```dart
Color get color
```

The ink's color.

### color

```dart
set color(Color value)
```

### customBorder

```dart
ShapeBorder? get customBorder
```

The ink's optional custom border.

### customBorder

```dart
set customBorder(ShapeBorder? value)
```

### paintInkCircle()

```dart
void paintInkCircle({required Canvas canvas, required Matrix4 transform, required Paint paint, required Offset center, required double radius, TextDirection? textDirection, ShapeBorder? customBorder, BorderRadius borderRadius = BorderRadius.zero, RectCallback? clipCallback})
```

Draws an ink splash or ink ripple on the passed in [Canvas].

The [transform] argument is the [Matrix4] transform that typically shifts the coordinate space of the canvas to the space in which the ink circle is to be painted.

[center] is the [Offset] from origin of the canvas where the center of the circle is drawn.

[paint] takes a [Paint] object that describes the styles used to draw the ink circle. For example, [paint] can specify properties like color, strokewidth, colorFilter.

[radius] is the radius of ink circle to be drawn on canvas.

[clipCallback] is the callback used to obtain the [Rect] used for clipping the ink effect. If [clipCallback] is null, no clipping is performed on the ink circle.

Clipping can happen in 3 different ways:

1.  If [customBorder] is provided, it is used to determine the path for clipping.
2.  If [customBorder] is null, and [borderRadius] is provided, the canvas is clipped by an [RRect] created from [clipCallback] and [borderRadius].
3.  If [borderRadius] is the default [BorderRadius.zero], then the [Rect] provided by [clipCallback] is used for clipping.

[textDirection] is used by [customBorder] if it is non-null. This allows the [customBorder]'s path to be properly defined if it was the path was expressed in terms of "start" and "end" instead of "left" and "right".

For examples on how the function is used, see [InkSplash] and [InkRipple].

# InteractiveInkFeatureFactory

```dart
abstract class InteractiveInkFeatureFactory {}
```

An encapsulation of an [InteractiveInkFeature] constructor used by [InkWell], [InkResponse], and [ThemeData].

Interactive ink feature implementations should provide a static const `splashFactory` value that's an instance of this class. The `splashFactory` can be used to configure an [InkWell], [InkResponse] or [ThemeData].

See also:

- [InkSplash.splashFactory]
- [InkRipple.splashFactory]

### InteractiveInkFeatureFactory()

```dart
InteractiveInkFeatureFactory()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

Subclasses should provide a const constructor.

### create()

```dart
InteractiveInkFeature create({required MaterialInkController controller, required RenderBox referenceBox, required Offset position, required Color color, required TextDirection textDirection, bool containedInkWell = false, RectCallback? rectCallback, BorderRadius? borderRadius, ShapeBorder? customBorder, double? radius, VoidCallback? onRemoved})
```

The factory method.

Subclasses should override this method to return a new instance of an [InteractiveInkFeature].

# InkResponse

```dart
class InkResponse extends StatelessWidget {}
```

An area of a [Material] that responds to touch. Has a configurable shape and can be configured to clip splashes that extend outside its bounds or not.

For a variant of this widget that is specialized for rectangular areas that always clip splashes, see [InkWell].

An [InkResponse] widget does two things when responding to a tap:

- It starts to animate a _highlight_. The shape of the highlight is determined by [highlightShape]. If it is a [BoxShape.circle], the default, then the highlight is a circle of fixed size centered in the [InkResponse]. If it is [BoxShape.rectangle], then the highlight is a box the size of the [InkResponse] itself, unless [getRectCallback] is provided, in which case that callback defines the rectangle. The color of the highlight is set by [highlightColor].

- Simultaneously, it starts to animate a _splash_. This is a growing circle initially centered on the tap location. If this is a [containedInkWell], the splash grows to the [radius] while remaining centered at the tap location. Otherwise, the splash migrates to the center of the box as it grows.

The following two diagrams show how [InkResponse] looks when tapped if the [highlightShape] is [BoxShape.circle] (the default) and [containedInkWell] is false (also the default).

The first diagram shows how it looks if the [InkResponse] is relatively large:

![The highlight is a disc centered in the box, smaller than the child widget.](https://flutter.github.io/assets-for-api-docs/assets/material/ink_response_large.png)

The second diagram shows how it looks if the [InkResponse] is small:

![The highlight is a disc overflowing the box, centered on the child.](https://flutter.github.io/assets-for-api-docs/assets/material/ink_response_small.png)

The main thing to notice from these diagrams is that the splashes happily exceed the bounds of the widget (because [containedInkWell] is false).

The following diagram shows the effect when the [InkResponse] has a [highlightShape] of [BoxShape.rectangle] with [containedInkWell] set to true. These are the values used by [InkWell].

![The highlight is a rectangle the size of the box.](https://flutter.github.io/assets-for-api-docs/assets/material/ink_well.png)

The [InkResponse] widget must have a [Material] widget as an ancestor. The [Material] widget is where the ink reactions are actually painted. This matches the Material Design premise wherein the [Material] is what is actually reacting to touches by spreading ink.

If a Widget uses this class directly, it should include the following line at the top of its build function to call [debugCheckHasMaterial]:

```dart
assert(debugCheckHasMaterial(context));
```

## Troubleshooting

### The ink splashes aren't visible!

If there is an opaque graphic, e.g. painted using a [Container], [Image], or [DecoratedBox], between the [Material] widget and the [InkResponse] widget, then the splash won't be visible because it will be under the opaque graphic. This is because ink splashes draw on the underlying [Material] itself, as if the ink was spreading inside the material.

The [Ink] widget can be used as a replacement for [Image], [Container], or [DecoratedBox] to ensure that the image or decoration also paints in the [Material] itself, below the ink.

If this is not possible for some reason, e.g. because you are using an opaque [CustomPaint] widget, alternatively consider using a second [Material] above the opaque widget but below the [InkResponse] (as an ancestor to the ink response). The [MaterialType.transparency] material kind can be used for this purpose.

See also:

- [GestureDetector], for listening for gestures without ink splashes.
- [ElevatedButton] and [TextButton], two kinds of buttons in Material Design.
- [IconButton], which combines [InkResponse] with an [Icon].

### InkResponse()

```dart
InkResponse({dynamic key, Widget? child, GestureTapCallback? onTap, GestureTapDownCallback? onTapDown, GestureTapUpCallback? onTapUp, GestureTapCallback? onTapCancel, GestureTapCallback? onDoubleTap, GestureLongPressCallback? onLongPress, GestureLongPressUpCallback? onLongPressUp, GestureTapCallback? onSecondaryTap, GestureTapUpCallback? onSecondaryTapUp, GestureTapDownCallback? onSecondaryTapDown, GestureTapCallback? onSecondaryTapCancel, ValueChanged<bool>? onHighlightChanged, ValueChanged<bool>? onHover, MouseCursor? mouseCursor, bool containedInkWell = false, BoxShape highlightShape = BoxShape.circle, double? radius, BorderRadius? borderRadius, ShapeBorder? customBorder, Color? focusColor, Color? hoverColor, Color? highlightColor, WidgetStateProperty<Color?>? overlayColor, Color? splashColor, InteractiveInkFeatureFactory? splashFactory, bool enableFeedback = true, bool excludeFromSemantics = false, FocusNode? focusNode, bool canRequestFocus = true, ValueChanged<bool>? onFocusChange, bool autofocus = false, MaterialStatesController? statesController, Duration? hoverDuration})
```

Creates an area of a [Material] that responds to touch.

Must have an ancestor [Material] widget in which to cause ink reactions.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### onTap

```dart
GestureTapCallback? onTap
```

Called when the user taps this part of the material.

### onTapDown

```dart
GestureTapDownCallback? onTapDown
```

Called when the user taps down this part of the material.

### onTapUp

```dart
GestureTapUpCallback? onTapUp
```

Called when the user releases a tap that was started on this part of the material. [onTap] is called immediately after.

### onTapCancel

```dart
GestureTapCallback? onTapCancel
```

Called when the user cancels a tap that was started on this part of the material.

### onDoubleTap

```dart
GestureTapCallback? onDoubleTap
```

Called when the user double taps this part of the material.

### onLongPress

```dart
GestureLongPressCallback? onLongPress
```

Called when the user long-presses on this part of the material.

### onLongPressUp

```dart
GestureLongPressUpCallback? onLongPressUp
```

Called when the user lifts their finger after a long press on the button.

This callback is triggered at the end of a long press gesture, specifically after the user holds a long press and then releases it. It does not include position details.

Common use cases include performing an action only after the long press completes, such as displaying a context menu or confirming a held gesture.

See also:

- [onLongPress], which is triggered when the long press gesture is first recognized.

### onSecondaryTap

```dart
GestureTapCallback? onSecondaryTap
```

Called when the user taps this part of the material with a secondary button.

See also:

- [kSecondaryButton], the button this callback responds to.

### onSecondaryTapDown

```dart
GestureTapDownCallback? onSecondaryTapDown
```

Called when the user taps down on this part of the material with a secondary button.

See also:

- [kSecondaryButton], the button this callback responds to.

### onSecondaryTapUp

```dart
GestureTapUpCallback? onSecondaryTapUp
```

Called when the user releases a secondary button tap that was started on this part of the material. [onSecondaryTap] is called immediately after.

See also:

- [onSecondaryTap], a handler triggered right after this one that doesn't pass any details about the tap.
- [kSecondaryButton], the button this callback responds to.

### onSecondaryTapCancel

```dart
GestureTapCallback? onSecondaryTapCancel
```

Called when the user cancels a secondary button tap that was started on this part of the material.

See also:

- [kSecondaryButton], the button this callback responds to.

### onHighlightChanged

```dart
ValueChanged<bool>? onHighlightChanged
```

Called when this part of the material either becomes highlighted or stops being highlighted.

The value passed to the callback is true if this part of the material has become highlighted and false if this part of the material has stopped being highlighted.

If all of [onTap], [onDoubleTap], [onLongPress], and [onLongPressUp] become null while a gesture is ongoing, then [onTapCancel] will be fired and [onHighlightChanged] will be fired with the value false _during the build_. This means, for instance, that in that scenario [State.setState] cannot be called.

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the ink response area.

The value passed to the callback is true if a pointer has entered this part of the material and false if a pointer has exited this part of the material.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

{@template flutter.material.InkWell.mouseCursor} If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### containedInkWell

```dart
bool containedInkWell
```

Whether this ink response should be clipped its bounds.

This flag also controls whether the splash migrates to the center of the [InkResponse] or not. If [containedInkWell] is true, the splash remains centered around the tap location. If it is false, the splash migrates to the center of the [InkResponse] as it grows.

See also:

- [highlightShape], the shape of the focus, hover, and pressed highlights.
- [borderRadius], which controls the corners when the box is a rectangle.
- [getRectCallback], which controls the size and position of the box when it is a rectangle.

### highlightShape

```dart
BoxShape highlightShape
```

The shape (e.g., circle, rectangle) to use for the highlight drawn around this part of the material when pressed, hovered over, or focused.

The same shape is used for the pressed highlight (see [highlightColor]), the focus highlight (see [focusColor]), and the hover highlight (see [hoverColor]).

If the shape is [BoxShape.circle], then the highlight is centered on the [InkResponse]. If the shape is [BoxShape.rectangle], then the highlight fills the [InkResponse], or the rectangle provided by [getRectCallback] if the callback is specified.

See also:

- [containedInkWell], which controls clipping behavior.
- [borderRadius], which controls the corners when the box is a rectangle.
- [highlightColor], the color of the highlight.
- [getRectCallback], which controls the size and position of the box when it is a rectangle.

### radius

```dart
double? radius
```

The radius of the ink splash.

Splashes grow up to this size. By default, this size is determined from the size of the rectangle provided by [getRectCallback], or the size of the [InkResponse] itself.

See also:

- [splashColor], the color of the splash.
- [splashFactory], which defines the appearance of the splash.

### borderRadius

```dart
BorderRadius? borderRadius
```

The border radius of the containing rectangle. This is effective only if [highlightShape] is [BoxShape.rectangle].

If this is null, it is interpreted as [BorderRadius.zero].

### customBorder

```dart
ShapeBorder? customBorder
```

The custom clip border.

If this is null, the ink response will not clip its content.

### focusColor

```dart
Color? focusColor
```

The color of the ink response when the parent widget is focused. If this property is null then the focus color of the theme, [ThemeData.focusColor], will be used.

See also:

- [highlightShape], the shape of the focus, hover, and pressed highlights.
- [hoverColor], the color of the hover highlight.
- [splashColor], the color of the splash.
- [splashFactory], which defines the appearance of the splash.

### hoverColor

```dart
Color? hoverColor
```

The color of the ink response when a pointer is hovering over it. If this property is null then the hover color of the theme, [ThemeData.hoverColor], will be used.

See also:

- [highlightShape], the shape of the focus, hover, and pressed highlights.
- [highlightColor], the color of the pressed highlight.
- [focusColor], the color of the focus highlight.
- [splashColor], the color of the splash.
- [splashFactory], which defines the appearance of the splash.

### highlightColor

```dart
Color? highlightColor
```

The highlight color of the ink response when pressed. If this property is null then the highlight color of the theme, [ThemeData.highlightColor], will be used.

See also:

- [hoverColor], the color of the hover highlight.
- [focusColor], the color of the focus highlight.
- [highlightShape], the shape of the focus, hover, and pressed highlights.
- [splashColor], the color of the splash.
- [splashFactory], which defines the appearance of the splash.

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

Defines the ink response focus, hover, and splash colors.

This default null property can be used as an alternative to [focusColor], [hoverColor], [highlightColor], and [splashColor]. If non-null, it is resolved against one of [WidgetState.focused], [WidgetState.hovered], and [WidgetState.pressed]. It's convenient to use when the parent widget can pass along its own WidgetStateProperty value for the overlay color.

[WidgetState.pressed] triggers a ripple (an ink splash), per the current Material Design spec. The [overlayColor] doesn't map a state to [highlightColor] because a separate highlight is not used by the current design guidelines. See https://material.io/design/interaction/states.html#pressed

If the overlay color is null or resolves to null, then [focusColor], [hoverColor], [splashColor] and their defaults are used instead.

See also:

- The Material Design specification for overlay colors and how they match a component's state: <https://material.io/design/interaction/states.html#anatomy>.

### splashColor

```dart
Color? splashColor
```

The splash color of the ink response. If this property is null then the splash color of the theme, [ThemeData.splashColor], will be used.

See also:

- [splashFactory], which defines the appearance of the splash.
- [radius], the (maximum) size of the ink splash.
- [highlightColor], the color of the highlight.

### splashFactory

```dart
InteractiveInkFeatureFactory? splashFactory
```

Defines the appearance of the splash.

Defaults to the value of the theme's splash factory: [ThemeData.splashFactory].

See also:

- [radius], the (maximum) size of the ink splash.
- [splashColor], the color of the splash.
- [highlightColor], the color of the highlight.
- [InkSplash.splashFactory], which defines the default splash.
- [InkRipple.splashFactory], which defines a splash that spreads out more aggressively than the default.

### enableFeedback

```dart
bool enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

Whether to exclude the gestures introduced by this widget from the semantics tree.

For example, a long-press gesture for showing a tooltip is usually excluded because the tooltip itself is included in the semantics tree directly and so having a gesture to show it would result in duplication of information.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

{@template flutter.material.inkwell.onFocusChange} Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus. {@endtemplate}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### canRequestFocus

```dart
bool canRequestFocus
```

{@macro flutter.widgets.Focus.canRequestFocus}

### getRectCallback()

```dart
RectCallback? getRectCallback(RenderBox referenceBox)
```

The rectangle to use for the highlight effect and for clipping the splash effects if [containedInkWell] is true.

This method is intended to be overridden by descendants that specialize [InkResponse] for unusual cases. For example, [TableRowInkWell] implements this method to return the rectangle corresponding to the row that the widget is in.

The default behavior returns null, which is equivalent to returning the referenceBox argument's bounding box (though slightly more efficient).

### statesController

```dart
MaterialStatesController? statesController
```

{@template flutter.material.inkwell.statesController} Represents the interactive "state" of this widget in terms of a set of [WidgetState]s, like [WidgetState.pressed] and [WidgetState.focused].

Classes based on this one can provide their own [WidgetStatesController] to which they've added listeners. They can also update the controller's [WidgetStatesController.value] however, this may only be done when it's safe to call [State.setState], like in an event handler. {@endtemplate}

### hoverDuration

```dart
Duration? hoverDuration
```

The duration of the animation that animates the hover effect.

The default is 50ms.

### build()

```dart
Widget build(BuildContext context)
```

### debugCheckContext()

```dart
bool debugCheckContext(BuildContext context)
```

Asserts that the given context satisfies the prerequisites for this class.

This method is intended to be overridden by descendants that specialize [InkResponse] for unusual cases. For example, [TableRowInkWell] implements this method to verify that the widget is in a table.

# InkWell

```dart
class InkWell extends InkResponse {}
```

A rectangular area of a [Material] that responds to touch.

For a variant of this widget that does not clip splashes, see [InkResponse].

The following diagram shows how an [InkWell] looks when tapped, when using default values.

![The highlight is a rectangle the size of the box.](https://flutter.github.io/assets-for-api-docs/assets/material/ink_well.png)

The [InkWell] widget must have a [Material] widget as an ancestor. The [Material] widget is where the ink reactions are actually painted. This matches the Material Design premise wherein the [Material] is what is actually reacting to touches by spreading ink.

If a Widget uses this class directly, it should include the following line at the top of its build function to call [debugCheckHasMaterial]:

```dart
assert(debugCheckHasMaterial(context));
```

## Troubleshooting

### The ink splashes aren't visible!

If there is an opaque graphic, e.g. painted using a [Container], [Image], or [DecoratedBox], between the [Material] widget and the [InkWell] widget, then the splash won't be visible because it will be under the opaque graphic. This is because ink splashes draw on the underlying [Material] itself, as if the ink was spreading inside the material.

The [Ink] widget can be used as a replacement for [Image], [Container], or [DecoratedBox] to ensure that the image or decoration also paints in the [Material] itself, below the ink.

If this is not possible for some reason, e.g. because you are using an opaque [CustomPaint] widget, alternatively consider using a second [Material] above the opaque widget but below the [InkWell] (as an ancestor to the ink well). The [MaterialType.transparency] material kind can be used for this purpose.

### InkWell isn't clipping properly

If you want to clip an InkWell or any [Ink] widgets you need to keep in mind that the [Material] that the Ink will be printed on is responsible for clipping. This means you can't wrap the [Ink] widget in a clipping widget directly, since this will leave the [Material] not clipped (and by extension the printed [Ink] widgets as well).

An easy solution is to deliberately wrap the [Ink] widgets you want to clip in a [Material], and wrap that in a clipping widget instead. See [Ink] for an example.

### The ink splashes don't track the size of an animated container

If the size of an InkWell's [Material] ancestor changes while the InkWell's splashes are expanding, you may notice that the splashes aren't clipped correctly. This can't be avoided.

An example of this situation is as follows:

{@tool dartpad} Tap the container to cause it to grow. Then, tap it again and hold before the widget reaches its maximum size to observe the clipped ink splash.

** See code in examples/api/lib/material/ink_well/ink_well.0.dart ** {@end-tool}

An InkWell's splashes will not properly update to conform to changes if the size of its underlying [Material], where the splashes are rendered, changes during animation. You should avoid using InkWells within [Material] widgets that are changing size.

See also:

- [GestureDetector], for listening for gestures without ink splashes.
- [ElevatedButton] and [TextButton], two kinds of buttons in Material Design.
- [InkResponse], a variant of [InkWell] that doesn't force a rectangular shape on the ink reaction.

### InkWell()

```dart
InkWell({dynamic key, dynamic child, dynamic onTap, dynamic onDoubleTap, dynamic onLongPress, dynamic onLongPressUp, dynamic onTapDown, dynamic onTapUp, dynamic onTapCancel, dynamic onSecondaryTap, dynamic onSecondaryTapUp, dynamic onSecondaryTapDown, dynamic onSecondaryTapCancel, dynamic onHighlightChanged, dynamic onHover, dynamic mouseCursor, dynamic focusColor, dynamic hoverColor, dynamic highlightColor, dynamic overlayColor, dynamic splashColor, InteractiveInkFeatureFactory? splashFactory, double? radius, dynamic borderRadius, dynamic customBorder, bool enableFeedback, bool excludeFromSemantics, dynamic focusNode, bool canRequestFocus, dynamic onFocusChange, bool autofocus, dynamic statesController, Duration? hoverDuration})
```

Creates an ink well.

Must have an ancestor [Material] widget in which to cause ink reactions.
