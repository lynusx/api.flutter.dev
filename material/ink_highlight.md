@docImport 'ink_decoration.dart'; @docImport 'ink_splash.dart'; @docImport 'ink_well.dart';

# InkHighlight

```dart
class InkHighlight extends InteractiveInkFeature {}
```

A visual emphasis on a part of a [Material] receiving user interaction.

This object is rarely created directly. Instead of creating an ink highlight directly, consider using an [InkResponse] or [InkWell] widget, which uses gestures (such as tap and long-press) to trigger ink highlights.

See also:

- [InkResponse], which uses gestures to trigger ink highlights and ink splashes in the parent [Material].
- [InkWell], which is a rectangular [InkResponse] (the most common type of ink response).
- [Material], which is the widget on which the ink highlight is painted.
- [InkSplash], which is an ink feature that shows a reaction to user input on a [Material].
- [Ink], a convenience widget for drawing images and other decorations on Material widgets.

### InkHighlight()

```dart
InkHighlight({required MaterialInkController controller, required dynamic referenceBox, required dynamic color, required TextDirection textDirection, BoxShape shape = BoxShape.rectangle, double? radius, BorderRadius? borderRadius, dynamic customBorder, RectCallback? rectCallback, dynamic onRemoved, Duration fadeDuration = _kDefaultHighlightFadeDuration})
```

Begin a highlight animation.

The [controller] argument is typically obtained via `Material.of(context)`.

If a `rectCallback` is given, then it provides the highlight rectangle, otherwise, the highlight rectangle is coincident with the [referenceBox].

When the highlight is removed, `onRemoved` will be called.

### active

```dart
bool get active
```

Whether this part of the material is being visually emphasized.

### activate()

```dart
void activate()
```

Start visually emphasizing this part of the material.

### deactivate()

```dart
void deactivate()
```

Stop visually emphasizing this part of the material.

### dispose()

```dart
void dispose()
```

### paintFeature()

```dart
void paintFeature(Canvas canvas, Matrix4 transform)
```
