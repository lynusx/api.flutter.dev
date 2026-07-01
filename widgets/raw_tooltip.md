@docImport 'package:flutter/material.dart';

@docImport 'gesture_detector.dart';

# TooltipComponentBuilder

```dart
typedef TooltipComponentBuilder = Widget Function(BuildContext context, Animation<double> animation)
```

Signature for building the tooltip overlay child.

The animation property exposes the underlying tooltip overlay child show and hide animation. This can be used to drive animations that sync up with the tooltip overlay child show/hide animation, for example to fade the tooltip in and out.

# TooltipPositionDelegate

```dart
typedef TooltipPositionDelegate = Offset Function(TooltipPositionContext context)
```

Signature for computing the position of a tooltip.

The [TooltipPositionContext] contains all the necessary information for positioning the tooltip, including the target location, sizes, offset, and positioning preference.

Returns the offset from the top left of the overlay to the top left of the tooltip.

See also:

- [TooltipPositionContext], which contains the positioning parameters.

# TooltipPositionContext

```dart
class TooltipPositionContext {}
```

Contextual information for positioning a tooltip.

This immutable data class contains all the necessary information for computing the position of a tooltip relative to its target widget.

See also:

- [TooltipPositionDelegate], which uses this context to compute tooltip positions.

### TooltipPositionContext()

```dart
TooltipPositionContext({required Offset target, required Size targetSize, required Size tooltipSize, required double verticalOffset, bool preferBelow = true, Size overlaySize = Size.infinite})
```

Creates a tooltip position context.

### target

```dart
Offset target
```

The center point of the target widget in the global coordinate system.

### targetSize

```dart
Size targetSize
```

The size of the target widget that triggers the tooltip.

### tooltipSize

```dart
Size tooltipSize
```

The size of the tooltip itself.

### verticalOffset

```dart
double verticalOffset
```

The configured vertical offset.

### preferBelow

```dart
bool preferBelow
```

Whether the tooltip prefers to be positioned below the target.

### overlaySize

```dart
Size overlaySize
```

The size of the overlay within which the tooltip is displayed.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# TooltipTriggerMode

```dart
enum TooltipTriggerMode {}
```

How touch events should trigger a tooltip.

When using a pointer device like a mouse, a tooltip is shown as soon as a pointer hovers over the widget, regardless of the value of [RawTooltip.triggerMode].

A tooltip might also be triggered through other means regardless of this option, such as by calling `ensureTooltipVisible`.

See also:

- [RawTooltip.triggerMode], which uses this enum.

See also:

- [RawTooltip.hoverDelay], which defines the length of time that a pointer must hover over a tooltip's widget before the tooltip will be shown.

Tooltip will not be triggered by touch events.

Tooltip will be shown after a long press.

See also:

- [GestureDetector.onLongPress], the event that is used for trigger.
- [Feedback.forLongPress], the feedback method called when feedback is enabled.

Tooltip will be shown after a single tap.

See also:

- [GestureDetector.onTap], the event that is used for trigger.
- [Feedback.forTap], the feedback method called when feedback is enabled.

# TooltipTriggeredCallback

```dart
typedef TooltipTriggeredCallback = VoidCallback
```

Signature for when a tooltip is triggered.

# RawTooltip

```dart
class RawTooltip extends StatefulWidget {}
```

A widget that wraps a child to display an informative overlay in response to user interactions, such as hovering or long-pressing.

Tooltips provide essential context by displaying text labels or brief descriptions that explain the function of a button or other user interface elements.

The tooltip can be triggered in several ways:

- By hovering a mouse pointer over the widget.
- By touch interactions, such as a long press or a tap, depending on the configuration of [triggerMode].
- Manually, by calling [RawTooltipState.ensureTooltipVisible].

See also:

- [Tooltip], a Material-themed [RawTooltip].

{@tool dartpad} This example shows how [RawTooltip] can be shown manually with [TooltipTriggerMode.manual] by calling the [TooltipState.ensureTooltipVisible] function.

** See code in examples/api/lib/widgets/raw_tooltip/raw_tooltip.0.dart ** {@end-tool}

### RawTooltip()

