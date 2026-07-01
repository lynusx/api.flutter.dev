@docImport 'package:flutter/material.dart';

# ImageIcon

```dart
class ImageIcon extends StatelessWidget {}
```

An icon that comes from an [ImageProvider], e.g. an [AssetImage].

See also:

- [IconButton], for interactive icons.
- [IconTheme], which provides ambient configuration for icons.
- [Icon], for icons based on glyphs from fonts instead of images.
- [Icons], the library of Material Icons.

### ImageIcon()

```dart
ImageIcon(ImageProvider? image, {dynamic key, double? size, Color? color, String? semanticLabel, bool useOriginalColors = false})
```

Creates an image icon.

The [size] and [color] default to the value given by the current [IconTheme].

### image

```dart
ImageProvider? image
```

The image to display as the icon.

The icon can be null, in which case the widget will render as an empty space of the specified [size].

### size

```dart
double? size
```

The size of the icon in logical pixels.

Icons occupy a square with width and height equal to size.

Defaults to the current [IconTheme] size, if any. If there is no [IconTheme], or it does not specify an explicit size, then it defaults to 24.0.

### color

```dart
Color? color
```

The color to use when drawing the icon.

Defaults to the current [IconTheme] color, if any. If there is no [IconTheme], then it defaults to not recolorizing the image.

The image will be additionally adjusted by the opacity of the current [IconTheme], if any.

### semanticLabel

```dart
String? semanticLabel
```

Semantic label for the icon.

Announced by assistive technologies (e.g TalkBack/VoiceOver). This label does not show in the UI.

- [SemanticsProperties.label], which is set to [semanticLabel] in the underlying [Semantics] widget.

### useOriginalColors

```dart
bool useOriginalColors
```

Whether to render the image using its original colors.

If this is false (the default), the image is colorized by merging the [color] (or, if that is null, the [IconTheme] color) with the image using [BlendMode.srcIn]. This is the standard behavior for icons.

If this is true, the color-blend filter is disabled, and the image is rendered with its original colors. This allows multi-colored images, such as brand logos, to be displayed accurately.

If this is true, [color] must be null.

Defaults to false.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
