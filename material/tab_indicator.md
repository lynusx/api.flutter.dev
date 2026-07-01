@docImport 'tabs.dart';

# UnderlineTabIndicator

```dart
class UnderlineTabIndicator extends Decoration {}
```

Used with [TabBar.indicator] to draw a horizontal line below the selected tab.

The selected tab underline is inset from the tab's boundary by [insets]. The [borderSide] defines the line's color and weight.

The [TabBar.indicatorSize] property can be used to define the indicator's bounds in terms of its (centered) widget with [TabBarIndicatorSize.label], or the entire tab with [TabBarIndicatorSize.tab].

### UnderlineTabIndicator()

```dart
UnderlineTabIndicator({BorderRadius? borderRadius, BorderSide borderSide = const BorderSide(width: 2.0, color: Colors.white), EdgeInsetsGeometry insets = EdgeInsets.zero})
```

Create an underline style selected tab indicator.

### borderRadius

```dart
BorderRadius? borderRadius
```

The radius of the indicator's corners.

If this value is non-null, rounded rectangular tab indicator is drawn, otherwise rectangular tab indicator is drawn.

### borderSide

```dart
BorderSide borderSide
```

The color and weight of the horizontal line drawn below the selected tab.

### insets

```dart
EdgeInsetsGeometry insets
```

Locates the selected tab's underline relative to the tab's boundary.

The [TabBar.indicatorSize] property can be used to define the tab indicator's bounds in terms of its (centered) tab widget with [TabBarIndicatorSize.label], or the entire tab with [TabBarIndicatorSize.tab].

### lerpFrom()

```dart
Decoration? lerpFrom(Decoration? a, double t)
```

### lerpTo()

```dart
Decoration? lerpTo(Decoration? b, double t)
```

### createBoxPainter()

```dart
BoxPainter createBoxPainter([VoidCallback? onChanged])
```

### getClipPath()

```dart
Path getClipPath(Rect rect, TextDirection textDirection)
```
