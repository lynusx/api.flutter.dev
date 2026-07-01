# TextureBox

```dart
class TextureBox extends RenderBox {}
```

A rectangle upon which a backend texture is mapped.

Backend textures are images that can be applied (mapped) to an area of the Flutter view. They are created, managed, and updated using a platform-specific texture registry. This is typically done by a plugin that integrates with host platform video player, camera, or OpenGL APIs, or similar image sources.

A texture box refers to its backend texture using an integer ID. Texture IDs are obtained from the texture registry and are scoped to the Flutter view. Texture IDs may be reused after deregistration, at the discretion of the registry. The use of texture IDs currently unknown to the registry will silently result in a blank rectangle.

Texture boxes are repainted autonomously as dictated by the backend (e.g. on arrival of a video frame). Such repainting generally does not involve executing Dart code.

The size of the rectangle is determined by the parent, and the texture is automatically scaled to fit.

See also:

- [TextureRegistry](/javadoc/io/flutter/view/TextureRegistry.html) for how to create and manage backend textures on Android.
- [TextureRegistry Protocol](/ios-embedder/protocol_flutter_texture_registry-p.html) for how to create and manage backend textures on iOS.

### TextureBox()

```dart
TextureBox({required int textureId, bool freeze = false, FilterQuality filterQuality = FilterQuality.low})
```

Creates a box backed by the texture identified by [textureId], and use [filterQuality] to set texture's [FilterQuality].

### textureId

```dart
int get textureId
```

The identity of the backend texture.

### textureId

```dart
set textureId(int value)
```

### freeze

```dart
bool get freeze
```

When true the texture will not be updated with new frames.

### freeze

```dart
set freeze(bool value)
```

### filterQuality

```dart
FilterQuality get filterQuality
```

{@macro flutter.widgets.Texture.filterQuality}

### filterQuality

```dart
set filterQuality(FilterQuality value)
```

### sizedByParent

```dart
bool get sizedByParent
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```
