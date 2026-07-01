@docImport 'color_scheme.dart'; @docImport 'material.dart';

# ElevationOverlay

```dart
abstract final class ElevationOverlay {}
```

A utility class for dealing with the overlay color needed to indicate elevation of surfaces.

### applySurfaceTint()

```dart
Color applySurfaceTint(Color color, Color? surfaceTint, double elevation)
```

Applies a surface tint color to a given container color to indicate the level of its elevation.

With Material Design 3, some components will use a "surface tint" color overlay with an opacity applied to their base color to indicate they are elevated. The amount of opacity will vary with the elevation as described in: https://m3.material.io/styles/color/the-color-system/color-roles.

If [surfaceTint] is not null and not completely transparent ([Color.alpha] is 0), then the returned color will be the given [color] with the [surfaceTint] of the appropriate opacity applied to it. Otherwise it will just return [color] unmodified.

### applyOverlay()

```dart
Color applyOverlay(BuildContext context, Color color, double elevation)
```

Applies an overlay color to a surface color to indicate the level of its elevation in a dark theme.

If using Material Design 3, this type of color overlay is no longer used. Instead a "surface tint" overlay is used instead. See [applySurfaceTint], [ThemeData.useMaterial3] for more information.

Material drop shadows can be difficult to see in a dark theme, so the elevation of a surface should be portrayed with an "overlay" in addition to the shadow. As the elevation of the component increases, the overlay increases in opacity. This function computes and applies this overlay to a given color as needed.

If the ambient theme is dark ([ThemeData.brightness] is [Brightness.dark]), and [ThemeData.applyElevationOverlayColor] is true, and the given [color] is [ColorScheme.surface] then this will return a version of the [color] with a semi-transparent [ColorScheme.onSurface] overlaid on top of it. The opacity of the overlay is computed based on the [elevation].

Otherwise it will just return the [color] unmodified.

See also:

- [ThemeData.applyElevationOverlayColor] which controls the whether an overlay color will be applied to indicate elevation.
- [overlayColor] which computes the needed overlay color.
- [Material] which uses this to apply an elevation overlay to its surface.
- <https://material.io/design/color/dark-theme.html>, which specifies how the overlay should be applied.

### overlayColor()

```dart
Color overlayColor(BuildContext context, double elevation)
```

Computes the appropriate overlay color used to indicate elevation in dark themes.

If using Material Design 3, this type of color overlay is no longer used. Instead a "surface tint" overlay is used instead. See [applySurfaceTint], [ThemeData.useMaterial3] for more information.

See also:

- https://material.io/design/color/dark-theme.html#properties which specifies the exact overlay values for a given elevation.

### colorWithOverlay()

```dart
Color colorWithOverlay(Color surface, Color overlay, double elevation)
```

Returns a color blended by laying a semi-transparent overlay (using the [overlay] color) on top of a surface (using the [surface] color).

If using Material Design 3, this type of color overlay is no longer used. Instead a "surface tint" overlay is used instead. See [applySurfaceTint], [ThemeData.useMaterial3] for more information.

The opacity of the overlay depends on [elevation]. As [elevation] increases, the opacity will also increase.

See https://material.io/design/color/dark-theme.html#properties.
