@docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'button.dart'; @docImport 'switch.dart';

# CupertinoTheme

```dart
class CupertinoTheme extends StatelessWidget {}
```

Applies a visual styling theme to descendant Cupertino widgets.

Affects the color and text styles of Cupertino widgets whose styling are not overridden when constructing the respective widgets instances.

Descendant widgets can retrieve the current [CupertinoThemeData] by calling [CupertinoTheme.of]. An [InheritedWidget] dependency is created when an ancestor [CupertinoThemeData] is retrieved via [CupertinoTheme.of].

The [CupertinoTheme] widget implies an [IconTheme] widget, whose [IconTheme.data] has the same color as [CupertinoThemeData.primaryColor]

See also:

- [CupertinoThemeData], specifies the theme's visual styling.
- [CupertinoApp], which will automatically add a [CupertinoTheme] based on the value of [CupertinoApp.theme].
- [Theme], a Material theme which will automatically add a [CupertinoTheme] with a [CupertinoThemeData] derived from the Material [ThemeData].

### CupertinoTheme()

```dart
CupertinoTheme({dynamic key, required CupertinoThemeData data, required Widget child})
```

Creates a [CupertinoTheme] to change descendant Cupertino widgets' styling.

### data

```dart
CupertinoThemeData data
```

The [CupertinoThemeData] styling for this theme.

### of()

```dart
CupertinoThemeData of(BuildContext context)
```

Retrieves the [CupertinoThemeData] from the closest ancestor [CupertinoTheme] widget, or a default [CupertinoThemeData] if no [CupertinoTheme] ancestor exists.

Resolves all the colors defined in that [CupertinoThemeData] against the given [BuildContext] on a best-effort basis.

### brightnessOf()

```dart
Brightness brightnessOf(BuildContext context)
```

Retrieves the [Brightness] to use for descendant Cupertino widgets, based on the value of [CupertinoThemeData.brightness] in the given [context].

If no [CupertinoTheme] can be found in the given [context], or its `brightness` is null, it will fall back to [MediaQueryData.platformBrightness].

Throws an exception if no valid [CupertinoTheme] or [MediaQuery] widgets exist in the ancestry tree.

See also:

- [maybeBrightnessOf], which returns null if no valid [CupertinoTheme] or [MediaQuery] exists, instead of throwing.
- [CupertinoThemeData.brightness], the property takes precedence over [MediaQueryData.platformBrightness] for descendant Cupertino widgets.

### maybeBrightnessOf()

```dart
Brightness? maybeBrightnessOf(BuildContext context)
```

Retrieves the [Brightness] to use for descendant Cupertino widgets, based on the value of [CupertinoThemeData.brightness] in the given [context].

If no [CupertinoTheme] can be found in the given [context], it will fall back to [MediaQueryData.platformBrightness].

Returns null if no valid [CupertinoTheme] or [MediaQuery] widgets exist in the ancestry tree.

See also:

- [CupertinoThemeData.brightness], the property takes precedence over [MediaQueryData.platformBrightness] for descendant Cupertino widgets.
- [brightnessOf], which throws if no valid [CupertinoTheme] or [MediaQuery] exists, instead of returning null.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# InheritedCupertinoTheme

```dart
class InheritedCupertinoTheme extends InheritedTheme {}
```

Provides a [CupertinoTheme] to all descendants.

### InheritedCupertinoTheme()

```dart
InheritedCupertinoTheme({dynamic key, required CupertinoTheme theme, required dynamic child})
```

Creates an [InheritedTheme] that provides a [CupertinoTheme] to all descendants.

### theme

```dart
CupertinoTheme theme
```

