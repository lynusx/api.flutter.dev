@docImport 'elevated_button.dart'; @docImport 'filled_button.dart'; @docImport 'material.dart'; @docImport 'outlined_button.dart';

# TextButton

```dart
class TextButton extends ButtonStyleButton {}
```

A Material Design "Text Button".

Use text buttons on toolbars, in dialogs, or inline with other content but offset from that content with padding so that the button's presence is obvious. Text buttons do not have visible borders and must therefore rely on their position relative to other content for context. In dialogs and cards, they should be grouped together in one of the bottom corners. Avoid using text buttons where they would blend in with other content, for example in the middle of lists.

A text button is a label [child] displayed on a (zero elevation) [Material] widget. The label's [Text] and [Icon] widgets are displayed in the [style]'s [ButtonStyle.foregroundColor]. The button reacts to touches by filling with the [style]'s [ButtonStyle.backgroundColor].

The text button's default style is defined by [defaultStyleOf]. The style of this text button can be overridden with its [style] parameter. The style of all text buttons in a subtree can be overridden with the [TextButtonTheme] and the style of all of the text buttons in an app can be overridden with the [Theme]'s [ThemeData.textButtonTheme] property.

The static [styleFrom] method is a convenient way to create a text button [ButtonStyle] from simple values.

If the [onPressed] and [onLongPress] callbacks are null, then this button will be disabled, it will not react to touch.

{@tool dartpad} This sample shows various ways to configure TextButtons, from the simplest default appearance to versions that don't resemble Material Design at all.

** See code in examples/api/lib/material/text_button/text_button.0.dart ** {@end-tool}

{@tool dartpad} This sample demonstrates using the [statesController] parameter to create a button that adds support for [WidgetState.selected].

** See code in examples/api/lib/material/text_button/text_button.1.dart ** {@end-tool}

See also:

- [ElevatedButton], a filled button whose material elevates when pressed.
- [FilledButton], a filled button that doesn't elevate when pressed.
- [FilledButton.tonal], a filled button variant that uses a secondary fill color.
- [OutlinedButton], a button with an outlined border and no fill color.
- <https://material.io/design/components/buttons.html>
- <https://m3.material.io/components/buttons>

### TextButton()

```dart
TextButton({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior, dynamic statesController, bool? isSemanticButton, required Widget child})
```

Create a [TextButton].

### TextButton.icon()

```dart
TextButton.icon({dynamic key, required dynamic onPressed, dynamic onLongPress, dynamic onHover, dynamic onFocusChange, ButtonStyle? style, dynamic focusNode, bool autofocus = false, dynamic clipBehavior = Clip.none, dynamic statesController, Widget? icon, required Widget label, IconAlignment? iconAlignment})
```

Create a text button from a pair of widgets that serve as the button's [icon] and [label].

The icon and label are arranged in a row and padded by 8 logical pixels at the ends, with an 8 pixel gap in between.

If [icon] is null, this constructor will create a [TextButton] that doesn't display an icon.

{@macro flutter.material.ButtonStyle.iconAlignment}

### styleFrom()

```dart
ButtonStyle styleFrom({Color? foregroundColor, Color? backgroundColor, Color? disabledForegroundColor, Color? disabledBackgroundColor, Color? shadowColor, Color? surfaceTintColor, Color? iconColor, double? iconSize, IconAlignment? iconAlignment, Color? disabledIconColor, Color? overlayColor, double? elevation, TextStyle? textStyle, EdgeInsetsGeometry? padding, Size? minimumSize, Size? fixedSize, Size? maximumSize, BorderSide? side, OutlinedBorder? shape, MouseCursor? enabledMouseCursor, MouseCursor? disabledMouseCursor, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory, ButtonLayerBuilder? backgroundBuilder, ButtonLayerBuilder? foregroundBuilder})
```

A static convenience method that constructs a text button [ButtonStyle] given simple values.

The [foregroundColor] and [disabledForegroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.foregroundColor], and a derived [ButtonStyle.overlayColor] if [overlayColor] isn't specified.

