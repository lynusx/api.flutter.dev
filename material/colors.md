@docImport 'app.dart'; @docImport 'app_bar.dart'; @docImport 'app_bar_theme.dart'; @docImport 'color_scheme.dart'; @docImport 'data_table.dart'; @docImport 'expand_icon.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart'; @docImport 'typography.dart';

# MaterialColor

```dart
class MaterialColor extends ColorSwatch<int> {}
```

Defines a single color as well a color swatch with ten shades of the color.

The color's shades are referred to by index. The greater the index, the darker the color. There are 10 valid indices: 50, 100, 200, ..., 900. The value of this color should the same the value of index 500 and [shade500].

## Updating to [ColorScheme]

The [ColorScheme] is preferred for representing colors in applications that are configured for Material 3 (see [ThemeData.useMaterial3]). For more information on colors in Material 3 see the spec at <https://m3.material.io/styles/color/the-color-system>.

{@template flutter.material.colors.colorRoles} In Material 3, colors are represented using color roles and corresponding tokens. Each property in the [ColorScheme] class represents one color role as defined in the spec above. {@endtemplate}

### Material 3 Colors in Flutter

{@template flutter.material.colors.settingColors} Flutter's Material widgets can be assigned colors at the widget level using widget properties, or at the app level using theme classes.

For example, you can set the background of the [AppBar] by setting the [AppBar.backgroundColor] to a specific [Color] value.

To globally set the AppBar background color for your app, you can set the [ThemeData.appBarTheme] property for your [MaterialApp] using the [ThemeData] class. You can also override the default appearance of all the [AppBar]s in a widget subtree by placing the [AppBarTheme] at the root of the subtree.

Alternatively, you can set the [ThemeData.colorScheme] property to a custom [ColorScheme]. This creates a unified [ColorScheme] to be used across the app. The [AppBar.backgroundColor] uses the [ColorScheme.surface] by default. {@endtemplate}

### Migrating from [MaterialColor] to [ColorScheme]

In most cases, there are new properties in Flutter widgets that accept a [ColorScheme] instead of a [MaterialColor].

For example, you may have previously constructed a [ThemeData] using a primarySwatch:

```dart
ThemeData(
  primarySwatch: Colors.amber,
)
```

In Material 3, you can use the [ColorScheme] class to construct a [ThemeData] with the same color palette by using the [ColorScheme.fromSeed] constructor:

```dart
ThemeData(
 colorScheme: ColorScheme.fromSeed(seedColor: Colors.amber),
)
```

The [ColorScheme.fromSeed] constructor will generate a set of tonal palettes, which are used to create the color scheme.

Alternatively you can use the [ColorScheme.fromSwatch] constructor:

```dart
ThemeData(
 colorScheme: ColorScheme.fromSwatch(primarySwatch: Colors.amber),
)
```

The [ColorScheme.fromSwatch] constructor will create the color scheme directly from the specific color values used in the [MaterialColor].

See also:

- [Colors], which defines all of the standard material colors.

### MaterialColor()

```dart
MaterialColor(dynamic primary, dynamic swatch)
```

Creates a color swatch with a variety of shades.

The `primary` argument should be the 32 bit ARGB value of one of the values in the swatch, as would be passed to the [Color.new] constructor for that same color, and as is exposed by [value]. (This is distinct from the specific index of the color in the swatch.)

### shade50

```dart
Color get shade50
```

The lightest shade.

### shade100

```dart
Color get shade100
```

The second lightest shade.

### shade200

```dart
Color get shade200
```

The third lightest shade.

### shade300

```dart
Color get shade300
```

The fourth lightest shade.

### shade400

```dart
Color get shade400
```

The fifth lightest shade.

### shade500

```dart
Color get shade500
```

The default shade.

### shade600

```dart
Color get shade600
```

The fourth darkest shade.

### shade700

```dart
Color get shade700
```

The third darkest shade.

### shade800

```dart
Color get shade800
```

The second darkest shade.

### shade900

```dart
Color get shade900
```

The darkest shade.

# MaterialAccentColor

