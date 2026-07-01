@docImport 'basic.dart'; @docImport 'color_filter.dart';

# ImageFiltered

```dart
class ImageFiltered extends SingleChildRenderObjectWidget {}
```

Applies an [ImageFilter] to its child.

An image filter will always apply its filter operation to the child widget, even if said filter is conceptually a "no-op", such as an ImageFilter.blur with a radius of 0 or an ImageFilter.matrix with an identity matrix. Setting [ImageFiltered.enabled] to `false` is a more efficient manner of disabling an image filter.

The framework does not attempt to optimize out "no-op" filters because it cannot tell the difference between an intentional no-op and a filter that is only incidentally a no-op. Consider an ImageFilter.matrix that is animated and happens to pass through the identity matrix. If the framework identified it as a no-op it would drop and then recreate the layer during the animation which would be more expensive than keeping it around.

{@youtube 560 315 https://www.youtube.com/watch?v=7Lftorq4i2o}

See also:

- [BackdropFilter], which applies an [ImageFilter] to everything beneath its child.
- [ColorFiltered], which applies a [ColorFilter] to its child.

### ImageFiltered()

```dart
ImageFiltered({dynamic key, required ImageFilter imageFilter, Widget? child, bool enabled = true})
```

Creates a widget that applies an [ImageFilter] to its child.

### imageFilter

```dart
ImageFilter imageFilter
```

The image filter to apply to the child of this widget.

### enabled

```dart
bool enabled
```

Whether or not to apply the image filter operation to the child of this widget.

Prefer setting enabled to `false` instead of creating a "no-op" filter type for performance reasons.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderObject renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