The [backgroundColor] and [disabledBackgroundColor] colors are used to create a [WidgetStateProperty] [ButtonStyle.backgroundColor].

Similarly, the [enabledMouseCursor] and [disabledMouseCursor] parameters are used to construct [ButtonStyle.mouseCursor].

The [iconColor], [disabledIconColor] are used to construct [ButtonStyle.iconColor] and [iconSize] is used to construct [ButtonStyle.iconSize].

If [iconColor] is null, the button icon will use [foregroundColor]. If [foregroundColor] is also null, the button icon will use the default icon color.

If [overlayColor] is specified and its value is [Colors.transparent] then the pressed/focused/hovered highlights are effectively defeated. Otherwise a [WidgetStateProperty] with the same opacities as the default is created.

All of the other parameters are either used directly or used to create a [WidgetStateProperty] with a single value for all states.

All parameters default to null. By default this method returns a [ButtonStyle] that doesn't override anything.

For example, to override the default text and icon colors for a [TextButton], as well as its overlay color, with all of the standard opacity adjustments for the pressed, focused, and hovered states, one could write:

```dart
TextButton(
  style: TextButton.styleFrom(foregroundColor: Colors.green),
  child: const Text('Give Kate a mix tape'),
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

{@template flutter.material.text_button.default_style_of} The button [child]'s [Text] and [Icon] widgets are rendered with the [ButtonStyle]'s foreground color. The button's [InkWell] adds the style's overlay color when the button is focused, hovered or pressed. The button's background color becomes its [Material] color and is transparent by default.

All of the [ButtonStyle]'s defaults appear below.

In this list "Theme.foo" is shorthand for `Theme.of(context).foo`. Color scheme values like "onSurface(0.38)" are shorthand for `onSurface.withOpacity(0.38)`. [WidgetStateProperty] valued properties that are not followed by a sublist have the same value for all states, otherwise the values are as specified for each state and "others" means all other states.

The "default font size" below refers to the font size specified in the [defaultStyleOf] method (or 14.0 if unspecified), scaled by the `MediaQuery.textScalerOf(context).scale` method. And the names of the EdgeInsets constructors and `EdgeInsetsGeometry.lerp` have been abbreviated for readability.

The color of the [ButtonStyle.textStyle] is not used, the [ButtonStyle.foregroundColor] color is used instead. {@endtemplate}

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
- `default font size <= 14` - (horizontal(12), vertical(8))
- `14 < default font size <= 28` - lerp(all(8), horizontal(8))
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

The default padding values for the [TextButton.icon] factory are slightly different:

- `padding`
- `default font size <= 14` - all(8)
- `14 < default font size <= 28 `- lerp(all(8), horizontal(4))
- `28 < default font size` - horizontal(4)

The default value for `side`, which defines the appearance of the button's outline, is null. That means that the outline is defined by the button shape's [OutlinedBorder.side]. Typically the default value of an [OutlinedBorder]'s side is [BorderSide.none], so an outline is not drawn.

## Material 3 defaults

If [ThemeData.useMaterial3] is set to true the following defaults will be used:

{@template flutter.material.text_button.material3_defaults}

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
- `default font size <= 14` - lerp(horizontal(12), horizontal(4))
- `14 < default font size <= 28` - lerp(all(8), horizontal(8))
- `28 < default font size <= 36` - lerp(horizontal(8), horizontal(4))
- `36 < default font size` - horizontal(4)
- `minimumSize` - Size(64, 40)
- `fixedSize` - null
- `maximumSize` - Size.infinite
- `side` - null
- `shape` - StadiumBorder()
- `mouseCursor` - WidgetStateMouseCursor.adaptiveClickable
- `visualDensity` - theme.visualDensity
- `tapTargetSize` - theme.materialTapTargetSize
- `animationDuration` - kThemeChangeDuration
- `enableFeedback` - true
- `alignment` - Alignment.center
- `splashFactory` - Theme.splashFactory

For the [TextButton.icon] factory, the end (generally the right) value of `padding` is increased from 12 to 16. {@endtemplate}

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```

Returns the [TextButtonThemeData.style] of the closest [TextButtonTheme] ancestor.
