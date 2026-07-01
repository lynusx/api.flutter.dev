@docImport 'material_localizations.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart';

# ScriptCategory

```dart
enum ScriptCategory {}
```

A characterization of the of a [TextTheme]'s glyphs that is used to define its localized [TextStyle] geometry for [ThemeData.textTheme].

The script category defines the overall geometry of a [TextTheme] for the [Typography.geometryThemeFor] method in terms of the three language categories defined in <https://material.io/go/design-typography>.

Generally speaking, font sizes for `ScriptCategory.tall` and `ScriptCategory.dense` scripts - for text styles that are smaller than the title style - are one unit larger than they are for `ScriptCategory.englishLike` scripts.

The languages of Western, Central, and Eastern Europe and much of Africa are typically written in the Latin alphabet. Vietnamese is a notable exception in that, while it uses a localized form of the Latin writing system, its accented glyphs can be much taller than those found in Western European languages. The Greek and Cyrillic writing systems are very similar to Latin.

Language scripts that require extra line height to accommodate larger glyphs, including Chinese, Japanese, and Korean.

Language scripts that require extra line height to accommodate larger glyphs, including South and Southeast Asian and Middle-Eastern languages, like Arabic, Hindi, Telugu, Thai, and Vietnamese.

# Typography

```dart
class Typography with Diagnosticable {}
```

The color and geometry [TextTheme]s for Material apps.

The text theme provided by the overall [Theme], [ThemeData.textTheme], is based on the current locale's [MaterialLocalizations.scriptCategory] and is created by merging a color text theme - [black] for [Brightness.light] themes and [white] for [Brightness.dark] themes - and a geometry text theme, one of [englishLike], [dense], or [tall], depending on the locale.

To lookup the localized text theme use `Theme.of(context).textTheme`.

