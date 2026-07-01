@docImport 'elevated_button_theme.dart'; @docImport 'menu_anchor.dart'; @docImport 'text_button_theme.dart'; @docImport 'text_theme.dart'; @docImport 'theme.dart';

# IconAlignment

```dart
enum IconAlignment {}
```

{@template flutter.material.ButtonStyle.iconAlignment} Determines the alignment of the icon within the widgets such as:

- [ElevatedButton.icon],
- [FilledButton.icon],
- [FilledButton.tonalIcon].
- [OutlinedButton.icon],
- [TextButton.icon],

The effect of `iconAlignment` depends on [TextDirection]. If textDirection is [TextDirection.ltr] then [IconAlignment.start] and [IconAlignment.end] align the icon on the left or right respectively. If textDirection is [TextDirection.rtl] the the alignments are reversed.

Defaults to [IconAlignment.start].

{@tool dartpad} This sample demonstrates how to use `iconAlignment` to align the button icon to the start or the end of the button.

** See code in examples/api/lib/material/icon_alignment/icon_alignment.0.dart ** {@end-tool}

{@endtemplate}

The icon is placed at the start of the button.

The icon is placed at the end of the button.

# ButtonStyleButton

```dart
abstract class ButtonStyleButton extends StatefulWidget {}
```

The base [StatefulWidget] class for buttons whose style is defined by a [ButtonStyle] object.

Concrete subclasses must override [defaultStyleOf] and [themeStyleOf].

See also:

- [ElevatedButton], a filled button whose material elevates when pressed.
- [FilledButton], a filled button that doesn't elevate when pressed.
- [FilledButton.tonal], a filled button variant that uses a secondary fill color.
- [OutlinedButton], a button with an outlined border and no fill color.
- [TextButton], a button with no outline or fill color.
- <https://m3.material.io/components/buttons/overview>, an overview of each of the Material Design button types and how they should be used in designs.

### ButtonStyleButton()

```dart
ButtonStyleButton({dynamic key, required VoidCallback? onPressed, required VoidCallback? onLongPress, required ValueChanged<bool>? onHover, required ValueChanged<bool>? onFocusChange, required ButtonStyle? style, required FocusNode? focusNode, required bool autofocus, required Clip? clipBehavior, MaterialStatesController? statesController, bool? isSemanticButton = true, IconAlignment? iconAlignment, String? tooltip, required Widget? child})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### onPressed

```dart
VoidCallback? onPressed
```

Called when the button is tapped or otherwise activated.

If this callback and [onLongPress] are null, then the button will be disabled.

See also:

- [enabled], which is true if the button is enabled.

### onLongPress

```dart
VoidCallback? onLongPress
```

Called when the button is long-pressed.

If this callback and [onPressed] are null, then the button will be disabled.

See also:

- [enabled], which is true if the button is enabled.

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the button response area.

The value passed to the callback is true if a pointer has entered this part of the material and false if a pointer has exited this part of the material.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus.

### style

```dart
ButtonStyle? style
```

Customizes this button's appearance.

Non-null properties of this style override the corresponding properties in [themeStyleOf] and [defaultStyleOf]. [WidgetStateProperty]s that resolve to non-null values will similarly override the corresponding [WidgetStateProperty]s in [themeStyleOf] and [defaultStyleOf].

Null by default.

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none] unless [ButtonStyle.backgroundBuilder] or [ButtonStyle.foregroundBuilder] is specified. In those cases the default is [Clip.antiAlias].

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### statesController

```dart
MaterialStatesController? statesController
```

{@macro flutter.material.inkwell.statesController}

### isSemanticButton

```dart
bool? isSemanticButton
```

Determine whether this subtree represents a button.

If this is null, the screen reader will not announce "button" when this is focused. This is useful for [MenuItemButton] and [SubmenuButton] when we traverse the menu system.

Defaults to true.

### iconAlignment

```dart
IconAlignment? iconAlignment
```

{@macro flutter.material.ButtonStyle.iconAlignment}

### tooltip

```dart
String? tooltip
```

Text that describes the action that will occur when the button is pressed or hovered over.

This text is displayed when the user long-presses or hovers over the button in a tooltip. This string is also used for accessibility.

If null, the button will not display a tooltip.

### child

```dart
Widget? child
```

Typically the button's label.

{@macro flutter.widgets.ProxyWidget.child}

### defaultStyleOf()

```dart
ButtonStyle defaultStyleOf(BuildContext context)
```

Returns a [ButtonStyle] that's based primarily on the [Theme]'s [ThemeData.textTheme] and [ThemeData.colorScheme], but has most values filled out (non-null).

The returned style can be overridden by the [style] parameter and by the style returned by [themeStyleOf] that some button-specific themes like [TextButtonTheme] or [ElevatedButtonTheme] override. For example the default style of the [TextButton] subclass can be overridden with its [TextButton.style] constructor parameter, or with a [TextButtonTheme].

Concrete button subclasses should return a [ButtonStyle] with as many non-null properties as possible, where all of the non-null [WidgetStateProperty] properties resolve to non-null values.

## Properties that can be null

Some properties, like [ButtonStyle.fixedSize] would override other values in the same [ButtonStyle] if set, so they are allowed to be null. Here is a summary of properties that are allowed to be null when returned in the [ButtonStyle] returned by this function, an why:

- [ButtonStyle.fixedSize] because it would override other values in the same [ButtonStyle], like [ButtonStyle.maximumSize].
- [ButtonStyle.side] because null is a valid value for a button that has no side. [OutlinedButton] returns a non-null default for this, however.
- [ButtonStyle.backgroundBuilder] and [ButtonStyle.foregroundBuilder] because they would override the [ButtonStyle.foregroundColor] and [ButtonStyle.backgroundColor] of the same [ButtonStyle].

See also:

- [themeStyleOf], returns the ButtonStyle of this button's component theme.

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```

