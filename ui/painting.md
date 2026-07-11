# Color

```dart
class Color {}
```

An immutable color value in ARGB format.

Consider the light teal of the [Flutter logo](https://flutter.dev/brand). It is fully opaque, with a red [r] channel value of `0.2588` (or `0x42` or `66` as an 8-bit value), a green [g] channel value of `0.6471` (or `0xA5` or `165` as an 8-bit value), and a blue [b] channel value of `0.9608` (or `0xF5` or `245` as an 8-bit value). In a common [CSS hex color syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/hex-color) for RGB color values, it would be described as `#42A5F5`.

Here are some ways it could be constructed:

```dart
const Color c1 = Color.from(alpha: 1.0, red: 0.2588, green: 0.6471, blue: 0.9608);
const Color c2 = Color(0xFF42A5F5);
const Color c3 = Color.fromARGB(0xFF, 0x42, 0xA5, 0xF5);
const Color c4 = Color.fromARGB(255, 66, 165, 245);
const Color c5 = Color.fromRGBO(66, 165, 245, 1.0);
```

If you are having a problem with [Color.new] wherein it seems your color is just not painting, check to make sure you are specifying the full 8 hexadecimal digits. If you only specify six, then the leading two digits are assumed to be zero, which means fully-transparent:

```dart
const Color c1 = Color(0xFFFFFF); // fully transparent white (invisible)
const Color c2 = Color(0xFFFFFFFF); // fully opaque white (visible)

// Or use double-based channel values:
const Color c3 = Color.from(alpha: 1.0, red: 1.0, green: 1.0, blue: 1.0);
```

[Color]'s color components are stored as floating-point values. Care should be taken if one does not want the literal equality provided by `operator==`. To test equality inside of Flutter tests consider using [`isSameColorAs`][].

See also:

- [Colors](https://api.flutter.dev/flutter/material/Colors-class.html), which defines the colors found in the Material Design specification.
- [`isSameColorAs`][], a Matcher to handle floating-point deltas when checking [Color] equality.

[`isSameColorAs`]: https://api.flutter.dev/flutter/flutter_test/isSameColorAs.html

### Color()

```dart
Color(int value)
```

Construct an [ColorSpace.sRGB] color from the lower 32 bits of an [int].

The bits are interpreted as follows:

- Bits 24-31 are the alpha value.
- Bits 16-23 are the red value.
- Bits 8-15 are the green value.
- Bits 0-7 are the blue value.

In other words, if AA is the alpha value in hex, RR the red value in hex, GG the green value in hex, and BB the blue value in hex, a color can be expressed as `Color(0xAARRGGBB)`.

For example, to get a fully opaque orange, you would use `const Color(0xFFFF9000)` (`FF` for the alpha, `FF` for the red, `90` for the green, and `00` for the blue).

{@template dart.ui.Color.componentsStoredAsFloatingPoint}

> [!NOTE]
> Each color is stored as floating-point color components, where the final
> value of each component is approximated by storing `c / 255`, where `c`
> is one of the four components (alpha, red, green, blue). {@endtemplate}

### Color.from()

```dart
Color.from({required double alpha, required double red, required double green, required double blue, ColorSpace colorSpace = ColorSpace.sRGB})
```

Construct a color with floating-point color components.

Color components allows arbitrary bit depths for color components to be be supported. The values are interpreted relative to the [ColorSpace] argument.

## Example

```dart
// Fully opaque maximum red color
const Color c1 = Color.from(alpha: 1.0, red: 1.0, green: 0.0, blue: 0.0);

// Partially transparent moderately blue and green color
const Color c2 = Color.from(alpha: 0.5, red: 0.0, green: 0.5, blue: 0.5);

// Fully transparent color
const Color c3 = Color.from(alpha: 0.0, red: 0.0, green: 0.0, blue: 0.0);
```

### Color.fromARGB()

```dart
Color.fromARGB(int a, int r, int g, int b)
```

Construct an sRGB color from the lower 8 bits of four integers.

- `a` is the alpha value, with 0 being transparent and 255 being fully opaque.
- `r` is [red], from 0 to 255.
- `g` is [green], from 0 to 255.
- `b` is [blue], from 0 to 255.

Out of range values are brought into range using modulo 255.

See also [fromRGBO], which takes the alpha value as a floating point value.

{@macro dart.ui.Color.componentsStoredAsFloatingPoint}

### Color.fromRGBO()

```dart
Color.fromRGBO(int r, int g, int b, double opacity)
```

Create an sRGB color from red, green, blue, and opacity, similar to `rgba()` in CSS.

- `r` is [red], from 0 to 255.
- `g` is [green], from 0 to 255.
- `b` is [blue], from 0 to 255.
- `opacity` is alpha channel of this color as a double, with 0.0 being transparent and 1.0 being fully opaque.

Out of range values are brought into range using modulo 255.

See also [fromARGB], which takes the opacity as an integer value.

{@macro dart.ui.Color.componentsStoredAsFloatingPoint}

### a

```dart
double a
```

The alpha channel of this color.

### r

```dart
double r
```

The red channel of this color.

### g

```dart
double g
```

The green channel of this color.

### b

```dart
double b
```

The blue channel of this color.

### colorSpace

```dart
ColorSpace colorSpace
```

The color space of this color.

### value

```dart
int get value
```

A 32 bit value representing this color.

This getter is a _stub_. It is recommended instead to use the explicit [toARGB32] method.

### toARGB32()

```dart
int toARGB32()
```

Returns a 32-bit value representing this color.

The returned value is compatible with the default constructor ([Color.new]) but does _not_ guarantee to result in the same color due to [imprecisions in numeric conversions](https://en.wikipedia.org/wiki/Floating-point_error_mitigation).

Unlike accessing the floating point equivalent channels individually ([a], [r], [g], [b]), this method is intentionally _lossy_, and scales each channel using `(channel * 255.0).round().clamp(0, 255)`.

While useful for storing a 32-bit integer value, prefer accessing the individual channels (and storing the double equivalent) where higher precision is required.

The bits are assigned as follows:

- Bits 24-31 represents the [a] channel as an 8-bit unsigned integer.
- Bits 16-23 represents the [r] channel as an 8-bit unsigned integer.
- Bits 8-15 represents the [g] channel as an 8-bit unsigned integer.
- Bits 0-7 represents the [b] channel as an 8-bit unsigned integer.

> [!WARNING]
> The value returned by this getter implicitly converts floating-point
> component values (such as `0.5`) into their 8-bit equivalent by using
> the [toARGB32] method; the returned value is not guaranteed to be stable
> across different platforms or executions due to the complexity of
> floating-point math.

### alpha

```dart
int get alpha
```

The alpha channel of this color in an 8 bit value.

A value of 0 means this color is fully transparent. A value of 255 means this color is fully opaque.

### opacity

```dart
double get opacity
```

The alpha channel of this color as a double.

A value of 0.0 means this color is fully transparent. A value of 1.0 means this color is fully opaque.

### red

```dart
int get red
```

The red channel of this color in an 8 bit value.

### green

```dart
int get green
```

The green channel of this color in an 8 bit value.

### blue

```dart
int get blue
```

The blue channel of this color in an 8 bit value.

### withValues()

```dart
Color withValues({double? alpha, double? red, double? green, double? blue, ColorSpace? colorSpace})
```

Returns a new color with the provided components updated.

Each component ([alpha], [red], [green], [blue]) represents a floating-point value; see [Color.from] for details and examples.

If [colorSpace] is provided, and is different than the current color space, the component values are updated before transforming them to the provided [ColorSpace].

Example:

```dart
import 'dart:ui';
/// Create a color with 50% opacity.
Color makeTransparent(Color color) => color.withValues(alpha: 0.5);
```

### withAlpha()

```dart
Color withAlpha(int a)
```

Returns a new color that matches this color with the alpha channel replaced with `a` (which ranges from 0 to 255).

Out of range values will have unexpected effects.

### withOpacity()

```dart
Color withOpacity(double opacity)
```

Returns a new color that matches this color with the alpha channel replaced with the given `opacity` (which ranges from 0.0 to 1.0).

Out of range values will have unexpected effects.

### withRed()

```dart
Color withRed(int r)
```

Returns a new color that matches this color with the red channel replaced with `r` (which ranges from 0 to 255).

Out of range values will have unexpected effects.

### withGreen()

```dart
Color withGreen(int g)
```

Returns a new color that matches this color with the green channel replaced with `g` (which ranges from 0 to 255).

Out of range values will have unexpected effects.

### withBlue()

```dart
Color withBlue(int b)
```

Returns a new color that matches this color with the blue channel replaced with `b` (which ranges from 0 to 255).

Out of range values will have unexpected effects.

### computeLuminance()

```dart
double computeLuminance()
```

Returns a brightness value between 0 for darkest and 1 for lightest.

Represents the relative luminance of the color. This value is computationally expensive to calculate.

See <https://en.wikipedia.org/wiki/Relative_luminance>.

### lerp()

```dart
Color? lerp(Color? x, Color? y, double t)
```

Linearly interpolate between two colors.

This is intended to be fast but as a result may be ugly. Consider [HSVColor] or writing custom logic for interpolating colors.

If either color is null, this function linearly interpolates from a transparent instance of the other color. This is usually preferable to interpolating from [material.Colors.transparent] (`const Color(0x00000000)`), which is specifically transparent _black_.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]). Each channel will be clamped to the range 0 to 255.

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

If the two colors are in different color spaces, both are converted to the wider gamut color space before interpolating. The result will be in the wider gamut color space. For example, interpolating between an sRGB color and a Display P3 color will produce a Display P3 result.

### alphaBlend()

```dart
Color alphaBlend(Color foreground, Color background)
```

Combine the foreground color as a transparent color over top of a background color, and return the resulting combined color.

This uses standard alpha blending ("SRC over DST") rules to produce a blended color from two colors. This can be used as a performance enhancement when trying to avoid needless alpha blending compositing operations for two things that are solid colors with the same shape, but overlay each other: instead, just paint one with the combined color.

### getAlphaFromOpacity()

```dart
int getAlphaFromOpacity(double opacity)
```

Returns an alpha value representative of the provided [opacity] value.

The [opacity] value may not be null.

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

# BlendMode

```dart
enum BlendMode {}
```

Algorithms to use when painting on the canvas.

When drawing a shape or image onto a canvas, different algorithms can be used to blend the pixels. The different values of [BlendMode] specify different such algorithms.

Each algorithm has two inputs, the _source_, which is the image being drawn, and the _destination_, which is the image into which the source image is being composited. The destination is often thought of as the _background_. The source and destination both have four color channels, the red, green, blue, and alpha channels. These are typically represented as numbers in the range 0.0 to 1.0. The output of the algorithm also has these same four channels, with values computed from the source and destination.

The documentation of each value below describes how the algorithm works. In each case, an image shows the output of blending a source image with a destination image. In the images below, the destination is represented by an image with horizontal lines and an opaque landscape photograph, and the source is represented by an image with vertical lines (the same lines but rotated) and a bird clip-art image. The [src] mode shows only the source image, and the [dst] mode shows only the destination image. In the documentation below, the transparency is illustrated by a checkerboard pattern. The [clear] mode drops both the source and destination, resulting in an output that is entirely transparent (illustrated by a solid checkerboard pattern).

The horizontal and vertical bars in these images show the red, green, and blue channels with varying opacity levels, then all three color channels together with those same varying opacity levels, then all three color channels set to zero with those varying opacity levels, then two bars showing a red/green/blue repeating gradient, the first with full opacity and the second with partial opacity, and finally a bar with the three color channels set to zero but the opacity varying in a repeating gradient.

## Application to the [Canvas] API

When using [Canvas.saveLayer] and [Canvas.restore], the blend mode of the [Paint] given to the [Canvas.saveLayer] will be applied when [Canvas.restore] is called. Each call to [Canvas.saveLayer] introduces a new layer onto which shapes and images are painted; when [Canvas.restore] is called, that layer is then composited onto the parent layer, with the source being the most-recently-drawn shapes and images, and the destination being the parent layer. (For the first [Canvas.saveLayer] call, the parent layer is the canvas itself.)

See also:

- [Paint.blendMode], which uses [BlendMode] to define the compositing strategy.

Drop both the source and destination images, leaving nothing.

This corresponds to the "clear" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_clear.png)

Drop the destination image, only paint the source image.

Conceptually, the destination is first cleared, then the source image is painted.

This corresponds to the "Copy" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_src.png)

Drop the source image, only paint the destination image.

Conceptually, the source image is discarded, leaving the destination untouched.

This corresponds to the "Destination" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dst.png)

Composite the source image over the destination image.

This is the default value. It represents the most intuitive case, where shapes are painted on top of what is below, with transparent areas showing the destination layer.

This corresponds to the "Source over Destination" Porter-Duff operator, also known as the Painter's Algorithm.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcOver.png)

Composite the source image under the destination image.

This is the opposite of [srcOver].

This corresponds to the "Destination over Source" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstOver.png)

This is useful when the source image should have been painted before the destination image, but could not be.

Show the source image, but only where the two images overlap. The destination image is not rendered, it is treated merely as a mask. The color channels of the destination are ignored, only the opacity has an effect.

To show the destination image instead, consider [dstIn].

To reverse the semantic of the mask (only showing the source where the destination is absent, rather than where it is present), consider [srcOut].

This corresponds to the "Source in Destination" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcIn.png)

Show the destination image, but only where the two images overlap. The source image is not rendered, it is treated merely as a mask. The color channels of the source are ignored, only the opacity has an effect.

To show the source image instead, consider [srcIn].

To reverse the semantic of the mask (only showing the source where the destination is present, rather than where it is absent), consider [dstOut].

This corresponds to the "Destination in Source" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstIn.png)

Show the source image, but only where the two images do not overlap. The destination image is not rendered, it is treated merely as a mask. The color channels of the destination are ignored, only the opacity has an effect.

To show the destination image instead, consider [dstOut].

To reverse the semantic of the mask (only showing the source where the destination is present, rather than where it is absent), consider [srcIn].

This corresponds to the "Source out Destination" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcOut.png)

Show the destination image, but only where the two images do not overlap. The source image is not rendered, it is treated merely as a mask. The color channels of the source are ignored, only the opacity has an effect.

To show the source image instead, consider [srcOut].

To reverse the semantic of the mask (only showing the destination where the source is present, rather than where it is absent), consider [dstIn].

This corresponds to the "Destination out Source" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstOut.png)

Composite the source image over the destination image, but only where it overlaps the destination.

This corresponds to the "Source atop Destination" Porter-Duff operator.

This is essentially the [srcOver] operator, but with the output's opacity channel being set to that of the destination image instead of being a combination of both image's opacity channels.

For a variant with the destination on top instead of the source, see [dstATop].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcATop.png)

Composite the destination image over the source image, but only where it overlaps the source.

This corresponds to the "Destination atop Source" Porter-Duff operator.

This is essentially the [dstOver] operator, but with the output's opacity channel being set to that of the source image instead of being a combination of both image's opacity channels.

For a variant with the source on top instead of the destination, see [srcATop].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstATop.png)

Apply a bitwise `xor` operator to the source and destination images. This leaves transparency where they would overlap.

This corresponds to the "Source xor Destination" Porter-Duff operator.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_xor.png)

Sum the components of the source and destination images.

Transparency in a pixel of one of the images reduces the contribution of that image to the corresponding output pixel, as if the color of that pixel in that image was darker.

This corresponds to the "Source plus Destination" Porter-Duff operator.

This is the right blend mode for cross-fading between two images. Consider two images A and B, and an interpolation time variable _t_ (from 0.0 to 1.0). To cross fade between them, A should be drawn with opacity 1.0 - _t_ into a new layer using [BlendMode.srcOver], and B should be drawn on top of it, at opacity _t_, into the same layer, using [BlendMode.plus].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_plus.png)

Multiply the color components of the source and destination images.

This can only result in the same or darker colors (multiplying by white, 1.0, results in no change; multiplying by black, 0.0, results in black).

When compositing two opaque images, this has similar effect to overlapping two transparencies on a projector.

For a variant that also multiplies the alpha channel, consider [multiply].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_modulate.png)

See also:

- [screen], which does a similar computation but inverted.
- [overlay], which combines [modulate] and [screen] to favor the destination image.
- [hardLight], which combines [modulate] and [screen] to favor the source image.

Multiply the inverse of the components of the source and destination images, and inverse the result.

Inverting the components means that a fully saturated channel (opaque white) is treated as the value 0.0, and values normally treated as 0.0 (black, transparent) are treated as 1.0.

This is essentially the same as [modulate] blend mode, but with the values of the colors inverted before the multiplication and the result being inverted back before rendering.

This can only result in the same or lighter colors (multiplying by black, 1.0, results in no change; multiplying by white, 0.0, results in white). Similarly, in the alpha channel, it can only result in more opaque colors.

This has similar effect to two projectors displaying their images on the same screen simultaneously.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_screen.png)

See also:

- [modulate], which does a similar computation but without inverting the values.
- [overlay], which combines [modulate] and [screen] to favor the destination image.
- [hardLight], which combines [modulate] and [screen] to favor the source image.

Multiply the components of the source and destination images after adjusting them to favor the destination.

Specifically, if the destination value is smaller, this multiplies it with the source value, whereas is the source value is smaller, it multiplies the inverse of the source value with the inverse of the destination value, then inverts the result.

Inverting the components means that a fully saturated channel (opaque white) is treated as the value 0.0, and values normally treated as 0.0 (black, transparent) are treated as 1.0.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_overlay.png)

See also:

- [modulate], which always multiplies the values.
- [screen], which always multiplies the inverses of the values.
- [hardLight], which is similar to [overlay] but favors the source image instead of the destination image.

Composite the source and destination image by choosing the lowest value from each color channel.

The opacity of the output image is computed in the same way as for [srcOver].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_darken.png)

Composite the source and destination image by choosing the highest value from each color channel.

The opacity of the output image is computed in the same way as for [srcOver].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_lighten.png)

Divide the destination by the inverse of the source.

Inverting the components means that a fully saturated channel (opaque white) is treated as the value 0.0, and values normally treated as 0.0 (black, transparent) are treated as 1.0.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_colorDodge.png)

Divide the inverse of the destination by the source, and inverse the result.

Inverting the components means that a fully saturated channel (opaque white) is treated as the value 0.0, and values normally treated as 0.0 (black, transparent) are treated as 1.0.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_colorBurn.png)

Multiply the components of the source and destination images after adjusting them to favor the source.

Specifically, if the source value is smaller, this multiplies it with the destination value, whereas is the destination value is smaller, it multiplies the inverse of the destination value with the inverse of the source value, then inverts the result.

Inverting the components means that a fully saturated channel (opaque white) is treated as the value 0.0, and values normally treated as 0.0 (black, transparent) are treated as 1.0.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_hardLight.png)

See also:

- [modulate], which always multiplies the values.
- [screen], which always multiplies the inverses of the values.
- [overlay], which is similar to [hardLight] but favors the destination image instead of the source image.

Use [colorDodge] for source values below 0.5 and [colorBurn] for source values above 0.5.

This results in a similar but softer effect than [overlay].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_softLight.png)

See also:

- [color], which is a more subtle tinting effect.

Subtract the smaller value from the bigger value for each channel.

Compositing black has no effect; compositing white inverts the colors of the other image.

The opacity of the output image is computed in the same way as for [srcOver].

The effect is similar to [exclusion] but harsher.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_difference.png)

Subtract double the product of the two images from the sum of the two images.

Compositing black has no effect; compositing white inverts the colors of the other image.

