# SafeArea

```dart
class SafeArea extends StatelessWidget {}
```

A widget that insets its child with sufficient padding to avoid intrusions by the operating system.

{@youtube 560 315 https://www.youtube.com/watch?v=lkF0TQJO0bA}

When a [minimum] padding is specified, the greater of the minimum padding or the safe area padding will be applied.

{@tool dartpad} This example shows how `SafeArea` can apply padding within a mobile device's screen to make the relevant content completely visible.

** See code in examples/api/lib/widgets/safe_area/safe_area.0.dart ** {@end-tool}

{@tool snippet}

This example creates a blue box containing text that is sufficiently padded to avoid intrusions by the operating system.

```dart
SafeArea(
  child: Container(
    constraints: const BoxConstraints.expand(),
    alignment: Alignment.center,
    color: Colors.blue,
    child: const Text('Hello, World!'),
  ),
)
```

{@end-tool}

### [MediaQuery] impact

The padding on the [MediaQuery] for the [child] will be suitably adjusted to zero out any sides that were avoided by this widget.

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

See also:

- [SliverSafeArea], for insetting slivers to avoid operating system intrusions.
- [Padding], for insetting widgets in general.
- [MediaQuery], from which the view padding is obtained.
- [dart:ui.FlutterView.padding], which reports the padding from the operating system.

### SafeArea()

```dart
SafeArea({dynamic key, bool left = true, bool top = true, bool right = true, bool bottom = true, EdgeInsets minimum = EdgeInsets.zero, bool maintainBottomViewPadding = false, required Widget child})
```

Creates a widget that avoids operating system interfaces.

### left

```dart
bool left
```

Whether to avoid system intrusions on the left.

### top

```dart
bool top
```

Whether to avoid system intrusions at the top of the screen, typically the system status bar.

### right

```dart
bool right
```

Whether to avoid system intrusions on the right.

### bottom

```dart
bool bottom
```

Whether to avoid system intrusions on the bottom side of the screen.

### minimum

```dart
EdgeInsets minimum
```

This minimum padding to apply.

The greater of the minimum insets and the media padding will be applied.

### maintainBottomViewPadding

```dart
bool maintainBottomViewPadding
```

Specifies whether the [SafeArea] should maintain the bottom [MediaQueryData.viewPadding] instead of the bottom [MediaQueryData.padding], defaults to false.

For example, if there is an onscreen keyboard displayed above the SafeArea, the padding can be maintained below the obstruction rather than being consumed. This can be helpful in cases where your layout contains flexible widgets, which could visibly move when opening a software keyboard due to the change in the padding value. Setting this to true will avoid the UI shift.

### child

```dart
Widget child
```

The widget below this widget in the tree.

The padding on the [MediaQuery] for the [child] will be suitably adjusted to zero out any sides that were avoided by this widget.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverSafeArea

```dart
class SliverSafeArea extends StatelessWidget {}
```

A sliver that insets another sliver by sufficient padding to avoid intrusions by the operating system.

For example, this will indent the sliver by enough to avoid the status bar at the top of the screen.

It will also indent the sliver by the amount necessary to avoid The Notch on the iPhone X, or other similar creative physical features of the display.

When a [minimum] padding is specified, the greater of the minimum padding or the safe area padding will be applied.

See also:

- [SafeArea], for insetting box widgets to avoid operating system intrusions.
- [SliverPadding], for insetting slivers in general.
- [MediaQuery], from which the window padding is obtained.
- [dart:ui.FlutterView.padding], which reports the padding from the operating system.

### SliverSafeArea()

```dart
SliverSafeArea({dynamic key, bool left = true, bool top = true, bool right = true, bool bottom = true, EdgeInsets minimum = EdgeInsets.zero, required Widget sliver})
```

Creates a sliver that avoids operating system interfaces.

### left

```dart
bool left
```

Whether to avoid system intrusions on the left.

### top

```dart
bool top
```

Whether to avoid system intrusions at the top of the screen, typically the system status bar.

### right

```dart
bool right
```

Whether to avoid system intrusions on the right.

### bottom

```dart
bool bottom
```

Whether to avoid system intrusions on the bottom side of the screen.

### minimum

```dart
EdgeInsets minimum
```

This minimum padding to apply.

The greater of the minimum padding and the media padding is be applied.

### sliver

```dart
Widget sliver
```

The sliver below this sliver in the tree.

The padding on the [MediaQuery] for the [sliver] will be suitably adjusted to zero out any sides that were avoided by this sliver.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
