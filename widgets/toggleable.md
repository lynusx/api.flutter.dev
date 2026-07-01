@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# ToggleableStateMixin

```dart
mixin ToggleableStateMixin<S extends StatefulWidget> on TickerProviderStateMixin<S> {}
```

A mixin for [StatefulWidget]s that implement toggleable controls with toggle animations (e.g. [Switch]es, [CupertinoSwitch]es, [Checkbox]es, [CupertinoCheckbox]es, [Radio]s, and [CupertinoRadio]s).

The mixin implements the logic for toggling the control (e.g. when tapped) and provides a series of animation controllers to transition the control from one state to another. It does not have any opinion about the visual representation of the toggleable widget. The visuals are defined by a [CustomPainter] passed to the [buildToggleable]. [State] objects using this mixin should call that method from their [build] method.

### positionController

```dart
AnimationController get positionController
```

Used by subclasses to manipulate the visual value of the control.

Some controls respond to user input by updating their visual value. For example, the thumb of a switch moves from one position to another when dragged. These controls manipulate this animation controller to update their [position] and eventually trigger an [onChanged] callback when the animation reaches either 0.0 or 1.0.

### position

```dart
CurvedAnimation get position
```

The visual value of the control.

When the control is inactive, the [value] is false and this animation has the value 0.0. When the control is active, the value is either true or tristate is true and the value is null. When the control is active the animation has a value of 1.0. When the control is changing from inactive to active (or vice versa), [value] is the target value and this animation gradually updates from 0.0 to 1.0 (or vice versa).

### reactionController

```dart
AnimationController get reactionController
```

Used by subclasses to control the radial reaction animation.

Some controls have a radial ink reaction to user input. This animation controller can be used to start or stop these ink reactions.

To paint the actual radial reaction, [ToggleablePainter.paintRadialReaction] may be used.

### reaction

```dart
CurvedAnimation get reaction
```

The visual value of the radial reaction animation.

Some controls have a radial ink reaction to user input. This animation controls the progress of these ink reactions.

To paint the actual radial reaction, [ToggleablePainter.paintRadialReaction] may be used.

### reactionHoverFade

```dart
CurvedAnimation get reactionHoverFade
```

Controls the radial reaction's opacity animation for hover changes.

Some controls have a radial ink reaction to pointer hover. This animation controls these ink reaction fade-ins and fade-outs.

To paint the actual radial reaction, [ToggleablePainter.paintRadialReaction] may be used.

### reactionFocusFade

```dart
CurvedAnimation get reactionFocusFade
```

Controls the radial reaction's opacity animation for focus changes.

Some controls have a radial ink reaction to focus. This animation controls these ink reaction fade-ins and fade-outs.

To paint the actual radial reaction, [ToggleablePainter.paintRadialReaction] may be used.

### reactionAnimationDuration

```dart
Duration? get reactionAnimationDuration
```

The amount of time a circular ink response should take to expand to its full size if a radial reaction is drawn using [ToggleablePainter.paintRadialReaction].

### isInteractive

```dart
bool get isInteractive
```

Whether [value] of this control can be changed by user interaction.

The control is considered interactive if the [onChanged] callback is non-null. If the callback is null, then the control is disabled, and non-interactive. A disabled checkbox, for example, is displayed using a grey color and its value cannot be changed.

### onChanged

```dart
ValueChanged<bool?>? get onChanged
```

Called when the control changes value.

If the control is tapped, [onChanged] is called immediately with the new value.

The control is considered interactive (see [isInteractive]) if this callback is non-null. If the callback is null, then the control is disabled, and non-interactive. A disabled checkbox, for example, is displayed using a grey color and its value cannot be changed.

### value

```dart
bool? get value
```

False if this control is "inactive" (not checked, off, or unselected).

If value is true then the control "active" (checked, on, or selected). If tristate is true and value is null, then the control is considered to be in its third or "indeterminate" state.

When the value changes, this object starts the [positionController] and [position] animations to animate the visual appearance of the control to the new value.

### tristate

```dart
bool get tristate
```

If true, [value] can be true, false, or null, otherwise [value] must be true or false.

When [tristate] is true and [value] is null, then the control is considered to be in its third or "indeterminate" state.

### initState()

