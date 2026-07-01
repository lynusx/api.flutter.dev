@docImport 'package:flutter/material.dart';

# HSVColor

```dart
class HSVColor {}
```

A color represented using [alpha], [hue], [saturation], and [value].

An [HSVColor] is represented in a parameter space that's based on human perception of color in pigments (e.g. paint and printer's ink). The representation is useful for some color computations (e.g. rotating the hue through the colors), because interpolation and picking of colors as red, green, and blue channels doesn't always produce intuitive results.

The HSV color space models the way that different pigments are perceived when mixed. The hue describes which pigment is used, the saturation describes which shade of the pigment, and the value resembles mixing the pigment with different amounts of black or white pigment.

See also:

- [HSLColor], a color that uses a color space based on human perception of colored light.
- [HSV and HSL](https://en.wikipedia.org/wiki/HSL_and_HSV) Wikipedia article, which this implementation is based upon.

### HSVColor.fromAHSV()

```dart
HSVColor.fromAHSV(double alpha, double hue, double saturation, double value)
```

Creates a color.

All the arguments must be in their respective ranges. See the fields for each parameter for a description of their ranges.

### HSVColor.fromColor()

```dart
HSVColor.fromColor(Color color)
```

Creates an [HSVColor] from an RGB [Color].

This constructor does not necessarily round-trip with [toColor] because of floating point imprecision.

### alpha

```dart
double alpha
```

Alpha, from 0.0 to 1.0. The describes the transparency of the color. A value of 0.0 is fully transparent, and 1.0 is fully opaque.

### hue

```dart
double hue
```

Hue, from 0.0 to 360.0. Describes which color of the spectrum is represented. A value of 0.0 represents red, as does 360.0. Values in between go through all the hues representable in RGB. You can think of this as selecting which pigment will be added to a color.

### saturation

```dart
double saturation
```

Saturation, from 0.0 to 1.0. This describes how colorful the color is. 0.0 implies a shade of grey (i.e. no pigment), and 1.0 implies a color as vibrant as that hue gets. You can think of this as the equivalent of how much of a pigment is added.

### value

```dart
double value
```

Value, from 0.0 to 1.0. The "value" of a color that, in this context, describes how bright a color is. A value of 0.0 indicates black, and 1.0 indicates full intensity color. You can think of this as the equivalent of removing black from the color as value increases.

### withAlpha()

```dart
HSVColor withAlpha(double alpha)
```

Returns a copy of this color with the [alpha] parameter replaced with the given value.

### withHue()

```dart
HSVColor withHue(double hue)
```

Returns a copy of this color with the [hue] parameter replaced with the given value.

### withSaturation()

```dart
HSVColor withSaturation(double saturation)
```

Returns a copy of this color with the [saturation] parameter replaced with the given value.

### withValue()

```dart
HSVColor withValue(double value)
```

Returns a copy of this color with the [value] parameter replaced with the given value.

### toColor()

```dart
Color toColor()
```

Returns this color in RGB.

### lerp()

```dart
HSVColor? lerp(HSVColor? a, HSVColor? b, double t)
```

Linearly interpolate between two HSVColors.

The colors are interpolated by interpolating the [alpha], [hue], [saturation], and [value] channels separately, which usually leads to a more pleasing effect than [Color.lerp] (which interpolates the red, green, and blue channels separately).

If either color is null, this function linearly interpolates from a transparent instance of the other color. This is usually preferable to interpolating from [Colors.transparent] (`const Color(0x00000000)`) since that will interpolate from a transparent red and cycle through the hues to match the target color, regardless of what that color's hue is.

{@macro dart.ui.shadow.lerp}

Values outside of the valid range for each channel will be clamped.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# HSLColor

```dart
class HSLColor {}
```

A color represented using [alpha], [hue], [saturation], and [lightness].

An [HSLColor] is represented in a parameter space that's based up human perception of colored light. The representation is useful for some color computations (e.g., combining colors of light), because interpolation and picking of colors as red, green, and blue channels doesn't always produce intuitive results.

HSL is a perceptual color model, placing fully saturated colors around a circle (conceptually) at a lightness of ​0.5, with a lightness of 0.0 being completely black, and a lightness of 1.0 being completely white. As the lightness increases or decreases from 0.5, the apparent saturation decreases proportionally (even though the [saturation] parameter hasn't changed).

See also:

- [HSVColor], a color that uses a color space based on human perception of pigments (e.g. paint and printer's ink).
- [HSV and HSL](https://en.wikipedia.org/wiki/HSL_and_HSV) Wikipedia article, which this implementation is based upon.

### HSLColor.fromAHSL()

```dart
HSLColor.fromAHSL(double alpha, double hue, double saturation, double lightness)
```

Creates a color.

All the arguments must be in their respective ranges. See the fields for each parameter for a description of their ranges.

### HSLColor.fromColor()

```dart
HSLColor.fromColor(Color color)
```

Creates an [HSLColor] from an RGB [Color].

This constructor does not necessarily round-trip with [toColor] because of floating point imprecision.

### alpha

```dart
double alpha
```

Alpha, from 0.0 to 1.0. The describes the transparency of the color. A value of 0.0 is fully transparent, and 1.0 is fully opaque.

### hue

```dart
double hue
```

Hue, from 0.0 to 360.0. Describes which color of the spectrum is represented. A value of 0.0 represents red, as does 360.0. Values in between go through all the hues representable in RGB. You can think of this as selecting which color filter is placed over a light.

### saturation

```dart
double saturation
```

Saturation, from 0.0 to 1.0. This describes how colorful the color is. 0.0 implies a shade of grey (i.e. no pigment), and 1.0 implies a color as vibrant as that hue gets. You can think of this as the purity of the color filter over the light.

### lightness

```dart
double lightness
```

Lightness, from 0.0 to 1.0. The lightness of a color describes how bright a color is. A value of 0.0 indicates black, and 1.0 indicates white. You can think of this as the intensity of the light behind the filter. As the lightness approaches 0.5, the colors get brighter and appear more saturated, and over 0.5, the colors start to become less saturated and approach white at 1.0.

### withAlpha()

```dart
HSLColor withAlpha(double alpha)
```

Returns a copy of this color with the alpha parameter replaced with the given value.

### withHue()

```dart
HSLColor withHue(double hue)
```

Returns a copy of this color with the [hue] parameter replaced with the given value.

### withSaturation()

```dart
HSLColor withSaturation(double saturation)
```

Returns a copy of this color with the [saturation] parameter replaced with the given value.

### withLightness()

```dart
HSLColor withLightness(double lightness)
```

Returns a copy of this color with the [lightness] parameter replaced with the given value.

### toColor()

```dart
Color toColor()
```

Returns this HSL color in RGB.

### lerp()

```dart
HSLColor? lerp(HSLColor? a, HSLColor? b, double t)
```

Linearly interpolate between two HSLColors.

The colors are interpolated by interpolating the [alpha], [hue], [saturation], and [lightness] channels separately, which usually leads to a more pleasing effect than [Color.lerp] (which interpolates the red, green, and blue channels separately).

If either color is null, this function linearly interpolates from a transparent instance of the other color. This is usually preferable to interpolating from [Colors.transparent] (`const Color(0x00000000)`) since that will interpolate from a transparent red and cycle through the hues to match the target color, regardless of what that color's hue is.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values between them meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values outside of the valid range for each channel will be clamped.

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# ColorSwatch

```dart
class ColorSwatch<T> extends Color {}
```

A color that has a small table of related colors called a "swatch".

The table is accessed by key values of type `T`.

See also:

- [MaterialColor] and [MaterialAccentColor], which define Material Design primary and accent color swatches.
- [Colors], which defines all of the standard Material Design colors.

### ColorSwatch()

```dart
ColorSwatch(dynamic primary, Map<T, Color> _swatch)
```

Creates a color that has a small table of related colors called a "swatch".

The `primary` argument should be the 32 bit ARGB value of one of the values in the swatch, as would be passed to the [Color.new] constructor for that same color, and as is exposed by [value]. (This is distinct from the key of any color in the swatch.)

### operator []()

```dart
Color? operator [](T key)
```

Returns an element of the swatch table.

### keys

```dart
Iterable<T> get keys
```

Returns the valid keys for accessing operator[].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

### lerp()

```dart
ColorSwatch<T>? lerp<T>(ColorSwatch<T>? a, ColorSwatch<T>? b, double t)
```

Linearly interpolate between two [ColorSwatch]es.

It delegates to [Color.lerp] to interpolate the different colors of the swatch.

If either color is null, this function linearly interpolates from a transparent instance of the other color.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]). Each channel will be clamped to the range 0 to 255.

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

# ColorProperty

```dart
class ColorProperty extends DiagnosticsProperty<Color> {}
```

[DiagnosticsProperty] that has an [Color] as value.

### ColorProperty()

```dart
ColorProperty(String name, dynamic value, {dynamic showName, dynamic defaultValue, dynamic style, dynamic level})
```

Create a diagnostics property for [Color].

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```
