@docImport 'button_style_button.dart'; @docImport 'constants.dart'; @docImport 'elevated_button.dart'; @docImport 'elevated_button_theme.dart'; @docImport 'filled_button.dart'; @docImport 'filled_button_theme.dart'; @docImport 'material.dart'; @docImport 'no_splash.dart'; @docImport 'outlined_button.dart'; @docImport 'outlined_button_theme.dart'; @docImport 'text_button.dart'; @docImport 'text_button_theme.dart'; @docImport 'theme.dart';

# ButtonLayerBuilder

```dart
typedef ButtonLayerBuilder = Widget Function(BuildContext context, Set<WidgetState> states, Widget? child)
```

The type for [ButtonStyle.backgroundBuilder] and [ButtonStyle.foregroundBuilder].

The [states] parameter is the button's current pressed/hovered/etc state. The [child] is typically a descendant of the returned widget.

# ButtonStyle

```dart
class ButtonStyle with Diagnosticable {}
```

The visual properties that most buttons have in common.

Buttons and their themes have a ButtonStyle property which defines the visual properties whose default values are to be overridden. The default values are defined by the individual button widgets and are typically based on overall theme's [ThemeData.colorScheme] and [ThemeData.textTheme].

All of the ButtonStyle properties are null by default.

Many of the ButtonStyle properties are [WidgetStateProperty] objects which resolve to different values depending on the button's state. For example the [Color] properties are defined with `WidgetStateProperty<Color>` and can resolve to different colors depending on if the button is pressed, hovered, focused, disabled, etc.

These properties can override the default value for just one state or all of them. For example to create a [ElevatedButton] whose background color is the color scheme’s primary color with 50% opacity, but only when the button is pressed, one could write:

```dart
ElevatedButton(
  style: ButtonStyle(
    backgroundColor: WidgetStateProperty.resolveWith<Color?>(
      (Set<WidgetState> states) {
        if (states.contains(WidgetState.pressed)) {
          return Theme.of(context).colorScheme.primary.withValues(alpha: 0.5);
        }
        return null; // Use the component's default.
      },
    ),
  ),
  child: const Text('Fly me to the moon'),
  onPressed: () {
    // ...
  },
),
```

In this case the background color for all other button states would fallback to the ElevatedButton’s default values. To unconditionally set the button's [backgroundColor] for all states one could write:

```dart
ElevatedButton(
  style: const ButtonStyle(
    backgroundColor: WidgetStatePropertyAll<Color>(Colors.green),
  ),
  child: const Text('Let me play among the stars'),
  onPressed: () {
    // ...
  },
),
```

Configuring a ButtonStyle directly makes it possible to very precisely control the button’s visual attributes for all states. This level of control is typically required when a custom “branded” look and feel is desirable. However, in many cases it’s useful to make relatively sweeping changes based on a few initial parameters with simple values. The button styleFrom() methods enable such sweeping changes. See for example: [ElevatedButton.styleFrom], [FilledButton.styleFrom], [OutlinedButton.styleFrom], [TextButton.styleFrom].

For example, to override the default text and icon colors for a [TextButton], as well as its overlay color, with all of the standard opacity adjustments for the pressed, focused, and hovered states, one could write:

```dart
TextButton(
  style: TextButton.styleFrom(foregroundColor: Colors.green),
  child: const Text('Let me see what spring is like'),
  onPressed: () {
    // ...
  },
),
```

To configure all of the application's text buttons in the same way, specify the overall theme's `textButtonTheme`:

```dart
MaterialApp(
  theme: ThemeData(
    textButtonTheme: TextButtonThemeData(
      style: TextButton.styleFrom(foregroundColor: Colors.green),
    ),
  ),
  home: const MyAppHome(),
),
```

## Material 3 button types

Material Design 3 specifies five types of common buttons. Flutter provides support for these using the following button classes: <style>table,td,th { border-collapse: collapse; padding: 0.45em; } td { border: 1px solid }</style>

| Type         | Flutter implementation |
| :----------- | :--------------------- |
| Elevated     | [ElevatedButton]       |
| Filled       | [FilledButton]         |
| Filled Tonal | [FilledButton.tonal]   |
| Outlined     | [OutlinedButton]       |
| Text         | [TextButton]           |

{@tool dartpad} This sample shows how to create each of the Material 3 button types with Flutter.

** See code in examples/api/lib/material/button_style/button_style.0.dart ** {@end-tool}

See also:

- [ElevatedButtonTheme], the theme for [ElevatedButton]s.
- [FilledButtonTheme], the theme for [FilledButton]s.
- [OutlinedButtonTheme], the theme for [OutlinedButton]s.
- [TextButtonTheme], the theme for [TextButton]s.

### ButtonStyle()