The color text themes are [blackMountainView], [whiteMountainView], [blackCupertino], and [whiteCupertino]. The Mountain View theme [TextStyle]s are based on the Roboto fonts as used on Android. The Cupertino themes are based on the [San Francisco font](https://developer.apple.com/design/human-interface-guidelines/typography/) fonts as used by Apple on iOS.

Two sets of geometry themes are provided: 2014 and 2018. The 2014 themes correspond to the original version of the Material Design spec and are the defaults. The 2018 themes correspond the second iteration of the specification and feature different font sizes, font weights, and letter spacing values.

By default, [ThemeData.typography] is `Typography.material2014(platform: platform)` which uses [englishLike2014], [dense2014] and [tall2014]. To use the 2018 text theme geometries, specify a value using the [Typography.material2018] constructor:

```dart
typography: Typography.material2018(platform: platform)
```

See also:

- <https://material.io/design/typography/>
- <https://m3.material.io/styles/typography>

### Typography()

```dart
Typography({TargetPlatform? platform, TextTheme? black, TextTheme? white, TextTheme? englishLike, TextTheme? dense, TextTheme? tall})
```

Creates a typography instance.

This constructor is identical to [Typography.material2018].

### Typography.material2014()

```dart
Typography.material2014({TargetPlatform? platform = TargetPlatform.android, TextTheme? black, TextTheme? white, TextTheme? englishLike, TextTheme? dense, TextTheme? tall})
```

Creates a typography instance using Material Design's 2014 defaults.

If [platform] is [TargetPlatform.iOS] or [TargetPlatform.macOS], the default values for [black] and [white] are [blackCupertino] and [whiteCupertino] respectively. Otherwise they are [blackMountainView] and [whiteMountainView]. If [platform] is null then both [black] and [white] must be specified.

The default values for [englishLike], [dense], and [tall] are [englishLike2014], [dense2014], and [tall2014].

### Typography.material2018()

```dart
Typography.material2018({TargetPlatform? platform = TargetPlatform.android, TextTheme? black, TextTheme? white, TextTheme? englishLike, TextTheme? dense, TextTheme? tall})
```

Creates a typography instance using Material Design's 2018 defaults.

If [platform] is [TargetPlatform.iOS] or [TargetPlatform.macOS], the default values for [black] and [white] are [blackCupertino] and [whiteCupertino] respectively. Otherwise they are [blackMountainView] and [whiteMountainView]. If [platform] is null then both [black] and [white] must be specified.

The default values for [englishLike], [dense], and [tall] are [englishLike2018], [dense2018], and [tall2018].

### Typography.material2021()

```dart
Typography.material2021({TargetPlatform? platform = TargetPlatform.android, ColorScheme colorScheme = const ColorScheme.light(), TextTheme? black, TextTheme? white, TextTheme? englishLike, TextTheme? dense, TextTheme? tall})
```

Creates a typography instance using Material Design 3 2021 defaults.

If [platform] is [TargetPlatform.iOS] or [TargetPlatform.macOS], the default values for [black] and [white] are [blackCupertino] and [whiteCupertino] respectively. Otherwise they are [blackMountainView] and [whiteMountainView]. If [platform] is null then both [black] and [white] must be specified.

The default values for [englishLike], [dense], and [tall] are [englishLike2021], [dense2021], and [tall2021].

See also:

- <https://m3.material.io/styles/typography>

### black

```dart
TextTheme black
```

A Material Design text theme with dark glyphs.

This [TextTheme] should provide color but not geometry (font size, weight, etc). A text theme's geometry depends on the locale. To look up a localized [TextTheme], use the overall [Theme], for example: `Theme.of(context).textTheme`.

The [englishLike], [dense], and [tall] text theme's provide locale-specific geometry.

### white

```dart
TextTheme white
```

A Material Design text theme with light glyphs.

This [TextTheme] provides color but not geometry (font size, weight, etc). A text theme's geometry depends on the locale. To look up a localized [TextTheme], use the overall [Theme], for example: `Theme.of(context).textTheme`.

The [englishLike], [dense], and [tall] text theme's provide locale-specific geometry.

### englishLike

```dart
TextTheme englishLike
```

Defines text geometry for `ScriptCategory.englishLike` scripts, such as English, French, Russian, etc.

This text theme is merged with either [black] or [white], depending on the overall [ThemeData.brightness], when the current locale's [MaterialLocalizations.scriptCategory] is `ScriptCategory.englishLike`.

To look up a localized [TextTheme], use the overall [Theme], for example: `Theme.of(context).textTheme`.

### dense

```dart
TextTheme dense
```

Defines text geometry for dense scripts, such as Chinese, Japanese and Korean.

This text theme is merged with either [black] or [white], depending on the overall [ThemeData.brightness], when the current locale's [MaterialLocalizations.scriptCategory] is `ScriptCategory.dense`.

To look up a localized [TextTheme], use the overall [Theme], for example: `Theme.of(context).textTheme`.

### tall

```dart
TextTheme tall
```

Defines text geometry for tall scripts, such as Farsi, Hindi, and Thai.

This text theme is merged with either [black] or [white], depending on the overall [ThemeData.brightness], when the current locale's [MaterialLocalizations.scriptCategory] is `ScriptCategory.tall`.

To look up a localized [TextTheme], use the overall [Theme], for example: `Theme.of(context).textTheme`.

### geometryThemeFor()

```dart
TextTheme geometryThemeFor(ScriptCategory category)
```

Returns one of [englishLike], [dense], or [tall].

### copyWith()

```dart
Typography copyWith({TextTheme? black, TextTheme? white, TextTheme? englishLike, TextTheme? dense, TextTheme? tall})
```

Creates a copy of this [Typography] with the given fields replaced by the non-null parameter values.

### lerp()

```dart
Typography lerp(Typography a, Typography b, double t)
```

Linearly interpolate between two [Typography] objects.

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

### blackMountainView

```dart
TextTheme blackMountainView
```

A Material Design text theme with dark glyphs based on Roboto.

This [TextTheme] provides color but not geometry (font size, weight, etc).

### whiteMountainView

```dart
TextTheme whiteMountainView
```

A Material Design text theme with light glyphs based on Roboto.

This [TextTheme] provides color but not geometry (font size, weight, etc).

### blackRedmond

```dart
TextTheme blackRedmond
```

A Material Design text theme with dark glyphs based on Segoe UI.

This [TextTheme] provides color but not geometry (font size, weight, etc).

### whiteRedmond

```dart
TextTheme whiteRedmond
```

A Material Design text theme with light glyphs based on Segoe UI.

This [TextTheme] provides color but not geometry (font size, weight, etc).

### blackHelsinki

```dart
TextTheme blackHelsinki
```

A Material Design text theme with dark glyphs based on Roboto, with fallback fonts that are likely (but not guaranteed) to be installed on Linux.

This [TextTheme] provides color but not geometry (font size, weight, etc).

### whiteHelsinki

```dart
TextTheme whiteHelsinki
```

A Material Design text theme with light glyphs based on Roboto, with fallbacks of DejaVu Sans, Liberation Sans and Arial.

This [TextTheme] provides color but not geometry (font size, weight, etc).

### blackCupertino

```dart
TextTheme blackCupertino
```

A Material Design text theme with dark glyphs based on San Francisco.

This [TextTheme] provides color but not geometry (font size, weight, etc).

This theme uses the iOS version of the font names.

### whiteCupertino

```dart
TextTheme whiteCupertino
```

A Material Design text theme with light glyphs based on San Francisco.

This [TextTheme] provides color but not geometry (font size, weight, etc).

This theme uses the iOS version of the font names.

### blackRedwoodCity

```dart
TextTheme blackRedwoodCity
```

A Material Design text theme with dark glyphs based on San Francisco.

This [TextTheme] provides color but not geometry (font size, weight, etc).

This theme uses the macOS version of the font names.

### whiteRedwoodCity

```dart
TextTheme whiteRedwoodCity
```

A Material Design text theme with light glyphs based on San Francisco.

This [TextTheme] provides color but not geometry (font size, weight, etc).

This theme uses the macOS version of the font names.

### englishLike2014

```dart
TextTheme englishLike2014
```

Defines text geometry for `ScriptCategory.englishLike` scripts, such as English, French, Russian, etc.

### englishLike2018

```dart
TextTheme englishLike2018
```

Defines text geometry for `ScriptCategory.englishLike` scripts, such as English, French, Russian, etc.

The font sizes, weights, and letter spacings in this version match the [2018 Material Design specification](https://material.io/go/design-typography#typography-styles).

### dense2014

```dart
TextTheme dense2014
```

Defines text geometry for dense scripts, such as Chinese, Japanese and Korean.

### dense2018

```dart
TextTheme dense2018
```

Defines text geometry for dense scripts, such as Chinese, Japanese and Korean.

The font sizes, weights, and letter spacings in this version match the 2018 [Material Design specification](https://material.io/go/design-typography#typography-styles).

### tall2014

```dart
TextTheme tall2014
```

Defines text geometry for tall scripts, such as Farsi, Hindi, and Thai.

### tall2018

```dart
TextTheme tall2018
```

Defines text geometry for tall scripts, such as Farsi, Hindi, and Thai.

The font sizes, weights, and letter spacings in this version match the 2018 [Material Design specification](https://material.io/go/design-typography#typography-styles).

### englishLike2021

```dart
TextTheme englishLike2021
```

Defines text geometry for `ScriptCategory.englishLike` scripts, such as English, French, Russian, etc.

The font sizes, weights, and letter spacings in this version match the [2021 Material Design 3 specification](https://m3.material.io/styles/typography/overview).

### dense2021

```dart
TextTheme dense2021
```

Defines text geometry for dense scripts, such as Chinese, Japanese and Korean.

The Material Design 3 specification does not include 'dense' text themes, so this is just here to be consistent with the API.

### tall2021

```dart
TextTheme tall2021
```

Defines text geometry for tall scripts, such as Farsi, Hindi, and Thai.

The Material Design 3 specification does not include 'tall' text themes, so this is just here to be consistent with the API.