```dart
class MaterialAccentColor extends ColorSwatch<int> {}
```

Defines a single accent color as well a swatch of four shades of the accent color.

The color's shades are referred to by index, the colors with smaller indices are lighter, larger indices are darker. There are four valid indices: 100, 200, 400, and 700. The value of this color should be the same as the value of index 200 and [shade200].

See also:

- [Colors], which defines all of the standard material colors.
- <https://material.io/go/design-theming#color-color-schemes>

### MaterialAccentColor()

```dart
MaterialAccentColor(dynamic primary, dynamic swatch)
```

Creates a color swatch with a variety of shades appropriate for accent colors.

### shade100

```dart
Color get shade100
```

The lightest shade.

### shade200

```dart
Color get shade200
```

The default shade.

### shade400

```dart
Color get shade400
```

The second darkest shade.

### shade700

```dart
Color get shade700
```

The darkest shade.

# Colors

```dart
abstract final class Colors {}
```

[Color] and [ColorSwatch] constants which represent Material design's [color palette](https://material.io/design/color/).

Instead of using an absolute color from these palettes, consider using [Theme.of] to obtain the local [ThemeData.colorScheme], which defines the colors that most of the Material components use by default.

Most swatches have colors from 100 to 900 in increments of one hundred, plus the color 50. The smaller the number, the more pale the color. The greater the number, the darker the color. The accent swatches (e.g. [redAccent]) only have the values 100, 200, 400, and 700.

In addition, a series of blacks and whites with common opacities are available. For example, [black54] is a pure black with 54% opacity.

{@tool snippet}

To select a specific color from one of the swatches, index into the swatch using an integer for the specific color desired, as follows:

```dart
Color selection = Colors.green[400]!; // Selects a mid-range green.
```

{@end-tool} {@tool snippet}

Each [ColorSwatch] constant is a color and can used directly. For example:

```dart
Container(
  color: Colors.blue, // same as Colors.blue[500] or Colors.blue.shade500
)
```

{@end-tool}

## Color palettes

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueGrey.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.brown.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.grey.png)

## Blacks and whites

These colors are identified by their transparency. The low transparency levels (e.g. [Colors.white12] and [Colors.white10]) are very hard to see and should be avoided in general. They are intended for very subtle effects.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

The [Colors.transparent] color isn't shown here because it is entirely invisible!

See also:

- Cookbook: [Use themes to share colors and font styles](https://docs.flutter.dev/cookbook/design/themes)

### transparent

```dart
Color transparent
```

Completely invisible.

### black

```dart
Color black
```

Completely opaque black.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

See also:

- [black87], [black54], [black45], [black38], [black26], [black12], which are variants on this color but with different opacities.
- [white], a solid white color.
- [transparent], a fully-transparent color.

### black87

```dart
Color black87
```

Black with 87% opacity.

This is a good contrasting color for text in light themes.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

See also:

- [Typography.black], which uses this color for its text styles.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [black], [black54], [black45], [black38], [black26], [black12], which are variants on this color but with different opacities.

### black54

```dart
Color black54
```

Black with 54% opacity.

This is a color commonly used for headings in light themes. It's also used as the mask color behind dialogs.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

See also:

- [Typography.black], which uses this color for its text styles.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [black], [black87], [black45], [black38], [black26], [black12], which are variants on this color but with different opacities.

### black45

```dart
Color black45
```

Black with 45% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

See also:

- [black], [black87], [black54], [black38], [black26], [black12], which are variants on this color but with different opacities.

### black38

```dart
Color black38
```

Black with 38% opacity.

For light themes, i.e. when the Theme's [ThemeData.brightness] is [Brightness.light], this color is used for disabled icons and for placeholder text in [DataTable].

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

See also:

- [black], [black87], [black54], [black45], [black26], [black12], which are variants on this color but with different opacities.

### black26

```dart
Color black26
```

Black with 26% opacity.

Used for disabled radio buttons and the text of disabled flat buttons in light themes.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

See also:

- [ThemeData.disabledColor], which uses this color by default in light themes.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [black], [black87], [black54], [black45], [black38], [black12], which are variants on this color but with different opacities.

### black12

```dart
Color black12
```

Black with 12% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blacks.png)