```dart
ButtonStyle({WidgetStateProperty<TextStyle?>? textStyle, WidgetStateProperty<Color?>? backgroundColor, WidgetStateProperty<Color?>? foregroundColor, WidgetStateProperty<Color?>? overlayColor, WidgetStateProperty<Color?>? shadowColor, WidgetStateProperty<Color?>? surfaceTintColor, WidgetStateProperty<double?>? elevation, WidgetStateProperty<EdgeInsetsGeometry?>? padding, WidgetStateProperty<Size?>? minimumSize, WidgetStateProperty<Size?>? fixedSize, WidgetStateProperty<Size?>? maximumSize, WidgetStateProperty<Color?>? iconColor, WidgetStateProperty<double?>? iconSize, IconAlignment? iconAlignment, WidgetStateProperty<BorderSide?>? side, WidgetStateProperty<OutlinedBorder?>? shape, WidgetStateProperty<MouseCursor?>? mouseCursor, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory, ButtonLayerBuilder? backgroundBuilder, ButtonLayerBuilder? foregroundBuilder})
```

Create a [ButtonStyle].

### textStyle

```dart
WidgetStateProperty<TextStyle?>? textStyle
```

The style for a button's [Text] widget descendants.

The color of the [textStyle] is typically not used directly, the [foregroundColor] is used instead.

### backgroundColor

```dart
WidgetStateProperty<Color?>? backgroundColor
```

The button's background fill color.

### foregroundColor

```dart
WidgetStateProperty<Color?>? foregroundColor
```

The color for the button's [Text] widget descendants.

This color is typically used instead of the color of the [textStyle]. All of the components that compute defaults from [ButtonStyle] values compute a default [foregroundColor] and use that instead of the [textStyle]'s color.

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

The highlight color that's typically used to indicate that the button is focused, hovered, or pressed.

### shadowColor

```dart
WidgetStateProperty<Color?>? shadowColor
```

The shadow color of the button's [Material].

The material's elevation shadow can be difficult to see for dark themes, so by default the button classes add a semi-transparent overlay to indicate elevation. See [ThemeData.applyElevationOverlayColor].

### surfaceTintColor

```dart
WidgetStateProperty<Color?>? surfaceTintColor
```

The surface tint color of the button's [Material].

See [Material.surfaceTintColor] for more details.

### elevation

```dart
WidgetStateProperty<double?>? elevation
```

The elevation of the button's [Material].

### padding

```dart
WidgetStateProperty<EdgeInsetsGeometry?>? padding
```

The padding between the button's boundary and its child.

The vertical aspect of the default or user-specified padding is adjusted automatically based on [visualDensity].

When the visual density is [VisualDensity.compact], the top and bottom insets are reduced by 8 pixels or set to 0 pixels if the result of the reduced padding is negative. For example: the visual density defaults to [VisualDensity.compact] on desktop and web, so if the provided padding is 16 pixels on the top and bottom, it will be reduced to 8 pixels on the top and bottom. If the provided padding is 4 pixels, the result will be no padding on the top and bottom.

When the visual density is [VisualDensity.comfortable], the top and bottom insets are reduced by 4 pixels or set to 0 pixels if the result of the reduced padding is negative.

When the visual density is [VisualDensity.standard] the top and bottom insets are not changed. The visual density defaults to [VisualDensity.standard] on mobile.

See [ThemeData.visualDensity] for more details.

### minimumSize

```dart
WidgetStateProperty<Size?>? minimumSize
```

The minimum size of the button itself before applying [visualDensity].

The size of the rectangle the button lies within may be larger per [tapTargetSize].

This value must be less than or equal to [maximumSize].

The minimum size is adjusted automatically based on [visualDensity].

When visual density is [VisualDensity.compact], the minimum size is reduced by 8 pixels on both dimensions.

When visual density is [VisualDensity.comfortable], the minimum size is [minimumSize] reduced by 4 pixels on both dimensions.

When visual density is [VisualDensity.standard], the minimum size is [minimumSize].

### fixedSize

```dart
WidgetStateProperty<Size?>? fixedSize
```

The button's size.

This size is still constrained by the style's [minimumSize] and [maximumSize]. Fixed size dimensions whose value is [double.infinity] are ignored.

The size of the rectangle the button lies within may be larger per [tapTargetSize].

To specify buttons with a fixed width and the default height use `fixedSize: Size.fromWidth(320)`. Similarly, to specify a fixed height and the default width use `fixedSize: Size.fromHeight(100)`.

### maximumSize

```dart
WidgetStateProperty<Size?>? maximumSize
```

The maximum size of the button itself.

A [Size.infinite] or null value for this property means that the button's maximum size is not constrained.

This value must be greater than or equal to [minimumSize].

### iconColor

```dart
WidgetStateProperty<Color?>? iconColor
```

The icon's color inside of the button.

### iconSize

```dart
WidgetStateProperty<double?>? iconSize
```

The icon's size inside of the button.

### iconAlignment

```dart
IconAlignment? iconAlignment
```

The alignment of the button's icon.

This property is supported for the following button types:

