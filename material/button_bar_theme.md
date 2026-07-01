@docImport 'button_bar.dart'; @docImport 'dropdown.dart'; @docImport 'text_theme.dart';

# ButtonBarThemeData

```dart
class ButtonBarThemeData with Diagnosticable {}
```

Defines the visual properties of [ButtonBar] widgets.

Used by [ButtonBarTheme] to control the visual properties of [ButtonBar] instances in a widget subtree.

To obtain this configuration, use [ButtonBarTheme.of] to access the closest ancestor [ButtonBarTheme] of the current [BuildContext].

See also:

- [ButtonBarTheme], an [InheritedWidget] that propagates the theme down its subtree.
- [ButtonBar], which uses this to configure itself and its children button widgets.

### ButtonBarThemeData()

```dart
ButtonBarThemeData({MainAxisAlignment? alignment, MainAxisSize? mainAxisSize, ButtonTextTheme? buttonTextTheme, double? buttonMinWidth, double? buttonHeight, EdgeInsetsGeometry? buttonPadding, bool? buttonAlignedDropdown, ButtonBarLayoutBehavior? layoutBehavior, VerticalDirection? overflowDirection})
```

Constructs the set of properties used to configure [ButtonBar] widgets.

Both [buttonMinWidth] and [buttonHeight] must be non-negative if they are not null.

### alignment

```dart
MainAxisAlignment? alignment
```

How the children should be placed along the horizontal axis.

### mainAxisSize

```dart
MainAxisSize? mainAxisSize
```

How much horizontal space is available. See [Row.mainAxisSize].

### buttonTextTheme

```dart
ButtonTextTheme? buttonTextTheme
```

Defines a [ButtonBar] button's base colors, and the defaults for the button's minimum size, internal padding, and shape.

This will override the surrounding [ButtonThemeData.textTheme] setting for buttons contained in the [ButtonBar].

Despite the name, this property is not a [TextTheme], its value is not a collection of [TextStyle]s.

### buttonMinWidth

```dart
double? buttonMinWidth
```

The minimum width for [ButtonBar] buttons.

This will override the surrounding [ButtonThemeData.minWidth] setting for buttons contained in the [ButtonBar].

The actual horizontal space allocated for a button's child is at least this value less the theme's horizontal [ButtonThemeData.padding].

### buttonHeight

```dart
double? buttonHeight
```

The minimum height for [ButtonBar] buttons.

This will override the surrounding [ButtonThemeData.height] setting for buttons contained in the [ButtonBar].

### buttonPadding

```dart
EdgeInsetsGeometry? buttonPadding
```

Padding for a [ButtonBar] button's child (typically the button's label).

This will override the surrounding [ButtonThemeData.padding] setting for buttons contained in the [ButtonBar].

### buttonAlignedDropdown

```dart
bool? buttonAlignedDropdown
```

If true, then a [DropdownButton] menu's width will match the [ButtonBar] button's width.

If false, then the dropdown's menu will be wider than its button. In either case the dropdown button will line up the leading edge of the menu's value with the leading edge of the values displayed by the menu items.

This will override the surrounding [ButtonThemeData.alignedDropdown] setting for buttons contained in the [ButtonBar].

This property only affects [DropdownButton] contained in a [ButtonBar] and its menu.

### layoutBehavior

```dart
ButtonBarLayoutBehavior? layoutBehavior
```

Defines whether a [ButtonBar] should size itself with a minimum size constraint or with padding.

### overflowDirection

```dart
VerticalDirection? overflowDirection
```

Defines the vertical direction of a [ButtonBar]'s children if it overflows.

If the [ButtonBar]'s children do not fit into a single row, then they are arranged in a column. The first action is at the top of the column if this property is set to [VerticalDirection.down], since it "starts" at the top and "ends" at the bottom. On the other hand, the first action will be at the bottom of the column if this property is set to [VerticalDirection.up], since it "starts" at the bottom and "ends" at the top.

### copyWith()

```dart
ButtonBarThemeData copyWith({MainAxisAlignment? alignment, MainAxisSize? mainAxisSize, ButtonTextTheme? buttonTextTheme, double? buttonMinWidth, double? buttonHeight, EdgeInsetsGeometry? buttonPadding, bool? buttonAlignedDropdown, ButtonBarLayoutBehavior? layoutBehavior, VerticalDirection? overflowDirection})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
ButtonBarThemeData? lerp(ButtonBarThemeData? a, ButtonBarThemeData? b, double t)
```

Linearly interpolate between two button bar themes.

If both arguments are null, then null is returned.

{@macro dart.ui.shadow.lerp}

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

# ButtonBarTheme

```dart
class ButtonBarTheme extends InheritedWidget {}
```

Applies a button bar theme to descendant [ButtonBar] widgets.

A button bar theme describes the layout and properties for the buttons contained in a [ButtonBar].

Descendant widgets obtain the current theme's [ButtonBarTheme] object using [ButtonBarTheme.of]. When a widget uses [ButtonBarTheme.of], it is automatically rebuilt if the theme later changes.

A button bar theme can be specified as part of the overall Material theme using [ThemeData.buttonBarTheme].

See also:

- [ButtonBarThemeData], which describes the actual configuration of a button bar theme.

### ButtonBarTheme()

```dart
ButtonBarTheme({dynamic key, required ButtonBarThemeData data, required dynamic child})
```

Constructs a button bar theme that configures all descendant [ButtonBar] widgets.

### data

```dart
ButtonBarThemeData data
```

The properties used for all descendant [ButtonBar] widgets.

### of()

```dart
ButtonBarThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [ButtonBarTheme] ancestor. If there is no ancestor, it returns [ThemeData.buttonBarTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
// ignore: deprecated_member_use
ButtonBarThemeData theme = ButtonBarTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ButtonBarTheme oldWidget)
```
