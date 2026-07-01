@docImport 'elevated_button.dart'; @docImport 'filled_button.dart'; @docImport 'material.dart'; @docImport 'text_button.dart';

# OutlinedButton

```dart
class OutlinedButton extends ButtonStyleButton {}
```

A Material Design "Outlined Button"; essentially a [TextButton] with an outlined border.

Outlined buttons are medium-emphasis buttons. They contain actions that are important, but they aren’t the primary action in an app.

An outlined button is a label [child] displayed on a (zero elevation) [Material] widget. The label's [Text] and [Icon] widgets are displayed in the [style]'s [ButtonStyle.foregroundColor] and the outline's weight and color are defined by [ButtonStyle.side]. The button reacts to touches by filling with the [style]'s [ButtonStyle.overlayColor].

The outlined button's default style is defined by [defaultStyleOf]. The style of this outline button can be overridden with its [style] parameter. The style of all text buttons in a subtree can be overridden with the [OutlinedButtonTheme] and the style of all of the outlined buttons in an app can be overridden with the [Theme]'s [ThemeData.outlinedButtonTheme] property.

Unlike [TextButton] or [ElevatedButton], outline buttons have a default [ButtonStyle.side] which defines the appearance of the outline. Because the default `side` is non-null, it unconditionally overrides the shape's [OutlinedBorder.side]. In other words, to specify an outlined button's shape _and_ the appearance of its outline, both the [ButtonStyle.shape] and [ButtonStyle.side] properties must be specified.

{@tool dartpad} Here is an example of a basic [OutlinedButton].

** See code in examples/api/lib/material/outlined_button/outlined_button.0.dart ** {@end-tool}

The static [styleFrom] method is a convenient way to create a outlined button [ButtonStyle] from simple values.

See also:

- [ElevatedButton], a filled button whose material elevates when pressed.
- [FilledButton], a filled button that doesn't elevate when pressed.
- [FilledButton.tonal], a filled button variant that uses a secondary fill color.
- [TextButton], a button with no outline or fill color.
- <https://material.io/design/components/buttons.html>
- <https://m3.material.io/components/buttons>

### OutlinedButton()

```dart
OutlinedButton({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior, dynamic statesController, required dynamic child})
```

Create an OutlinedButton.

### OutlinedButton.icon()

```dart
OutlinedButton.icon({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior, dynamic statesController, Widget? icon, required Widget label, IconAlignment? iconAlignment})
```

Create an outlined button from a pair of widgets that serve as the button's [icon] and [label].

The icon and label are arranged in a row and padded by 12 logical pixels at the start, and 16 at the end, with an 8 pixel gap in between.

If [icon] is null, this constructor will create an outlined button that doesn't display an icon.

{@macro flutter.material.ButtonStyle.iconAlignment}

### styleFrom()

```dart
ButtonStyle styleFrom({Color? foregroundColor, Color? backgroundColor, Color? disabledForegroundColor, Color? disabledBackgroundColor, Color? shadowColor, Color? surfaceTintColor, Color? iconColor, double? iconSize, IconAlignment? iconAlignment, Color? disabledIconColor, Color? overlayColor, double? elevation, TextStyle? textStyle, EdgeInsetsGeometry? padding, Size? minimumSize, Size? fixedSize, Size? maximumSize, BorderSide? side, OutlinedBorder? shape, MouseCursor? enabledMouseCursor, MouseCursor? disabledMouseCursor, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory, ButtonLayerBuilder? backgroundBuilder, ButtonLayerBuilder? foregroundBuilder})
```

A static convenience method that constructs an outlined button [ButtonStyle] given simple values.

The [foregroundColor] and [disabledForegroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.foregroundColor], and a derived [ButtonStyle.overlayColor] if [overlayColor] isn't specified.

The [backgroundColor] and [disabledBackgroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.backgroundColor].

Similarly, the [enabledMouseCursor] and [disabledMouseCursor] parameters are used to construct [ButtonStyle.mouseCursor].

The [iconColor], [disabledIconColor] are used to construct [ButtonStyle.iconColor] and [iconSize] is used to construct [ButtonStyle.iconSize].

If [iconColor] is null, the button icon will use [foregroundColor]. If [foregroundColor] is also null, the button icon will use the default icon color.

If [overlayColor] is specified and its value is [Colors.transparent] then the pressed/focused/hovered highlights are effectively defeated. Otherwise a [WidgetStateProperty] with the same opacities as the default is created.

All of the other parameters are either used directly or used to create a [WidgetStateProperty] with a single value for all states.