```dart
void initState()
```

### animateToValue()

```dart
void animateToValue()
```

Runs the [position] animation to transition the Toggleable's appearance to match [value].

This method must be called whenever [value] changes to ensure that the visual representation of the Toggleable matches the current [value].

### dispose()

```dart
void dispose()
```

### downPosition

```dart
Offset? get downPosition
```

The most recent [Offset] at which a pointer touched the Toggleable.

This is null if currently no pointer is touching the Toggleable or if [isInteractive] is false.

### states

```dart
Set<WidgetState> get states
```

Describes the current [WidgetState] of the Toggleable.

The returned set will include:

- [WidgetState.disabled], if [isInteractive] is false
- [WidgetState.hovered], if a pointer is hovering over the Toggleable
- [WidgetState.focused], if the Toggleable has input focus
- [WidgetState.selected], if [value] is true or null

### buildToggleable()

```dart
Widget buildToggleable({FocusNode? focusNode, ValueChanged<bool>? onFocusChange, bool autofocus = false, WidgetStateProperty<MouseCursor>? mouseCursor, required Size size, required CustomPainter painter})
```

Typically wraps a `painter` that draws the actual visuals of the Toggleable with logic to toggle it.

Use [buildToggleableWithChild] if one would like to provide a [Widget] instead of [CustomPainter].

If drawing a radial ink reaction is desired (in Material Design for example), consider providing a subclass of [ToggleablePainter] as a `painter`, which implements logic to draw a radial ink reaction for this control. The painter is usually configured with the [reaction], [position], [reactionHoverFade], and [reactionFocusFade] animation provided by this mixin. It is expected to draw the visuals of the Toggleable based on the current value of these animations. The animations are triggered by this mixin to transition the Toggleable from one state to another.

Material Toggleables must provide a [mouseCursor] which resolves to a [MouseCursor] based on the current [WidgetState] of the Toggleable. Cupertino Toggleables may not provide a [mouseCursor]. If no [mouseCursor] is provided, [SystemMouseCursors.basic] will be used as the [mouseCursor] across all [WidgetState]s.

This method must be called from the [build] method of the [State] class that uses this mixin. The returned [Widget] must be returned from the build method - potentially after wrapping it in other widgets.

### buildToggleableWithChild()

```dart
Widget buildToggleableWithChild({FocusNode? focusNode, ValueChanged<bool>? onFocusChange, bool autofocus = false, WidgetStateProperty<MouseCursor>? mouseCursor, required Widget child})
```

Typically wraps a child that draws the actual visuals of the Toggleable with logic to toggle it.

{@template flutter.widgets.ToggleableStateMixin.buildToggleableWithChild} If drawing a radial ink reaction is desired (in Material Design for example), consider providing [CustomPaint] with a subclass of [ToggleablePainter] as a [CustomPaint.painter], which implements logic to draw a radial ink reaction for this control. The painter is usually configured with the [ToggleableStateMixin.reaction], [ToggleableStateMixin.position], [ToggleableStateMixin.reactionHoverFade], and [ToggleableStateMixin.reactionFocusFade] animation provided by this mixin. It is expected to draw the visuals of the Toggleable based on the current value of these animations. The animations are triggered by this mixin to transition the Toggleable from one state to another. {@endtemplate}

Material Toggleables must provide a [mouseCursor] which resolves to a [MouseCursor] based on the current [WidgetState] of the Toggleable. Cupertino Toggleables may not provide a [mouseCursor]. If no [mouseCursor] is provided, [SystemMouseCursors.basic] will be used as the [mouseCursor] across all [WidgetState]s.

This method must be called from the [build] method of the [State] class that uses this mixin. The returned [Widget] must be returned from the build method - potentially after wrapping it in other widgets.

# ToggleablePainter

```dart
abstract class ToggleablePainter extends ChangeNotifier implements CustomPainter {}
```

A base class for a [CustomPainter] that may be passed to [ToggleableStateMixin.buildToggleable] to draw the visual representation of a Toggleable.

Subclasses must implement the [paint] method to draw the actual visuals of the Toggleable.

If drawing a radial ink reaction is desired (in Material Design for example), subclasses may call [paintRadialReaction] in their [paint] method.

### position

```dart
Animation<double> get position
```

