@docImport 'tooltip.dart';

# TooltipVisibility

```dart
class TooltipVisibility extends StatelessWidget {}
```

Overrides the visibility of descendant [Tooltip] widgets.

If disabled, the descendant [Tooltip] widgets will not display a tooltip when tapped, long-pressed, hovered by the mouse, or when `ensureTooltipVisible` is called. This only visually disables tooltips but continues to provide any semantic information that is provided.

### TooltipVisibility()

```dart
TooltipVisibility({dynamic key, required bool visible, required Widget child})
```

Creates a widget that configures the visibility of [Tooltip].

### child

```dart
Widget child
```

The widget below this widget in the tree.

The entire app can be wrapped in this widget to globally control [Tooltip] visibility.

{@macro flutter.widgets.ProxyWidget.child}

### visible

```dart
bool visible
```

Determines the visibility of [Tooltip] widgets that inherit from this widget.

### of()

```dart
bool of(BuildContext context)
```

The [visible] of the closest instance of this class that encloses the given context. Defaults to `true` if none are found.

### build()

```dart
Widget build(BuildContext context)
```