The [CupertinoTheme] that is provided to widgets lower in the tree.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(InheritedCupertinoTheme oldWidget)
```

# CupertinoThemeData

```dart
class CupertinoThemeData extends NoDefaultCupertinoThemeData with Diagnosticable {}
```

Styling specifications for a [CupertinoTheme].

All constructor parameters can be null, in which case a [CupertinoColors.activeBlue] based default iOS theme styling is used.

Parameters can also be partially specified, in which case some parameters will cascade down to other dependent parameters to create a cohesive visual effect. For instance, if a [primaryColor] is specified, it would cascade down to affect some fonts in [textTheme] if [textTheme] is not specified.

See also:

- [CupertinoTheme], in which this [CupertinoThemeData] is inserted.
- [ThemeData], a Material equivalent that also configures Cupertino styling via a [CupertinoThemeData] subclass [MaterialBasedCupertinoThemeData].

### CupertinoThemeData()

```dart
CupertinoThemeData({Brightness? brightness, Color? primaryColor, Color? primaryContrastingColor, CupertinoTextThemeData? textTheme, Color? barBackgroundColor, Color? scaffoldBackgroundColor, Color? selectionHandleColor, bool? applyThemeToAll})
```

Creates a [CupertinoTheme] styling specification.

Unspecified parameters default to a reasonable iOS default style.

### CupertinoThemeData.raw()

```dart
CupertinoThemeData.raw(Brightness? brightness, Color? primaryColor, Color? primaryContrastingColor, CupertinoTextThemeData? textTheme, Color? barBackgroundColor, Color? scaffoldBackgroundColor, Color? selectionHandleColor, bool? applyThemeToAll)
```

Same as the default constructor but with positional arguments to avoid forgetting any and to specify all arguments.

Used by subclasses to get the superclass's defaulting behaviors.

### primaryColor

```dart
Color get primaryColor
```

### primaryContrastingColor

```dart
Color get primaryContrastingColor
```

### textTheme

```dart
CupertinoTextThemeData get textTheme
```

### barBackgroundColor

```dart
Color get barBackgroundColor
```

### scaffoldBackgroundColor

```dart
Color get scaffoldBackgroundColor
```

### selectionHandleColor

```dart
Color get selectionHandleColor
```

### applyThemeToAll

```dart
bool get applyThemeToAll
```

### noDefault()

```dart
NoDefaultCupertinoThemeData noDefault()
```

### resolveFrom()

```dart
CupertinoThemeData resolveFrom(BuildContext context)
```

### copyWith()

```dart
CupertinoThemeData copyWith({Brightness? brightness, Color? primaryColor, Color? primaryContrastingColor, CupertinoTextThemeData? textTheme, Color? barBackgroundColor, Color? scaffoldBackgroundColor, Color? selectionHandleColor, bool? applyThemeToAll})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# NoDefaultCupertinoThemeData

```dart
class NoDefaultCupertinoThemeData {}
```

Styling specifications for a cupertino theme without default values for unspecified properties.

Unlike [CupertinoThemeData] instances of this class do not return default values for properties that have been left unspecified in the constructor. Instead, unspecified properties will return null. This is used by Material's [ThemeData.cupertinoOverrideTheme].

See also:

- [CupertinoThemeData], which uses reasonable default values for unspecified theme properties.

### NoDefaultCupertinoThemeData()

```dart
NoDefaultCupertinoThemeData({Brightness? brightness, Color? primaryColor, Color? primaryContrastingColor, CupertinoTextThemeData? textTheme, Color? barBackgroundColor, Color? scaffoldBackgroundColor, Color? selectionHandleColor, bool? applyThemeToAll})
```

Creates a [NoDefaultCupertinoThemeData] styling specification.

Unspecified properties default to null.

### brightness

```dart
Brightness? brightness
```

The brightness override for Cupertino descendants.

Defaults to null. If a non-null [Brightness] is specified, the value will take precedence over the ambient [MediaQueryData.platformBrightness], when determining the brightness of descendant Cupertino widgets.

If coming from a Material [Theme] and unspecified, [brightness] will be derived from the Material [ThemeData]'s [brightness].

See also:

- [MaterialBasedCupertinoThemeData], a [CupertinoThemeData] that defers [brightness] to its Material [Theme] parent if it's unspecified.

- [CupertinoTheme.brightnessOf], a method used to retrieve the overall [Brightness] from a [BuildContext], for Cupertino widgets.

### primaryColor

```dart
Color? primaryColor
```

A color used on interactive elements of the theme.

This color is generally used on text and icons in buttons and tappable elements. Defaults to [CupertinoColors.activeBlue].

If coming from a Material [Theme] and unspecified, [primaryColor] will be derived from the Material [ThemeData]'s `colorScheme.primary`. However, in iOS styling, the [primaryColor] is more sparsely used than in Material Design where the [primaryColor] can appear on non-interactive surfaces like the [AppBar] background, [TextField] borders etc.

See also:

- [MaterialBasedCupertinoThemeData], a [CupertinoThemeData] that defers [primaryColor] to its Material [Theme] parent if it's unspecified.

### primaryContrastingColor

```dart
Color? primaryContrastingColor
```

A color that must be easy to see when rendered on a [primaryColor] background.

For example, this color is used for a [CupertinoButton]'s text and icons when the button's background is [primaryColor].

If coming from a Material [Theme] and unspecified, [primaryContrastingColor] will be derived from the Material [ThemeData]'s `colorScheme.onPrimary`.

See also:

- [MaterialBasedCupertinoThemeData], a [CupertinoThemeData] that defers [primaryContrastingColor] to its Material [Theme] parent if it's unspecified.

### textTheme

```dart
CupertinoTextThemeData? textTheme
```

Text styles used by Cupertino widgets.

Derived from [primaryColor] if unspecified.

### barBackgroundColor

```dart
Color? barBackgroundColor
```

Background color of the top nav bar and bottom tab bar.

Defaults to a light gray in light mode, or a dark translucent gray color in dark mode.

### scaffoldBackgroundColor

```dart
Color? scaffoldBackgroundColor
```

Background color of the scaffold.

Defaults to [CupertinoColors.systemBackground].

### selectionHandleColor

```dart
Color? selectionHandleColor
```

The color of the selection handles on the text field.

Defaults to [CupertinoColors.systemBlue].

### applyThemeToAll

```dart
bool? applyThemeToAll
```

Flag to apply this theme to all descendant Cupertino widgets.

Certain Cupertino widgets previously didn't use theming, matching past versions of iOS. For example, [CupertinoSwitch]s always used [CupertinoColors.systemGreen] when active.

Today, however, these widgets can indeed be themed on iOS. Moreover on macOS, the accent color is reflected in these widgets. Turning this flag on ensures that descendant Cupertino widgets will be themed accordingly.

This flag currently applies to the following widgets:

- [CupertinoSwitch] & [Switch.adaptive]

Defaults to false.

### noDefault()

```dart
NoDefaultCupertinoThemeData noDefault()
```

Returns an instance of the theme data whose property getters only return the construction time specifications with no derived values.

Used in Material themes to let unspecified properties fallback to Material theme properties instead of iOS defaults.

### resolveFrom()

```dart
NoDefaultCupertinoThemeData resolveFrom(BuildContext context)
```

Returns a new theme data with all its colors resolved against the given [BuildContext].

Called by [CupertinoTheme.of] to resolve colors defined in the retrieved [CupertinoThemeData].

### copyWith()

```dart
NoDefaultCupertinoThemeData copyWith({Brightness? brightness, Color? primaryColor, Color? primaryContrastingColor, CupertinoTextThemeData? textTheme, Color? barBackgroundColor, Color? scaffoldBackgroundColor, Color? selectionHandleColor, bool? applyThemeToAll})
```

Creates a copy of the theme data with specified attributes overridden.

Only the current instance's specified attributes are copied instead of derived values. For instance, if the current [textTheme] is implied from the current [primaryColor] because it was not specified, copying with a different [primaryColor] will also change the copy's implied [textTheme].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```