The opacity of the output image is computed in the same way as for [srcOver].

The effect is similar to [difference] but softer.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_exclusion.png)

Multiply the components of the source and destination images, including the alpha channel.

This can only result in the same or darker colors (multiplying by white, 1.0, results in no change; multiplying by black, 0.0, results in black).

Since the alpha channel is also multiplied, a fully-transparent pixel (opacity 0.0) in one image results in a fully transparent pixel in the output. This is similar to [dstIn], but with the colors combined.

For a variant that multiplies the colors but does not multiply the alpha channel, consider [modulate].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_multiply.png)

Take the hue of the source image, and the saturation and luminosity of the destination image.

The effect is to tint the destination image with the source image.

The opacity of the output image is computed in the same way as for [srcOver]. Regions that are entirely transparent in the source image take their hue from the destination.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_hue.png)

See also:

- [color], which is a similar but stronger effect as it also applies the saturation of the source image.
- [HSVColor], which allows colors to be expressed using Hue rather than the red/green/blue channels of [Color].

Take the saturation of the source image, and the hue and luminosity of the destination image.

The opacity of the output image is computed in the same way as for [srcOver]. Regions that are entirely transparent in the source image take their saturation from the destination.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_saturation.png)

See also:

- [color], which also applies the hue of the source image.
- [luminosity], which applies the luminosity of the source image to the destination.

Take the hue and saturation of the source image, and the luminosity of the destination image.

The effect is to tint the destination image with the source image.

The opacity of the output image is computed in the same way as for [srcOver]. Regions that are entirely transparent in the source image take their hue and saturation from the destination.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_color.png)

See also:

- [hue], which is a similar but weaker effect.
- [softLight], which is a similar tinting effect but also tints white.
- [saturation], which only applies the saturation of the source image.

Take the luminosity of the source image, and the hue and saturation of the destination image.

The opacity of the output image is computed in the same way as for [srcOver]. Regions that are entirely transparent in the source image take their luminosity from the destination.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_luminosity.png)

See also:

- [saturation], which applies the saturation of the source image to the destination.
- [ImageFilter.blur], which can be used with [BackdropFilter] for a related effect.

# FilterQuality

```dart
enum FilterQuality {}
```

Quality levels for image sampling in [ImageFilter] and [Shader] objects that sample images and for [Canvas] operations that render images.

When scaling up typically the quality is lowest at [none], higher at [low] and [medium], and for very large scale factors (over 10x) the highest at [high].

When scaling down, [medium] provides the best quality especially when scaling an image to less than half its size or for animating the scale factor between such reductions. Otherwise, [low] and [high] provide similar effects for reductions of between 50% and 100% but the image may lose detail and have dropouts below 50%.

To get high quality when scaling images up and down, or when the scale is unknown, [medium] is typically a good balanced choice.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/filter_quality.png)

See also:

- [Paint.filterQuality], which is used to pass [FilterQuality] to the engine while using drawImage calls on a [Canvas].
- [ImageShader].
- [FragmentShader.setImageSampler].
- [ImageFilter.matrix].
- [Canvas.drawImage].
- [Canvas.drawImageRect].
- [Canvas.drawImageNine].
- [Canvas.drawAtlas].

The fastest filtering method, albeit also the lowest quality.

This value results in a "Nearest Neighbor" algorithm which just repeats or eliminates pixels as an image is scaled up or down.

Better quality than [none], faster than [medium].

This value results in a "Bilinear" algorithm which smoothly interpolates between pixels in an image.

The best all around filtering method that is only worse than [high] at extremely large scale factors.

This value improves upon the "Bilinear" algorithm specified by [low] by utilizing a Mipmap that pre-computes high quality lower resolutions of the image at half (and quarter and eighth, etc.) sizes and then blends between those to prevent loss of detail at small scale sizes.

{@template dart.ui.filterQuality.seeAlso} See also:

- [FilterQuality] class-level documentation that goes into detail about relative qualities of the constant values. {@endtemplate}

Best possible quality when scaling up images by scale factors larger than 5-10x.

When images are scaled down, this can be worse than [medium] for scales smaller than 0.5x, or when animating the scale factor.

This option is also the slowest.

This value results in a standard "Bicubic" algorithm which uses a 3rd order equation to smooth the abrupt transitions between pixels while preserving some of the sense of an edge and avoiding sharp peaks in the result.

{@macro dart.ui.filterQuality.seeAlso}

# StrokeCap

```dart
enum StrokeCap {}
```

Styles to use for line endings.

See also:

- [Paint.strokeCap] for how this value is used.
- [StrokeJoin] for the different kinds of line segment joins.

Begin and end contours with a flat edge and no extension.

![A butt cap ends line segments with a square end that stops at the end of the line segment.](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/butt_cap.png)

Compare to the [square] cap, which has the same shape, but extends past the end of the line by half a stroke width.

Begin and end contours with a semi-circle extension.

![A round cap adds a rounded end to the line segment that protrudes by one half of the thickness of the line (which is the radius of the cap) past the end of the segment.](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/round_cap.png)

The cap is colored in the diagram above to highlight it: in normal use it is the same color as the line.

Begin and end contours with a half square extension. This is similar to extending each contour by half the stroke width (as given by [Paint.strokeWidth]).

![A square cap has a square end that effectively extends the line length by half of the stroke width.](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/square_cap.png)

The cap is colored in the diagram above to highlight it: in normal use it is the same color as the line.

Compare to the [butt] cap, which has the same shape, but doesn't extend past the end of the line.

# StrokeJoin

```dart
enum StrokeJoin {}
```

Styles to use for line segment joins.

This only affects line joins for polygons drawn by [Canvas.drawPath] and rectangles, not points drawn as lines with [Canvas.drawPoints].

See also:

- [Paint.strokeJoin] and [Paint.strokeMiterLimit] for how this value is used.
- [StrokeCap] for the different kinds of line endings.

Joins between line segments form sharp corners.

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_4_join.mp4}

The center of the line segment is colored in the diagram above to highlight the join, but in normal usage the join is the same color as the line.

See also:

- [Paint.strokeJoin], used to set the line segment join style to this value.
- [Paint.strokeMiterLimit], used to define when a miter is drawn instead of a bevel when the join is set to this value.

Joins between line segments are semi-circular.

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/round_join.mp4}

The center of the line segment is colored in the diagram above to highlight the join, but in normal usage the join is the same color as the line.

See also:

- [Paint.strokeJoin], used to set the line segment join style to this value.

Joins between line segments connect the corners of the butt ends of the line segments to give a beveled appearance.

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/bevel_join.mp4}

The center of the line segment is colored in the diagram above to highlight the join, but in normal usage the join is the same color as the line.

See also:

- [Paint.strokeJoin], used to set the line segment join style to this value.

# PaintingStyle

```dart
enum PaintingStyle {}
```

Strategies for painting shapes and paths on a canvas.

See [Paint.style].

Apply the [Paint] to the inside of the shape. For example, when applied to the [Canvas.drawCircle] call, this results in a disc of the given size being painted.

Apply the [Paint] to the edge of the shape. For example, when applied to the [Canvas.drawCircle] call, this results is a hoop of the given size being painted. The line drawn on the edge will be the width given by the [Paint.strokeWidth] property.

# Clip

```dart
enum Clip {}
```

Different ways to clip content.

See also:

- [Paint.isAntiAlias], the anti-aliasing switch for general draw operations.

No clip at all.

This is the default option for most widgets: if the content does not overflow the widget boundary, don't pay any performance cost for clipping.

If the content does overflow, consider the following [Clip] options:

- [hardEdge], which is the fastest clipping, but with lower fidelity.
- [antiAlias], which is a little slower than [hardEdge], but with smoothed edges.
- [antiAliasWithSaveLayer], which is much slower than [antiAlias], and should rarely be used.

Clip, but do not apply anti-aliasing.

This mode enables clipping, but curves and non-axis-aligned straight lines will be jagged as no effort is made to anti-alias.

Faster than other clipping modes, but slower than [none].

This is a reasonable choice when clipping is needed, if the container is an axis- aligned rectangle or an axis-aligned rounded rectangle with very small corner radii.

See also:

- [antiAlias], recommended when clipping is needed and the shape is not an axis-aligned rectangle.

Clip with anti-aliasing.

This mode has anti-aliased clipping edges, which reduces jagged edges when the clip shape itself has edges that are diagonal, curved, or otherwise not axis-aligned.

This is much faster than [antiAliasWithSaveLayer], but slower than [hardEdge].

