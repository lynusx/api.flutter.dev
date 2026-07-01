@docImport 'routes.dart';

# ModalBarrier

```dart
class ModalBarrier extends StatelessWidget {}
```

A widget that prevents the user from interacting with widgets behind itself.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

For example, when a dialog is on the screen, the page below the dialog is usually darkened by the modal barrier.

See also:

- [ModalRoute], which indirectly uses this widget.
- [AnimatedModalBarrier], which is similar but takes an animated [color] instead of a single color value.

### ModalBarrier()

```dart
ModalBarrier({dynamic key, Color? color, bool dismissible = true, VoidCallback? onDismiss, String? semanticsLabel, bool? barrierSemanticsDismissible = true, ValueNotifier<EdgeInsets>? clipDetailsNotifier, String? semanticsOnTapHint})
```

Creates a widget that blocks user interaction.

### color

```dart
Color? color
```

If non-null, fill the barrier with this color.

See also:

- [ModalRoute.barrierColor], which controls this property for the [ModalBarrier] built by [ModalRoute] pages.

### dismissible

```dart
bool dismissible
```

Specifies if the barrier will be dismissed when the user taps on it.

If true, and [onDismiss] is non-null, [onDismiss] will be called, otherwise the current route will be popped from the ambient [Navigator].

If false, tapping on the barrier will do nothing.

See also:

- [ModalRoute.barrierDismissible], which controls this property for the [ModalBarrier] built by [ModalRoute] pages.

### onDismiss

```dart
VoidCallback? onDismiss
```

{@template flutter.widgets.ModalBarrier.onDismiss} Called when the barrier is being dismissed.

If non-null [onDismiss] will be called in place of popping the current route. It is up to the callback to handle dismissing the barrier.

If null, the ambient [Navigator]'s current route will be popped.

This field is ignored if [dismissible] is false. {@endtemplate}

### barrierSemanticsDismissible

```dart
bool? barrierSemanticsDismissible
```

Whether the modal barrier semantics are included in the semantics tree.

See also:

- [ModalRoute.semanticsDismissible], which controls this property for the [ModalBarrier] built by [ModalRoute] pages.

### semanticsLabel

```dart
String? semanticsLabel
```

Semantics label used for the barrier if it is [dismissible].

The semantics label is read out by accessibility tools (e.g. TalkBack on Android and VoiceOver on iOS) when the barrier is focused.

See also:

- [ModalRoute.barrierLabel], which controls this property for the [ModalBarrier] built by [ModalRoute] pages.

### clipDetailsNotifier

```dart
ValueNotifier<EdgeInsets>? clipDetailsNotifier
```

{@template flutter.widgets.ModalBarrier.clipDetailsNotifier} Contains a value of type [EdgeInsets] that specifies how the [SemanticsNode.rect] of the widget should be clipped.

See also:

- [_SemanticsClipper], which utilizes the value inside to update the [SemanticsNode.rect] for its child. {@endtemplate}

### semanticsOnTapHint

```dart
String? semanticsOnTapHint
```

{@macro flutter.material.ModalBottomSheetRoute.barrierOnTapHint}

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedModalBarrier

```dart
class AnimatedModalBarrier extends AnimatedWidget {}
```

A widget that prevents the user from interacting with widgets behind itself, and can be configured with an animated color value.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

For example, when a dialog is on the screen, the page below the dialog is usually darkened by the modal barrier.

This widget is similar to [ModalBarrier] except that it takes an animated [color] instead of a single color.

See also:

- [ModalRoute], which uses this widget.

### AnimatedModalBarrier()

```dart
AnimatedModalBarrier({dynamic key, required Animation<Color?> color, bool dismissible = true, String? semanticsLabel, bool? barrierSemanticsDismissible, VoidCallback? onDismiss, ValueNotifier<EdgeInsets>? clipDetailsNotifier, String? semanticsOnTapHint})
```

Creates a widget that blocks user interaction.

### color

```dart
Animation<Color?> get color
```

If non-null, fill the barrier with this color.

See also:

- [ModalRoute.barrierColor], which controls this property for the [AnimatedModalBarrier] built by [ModalRoute] pages.

### dismissible

```dart
bool dismissible
```

Whether touching the barrier will pop the current route off the [Navigator].

See also:

- [ModalRoute.barrierDismissible], which controls this property for the [AnimatedModalBarrier] built by [ModalRoute] pages.

### semanticsLabel

```dart
String? semanticsLabel
```

Semantics label used for the barrier if it is [dismissible].

The semantics label is read out by accessibility tools (e.g. TalkBack on Android and VoiceOver on iOS) when the barrier is focused. See also:

- [ModalRoute.barrierLabel], which controls this property for the [ModalBarrier] built by [ModalRoute] pages.

### barrierSemanticsDismissible

```dart
bool? barrierSemanticsDismissible
```

Whether the modal barrier semantics are included in the semantics tree.

See also:

- [ModalRoute.semanticsDismissible], which controls this property for the [ModalBarrier] built by [ModalRoute] pages.

### onDismiss

```dart
VoidCallback? onDismiss
```

{@macro flutter.widgets.ModalBarrier.onDismiss}

### clipDetailsNotifier

```dart
ValueNotifier<EdgeInsets>? clipDetailsNotifier
```

{@macro flutter.widgets.ModalBarrier.clipDetailsNotifier}

### semanticsOnTapHint

```dart
String? semanticsOnTapHint
```

This hint text instructs users what they are able to do when they tap on the [ModalBarrier]

E.g. If the hint text is 'close bottom sheet", it will be announced as "Double tap to close bottom sheet".

If this value is null, the default onTapHint will be applied, resulting in the announcement of 'Double tap to activate'.

### build()

```dart
Widget build(BuildContext context)
```