- [ElevatedButton.icon].
- [FilledButton.icon].
- [FilledButton.tonalIcon].
- [OutlinedButton.icon].
- [TextButton.icon].

See also:

- [IconAlignment], for more information about the different icon alignments.

### side

```dart
WidgetStateProperty<BorderSide?>? side
```

The color and weight of the button's outline.

This value is combined with [shape] to create a shape decorated with an outline.

### shape

```dart
WidgetStateProperty<OutlinedBorder?>? shape
```

The shape of the button's underlying [Material].

This shape is combined with [side] to create a shape decorated with an outline.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over this button's [InkWell].

### visualDensity

```dart
VisualDensity? visualDensity
```

Defines how compact the button's layout will be.

{@macro flutter.material.themedata.visualDensity}

See also:

- [ThemeData.visualDensity], which specifies the [visualDensity] for all widgets within a [Theme].

### tapTargetSize

```dart
MaterialTapTargetSize? tapTargetSize
```

Configures the minimum size of the area within which the button may be pressed.

If the [tapTargetSize] is larger than [minimumSize], the button will include a transparent margin that responds to taps.

Always defaults to [ThemeData.materialTapTargetSize].

### animationDuration

```dart
Duration? animationDuration
```

Defines the duration of animated changes for [shape] and [elevation].

Typically the component default value is [kThemeChangeDuration].

### enableFeedback

```dart
bool? enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

Typically the component default value is true.

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### alignment

```dart
AlignmentGeometry? alignment
```

The alignment of the button's child.

Typically buttons are sized to be just big enough to contain the child and its padding. If the button's size is constrained to a fixed size, for example by enclosing it with a [SizedBox], this property defines how the child is aligned within the available space.

Always defaults to [Alignment.center].

### splashFactory

```dart
InteractiveInkFeatureFactory? splashFactory
```

Creates the [InkWell] splash factory, which defines the appearance of "ink" splashes that occur in response to taps.

Use [NoSplash.splashFactory] to defeat ink splash rendering. For example:

```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(
    splashFactory: NoSplash.splashFactory,
  ),
  onPressed: () { },
  child: const Text('No Splash'),
)
```

### backgroundBuilder

```dart
ButtonLayerBuilder? backgroundBuilder
```

Creates a widget that becomes the child of the button's [Material] and whose child is the rest of the button, including the button's `child` parameter.

The widget created by [backgroundBuilder] is constrained to be the same size as the overall button and will appear behind the button's child. The widget created by [foregroundBuilder] is constrained to be the same size as the button's child, i.e. it's inset by [ButtonStyle.padding] and aligned by the button's [ButtonStyle.alignment].

By default the returned widget is clipped to the Material's [ButtonStyle.shape].

See also:

- [foregroundBuilder], to create a widget that's as big as the button's child and is layered behind the child.
- [ButtonStyleButton.clipBehavior], for more information about configuring clipping.

### foregroundBuilder

```dart
ButtonLayerBuilder? foregroundBuilder
```

Creates a Widget that contains the button's child parameter which is used instead of the button's child.

The returned widget is clipped by the button's [ButtonStyle.shape], inset by the button's [ButtonStyle.padding] and aligned by the button's [ButtonStyle.alignment].

See also:

- [backgroundBuilder], to create a widget that's as big as the button and is layered behind the button's child.
- [ButtonStyleButton.clipBehavior], for more information about configuring clipping.

### copyWith()

```dart
ButtonStyle copyWith({WidgetStateProperty<TextStyle?>? textStyle, WidgetStateProperty<Color?>? backgroundColor, WidgetStateProperty<Color?>? foregroundColor, WidgetStateProperty<Color?>? overlayColor, WidgetStateProperty<Color?>? shadowColor, WidgetStateProperty<Color?>? surfaceTintColor, WidgetStateProperty<double?>? elevation, WidgetStateProperty<EdgeInsetsGeometry?>? padding, WidgetStateProperty<Size?>? minimumSize, WidgetStateProperty<Size?>? fixedSize, WidgetStateProperty<Size?>? maximumSize, WidgetStateProperty<Color?>? iconColor, WidgetStateProperty<double?>? iconSize, IconAlignment? iconAlignment, WidgetStateProperty<BorderSide?>? side, WidgetStateProperty<OutlinedBorder?>? shape, WidgetStateProperty<MouseCursor?>? mouseCursor, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory, ButtonLayerBuilder? backgroundBuilder, ButtonLayerBuilder? foregroundBuilder})
```

Returns a copy of this ButtonStyle with the given fields replaced with the new values.

### merge()

```dart
ButtonStyle merge(ButtonStyle? style)
```

Returns a copy of this ButtonStyle where the non-null fields in [style] have replaced the corresponding null fields in this ButtonStyle.

In other words, [style] is used to fill in unspecified (null) fields this ButtonStyle.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### lerp()

```dart
ButtonStyle? lerp(ButtonStyle? a, ButtonStyle? b, double t)
```

Linearly interpolate between two [ButtonStyle]s.
