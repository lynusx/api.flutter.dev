@docImport 'input_decorator.dart'; @docImport 'scaffold.dart';

# DynamicSchemeVariant

```dart
enum DynamicSchemeVariant {}
```

The algorithm used to construct a [ColorScheme] in [ColorScheme.fromSeed].

The `tonalSpot` variant builds default Material scheme colors. These colors are mapped to light or dark tones to achieve visually accessible color pairings with sufficient contrast between foreground and background elements.

In some cases, the tones can prevent colors from appearing as intended, such as when a color is too light to offer enough contrast for accessibility. Color fidelity (`DynamicSchemeVariant.fidelity`) is a feature that adjusts tones in these cases to produce the intended visual results without harming visual contrast.

Default for Material theme colors. Builds pastel palettes with a low chroma.

The resulting color palettes match seed color, even if the seed color is very bright (high chroma).

All colors are grayscale, no chroma.

Close to grayscale, a hint of chroma.

Pastel colors, high chroma palettes. The primary palette's chroma is at maximum. Use `fidelity` instead if tokens should alter their tone to match the palette vibrancy.

Pastel colors, medium chroma palettes. The primary palette's hue is different from the seed color, for variety.

Almost identical to `fidelity`. Tokens and palettes match the seed color. [ColorScheme.primaryContainer] is the seed color, adjusted to ensure contrast with surfaces. The tertiary palette is analogue of the seed color.

A playful theme - the seed color's hue does not appear in the theme.

A playful theme - the seed color's hue does not appear in the theme.

# ColorScheme

```dart
class ColorScheme with Diagnosticable {}
```