Returns the ButtonStyle that belongs to the button's component theme.

The returned style can be overridden by the [style] parameter.

Concrete button subclasses should return the ButtonStyle for the nearest subclass-specific inherited theme, and if no such theme exists, then the same value from the overall [Theme].

See also:

- [defaultStyleOf], Returns the default [ButtonStyle] for this button.

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled.

Buttons are disabled by default. To enable a button, set its [onPressed] or [onLongPress] properties to a non-null value.

### createState()

```dart
State<ButtonStyleButton> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### allOrNull()

```dart
WidgetStateProperty<T>? allOrNull<T>(T? value)
```

Returns null if [value] is null, otherwise `WidgetStatePropertyAll<T>(value)`.

A convenience method for subclasses.

### defaultColor()

```dart
WidgetStateProperty<Color?>? defaultColor(Color? enabled, Color? disabled)
```

Returns null if [enabled] and [disabled] are null. Otherwise, returns a [WidgetStateProperty] that resolves to [disabled] when [WidgetState.disabled] is active, and [enabled] otherwise.

A convenience method for subclasses.

### scaledPadding()

```dart
EdgeInsetsGeometry scaledPadding(EdgeInsetsGeometry geometry1x, EdgeInsetsGeometry geometry2x, EdgeInsetsGeometry geometry3x, double fontSizeMultiplier)
```

A convenience method used by subclasses in the framework, that returns an interpolated value based on the [fontSizeMultiplier] parameter:

- 0 - 1 [geometry1x]
- 1 - 2 lerp([geometry1x], [geometry2x], [fontSizeMultiplier] - 1)
- 2 - 3 lerp([geometry2x], [geometry3x], [fontSizeMultiplier] - 2)
- otherwise [geometry3x]

This method is used by the framework for estimating the default paddings to use on a button with a text label, when the system text scaling setting changes. It's usually supplied with empirical [geometry1x], [geometry2x], [geometry3x] values adjusted for different system text scaling values, when the unscaled font size is set to 14.0 (the default [TextTheme.labelLarge] value).

The `fontSizeMultiplier` argument, for historical reasons, is the default font size specified in the [ButtonStyle], scaled by the ambient font scaler, then divided by 14.0 (the default font size used in buttons).
