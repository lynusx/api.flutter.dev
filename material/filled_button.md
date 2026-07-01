@docImport 'elevated_button.dart'; @docImport 'floating_action_button.dart'; @docImport 'material.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart';

# FilledButton

```dart
class FilledButton extends ButtonStyleButton {}
```

A Material Design filled button.

Filled buttons have the most visual impact after the [FloatingActionButton], and should be used for important, final actions that complete a flow, like **Save**, **Join now**, or **Confirm**.

A filled button is a label [child] displayed on a [Material] widget. The label's [Text] and [Icon] widgets are displayed in [style]'s [ButtonStyle.foregroundColor] and the button's filled background is the [ButtonStyle.backgroundColor].

The filled button's default style is defined by [defaultStyleOf]. The style of this filled button can be overridden with its [style] parameter. The style of all filled buttons in a subtree can be overridden with the [FilledButtonTheme], and the style of all of the filled buttons in an app can be overridden with the [Theme]'s [ThemeData.filledButtonTheme] property.

The static [styleFrom] method is a convenient way to create a filled button [ButtonStyle] from simple values.

If [onPressed] and [onLongPress] callbacks are null, then the button will be disabled.

To create a 'filled tonal' button, use [FilledButton.tonal].

{@tool dartpad} This sample produces enabled and disabled filled and filled tonal buttons.

** See code in examples/api/lib/material/filled_button/filled_button.0.dart ** {@end-tool}

## Visual density effects

The button's appearance is affected by the [VisualDensity] from the enclosing [Theme] or from its [style]. Visual density adjusts the [ButtonStyle.padding] and [ButtonStyle.minimumSize] to accommodate different UI densities across platforms. See [VisualDensity] for more details on how it affects component layout and the platform-specific defaults.

See also:

- [ElevatedButton], a filled button whose material elevates when pressed.
- [OutlinedButton], a button with an outlined border and no fill color.
- [TextButton], a button with no outline or fill color.
- <https://material.io/design/components/buttons.html>
- <https://m3.material.io/components/buttons>

### FilledButton()

```dart
FilledButton({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior = Clip.none, dynamic statesController, required dynamic child})
```

Create a FilledButton.

### FilledButton.icon()

```dart
FilledButton.icon({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior = Clip.none, dynamic statesController, Widget? icon, required Widget label, IconAlignment? iconAlignment})
```

Create a filled button from [icon] and [label].

The icon and label are arranged in a row with padding at the start and end and a gap between them.

If [icon] is null, this constructor will create a [FilledButton] that doesn't display an icon.

{@macro flutter.material.ButtonStyle.iconAlignment}

### FilledButton.tonal()

```dart
FilledButton.tonal({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior = Clip.none, dynamic statesController, required dynamic child})
```

Create a tonal variant of FilledButton.

A filled tonal button is an alternative middle ground between [FilledButton] and [OutlinedButton]. They’re useful in contexts where a lower-priority button requires slightly more emphasis than an outline would give, such as "Next" in an onboarding flow.

### FilledButton.tonalIcon()

```dart
FilledButton.tonalIcon({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior = Clip.none, dynamic statesController, Widget? icon, required Widget label, IconAlignment? iconAlignment})
```

Create a filled tonal button from [icon] and [label].

The [icon] and [label] are arranged in a row with padding at the start and end and a gap between them.

If [icon] is null, this constructor will create a [FilledButton] that doesn't display an icon.

### styleFrom()

```dart
ButtonStyle styleFrom({Color? foregroundColor, Color? backgroundColor, Color? disabledForegroundColor, Color? disabledBackgroundColor, Color? shadowColor, Color? surfaceTintColor, Color? iconColor, double? iconSize, IconAlignment? iconAlignment, Color? disabledIconColor, Color? overlayColor, double? elevation, TextStyle? textStyle, EdgeInsetsGeometry? padding, Size? minimumSize, Size? fixedSize, Size? maximumSize, BorderSide? side, OutlinedBorder? shape, MouseCursor? enabledMouseCursor, MouseCursor? disabledMouseCursor, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory, ButtonLayerBuilder? backgroundBuilder, ButtonLayerBuilder? foregroundBuilder})
```

A static convenience method that constructs a filled button [ButtonStyle] given simple values.