Unlike [hardEdge] and [antiAliasWithSaveLayer], this clipping can have bleeding edge artifacts ([Skia Fiddle example](https://fiddle.skia.org/c/21cb4c2b2515996b537f36e7819288ae)).

See also:

- [hardEdge], which is faster, but with lower fidelity.
- [antiAliasWithSaveLayer], which is much slower, but avoids bleeding edge artifacts.
- [Paint.isAntiAlias], which is the anti-aliasing switch for general draw operations.

Clip with anti-aliasing and `saveLayer` immediately following the clip.

This mode not only clips with anti-aliasing, but also allocates an offscreen buffer. All subsequent paints are carried out on that buffer before finally being clipped and composited back.

This is very slow. It has no bleeding edge artifacts, unlike [antiAlias], but it changes the semantics as it introduces an offscreen buffer. For example, see this [Skia Fiddle without `saveLayer`](https://fiddle.skia.org/c/83ed46ceadaf90f36a4df3b98cbe1c35) and this [Skia Fiddle with `saveLayer`](https://fiddle.skia.org/c/704acfa049a7e99fbe685232c45d1582).

Use this mode only if necessary. For example, if you have an image overlaid on a very different background color. In these cases, consider if you can avoid overlaying multiple colors in one location (e.g. by having the background color only present where the image is absent). If possible, prefer [antiAlias] as it is much faster.

See also:

- [antiAlias], which is much faster, and has similar clipping results.
- [Canvas.saveLayer].

# Paint

```dart
final class Paint {}
```

A description of the style to use when drawing on a [Canvas].

Most APIs on [Canvas] take a [Paint] object to describe the style to use for that operation.

### Paint()

```dart
Paint()
```

Constructs an empty [Paint] object with all fields initialized to their defaults.

### Paint.from()

```dart
Paint.from(Paint other)
```

Constructs a new [Paint] object with the same fields as [other].

Any changes made to the object returned will not affect [other], and changes to [other] will not affect the object returned.

Backends (for example web versus native) may have different performance characteristics. If the code is performance-sensitive, consider profiling and falling back to reusing a single [Paint] object if necessary.

### isAntiAlias

```dart
bool get isAntiAlias
```

Whether to apply anti-aliasing to lines and images drawn on the canvas.

Defaults to true.

### isAntiAlias

```dart
set isAntiAlias(bool value)
```

### color

```dart
Color get color
```

The color to use when stroking or filling a shape.

Defaults to opaque black.

See also:

- [style], which controls whether to stroke or fill (or both).
- [colorFilter], which overrides [color].
- [shader], which overrides [color] with more elaborate effects.

This color is not used when compositing. To colorize a layer, use [colorFilter].

### color

```dart
set color(Color value)
```

### blendMode

```dart
BlendMode get blendMode
```

A blend mode to apply when a shape is drawn or a layer is composited.

The source colors are from the shape being drawn (e.g. from [Canvas.drawPath]) or layer being composited (the graphics that were drawn between the [Canvas.saveLayer] and [Canvas.restore] calls), after applying the [colorFilter], if any.

The destination colors are from the background onto which the shape or layer is being composited.

Defaults to [BlendMode.srcOver].

See also:

- [Canvas.saveLayer], which uses its [Paint]'s [blendMode] to composite the layer when [Canvas.restore] is called.
- [BlendMode], which discusses the user of [Canvas.saveLayer] with [blendMode].

### blendMode

```dart
set blendMode(BlendMode value)
```

### style

```dart
PaintingStyle get style
```

Whether to paint inside shapes, the edges of shapes, or both.

Defaults to [PaintingStyle.fill].

### style

```dart
set style(PaintingStyle value)
```

### strokeWidth

```dart
double get strokeWidth
```

How wide to make edges drawn when [style] is set to [PaintingStyle.stroke]. The width is given in logical pixels measured in the direction orthogonal to the direction of the path.

Defaults to 0.0, which correspond to a hairline width.

### strokeWidth

```dart
set strokeWidth(double value)
```

### strokeCap

```dart
StrokeCap get strokeCap
```

The kind of finish to place on the end of lines drawn when [style] is set to [PaintingStyle.stroke].

Defaults to [StrokeCap.butt], i.e. no caps.

### strokeCap

```dart
set strokeCap(StrokeCap value)
```

### strokeJoin

```dart
StrokeJoin get strokeJoin
```

The kind of finish to place on the joins between segments.

This applies to paths drawn when [style] is set to [PaintingStyle.stroke], It does not apply to points drawn as lines with [Canvas.drawPoints].

Defaults to [StrokeJoin.miter], i.e. sharp corners.

Some examples of joins:

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_4_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/round_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/bevel_join.mp4}

The centers of the line segments are colored in the diagrams above to highlight the joins, but in normal usage the join is the same color as the line.

See also:

- [strokeMiterLimit] to control when miters are replaced by bevels when this is set to [StrokeJoin.miter].
- [strokeCap] to control what is drawn at the ends of the stroke.
- [StrokeJoin] for the definitive list of stroke joins.

### strokeJoin

```dart
set strokeJoin(StrokeJoin value)
```

### strokeMiterLimit

```dart
double get strokeMiterLimit
```

The limit for miters to be drawn on segments when the join is set to [StrokeJoin.miter] and the [style] is set to [PaintingStyle.stroke]. If this limit is exceeded, then a [StrokeJoin.bevel] join will be drawn instead. This may cause some 'popping' of the corners of a path if the angle between line segments is animated, as seen in the diagrams below.

This limit is expressed as a limit on the length of the miter.

Defaults to 4.0. Using zero as a limit will cause a [StrokeJoin.bevel] join to be used all the time.

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_0_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_4_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_6_join.mp4}

The centers of the line segments are colored in the diagrams above to highlight the joins, but in normal usage the join is the same color as the line.

See also:

- [strokeJoin] to control the kind of finish to place on the joins between segments.
- [strokeCap] to control what is drawn at the ends of the stroke.

### strokeMiterLimit

```dart
set strokeMiterLimit(double value)
```

### maskFilter

```dart
MaskFilter? get maskFilter
```

A mask filter (for example, a blur) to apply to a shape after it has been drawn but before it has been composited into the image.

See [MaskFilter] for details.

### maskFilter

```dart
set maskFilter(MaskFilter? value)
```

### filterQuality

```dart
FilterQuality get filterQuality
```

Controls the performance vs quality trade-off to use when sampling bitmaps, as with an [ImageShader], or when drawing images, as with [Canvas.drawImage], [Canvas.drawImageRect], [Canvas.drawImageNine] or [Canvas.drawAtlas].

Defaults to [FilterQuality.none].

### filterQuality

```dart
set filterQuality(FilterQuality value)
```

### shader

```dart
Shader? get shader
```

The shader to use when stroking or filling a shape.

When this is null, the [color] is used instead.

See also:

- [Gradient], a shader that paints a color gradient.
- [ImageShader], a shader that tiles an [Image].
- [colorFilter], which overrides [shader].
- [color], which is used if [shader] and [colorFilter] are null.

### shader

```dart
set shader(Shader? value)
```

### colorFilter

```dart
ColorFilter? get colorFilter
```

A color filter to apply when a shape is drawn or when a layer is composited.

See [ColorFilter] for details.

When a shape is being drawn, [colorFilter] overrides [color] and [shader].

### colorFilter

```dart
set colorFilter(ColorFilter? value)
```

### imageFilter

```dart
ImageFilter? get imageFilter
```

The [ImageFilter] to use when drawing raster images.

For example, to blur an image using [Canvas.drawImage], apply an [ImageFilter.blur]:

```dart
void paint(Canvas canvas, Size size) {
  canvas.drawImage(
    _image,
    ui.Offset.zero,
    Paint()..imageFilter = ui.ImageFilter.blur(sigmaX: 0.5, sigmaY: 0.5),
  );
}
```

See also:

- [MaskFilter], which is used for drawing geometry.

### imageFilter

```dart
set imageFilter(ImageFilter? value)
```

### invertColors

```dart
bool get invertColors
```

Whether the colors of the image are inverted when drawn.

Inverting the colors of an image applies a new color filter that will be composed with any user provided color filters. This is primarily used for implementing smart invert on iOS.

### invertColors

```dart
set invertColors(bool value)
```

### toString()

```dart
String toString()
```

# ColorSpace

```dart
enum ColorSpace {}
```

The color space describes the colors that are available to an [Image].

This value can help decide which [ImageByteFormat] to use with [Image.toByteData]. Images that are in the [extendedSRGB] color space should use something like [ImageByteFormat.rawExtendedRgba128] so that colors outside of the sRGB gamut aren't lost.

This is also the result of [Image.colorSpace].

See also: https://en.wikipedia.org/wiki/Color_space

The sRGB color space.

You may know this as the standard color space for the web or the color space of non-wide-gamut Flutter apps.

See also: https://en.wikipedia.org/wiki/SRGB

A color space that is backwards compatible with sRGB but can represent colors outside of that gamut with values outside of [0..1]. In order to see the extended values an [ImageByteFormat] like [ImageByteFormat.rawExtendedRgba128] must be used.

The Display P3 color space.

This is a wide gamut color space that has broad hardware support. It's supported in cases like using Impeller on iOS. When used on a platform that doesn't support Display P3, the colors will be clamped to sRGB.

See also: https://en.wikipedia.org/wiki/DCI-P3

# ImageByteFormat

```dart
enum ImageByteFormat {}
```

The format in which image bytes should be returned when using [Image.toByteData].

Raw RGBA format.

Unencoded bytes, in RGBA row-primary form with premultiplied alpha, 8 bits per channel.

Raw straight RGBA format.

Unencoded bytes, in RGBA row-primary form with straight alpha, 8 bits per channel.

Raw unmodified format.

Unencoded bytes, in the image's existing format. For example, a grayscale image may use a single 8-bit channel for each pixel.

Raw extended range RGBA format.

Unencoded bytes, in RGBA row-primary form with straight alpha, 32 bit float (IEEE 754 binary32) per channel.

Example usage:

```dart
import 'dart:ui' as ui;
import 'dart:typed_data';

Future<Map<String, double>> getFirstPixel(ui.Image image) async {
  final ByteData data =
      (await image.toByteData(format: ui.ImageByteFormat.rawExtendedRgba128))!;
  final Float32List floats = Float32List.view(data.buffer);
  return <String, double>{
    'r': floats[0],
    'g': floats[1],
    'b': floats[2],
    'a': floats[3],
  };
}
```

PNG format.

A loss-less compression format for images. This format is well suited for images with hard edges, such as screenshots or sprites, and images with text. Transparency is supported. The PNG format supports images up to 2,147,483,647 pixels in either dimension, though in practice available memory provides a more immediate limitation on maximum image size.

PNG images normally use the `.png` file extension and the `image/png` MIME type.

See also:

- <https://en.wikipedia.org/wiki/Portable_Network_Graphics>, the Wikipedia page on PNG.
- <https://tools.ietf.org/rfc/rfc2083.txt>, the PNG standard.

# PixelFormat

```dart
enum PixelFormat {}
```

The format of pixel data given to [decodeImageFromPixels].

Each pixel is 32 bits, with the highest 8 bits encoding red, the next 8 bits encoding green, the next 8 bits encoding blue, and the lowest 8 bits encoding alpha. Premultiplied alpha is used.

Each pixel is 32 bits, with the highest 8 bits encoding blue, the next 8 bits encoding green, the next 8 bits encoding red, and the lowest 8 bits encoding alpha. Premultiplied alpha is used.

Each pixel is 128 bits, where each color component is a 32 bit float that is normalized across the sRGB gamut. The first float is the red component, followed by: green, blue and alpha. Premultiplied alpha isn't used, matching [ImageByteFormat.rawExtendedRgba128].

Each pixel is 32 bits, the red channel is just one 32 bit float.

# TargetPixelFormat

```dart
enum TargetPixelFormat {}
```

The format of pixel data of the texture generated by [decodeImageFromPixels].

Unspecified pixel format, let the engine decide the best pixel format.

Each pixel is 128 bits, where each color component is a 32 bit float.

Each pixel is 32 bits, the red channel is just one 32 bit float.

# ImageEventCallback

```dart
typedef ImageEventCallback = void Function(Image image)
```

Signature for [Image] lifecycle events.

# Image

```dart
class Image {}
```

Opaque handle to raw decoded image data (pixels).

To obtain an [Image] object, use the [ImageDescriptor] API.

To draw an [Image], use one of the methods on the [Canvas] class, such as [Canvas.drawImage].

A class or method that receives an image object must call [dispose] on the handle when it is no longer needed. To create a shareable reference to the underlying image, call [clone]. The method or object that receives the new instance will then be responsible for disposing it, and the underlying image itself will be disposed when all outstanding handles are disposed.

If `dart:ui` passes an `Image` object and the recipient wishes to share that handle with other callers, [clone] must be called _before_ [dispose]. A handle that has been disposed cannot create new handles anymore.

See also:

- [Image](https://api.flutter.dev/flutter/widgets/Image-class.html), the class in the [widgets] library.
- [ImageDescriptor], which allows reading information about the image and creating a codec to decode it.
- [instantiateImageCodec], a utility method that wraps [ImageDescriptor].

### onCreate

```dart
ImageEventCallback? onCreate
```

A callback that is invoked to report an image creation.

It's preferred to use [MemoryAllocations] in flutter/foundation.dart than to use [onCreate] directly because [MemoryAllocations] allows multiple callbacks.

### onDispose

```dart
ImageEventCallback? onDispose
```

A callback that is invoked to report the image disposal.

It's preferred to use [MemoryAllocations] in flutter/foundation.dart than to use [onDispose] directly because [MemoryAllocations] allows multiple callbacks.

### width

```dart
int width
```

The number of image pixels along the image's horizontal axis.

### height

```dart
int height
```

The number of image pixels along the image's vertical axis.

### dispose()

```dart
void dispose()
```

Release this handle's claim on the underlying Image. This handle is no longer usable after this method is called.

Once all outstanding handles have been disposed, the underlying image will be disposed as well.

In debug mode, [debugGetOpenHandleStackTraces] will return a list of [StackTrace] objects from all open handles' creation points. This is useful when trying to determine what parts of the program are keeping an image resident in memory.

### debugDisposed

```dart
bool get debugDisposed
```

Whether this reference to the underlying image is [dispose]d.

This only returns a valid value if asserts are enabled, and must not be used otherwise.

### toByteData()

```dart
Future<ByteData?> toByteData({ImageByteFormat format = ImageByteFormat.rawRgba})
```

Converts the [Image] object into a byte array.

The [format] argument specifies the format in which the bytes will be returned.

Using [ImageByteFormat.rawRgba] on an image in the color space [ColorSpace.extendedSRGB] will result in the gamut being squished to fit into the sRGB gamut, resulting in the loss of wide-gamut colors.

Returns a future that completes with the binary image data or an error if encoding fails.

### colorSpace

```dart
ColorSpace get colorSpace
```

The color space that is used by the [Image]'s colors.

This value is a consequence of how the [Image] has been created. For example, loading a PNG that is in the Display P3 color space will result in a [ColorSpace.extendedSRGB] image.

On rendering backends that don't support wide gamut colors (anything but iOS impeller), wide gamut images will still report [ColorSpace.sRGB] if rendering wide gamut colors isn't supported.

### debugGetOpenHandleStackTraces()

```dart
List<StackTrace>? debugGetOpenHandleStackTraces()
```

If asserts are enabled, returns the [StackTrace]s of each open handle from [clone], in creation order.

If asserts are disabled, this method always returns null.

### clone()

```dart
Image clone()
```

Creates a disposable handle to this image.

Holders of an [Image] must dispose of the image when they no longer need to access it or draw it. However, once the underlying image is disposed, it is no longer possible to use it. If a holder of an image needs to share access to that image with another object or method, [clone] creates a duplicate handle. The underlying image will only be disposed once all outstanding handles are disposed. This allows for safe sharing of image references while still disposing of the underlying resources when all consumers are finished.

It is safe to pass an [Image] handle to another object or method if the current holder no longer needs it.

To check whether two [Image] references are referring to the same underlying image memory, use [isCloneOf] rather than the equality operator or [identical].

The following example demonstrates valid usage.

```dart
import 'dart:async';
import 'dart:typed_data';
import 'dart:ui';

Future<Image> _loadImage(int width, int height) {
  final Completer<Image> completer = Completer<Image>();
  decodeImageFromPixels(
    Uint8List.fromList(List<int>.filled(width * height * 4, 0xFF)),
    width,
    height,
    PixelFormat.rgba8888,
    // Don't worry about disposing or cloning this image - responsibility
    // is transferred to the caller, and that is safe since this method
    // will not touch it again.
    (Image image) => completer.complete(image),
  );
  return completer.future;
}

Future<void> main() async {
  final Image image = await _loadImage(5, 5);
  // Make sure to clone the image, because MyHolder might dispose it
  // and we need to access it again.
  final MyImageHolder holder = MyImageHolder(image.clone());
  final MyImageHolder holder2 = MyImageHolder(image.clone());
  // Now we dispose it because we won't need it again.
  image.dispose();

  final PictureRecorder recorder = PictureRecorder();
  final Canvas canvas = Canvas(recorder);

  holder.draw(canvas);
  holder.dispose();

  canvas.translate(50, 50);
  holder2.draw(canvas);
  holder2.dispose();
}

class MyImageHolder {
  MyImageHolder(this.image);

  final Image image;

  void draw(Canvas canvas) {
    canvas.drawImage(image, Offset.zero, Paint());
  }

  void dispose() => image.dispose();
}
```

The returned object behaves identically to this image. Calling [dispose] on it will only dispose the underlying native resources if it is the last remaining handle.

### isCloneOf()

```dart
bool isCloneOf(Image other)
```

Returns true if `other` is a [clone] of this and thus shares the same underlying image memory, even if this or `other` is [dispose]d.

This method may return false for two images that were decoded from the same underlying asset, if they are not sharing the same memory. For example, if the same file is decoded using [instantiateImageCodec] twice, or the same bytes are decoded using [decodeImageFromPixels] twice, there will be two distinct [Image]s that render the same but do not share underlying memory, and so will not be treated as clones of each other.

### toString()

```dart
String toString()
```

# ImageDecoderCallback

```dart
typedef ImageDecoderCallback = void Function(Image result)
```

Callback signature for [decodeImageFromList].

# FrameInfo

```dart
class FrameInfo {}
```

Information for a single frame of an animation.

To obtain an instance of the [FrameInfo] interface, see [Codec.getNextFrame].

The recipient of an instance of this class is responsible for calling [Image.dispose] on [image]. To share the image with other interested parties, use [Image.clone]. If the [FrameInfo] object itself is passed to another method or object, that method or object must assume it is responsible for disposing the image when done, and the passer must not access the [image] after that point.

For example, the following code sample is incorrect:

```dart
/// BAD
Future<void> nextFrameRoutine(ui.Codec codec) async {
  final ui.FrameInfo frameInfo = await codec.getNextFrame();
  _cacheImage(frameInfo);
  // ERROR - _cacheImage is now responsible for disposing the image, and
  // the image may not be available any more for this drawing routine.
  _drawImage(frameInfo);
  // ERROR again - the previous methods might or might not have created
  // handles to the image.
  frameInfo.image.dispose();
}
```

Correct usage is:

```dart
/// GOOD
Future<void> nextFrameRoutine(ui.Codec codec) async {
  final ui.FrameInfo frameInfo = await codec.getNextFrame();
  _cacheImage(frameInfo.image.clone(), frameInfo.duration);
  _drawImage(frameInfo.image.clone(), frameInfo.duration);
  // This method is done with its handle, and has passed handles to its
  // clients already.
  // The image will live until those clients dispose of their handles, and
  // this one must not be disposed since it will not be used again.
  frameInfo.image.dispose();
}
```

### duration

```dart
Duration duration
```

The duration this frame should be shown.

A zero duration indicates that the frame should be shown indefinitely.

### image

```dart
Image image
```

The [Image] object for this frame.

This object must be disposed by the recipient of this frame info.

To share this image with other interested parties, use [Image.clone].

# Codec

```dart
abstract class Codec {}
```

A handle to an image codec.

This class is created by the engine, and should not be instantiated or extended directly.

To obtain an instance of the [Codec] interface, see [instantiateImageCodec].

### frameCount

```dart
int get frameCount
```

Number of frames in this image.

### repetitionCount

```dart
int get repetitionCount
```

Number of times to repeat the animation.

- 0 when the animation should be played once.
- -1 for infinity repetitions.

### getNextFrame()

```dart
Future<FrameInfo> getNextFrame()
```

Fetches the next animation frame.

Wraps back to the first frame after returning the last frame.

The returned future can complete with an error if the decoding has failed.

The caller of this method is responsible for disposing the [FrameInfo.image] on the returned object.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

This can't be a leaf call because the native function calls Dart API (Dart_SetNativeInstanceField).

# instantiateImageCodec()

```dart
Future<Codec> instantiateImageCodec(Uint8List list, {int? targetWidth, int? targetHeight, bool allowUpscaling = true})
```

Instantiates an image [Codec].

This method is a convenience wrapper around the [ImageDescriptor] API, and using [ImageDescriptor] directly is preferred since it allows the caller to make better determinations about how and whether to use the `targetWidth` and `targetHeight` parameters.

The `list` parameter is the binary image data (e.g a PNG or GIF binary data). The data can be for either static or animated images. The following image formats are supported:

{@template dart.ui.imageFormats} JPEG, PNG, GIF, Animated GIF, WebP, Animated WebP, BMP, and WBMP. Additional formats may be supported by the underlying platform. Flutter will attempt to call platform API to decode unrecognized formats, and if the platform API supports decoding the image Flutter will be able to render it. {@endtemplate}

The `targetWidth` and `targetHeight` arguments specify the size of the output image, in image pixels. If they are not equal to the intrinsic dimensions of the image, then the image will be scaled after being decoded. If the `allowUpscaling` parameter is not set to true, both dimensions will be capped at the intrinsic dimensions of the image, even if only one of them would have exceeded those intrinsic dimensions. If exactly one of these two arguments is specified, then the aspect ratio will be maintained while forcing the image to match the other given dimension. If neither is specified, then the image maintains its intrinsic size.

Scaling the image to larger than its intrinsic size should usually be avoided, since it causes the image to use more memory than necessary. Instead, prefer scaling the [Canvas] transform. If the image must be scaled up, the `allowUpscaling` parameter must be set to true.

The returned future can complete with an error if the image decoding has failed.

# instantiateImageCodecFromBuffer()

```dart
Future<Codec> instantiateImageCodecFromBuffer(ImmutableBuffer buffer, {int? targetWidth, int? targetHeight, bool allowUpscaling = true})
```

Instantiates an image [Codec].

This method is a convenience wrapper around the [ImageDescriptor] API, and using [ImageDescriptor] directly is preferred since it allows the caller to make better determinations about how and whether to use the `targetWidth` and `targetHeight` parameters.

The [buffer] parameter is the binary image data (e.g a PNG or GIF binary data). The data can be for either static or animated images. The following image formats are supported: {@macro dart.ui.imageFormats}

The [buffer] will be disposed by this method once the codec has been created, so the caller must relinquish ownership of the [buffer] when they call this method.

The [targetWidth] and [targetHeight] arguments specify the size of the output image, in image pixels. If they are not equal to the intrinsic dimensions of the image, then the image will be scaled after being decoded. If the `allowUpscaling` parameter is not set to true, both dimensions will be capped at the intrinsic dimensions of the image, even if only one of them would have exceeded those intrinsic dimensions. If exactly one of these two arguments is specified, then the aspect ratio will be maintained while forcing the image to match the other given dimension. If neither is specified, then the image maintains its intrinsic size.

Scaling the image to larger than its intrinsic size should usually be avoided, since it causes the image to use more memory than necessary. Instead, prefer scaling the [Canvas] transform. If the image must be scaled up, the `allowUpscaling` parameter must be set to true.

The returned future can complete with an error if the image decoding has failed.

# instantiateImageCodecWithSize()

```dart
Future<Codec> instantiateImageCodecWithSize(ImmutableBuffer buffer, {TargetImageSizeCallback? getTargetSize})
```

Instantiates an image [Codec].

This method is a convenience wrapper around the [ImageDescriptor] API.

The [buffer] parameter is the binary image data (e.g a PNG or GIF binary data). The data can be for either static or animated images. The following image formats are supported: {@macro dart.ui.imageFormats}

The [buffer] will be disposed by this method once the codec has been created, so the caller must relinquish ownership of the [buffer] when they call this method.

The [getTargetSize] parameter, when specified, will be invoked and passed the image's intrinsic size to determine the size to decode the image to. The width and the height of the size it returns must be positive values greater than or equal to 1, or null. It is valid to return a [TargetImageSize] that specifies only one of `width` and `height` with the other remaining null, in which case the omitted dimension will be scaled to maintain the aspect ratio of the original dimensions. When both are null or omitted, the image will be decoded at its native resolution (as will be the case if the [getTargetSize] parameter is omitted).

Scaling the image to larger than its intrinsic size should usually be avoided, since it causes the image to use more memory than necessary. Instead, prefer scaling the [Canvas] transform.

The returned future can complete with an error if the image decoding has failed.

# TargetImageSizeCallback

```dart
typedef TargetImageSizeCallback = TargetImageSize Function(int intrinsicWidth, int intrinsicHeight)
```

Signature for a callback that determines the size to which an image should be decoded given its intrinsic size.

See also:

- [instantiateImageCodecWithSize], which used this signature for its `getTargetSize` argument.

# TargetImageSize

```dart
class TargetImageSize {}
```

A specification of the size to which an image should be decoded.

See also:

- [TargetImageSizeCallback], a callback that returns instances of this class when consulted by image decoding methods such as [instantiateImageCodecWithSize].

### TargetImageSize()

```dart
TargetImageSize({int? width, int? height})
```

Creates a new instance of this class.

The `width` and `height` may both be null, but if they're non-null, they must be positive.

### width

```dart
int? width
```

The width into which to load the image.

If this is non-null, the image will be decoded into the specified width. If this is null and [height] is also null, the image will be decoded into its intrinsic size. If this is null and [height] is non-null, the image will be decoded into a width that maintains its intrinsic aspect ratio while respecting the [height] value.

If this value is non-null, it must be positive.

### height

```dart
int? height
```

The height into which to load the image.

If this is non-null, the image will be decoded into the specified height. If this is null and [width] is also null, the image will be decoded into its intrinsic size. If this is null and [width] is non-null, the image will be decoded into a height that maintains its intrinsic aspect ratio while respecting the [width] value.

If this value is non-null, it must be positive.

### toString()

```dart
String toString()
```

# decodeImageFromList()

```dart
void decodeImageFromList(Uint8List list, ImageDecoderCallback callback)
```

Loads a single image frame from a byte array into an [Image] object.

This is a convenience wrapper around [instantiateImageCodec]. Prefer using [instantiateImageCodec] which also supports multi frame images and offers better error handling. This function swallows asynchronous errors.

# decodeImageFromPixels()

```dart
void decodeImageFromPixels(Uint8List pixels, int width, int height, PixelFormat format, ImageDecoderCallback callback, {int? rowBytes, int? targetWidth, int? targetHeight, bool allowUpscaling = true, TargetPixelFormat targetFormat = TargetPixelFormat.dontCare})
```

Convert an array of pixel values into an [Image] object.

The `pixels` parameter is the pixel data. They are packed in bytes in the order described by `format`, then grouped in rows, from left to right, then top to bottom.

The `rowBytes` parameter is the number of bytes consumed by each row of pixels in the data buffer. If unspecified, it defaults to `width` multiplied by the number of bytes per pixel in the provided `format`.

The `targetWidth` and `targetHeight` arguments specify the size of the output image, in image pixels. If they are not equal to the intrinsic dimensions of the image, then the image will be scaled after being decoded. If the `allowUpscaling` parameter is not set to true, both dimensions will be capped at the intrinsic dimensions of the image, even if only one of them would have exceeded those intrinsic dimensions. If exactly one of these two arguments is specified, then the aspect ratio will be maintained while forcing the image to match the other given dimension. If neither is specified, then the image maintains its intrinsic size.

Scaling the image to larger than its intrinsic size should usually be avoided, since it causes the image to use more memory than necessary. Instead, prefer scaling the [Canvas] transform. If the image must be scaled up, the `allowUpscaling` parameter must be set to true.

# decodeImageFromPixelsSync()

```dart
Image decodeImageFromPixelsSync(Uint8List pixels, int width, int height, PixelFormat format)
```

Decodes the given [pixels] into an [Image] synchronously.

The [pixels] are expected to be in the format specified by [format].

The [width] and [height] arguments specify the dimensions of the image.

This function returns an [Image] immediately. The image might not be fully decoded yet, but it can be drawn to a [Canvas].

# PathFillType

```dart
enum PathFillType {}
```

Determines the winding rule that decides how the interior of a [Path] is calculated.

This enum is used by the [Path.fillType] property.

The interior is defined by a non-zero sum of signed edge crossings.

For a given point, the point is considered to be on the inside of the path if a line drawn from the point to infinity crosses lines going clockwise around the point a different number of times than it crosses lines going counter-clockwise around that point.

See: <https://en.wikipedia.org/wiki/Nonzero-rule>

The interior is defined by an odd number of edge crossings.

For a given point, the point is considered to be on the inside of the path if a line drawn from the point to infinity crosses an odd number of lines.

See: <https://en.wikipedia.org/wiki/Even-odd_rule>

# PathOperation

```dart
enum PathOperation {}
```

Strategies for combining paths.

See also:

- [Path.combine], which uses this enum to decide how to combine two paths.

Subtract the second path from the first path.

For example, if the two paths are overlapping circles of equal diameter but differing centers, the result would be a crescent portion of the first circle that was not overlapped by the second circle.

See also:

- [reverseDifference], which is the same but subtracting the first path from the second.

Create a new path that is the intersection of the two paths, leaving the overlapping pieces of the path.

For example, if the two paths are overlapping circles of equal diameter but differing centers, the result would be only the overlapping portion of the two circles.

See also:

- [xor], which is the inverse of this operation

Create a new path that is the union (inclusive-or) of the two paths.

For example, if the two paths are overlapping circles of equal diameter but differing centers, the result would be a figure-eight like shape matching the outer boundaries of both circles.

Create a new path that is the exclusive-or of the two paths, leaving everything but the overlapping pieces of the path.

For example, if the two paths are overlapping circles of equal diameter but differing centers, the figure-eight like shape less the overlapping parts

See also:

- [intersect], which is the inverse of this operation

Subtract the first path from the second path.

For example, if the two paths are overlapping circles of equal diameter but differing centers, the result would be a crescent portion of the second circle that was not overlapped by the first circle.

See also:

- [difference], which is the same but subtracting the second path from the first.

# EngineLayer

```dart
abstract class EngineLayer {}
```

A handle for the framework to hold and retain an engine layer across frames.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

EngineLayers indirectly retain platform specific graphics resources. Some of these resources, such as images, may be memory intensive. It is important to dispose of EngineLayer objects that will no longer be used as soon as possible to avoid retaining these resources until the next garbage collection.

Once this EngineLayer is disposed, it is no longer eligible for use as a retained layer, and must not be passed as an `oldLayer` to any of the [SceneBuilder] methods which accept that parameter.

This can't be a leaf call because the native function calls Dart API (Dart_SetNativeInstanceField).

# Path

```dart
abstract class Path {}
```

A complex, one-dimensional subset of a plane.

A path consists of a number of sub-paths, and a _current point_.

Sub-paths consist of segments of various types, such as lines, arcs, or beziers. Sub-paths can be open or closed, and can self-intersect.

Closed sub-paths enclose a (possibly discontiguous) region of the plane based on the current [fillType].

The _current point_ is initially at the origin. After each operation adding a segment to a sub-path, the current point is updated to the end of that segment.

Paths can be drawn on canvases using [Canvas.drawPath], and can used to create clip regions using [Canvas.clipPath].

### Path()

```dart
Path()
```

### Path.from()

```dart
Path.from(Path source)
```

Creates a copy of another [Path].

This copy is fast and does not require additional memory unless either the `source` path or the path returned by this constructor are modified.

### fillType

```dart
PathFillType get fillType
```

Determines how the interior of this path is calculated.

Defaults to the non-zero winding rule, [PathFillType.nonZero].

### fillType

```dart
set fillType(PathFillType value)
```

### moveTo()

```dart
void moveTo(double x, double y)
```

Starts a new sub-path at the given coordinate.

### relativeMoveTo()

```dart
void relativeMoveTo(double dx, double dy)
```

Starts a new sub-path at the given offset from the current point.

### lineTo()

```dart
void lineTo(double x, double y)
```

Adds a straight line segment from the current point to the given point.

### relativeLineTo()

```dart
void relativeLineTo(double dx, double dy)
```

Adds a straight line segment from the current point to the point at the given offset from the current point.

### quadraticBezierTo()

```dart
void quadraticBezierTo(double x1, double y1, double x2, double y2)
```

Adds a quadratic bezier segment that curves from the current point to the given point (x2,y2), using the control point (x1,y1).

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_quadratic_to.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_quadratic_to_dark.png#gh-dark-mode-only)

### relativeQuadraticBezierTo()

```dart
void relativeQuadraticBezierTo(double x1, double y1, double x2, double y2)
```

Adds a quadratic bezier segment that curves from the current point to the point at the offset (x2,y2) from the current point, using the control point at the offset (x1,y1) from the current point.

### cubicTo()

```dart
void cubicTo(double x1, double y1, double x2, double y2, double x3, double y3)
```

Adds a cubic bezier segment that curves from the current point to the given point (x3,y3), using the control points (x1,y1) and (x2,y2).

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_cubic_to.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_cubic_to_dark.png#gh-dark-mode-only)

### relativeCubicTo()

```dart
void relativeCubicTo(double x1, double y1, double x2, double y2, double x3, double y3)
```

Adds a cubic bezier segment that curves from the current point to the point at the offset (x3,y3) from the current point, using the control points at the offsets (x1,y1) and (x2,y2) from the current point.

### conicTo()

```dart
void conicTo(double x1, double y1, double x2, double y2, double w)
```

Adds a bezier segment that curves from the current point to the given point (x2,y2), using the control points (x1,y1) and the weight w. If the weight is greater than 1, then the curve is a hyperbola; if the weight equals 1, it's a parabola; and if it is less than 1, it is an ellipse.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_conic_to.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_conic_to_dark.png#gh-dark-mode-only)

### relativeConicTo()

```dart
void relativeConicTo(double x1, double y1, double x2, double y2, double w)
```

Adds a bezier segment that curves from the current point to the point at the offset (x2,y2) from the current point, using the control point at the offset (x1,y1) from the current point and the weight w. If the weight is greater than 1, then the curve is a hyperbola; if the weight equals 1, it's a parabola; and if it is less than 1, it is an ellipse.

### arcTo()

```dart
void arcTo(Rect rect, double startAngle, double sweepAngle, bool forceMoveTo)
```

If the `forceMoveTo` argument is false, adds a straight line segment and an arc segment.

If the `forceMoveTo` argument is true, starts a new sub-path consisting of an arc segment.

In either case, the arc segment consists of the arc that follows the edge of the oval bounded by the given rectangle, from startAngle radians around the oval up to startAngle + sweepAngle radians around the oval, with zero radians being the point on the right hand side of the oval that crosses the horizontal line that intersects the center of the rectangle and with positive angles going clockwise around the oval.

The line segment added if `forceMoveTo` is false starts at the current point and ends at the start of the arc. Note that this method does not draw anything if the [sweepAngle] is a multiple of $2\pi$ (e.g., $2\pi$, $4\pi$). If you need to draw a full circle or an overlapping arc, use [addArc] as a workaround.

### arcToPoint()

```dart
void arcToPoint(Offset arcEnd, {Radius radius = Radius.zero, double rotation = 0.0, bool largeArc = false, bool clockwise = true})
```

Appends up to four conic curves weighted to describe an oval of `radius` and rotated by `rotation` (measured in degrees and clockwise).

The first curve begins from the last point in the path and the last ends at `arcEnd`. The curves follow a path in a direction determined by `clockwise` and `largeArc` in such a way that the sweep angle is always less than 360 degrees.

A simple line is appended if either radii are zero or the last point in the path is `arcEnd`. The radii are scaled to fit the last path point if both are greater than zero but too small to describe an arc.

### relativeArcToPoint()

```dart
void relativeArcToPoint(Offset arcEndDelta, {Radius radius = Radius.zero, double rotation = 0.0, bool largeArc = false, bool clockwise = true})
```

Appends up to four conic curves weighted to describe an oval of `radius` and rotated by `rotation` (measured in degrees and clockwise).

The last path point is described by (px, py).

The first curve begins from the last point in the path and the last ends at `arcEndDelta.dx + px` and `arcEndDelta.dy + py`. The curves follow a path in a direction determined by `clockwise` and `largeArc` in such a way that the sweep angle is always less than 360 degrees.

A simple line is appended if either radii are zero, or, both `arcEndDelta.dx` and `arcEndDelta.dy` are zero. The radii are scaled to fit the last path point if both are greater than zero but too small to describe an arc.

### addRect()

```dart
void addRect(Rect rect)
```

Adds a new sub-path that consists of four lines that outline the given rectangle.

### addOval()

```dart
void addOval(Rect oval)
```

Adds a new sub-path that consists of a curve that forms the ellipse that fills the given rectangle.

To add a circle, pass an appropriate rectangle as `oval`. [Rect.fromCircle] can be used to easily describe the circle's center [Offset] and radius.

### addArc()

```dart
void addArc(Rect oval, double startAngle, double sweepAngle)
```

Adds a new sub-path with one arc segment that consists of the arc that follows the edge of the oval bounded by the given rectangle, from startAngle radians around the oval up to startAngle + sweepAngle radians around the oval, with zero radians being the point on the right hand side of the oval that crosses the horizontal line that intersects the center of the rectangle and with positive angles going clockwise around the oval.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc_dark.png#gh-dark-mode-only)

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc_ccw.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc_ccw_dark.png#gh-dark-mode-only)

### addPolygon()

```dart
void addPolygon(List<Offset> points, bool close)
```

Adds a new sub-path with a sequence of line segments that connect the given points.

If `close` is true, a final line segment will be added that connects the last point to the first point.

The `points` argument is interpreted as offsets from the origin.

### addRRect()

```dart
void addRRect(RRect rrect)
```

Adds a new sub-path that consists of the straight lines and curves needed to form the rounded rectangle described by the argument.

### addRSuperellipse()

```dart
void addRSuperellipse(RSuperellipse rsuperellipse)
```

Adds a new sub-path that consists of curves needed to form the rounded superellipse described by the argument.

### addPath()

```dart
void addPath(Path path, Offset offset, {Float64List? matrix4})
```

Adds the sub-paths of `path`, offset by `offset`, to this path.

If `matrix4` is specified, the path will be transformed by this matrix after the matrix is translated by the given offset. The matrix is a 4x4 matrix stored in column major order.

### extendWithPath()

```dart
void extendWithPath(Path path, Offset offset, {Float64List? matrix4})
```

Adds the sub-paths of `path`, offset by `offset`, to this path. The current sub-path is extended with the first sub-path of `path`, connecting them with a lineTo if necessary.

If `matrix4` is specified, the path will be transformed by this matrix after the matrix is translated by the given `offset`. The matrix is a 4x4 matrix stored in column major order.

### close()

```dart
void close()
```

Closes the last sub-path, as if a straight line had been drawn from the current point to the first point of the sub-path.

### reset()

```dart
void reset()
```

Clears the [Path] object of all sub-paths, returning it to the same state it had when it was created. The _current point_ is reset to the origin.

### contains()

```dart
bool contains(Offset point)
```

Tests to see if the given point is within the path. (That is, whether the point would be in the visible portion of the path if the path was used with [Canvas.clipPath].)

The `point` argument is interpreted as an offset from the origin.

Returns true if the point is in the path, and false otherwise.

### shift()

```dart
Path shift(Offset offset)
```

Returns a copy of the path with all the segments of every sub-path translated by the given offset.

### transform()

```dart
Path transform(Float64List matrix4)
```

Returns a copy of the path with all the segments of every sub-path transformed by the given matrix.

### getBounds()

```dart
Rect getBounds()
```

Computes the bounding rectangle for this path.

A path containing only axis-aligned points on the same straight line will have no area, and therefore `Rect.isEmpty` will return true for such a path. Consider checking `rect.width + rect.height > 0.0` instead, or using the [computeMetrics] API to check the path length.

For many more elaborate paths, the bounds may be inaccurate. For example, when a path contains a circle, the points used to compute the bounds are the circle's implied control points, which form a square around the circle; if the circle has a transformation applied using [transform] then that square is rotated, and the (axis-aligned, non-rotated) bounding box therefore ends up grossly overestimating the actual area covered by the circle.

### combine()

```dart
Path combine(PathOperation operation, Path path1, Path path2)
```

Combines the two paths according to the manner specified by the given `operation`.

The resulting path will be constructed from non-overlapping contours. The curve order is reduced where possible so that cubics may be turned into quadratics, and quadratics maybe turned into lines.

### computeMetrics()

```dart
PathMetrics computeMetrics({bool forceClosed = false})
```

Creates a [PathMetrics] object for this path, which can describe various properties about the contours of the path.

A [Path] is made up of zero or more contours. A contour is made up of connected curves and segments, created via methods like [lineTo], [cubicTo], [arcTo], [quadraticBezierTo], their relative counterparts, as well as the add\* methods such as [addRect]. Creating a new [Path] starts a new contour once it has any drawing instructions, and another new contour is started for each [moveTo] instruction.

A [PathMetric] object describes properties of an individual contour, such as its length, whether it is closed, what the tangent vector of a particular offset along the path is. It also provides a method for creating sub-paths: [PathMetric.extractPath].

Calculating [PathMetric] objects is not trivial. The [PathMetrics] object returned by this method is a lazy [Iterable], meaning it only performs calculations when the iterator is moved to the next [PathMetric]. Callers that wish to memoize this iterable can easily do so by using [Iterable.toList] on the result of this method. In particular, callers looking for information about how many contours are in the path should either store the result of `path.computeMetrics().length`, or should use `path.computeMetrics().toList()` so they can repeatedly check the length, since calling `Iterable.length` causes traversal of the entire iterable.

In particular, callers should be aware that [PathMetrics.length] is the number of contours, **not the length of the path**. To get the length of a contour in a path, use [PathMetric.length].

Zero-length contours (where the start and end points are the same, such as `Path()..lineTo(0, 0)`) are not included in the returned [PathMetrics]. Only contours with a positive length will have a corresponding [PathMetric].

If `forceClosed` is set to true, the contours of the path will be measured as if they had been closed, even if they were not explicitly closed.

# Tangent

```dart
class Tangent {}
```

The geometric description of a tangent: the angle at a point.

See also:

- [PathMetric.getTangentForOffset], which returns the tangent of an offset along a path.

### Tangent()

```dart
Tangent(Offset position, Offset vector)
```

Creates a [Tangent] with the given values.

The arguments must not be null.

### Tangent.fromAngle()

```dart
Tangent.fromAngle(Offset position, double angle)
```

Creates a [Tangent] based on the angle rather than the vector.

The [vector] is computed to be the unit vector at the given angle, interpreted as clockwise radians from the x axis.

### position

```dart
Offset position
```

Position of the tangent.

When used with [PathMetric.getTangentForOffset], this represents the precise position that the given offset along the path corresponds to.

### vector

```dart
Offset vector
```

The vector of the curve at [position].

When used with [PathMetric.getTangentForOffset], this is the vector of the curve that is at the given offset along the path (i.e. the direction of the curve at [position]).

### angle

```dart
double get angle
```

The direction of the curve at [position].

When used with [PathMetric.getTangentForOffset], this is the angle of the curve that is the given offset along the path (i.e. the direction of the curve at [position]).

This value is in radians, with 0.0 meaning pointing along the x axis in the positive x-axis direction, positive numbers pointing downward toward the negative y-axis, i.e. in a clockwise direction, and negative numbers pointing upward toward the positive y-axis, i.e. in a counter-clockwise direction.

# PathMetrics

```dart
class PathMetrics extends collection.IterableBase<PathMetric> {}
```

An iterable collection of [PathMetric] objects describing a [Path].

A [PathMetrics] object is created by using the [Path.computeMetrics] method, and represents the path as it stood at the time of the call. Subsequent modifications of the path do not affect the [PathMetrics] object.

Each path metric corresponds to a segment, or contour, of a path.

For example, a path consisting of a [Path.lineTo], a [Path.moveTo], and another [Path.lineTo] will contain two contours and thus be represented by two [PathMetric] objects.

This iterable does not memoize. Callers who need to traverse the list multiple times, or who need to randomly access elements of the list, should use [toList] on this object.

### iterator

```dart
Iterator<PathMetric> get iterator
```

# PathMetricIterator

```dart
class PathMetricIterator implements Iterator<PathMetric> {}
```

Used by [PathMetrics] to track iteration from one segment of a path to the next for measurement.

### current

```dart
PathMetric get current
```

### moveNext()

```dart
bool moveNext()
```

# PathMetric

```dart
class PathMetric {}
```

Utilities for measuring a [Path] and extracting sub-paths.

Iterate over the object returned by [Path.computeMetrics] to obtain [PathMetric] objects. Callers that want to randomly access elements or iterate multiple times should use `path.computeMetrics().toList()`, since [PathMetrics] does not memoize.

Once created, the metrics are only valid for the path as it was specified when [Path.computeMetrics] was called. If additional contours are added or any contours are updated, the metrics need to be recomputed. Previously created metrics will still refer to a snapshot of the path at the time they were computed, rather than to the actual metrics for the new mutations to the path.

### length

```dart
double length
```

Return the total length of the current contour.

The length may be calculated from an approximation of the geometry originally added. For this reason, it is not recommended to rely on this property for mathematically correct lengths of common shapes.

### isClosed

```dart
bool isClosed
```

Whether the contour is closed.

Returns true if the contour ends with a call to [Path.close] (which may have been implied when using methods like [Path.addRect]) or if `forceClosed` was specified as true in the call to [Path.computeMetrics]. Returns false otherwise.

### contourIndex

```dart
int contourIndex
```

The zero-based index of the contour.

[Path] objects are made up of zero or more contours. The first contour is created once a drawing command (e.g. [Path.lineTo]) is issued. A [Path.moveTo] command after a drawing command may create a new contour, although it may not if optimizations are applied that determine the move command did not actually result in moving the pen.

This property is only valid with reference to its original iterator and the contours of the path at the time the path's metrics were computed. If additional contours were added or existing contours updated, this metric will be invalid for the current state of the path.

### getTangentForOffset()

```dart
Tangent? getTangentForOffset(double distance)
```

Computes the position of the current contour at the given offset, and the angle of the path at that point.

For example, calling this method with a distance of 1.41 for a line from 0.0,0.0 to 2.0,2.0 would give a point 1.0,1.0 and the angle 45 degrees (but in radians).

Returns null if the contour has zero [length].

The distance is clamped to the [length] of the current contour.

### extractPath()

```dart
Path extractPath(double start, double end, {bool startWithMoveTo = true})
```

Given a start and end distance, return the intervening segment(s).

`start` and `end` are clamped to legal values (0..[length]) Begin the segment with a moveTo if `startWithMoveTo` is true.

### toString()

```dart
String toString()
```

# BlurStyle

```dart
enum BlurStyle {}
```

Styles to use for blurs in [MaskFilter] objects.

Fuzzy inside and outside. This is useful for painting shadows that are offset from the shape that ostensibly is casting the shadow.

Solid inside, fuzzy outside. This corresponds to drawing the shape, and additionally drawing the blur. This can make objects appear brighter, maybe even as if they were fluorescent.

Nothing inside, fuzzy outside. This is useful for painting shadows for partially transparent shapes, when they are painted separately but without an offset, so that the shadow doesn't paint below the shape.

Fuzzy inside, nothing outside. This can make shapes appear to be lit from within.

# MaskFilter

```dart
class MaskFilter {}
```

A mask filter to apply to shapes as they are painted. A mask filter is a function that takes a bitmap of color pixels, and returns another bitmap of color pixels.

Instances of this class are used with [Paint.maskFilter] on [Paint] objects.

### MaskFilter.blur()

```dart
MaskFilter.blur(BlurStyle _style, double _sigma)
```

Creates a mask filter that takes the shape being drawn and blurs it.

This is commonly used to approximate shadows.

The `style` argument controls the kind of effect to draw; see [BlurStyle].

The `sigma` argument controls the size of the effect. It is the standard deviation of the Gaussian blur to apply. The value must be greater than zero. The sigma corresponds to very roughly half the radius of the effect in pixels.

A blur is an expensive operation and should therefore be used sparingly.

The arguments must not be null.

See also:

- [Canvas.drawShadow], which is a more efficient way to draw shadows.

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

# ColorFilter

```dart
class ColorFilter implements ImageFilter {}
```

A description of a color filter to apply when drawing a shape or compositing a layer with a particular [Paint]. A color filter is a function that takes two colors, and outputs one color. When applied during compositing, it is independently applied to each pixel of the layer being drawn before the entire layer is merged with the destination.

Instances of this class are used with [Paint.colorFilter] on [Paint] objects.

### ColorFilter.mode()

```dart
ColorFilter.mode(Color color, BlendMode blendMode)
```

Creates a color filter that applies the blend mode given as the second argument. The source color is the one given as the first argument, and the destination color is the one from the layer being composited.

The output of this filter is then composited into the background according to the [Paint.blendMode], using the output of this filter as the source and the background as the destination.

### ColorFilter.matrix()

```dart
ColorFilter.matrix(List<double> matrix)
```

Construct a color filter from a 4x5 row-major matrix. The matrix is interpreted as a 5x5 matrix, where the fifth row is the identity configuration.

Every pixel's color value, represented as an `[R, G, B, A]`, is matrix multiplied to create a new color:

| R' | | a00 a01 a02 a03 a04 | | R | | G' | | a10 a11 a12 a13 a14 | | G | | B' | = | a20 a21 a22 a23 a24 | \* | B | | A' | | a30 a31 a32 a33 a34 | | A | | 1 | | 0 0 0 0 1 | | 1 |

The matrix is in row-major order and the translation column is specified in unnormalized, 0...255, space. For example, the identity matrix is:

```dart
const ColorFilter identity = ColorFilter.matrix(<double>[
  1, 0, 0, 0, 0,
  0, 1, 0, 0, 0,
  0, 0, 1, 0, 0,
  0, 0, 0, 1, 0,
]);
```

## Examples

An inversion color matrix:

```dart
const ColorFilter invert = ColorFilter.matrix(<double>[
  -1,  0,  0, 0, 255,
   0, -1,  0, 0, 255,
   0,  0, -1, 0, 255,
   0,  0,  0, 1,   0,
]);
```

A sepia-toned color matrix (values based on the [Filter Effects Spec](https://www.w3.org/TR/filter-effects-1/#sepiaEquivalent)):

```dart
const ColorFilter sepia = ColorFilter.matrix(<double>[
  0.393, 0.769, 0.189, 0, 0,
  0.349, 0.686, 0.168, 0, 0,
  0.272, 0.534, 0.131, 0, 0,
  0,     0,     0,     1, 0,
]);
```

A greyscale color filter (values based on the [Filter Effects Spec](https://www.w3.org/TR/filter-effects-1/#grayscaleEquivalent)):

```dart
const ColorFilter greyscale = ColorFilter.matrix(<double>[
  0.2126, 0.7152, 0.0722, 0, 0,
  0.2126, 0.7152, 0.0722, 0, 0,
  0.2126, 0.7152, 0.0722, 0, 0,
  0,      0,      0,      1, 0,
]);
```

### ColorFilter.linearToSrgbGamma()

```dart
ColorFilter.linearToSrgbGamma()
```

Construct a color filter that applies the sRGB gamma curve to the RGB channels.

### ColorFilter.srgbToLinearGamma()

```dart
ColorFilter.srgbToLinearGamma()
```

Creates a color filter that applies the inverse of the sRGB gamma curve to the RGB channels.

### ColorFilter.saturation()

```dart
ColorFilter.saturation(double saturation)
```

Creates a color filter that applies the given saturation to the RGB channels.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugShortDescription

```dart
String get debugShortDescription
```

### toString()

```dart
String toString()
```

# ImageFilter

```dart
abstract class ImageFilter {}
```

A filter operation to apply to a raster image.

See also:

- [BackdropFilter], a widget that applies [ImageFilter] to its rendering.
- [ClipRect], a widget that limits the area affected by the [ImageFilter] when used with [BackdropFilter].
- [ImageFiltered], a widget that applies [ImageFilter] to its children.
- [SceneBuilder.pushBackdropFilter], which is the low-level API for using this class as a backdrop filter.
- [SceneBuilder.pushImageFilter], which is the low-level API for using this class as a child layer filter.

### ImageFilter.blur()

```dart
ImageFilter.blur({double sigmaX = 0.0, double sigmaY = 0.0, TileMode? tileMode, Rect? bounds})
```

Creates an image filter that applies a Gaussian blur.

The `sigma_x` and `sigma_y` are the standard deviation of the Gaussian kernel in the X direction and the Y direction, respectively.

The `tile_mode` defines the behavior of sampling pixels at the edges when performing a standard, unbounded blur.

The `bounds` argument is optional and enables "bounded blur" mode. When `bounds` is non-null, the image filter substitutes transparent black for any sample it reads from outside the defined bounding rectangle. The final weighted sum is then divided by the total weight of the non-transparent samples (the effective alpha), resulting in opaque output.

The bounded mode prevents color bleeding from content adjacent to the bounds into the blurred area, and is typically used when the blur must be strictly contained within a clipped region, such as for iOS-style frosted glass effects.

The `bounds` rectangle is specified in the canvas's current coordinate space and is affected by the current transform; consequently, the bounds may not be axis-aligned in the final canvas coordinates.

### ImageFilter.dilate()

```dart
ImageFilter.dilate({double radiusX = 0.0, double radiusY = 0.0})
```

Creates an image filter that dilates each input pixel's channel values to the max value within the given radii along the x and y axes.

### ImageFilter.erode()

```dart
ImageFilter.erode({double radiusX = 0.0, double radiusY = 0.0})
```

Create a filter that erodes each input pixel's channel values to the minimum channel value within the given radii along the x and y axes.

### ImageFilter.matrix()

```dart
ImageFilter.matrix(Float64List matrix4, {FilterQuality filterQuality = FilterQuality.medium})
```

Creates an image filter that applies a matrix transformation.

For example, applying a positive scale matrix (see [Matrix4.diagonal3]) when used with [BackdropFilter] would magnify the background image.

### ImageFilter.compose()

```dart
ImageFilter.compose({required ImageFilter outer, required ImageFilter inner})
```

Composes the `inner` filter with `outer`, to combine their effects.

Creates a single [ImageFilter] that when applied, has the same effect as subsequently applying `inner` and `outer`, i.e., result = outer(inner(source)).

### ImageFilter.shader()

```dart
ImageFilter.shader(FragmentShader shader)
```

Creates an image filter from a [FragmentShader].

> [!WARNING]
> This API is only supported when using the Impeller rendering engine.
> On other backends, an [UnsupportedError] will be thrown.

> To check at runtime whether this API is supported, use [isShaderFilterSupported].

Example usage:

```dart
if (ui.ImageFilter.isShaderFilterSupported) {
  // Use the filter...
}
```

The fragment shader provided here has additional requirements to be used by the engine for filtering. The first uniform value must be a vec2, this will be set by the engine to the size of the bound texture. There must also be at least one sampler2D uniform, the first of which will be set by the engine to contain the filter input.

When Impeller uses the OpenGL(ES) backend, the y-axis direction is reversed. Custom fragment shaders must invert the y-axis on GLES or they will render upside-down.

For example, the following is a valid fragment shader that can be used with this API. Note that the uniform names are not required to have any particular value.

```glsl
#include <flutter/runtime_effect.glsl>

uniform vec2 u_size;
uniform float u_time;

uniform sampler2D u_texture_input;

out vec4 frag_color;

void main() {
  vec2 uv = FlutterFragCoord().xy / u_size;
// Reverse y axis for OpenGL backend.
#ifdef IMPELLER_TARGET_OPENGLES
  uv.y = 1.0 - uv.y
#endif
  frag_color = texture(u_texture_input, uv) * u_time;

}

```

### isShaderFilterSupported

```dart
bool get isShaderFilterSupported
```

Whether [ImageFilter.shader] is supported on the current backend.

> [!WARNING]
> This property will only return true when the Impeller rendering engine is enabled.
> Attempting to create an [ImageFilter.shader] when this property is `false` will throw an [UnsupportedError].

### debugShortDescription

```dart
String get debugShortDescription
```

The description text to show when the filter is part of a composite [ImageFilter] created using [ImageFilter.compose].

# Shader

```dart
base class Shader extends NativeFieldWrapperClass1 {}
```

Base class for objects such as [Gradient] and [ImageShader] which correspond to shaders as used by [Paint.shader].

### debugDisposed

```dart
bool get debugDisposed
```

Whether [dispose] has been called.

This must only be used when asserts are enabled. Otherwise, it will throw.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

The underlying memory allocated by this object will be retained beyond this call if it is still needed by another object that has not been disposed. For example, a [Picture] that has not been disposed that refers to an [ImageShader] may keep its underlying resources alive.

Classes that override this method must call `super.dispose()`.

# TileMode

```dart
enum TileMode {}
```

Defines how to handle areas outside the defined bounds of a gradient or image filter.

## For Gradients

Gradients are defined with some specific bounds creating an inner area and an outer area, and `TileMode` controls how colors are determined for areas outside these bounds:

- **Linear gradients**: The inner area is the area between two points (typically referred to as `start` and `end` in the gradient API), or more precisely, it's the area between the parallel lines that are orthogonal to the line drawn between the two points. Colors outside this area are determined by the `TileMode`.

- **Radial gradients**: The inner area is the disc defined by a center and radius. Colors outside this disc are determined by the `TileMode`.

- **Sweep gradients**: The inner area is the angular sector between `startAngle` and `endAngle`. Colors outside this sector are determined by the `TileMode`.

## For Image Filters

When applying filters (like blur) that sample colors from outside an image's bounds, `TileMode` defines how those out-of-bounds samples are determined:

- It controls what color values are used when the filter needs to sample from areas outside the original image.
- This is particularly important for effects like blurring near image edges.

See also:

- [painting.Gradient], the superclass for [LinearGradient] and [RadialGradient], as used by [BoxDecoration] et al, which works in relative coordinates and can create a [Shader] representing the gradient for a particular [Rect] on demand.
- [dart:ui.Gradient], the low-level class used when dealing with the [Paint.shader] property directly, with its [Gradient.linear] and [Gradient.radial] constructors.
- [dart:ui.ImageFilter.blur], an ImageFilter that may sometimes need to read samples from outside an image to combine with the pixels near the edge of the image.

Samples beyond the edge are clamped to the nearest color in the defined inner area.

For gradients, this means the region outside the inner area is painted with the color at the end of the color stop list closest to that region.

For sweep gradients specifically, the entire area outside the angular sector defined by [startAngle] and [endAngle] will be painted with the color at the end of the color stop list closest to that region.

An image filter will substitute the nearest edge pixel for any samples taken from outside its source image.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_sweep.png)

Samples beyond the edge are repeated from the far end of the defined area.

For a gradient, this technique is as if the stop points from 0.0 to 1.0 were then repeated from 1.0 to 2.0, 2.0 to 3.0, and so forth (and for linear gradients, similarly from -1.0 to 0.0, -2.0 to -1.0, etc).

For sweep gradients, the gradient pattern is repeated in the same direction (clockwise) for angles beyond [endAngle] and before [startAngle].

An image filter will treat its source image as if it were tiled across the enlarged sample space from which it reads, each tile in the same orientation as the base image.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_sweep.png)

Samples beyond the edge are mirrored back and forth across the defined area.

For a gradient, this technique is as if the stop points from 0.0 to 1.0 were then repeated backwards from 2.0 to 1.0, then forwards from 2.0 to 3.0, then backwards again from 4.0 to 3.0, and so forth (and for linear gradients, similarly in the negative direction).

For sweep gradients, the gradient pattern is mirrored back and forth as the angle increases beyond [endAngle] or decreases below [startAngle].

An image filter will treat its source image as tiled in an alternating forwards and backwards or upwards and downwards direction across the sample space from which it is reading.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_sweep.png)

Samples beyond the edge are treated as transparent black.

A gradient will render transparency over any region that is outside the circle of a radial gradient, outside the parallel lines that define the inner area of a linear gradient, or outside the angular sector of a sweep gradient.

For sweep gradients, only the sector between [startAngle] and [endAngle] will be painted; all other areas will be transparent.

An image filter will substitute transparent black for any sample it must read from outside its source image.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_sweep.png)

# Gradient

```dart
base class Gradient extends Shader {}
```

A shader (as used by [Paint.shader]) that renders a color gradient.

There are several types of gradients, represented by the various constructors on this class.

See also:

- [Gradient](https://api.flutter.dev/flutter/painting/Gradient-class.html), the class in the [painting] library.

### Gradient.linear()

```dart
Gradient.linear(Offset from, Offset to, List<Color> colors, [List<double>? colorStops, TileMode tileMode = TileMode.clamp, Float64List? matrix4])
```

Creates a linear gradient from `from` to `to`.

If `colorStops` is provided, `colorStops[i]` is a number from 0.0 to 1.0 that specifies where `color[i]` begins in the gradient. If `colorStops` is not provided, then only two stops, at 0.0 and 1.0, are implied (and `color` must therefore only have two entries). Stop values less than 0.0 will be rounded up to 0.0 and stop values greater than 1.0 will be rounded down to 1.0. Each stop value must be greater than or equal to the previous stop value. Stop values that do not meet this criteria will be rounded up to the previous stop value.

The behavior before `from` and after `to` is described by the `tileMode` argument. For details, see the [TileMode] enum.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_linear.png)

If `from`, `to`, `colors`, or `tileMode` are null, or if `colors` or `colorStops` contain null values, this constructor will throw a [NoSuchMethodError].

If `matrix4` is provided, the gradient fill will be transformed by the specified 4x4 matrix relative to the local coordinate system. `matrix4` must be a column-major matrix packed into a list of 16 values.

### Gradient.radial()

```dart
Gradient.radial(Offset center, double radius, List<Color> colors, [List<double>? colorStops, TileMode tileMode = TileMode.clamp, Float64List? matrix4, Offset? focal, double focalRadius = 0.0])
```

Creates a radial gradient centered at `center` that ends at `radius` distance from the center.

If `colorStops` is provided, `colorStops[i]` is a number from 0.0 to 1.0 that specifies where `color[i]` begins in the gradient. If `colorStops` is not provided, then only two stops, at 0.0 and 1.0, are implied (and `color` must therefore only have two entries). Stop values less than 0.0 will be rounded up to 0.0 and stop values greater than 1.0 will be rounded down to 1.0. Each stop value must be greater than or equal to the previous stop value. Stop values that do not meet this criteria will be rounded up to the previous stop value.

The behavior before and after the radius is described by the `tileMode` argument. For details, see the [TileMode] enum.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_radial.png)

If `center`, `radius`, `colors`, or `tileMode` are null, or if `colors` or `colorStops` contain null values, this constructor will throw a [NoSuchMethodError].

If `matrix4` is provided, the gradient fill will be transformed by the specified 4x4 matrix relative to the local coordinate system. `matrix4` must be a column-major matrix packed into a list of 16 values.

If `focal` is provided and not equal to `center` and `focalRadius` is provided and not equal to 0.0, the generated shader will be a two point conical radial gradient, with `focal` being the center of the focal circle and `focalRadius` being the radius of that circle. If `focal` is provided and not equal to `center`, at least one of the two offsets must not be equal to [Offset.zero].

### Gradient.sweep()

```dart
Gradient.sweep(Offset center, List<Color> colors, [List<double>? colorStops, TileMode tileMode = TileMode.clamp, double startAngle = 0.0, double endAngle = math.pi * 2, Float64List? matrix4])
```

Creates a sweep gradient centered at `center` that starts at `startAngle` and ends at `endAngle`.

`startAngle` and `endAngle` should be provided in radians, with zero radians being the horizontal line to the right of the `center` and with positive angles going clockwise around the `center`.

If `colorStops` is provided, `colorStops[i]` is a number from 0.0 to 1.0 that specifies where `colors[i]` begins in the gradient. If `colorStops` is not provided, then only two stops, at 0.0 and 1.0, are implied (and `colors` must therefore only have two entries). Stop values less than 0.0 will be rounded up to 0.0 and stop values greater than 1.0 will be rounded down to 1.0. Each stop value must be greater than or equal to the previous stop value. Stop values that do not meet this criteria will be rounded up to the previous stop value.

The `startAngle` and `endAngle` parameters define the angular sector to be painted. Angles are measured in radians clockwise from the positive x-axis. Values outside the range `[0, 2π]` are normalized to this range using modulo arithmetic. The gradient is only painted in the sector between `startAngle` and `endAngle`. The `tileMode` determines how the gradient behaves outside this sector.

The `tileMode` argument specifies how the gradient should handle areas outside the angular sector defined by `startAngle` and `endAngle`:

The behavior before `startAngle` and after `endAngle` is described by the `tileMode` argument. For details, see the [TileMode] enum.

- [TileMode.clamp]: The edge colors are extended to infinity.
- [TileMode.mirror]: The gradient is repeated, alternating direction each time.
- [TileMode.repeated]: The gradient is repeated in the same direction.
- [TileMode.decal]: Only the colors within the gradient's angular sector are drawn, with transparent black elsewhere.

The [colorStops] argument must have the same number of values as [colors], if specified. It specifies the position of each color stop between 0.0 and 1.0. If it is null, a uniform distribution is assumed. The stop values must be in ascending order. A stop value of 0.0 corresponds to [startAngle], and a stop value of 1.0 corresponds to [endAngle].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_sweep.png)

