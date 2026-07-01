# Texture

```dart
class Texture extends LeafRenderObjectWidget {}
```

A rectangle upon which a backend texture is mapped.

Backend textures are images that can be applied (mapped) to an area of the Flutter view. They are created, managed, and updated using a platform-specific texture registry. This is typically done by a plugin that integrates with host platform video player, camera, or OpenGL APIs, or similar image sources.

A texture widget refers to its backend texture using an integer ID. Texture IDs are obtained from the texture registry and are scoped to the Flutter view. Texture IDs may be reused after deregistration, at the discretion of the registry. The use of texture IDs currently unknown to the registry will silently result in a blank rectangle.

Texture widgets are repainted autonomously as dictated by the backend (e.g. on arrival of a video frame). Such repainting generally does not involve executing Dart code.

The size of the rectangle is determined by its parent widget, and the texture is automatically scaled to fit.

See also:

- [TextureRegistry](/javadoc/io/flutter/view/TextureRegistry.html) for how to create and manage backend textures on Android.
- [TextureRegistry Protocol](/ios-embedder/protocol_flutter_texture_registry-p.html) for how to create and manage backend textures on iOS.

### Texture()

```dart
Texture({dynamic key, required int textureId, bool freeze = false, FilterQuality filterQuality = FilterQuality.low})
```

Creates a widget backed by the texture identified by [textureId], and use [filterQuality] to set texture's [FilterQuality].

### textureId

```dart
int textureId
```

The identity of the backend texture.

### freeze

```dart
bool freeze
```

When true the texture will not be updated with new frames.

### filterQuality

```dart
FilterQuality filterQuality
```

{@template flutter.widgets.Texture.filterQuality} The quality of sampling the texture and rendering it on screen.

When the texture is scaled, a default [FilterQuality.low] is used for a higher quality but slower interpolation (typically bilinear). It can be changed to [FilterQuality.none] for a lower quality but faster interpolation (typically nearest-neighbor). See also [FilterQuality.medium] and [FilterQuality.high] for more options. {@endtemplate}

### createRenderObject()

```dart
TextureBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, TextureBox renderObject)
```
