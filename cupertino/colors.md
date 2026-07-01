@docImport 'package:flutter/material.dart';

@docImport 'button.dart'; @docImport 'nav_bar.dart';

# CupertinoColors

```dart
abstract final class CupertinoColors {}
```

A palette of [Color] constants that describe colors commonly used when matching the iOS platform aesthetics.

## Color palettes

### Basic Colors

![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_basic_colors.png)

### Active Colors

![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_active_colors.png)

### System Colors

![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_system_colors_1.png) ![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_system_colors_2.png) ![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_system_colors_3.png)

### Label Colors

![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_label_colors.png)

### Background Colors

![](https://flutter.github.io/assets-for-api-docs/assets/cupertino/cupertino_background_colors.png)

### activeBlue

```dart
CupertinoDynamicColor activeBlue
```

iOS 13's default blue color. Used to indicate active elements such as buttons, selected tabs and your own chat bubbles.

This is SystemBlue in the iOS palette.

### activeGreen

```dart
CupertinoDynamicColor activeGreen
```

iOS 13's default green color. Used to indicate active accents such as the switch in its on state and some accent buttons such as the call button and Apple Map's 'Go' button.

This is SystemGreen in the iOS palette.

### activeOrange

```dart
CupertinoDynamicColor activeOrange
```

iOS 13's orange color.

This is SystemOrange in the iOS palette.

### white

```dart
Color white
```

Opaque white color. Used for backgrounds and fonts against dark backgrounds.

This is SystemWhiteColor in the iOS palette.

See also:

- [Colors.white], the same color, in the Material Design palette.
- [black], opaque black in the [CupertinoColors] palette.

### black

```dart
Color black
```

Opaque black color. Used for texts against light backgrounds.

This is SystemBlackColor in the iOS palette.

See also:

- [Colors.black], the same color, in the Material Design palette.
- [white], opaque white in the [CupertinoColors] palette.

### transparent

```dart
Color transparent
```

A fully-transparent color, completely invisible.

See also:

- [Colors.transparent], the same color, in the Material Design palette.

### lightBackgroundGray

```dart
Color lightBackgroundGray
```

Used in iOS 10 for light background fills such as the chat bubble background.

This is SystemLightGrayColor in the iOS palette.

### extraLightBackgroundGray

```dart
Color extraLightBackgroundGray
```

Used in iOS 12 for very light background fills in tables between cell groups.

This is SystemExtraLightGrayColor in the iOS palette.

### darkBackgroundGray

```dart
Color darkBackgroundGray
```

Used in iOS 12 for very dark background fills in tables between cell groups in dark mode.

### inactiveGray

```dart
CupertinoDynamicColor inactiveGray
```

Used in iOS 13 for unselected selectables such as tab bar items in their inactive state or de-emphasized subtitles and details text.

Not the same grey as disabled buttons etc.

This is the disabled color in the iOS palette.

### destructiveRed

```dart
CupertinoDynamicColor destructiveRed
```

Used for iOS 13 for destructive actions such as the delete actions in table view cells and dialogs.

Not the same red as the camera shutter or springboard icon notifications or the foreground red theme in various native apps such as HealthKit.

This is SystemRed in the iOS palette.

### systemBlue

```dart
CupertinoDynamicColor systemBlue
```

A blue color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemBlue](https://developer.apple.com/documentation/uikit/uicolor/3173141-systemblue), the `UIKit` equivalent.

### systemGreen

```dart
CupertinoDynamicColor systemGreen
```

A green color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemGreen](https://developer.apple.com/documentation/uikit/uicolor/3173144-systemgreen), the `UIKit` equivalent.

### systemMint

```dart
CupertinoDynamicColor systemMint
```

A mint color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemMint](https://developer.apple.com/documentation/uikit/uicolor/3852741-systemmint), the `UIKit` equivalent.

### systemIndigo

```dart
CupertinoDynamicColor systemIndigo
```

An indigo color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemIndigo](https://developer.apple.com/documentation/uikit/uicolor/3173146-systemindigo), the `UIKit` equivalent.

### systemOrange

```dart
CupertinoDynamicColor systemOrange
```

An orange color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemOrange](https://developer.apple.com/documentation/uikit/uicolor/3173147-systemorange), the `UIKit` equivalent.

### systemPink

```dart
CupertinoDynamicColor systemPink
```

A pink color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemPink](https://developer.apple.com/documentation/uikit/uicolor/3173148-systempink), the `UIKit` equivalent.

### systemBrown

```dart
CupertinoDynamicColor systemBrown
```

A brown color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemBrown](https://developer.apple.com/documentation/uikit/uicolor/3173142-systembrown), the `UIKit` equivalent.

### systemPurple

```dart
CupertinoDynamicColor systemPurple
```

A purple color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemPurple](https://developer.apple.com/documentation/uikit/uicolor/3173149-systempurple), the `UIKit` equivalent.

### systemRed

```dart
CupertinoDynamicColor systemRed
```

A red color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemRed](https://developer.apple.com/documentation/uikit/uicolor/3173150-systemred), the `UIKit` equivalent.

### systemTeal

```dart
CupertinoDynamicColor systemTeal
```

A teal color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemTeal](https://developer.apple.com/documentation/uikit/uicolor/3173151-systemteal), the `UIKit` equivalent.

### systemCyan

```dart
CupertinoDynamicColor systemCyan
```

A cyan color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemCyan](https://developer.apple.com/documentation/uikit/uicolor/3852740-systemcyan), the `UIKit` equivalent.

### systemYellow

```dart
CupertinoDynamicColor systemYellow
```

A yellow color that can adapt to the given [BuildContext].

See also:

- [UIColor.systemYellow](https://developer.apple.com/documentation/uikit/uicolor/3173152-systemyellow), the `UIKit` equivalent.

### systemGrey

```dart
CupertinoDynamicColor systemGrey
```

The base grey color.

See also:

- [UIColor.systemGray](https://developer.apple.com/documentation/uikit/uicolor/3173143-systemgray), the `UIKit` equivalent.

### systemGrey2

```dart
CupertinoDynamicColor systemGrey2
```

A second-level shade of grey.

See also:

- [UIColor.systemGray2](https://developer.apple.com/documentation/uikit/uicolor/3255071-systemgray2), the `UIKit` equivalent.

### systemGrey3

```dart
CupertinoDynamicColor systemGrey3
```

A third-level shade of grey.

See also:

- [UIColor.systemGray3](https://developer.apple.com/documentation/uikit/uicolor/3255072-systemgray3), the `UIKit` equivalent.

### systemGrey4

```dart
CupertinoDynamicColor systemGrey4
```

A fourth-level shade of grey.

See also:

- [UIColor.systemGray4](https://developer.apple.com/documentation/uikit/uicolor/3255073-systemgray4), the `UIKit` equivalent.

### systemGrey5

```dart
CupertinoDynamicColor systemGrey5
```

A fifth-level shade of grey.

See also:

- [UIColor.systemGray5](https://developer.apple.com/documentation/uikit/uicolor/3255074-systemgray5), the `UIKit` equivalent.

### systemGrey6

```dart
CupertinoDynamicColor systemGrey6
```

A sixth-level shade of grey.

See also:

- [UIColor.systemGray6](https://developer.apple.com/documentation/uikit/uicolor/3255075-systemgray6), the `UIKit` equivalent.

### label

```dart
CupertinoDynamicColor label
```

The color for text labels containing primary content, equivalent to [UIColor.label](https://developer.apple.com/documentation/uikit/uicolor/3173131-label).

### secondaryLabel

```dart
CupertinoDynamicColor secondaryLabel
```

The color for text labels containing secondary content, equivalent to [UIColor.secondaryLabel](https://developer.apple.com/documentation/uikit/uicolor/3173136-secondarylabel).

### tertiaryLabel

```dart
CupertinoDynamicColor tertiaryLabel
```

The color for text labels containing tertiary content, equivalent to [UIColor.tertiaryLabel](https://developer.apple.com/documentation/uikit/uicolor/3173153-tertiarylabel).

### quaternaryLabel

```dart
CupertinoDynamicColor quaternaryLabel
```

The color for text labels containing quaternary content, equivalent to [UIColor.quaternaryLabel](https://developer.apple.com/documentation/uikit/uicolor/3173135-quaternarylabel).

### systemFill

```dart
CupertinoDynamicColor systemFill
```

An overlay fill color for thin and small shapes, equivalent to [UIColor.systemFill](https://developer.apple.com/documentation/uikit/uicolor/3255070-systemfill).

### secondarySystemFill

```dart
CupertinoDynamicColor secondarySystemFill
```

An overlay fill color for medium-size shapes, equivalent to [UIColor.secondarySystemFill](https://developer.apple.com/documentation/uikit/uicolor/3255069-secondarysystemfill).

### tertiarySystemFill

```dart
CupertinoDynamicColor tertiarySystemFill
```

An overlay fill color for large shapes, equivalent to [UIColor.tertiarySystemFill](https://developer.apple.com/documentation/uikit/uicolor/3255076-tertiarysystemfill).

### quaternarySystemFill

```dart
CupertinoDynamicColor quaternarySystemFill
```

An overlay fill color for large areas containing complex content, equivalent to [UIColor.quaternarySystemFill](https://developer.apple.com/documentation/uikit/uicolor/3255068-quaternarysystemfill).

### placeholderText

```dart
CupertinoDynamicColor placeholderText
```

The color for placeholder text in controls or text views, equivalent to [UIColor.placeholderText](https://developer.apple.com/documentation/uikit/uicolor/3173134-placeholdertext).

### systemBackground

```dart
CupertinoDynamicColor systemBackground
```

The color for the main background of your interface, equivalent to [UIColor.systemBackground](https://developer.apple.com/documentation/uikit/uicolor/3173140-systembackground).

Typically used for designs that have a white primary background in a light environment.

### secondarySystemBackground

```dart
CupertinoDynamicColor secondarySystemBackground
```

The color for content layered on top of the main background, equivalent to [UIColor.secondarySystemBackground](https://developer.apple.com/documentation/uikit/uicolor/3173137-secondarysystembackground).

Typically used for designs that have a white primary background in a light environment.

### tertiarySystemBackground

```dart
CupertinoDynamicColor tertiarySystemBackground
```

The color for content layered on top of secondary backgrounds, equivalent to [UIColor.tertiarySystemBackground](https://developer.apple.com/documentation/uikit/uicolor/3173154-tertiarysystembackground).

Typically used for designs that have a white primary background in a light environment.

### systemGroupedBackground

```dart
CupertinoDynamicColor systemGroupedBackground
```

The color for the main background of your grouped interface, equivalent to [UIColor.systemGroupedBackground](https://developer.apple.com/documentation/uikit/uicolor/3173145-systemgroupedbackground).

Typically used for grouped content, including table views and platter-based designs.

### secondarySystemGroupedBackground

```dart
CupertinoDynamicColor secondarySystemGroupedBackground
```

The color for content layered on top of the main background of your grouped interface, equivalent to [UIColor.secondarySystemGroupedBackground](https://developer.apple.com/documentation/uikit/uicolor/3173138-secondarysystemgroupedbackground).

Typically used for grouped content, including table views and platter-based designs.

### tertiarySystemGroupedBackground

```dart
CupertinoDynamicColor tertiarySystemGroupedBackground
```

The color for content layered on top of secondary backgrounds of your grouped interface, equivalent to [UIColor.tertiarySystemGroupedBackground](https://developer.apple.com/documentation/uikit/uicolor/3173155-tertiarysystemgroupedbackground).

Typically used for grouped content, including table views and platter-based designs.

### separator

```dart
CupertinoDynamicColor separator
```

The color for thin borders or divider lines that allows some underlying content to be visible, equivalent to [UIColor.separator](https://developer.apple.com/documentation/uikit/uicolor/3173139-separator).

### opaqueSeparator

```dart
CupertinoDynamicColor opaqueSeparator
```

The color for borders or divider lines that hide any underlying content, equivalent to [UIColor.opaqueSeparator](https://developer.apple.com/documentation/uikit/uicolor/3173133-opaqueseparator).

### link

```dart
CupertinoDynamicColor link
```

The color for links, equivalent to [UIColor.link](https://developer.apple.com/documentation/uikit/uicolor/3173132-link).

# CupertinoDynamicColor

```dart
class CupertinoDynamicColor with Diagnosticable implements Color {}
```

A [Color] subclass that represents a family of colors, and the correct effective color in the color family.

When used as a regular color, [CupertinoDynamicColor] is equivalent to the effective color (i.e. [CupertinoDynamicColor.value] will come from the effective color), which is determined by the [BuildContext] it is last resolved against. If it has never been resolved, the light, normal contrast, base elevation variant [CupertinoDynamicColor.color] will be the default effective color.

Sometimes manually resolving a [CupertinoDynamicColor] is not necessary, because the Cupertino Library provides built-in support for it.

### Using [CupertinoDynamicColor] in a Cupertino widget

When a Cupertino widget is provided with a [CupertinoDynamicColor], either directly in its constructor, or from an [InheritedWidget] it depends on (for example, [DefaultTextStyle]), the widget will automatically resolve the color using [CupertinoDynamicColor.resolve] against its own [BuildContext], on a best-effort basis.

{@tool snippet} By default a [CupertinoButton] has no background color. The following sample code shows how to build a [CupertinoButton] that appears white in light mode, and changes automatically to black in dark mode.

```dart
CupertinoButton(
  // CupertinoDynamicColor works out of box in a CupertinoButton.
  color: const CupertinoDynamicColor.withBrightness(
    color: CupertinoColors.white,
    darkColor: CupertinoColors.black,
  ),
  onPressed: () { },
  child: child,
)
```

{@end-tool}

### Using a [CupertinoDynamicColor] from a [CupertinoTheme]

When referring to a [CupertinoTheme] color, generally the color will already have adapted to the ambient [BuildContext], because [CupertinoTheme.of] implicitly resolves all the colors used in the retrieved [CupertinoThemeData], before returning it.

{@tool snippet} The following code sample creates a [Container] with the `primaryColor` of the current theme. If `primaryColor` is a [CupertinoDynamicColor], the container will be adaptive, thanks to [CupertinoTheme.of]: it will switch to `primaryColor`'s dark variant once dark mode is turned on, and turns to primaryColor`'s high contrast variant when [MediaQueryData.highContrast] is requested in the ambient [MediaQuery], etc.

```dart
Container(
  // Container is not a Cupertino widget, but CupertinoTheme.of implicitly
  // resolves colors used in the retrieved CupertinoThemeData.
  color: CupertinoTheme.of(context).primaryColor,
)
```

{@end-tool}

### Manually Resolving a [CupertinoDynamicColor]

When used to configure a non-Cupertino widget, or wrapped in an object opaque to the receiving Cupertino component, a [CupertinoDynamicColor] may need to be manually resolved using [CupertinoDynamicColor.resolve], before it can used to paint. For example, to use a custom [Border] in a [CupertinoNavigationBar], the colors used in the [Border] have to be resolved manually before being passed to [CupertinoNavigationBar]'s constructor.

{@tool snippet}

The following code samples demonstrate two cases where you have to manually resolve a [CupertinoDynamicColor].

```dart
CupertinoNavigationBar(
  // CupertinoNavigationBar does not know how to resolve colors used in
  // a Border class.
  border: Border(
    bottom: BorderSide(
      color: CupertinoDynamicColor.resolve(CupertinoColors.systemBlue, context),
    ),
  ),
)
```

```dart
Container(
  // Container is not a Cupertino widget.
  color: CupertinoDynamicColor.resolve(CupertinoColors.systemBlue, context),
)
```

{@end-tool}

See also:

- [CupertinoUserInterfaceLevel], an [InheritedWidget] that may affect color resolution of a [CupertinoDynamicColor].
- [CupertinoTheme.of], a static method that retrieves the ambient [CupertinoThemeData], and then resolves [CupertinoDynamicColor]s used in the retrieved data.

### CupertinoDynamicColor()

```dart
CupertinoDynamicColor({String? debugLabel, required Color color, required Color darkColor, required Color highContrastColor, required Color darkHighContrastColor, required Color elevatedColor, required Color darkElevatedColor, required Color highContrastElevatedColor, required Color darkHighContrastElevatedColor})
```

Creates an adaptive [Color] that changes its effective color based on the [BuildContext] given. The default effective color is [color].

### CupertinoDynamicColor.withBrightnessAndContrast()

```dart
CupertinoDynamicColor.withBrightnessAndContrast({String? debugLabel, required Color color, required Color darkColor, required Color highContrastColor, required Color darkHighContrastColor})
```

Creates an adaptive [Color] that changes its effective color based on the given [BuildContext]'s brightness (from [MediaQueryData.platformBrightness] or [CupertinoThemeData.brightness]) and accessibility contrast setting ([MediaQueryData.highContrast]). The default effective color is [color].

### CupertinoDynamicColor.withBrightness()

```dart
CupertinoDynamicColor.withBrightness({String? debugLabel, required Color color, required Color darkColor})
```

Creates an adaptive [Color] that changes its effective color based on the given [BuildContext]'s brightness (from [MediaQueryData.platformBrightness] or [CupertinoThemeData.brightness]). The default effective color is [color].

### color

```dart
Color color
```

The color to use when the [BuildContext] implies a combination of light mode, normal contrast, and base interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.light], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.light].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `false`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.base].

### darkColor

```dart
Color darkColor
```

The color to use when the [BuildContext] implies a combination of dark mode, normal contrast, and base interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.dark], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.dark].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `false`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.base].

### highContrastColor

```dart
Color highContrastColor
```

The color to use when the [BuildContext] implies a combination of light mode, high contrast, and base interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.light], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.light].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `true`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.base].

### darkHighContrastColor

```dart
Color darkHighContrastColor
```

The color to use when the [BuildContext] implies a combination of dark mode, high contrast, and base interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.dark], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.dark].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `true`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.base].

### elevatedColor

```dart
Color elevatedColor
```

The color to use when the [BuildContext] implies a combination of light mode, normal contrast, and elevated interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.light], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.light].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `false`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.elevated].

### darkElevatedColor

```dart
Color darkElevatedColor
```

The color to use when the [BuildContext] implies a combination of dark mode, normal contrast, and elevated interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.dark], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.dark].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `false`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.elevated].

### highContrastElevatedColor

```dart
Color highContrastElevatedColor
```

The color to use when the [BuildContext] implies a combination of light mode, high contrast, and elevated interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.light], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.light].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `true`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.elevated].

### darkHighContrastElevatedColor

```dart
Color darkHighContrastElevatedColor
```

The color to use when the [BuildContext] implies a combination of dark mode, high contrast, and elevated interface elevation.

In other words, this color will be the effective color of the [CupertinoDynamicColor] after it is resolved against a [BuildContext] that:

- has a [CupertinoTheme] whose [CupertinoThemeData.brightness] is [Brightness.dark], or a [MediaQuery] whose [MediaQueryData.platformBrightness] is [Brightness.dark].
- has a [MediaQuery] whose [MediaQueryData.highContrast] is `true`.
- has a [CupertinoUserInterfaceLevel] that indicates [CupertinoUserInterfaceLevelData.elevated].

### resolve()

```dart
Color resolve(Color resolvable, BuildContext context)
```

Resolves the given [Color] by calling [resolveFrom].

If the given color is already a concrete [Color], it will be returned as is. If the given color is a [CupertinoDynamicColor], but the given [BuildContext] lacks the dependencies required to the color resolution, the default trait value will be used ([Brightness.light] platform brightness, normal contrast, [CupertinoUserInterfaceLevelData.base] elevation level).

See also:

- [maybeResolve], which is similar to this function, but will allow a null `resolvable` color.

### maybeResolve()

```dart
Color? maybeResolve(Color? resolvable, BuildContext context)
```

Resolves the given [Color] by calling [resolveFrom].

If the given color is already a concrete [Color], it will be returned as is. If the given color is null, returns null. If the given color is a [CupertinoDynamicColor], but the given [BuildContext] lacks the dependencies required to the color resolution, the default trait value will be used ([Brightness.light] platform brightness, normal contrast, [CupertinoUserInterfaceLevelData.base] elevation level).

See also:

- [resolve], which is similar to this function, but returns a non-nullable value, and does not allow a null `resolvable` color.

### resolveFrom()

```dart
CupertinoDynamicColor resolveFrom(BuildContext context)
```

Resolves this [CupertinoDynamicColor] using the provided [BuildContext].

Calling this method will create a new [CupertinoDynamicColor] that is almost identical to this [CupertinoDynamicColor], except the effective color is changed to adapt to the given [BuildContext].

For example, if the given [BuildContext] indicates the widgets in the subtree should be displayed in dark mode (the surrounding [CupertinoTheme]'s [CupertinoThemeData.brightness] or [MediaQuery]'s [MediaQueryData.platformBrightness] is [Brightness.dark]), with a high accessibility contrast (the surrounding [MediaQuery]'s [MediaQueryData.highContrast] is `true`), and an elevated interface elevation (the surrounding [CupertinoUserInterfaceLevel]'s `data` is [CupertinoUserInterfaceLevelData.elevated]), the resolved [CupertinoDynamicColor] will be the same as this [CupertinoDynamicColor], except its effective color will be the `darkHighContrastElevatedColor` variant from the original [CupertinoDynamicColor].

Calling this function may create dependencies on the closest instance of some [InheritedWidget]s that enclose the given [BuildContext]. E.g., if [darkColor] is different from [color], this method will call [CupertinoTheme.maybeBrightnessOf] in an effort to determine the brightness. If [color] is different from [highContrastColor], this method will call [MediaQuery.maybeHighContrastOf] in an effort to determine the high contrast setting.

If any of the required dependencies are missing from the given context, the default value of that trait will be used ([Brightness.light] platform brightness, normal contrast, [CupertinoUserInterfaceLevelData.base] elevation level).

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
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### value

```dart
int get value
```

### toARGB32()

```dart
int toARGB32()
```

### alpha

```dart
int get alpha
```

### blue

```dart
int get blue
```

### computeLuminance()

```dart
double computeLuminance()
```

### green

```dart
int get green
```

### opacity

```dart
double get opacity
```

### red

```dart
int get red
```

### withAlpha()

```dart
Color withAlpha(int a)
```

### withBlue()

```dart
Color withBlue(int b)
```

### withGreen()

```dart
Color withGreen(int g)
```

### withOpacity()

```dart
Color withOpacity(double opacity)
```

### withRed()

```dart
Color withRed(int r)
```

### a

```dart
double get a
```

### r

```dart
double get r
```

### g

```dart
double get g
```

### b

```dart
double get b
```

### colorSpace

```dart
ColorSpace get colorSpace
```

### withValues()

```dart
Color withValues({double? alpha, double? red, double? green, double? blue, ColorSpace? colorSpace})
```

# createCupertinoColorProperty()

```dart
DiagnosticsProperty<Color> createCupertinoColorProperty(String name, Color? value, {bool showName = true, Object? defaultValue = kNoDefaultValue, DiagnosticsTreeStyle style = DiagnosticsTreeStyle.singleLine, DiagnosticLevel level = DiagnosticLevel.info})
```

Creates a diagnostics property for [CupertinoDynamicColor].