If `center`, `colors`, `tileMode`, `startAngle`, or `endAngle` are null, or if `colors` or `colorStops` contain null values, this constructor will throw a [NoSuchMethodError].

If `matrix4` is provided, the gradient fill will be transformed by the specified 4x4 matrix relative to the local coordinate system. `matrix4` must be a column-major matrix packed into a list of 16 values.

# ImageShader

```dart
base class ImageShader extends Shader {}
```

A shader (as used by [Paint.shader]) that tiles an image.

### ImageShader()

```dart
ImageShader(Image image, TileMode tmx, TileMode tmy, Float64List matrix4, {FilterQuality? filterQuality})
```

Creates an image-tiling shader.

The first argument specifies the image to render. The [decodeImageFromList] function can be used to decode an image from bytes into the form expected here. (In production code, starting from [instantiateImageCodec] may be preferable.)

The second and third arguments specify the [TileMode] for the x direction and y direction respectively. [TileMode.repeated] can be used for tiling images.

The fourth argument gives the matrix to apply to the effect. The expression `Matrix4.identity().storage` creates a [Float64List] prepopulated with the identity matrix.

All the arguments are required and must not be null, except for [filterQuality]. If [filterQuality] is not specified at construction time it will be deduced from the environment where it is used, such as from [Paint.filterQuality].