Used for the background of disabled raised buttons in light themes.

See also:

- [black], [black87], [black54], [black45], [black38], [black26], which are variants on this color but with different opacities.

### white

```dart
Color white
```

Completely opaque white.

This is a good contrasting color for the [ThemeData.primaryColor] in the dark theme. See [ThemeData.brightness].

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [Typography.white], which uses this color for its text styles.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [white70], [white60], [white54], [white38], [white30], [white12], [white10], which are variants on this color but with different opacities.
- [black], a solid black color.
- [transparent], a fully-transparent color.

### white70

```dart
Color white70
```

White with 70% opacity.

This is a color commonly used for headings in dark themes.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [Typography.white], which uses this color for its text styles.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [white], [white60], [white54], [white38], [white30], [white12], [white10], which are variants on this color but with different opacities.

### white60

```dart
Color white60
```

White with 60% opacity.

Used for medium-emphasis text and hint text when [ThemeData.brightness] is set to [Brightness.dark].

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [ExpandIcon], which uses this color for dark themes.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [white], [white54], [white30], [white38], [white12], [white10], which are variants on this color but with different opacities.

### white54

```dart
Color white54
```

White with 54% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [white], [white60], [white38], [white30], [white12], [white10], which are variants on this color but with different opacities.

### white38

```dart
Color white38
```

White with 38% opacity.

Used for disabled radio buttons and the text of disabled flat buttons in dark themes.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [ThemeData.disabledColor], which uses this color by default in dark themes.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [white], [white60], [white54], [white70], [white30], [white12], [white10], which are variants on this color but with different opacities.

### white30

```dart
Color white30
```

White with 30% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.
- [white], [white60], [white54], [white70], [white38], [white12], [white10], which are variants on this color but with different opacities.

### white24

```dart
Color white24
```

White with 24% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

Used for the splash color for filled buttons.

See also:

- [white], [white60], [white54], [white70], [white38], [white30], [white10], which are variants on this color but with different opacities.

### white12

```dart
Color white12
```

White with 12% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

Used for the background of disabled raised buttons in dark themes.

See also:

- [white], [white60], [white54], [white70], [white38], [white30], [white10], which are variants on this color but with different opacities.

### white10

```dart
Color white10
```

White with 10% opacity.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.whites.png)

See also:

- [white], [white60], [white54], [white70], [white38], [white30], [white12], which are variants on this color but with different opacities.
- [transparent], a fully-transparent color, not far from this one.

### red

```dart
MaterialColor red
```

The red primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.red[400],
)
```

{@end-tool}

See also:

- [redAccent], the corresponding accent colors.
- [deepOrange] and [pink], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### redAccent

```dart
MaterialAccentColor redAccent
```

The red accent swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.redAccent[400],
)
```

{@end-tool}

See also:

- [red], the corresponding primary colors.
- [deepOrangeAccent] and [pinkAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### pink

```dart
MaterialColor pink
```

The pink primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.pink[400],
)
```

{@end-tool}

See also:

- [pinkAccent], the corresponding accent colors.
- [red] and [purple], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### pinkAccent

```dart
MaterialAccentColor pinkAccent
```

The pink accent color swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.pinkAccent[400],
)
```

{@end-tool}

See also:

- [pink], the corresponding primary colors.
- [redAccent] and [purpleAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### purple

```dart
MaterialColor purple
```

The purple primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.purple[400],
)
```

{@end-tool}

See also:

- [purpleAccent], the corresponding accent colors.
- [deepPurple] and [pink], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### purpleAccent

```dart
MaterialAccentColor purpleAccent
```

The purple accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pink.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.pinkAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.purpleAccent[400],
)
```

{@end-tool}

See also:

- [purple], the corresponding primary colors.
- [deepPurpleAccent] and [pinkAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### deepPurple

```dart
MaterialColor deepPurple
```

The deep purple primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.deepPurple[400],
)
```

{@end-tool}

See also:

- [deepPurpleAccent], the corresponding accent colors.
- [purple] and [indigo], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### deepPurpleAccent

```dart
MaterialAccentColor deepPurpleAccent
```

The deep purple accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.purpleAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.deepPurpleAccent[400],
)
```

{@end-tool}

See also:

- [deepPurple], the corresponding primary colors.
- [purpleAccent] and [indigoAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### indigo

```dart
MaterialColor indigo
```

The indigo primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.indigo[400],
)
```

{@end-tool}

See also:

- [indigoAccent], the corresponding accent colors.
- [blue] and [deepPurple], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### indigoAccent

```dart
MaterialAccentColor indigoAccent
```

The indigo accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurple.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepPurpleAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.indigoAccent[400],
)
```

{@end-tool}

See also:

- [indigo], the corresponding primary colors.
- [blueAccent] and [deepPurpleAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### blue

```dart
MaterialColor blue
```

The blue primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueGrey.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.blue[400],
)
```

{@end-tool}

See also:

- [blueAccent], the corresponding accent colors.
- [indigo], [lightBlue], and [blueGrey], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### blueAccent

```dart
MaterialAccentColor blueAccent
```

The blue accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigo.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.indigoAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.blueAccent[400],
)
```

{@end-tool}

See also:

- [blue], the corresponding primary colors.
- [indigoAccent] and [lightBlueAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### lightBlue

```dart
MaterialColor lightBlue
```

The light blue primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.lightBlue[400],
)
```

{@end-tool}

See also:

- [lightBlueAccent], the corresponding accent colors.
- [blue] and [cyan], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### lightBlueAccent

```dart
MaterialAccentColor lightBlueAccent
```

The light blue accent swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.lightBlueAccent[400],
)
```

{@end-tool}

See also:

- [lightBlue], the corresponding primary colors.
- [blueAccent] and [cyanAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### cyan

```dart
MaterialColor cyan
```

The cyan primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueGrey.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.cyan[400],
)
```

{@end-tool}

See also:

- [cyanAccent], the corresponding accent colors.
- [lightBlue], [teal], and [blueGrey], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### cyanAccent

```dart
MaterialAccentColor cyanAccent
```

The cyan accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlue.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightBlueAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.cyanAccent[400],
)
```

{@end-tool}

See also:

- [cyan], the corresponding primary colors.
- [lightBlueAccent] and [tealAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### teal

```dart
MaterialColor teal
```

The teal primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.teal[400],
)
```

{@end-tool}

See also:

- [tealAccent], the corresponding accent colors.
- [green] and [cyan], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### tealAccent

```dart
MaterialAccentColor tealAccent
```

The teal accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyanAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.tealAccent[400],
)
```

{@end-tool}

See also:

- [teal], the corresponding primary colors.
- [greenAccent] and [cyanAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### green

```dart
MaterialColor green
```

The green primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.green[400],
)
```

{@end-tool}

See also:

- [greenAccent], the corresponding accent colors.
- [teal], [lightGreen], and [lime], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### greenAccent

```dart
MaterialAccentColor greenAccent
```

The green accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.teal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.tealAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.greenAccent[400],
)
```

{@end-tool}

See also:

- [green], the corresponding primary colors.
- [tealAccent], [lightGreenAccent], and [limeAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### lightGreen

```dart
MaterialColor lightGreen
```

The light green primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.lightGreen[400],
)
```

{@end-tool}

See also:

- [lightGreenAccent], the corresponding accent colors.
- [green] and [lime], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### lightGreenAccent

```dart
MaterialAccentColor lightGreenAccent
```

The light green accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.green.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.greenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.lightGreenAccent[400],
)
```

{@end-tool}

See also:

- [lightGreen], the corresponding primary colors.
- [greenAccent] and [limeAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### lime

```dart
MaterialColor lime
```

The lime primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.lime[400],
)
```

{@end-tool}

See also:

- [limeAccent], the corresponding accent colors.
- [lightGreen] and [yellow], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### limeAccent

```dart
MaterialAccentColor limeAccent
```

The lime accent primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreen.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lightGreenAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.limeAccent[400],
)
```