The visual value of the control.

Usually set to [ToggleableStateMixin.position].

### position

```dart
set position(Animation<double> value)
```

### reaction

```dart
Animation<double> get reaction
```

The visual value of the radial reaction animation.

Usually set to [ToggleableStateMixin.reaction].

### reaction

```dart
set reaction(Animation<double> value)
```

### reactionFocusFade

```dart
Animation<double> get reactionFocusFade
```

Controls the radial reaction's opacity animation for focus changes.

Usually set to [ToggleableStateMixin.reactionFocusFade].

### reactionFocusFade

```dart
set reactionFocusFade(Animation<double> value)
```

### reactionHoverFade

```dart
Animation<double> get reactionHoverFade
```

Controls the radial reaction's opacity animation for hover changes.

Usually set to [ToggleableStateMixin.reactionHoverFade].

### reactionHoverFade

```dart
set reactionHoverFade(Animation<double> value)
```

### activeColor

```dart
Color get activeColor
```

The color that should be used in the active state (i.e., when [ToggleableStateMixin.value] is true).

For example, a checkbox should use this color when checked.

### activeColor

```dart
set activeColor(Color value)
```

### inactiveColor

```dart
Color get inactiveColor
```

The color that should be used in the inactive state (i.e., when [ToggleableStateMixin.value] is false).

For example, a checkbox should use this color when unchecked.

### inactiveColor

```dart
set inactiveColor(Color value)
```

### inactiveReactionColor

```dart
Color get inactiveReactionColor
```

The color that should be used for the reaction when the toggleable is inactive.

Used when the toggleable needs to change the reaction color/transparency that is displayed when the toggleable is inactive and tapped.

### inactiveReactionColor

```dart
set inactiveReactionColor(Color value)
```

### reactionColor

```dart
Color get reactionColor
```

The color that should be used for the reaction when the toggleable is active.

Used when the toggleable needs to change the reaction color/transparency that is displayed when the toggleable is active and tapped.

### reactionColor

```dart
set reactionColor(Color value)
```

### hoverColor

```dart
Color get hoverColor
```

The color that should be used for the reaction when [isHovered] is true.

Used when the toggleable needs to change the reaction color/transparency, when it is being hovered over.

### hoverColor

```dart
set hoverColor(Color value)
```

### focusColor

```dart
Color get focusColor
```

The color that should be used for the reaction when [isFocused] is true.

Used when the toggleable needs to change the reaction color/transparency, when it has focus.

### focusColor

```dart
set focusColor(Color value)
```

### splashRadius

```dart
double get splashRadius
```

The splash radius for the radial reaction.

### splashRadius

```dart
set splashRadius(double value)
```

### downPosition

```dart
Offset? get downPosition
```

The [Offset] within the Toggleable at which a pointer touched the Toggleable.

This is null if currently no pointer is touching the Toggleable.

Usually set to [ToggleableStateMixin.downPosition].

### downPosition

```dart
set downPosition(Offset? value)
```

### isFocused

```dart
bool get isFocused
```

True if this toggleable has the input focus.

### isFocused

```dart
set isFocused(bool? value)
```

### isHovered

```dart
bool get isHovered
```

True if this toggleable is being hovered over by a pointer.

### isHovered

```dart
set isHovered(bool? value)
```

### isActive

```dart
bool get isActive
```

Determines whether the toggleable shows as active.

### isActive

```dart
set isActive(bool? value)
```

### paintRadialReaction()

```dart
void paintRadialReaction({required Canvas canvas, Offset offset = Offset.zero, required Offset origin})
```

Used by subclasses to paint the radial ink reaction for this control.

The reaction is painted on the given canvas at the given offset. The origin is the center point of the reaction (usually distinct from the [downPosition] at which the user interacted with the control).

### dispose()

```dart
void dispose()
```

### shouldRepaint()

```dart
bool shouldRepaint(CustomPainter oldDelegate)
```

### hitTest()

```dart
bool? hitTest(Offset position)
```

### semanticsBuilder

```dart
SemanticsBuilderCallback? get semanticsBuilder
```

### shouldRebuildSemantics()

```dart
bool shouldRebuildSemantics(CustomPainter oldDelegate)
```

### toString()

```dart
String toString()
```