### dispose()

```dart
void dispose()
```

# FragmentProgram

```dart
base class FragmentProgram extends NativeFieldWrapperClass1 {}
```

An instance of [FragmentProgram] creates [Shader] objects (as used by [Paint.shader]).

For more information, see the website [documentation](https://docs.flutter.dev/development/ui/advanced/shaders).

### fromAsset()

```dart
Future<FragmentProgram> fromAsset(String assetKey)
```

Creates a fragment program from the asset with key [assetKey].

The asset must be a file produced as the output of the `impellerc` compiler. The constructed object should then be reused via the [fragmentShader] method to create [Shader] objects that can be used by [Paint.shader].

### fragmentShader()

```dart
FragmentShader fragmentShader()
```

Returns a fresh instance of [FragmentShader].

# UniformType

```dart
sealed class UniformType {}
```

A binding into a uniform defined in a shader. Used now to restrict the types of UniformArrays that can be created.

# UniformFloatSlot

```dart
base class UniformFloatSlot extends UniformType {}
```

A binding to a uniform of type float. Calling [set] on this object updates a float uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uColor', 0).set(1.0);
  shader.getUniformFloat('uColor', 1).set(0.0);
  shader.getUniformFloat('uColor', 2).set(0.0);
}
```

See also: [FragmentShader.getUniformFloat] - How [UniformFloatSlot] instances are acquired.

### set()

```dart
void set(double val)
```

Set the float value of the bound uniform.

### shaderIndex

```dart
int get shaderIndex
```

VisibleForTesting: This is the index one would use with [FragmentShader.setFloat] for this uniform.

### name

```dart
String name
```

The name of the bound uniform.

### index

```dart
int index
```

The offset into the bound uniform. For example, 1 for `.y` or 2 for `.b`.

# UniformVec2Slot

```dart
base class UniformVec2Slot extends UniformType {}
```

A binding to a uniform of type vec2. Calling [set] on this object updates the uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformVec2('uSize').set(100, 100);
}
```

See also: [FragmentShader.getUniformVec2] - How [UniformVec2Slot] instances are acquired.

### set()

```dart
void set(double x, double y)
```