All parameters default to null, by default this method returns a [ButtonStyle] that doesn't override anything.

For example, to override the default shape and outline for an [OutlinedButton], one could write:

```dart
OutlinedButton(
  style: OutlinedButton.styleFrom(
     shape: const StadiumBorder(),
     side: const BorderSide(width: 2, color: Colors.green),
  ),
  child: const Text('Seasons of Love'),
  onPressed: () {
    // ...
  },
),
```

### defaultStyleOf()

```dart
ButtonStyle defaultStyleOf(BuildContext context)
```

Defines the button's default appearance.

With the exception of [ButtonStyle.side], which defines the outline, and [ButtonStyle.padding], the returned style is the same as for [TextButton].

The button [child]'s [Text] and [Icon] widgets are rendered with the [ButtonStyle]'s foreground color. The button's [InkWell] adds the style's overlay color when the button is focused, hovered or pressed. The button's background color becomes its [Material] color and is transparent by default.

All of the ButtonStyle's defaults appear below. In this list "Theme.foo" is shorthand for `Theme.of(context).foo`. Color scheme values like "onSurface(0.38)" are shorthand for `onSurface.withOpacity(0.38)`. [WidgetStateProperty] valued properties that are not followed by a sublist have the same value for all states, otherwise the values are as specified for each state and "others" means all other states.

The color of the [ButtonStyle.textStyle] is not used, the [ButtonStyle.foregroundColor] is used instead.

## Material 2 defaults

- `textStyle` - Theme.textTheme.button
- `backgroundColor` - transparent
- `foregroundColor`
- disabled - Theme.colorScheme.onSurface(0.38)
- others - Theme.colorScheme.primary
- `overlayColor`
- hovered - Theme.colorScheme.primary(0.08)
- focused or pressed - Theme.colorScheme.primary(0.12)
- `shadowColor` - Theme.shadowColor
- `elevation` - 0
- `padding`
- `default font size <= 14` - horizontal(16)
- `14 < default font size <= 28` - lerp(horizontal(16), horizontal(8))
- `28 < default font size <= 36` - lerp(horizontal(8), horizontal(4))
- `36 < default font size` - horizontal(4)
- `minimumSize` - Size(64, 36)
- `fixedSize` - null
- `maximumSize` - Size.infinite
- `side` - BorderSide(width: 1, color: Theme.colorScheme.onSurface(0.12))
- `shape` - RoundedRectangleBorder(borderRadius: BorderRadius.circular(4))
- `mouseCursor` - WidgetStateMouseCursor.adaptiveClickable
- `visualDensity` - theme.visualDensity
- `tapTargetSize` - theme.materialTapTargetSize
- `animationDuration` - kThemeChangeDuration
- `enableFeedback` - true
- `alignment` - Alignment.center
- `splashFactory` - InkRipple.splashFactory

## Material 3 defaults

If [ThemeData.useMaterial3] is set to true the following defaults will be used:

- `textStyle` - Theme.textTheme.labelLarge
- `backgroundColor` - transparent
- `foregroundColor`
- disabled - Theme.colorScheme.onSurface(0.38)
- others - Theme.colorScheme.primary
- `overlayColor`
- hovered - Theme.colorScheme.primary(0.08)
- focused or pressed - Theme.colorScheme.primary(0.1)
- others - null
- `shadowColor` - Colors.transparent,
- `surfaceTintColor` - null
- `elevation` - 0
- `padding`
- `default font size <= 14` - horizontal(24)
- `14 < default font size <= 28` - lerp(horizontal(24), horizontal(12))
- `28 < default font size <= 36` - lerp(horizontal(12), horizontal(6))
- `36 < default font size` - horizontal(6)
- `minimumSize` - Size(64, 40)
- `fixedSize` - null
- `maximumSize` - Size.infinite
- `side`
- disabled - BorderSide(color: Theme.colorScheme.onSurface(0.12))
- others - BorderSide(color: Theme.colorScheme.outline)
- `shape` - StadiumBorder()
- `mouseCursor` - WidgetStateMouseCursor.adaptiveClickable
- `visualDensity` - theme.visualDensity
- `tapTargetSize` - theme.materialTapTargetSize
- `animationDuration` - kThemeChangeDuration
- `enableFeedback` - true
- `alignment` - Alignment.center
- `splashFactory` - Theme.splashFactory

For the [OutlinedButton.icon] factory, the start (generally the left) value of [ButtonStyle.padding] is reduced from 24 to 16.

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```
