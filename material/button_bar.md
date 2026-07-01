@docImport 'card.dart'; @docImport 'dropdown.dart'; @docImport 'elevated_button.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart'; @docImport 'theme_data.dart';

# ButtonBar

```dart
class ButtonBar extends StatelessWidget {}
```

An end-aligned row of buttons, laying out into a column if there is not enough horizontal space.

## Updating to [OverflowBar]

[ButtonBar] has been replaced by a more efficient widget, [OverflowBar].

```dart
// Before
// ignore: deprecated_member_use
ButtonBar(
  alignment: MainAxisAlignment.spaceEvenly,
  children: <Widget>[
    TextButton( child: const Text('Button 1'), onPressed: () {}),
    TextButton( child: const Text('Button 2'), onPressed: () {}),
    TextButton( child: const Text('Button 3'), onPressed: () {}),
  ],
);
```

```dart
// After
OverflowBar(
  alignment: MainAxisAlignment.spaceEvenly,
  children: <Widget>[
    TextButton( child: const Text('Button 1'), onPressed: () {}),
    TextButton( child: const Text('Button 2'), onPressed: () {}),
    TextButton( child: const Text('Button 3'), onPressed: () {}),
  ],
);
```

See the [OverflowBar] documentation for more details.

## Using [ButtonBar]

Places the buttons horizontally according to the [buttonPadding]. The children are laid out in a [Row] with [MainAxisAlignment.end]. When the [Directionality] is [TextDirection.ltr], the button bar's children are right justified and the last child becomes the rightmost child. When the [Directionality] [TextDirection.rtl] the children are left justified and the last child becomes the leftmost child.

If the button bar's width exceeds the maximum width constraint on the widget, it aligns its buttons in a column. The key difference here is that the [MainAxisAlignment] will then be treated as a cross-axis/horizontal alignment. For example, if the buttons overflow and [ButtonBar.alignment] was set to [MainAxisAlignment.start], the buttons would align to the horizontal start of the button bar.

The [ButtonBar] can be configured with a [ButtonBarTheme]. For any null property on the ButtonBar, the surrounding ButtonBarTheme's property will be used instead. If the ButtonBarTheme's property is null as well, the property will default to a value described in the field documentation below.

The [children] are wrapped in a [ButtonTheme] that is a copy of the surrounding ButtonTheme with the button properties overridden by the properties of the ButtonBar as described above. These properties include [buttonTextTheme], [buttonMinWidth], [buttonHeight], [buttonPadding], and [buttonAlignedDropdown].

Used by [Dialog] to arrange the actions at the bottom of the dialog.

See also:

- [TextButton], a simple flat button without a shadow.
- [ElevatedButton], a filled button whose material elevates when pressed.
- [OutlinedButton], a [TextButton] with a border outline.
- [Card], at the bottom of which it is common to place a [ButtonBar].
- [Dialog], which uses a [ButtonBar] for its actions.
- [ButtonBarTheme], which configures the [ButtonBar].

### ButtonBar()

```dart
ButtonBar({dynamic key, MainAxisAlignment? alignment, MainAxisSize? mainAxisSize, ButtonTextTheme? buttonTextTheme, double? buttonMinWidth, double? buttonHeight, EdgeInsetsGeometry? buttonPadding, bool? buttonAlignedDropdown, ButtonBarLayoutBehavior? layoutBehavior, VerticalDirection? overflowDirection, double? overflowButtonSpacing, List<Widget> children = const <Widget>[]})
```

Creates a button bar.

Both [buttonMinWidth] and [buttonHeight] must be non-negative if they are not null.

### alignment

```dart
MainAxisAlignment? alignment
```

How the children should be placed along the horizontal axis.

If null then it will use [ButtonBarThemeData.alignment]. If that is null, it will default to [MainAxisAlignment.end].

### mainAxisSize

```dart
MainAxisSize? mainAxisSize
```

How much horizontal space is available. See [Row.mainAxisSize].

If null then it will use the surrounding [ButtonBarThemeData.mainAxisSize]. If that is null, it will default to [MainAxisSize.max].

### buttonTextTheme

```dart
ButtonTextTheme? buttonTextTheme
```

Overrides the surrounding [ButtonBarThemeData.buttonTextTheme] to define a button's base colors, size, internal padding and shape.

If null then it will use the surrounding [ButtonBarThemeData.buttonTextTheme]. If that is null, it will default to [ButtonTextTheme.primary].

### buttonMinWidth

```dart
double? buttonMinWidth
```

Overrides the surrounding [ButtonThemeData.minWidth] to define a button's minimum width.

If null then it will use the surrounding [ButtonBarThemeData.buttonMinWidth]. If that is null, it will default to 64.0 logical pixels.

### buttonHeight

```dart
double? buttonHeight
```

Overrides the surrounding [ButtonThemeData.height] to define a button's minimum height.

If null then it will use the surrounding [ButtonBarThemeData.buttonHeight]. If that is null, it will default to 36.0 logical pixels.

### buttonPadding

```dart
EdgeInsetsGeometry? buttonPadding
```

Overrides the surrounding [ButtonThemeData.padding] to define the padding for a button's child (typically the button's label).

If null then it will use the surrounding [ButtonBarThemeData.buttonPadding]. If that is null, it will default to 8.0 logical pixels on the left and right.

### buttonAlignedDropdown

```dart
bool? buttonAlignedDropdown
```

Overrides the surrounding [ButtonThemeData.alignedDropdown] to define whether a [DropdownButton] menu's width will match the button's width.

If null then it will use the surrounding [ButtonBarThemeData.buttonAlignedDropdown]. If that is null, it will default to false.

### layoutBehavior

```dart
ButtonBarLayoutBehavior? layoutBehavior
```

Defines whether a [ButtonBar] should size itself with a minimum size constraint or with padding.

Overrides the surrounding [ButtonThemeData.layoutBehavior].

If null then it will use the surrounding [ButtonBarThemeData.layoutBehavior]. If that is null, it will default [ButtonBarLayoutBehavior.padded].

### overflowDirection

```dart
VerticalDirection? overflowDirection
```

Defines the vertical direction of a [ButtonBar]'s children if it overflows.

If [children] do not fit into a single row, then they are arranged in a column. The first action is at the top of the column if this property is set to [VerticalDirection.down], since it "starts" at the top and "ends" at the bottom. On the other hand, the first action will be at the bottom of the column if this property is set to [VerticalDirection.up], since it "starts" at the bottom and "ends" at the top.

If null then it will use the surrounding [ButtonBarThemeData.overflowDirection]. If that is null, it will default to [VerticalDirection.down].

### overflowButtonSpacing

```dart
double? overflowButtonSpacing
```

The spacing between buttons when the button bar overflows.

If the [children] do not fit into a single row, they are arranged into a column. This parameter provides additional vertical space in between buttons when it does overflow.

The button spacing may appear to be more than the value provided. This is because most buttons adhere to the [MaterialTapTargetSize] of 48px. So, even though a button might visually be 36px in height, it might still take up to 48px vertically.

If null then no spacing will be added in between buttons in an overflow state.

### children

```dart
List<Widget> children
```

The buttons to arrange horizontally.

Typically [ElevatedButton] or [TextButton] widgets.

### build()

```dart
Widget build(BuildContext context)
```