```dart
RawTooltip({dynamic key, required String? semanticsTooltip, required TooltipComponentBuilder tooltipBuilder, Duration hoverDelay = Duration.zero, Duration touchDelay = const Duration(milliseconds: 1500), Duration dismissDelay = const Duration(milliseconds: 100), bool enableTapToDismiss = true, TooltipTriggerMode triggerMode = TooltipTriggerMode.longPress, bool enableFeedback = true, TooltipTriggeredCallback? onTriggered, AnimationStyle animationStyle = _kDefaultAnimationStyle, TooltipPositionDelegate? positionDelegate, bool ignorePointer = false, required Widget child})
```

Creates a raw tooltip.

The [semanticsTooltip], [tooltipBuilder], and [child] arguments are required.

### semanticsTooltip

```dart
String? semanticsTooltip
```

The text to display in the tooltip's semantics announcement.

This string is used by assistive technologies, most notably screen readers like TalkBack and VoiceOver, to describe the tooltip's purpose.

Providing a non-empty string adds a [Semantics] tooltip string for assistive technologies. If the tooltip should not have a semantic description, this property must be explicitly set to null.

### tooltipBuilder

```dart
TooltipComponentBuilder tooltipBuilder
```

Builds the widget that will be displayed in the tooltip's overlay.

The `animation` parameter is an [Animation] that maps to the tooltip's show and hide animation. Its value goes from 0.0 to 1.0 when the tooltip is shown, and from 1.0 to 0.0 when it is hidden.

This animation can be used to create custom transitions for the tooltip, such as fading or scaling, by wrapping the tooltip's content in a [FadeTransition] or [ScaleTransition] and using the provided `animation`.

The characteristics of the animation, such as its duration and curve, can be customized using the [RawTooltip.animationStyle] property.

{@tool snippet} A common use case is to fade the tooltip's content in and out.

```dart
RawTooltip(
  semanticsTooltip: 'An example tooltip',
  tooltipBuilder: (BuildContext context, Animation<double> animation) {
    return FadeTransition(
      opacity: animation,
      child: Container(
        padding: const EdgeInsets.all(8.0),
        color: Colors.grey,
        child: const Text('I am a tooltip!'),
      ),
    );
  },
  child: const Icon(Icons.info),
)
```

{@end-tool}

### hoverDelay

```dart
Duration hoverDelay
```

{@template flutter.widgets.RawTooltip.hoverDelay} The length of time that a pointer must hover over a tooltip's widget before the tooltip will be shown.

Defaults to 0 milliseconds (the tooltip is shown immediately upon hover). {@endtemplate}

### touchDelay

```dart
Duration touchDelay
```

{@template flutter.widgets.RawTooltip.touchDelay} The length of time that the tooltip will be shown after a long press is released (if triggerMode is [TooltipTriggerMode.longPress]) or a tap is released (if triggerMode is [TooltipTriggerMode.tap]).

This property does not affect mouse pointer devices.

Defaults to 1.5 seconds (the tooltip is shown 1.5 seconds after a tap or long press is released). {@endtemplate}

See also:

- [dismissDelay], which allows configuring the time until a pointer disappears when hovering.

### dismissDelay

```dart
Duration dismissDelay
```

{@template flutter.widgets.RawTooltip.dismissDelay} The length of time that a pointer must have stopped hovering over a tooltip's widget before the tooltip will be hidden.

Defaults to 100 milliseconds. {@endtemplate}

See also:

- [touchDelay], which allows configuring the length of time that a tooltip will be visible after touch events are released.

### enableTapToDismiss

```dart
bool enableTapToDismiss
```

{@template flutter.widgets.RawTooltip.enableTapToDismiss} Whether the tooltip can be dismissed by tap.

The default value is true. {@endtemplate}

### triggerMode

```dart
TooltipTriggerMode triggerMode
```

{@template flutter.widgets.RawTooltip.triggerMode} The [TooltipTriggerMode] that will show the tooltip.

This property does not affect mouse devices. Setting [triggerMode] to [TooltipTriggerMode.manual] will not prevent the tooltip from showing when the mouse cursor hovers over it. {@endtemplate}

### enableFeedback

```dart
bool enableFeedback
```

{@template flutter.widgets.RawTooltip.enableFeedback} Whether the tooltip should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

When null, the default value is true.

See also:

- [Feedback], for providing platform-specific feedback to certain actions. {@endtemplate}

