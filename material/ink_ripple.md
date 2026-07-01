@docImport 'button_style.dart'; @docImport 'ink_highlight.dart'; @docImport 'ink_splash.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart';

# InkRipple

```dart
class InkRipple extends InteractiveInkFeature {}
```

A visual reaction on a piece of [Material] to user input.

A circular ink feature whose origin starts at the input touch point and whose radius expands from 60% of the final radius. The splash origin animates to the center of its [referenceBox].

This object is rarely created directly. Instead of creating an ink ripple, consider using an [InkResponse] or [InkWell] widget, which uses gestures (such as tap and long-press) to trigger ink splashes. This class is used when the [Theme]'s [ThemeData.splashFactory] is [InkRipple.splashFactory].

See also:

- [InkSplash], which is an ink splash feature that expands less aggressively than the ripple.
- [InkResponse], which uses gestures to trigger ink highlights and ink splashes in the parent [Material].
- [InkWell], which is a rectangular [InkResponse] (the most common type of ink response).
- [Material], which is the widget on which the ink splash is painted.
- [InkHighlight], which is an ink feature that emphasizes a part of a [Material].

### InkRipple()

```dart
InkRipple({required MaterialInkController controller, required dynamic referenceBox, required Offset position, required Color color, required TextDirection textDirection, bool containedInkWell = false, RectCallback? rectCallback, BorderRadius? borderRadius, dynamic customBorder, double? radius, dynamic onRemoved})
```

Begin a ripple, centered at [position] relative to [referenceBox].

The [controller] argument is typically obtained via `Material.of(context)`.

If [containedInkWell] is true, then the ripple will be sized to fit the well rectangle, then clipped to it when drawn. The well rectangle is the box returned by [rectCallback], if provided, or otherwise is the bounds of the [referenceBox].

If [containedInkWell] is false, then [rectCallback] should be null. The ink ripple is clipped only to the edges of the [Material]. This is the default.

When the ripple is removed, [onRemoved] will be called.

### splashFactory

```dart
InteractiveInkFeatureFactory splashFactory
```

Used to specify this type of ink splash for an [InkWell], [InkResponse], material [Theme], or [ButtonStyle].

### confirm()

```dart
void confirm()
```

### cancel()

```dart
void cancel()
```

### dispose()

```dart
void dispose()
```

### paintFeature()

```dart
void paintFeature(Canvas canvas, Matrix4 transform)
```