Set the float value of the bound uniform.

# UniformVec3Slot

```dart
base class UniformVec3Slot extends UniformType {}
```

A binding to a uniform of type vec3. Calling [set] on this object updates the uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader, double time) {
  shader.getUniformVec3('uScaledTime').set(time, time*0.1, time*0.01);
}
```

See also: [FragmentShader.getUniformVec3] - How [UniformVec3Slot] instances are acquired.

### set()

```dart
void set(double x, double y, double z)
```

Set the float value of the bound uniform.

# UniformVec4Slot

```dart
base class UniformVec4Slot extends UniformType {}
```

A binding to a uniform of type vec4. Calling [set] on this object updates the uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformVec4('uColor').set(1.0, 0.0, 1.0, 1.0);
}
```

See also: [FragmentShader.getUniformVec4] - How [UniformVec4Slot] instances are acquired.

### set()

```dart
void set(double x, double y, double z, double w)
```

Set the float value of the bound uniform.

# UniformMat2Slot

```dart
base class UniformMat2Slot extends UniformType {}
```

A binding to a uniform of type mat2. Calling [set] on this object updates the uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat2('uIdentity').set(
    1.0, 0.0,
    0.0, 1.0
  );
}
```

See also: [FragmentShader.getUniformMat2] - How [UniformMat2Slot] instances are acquired.

### set()

```dart
void set(double m00, double m01, double m10, double m11)
```

Set the float value of the matrix in row-major order.

# UniformMat3Slot

```dart
base class UniformMat3Slot extends UniformType {}
```

A binding to a uniform of type mat3. Calling [set] on this object updates the uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat3('uIdentity').set(
    1.0, 0.0, 0.0,
    0.0, 1.0, 0.0,
    0.0, 0.0, 1.0
  );
}
```

See also: [FragmentShader.getUniformMat3] - How [UniformMat3Slot] instances are acquired.

### set()

```dart
void set(double m00, double m01, double m02, double m10, double m11, double m12, double m20, double m21, double m22)
```

Set the float value of the matrix in row-major order.

# UniformMat4Slot

```dart
base class UniformMat4Slot extends UniformType {}
```

A binding to a uniform of type mat4. Calling [set] on this object updates the uniform's value.

Example:

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat4('uIdentity').set(
    1.0, 0.0, 0.0, 0.0,
    0.0, 1.0, 0.0, 0.0,
    0.0, 0.0, 1.0, 0.0,
    0.0, 0.0, 0.0, 1.0
  );
}
```

See also: [FragmentShader.getUniformMat4] - How [UniformMat4Slot] instances are acquired.

### set()

```dart
void set(double m00, double m01, double m02, double m03, double m10, double m11, double m12, double m13, double m20, double m21, double m22, double m23, double m30, double m31, double m32, double m33)
```

Set the float value of the matrix in row-major order.

# UniformArray

```dart
class UniformArray<T extends UniformType> {}
```

An array of bindings to uniforms of the same type T. Access elements via [] and set them individually. Example:

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec4Slot> colors = shader.getUniformVec4Array('uColorArray');
  colors[0].set(1.0, 0.0, 1.0, 0.3);
}
```

See also: [FragmentShader.getUniformFloatArray] - How [UniformArray<Float>] instances are acquired.

### operator []()

```dart
T operator [](int index)
```

Access an element of the UniformArray.

### length

```dart
int get length
```

The number of Uniforms in the UniformArray.

# ImageSamplerSlot

```dart
base class ImageSamplerSlot {}
```

A binding to a shader's image sampler. Calling [set] on this object updates a sampler's bound image.

### set()

```dart
void set(Image val)
```

Set the [Image] value for the bound sampler associated with this slot.

### shaderIndex

```dart
int get shaderIndex
```

VisibleForTesting: This is the index one would use with [FragmentShader.setImageSampler] for this sampler.

### name

```dart
String name
```

The name of the bound uniform.

# FragmentShader

```dart
base class FragmentShader extends Shader {}
```

A [Shader] generated from a [FragmentProgram].

Instances of this class can be obtained from the [FragmentProgram.fragmentShader] method. The float uniforms list is initialized to the size expected by the shader and is zero-filled. Uniforms of float type can then be set by calling [setFloat]. Sampler uniforms are set by calling [setImageSampler].

A [FragmentShader] can be re-used, and this is an efficient way to avoid allocating and re-initializing the uniform buffer and samplers. However, if two [FragmentShader] objects with different float uniforms or samplers are required to exist simultaneously, they must be obtained from two different calls to [FragmentProgram.fragmentShader].

### setFloat()

```dart
void setFloat(int index, double value)
```

Sets the float uniform at [index] to [value].

All uniforms defined in a fragment shader that are not samplers must be set through this method. This includes floats and vec2, vec3, and vec4. The correct index for each uniform is determined by the order of the uniforms as defined in the fragment program, ignoring any samplers. For data types that are composed of multiple floats such as a vec4, more than one call to [setFloat] is required.

For example, given the following uniforms in a fragment program:

```glsl
uniform float uScale;
uniform sampler2D uTexture;
uniform vec2 uMagnitude;
uniform vec4 uColor;
```

Then the corresponding Dart code to correctly initialize these uniforms is:

```dart
void updateShader(ui.FragmentShader shader, Color color, ui.Image image) {
  shader.setFloat(0, 23);  // uScale
  shader.setFloat(1, 114); // uMagnitude x
  shader.setFloat(2, 83);  // uMagnitude y

  // Convert color to premultiplied opacity.
  shader.setFloat(3, color.r * color.a); // uColor r
  shader.setFloat(4, color.g * color.a); // uColor g
  shader.setFloat(5, color.b * color.a); // uColor b
  shader.setFloat(6, color.a);           // uColor a

  // initialize sampler uniform.
  shader.setImageSampler(0, image);
}
```

Note how the indexes used does not count the `sampler2D` uniform. This uniform will be set separately with [setImageSampler], with the index starting over at 0.

Any float uniforms that are left uninitialized will default to `0`.

### getUniformFloat()

```dart
UniformFloatSlot getUniformFloat(String name, [int? index])
```

Access the float binding for uniform named [name] with optional offset [index]. Example [index] values: 1 for 'foo.y', 2 for 'foo.b'.

Example:

```glsl
uniform float uScale;
uniform sampler2D uTexture;
uniform vec2 uMagnitude;
uniform vec4 uColor;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformFloat('uMagnitude', 0);
  shader.getUniformFloat('uMagnitude', 1);
  shader.getUniformFloat('uColor', 0);
  shader.getUniformFloat('uColor', 1);
  shader.getUniformFloat('uColor', 2);
  shader.getUniformFloat('uColor', 3);
}
```

### getUniformVec2()

```dart
UniformVec2Slot getUniformVec2(String name)
```

Access the float binding for a vec2 uniform named [name].

Example:

```glsl
uniform float uScale;
uniform vec2 uMagnitude;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformVec2('uMagnitude');
}
```

### getUniformVec3()

```dart
UniformVec3Slot getUniformVec3(String name)
```

Access the float binding for a vec3 uniform named [name].

Example:

```glsl
uniform float uScale;
uniform vec3 uScaledTime;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformVec3('uScaledTime');
}
```

### getUniformVec4()

```dart
UniformVec4Slot getUniformVec4(String name)
```

Access the float binding for a vec4 uniform named [name].

Example:

```glsl
uniform float uScale;
uniform vec4 uColor;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformVec4('uColor');
}
```

### getUniformMat2()

```dart
UniformMat2Slot getUniformMat2(String name)
```

Access the float binding for a mat2 uniform named [name].

Example:

```glsl
uniform mat2 uIdentity;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat2('uIdentity');
}
```

### getUniformMat3()

```dart
UniformMat3Slot getUniformMat3(String name)
```

Access the float binding for a mat3 uniform named [name].

Example:

```glsl
uniform mat3 uIdentity;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat3('uIdentity');
}
```

### getUniformMat4()

```dart
UniformMat4Slot getUniformMat4(String name)
```

Access the float binding for a mat4 uniform named [name].

Example:

```glsl
uniform mat4 uIdentity;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat4('uIdentity');
}
```

### getUniformFloatArray()

```dart
UniformArray<UniformFloatSlot> getUniformFloatArray(String name)
```

Access the binding for a float[] uniform named [name].

Example:

```glsl
uniform float[10] uValues;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformFloatSlot> values = shader.getUniformFloatArray('uValues');
  values[2].set(1.0);
}
```

### getUniformVec2Array()

```dart
UniformArray<UniformVec2Slot> getUniformVec2Array(String name)
```

Access the binding for a vec2[] uniform named [name].

Example:

```glsl
uniform vec2[10] uPositions;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec2Slot> positions = shader.getUniformVec2Array('uPositions');
  positions[2].set(6.0, 7.0);
}
```

### getUniformVec3Array()

```dart
UniformArray<UniformVec3Slot> getUniformVec3Array(String name)
```

Access the binding for a vec3[] uniform named [name].

Example:

```glsl
uniform vec3[10] uColors;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec3Slot> colors = shader.getUniformVec3Array('uColors');
  colors[0].set(1.0, 0.0, 1.0);
}
```

### getUniformVec4Array()

```dart
UniformArray<UniformVec4Slot> getUniformVec4Array(String name)
```

Access the binding for a vec4[] uniform named [name].

Example:

```glsl
uniform vec4[10] uColors;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec4Slot> colors = shader.getUniformVec4Array('uColors');
  colors[0].set(1.0, 0.0, 1.0, 0.5);
}
```

### getUniformMat2Array()

```dart
UniformArray<UniformMat2Slot> getUniformMat2Array(String name)
```

Access the binding for a mat2[] uniform named [name].

Example:

```glsl
uniform mat2[10] uMatricies;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformMat2Slot> mats = shader.getUniformMat2Array('uMatricies');
  mats[0].set(
    1.0, 0.0,
    1.0, 0.5
  );
}
```

### getUniformMat3Array()

```dart
UniformArray<UniformMat3Slot> getUniformMat3Array(String name)
```

Access the binding for a mat3[] uniform named [name].

Example:

```glsl
uniform mat3[10] uMatricies;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformMat3Slot> mats = shader.getUniformMat3Array('uMatricies');
  mats[0].set(
    1.0, 0.0, 0.0,
    1.0, 0.5, 0.0,
    1.0, 0.3, 1.2
  );
}
```

### getUniformMat4Array()

```dart
UniformArray<UniformMat4Slot> getUniformMat4Array(String name)
```

Access the binding for a mat4[] uniform named [name].

Example:

```glsl
uniform mat4[10] uMatricies;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformMat4Slot> mats = shader.getUniformMat4Array('uMatricies');
  mats[0].set(
    1.0, 0.0, 0.0, 1.0,
    1.0, 0.5, 0.0, 0.4,
    1.0, 0.3, 1.2, 0.2,
    0.0, 0.0, 1.0, 0.3,
  );
}
```

### getImageSampler()

```dart
ImageSamplerSlot getImageSampler(String name)
```

Access the [ImageSamplerSlot] binding associated with the sampler named [name].

The index provided to setImageSampler is the index of the sampler uniform defined in the fragment program, excluding all non-sampler uniforms.

### setImageSampler()

```dart
void setImageSampler(int index, Image image, {FilterQuality filterQuality = FilterQuality.none})
```

Sets the sampler uniform at [index] to [image].

The index provided to setImageSampler is the index of the sampler uniform defined in the fragment program, excluding all non-sampler uniforms.

The optional [filterQuality] argument may be provided to set the quality level used to sample the image. By default, it is set to [FilterQuality.none].

All the sampler uniforms that a shader expects must be provided or the results will be undefined.

### dispose()

```dart
void dispose()
```

Releases the native resources held by the [FragmentShader].

After this method is called, calling methods on the shader, or attaching it to a [Paint] object will fail with an exception. Calling [dispose] twice will also result in an exception being thrown.

# VertexMode

```dart
enum VertexMode {}
```

Defines how a list of points is interpreted when drawing a set of triangles.

Used by [Canvas.drawVertices].

Draw each sequence of three points as the vertices of a triangle.

Draw each sliding window of three points as the vertices of a triangle.

Draw the first point and each sliding window of two points as the vertices of a triangle.

This mode is not natively supported by most backends, and is instead implemented by unrolling the points into the equivalent [VertexMode.triangles], which is generally more efficient.

# Vertices

```dart
base class Vertices extends NativeFieldWrapperClass1 {}
```

A set of vertex data used by [Canvas.drawVertices].

Vertex data consists of a series of points in the canvas coordinate space. Based on the [VertexMode], these points are interpreted either as independent triangles ([VertexMode.triangles]), as a sliding window of points forming a chain of triangles each sharing one side with the next ([VertexMode.triangleStrip]), or as a fan of triangles with a single shared point ([VertexMode.triangleFan]).

Each point can be associated with a color. Each triangle is painted as a gradient that blends between the three colors at the three points of that triangle. If no colors are specified, transparent black is assumed for all the points.

