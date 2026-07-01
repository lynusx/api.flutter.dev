# RenderDecoratedSliver

```dart
class RenderDecoratedSliver extends RenderProxySliver {}
```

Paints a [Decoration] either before or after its child paints.

If the child has infinite scroll extent, then the [Decoration] paints itself up to the bottom cache extent.

### RenderDecoratedSliver()

```dart
RenderDecoratedSliver({required Decoration decoration, DecorationPosition position = DecorationPosition.background, ImageConfiguration configuration = ImageConfiguration.empty})
```

Creates a decorated sliver.

The [decoration], [position], and [configuration] arguments must not be null. By default the decoration paints behind the child.

The [ImageConfiguration] will be passed to the decoration (with the size filled in) to let it resolve images.

### decoration

```dart
Decoration get decoration
```

What decoration to paint.

Commonly a [BoxDecoration].

### decoration

```dart
set decoration(Decoration value)
```

### position

```dart
DecorationPosition get position
```

Whether to paint the box decoration behind or in front of the child.

### position

```dart
set position(DecorationPosition value)
```

### configuration

```dart
ImageConfiguration get configuration
```

The settings to pass to the decoration when painting, so that it can resolve images appropriately. See [ImageProvider.resolve] and [BoxPainter.paint].

The [ImageConfiguration.textDirection] field is also used by direction-sensitive [Decoration]s for painting and hit-testing.

### configuration

```dart
set configuration(ImageConfiguration value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### dispose()

```dart
void dispose()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