The [foregroundColor] and [disabledForegroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.foregroundColor], and a derived [ButtonStyle.overlayColor] if [overlayColor] isn't specified.

If [overlayColor] is specified and its value is [Colors.transparent] then the pressed/focused/hovered highlights are effectively defeated. Otherwise a [WidgetStateProperty] with the same opacities as the default is created.

Similarly, the [enabledMouseCursor] and [disabledMouseCursor] parameters are used to construct [ButtonStyle.mouseCursor].

The [iconColor], [disabledIconColor] are used to construct [ButtonStyle.iconColor] and [iconSize] is used to construct [ButtonStyle.iconSize].

If [iconColor] is null, the button icon will use [foregroundColor]. If [foregroundColor] is also null, the button icon will use the default icon color.

The button's elevations are defined relative to the [elevation] parameter. The disabled elevation is the same as the parameter value, [elevation] + 2 is used when the button is hovered or focused, and elevation + 6 is used when the button is pressed.

All of the other parameters are either used directly or used to create a [WidgetStateProperty] with a single value for all states.

All parameters default to null, by default this method returns a [ButtonStyle] that doesn't override anything.

For example, to override the default text and icon colors for a [FilledButton], as well as its overlay color, with all of the standard opacity adjustments for the pressed, focused, and hovered states, one could write:

```dart
FilledButton(
  style: FilledButton.styleFrom(foregroundColor: Colors.green),
  onPressed: () {},
  child: const Text('Filled button'),
);
```

or for a Filled tonal variant:

```dart
FilledButton.tonal(
  style: FilledButton.styleFrom(foregroundColor: Colors.green),
  onPressed: () {},
  child: const Text('Filled tonal button'),
);
```

### defaultStyleOf()

```dart
ButtonStyle defaultStyleOf(BuildContext context)
```

Defines the button's default appearance.

The button [child]'s [Text] and [Icon] widgets are rendered with the [ButtonStyle]'s foreground color. The button's [InkWell] adds the style's overlay color when the button is focused, hovered or pressed. The button's background color becomes its [Material] color.

All of the ButtonStyle's defaults appear below. In this list "Theme.foo" is shorthand for `Theme.of(context).foo`. Color scheme values like "onSurface(0.38)" are shorthand for `onSurface.withOpacity(0.38)`. [WidgetStateProperty] valued properties that are not followed by a sublist have the same value for all states, otherwise the values are as specified for each state, and "others" means all other states.

{@macro flutter.material.elevated_button.default_font_size}

The color of the [ButtonStyle.textStyle] is not used, the [ButtonStyle.foregroundColor] color is used instead.

- `textStyle` - Theme.textTheme.labelLarge
- `backgroundColor`
- disabled - Theme.colorScheme.onSurface(0.12)
- others - Theme.colorScheme.secondaryContainer
- `foregroundColor`
- disabled - Theme.colorScheme.onSurface(0.38)
- others - Theme.colorScheme.onSecondaryContainer
- `overlayColor`
- hovered - Theme.colorScheme.onSecondaryContainer(0.08)
- focused or pressed - Theme.colorScheme.onSecondaryContainer(0.12)
- `shadowColor` - Theme.colorScheme.shadow
- `surfaceTintColor` - null
- `elevation`
- disabled - 0
- default - 0
- hovered - 1
- focused or pressed - 0
- `padding`
- `default font size <= 14` - horizontal(16)
- `14 < default font size <= 28` - lerp(horizontal(16), horizontal(8))
- `28 < default font size <= 36` - lerp(horizontal(8), horizontal(4))
- `36 < default font size` - horizontal(4)
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

The default padding values for the [FilledButton.icon] factory are slightly different:

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
- others - Theme.colorScheme.secondaryContainer
- `foregroundColor`
- disabled - Theme.colorScheme.onSurface(0.38)
- others - Theme.colorScheme.onSecondaryContainer
- `overlayColor`
- hovered - Theme.colorScheme.onSecondaryContainer(0.08)
- focused or pressed - Theme.colorScheme.onSecondaryContainer(0.1)
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

For the [FilledButton.icon] factory, the start (generally the left) value of [ButtonStyle.padding] is reduced from 24 to 16.

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```

Returns the [FilledButtonThemeData.style] of the closest [FilledButtonTheme] ancestor.
