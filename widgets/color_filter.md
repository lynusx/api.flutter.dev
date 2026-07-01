@docImport 'basic.dart';

# ColorFiltered

```dart
class ColorFiltered extends SingleChildRenderObjectWidget {}
```

Applies a [ColorFilter] to its child.

This widget applies a function independently to each pixel of [child]'s content, according to the [ColorFilter] specified. Use the [ColorFilter.mode] constructor to apply a [Color] using a [BlendMode]. Use the [BackdropFilter] widget instead, if the [ColorFilter] needs to be applied onto the content beneath [child].

{@youtube 560 315 https://www.youtube.com/watch?v=F7Cll22Dno8}

{@tool dartpad} These two images have two [ColorFilter]s applied with different [BlendMode]s, one with red color and [BlendMode.modulate] another with a grey color and [BlendMode.saturation].

** See code in examples/api/lib/widgets/color_filter/color_filtered.0.dart ** {@end-tool}

See also:

- [BlendMode], describes how to blend a source image with the destination image.
- [ColorFilter], which describes a function that modify a color to a different color.

### ColorFiltered()

```dart
ColorFiltered({required ColorFilter colorFilter, Widget? child, dynamic key})
```

Creates a widget that applies a [ColorFilter] to its child.

### colorFilter

```dart
ColorFilter colorFilter
```

The color filter to apply to the child of this widget.

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
