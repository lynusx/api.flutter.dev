@docImport 'box_decoration.dart';

# FlutterLogoStyle

```dart
enum FlutterLogoStyle {}
```

Possible ways to draw Flutter's logo.

Show only Flutter's logo, not the "Flutter" label.

This is the default behavior for [FlutterLogoDecoration] objects.

Show Flutter's logo on the left, and the "Flutter" label to its right.

Show Flutter's logo above the "Flutter" label.

# FlutterLogoDecoration

```dart
class FlutterLogoDecoration extends Decoration {}
```

An immutable description of how to paint Flutter's logo.

### FlutterLogoDecoration()

```dart
FlutterLogoDecoration({Color textColor = const Color(0xFF757575), FlutterLogoStyle style = FlutterLogoStyle.markOnly, EdgeInsets margin = EdgeInsets.zero})
```

Creates a decoration that knows how to paint Flutter's logo.

The [style] controls whether and where to draw the "Flutter" label. If one is shown, the [textColor] controls the color of the label.

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

### margin

```dart
EdgeInsets margin
```

How far to inset the logo from the edge of the container.

### debugAssertIsValid()

```dart
bool debugAssertIsValid()
```

### isComplex

```dart
bool get isComplex
```

### lerp()

```dart
FlutterLogoDecoration? lerp(FlutterLogoDecoration? a, FlutterLogoDecoration? b, double t)
```

Linearly interpolate between two Flutter logo descriptions.

Interpolates both the color and the style in a continuous fashion.

If both values are null, this returns null. Otherwise, it returns a non-null value. If one of the values is null, then the result is obtained by scaling the other value's opacity and [margin].

{@macro dart.ui.shadow.lerp}

See also:

- [Decoration.lerp], which interpolates between arbitrary decorations.

### lerpFrom()

```dart
FlutterLogoDecoration? lerpFrom(Decoration? a, double t)
```

### lerpTo()

```dart
FlutterLogoDecoration? lerpTo(Decoration? b, double t)
```

### hitTest()

```dart
bool hitTest(Size size, Offset position, {TextDirection? textDirection})
```

### createBoxPainter()

```dart
BoxPainter createBoxPainter([VoidCallback? onChanged])
```

### getClipPath()

```dart
Path getClipPath(Rect rect, TextDirection textDirection)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
