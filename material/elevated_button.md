@docImport 'filled_button.dart'; @docImport 'material.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart';

# ElevatedButton

```dart
class ElevatedButton extends ButtonStyleButton {}
```

A Material Design "elevated button".

Use elevated buttons to add dimension to otherwise mostly flat layouts, e.g. in long busy lists of content, or in wide spaces. Avoid using elevated buttons on already-elevated content such as dialogs or cards.

An elevated button is a label [child] displayed on a [Material] widget whose [Material.elevation] increases when the button is pressed. The label's [Text] and [Icon] widgets are displayed in [style]'s [ButtonStyle.foregroundColor] and the button's filled background is the [ButtonStyle.backgroundColor].

The elevated button's default style is defined by [defaultStyleOf]. The style of this elevated button can be overridden with its [style] parameter. The style of all elevated buttons in a subtree can be overridden with the [ElevatedButtonTheme], and the style of all of the elevated buttons in an app can be overridden with the [Theme]'s [ThemeData.elevatedButtonTheme] property.

The static [styleFrom] method is a convenient way to create a elevated button [ButtonStyle] from simple values.

If [onPressed] and [onLongPress] callbacks are null, then the button will be disabled.

{@tool dartpad} This sample produces an enabled and a disabled ElevatedButton.

** See code in examples/api/lib/material/elevated_button/elevated_button.0.dart ** {@end-tool}

See also:

- [FilledButton], a filled button that doesn't elevate when pressed.
- [FilledButton.tonal], a filled button variant that uses a secondary fill color.
- [OutlinedButton], a button with an outlined border and no fill color.
- [TextButton], a button with no outline or fill color.
- <https://material.io/design/components/buttons.html>
- <https://m3.material.io/components/buttons>

### ElevatedButton()

```dart
ElevatedButton({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior, dynamic statesController, required dynamic child})
```

Create an ElevatedButton.

### ElevatedButton.icon()

```dart
ElevatedButton.icon({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior = Clip.none, dynamic statesController, Widget? icon, required Widget label, IconAlignment? iconAlignment})
```

Create an elevated button from a pair of widgets that serve as the button's [icon] and [label].

The icon and label are arranged in a row and padded by 12 logical pixels at the start, and 16 at the end, with an 8 pixel gap in between.

If [icon] is null, this constructor will create an [ElevatedButton] that doesn't display an icon.

{@macro flutter.material.ButtonStyle.iconAlignment}

### styleFrom()

```dart
ButtonStyle styleFrom({Color? foregroundColor, Color? backgroundColor, Color? disabledForegroundColor, Color? disabledBackgroundColor, Color? shadowColor, Color? surfaceTintColor, Color? iconColor, double? iconSize, IconAlignment? iconAlignment, Color? disabledIconColor, Color? overlayColor, double? elevation, TextStyle? textStyle, EdgeInsetsGeometry? padding, Size? minimumSize, Size? fixedSize, Size? maximumSize, BorderSide? side, OutlinedBorder? shape, MouseCursor? enabledMouseCursor, MouseCursor? disabledMouseCursor, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory, ButtonLayerBuilder? backgroundBuilder, ButtonLayerBuilder? foregroundBuilder})
```

A static convenience method that constructs an elevated button [ButtonStyle] given simple values.

The [foregroundColor] and [disabledForegroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.foregroundColor], and a derived [ButtonStyle.overlayColor] if [overlayColor] isn't specified.

If [overlayColor] is specified and its value is [Colors.transparent] then the pressed/focused/hovered highlights are effectively defeated. Otherwise a [WidgetStateProperty] with the same opacities as the default is created.

The [backgroundColor] and [disabledBackgroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.backgroundColor].

Similarly, the [enabledMouseCursor] and [disabledMouseCursor] parameters are used to construct [ButtonStyle.mouseCursor].

The [iconColor], [disabledIconColor] are used to construct [ButtonStyle.iconColor] and [iconSize] is used to construct [ButtonStyle.iconSize].

If [iconColor] is null, the button icon will use [foregroundColor]. If [foregroundColor] is also null, the button icon will use the default icon color.

The button's elevations are defined relative to the [elevation] parameter. The disabled elevation is the same as the parameter value, [elevation] + 2 is used when the button is hovered or focused, and elevation + 6 is used when the button is pressed.

All of the other parameters are either used directly or used to create a [WidgetStateProperty] with a single value for all states.

All parameters default to null, by default this method returns a [ButtonStyle] that doesn't override anything.

For example, to override the default text and icon colors for an [ElevatedButton], as well as its overlay color, with all of the standard opacity adjustments for the pressed, focused, and hovered states, one could write:

```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(foregroundColor: Colors.green),
  onPressed: () {
    // ...
  },
  child: const Text('Jump'),
),
```

And to change the fill color:

```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(backgroundColor: Colors.green),
  onPressed: () {
    // ...
  },
  child: const Text('Meow'),
),
```

### defaultStyleOf()

```dart
ButtonStyle defaultStyleOf(BuildContext context)
```