{@template flutter.material.color_scheme.ColorScheme} A set of 45 colors based on the [Material spec](https://m3.material.io/styles/color/the-color-system/color-roles) that can be used to configure the color properties of most components. {@endtemplate}

### Colors in Material 3

{@macro flutter.material.colors.colorRoles}

The main accent color groups in the scheme are [primary], [secondary], and [tertiary].

- Primary colors are used for key components across the UI, such as the FAB, prominent buttons, and active states.

- Secondary colors are used for less prominent components in the UI, such as filter chips, while expanding the opportunity for color expression.

- Tertiary colors are used for contrasting accents that can be used to balance primary and secondary colors or bring heightened attention to an element, such as an input field. The tertiary colors are left for makers to use at their discretion and are intended to support broader color expression in products.

Each accent color group (primary, secondary and tertiary) includes '-Fixed' '-Dim' color roles, such as [primaryFixed] and [primaryFixedDim]. Fixed roles are appropriate to use in places where Container roles are normally used, but they stay the same color between light and dark themes. The '-Dim' roles provide a stronger, more emphasized color with the same fixed behavior.

The remaining colors of the scheme are composed of neutral colors used for backgrounds and surfaces, as well as specific colors for errors, dividers and shadows. Surface colors are used for backgrounds and large, low-emphasis areas of the screen.

Material 3 also introduces tone-based surfaces and surface containers. They replace the old opacity-based model which applied a tinted overlay on top of surfaces based on their elevation. These colors include: [surfaceBright], [surfaceDim], [surfaceContainerLowest], [surfaceContainerLow], [surfaceContainer], [surfaceContainerHigh], and [surfaceContainerHighest].

Many of the colors have matching 'on' colors, which are used for drawing content on top of the matching color. For example, if something is using [primary] for a background color, [onPrimary] would be used to paint text and icons on top of it. For this reason, the 'on' colors should have a contrast ratio with their matching colors of at least 4.5:1 in order to be readable. On '-FixedVariant' roles, such as [onPrimaryFixedVariant], also have the same color between light and dark themes, but compared with on '-Fixed' roles, such as [onPrimaryFixed], they provide a lower-emphasis option for text and icons.

{@tool dartpad} This example shows all Material [ColorScheme] roles in light and dark brightnesses.

** See code in examples/api/lib/material/color_scheme/color_scheme.0.dart ** {@end-tool}

### Setting Colors in Flutter

{@macro flutter.material.colors.settingColors}

### ColorScheme()

```dart
ColorScheme({required Brightness brightness, required Color primary, required Color onPrimary, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, required Color secondary, required Color onSecondary, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, required Color error, required Color onError, Color? errorContainer, Color? onErrorContainer, required Color surface, required Color onSurface, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? outline, Color? outlineVariant, Color? shadow, Color? scrim, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? surfaceTint, Color? background, Color? onBackground, Color? surfaceVariant})
```

Create a ColorScheme instance from the given colors.

[ColorScheme.fromSeed] can be used as a simpler way to create a full color scheme derived from a single seed color.

For the color parameters that are nullable, it is still recommended that applications provide values for them. They are only nullable due to backwards compatibility concerns.

If a color is not provided, the closest fallback color from the given colors will be used for it (e.g. [primaryContainer] will default to [primary]). Material Design 3 makes use of these colors for many component defaults, so for the best results the application should supply colors for all the parameters. An easy way to ensure this is to use [ColorScheme.fromSeed] to generate a full set of colors.

During the migration to Material Design 3, if an app's [ThemeData.useMaterial3] is false, then components will only use the following colors for defaults:

- [primary]
- [onPrimary]
- [secondary]
- [onSecondary]
- [error]
- [onError]
- [surface]
- [onSurface] DEPRECATED:
- [background]
- [onBackground]

### ColorScheme.fromSeed()

```dart
ColorScheme.fromSeed({required Color seedColor, Brightness brightness = Brightness.light, DynamicSchemeVariant dynamicSchemeVariant = DynamicSchemeVariant.tonalSpot, double contrastLevel = 0.0, Color? primary, Color? onPrimary, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color? secondary, Color? onSecondary, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color? error, Color? onError, Color? errorContainer, Color? onErrorContainer, Color? outline, Color? outlineVariant, Color? surface, Color? onSurface, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? shadow, Color? scrim, Color? surfaceTint, Color? background, Color? onBackground, Color? surfaceVariant})
```

Generate a [ColorScheme] derived from the given `seedColor`.

Using the `seedColor` as a starting point, a set of tonal palettes are constructed. By default, the tonal palettes are based on the Material 3 Color system and provide all of the [ColorScheme] colors. These colors are designed to work well together and meet contrast requirements for accessibility.

If any of the optional color parameters are non-null they will be used in place of the generated colors for that field in the resulting color scheme. This allows apps to override specific colors for their needs.

Given the nature of the algorithm, the `seedColor` may not wind up as one of the ColorScheme colors.

The `dynamicSchemeVariant` parameter creates different types of [DynamicScheme]s, which are used to generate different styles of [ColorScheme]s. By default, `dynamicSchemeVariant` is set to `tonalSpot`. A [ColorScheme] constructed by `dynamicSchemeVariant.tonalSpot` has pastel palettes and won't be too "colorful" even if the `seedColor` has a high chroma value. If the resulting color scheme is too dark, consider setting `dynamicSchemeVariant` to [DynamicSchemeVariant.fidelity], whose palettes match the seed color.

The `contrastLevel` parameter indicates the contrast level between color pairs, such as [primary] and [onPrimary]. 0.0 is the default (normal); -1.0 is the lowest; 1.0 is the highest. From Material Design guideline, the medium and high contrast correspond to 0.5 and 1.0 respectively.

{@tool dartpad} This sample shows how to use [ColorScheme.fromSeed] to create dynamic color schemes with different [DynamicSchemeVariant]s and different contrast level.

** See code in examples/api/lib/material/color_scheme/color_scheme.0.dart ** {@end-tool}

See also:

- <https://m3.material.io/styles/color/the-color-system/color-roles>, the Material 3 Color system specification.
- <https://pub.dev/packages/material_color_utilities>, the package used to generate the tonal palettes needed for the scheme.

### ColorScheme.light()

```dart
ColorScheme.light({Brightness brightness = Brightness.light, Color primary = const Color(0xff6200ee), Color onPrimary = Colors.white, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color secondary = const Color(0xff03dac6), Color onSecondary = Colors.black, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color error = const Color(0xffb00020), Color onError = Colors.white, Color? errorContainer, Color? onErrorContainer, Color surface = Colors.white, Color onSurface = Colors.black, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? outline, Color? outlineVariant, Color? shadow, Color? scrim, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? surfaceTint, Color? background = Colors.white, Color? onBackground = Colors.black, Color? surfaceVariant})
```

Create a light ColorScheme based on a purple primary color that matches the [baseline Material 2 color scheme](https://material.io/design/color/the-color-system.html#color-theme-creation).

This constructor shouldn't be used to update the Material 3 color scheme.

For Material 3, use [ColorScheme.fromSeed] to create a color scheme from a single seed color based on the Material 3 color system.

{@tool snippet} This example demonstrates how to create a color scheme similar to [ColorScheme.light] using the [ColorScheme.fromSeed] constructor:

```dart
colorScheme: ColorScheme.fromSeed(seedColor: const Color(0xff6200ee)).copyWith(
  primaryContainer: const Color(0xff6200ee),
  onPrimaryContainer: Colors.white,
  secondaryContainer: const Color(0xff03dac6),
  onSecondaryContainer: Colors.black,
  error: const Color(0xffb00020),
  onError: Colors.white,
),
```

{@end-tool}

### ColorScheme.dark()

```dart
ColorScheme.dark({Brightness brightness = Brightness.dark, Color primary = const Color(0xffbb86fc), Color onPrimary = Colors.black, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color secondary = const Color(0xff03dac6), Color onSecondary = Colors.black, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color error = const Color(0xffcf6679), Color onError = Colors.black, Color? errorContainer, Color? onErrorContainer, Color surface = const Color(0xff121212), Color onSurface = Colors.white, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? outline, Color? outlineVariant, Color? shadow, Color? scrim, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? surfaceTint, Color? background = const Color(0xff121212), Color? onBackground = Colors.white, Color? surfaceVariant})
```

Create the dark color scheme that matches the [baseline Material 2 color scheme](https://material.io/design/color/dark-theme.html#ui-application).

This constructor shouldn't be used to update the Material 3 color scheme.

For Material 3, use [ColorScheme.fromSeed] to create a color scheme from a single seed color based on the Material 3 color system. Override the `brightness` property of [ColorScheme.fromSeed] to create a dark color scheme.

{@tool snippet} This example demonstrates how to create a color scheme similar to [ColorScheme.dark] using the [ColorScheme.fromSeed] constructor:

```dart
colorScheme: ColorScheme.fromSeed(
  seedColor: const Color(0xffbb86fc),
  brightness: Brightness.dark,
).copyWith(
  primaryContainer: const Color(0xffbb86fc),
  onPrimaryContainer: Colors.black,
  secondaryContainer: const Color(0xff03dac6),
  onSecondaryContainer: Colors.black,
  error: const Color(0xffcf6679),
  onError: Colors.black,
),
```

{@end-tool}

### ColorScheme.highContrastLight()

```dart
ColorScheme.highContrastLight({Brightness brightness = Brightness.light, Color primary = const Color(0xff0000ba), Color onPrimary = Colors.white, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color secondary = const Color(0xff66fff9), Color onSecondary = Colors.black, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color error = const Color(0xff790000), Color onError = Colors.white, Color? errorContainer, Color? onErrorContainer, Color surface = Colors.white, Color onSurface = Colors.black, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? outline, Color? outlineVariant, Color? shadow, Color? scrim, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? surfaceTint, Color? background = Colors.white, Color? onBackground = Colors.black, Color? surfaceVariant})
```

Create a high contrast ColorScheme based on a purple primary color that matches the [baseline Material 2 color scheme](https://material.io/design/color/the-color-system.html#color-theme-creation).

This constructor shouldn't be used to update the Material 3 color scheme.

For Material 3, use [ColorScheme.fromSeed] to create a color scheme from a single seed color based on the Material 3 color system. To create a high-contrast color scheme, set `contrastLevel` to 1.0.

{@tool snippet} This example demonstrates how to create a color scheme similar to [ColorScheme.highContrastLight] using the [ColorScheme.fromSeed] constructor:

```dart
colorScheme: ColorScheme.fromSeed(seedColor: const Color(0xff0000ba)).copyWith(
  primaryContainer: const Color(0xff0000ba),
  onPrimaryContainer: Colors.white,
  secondaryContainer: const Color(0xff66fff9),
  onSecondaryContainer: Colors.black,
  error: const Color(0xff790000),
  onError: Colors.white,
),
```

{@end-tool}

### ColorScheme.highContrastDark()

```dart
ColorScheme.highContrastDark({Brightness brightness = Brightness.dark, Color primary = const Color(0xffefb7ff), Color onPrimary = Colors.black, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color secondary = const Color(0xff66fff9), Color onSecondary = Colors.black, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color error = const Color(0xff9b374d), Color onError = Colors.black, Color? errorContainer, Color? onErrorContainer, Color surface = const Color(0xff121212), Color onSurface = Colors.white, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? outline, Color? outlineVariant, Color? shadow, Color? scrim, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? surfaceTint, Color? background = const Color(0xff121212), Color? onBackground = Colors.white, Color? surfaceVariant})
```

Create a high contrast ColorScheme based on the dark [baseline Material 2 color scheme](https://material.io/design/color/dark-theme.html#ui-application).

This constructor shouldn't be used to update the Material 3 color scheme.

For Material 3, use [ColorScheme.fromSeed] to create a color scheme from a single seed color based on the Material 3 color system. Override the `brightness` property of [ColorScheme.fromSeed] to create a dark color scheme. To create a high-contrast color scheme, set `contrastLevel` to 1.0.

{@tool snippet} This example demonstrates how to create a color scheme similar to [ColorScheme.highContrastDark] using the [ColorScheme.fromSeed] constructor:

```dart
colorScheme: ColorScheme.fromSeed(
  seedColor: const Color(0xffefb7ff),
  brightness: Brightness.dark,
).copyWith(
  primaryContainer: const Color(0xffefb7ff),
  onPrimaryContainer: Colors.black,
  secondaryContainer: const Color(0xff66fff9),
  onSecondaryContainer: Colors.black,
  error: const Color(0xff9b374d),
  onError: Colors.white,
),
```

{@end-tool}

### ColorScheme.fromSwatch()

```dart
ColorScheme.fromSwatch({MaterialColor primarySwatch = Colors.blue, Color? accentColor, Color? cardColor, Color? backgroundColor, Color? errorColor, Brightness brightness = Brightness.light})
```

Creates a color scheme from a [MaterialColor] swatch.

In Material 3, this constructor is ignored by [ThemeData] when creating its default color scheme. Instead, [ThemeData] uses [ColorScheme.fromSeed] to create its default color scheme. This constructor shouldn't be used to update the Material 3 color scheme. It will be phased out gradually; see https://github.com/flutter/flutter/issues/120064 for more details.

If [ThemeData.useMaterial3] is false, then this constructor is used by [ThemeData] to create its default color scheme.

### brightness

```dart
Brightness brightness
```

The overall brightness of this color scheme.

### primary

```dart
Color primary
```

The color displayed most frequently across your app’s screens and components.

### onPrimary

```dart
Color onPrimary
```

A color that's clearly legible when drawn on [primary].

To ensure that an app is accessible, a contrast ratio between [primary] and [onPrimary] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### primaryContainer

```dart
Color get primaryContainer
```

A color used for elements needing less emphasis than [primary].

### onPrimaryContainer

```dart
Color get onPrimaryContainer
```

A color that's clearly legible when drawn on [primaryContainer].

To ensure that an app is accessible, a contrast ratio between [primaryContainer] and [onPrimaryContainer] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### primaryFixed

```dart
Color get primaryFixed
```

A substitute for [primaryContainer] that's the same color for the dark and light themes.

### primaryFixedDim

```dart
Color get primaryFixedDim
```

A color used for elements needing more emphasis than [primaryFixed].

### onPrimaryFixed

```dart
Color get onPrimaryFixed
```

A color that is used for text and icons that exist on top of elements having [primaryFixed] color.

### onPrimaryFixedVariant

```dart
Color get onPrimaryFixedVariant
```

A color that provides a lower-emphasis option for text and icons than [onPrimaryFixed].

### secondary

```dart
Color secondary
```

An accent color used for less prominent components in the UI, such as filter chips, while expanding the opportunity for color expression.

### onSecondary

```dart
Color onSecondary
```

A color that's clearly legible when drawn on [secondary].

To ensure that an app is accessible, a contrast ratio between [secondary] and [onSecondary] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### secondaryContainer

```dart
Color get secondaryContainer
```

A color used for elements needing less emphasis than [secondary].

### onSecondaryContainer

```dart
Color get onSecondaryContainer
```

A color that's clearly legible when drawn on [secondaryContainer].

To ensure that an app is accessible, a contrast ratio between [secondaryContainer] and [onSecondaryContainer] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### secondaryFixed

```dart
Color get secondaryFixed
```

A substitute for [secondaryContainer] that's the same color for the dark and light themes.

### secondaryFixedDim

```dart
Color get secondaryFixedDim
```

A color used for elements needing more emphasis than [secondaryFixed].

### onSecondaryFixed

```dart
Color get onSecondaryFixed
```

A color that is used for text and icons that exist on top of elements having [secondaryFixed] color.

### onSecondaryFixedVariant

```dart
Color get onSecondaryFixedVariant
```

A color that provides a lower-emphasis option for text and icons than [onSecondaryFixed].

### tertiary

```dart
Color get tertiary
```

A color used as a contrasting accent that can balance [primary] and [secondary] colors or bring heightened attention to an element, such as an input field.

### onTertiary

```dart
Color get onTertiary
```

A color that's clearly legible when drawn on [tertiary].

To ensure that an app is accessible, a contrast ratio between [tertiary] and [onTertiary] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### tertiaryContainer

```dart
Color get tertiaryContainer
```

A color used for elements needing less emphasis than [tertiary].

### onTertiaryContainer

```dart
Color get onTertiaryContainer
```

A color that's clearly legible when drawn on [tertiaryContainer].

To ensure that an app is accessible, a contrast ratio between [tertiaryContainer] and [onTertiaryContainer] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### tertiaryFixed

```dart
Color get tertiaryFixed
```

A substitute for [tertiaryContainer] that's the same color for dark and light themes.

### tertiaryFixedDim

```dart
Color get tertiaryFixedDim
```

A color used for elements needing more emphasis than [tertiaryFixed].

### onTertiaryFixed

```dart
Color get onTertiaryFixed
```

A color that is used for text and icons that exist on top of elements having [tertiaryFixed] color.

### onTertiaryFixedVariant

```dart
Color get onTertiaryFixedVariant
```

A color that provides a lower-emphasis option for text and icons than [onTertiaryFixed].

### error

```dart
Color error
```

The color to use for input validation errors, e.g. for [InputDecoration.errorText].

### onError

```dart
Color onError
```

A color that's clearly legible when drawn on [error].

To ensure that an app is accessible, a contrast ratio between [error] and [onError] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### errorContainer

```dart
Color get errorContainer
```

A color used for error elements needing less emphasis than [error].

### onErrorContainer

```dart
Color get onErrorContainer
```

A color that's clearly legible when drawn on [errorContainer].

To ensure that an app is accessible, a contrast ratio between [errorContainer] and [onErrorContainer] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### surface

```dart
Color surface
```

The background color for widgets like [Scaffold].

### onSurface

```dart
Color onSurface
```

A color that's clearly legible when drawn on [surface].

To ensure that an app is accessible, a contrast ratio between [surface] and [onSurface] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### surfaceVariant

```dart
Color get surfaceVariant
```

A color variant of [surface] that can be used for differentiation against a component using [surface].

### surfaceDim

```dart
Color get surfaceDim
```

A color that's always darkest in the dark or light theme.

### surfaceBright

```dart
Color get surfaceBright
```

A color that's always the lightest in the dark or light theme.

### surfaceContainerLowest

```dart
Color get surfaceContainerLowest
```

A surface container color with the lightest tone and the least emphasis relative to the surface.

### surfaceContainerLow

```dart
Color get surfaceContainerLow
```

A surface container color with a lighter tone that creates less emphasis than [surfaceContainer] but more emphasis than [surfaceContainerLowest].

### surfaceContainer

```dart
Color get surfaceContainer
```

A recommended color role for a distinct area within the surface.

Surface container color roles are independent of elevation. They replace the old opacity-based model which applied a tinted overlay on top of surfaces based on their elevation.

Surface container colors include [surfaceContainerLowest], [surfaceContainerLow], [surfaceContainer], [surfaceContainerHigh] and [surfaceContainerHighest].

### surfaceContainerHigh

```dart
Color get surfaceContainerHigh
```

A surface container color with a darker tone. It is used to create more emphasis than [surfaceContainer] but less emphasis than [surfaceContainerHighest].

### surfaceContainerHighest

```dart
Color get surfaceContainerHighest
```

A surface container color with the darkest tone. It is used to create the most emphasis against the surface.

### onSurfaceVariant

```dart
Color get onSurfaceVariant
```

A color that's clearly legible when drawn on [surfaceVariant].

To ensure that an app is accessible, a contrast ratio between [surfaceVariant] and [onSurfaceVariant] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### outline

```dart
Color get outline
```

A utility color that creates boundaries and emphasis to improve usability.

### outlineVariant

```dart
Color get outlineVariant
```

A utility color that creates boundaries for decorative elements when a 3:1 contrast isn’t required, such as for dividers or decorative elements.

### shadow

```dart
Color get shadow
```

A color use to paint the drop shadows of elevated components.

### scrim

```dart
Color get scrim
```

A color use to paint the scrim around of modal components.

### inverseSurface

```dart
Color get inverseSurface
```

A surface color used for displaying the reverse of what’s seen in the surrounding UI, for example in a SnackBar to bring attention to an alert.

### onInverseSurface

```dart
Color get onInverseSurface
```

A color that's clearly legible when drawn on [inverseSurface].

To ensure that an app is accessible, a contrast ratio between [inverseSurface] and [onInverseSurface] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### inversePrimary

```dart
Color get inversePrimary
```

An accent color used for displaying a highlight color on [inverseSurface] backgrounds, like button text in a SnackBar.

### surfaceTint

```dart
Color get surfaceTint
```

A color used as an overlay on a surface color to indicate a component's elevation.

### background

```dart
Color get background
```

A color that typically appears behind scrollable content.

### onBackground

```dart
Color get onBackground
```

A color that's clearly legible when drawn on [background].

To ensure that an app is accessible, a contrast ratio between [background] and [onBackground] of at least 4.5:1 is recommended. See <https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html>.

### copyWith()

```dart
ColorScheme copyWith({Brightness? brightness, Color? primary, Color? onPrimary, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color? secondary, Color? onSecondary, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color? error, Color? onError, Color? errorContainer, Color? onErrorContainer, Color? surface, Color? onSurface, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? outline, Color? outlineVariant, Color? shadow, Color? scrim, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? surfaceTint, Color? background, Color? onBackground, Color? surfaceVariant})
```

Creates a copy of this color scheme with the given fields replaced by the non-null parameter values.

### lerp()

```dart
ColorScheme lerp(ColorScheme a, ColorScheme b, double t)
```

Linearly interpolate between two [ColorScheme] objects.

{@macro dart.ui.shadow.lerp}

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

### fromImageProvider()

```dart
Future<ColorScheme> fromImageProvider({required ImageProvider provider, Brightness brightness = Brightness.light, DynamicSchemeVariant dynamicSchemeVariant = DynamicSchemeVariant.tonalSpot, double contrastLevel = 0.0, Color? primary, Color? onPrimary, Color? primaryContainer, Color? onPrimaryContainer, Color? primaryFixed, Color? primaryFixedDim, Color? onPrimaryFixed, Color? onPrimaryFixedVariant, Color? secondary, Color? onSecondary, Color? secondaryContainer, Color? onSecondaryContainer, Color? secondaryFixed, Color? secondaryFixedDim, Color? onSecondaryFixed, Color? onSecondaryFixedVariant, Color? tertiary, Color? onTertiary, Color? tertiaryContainer, Color? onTertiaryContainer, Color? tertiaryFixed, Color? tertiaryFixedDim, Color? onTertiaryFixed, Color? onTertiaryFixedVariant, Color? error, Color? onError, Color? errorContainer, Color? onErrorContainer, Color? outline, Color? outlineVariant, Color? surface, Color? onSurface, Color? surfaceDim, Color? surfaceBright, Color? surfaceContainerLowest, Color? surfaceContainerLow, Color? surfaceContainer, Color? surfaceContainerHigh, Color? surfaceContainerHighest, Color? onSurfaceVariant, Color? inverseSurface, Color? onInverseSurface, Color? inversePrimary, Color? shadow, Color? scrim, Color? surfaceTint, Color? background, Color? onBackground, Color? surfaceVariant})
```

Generate a [ColorScheme] derived from the given `imageProvider`.

Material Color Utilities extracts the dominant color from the supplied [ImageProvider]. Using this color, a [ColorScheme] is generated with harmonious colors that meet contrast requirements for accessibility.

If any of the optional color parameters are non-null, they will be used in place of the generated colors for that field in the resulting [ColorScheme]. This allows apps to override specific colors for their needs.

Given the nature of the algorithm, the most dominant color of the `imageProvider` may not wind up as one of the [ColorScheme] colors.

The provided image will be scaled down to a maximum size of 112x112 pixels during color extraction.

{@tool dartpad} This sample shows how to use [ColorScheme.fromImageProvider] to create content-based dynamic color schemes.

** See code in examples/api/lib/material/color_scheme/dynamic_content_color.0.dart ** {@end-tool}

See also:

- [M3 Guidelines: Dynamic color from content](https://m3.material.io/styles/color/dynamic-color/user-generated-color#8af550b9-a19e-4e9f-bb0a-7f611fed5d0f)
- <https://pub.dev/packages/dynamic_color>, a package to create [ColorScheme]s based on a platform's implementation of dynamic color.
- <https://m3.material.io/styles/color/the-color-system/color-roles>, the Material 3 Color system specification.
- <https://pub.dev/packages/material_color_utilities>, the package used to algorithmically determine the dominant color and to generate the [ColorScheme].

### of()

```dart
ColorScheme of(BuildContext context)
```

The [ThemeData.colorScheme] of the ambient [Theme].

Equivalent to `Theme.of(context).colorScheme`.
