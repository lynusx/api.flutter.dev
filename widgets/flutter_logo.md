@docImport 'icon.dart'; @docImport 'image_icon.dart';

# FlutterLogo

```dart
class FlutterLogo extends StatelessWidget {}
```

The Flutter logo, in widget form. This widget respects the [IconTheme]. For guidelines on using the Flutter logo, visit https://flutter.dev/brand.

{@youtube 560 315 https://www.youtube.com/watch?v=aAmP-WcI6dg}

See also:

- [IconTheme], which provides ambient configuration for icons.
- [Icon], for showing icons the Material design icon library.
- [ImageIcon], for showing icons from [AssetImage]s or other [ImageProvider]s.

### FlutterLogo()

```dart
FlutterLogo({dynamic key, double? size, Color textColor = const Color(0xFF757575), FlutterLogoStyle style = FlutterLogoStyle.markOnly, Duration duration = const Duration(milliseconds: 750), Curve curve = Curves.fastOutSlowIn})
```

Creates a widget that paints the Flutter logo.

The [size] defaults to the value given by the current [IconTheme].

The [textColor], [style], [duration], and [curve] arguments must not be null.

### size

```dart
double? size
```

The size of the logo in logical pixels.

The logo will be fit into a square this size.

Defaults to the current [IconTheme] size, if any. If there is no [IconTheme], or it does not specify an explicit size, then it defaults to 24.0.

### textColor

```dart
Color textColor
```

The color used to paint the "Flutter" text on the logo, if [style] is [FlutterLogoStyle.horizontal] or [FlutterLogoStyle.stacked].

If possible, the default (a medium grey) should be used against a white background.

### style

```dart
FlutterLogoStyle style
```

Whether and where to draw the "Flutter" text. By default, only the logo itself is drawn.

### duration

```dart
Duration duration
```

The length of time for the animation if the [style] or [textColor] properties are changed.

### curve

```dart
Curve curve
```

The curve for the logo animation if the [style] or [textColor] change.

### build()

```dart
Widget build(BuildContext context)
```