These colors are then blended with the [Paint] specified in the call to [Canvas.drawVertices]. This paint is either a solid color ([Paint.color]), or a bitmap, specified using a shader ([Paint.shader]), typically either a gradient ([Gradient]) or image ([ImageFilter]). The bitmap uses the same coordinate space as the canvas (in the case of an [ImageFilter], this is notably different than the coordinate space of the source image; the source image is tiled according to the filter's configuration, and the image that is sampled when painting the triangles is the infinite one after all the repeating is applied.)

Each point in the [Vertices] is associated with a specific point on this image. Each triangle is painted by sampling points from this image by interpolating between the three points of the image corresponding to the three points of the triangle.

The [Vertices.new] constructor configures all this using lists of [Offset] and [Color] objects. The [Vertices.raw] constructor instead uses [Float32List], [Int32List], and [Uint16List] objects, which more closely corresponds to the data format used internally and therefore reduces some of the conversion overhead. The raw constructor is useful if the data is coming from another source (e.g. a file) and can therefore be parsed directly into the underlying representation.

### Vertices()

```dart
Vertices(VertexMode mode, List<Offset> positions, {List<Color>? colors, List<Offset>? textureCoordinates, List<int>? indices})
```

Creates a set of vertex data for use with [Canvas.drawVertices].

The `mode` parameter describes how the points should be interpreted: as independent triangles ([VertexMode.triangles]), as a sliding window of points forming a chain of triangles each sharing one side with the next ([VertexMode.triangleStrip]), or as a fan of triangles with a single shared point ([VertexMode.triangleFan]).

The `positions` parameter provides the points in the canvas space that will be use to draw the triangles.

The `colors` parameter, if specified, provides the color for each point in `positions`. Each triangle is painted as a gradient that blends between the three colors at the three points of that triangle. (These colors are then blended with the [Paint] specified in the call to [Canvas.drawVertices].)

The `textureCoordinates` parameter, if specified, provides the points in the [Paint] image to sample for the corresponding points in `positions`.

If the `colors` or `textureCoordinates` parameters are specified, they must be the same length as `positions`.

The `indices` parameter specifies the order in which the points should be painted. If it is omitted (or present but empty), the points are processed in the order they are given in `positions`, as if the `indices` was a list from 0 to n-1, where _n_ is the number of entries in `positions`. The `indices` parameter, if present and non-empty, must have at least three entries, but may be of any length beyond this. Indicies may refer to offsets in the positions array multiple times, or may skip positions entirely.

If the `indices` parameter is specified, all values in the list must be valid index values for `positions`.

The `mode` and `positions` parameters must not be null.

This constructor converts its parameters into [dart:typed_data] lists (e.g. using [Float32List]s for the coordinates) before sending them to the Flutter engine. If the data provided to this constructor is not already in [List] form, consider using the [Vertices.raw] constructor instead to avoid converting the data twice.

### Vertices.raw()

```dart
Vertices.raw(VertexMode mode, Float32List positions, {Int32List? colors, Float32List? textureCoordinates, Uint16List? indices})
```

Creates a set of vertex data for use with [Canvas.drawVertices], using the encoding expected by the Flutter engine.

The `mode` parameter describes how the points should be interpreted: as independent triangles ([VertexMode.triangles]), as a sliding window of points forming a chain of triangles each sharing one side with the next ([VertexMode.triangleStrip]), or as a fan of triangles with a single shared point ([VertexMode.triangleFan]).

The `positions` parameter provides the points in the canvas space that will be use to draw the triangles. Each point is represented as two numbers in the list, the first giving the x coordinate and the second giving the y coordinate. (As a result, the list must have an even number of entries.)

The `colors` parameter, if specified, provides the color for each point in `positions`. Each color is represented as ARGB with 8 bit color channels (like [Color.value]'s internal representation), and the list, if specified, must therefore be half the length of `positions`. Each triangle is painted as a gradient that blends between the three colors at the three points of that triangle. (These colors are then blended with the [Paint] specified in the call to [Canvas.drawVertices].)

The `textureCoordinates` parameter, if specified, provides the points in the [Paint] image to sample for the corresponding points in `positions`. Each point is represented as two numbers in the list, the first giving the x coordinate and the second giving the y coordinate. This list, if specified, must be the same length as `positions`.

The `indices` parameter specifies the order in which the points should be painted. If it is omitted (or present but empty), the points are processed in the order they are given in `positions`, as if the `indices` was a list from 0 to n-2, where _n_ is the number of pairs in `positions` (i.e. half the length of `positions`). The `indices` parameter, if present and non-empty, must have at least three entries, but may be of any length beyond this. Indicies may refer to offsets in the positions array multiple times, or may skip positions entirely.

If the `indices` parameter is specified, all values in the list must be valid index values for pairs in `positions`. For example, if there are 12 numbers in `positions` (representing 6 coordinates), the `indicies` must be numbers in the range 0..5 inclusive.

The `mode` and `positions` parameters must not be null.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

### debugDisposed

```dart
bool get debugDisposed
```

Whether this reference to the underlying vertex data is [dispose]d.

This only returns a valid value if asserts are enabled, and must not be used otherwise.

# PointMode

```dart
enum PointMode {}
```

Defines how a list of points is interpreted when drawing a set of points.

Used by [Canvas.drawPoints] and [Canvas.drawRawPoints].

Draw each point separately.

If the [Paint.strokeCap] is [StrokeCap.round], then each point is drawn as a circle with the diameter of the [Paint.strokeWidth], filled as described by the [Paint] (ignoring [Paint.style]).

Otherwise, each point is drawn as an axis-aligned square with sides of length [Paint.strokeWidth], filled as described by the [Paint] (ignoring [Paint.style]).

Draw each sequence of two points as a line segment.

If the number of points is odd, then the last point is ignored.

The lines are stroked as described by the [Paint] (ignoring [Paint.style]).

Draw the entire sequence of points as one line.

The lines are stroked as described by the [Paint] (ignoring [Paint.style]).

# ClipOp

```dart
enum ClipOp {}
```

Defines how a new clip region should be merged with the existing clip region.

Used by [Canvas.clipRect].

Subtract the new region from the existing region.

Intersect the new region from the existing region.

# Canvas

```dart
abstract class Canvas {}
```

An interface for recording graphical operations.

[Canvas] objects are used in creating [Picture] objects, which can themselves be used with a [SceneBuilder] to build a [Scene]. In normal usage, however, this is all handled by the framework.

A canvas has a current transformation matrix which is applied to all operations. Initially, the transformation matrix is the identity transform. It can be modified using the [translate], [scale], [rotate], [skew], and [transform] methods.

A canvas also has a current clip region which is applied to all operations. Initially, the clip region is infinite. It can be modified using the [clipRect], [clipRRect], and [clipPath] methods.

The current transform and clip can be saved and restored using the stack managed by the [save], [saveLayer], and [restore] methods.

## Use with the Flutter framework

The Flutter framework's [RendererBinding] provides a hook for creating [Canvas] objects ([RendererBinding.createCanvas]) that allows tests to hook into the scene creation logic. When creating a [Canvas] that will be used with a [PictureLayer] as part of the [Scene] in the context of the Flutter framework, consider calling [RendererBinding.createCanvas] instead of calling the [Canvas.new] constructor directly.

This does not apply when using a canvas to generate a bitmap for other purposes, e.g. for generating a PNG image using [Picture.toImage].

### Canvas()

```dart
Canvas(PictureRecorder recorder, [Rect? cullRect])
```

Creates a canvas for recording graphical operations into the given picture recorder.

Graphical operations that affect pixels entirely outside the given `cullRect` might be discarded by the implementation. However, the implementation might draw outside these bounds if, for example, a command draws partially inside and outside the `cullRect`. To ensure that pixels outside a given region are discarded, consider using a [clipRect]. The `cullRect` is optional; by default, all operations are kept.

To end the recording, call [PictureRecorder.endRecording] on the given recorder.

### save()

```dart
void save()
```

Saves a copy of the current transform and clip on the save stack.

Call [restore] to pop the save stack.

See also:

- [saveLayer], which does the same thing but additionally also groups the commands done until the matching [restore].

### saveLayer()

```dart
void saveLayer(Rect? bounds, Paint paint)
```

Saves a copy of the current transform and clip on the save stack, and then creates a new group which subsequent calls will become a part of. When the save stack is later popped, the group will be flattened into a layer and have the given `paint`'s [Paint.colorFilter] and [Paint.blendMode] applied.

This lets you create composite effects, for example making a group of drawing commands semi-transparent. Without using [saveLayer], each part of the group would be painted individually, so where they overlap would be darker than where they do not. By using [saveLayer] to group them together, they can be drawn with an opaque color at first, and then the entire group can be made transparent using the [saveLayer]'s paint.

Call [restore] to pop the save stack and apply the paint to the group.

## Using saveLayer with clips

When a rectangular clip operation (from [clipRect]) is not axis-aligned with the raster buffer, or when the clip operation is not rectilinear (e.g. because it is a rounded rectangle clip created by [clipRRect] or an arbitrarily complicated path clip created by [clipPath]), the edge of the clip needs to be anti-aliased.

If two draw calls overlap at the edge of such a clipped region, without using [saveLayer], the first drawing will be anti-aliased with the background first, and then the second will be anti-aliased with the result of blending the first drawing and the background. On the other hand, if [saveLayer] is used immediately after establishing the clip, the second drawing will cover the first in the layer, and thus the second alone will be anti-aliased with the background when the layer is clipped and composited (when [restore] is called).

For example, this [CustomPainter.paint] method paints a clean white rounded rectangle:

```dart
void paint(Canvas canvas, Size size) {
  Rect rect = Offset.zero & size;
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(rect, 100.0, 100.0));
  canvas.saveLayer(rect, Paint());
  canvas.drawPaint(Paint()..color = Colors.red);
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
  canvas.restore();
}
```

On the other hand, this one renders a red outline, the result of the red paint being anti-aliased with the background at the clip edge, then the white paint being similarly anti-aliased with the background _including the clipped red paint_:

```dart
void paint(Canvas canvas, Size size) {
  // (this example renders poorly, prefer the example above)
  Rect rect = Offset.zero & size;
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(rect, 100.0, 100.0));
  canvas.drawPaint(Paint()..color = Colors.red);
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
}
```

This point is moot if the clip only clips one draw operation. For example, the following paint method paints a pair of clean white rounded rectangles, even though the clips are not done on a separate layer:

```dart
void paint(Canvas canvas, Size size) {
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(Offset.zero & (size / 2.0), 50.0, 50.0));
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(size.center(Offset.zero) & (size / 2.0), 50.0, 50.0));
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
}
```

(Incidentally, rather than using [clipRRect] and [drawPaint] to draw rounded rectangles like this, prefer the [drawRRect] method. These examples are using [drawPaint] as a proxy for "complicated draw operations that will get clipped", to illustrate the point.)

## Performance considerations

Generally speaking, [saveLayer] is relatively expensive.

There are a several different hardware architectures for GPUs (graphics processing units, the hardware that handles graphics), but most of them involve batching commands and reordering them for performance. When layers are used, they cause the rendering pipeline to have to switch render target (from one layer to another). Render target switches can flush the GPU's command buffer, which typically means that optimizations that one could get with larger batching are lost. Render target switches also generate a lot of memory churn because the GPU needs to copy out the current frame buffer contents from the part of memory that's optimized for writing, and then needs to copy it back in once the previous render target (layer) is restored.

See also:

- [save], which saves the current state, but does not create a new layer for subsequent commands.
- [BlendMode], which discusses the use of [Paint.blendMode] with [saveLayer].

### restore()

```dart
void restore()
```

Pops the current save stack, if there is anything to pop. Otherwise, does nothing.

Use [save] and [saveLayer] to push state onto the stack.

If the state was pushed with [saveLayer], then this call will also cause the new layer to be composited into the previous layer.

### restoreToCount()

```dart
void restoreToCount(int count)
```

Restores the save stack to a previous level as might be obtained from [getSaveCount]. If [count] is less than 1, the stack is restored to its initial state. If [count] is greater than the current [getSaveCount] then nothing happens.

Use [save] and [saveLayer] to push state onto the stack.

If any of the state stack levels restored by this call were pushed with [saveLayer], then this call will also cause those layers to be composited into their previous layers.

### getSaveCount()

```dart
int getSaveCount()
```

Returns the number of items on the save stack, including the initial state. This means it returns 1 for a clean canvas, and that each call to [save] and [saveLayer] increments it, and that each matching call to [restore] decrements it.

This number cannot go below 1.

### translate()

```dart
void translate(double dx, double dy)
```

Add a translation to the current transform, shifting the coordinate space horizontally by the first argument and vertically by the second argument.

### scale()

```dart
void scale(double sx, [double? sy])
```

Add an axis-aligned scale to the current transform, scaling by the first argument in the horizontal direction and the second in the vertical direction.

If [sy] is unspecified, [sx] will be used for the scale in both directions.

### rotate()

```dart
void rotate(double radians)
```

Add a rotation to the current transform. The argument is in radians clockwise.

### skew()

```dart
void skew(double sx, double sy)
```

Add an axis-aligned skew to the current transform, with the first argument being the horizontal skew in rise over run units clockwise around the origin, and the second argument being the vertical skew in rise over run units clockwise around the origin.

### transform()

```dart
void transform(Float64List matrix4)
```

Multiply the current transform by the specified 4⨉4 transformation matrix specified as a list of values in column-major order.

### getTransform()

```dart
Float64List getTransform()
```

Returns the current transform including the combined result of all transform methods executed since the creation of this [Canvas] object, and respecting the save/restore history.

Methods that can change the current transform include [translate], [scale], [rotate], [skew], and [transform]. The [restore] method can also modify the current transform by restoring it to the same value it had before its associated [save] or [saveLayer] call.

### clipRect()

```dart
void clipRect(Rect rect, {ClipOp clipOp = ClipOp.intersect, bool doAntiAlias = true})
```

Reduces the clip region to the intersection of the current clip and the given rectangle.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_rect.png)

If [doAntiAlias] is true, then the clip will be anti-aliased.

If multiple draw commands intersect with the clip boundary, this can result in incorrect blending at the clip boundary. See [saveLayer] for a discussion of how to address that.

Use [ClipOp.difference] to subtract the provided rectangle from the current clip.

### clipRRect()

```dart
void clipRRect(RRect rrect, {bool doAntiAlias = true})
```

Reduces the clip region to the intersection of the current clip and the given rounded rectangle.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_rrect.png)

If [doAntiAlias] is true, then the clip will be anti-aliased.

If multiple draw commands intersect with the clip boundary, this can result in incorrect blending at the clip boundary. See [saveLayer] for a discussion of how to address that and some examples of using [clipRRect].

### clipRSuperellipse()

```dart
void clipRSuperellipse(RSuperellipse rsuperellipse, {bool doAntiAlias = true})
```

Reduces the clip region to the intersection of the current clip and the given rounded superellipse.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_rsuperellipse.png)

If [doAntiAlias] is true, then the clip will be anti-aliased.

If multiple draw commands intersect with the clip boundary, this can result in incorrect blending at the clip boundary. See [saveLayer] for a discussion of how to address that and some examples of using [clipRSuperellipse].

### clipPath()

```dart
void clipPath(Path path, {bool doAntiAlias = true})
```

Reduces the clip region to the intersection of the current clip and the given [Path].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_path.png)

If [doAntiAlias] is true, then the clip will be anti-aliased.

If multiple draw commands intersect with the clip boundary, this can result in incorrect blending at the clip boundary. See [saveLayer] for a discussion of how to address that.

### getLocalClipBounds()

```dart
Rect getLocalClipBounds()
```

Returns the conservative bounds of the combined result of all clip methods executed within the current save stack of this [Canvas] object, as measured in the local coordinate space under which rendering operations are currently performed.

The combined clip results are rounded out to an integer pixel boundary before they are transformed back into the local coordinate space which accounts for the pixel roundoff in rendering operations, particularly when antialiasing. Because the [Picture] may eventually be rendered into a scene within the context of transforming widgets or layers, the result may thus be overly conservative due to premature rounding. Using the [getDestinationClipBounds] method combined with the external transforms and rounding in the true device coordinate system will produce more accurate results, but this value may provide a more convenient approximation to compare rendering operations to the established clip.

{@template dart.ui.canvas.conservativeClipBounds} The conservative estimate of the bounds is based on intersecting the bounds of each clip method that was executed with [ClipOp.intersect] and potentially ignoring any clip method that was executed with [ClipOp.difference]. The [ClipOp] argument is only present on the [clipRect] method.

To understand how the bounds estimate can be conservative, consider the following two clip method calls:

```dart
void draw(Canvas canvas) {
  canvas.clipPath(Path()
    ..addRect(const Rect.fromLTRB(10, 10, 20, 20))
    ..addRect(const Rect.fromLTRB(80, 80, 100, 100)));
  canvas.clipPath(Path()
    ..addRect(const Rect.fromLTRB(80, 10, 100, 20))
    ..addRect(const Rect.fromLTRB(10, 80, 20, 100)));
  // ...
}
```

After executing both of those calls there is no area left in which to draw because the two paths have no overlapping regions. But, in this case, [getLocalClipBounds] would return a rectangle from `10, 10` to `100, 100` because it only intersects the bounds of the two path objects to obtain its conservative estimate.

The clip bounds are not affected by the bounds of any enclosing [saveLayer] call as the engine does not currently guarantee the strict enforcement of those bounds during rendering.

Methods that can change the current clip include [clipRect], [clipRRect], and [clipPath]. The [restore] method can also modify the current clip by restoring it to the same value it had before its associated [save] or [saveLayer] call. {@endtemplate}

### getDestinationClipBounds()

```dart
Rect getDestinationClipBounds()
```

Returns the conservative bounds of the combined result of all clip methods executed within the current save stack of this [Canvas] object, as measured in the destination coordinate space in which the [Picture] will be rendered.

Unlike [getLocalClipBounds], the bounds are not rounded out to an integer pixel boundary as the Destination coordinate space may not represent pixels if the [Picture] being constructed will be further transformed when it is rendered or added to a scene. In order to determine the true pixels being affected, those external transforms should be applied first before rounding out the result to integer pixel boundaries. Most typically, [Picture] objects are rendered in a scene with a scale transform representing the Device Pixel Ratio.

{@macro dart.ui.canvas.conservativeClipBounds}

### drawColor()

```dart
void drawColor(Color color, BlendMode blendMode)
```

Paints the given [Color] onto the canvas, applying the given [BlendMode], with the given color being the source and the background being the destination.

### drawLine()

```dart
void drawLine(Offset p1, Offset p2, Paint paint)
```

Draws a line between the given points using the given paint. The line is stroked, the value of the [Paint.style] is ignored for this call.

The `p1` and `p2` arguments are interpreted as offsets from the origin.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_line.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_line_dark.png#gh-dark-mode-only)

### drawPaint()

```dart
void drawPaint(Paint paint)
```

Fills the canvas with the given [Paint].

To fill the canvas with a solid color and blend mode, consider [drawColor] instead.

### drawRect()

```dart
void drawRect(Rect rect, Paint paint)
```

Draws a rectangle with the given [Paint]. Whether the rectangle is filled or stroked (or both) is controlled by [Paint.style].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rect.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rect_dark.png#gh-dark-mode-only)

### drawRRect()

```dart
void drawRRect(RRect rrect, Paint paint)
```

Draws a rounded rectangle with the given [Paint]. Whether the rectangle is filled or stroked (or both) is controlled by [Paint.style].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rrect.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rrect_dark.png#gh-dark-mode-only)

### drawDRRect()

```dart
void drawDRRect(RRect outer, RRect inner, Paint paint)
```

Draws a shape consisting of the difference between two rounded rectangles with the given [Paint]. Whether this shape is filled or stroked (or both) is controlled by [Paint.style].

This shape is almost but not quite entirely unlike an annulus.

### drawRSuperellipse()

```dart
void drawRSuperellipse(RSuperellipse rsuperellipse, Paint paint)
```

Draws a rounded superellipse with the given [Paint]. The shape is filled, and the value of the [Paint.style] is ignored for this call.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rsuperellipse.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rsuperellipse.png#gh-dark-mode-only)

### drawOval()

```dart
void drawOval(Rect rect, Paint paint)
```

Draws an axis-aligned oval that fills the given axis-aligned rectangle with the given [Paint]. Whether the oval is filled or stroked (or both) is controlled by [Paint.style].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_oval.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_oval_dark.png#gh-dark-mode-only)

### drawCircle()

```dart
void drawCircle(Offset c, double radius, Paint paint)
```

Draws a circle centered at the point given by the first argument and that has the radius given by the second argument, with the [Paint] given in the third argument. Whether the circle is filled or stroked (or both) is controlled by [Paint.style].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_circle.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_circle_dark.png#gh-dark-mode-only)

### drawArc()

```dart
void drawArc(Rect rect, double startAngle, double sweepAngle, bool useCenter, Paint paint)
```

Draw an arc scaled to fit inside the given rectangle.

It starts from `startAngle` radians around the oval up to `startAngle` + `sweepAngle` radians around the oval, with zero radians being the point on the right hand side of the oval that crosses the horizontal line that intersects the center of the rectangle and with positive angles going clockwise around the oval. If `useCenter` is true, the arc is closed back to the center, forming a circle sector. Otherwise, the arc is not closed, forming a circle segment.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_draw_arc.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_draw_arc_dark.png#gh-dark-mode-only)

This method is optimized for drawing arcs and should be faster than [Path.arcTo].

### drawPath()

```dart
void drawPath(Path path, Paint paint)
```

Draws the given [Path] with the given [Paint].

Whether this shape is filled or stroked (or both) is controlled by [Paint.style]. If the path is filled, then sub-paths within it are implicitly closed (see [Path.close]).

When drawing simple shapes (such as rectangles, ovals, or rounded rectangles), prefer using methods such as [drawRect], [drawOval], or [drawRRect] over [drawPath]. Methods that draw simple shapes are generally more efficient than drawing a [Path].

### drawImage()

```dart
void drawImage(Image image, Offset offset, Paint paint)
```

Draws the given [Image] into the canvas with its top-left corner at the given [Offset]. The image is composited into the canvas using the given [Paint].

### drawImageRect()

```dart
void drawImageRect(Image image, Rect src, Rect dst, Paint paint)
```

Draws the subset of the given image described by the `src` argument into the canvas in the axis-aligned rectangle given by the `dst` argument.

This might sample from outside the `src` rect by up to half the width of an applied filter.

Multiple calls to this method with different arguments (from the same image) can be batched into a single call to [drawAtlas] to improve performance.

### drawImageNine()

```dart
void drawImageNine(Image image, Rect center, Rect dst, Paint paint)
```

Draws the given [Image] into the canvas using the given [Paint].

The image is drawn in nine portions described by splitting the image by drawing two horizontal lines and two vertical lines, where the `center` argument describes the rectangle formed by the four points where these four lines intersect each other. (This forms a 3-by-3 grid of regions, the center region being described by the `center` argument.)

The four regions in the corners are drawn, without scaling, in the four corners of the destination rectangle described by `dst`. The remaining five regions are drawn by stretching them to fit such that they exactly cover the destination rectangle while maintaining their relative positions.

### drawPicture()

```dart
void drawPicture(Picture picture)
```

Draw the given picture onto the canvas. To create a picture, see [PictureRecorder].

### drawParagraph()

```dart
void drawParagraph(Paragraph paragraph, Offset offset)
```

Draws the text in the given [Paragraph] into this canvas at the given [Offset].

The [Paragraph] object must have had [Paragraph.layout] called on it first.

To align the text, set the `textAlign` on the [ParagraphStyle] object passed to the [ParagraphBuilder.new] constructor. For more details see [TextAlign] and the discussion at [ParagraphStyle.new].

If the text is left aligned or justified, the left margin will be at the position specified by the `offset` argument's [Offset.dx] coordinate.

If the text is right aligned or justified, the right margin will be at the position described by adding the [ParagraphConstraints.width] given to [Paragraph.layout], to the `offset` argument's [Offset.dx] coordinate.

If the text is centered, the centering axis will be at the position described by adding half of the [ParagraphConstraints.width] given to [Paragraph.layout], to the `offset` argument's [Offset.dx] coordinate.

### drawPoints()

```dart
void drawPoints(PointMode pointMode, List<Offset> points, Paint paint)
```

Draws a sequence of points according to the given [PointMode].

The `points` argument is interpreted as offsets from the origin.

The `paint` is used for each point ([PointMode.points]) or line ([PointMode.lines] or [PointMode.polygon]), ignoring [Paint.style].

See also:

- [drawRawPoints], which takes `points` as a [Float32List] rather than a [List<Offset>].

### drawRawPoints()

```dart
void drawRawPoints(PointMode pointMode, Float32List points, Paint paint)
```

Draws a sequence of points according to the given [PointMode].

The `points` argument is interpreted as a list of pairs of floating point numbers, where each pair represents an x and y offset from the origin.

The `paint` is used for each point ([PointMode.points]) or line ([PointMode.lines] or [PointMode.polygon]), ignoring [Paint.style].

See also:

- [drawPoints], which takes `points` as a [List<Offset>] rather than a [List<Float32List>].

### drawVertices()

```dart
void drawVertices(Vertices vertices, BlendMode blendMode, Paint paint)
```

Draws a set of [Vertices] onto the canvas as one or more triangles.

The [Paint.color] property specifies the default color to use for the triangles.

The [Paint.shader] property, if set, overrides the color entirely, replacing it with the colors from the specified [ImageShader], [Gradient], or other shader.

The `blendMode` parameter is used to control how the colors in the `vertices` are combined with the colors in the `paint`. If there are no colors specified in `vertices` then the `blendMode` has no effect. If there are colors in the `vertices`, then the color taken from the [Paint.shader] or [Paint.color] in the `paint` is blended with the colors specified in the `vertices` using the `blendMode` parameter. For the purposes of this blending, the colors from the `paint` parameter are considered the source, and the colors from the `vertices` are considered the destination. [BlendMode.dst] ignores the `paint` and uses only the colors of the `vertices`; [BlendMode.src] ignores the colors of the `vertices` and uses only the colors in the `paint`.