### onTriggered

```dart
TooltipTriggeredCallback? onTriggered
```

{@template flutter.widgets.RawTooltip.onTriggered} Called when the [RawTooltip] is triggered programmatically, on tap, or on long press.

The tooltip is triggered after a tap when [triggerMode] is [TooltipTriggerMode.tap] or after a long press when [triggerMode] is [TooltipTriggerMode.longPress].

Hovering over the tooltip with a mouse pointer does not trigger this callback.

See also:

- [TooltipTriggerMode], which defines the different ways a tooltip can be triggered. {@endtemplate}

### animationStyle

```dart
AnimationStyle animationStyle
```

Used to override the curve and duration of the animation that shows and hides the tooltip.

If [AnimationStyle.duration] is provided, it will be used to override the show tooltip animation duration. If it is null, defaults to 150ms.

If [AnimationStyle.curve] is provided, it will be used to override the show tooltip animation curve. If it is null, defaults to [Curves.fastOutSlowIn].

If [AnimationStyle.reverseDuration] is provided, it will be used to override the hide tooltip animation duration. If it is null, defaults to 75ms.

If [AnimationStyle.reverseCurve] is provided, it will be used to override the hide tooltip animation curve. If it is null, the same curve will be used as for the show tooltip animation.

To disable the tooltip show/hide animation, use [AnimationStyle.noAnimation].

### positionDelegate

```dart
TooltipPositionDelegate? positionDelegate
```

{@template flutter.widgets.RawTooltip.positionDelegate} A custom position delegate function for computing where the tooltip should be positioned.

If provided, this function will be called with a [TooltipPositionContext] containing all the necessary information for positioning the tooltip. The function should return an [Offset] indicating where to place the tooltip in the closest [Overlay].

This allows for custom positioning such as left/right positioning, or any other arbitrary positioning logic.

For example, if the [Overlay] takes up the entire screen, returning [Offset.zero] will position the tooltip at the top-left corner of the screen.

The [TooltipPositionContext] provides information that can be used to position the tooltip relative to the target/child.

For example:

```dart
positionDelegate: (TooltipPositionContext context) {
  // Use the context information to position the tooltip to the right of
  // the target.
  return Offset(
    context.target.dx + context.targetSize.width / 2,
    context.target.dy - context.tooltipSize.height / 2,
  );
}
```

If null, defaults to positioning the tooltip center-aligned and below the target using [positionDependentBox].

See also:

- [TooltipPositionContext], which contains the positioning parameters.
- [TooltipPositionDelegate], the function signature for custom positioning. {@endtemplate}

### ignorePointer

```dart
bool ignorePointer
```

Whether the tooltip should be invisible to hit testing.

Defaults to false.

See also:

- [IgnorePointer], for more information about how pointer events are handled or ignored.

### child

```dart
Widget child
```

The widget below this widget in the tree.

The widget returned in [tooltipBuilder] will be shown when the user hovers over this child widget.

{@macro flutter.widgets.ProxyWidget.child}

### dismissAllToolTips()

```dart
bool dismissAllToolTips()
```

{@template flutter.widgets.RawTooltip.dismissAllToolTips} Dismiss all of the tooltips that are currently shown on the screen, including those with mouse cursors currently hovering over them.

This method returns true if it successfully dismisses at least one tooltip and returns false if there is no tooltip currently displayed. {@endtemplate}

### createState()

```dart
State<RawTooltip> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RawTooltipState

```dart
class RawTooltipState extends State<RawTooltip> with SingleTickerProviderStateMixin {}
```

Contains the state for a [RawTooltip].

This class can be used to programmatically show the [RawTooltip]. See the [ensureTooltipVisible] method.

### ensureTooltipVisible()

```dart
bool ensureTooltipVisible()
```

{@template flutter.widgets.RawTooltipState.ensureTooltipVisible} Shows the tooltip if it is not already visible.

After made visible by this method, the tooltip does not automatically dismiss after [RawTooltip.hoverDelay] until the user dismisses/re-triggers it, or [RawTooltip.dismissAllToolTips] is called.

Returns `false` when the tooltip shouldn't be shown or when the tooltip was already visible. {@endtemplate}

### initState()

```dart
void initState()
```

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```