{@end-tool}

See also:

- [lime], the corresponding primary colors.
- [lightGreenAccent] and [yellowAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### yellow

```dart
MaterialColor yellow
```

The yellow primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.yellow[400],
)
```

{@end-tool}

See also:

- [yellowAccent], the corresponding accent colors.
- [lime] and [amber], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### yellowAccent

```dart
MaterialAccentColor yellowAccent
```

The yellow accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.lime.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.limeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.yellowAccent[400],
)
```

{@end-tool}

See also:

- [yellow], the corresponding primary colors.
- [limeAccent] and [amberAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### amber

```dart
MaterialColor amber
```

The amber primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.amber[400],
)
```

{@end-tool}

See also:

- [amberAccent], the corresponding accent colors.
- [yellow] and [orange], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### amberAccent

```dart
MaterialAccentColor amberAccent
```

The amber accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellow.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.yellowAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.amberAccent[400],
)
```

{@end-tool}

See also:

- [amber], the corresponding primary colors.
- [yellowAccent] and [orangeAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### orange

```dart
MaterialColor orange
```

The orange primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.brown.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.orange[400],
)
```

{@end-tool}

See also:

- [orangeAccent], the corresponding accent colors.
- [amber], [deepOrange], and [brown], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### orangeAccent

```dart
MaterialAccentColor orangeAccent
```

The orange accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amber.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.amberAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.orangeAccent[400],
)
```

{@end-tool}

See also:

- [orange], the corresponding primary colors.
- [amberAccent] and [deepOrangeAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### deepOrange

```dart
MaterialColor deepOrange
```

The deep orange primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.brown.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.deepOrange[400],
)
```

{@end-tool}

See also:

- [deepOrangeAccent], the corresponding accent colors.
- [orange], [red], and [brown], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### deepOrangeAccent

```dart
MaterialAccentColor deepOrangeAccent
```

The deep orange accent color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.deepOrangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orangeAccent.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.red.png) ![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.redAccent.png)

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.deepOrangeAccent[400],
)
```

{@end-tool}

See also:

- [deepOrange], the corresponding primary colors.
- [orangeAccent] [redAccent], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### brown

```dart
MaterialColor brown
```

The brown primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.brown.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.orange.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueGrey.png)

This swatch has no corresponding accent color and swatch.

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.brown[400],
)
```

{@end-tool}

See also:

- [orange] and [blueGrey], vaguely similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### grey

```dart
MaterialColor grey
```

The grey primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.grey.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueGrey.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.brown.png)

This swatch has no corresponding accent swatch.

This swatch, in addition to the values 50 and 100 to 900 in 100 increments, also features the special values 350 and 850. The 350 value is used for raised button while pressed in light themes, and 850 is used for the background color of the dark theme. See [ThemeData.brightness].

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.grey[400],
)
```

{@end-tool}

See also:

- [blueGrey] and [brown], somewhat similar colors.
- [black], [black87], [black54], [black45], [black38], [black26], [black12], which provide a different approach to showing shades of grey.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### blueGrey

```dart
MaterialColor blueGrey
```

The blue-grey primary color and swatch.

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blueGrey.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.grey.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.cyan.png)

![](https://flutter.github.io/assets-for-api-docs/assets/material/Colors.blue.png)

This swatch has no corresponding accent swatch.

{@tool snippet}

```dart
Icon(
  Icons.widgets,
  color: Colors.blueGrey[400],
)
```

{@end-tool}

See also:

- [grey], [cyan], and [blue], similar colors.
- [Theme.of], which allows you to select colors from the current theme rather than hard-coding colors in your build methods.

### primaries

```dart
List<MaterialColor> primaries
```

The Material Design primary color swatches, excluding grey.

### accents

```dart
List<MaterialAccentColor> accents
```

The Material Design accent color swatches.
