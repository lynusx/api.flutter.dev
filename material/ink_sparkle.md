@docImport 'button_style.dart'; @docImport 'elevated_button.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart';

# InkSparkle

```dart
class InkSparkle extends InteractiveInkFeature {}
```

Begin a Material 3 ink sparkle ripple, centered at the tap or click position relative to the [referenceBox].

To use this effect, pass an instance of [splashFactory] to the `splashFactory` parameter of either the Material [ThemeData] or any component that has a `splashFactory` parameter, such as buttons:

- [ElevatedButton]
- [TextButton]
- [OutlinedButton]

The [controller] argument is typically obtained via `Material.of(context)`.

If `containedInkWell` is true, then the effect will be sized to fit the well rectangle, and clipped to it when drawn. The well rectangle is the box returned by `rectCallback`, if provided, or otherwise is the bounds of the [referenceBox].

If `containedInkWell` is false, then `rectCallback` should be null. The ink ripple is clipped only to the edges of the [Material]. This is the default.

When the ripple is removed, [onRemoved] will be called.

{@tool snippet}

For typical use, pass the [InkSparkle.splashFactory] to the `splashFactory` parameter of a button style or [ThemeData].

```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(splashFactory: InkSparkle.splashFactory),
  child: const Text('Sparkle!'),
  onPressed: () { },
)
```

{@end-tool}

### InkSparkle()

```dart
InkSparkle({required MaterialInkController controller, required dynamic referenceBox, required dynamic color, required Offset position, required TextDirection textDirection, bool containedInkWell = true, RectCallback? rectCallback, BorderRadius? borderRadius, dynamic customBorder, double? radius, dynamic onRemoved, double? turbulenceSeed})
```

Begin a sparkly ripple effect, centered at [position] relative to [referenceBox].

The [color] defines the color of the splash itself. The sparkles are always white.

The [controller] argument is typically obtained via `Material.of(context)`.

[textDirection] is used by [customBorder] if it is non-null. This allows the [customBorder]'s path to be properly defined if it was the path was expressed in terms of "start" and "end" instead of "left" and "right".

If [containedInkWell] is true, then the ripple will be sized to fit the well rectangle, then clipped to it when drawn. The well rectangle is the box returned by [rectCallback], if provided, or otherwise is the bounds of the [referenceBox].

If [containedInkWell] is false, then [rectCallback] should be null. The ink ripple is clipped only to the edges of the [Material]. This is the default.

Clipping can happen in 3 different ways:

1.  If [customBorder] is provided, it is used to determine the path for clipping.
2.  If [customBorder] is null, and [borderRadius] is provided, then the canvas is clipped by an [RRect] created from [borderRadius].
3.  If [borderRadius] is the default [BorderRadius.zero], then the canvas is clipped with [rectCallback]. When the ripple is removed, [onRemoved] will be called.

[turbulenceSeed] can be passed if a non random seed should be used for the turbulence and sparkles. By default, the seed is a random number between 0.0 and 1000.0.

Turbulence is an input to the shader and helps to provides a more natural, non-circular, "splash" effect.

Sparkle randomization is also driven by the [turbulenceSeed]. Sparkles are identified in the shader as "noise", and the sparkles are derived from pseudorandom triangular noise.

### splashFactory

```dart
InteractiveInkFeatureFactory splashFactory
```

Used to specify this type of ink splash for an [InkWell], [InkResponse], material [Theme], or [ButtonStyle].

Since no `turbulenceSeed` is passed, the effect will be random for subsequent presses in the same position.

### constantTurbulenceSeedSplashFactory

```dart
InteractiveInkFeatureFactory constantTurbulenceSeedSplashFactory
```

Used to specify this type of ink splash for an [InkWell], [InkResponse], material [Theme], or [ButtonStyle].

Since a `turbulenceSeed` is passed, the effect will not be random for subsequent presses in the same position. This can be used for testing.

### dispose()

```dart
void dispose()
```

### paintFeature()

```dart
void paintFeature(Canvas canvas, Matrix4 transform)
```