All parameters must not be null.

See also:

- [Vertices.new], which creates a set of vertices to draw on the canvas.
- [Vertices.raw], which creates the vertices using typed data lists rather than unencoded lists.
- [paint], Image shaders can be used to draw images on a triangular mesh.

### drawAtlas()

```dart
void drawAtlas(Image atlas, List<RSTransform> transforms, List<Rect> rects, List<Color>? colors, BlendMode? blendMode, Rect? cullRect, Paint paint)
```

Draws many parts of an image - the [atlas] - onto the canvas.

This method allows for optimization when you want to draw many parts of an image onto the canvas, such as when using sprites or zooming. It is more efficient than using multiple calls to [drawImageRect] and provides more functionality to individually transform each image part by a separate rotation or scale and blend or modulate those parts with a solid color.

The method takes a list of [Rect] objects that each define a piece of the [atlas] image to be drawn independently. Each [Rect] is associated with an [RSTransform] entry in the [transforms] list which defines the location, rotation, and (uniform) scale with which to draw that portion of the image. Each [Rect] can also be associated with an optional [Color] which will be composed with the associated image part using the [blendMode] before blending the result onto the canvas. The full operation can be broken down as:

- Blend each rectangular portion of the image specified by an entry in the [rects] argument with its associated entry in the [colors] list using the [blendMode] argument (if a color is specified). In this part of the operation, the image part will be considered the source of the operation and the associated color will be considered the destination.
- Blend the result from the first step onto the canvas using the translation, rotation, and scale properties expressed in the associated entry in the [transforms] list using the properties of the [Paint] object.

If the first stage of the operation which blends each part of the image with a color is needed, then both the [colors] and [blendMode] arguments must not be null and there must be an entry in the [colors] list for each image part. If that stage is not needed, then the [colors] argument can be either null or an empty list and the [blendMode] argument may also be null.

The optional [cullRect] argument can provide an estimate of the bounds of the coordinates rendered by all components of the atlas to be compared against the clip to quickly reject the operation if it does not intersect.

An example usage to render many sprites from a single sprite atlas with no rotations or scales:

```dart
class Sprite {
  Sprite(this.index, this.center);
  int index;
  Offset center;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint();
    canvas.drawAtlas(spriteAtlas, <RSTransform>[
      for (final Sprite sprite in allSprites)
        RSTransform.fromComponents(
          rotation: 0.0,
          scale: 1.0,
          // Center of the sprite relative to its rect
          anchorX: 5.0,
          anchorY: 5.0,
          // Location at which to draw the center of the sprite
          translateX: sprite.center.dx,
          translateY: sprite.center.dy,
        ),
    ], <Rect>[
      for (final Sprite sprite in allSprites)
        Rect.fromLTWH(sprite.index * 10.0, 0.0, 10.0, 10.0),
    ], null, null, null, paint);
  }

  // ...
}
```

Another example usage which renders sprites with an optional opacity and rotation:

```dart
class Sprite {
  Sprite(this.index, this.center, this.alpha, this.rotation);
  int index;
  Offset center;
  int alpha;
  double rotation;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint();
    canvas.drawAtlas(spriteAtlas, <RSTransform>[
      for (final Sprite sprite in allSprites)
        RSTransform.fromComponents(
          rotation: sprite.rotation,
          scale: 1.0,
          // Center of the sprite relative to its rect
          anchorX: 5.0,
          anchorY: 5.0,
          // Location at which to draw the center of the sprite
          translateX: sprite.center.dx,
          translateY: sprite.center.dy,
        ),
    ], <Rect>[
      for (final Sprite sprite in allSprites)
        Rect.fromLTWH(sprite.index * 10.0, 0.0, 10.0, 10.0),
    ], <Color>[
      for (final Sprite sprite in allSprites)
        Colors.white.withAlpha(sprite.alpha),
    ], BlendMode.srcIn, null, paint);
  }

  // ...
}
```

The length of the [transforms] and [rects] lists must be equal and if the [colors] argument is not null then it must either be empty or have the same length as the other two lists.

See also:

- [drawRawAtlas], which takes its arguments as typed data lists rather than objects.

### drawRawAtlas()

```dart
void drawRawAtlas(Image atlas, Float32List rstTransforms, Float32List rects, Int32List? colors, BlendMode? blendMode, Rect? cullRect, Paint paint)
```

Draws many parts of an image - the [atlas] - onto the canvas.

This method allows for optimization when you want to draw many parts of an image onto the canvas, such as when using sprites or zooming. It is more efficient than using multiple calls to [drawImageRect] and provides more functionality to individually transform each image part by a separate rotation or scale and blend or modulate those parts with a solid color. It is also more efficient than [drawAtlas] as the data in the arguments is already packed in a format that can be directly used by the rendering code.

A full description of how this method uses its arguments to draw onto the canvas can be found in the description of the [drawAtlas] method.

The [rstTransforms] argument is interpreted as a list of four-tuples, with each tuple being ([RSTransform.scos], [RSTransform.ssin], [RSTransform.tx], [RSTransform.ty]).

The [rects] argument is interpreted as a list of four-tuples, with each tuple being ([Rect.left], [Rect.top], [Rect.right], [Rect.bottom]).

The [colors] argument, which can be null, is interpreted as a list of 32-bit colors, with the same packing as [Color.value]. If the [colors] argument is not null then the [blendMode] argument must also not be null.

An example usage to render many sprites from a single sprite atlas with no rotations or scales:

```dart
class Sprite {
  Sprite(this.index, this.center);
  int index;
  Offset center;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    // For best advantage, these lists should be cached and only specific
    // entries updated when the sprite information changes. This code is
    // illustrative of how to set up the data and not a recommendation for
    // optimal usage.
    Float32List rectList = Float32List(allSprites.length * 4);
    Float32List transformList = Float32List(allSprites.length * 4);
    for (int i = 0; i < allSprites.length; i++) {
      Sprite sprite = allSprites[i];
      final double rectX = sprite.index * 10.0;
      rectList[i * 4 + 0] = rectX;
      rectList[i * 4 + 1] = 0.0;
      rectList[i * 4 + 2] = rectX + 10.0;
      rectList[i * 4 + 3] = 10.0;

      // This example sets the RSTransform values directly for a common case of no
      // rotations or scales and just a translation to position the atlas entry. For
      // more complicated transforms one could use the RSTransform class to compute
      // the necessary values or do the same math directly.
      transformList[i * 4 + 0] = 1.0;
      transformList[i * 4 + 1] = 0.0;
      transformList[i * 4 + 2] = sprite.center.dx - 5.0;
      transformList[i * 4 + 3] = sprite.center.dy - 5.0;
    }
    Paint paint = Paint();
    canvas.drawRawAtlas(spriteAtlas, transformList, rectList, null, null, null, paint);
  }

  // ...
}
```

Another example usage which renders sprites with an optional opacity and rotation:

```dart
class Sprite {
  Sprite(this.index, this.center, this.alpha, this.rotation);
  int index;
  Offset center;
  int alpha;
  double rotation;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    // For best advantage, these lists should be cached and only specific
    // entries updated when the sprite information changes. This code is
    // illustrative of how to set up the data and not a recommendation for
    // optimal usage.
    Float32List rectList = Float32List(allSprites.length * 4);
    Float32List transformList = Float32List(allSprites.length * 4);
    Int32List colorList = Int32List(allSprites.length);
    for (int i = 0; i < allSprites.length; i++) {
      Sprite sprite = allSprites[i];
      final double rectX = sprite.index * 10.0;
      rectList[i * 4 + 0] = rectX;
      rectList[i * 4 + 1] = 0.0;
      rectList[i * 4 + 2] = rectX + 10.0;
      rectList[i * 4 + 3] = 10.0;

      // This example uses an RSTransform object to compute the necessary values for
      // the transform using a factory helper method because the sprites contain
      // rotation values which are not trivial to work with. But if the math for the
      // values falls out from other calculations on the sprites then the values could
      // possibly be generated directly from the sprite update code.
      final RSTransform transform = RSTransform.fromComponents(
        rotation: sprite.rotation,
        scale: 1.0,
        // Center of the sprite relative to its rect
        anchorX: 5.0,
        anchorY: 5.0,
        // Location at which to draw the center of the sprite
        translateX: sprite.center.dx,
        translateY: sprite.center.dy,
      );
      transformList[i * 4 + 0] = transform.scos;
      transformList[i * 4 + 1] = transform.ssin;
      transformList[i * 4 + 2] = transform.tx;
      transformList[i * 4 + 3] = transform.ty;

      // This example computes the color value directly, but one could also compute
      // an actual Color object and use its Color.value getter for the same result.
      // Since we are using BlendMode.srcIn, only the alpha component matters for
      // these colors which makes this a simple shift operation.
      colorList[i] = sprite.alpha << 24;
    }
    Paint paint = Paint();
    canvas.drawRawAtlas(spriteAtlas, transformList, rectList, colorList, BlendMode.srcIn, null, paint);
  }

  // ...
}
```

See also:

- [drawAtlas], which takes its arguments as objects rather than typed data lists.

### drawShadow()

```dart
void drawShadow(Path path, Color color, double elevation, bool transparentOccluder)
```

Draws a shadow for a [Path] representing the given material elevation.

The `transparentOccluder` argument should be true if the occluding object is not opaque.

The arguments must not be null.

# PictureEventCallback

```dart
typedef PictureEventCallback = void Function(Picture picture)
```

Signature for [Picture] lifecycle events.

# Picture

```dart
abstract class Picture {}
```

An object representing a sequence of recorded graphical operations.

To create a [Picture], use a [PictureRecorder].

A [Picture] can be placed in a [Scene] using a [SceneBuilder], via the [SceneBuilder.addPicture] method. A [Picture] can also be drawn into a [Canvas], using the [Canvas.drawPicture] method.

### onCreate

```dart
PictureEventCallback? onCreate
```

A callback that is invoked to report a picture creation.

It's preferred to use [MemoryAllocations] in flutter/foundation.dart than to use [onCreate] directly because [MemoryAllocations] allows multiple callbacks.

### onDispose

```dart
PictureEventCallback? onDispose
```

A callback that is invoked to report the picture disposal.

It's preferred to use [MemoryAllocations] in flutter/foundation.dart than to use [onDispose] directly because [MemoryAllocations] allows multiple callbacks.

### toImage()

```dart
Future<Image> toImage(int width, int height)
```

Creates an image from this picture.

The returned image will be `width` pixels wide and `height` pixels high. The picture is rasterized within the 0 (left), 0 (top), `width` (right), `height` (bottom) bounds. Content outside these bounds is clipped.

### toImageSync()

```dart
Image toImageSync(int width, int height, {TargetPixelFormat targetFormat = TargetPixelFormat.dontCare})
```

Synchronously creates a handle to an image of this picture.

{@template dart.ui.painting.Picture.toImageSync} The returned image will be [width] pixels wide and [height] pixels high. The picture is rasterized within the 0 (left), 0 (top), [width] (right), [height] (bottom) bounds. Content outside these bounds is clipped.

The image object is created and returned synchronously, but is rasterized asynchronously. If the rasterization fails, an exception will be thrown when the image is drawn to a [Canvas].

If a GPU context is available, this image will be created as GPU resident and not copied back to the host. This means the image will be more efficient to draw.

If no GPU context is available, the image will be rasterized on the CPU.

The [targetFormat] argument specifies the pixel format of the returned [Image]. If [TargetPixelFormat.dontCare] is specified, the pixel format will be chosen automatically based on the GPU capabilities. {@endtemplate}

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

### debugDisposed

```dart
bool get debugDisposed
```

Whether this reference to the underlying picture is [dispose]d.

This only returns a valid value if asserts are enabled, and must not be used otherwise.

### approximateBytesUsed

```dart
int get approximateBytesUsed
```

Returns the approximate number of bytes allocated for this object.

The actual size of this picture may be larger, particularly if it contains references to image or other large objects.

# PictureRecorder

```dart
abstract class PictureRecorder {}
```

Records a [Picture] containing a sequence of graphical operations.

To begin recording, construct a [Canvas] to record the commands. To end recording, use the [PictureRecorder.endRecording] method.

## Use with the Flutter framework

The Flutter framework's [RendererBinding] provides a hook for creating [PictureRecorder] objects ([RendererBinding.createPictureRecorder]) that allows tests to hook into the scene creation logic. When creating a [PictureRecorder] and [Canvas] that will be used with a [PictureLayer] as part of the [Scene] in the context of the Flutter framework, consider calling [RendererBinding.createPictureRecorder] instead of calling the [PictureRecorder.new] constructor directly.

This does not apply when using a canvas to generate a bitmap for other purposes, e.g. for generating a PNG image using [Picture.toImage].

### PictureRecorder()

```dart
PictureRecorder()
```

Creates a new idle PictureRecorder. To associate it with a [Canvas] and begin recording, pass this [PictureRecorder] to the [Canvas] constructor.

### isRecording

```dart
bool get isRecording
```

Whether this object is currently recording commands.

Specifically, this returns true if a [Canvas] object has been created to record commands and recording has not yet ended via a call to [endRecording], and false if either this [PictureRecorder] has not yet been associated with a [Canvas], or the [endRecording] method has already been called.

### endRecording()

```dart
Picture endRecording()
```

Finishes recording graphical operations.

Returns a picture containing the graphical operations that have been recorded thus far. After calling this function, both the picture recorder and the canvas objects are invalid and cannot be used further.

# Shadow

```dart
class Shadow {}
```

A single shadow.

Multiple shadows are stacked together in a [TextStyle].

### Shadow()

```dart
Shadow({Color color = const Color(_kColorDefault), Offset offset = Offset.zero, double blurRadius = 0.0})
```

Construct a shadow.

The default shadow is a black shadow with zero offset and zero blur. Default shadows should be completely covered by the casting element, and not be visible.

Transparency should be adjusted through the [color] alpha.

Shadow order matters due to compositing multiple translucent objects not being commutative.

### color

```dart
Color color
```

Color that the shadow will be drawn with.

The shadows are shapes composited directly over the base canvas, and do not represent optical occlusion.

### offset

```dart
Offset offset
```

The displacement of the shadow from the casting element.

Positive x/y offsets will shift the shadow to the right and down, while negative offsets shift the shadow to the left and up. The offsets are relative to the position of the element that is casting it.

### blurRadius

```dart
double blurRadius
```

The standard deviation of the Gaussian to convolve with the shadow's shape.

### convertRadiusToSigma()

```dart
double convertRadiusToSigma(double radius)
```

Converts a blur radius in pixels to sigmas.

See the sigma argument to [MaskFilter.blur].

### blurSigma

```dart
double get blurSigma
```

The [blurRadius] in sigmas instead of logical pixels.

See the sigma argument to [MaskFilter.blur].

### toPaint()

```dart
Paint toPaint()
```

Create the [Paint] object that corresponds to this shadow description.

The [offset] is not represented in the [Paint] object. To honor this as well, the shape should be translated by [offset] before being filled using this [Paint].

This class does not provide a way to disable shadows to avoid inconsistencies in shadow blur rendering, primarily as a method of reducing test flakiness. [toPaint] should be overridden in subclasses to provide this functionality.

### scale()

```dart
Shadow scale(double factor)
```

Returns a new shadow with its [offset] and [blurRadius] scaled by the given factor.

### lerp()

```dart
Shadow? lerp(Shadow? a, Shadow? b, double t)
```

Linearly interpolate between two shadows.

If either shadow is null, this function linearly interpolates from a shadow that matches the other shadow in color but has a zero offset and a zero blurRadius.

{@template dart.ui.shadow.lerp} The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController]. {@endtemplate}

### lerpList()

```dart
List<Shadow>? lerpList(List<Shadow>? a, List<Shadow>? b, double t)
```

Linearly interpolate between two lists of shadows.

If the lists differ in length, excess items are lerped with null.

{@macro dart.ui.shadow.lerp}

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

# ImmutableBuffer

```dart
base class ImmutableBuffer extends NativeFieldWrapperClass1 {}
```

A handle to a read-only byte buffer that is managed by the engine.

The creator of this object is responsible for calling [dispose] when it is no longer needed.

### fromUint8List()

```dart
Future<ImmutableBuffer> fromUint8List(Uint8List list)
```

Creates a copy of the data from a [Uint8List] suitable for internal use in the engine.

### fromAsset()

```dart
Future<ImmutableBuffer> fromAsset(String assetKey)
```

Create a buffer from the asset with key [assetKey].

Throws an [Exception] if the asset does not exist.

### fromFilePath()

```dart
Future<ImmutableBuffer> fromFilePath(String path)
```

Create a buffer from the file with [path].

Throws an [Exception] if the asset does not exist.

### length

```dart
int get length
```

The length, in bytes, of the underlying data.

### debugDisposed

```dart
bool get debugDisposed
```

Whether [dispose] has been called.

This must only be used when asserts are enabled. Otherwise, it will throw.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

The underlying memory allocated by this object will be retained beyond this call if it is still needed by another object that has not been disposed. For example, an [ImageDescriptor] that has not been disposed may still retain a reference to the memory from this buffer even if it has been disposed. Freeing that memory requires disposing all resources that may still hold it.

# ImageDescriptor

```dart
abstract class ImageDescriptor {}
```

A descriptor of data that can be turned into an [Image] via a [Codec].

Use this class to determine the height, width, and byte size of image data before decoding it.

### ImageDescriptor.raw()

```dart
ImageDescriptor.raw(ImmutableBuffer buffer, {required int width, required int height, int? rowBytes, required PixelFormat pixelFormat})
```

Creates an image descriptor from raw image pixels.

The `pixels` parameter is the pixel data. They are packed in bytes in the order described by `pixelFormat`, then grouped in rows, from left to right, then top to bottom.

The `rowBytes` parameter is the number of bytes consumed by each row of pixels in the data buffer. If unspecified, it defaults to `width` multiplied by the number of bytes per pixel in the provided `format`.

### encoded()

```dart
Future<ImageDescriptor> encoded(ImmutableBuffer buffer)
```

Creates an image descriptor from encoded data in a supported format.

### width

```dart
int get width
```

The width, in pixels, of the image.

On the Web, this is only supported for [raw] images.

### height

```dart
int get height
```

The height, in pixels, of the image.

On the Web, this is only supported for [raw] images.

### bytesPerPixel

```dart
int get bytesPerPixel
```

The number of bytes per pixel in the image.

On web, this is only supported for [raw] images.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

This can't be a leaf call because the native function calls Dart API (Dart_SetNativeInstanceField).

### instantiateCodec()

```dart
Future<Codec> instantiateCodec({int? targetWidth, int? targetHeight, TargetPixelFormat targetFormat = TargetPixelFormat.dontCare})
```

Creates a [Codec] object which is suitable for decoding the data in the buffer to an [Image].

If only one of targetWidth or targetHeight are specified, the other dimension will be scaled according to the aspect ratio of the supplied dimension.

If either targetWidth or targetHeight is less than or equal to zero, it will be treated as if it is null.

# PictureRasterizationException

```dart
class PictureRasterizationException implements Exception {}
```

An exception thrown by [Canvas.drawImage] and related methods when drawing an [Image] created via [Picture.toImageSync] that is in an invalid state.

This exception may be thrown if the requested image dimensions exceeded the maximum 2D texture size allowed by the GPU, or if no GPU surface or context was available for rasterization at request time.

### message

```dart
String message
```

A string containing details about the failure.

### stack

```dart
StackTrace? stack
```

If available, the stack trace at the time [Picture.toImageSync] was called.

### toString()

```dart
String toString()
```