Defines the button's default appearance.

The button [child]'s [Text] and [Icon] widgets are rendered with the [ButtonStyle]'s foreground color. The button's [InkWell] adds the style's overlay color when the button is focused, hovered or pressed. The button's background color becomes its [Material] color.

All of the ButtonStyle's defaults appear below. In this list "Theme.foo" is shorthand for `Theme.of(context).foo`. Color scheme values like "onSurface(0.38)" are shorthand for `onSurface.withOpacity(0.38)`. [WidgetStateProperty] valued properties that are not followed by a sublist have the same value for all states, otherwise the values are as specified for each state, and "others" means all other states.

{@template flutter.material.elevated_button.default_font_size} The "default font size" below refers to the font size specified in the [defaultStyleOf] method (or 14.0 if unspecified), scaled by the `MediaQuery.textScalerOf(context).scale` method. The names of the EdgeInsets constructors and `EdgeInsetsGeometry.lerp` have been abbreviated for readability. {@endtemplate}

The color of the [ButtonStyle.textStyle] is not used, the [ButtonStyle.foregroundColor] color is used instead.

## Material 2 defaults

- `textStyle` - Theme.textTheme.button
- `backgroundColor`
- disabled - Theme.colorScheme.onSurface(0.12)
- others - Theme.colorScheme.primary
- `foregroundColor`
- disabled - Theme.colorScheme.onSurface(0.38)
- others - Theme.colorScheme.onPrimary
- `overlayColor`
- hovered - Theme.colorScheme.onPrimary(0.08)
- focused or pressed - Theme.colorScheme.onPrimary(0.12)
- `shadowColor` - Theme.shadowColor
- `elevation`
- disabled - 0
- default - 2
- hovered or focused - 4
- pressed - 8
- `padding`
- `default font size <= 14` - horizontal(16)
- `14 < default font size <= 28` - lerp(horizontal(16), horizontal(8))
- `28 < default font size <= 36` - lerp(horizontal(8), horizontal(4))
- `36 < default font size` - horizontal(4)
- `minimumSize` - Size(64, 36)
- `fixedSize` - null
- `maximumSize` - Size.infinite
- `side` - null
- `shape` - RoundedRectangleBorder(borderRadius: BorderRadius.circular(4))
- `mouseCursor` - WidgetStateMouseCursor.adaptiveClickable
- `visualDensity` - theme.visualDensity
- `tapTargetSize` - theme.materialTapTargetSize
- `animationDuration` - kThemeChangeDuration
- `enableFeedback` - true
- `alignment` - Alignment.center
- `splashFactory` - InkRipple.splashFactory

The default padding values for the [ElevatedButton.icon] factory are slightly different:

- `padding`
- `default font size <= 14` - start(12) end(16)
- `14 < default font size <= 28` - lerp(start(12) end(16), horizontal(8))
- `28 < default font size <= 36` - lerp(horizontal(8), horizontal(4))
- `36 < default font size` - horizontal(4)

The default value for `side`, which defines the appearance of the button's outline, is null. That means that the outline is defined by the button shape's [OutlinedBorder.side]. Typically the default value of an [OutlinedBorder]'s side is [BorderSide.none], so an outline is not drawn.

## Material 3 defaults

If [ThemeData.useMaterial3] is set to true the following defaults will be used:

- `textStyle` - Theme.textTheme.labelLarge
- `backgroundColor`
- disabled - Theme.colorScheme.onSurface(0.12)
- others - Theme.colorScheme.surfaceContainerLow
- `foregroundColor`
- disabled - Theme.colorScheme.onSurface(0.38)
- others - Theme.colorScheme.primary
- `overlayColor`
- hovered - Theme.colorScheme.primary(0.08)
- focused or pressed - Theme.colorScheme.primary(0.1)
- `shadowColor` - Theme.colorScheme.shadow
- `surfaceTintColor` - Colors.transparent
- `elevation`
- disabled - 0
- default - 1
- hovered - 3
- focused or pressed - 1
- `padding`
- `default font size <= 14` - horizontal(24)
- `14 < default font size <= 28` - lerp(horizontal(24), horizontal(12))
- `28 < default font size <= 36` - lerp(horizontal(12), horizontal(6))
- `36 < default font size` - horizontal(6)
- `minimumSize` - Size(64, 40)
- `fixedSize` - null
- `maximumSize` - Size.infinite
- `side` - null
- `shape` - StadiumBorder()
- `mouseCursor` - WidgetStateMouseCursor.adaptiveClickable
- `visualDensity` - Theme.visualDensity
- `tapTargetSize` - Theme.materialTapTargetSize
- `animationDuration` - kThemeChangeDuration
- `enableFeedback` - true
- `alignment` - Alignment.center
- `splashFactory` - Theme.splashFactory

For the [ElevatedButton.icon] factory, the start (generally the left) value of [ButtonStyle.padding] is reduced from 24 to 16.

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```

Returns the [ElevatedButtonThemeData.style] of the closest [ElevatedButtonTheme] ancestor.
