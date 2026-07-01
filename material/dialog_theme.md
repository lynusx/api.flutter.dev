@docImport 'dialog.dart';

# DialogTheme

```dart
class DialogTheme extends InheritedTheme with Diagnosticable {}
```

Defines a theme for [Dialog] widgets.

Descendant widgets obtain the current [DialogThemeData] object using [DialogTheme.of]. Instances of [DialogThemeData] can be customized with [DialogThemeData.copyWith].

[titleTextStyle] and [contentTextStyle] are used in [AlertDialog]s and [SimpleDialog]s.

See also:

- [Dialog], a dialog that can be customized using this [DialogTheme].
- [AlertDialog], a dialog that can be customized using this [DialogTheme].
- [SimpleDialog], a dialog that can be customized using this [DialogTheme].
- [ThemeData], which describes the overall theme information for the application.

### DialogTheme()

```dart
DialogTheme({dynamic key, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, AlignmentGeometry? alignment, Color? iconColor, TextStyle? titleTextStyle, TextStyle? contentTextStyle, EdgeInsetsGeometry? actionsPadding, Color? barrierColor, EdgeInsets? insetPadding, Clip? clipBehavior, DialogThemeData? data, Widget? child})
```

Creates a dialog theme that can be used for [ThemeData.dialogTheme].

### backgroundColor

```dart
Color? get backgroundColor
```

Overrides the default value for [Dialog.backgroundColor].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.backgroundColor] property in [data] instead.

### elevation

```dart
double? get elevation
```

Overrides the default value for [Dialog.elevation].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.elevation] property in [data] instead.

### shadowColor

```dart
Color? get shadowColor
```

Overrides the default value for [Dialog.shadowColor].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.shadowColor] property in [data] instead.

### surfaceTintColor

```dart
Color? get surfaceTintColor
```

Overrides the default value for [Dialog.surfaceTintColor].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.surfaceTintColor] property in [data] instead.

### shape

```dart
ShapeBorder? get shape
```

Overrides the default value for [Dialog.shape].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.shape] property in [data] instead.

### alignment

```dart
AlignmentGeometry? get alignment
```

Overrides the default value for [Dialog.alignment].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.alignment] property in [data] instead.

### titleTextStyle

```dart
TextStyle? get titleTextStyle
```

Overrides the default value for [DefaultTextStyle] for [SimpleDialog.title] and [AlertDialog.title].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.titleTextStyle] property in [data] instead.

### contentTextStyle

```dart
TextStyle? get contentTextStyle
```

Overrides the default value for [DefaultTextStyle] for [SimpleDialog.children] and [AlertDialog.content].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.contentTextStyle] property in [data] instead.

### actionsPadding

```dart
EdgeInsetsGeometry? get actionsPadding
```

Overrides the default value for [AlertDialog.actionsPadding].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.actionsPadding] property in [data] instead.

### iconColor

```dart
Color? get iconColor
```

Used to configure the [IconTheme] for the [AlertDialog.icon] widget.

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.iconColor] property in [data] instead.

### barrierColor

```dart
Color? get barrierColor
```

Overrides the default value for [barrierColor] in [showDialog].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.barrierColor] property in [data] instead.

### insetPadding

```dart
EdgeInsets? get insetPadding
```

Overrides the default value for [Dialog.insetPadding].

### clipBehavior

```dart
Clip? get clipBehavior
```

Overrides the default value of [Dialog.clipBehavior].

This property is obsolete and will be deprecated in a future release: please use the [DialogThemeData.clipBehavior] property in [data] instead.

### data

```dart
DialogThemeData get data
```

The properties used for all descendant [Dialog] widgets.

### of()

```dart
DialogThemeData of(BuildContext context)
```

Retrieves the [DialogThemeData] from the closest ancestor [DialogTheme].

If there is no enclosing [DialogTheme] widget, then [ThemeData.dialogTheme] is used.

Typical usage is as follows:

```dart
DialogThemeData theme = DialogTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DialogTheme oldWidget)
```

### copyWith()

```dart
DialogTheme copyWith({Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, AlignmentGeometry? alignment, Color? iconColor, TextStyle? titleTextStyle, TextStyle? contentTextStyle, EdgeInsetsGeometry? actionsPadding, Color? barrierColor, EdgeInsets? insetPadding, Clip? clipBehavior})
```

Creates a copy of this object but with the given fields replaced with the new values.

This method is obsolete and will be deprecated in a future release: please use the [DialogThemeData.copyWith] instead.

### lerp()

```dart
DialogTheme lerp(DialogTheme? a, DialogTheme? b, double t)
```

Linearly interpolate between two dialog themes.

{@macro dart.ui.shadow.lerp}

This method is obsolete and will be deprecated in a future release: please use the [DialogThemeData.lerp] instead.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DialogThemeData

```dart
class DialogThemeData with Diagnosticable {}
```

Defines default property values for descendant [Dialog] widgets.

Descendant widgets obtain the current [DialogThemeData] object using [DialogTheme.of]. Instances of [DialogThemeData] can be customized with [DialogThemeData.copyWith].

Typically a [DialogThemeData] is specified as part of the overall [Theme] with [ThemeData.dialogTheme].

All [DialogThemeData] properties are `null` by default. When null, the [Dialog] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults. See the individual [Dialog] properties for details.

See also:

- [Dialog], a dialog that can be customized using this [DialogTheme].
- [AlertDialog], a dialog that can be customized using this [DialogTheme].
- [SimpleDialog], a dialog that can be customized using this [DialogTheme].
- [ThemeData], which describes the overall theme information for the application.

### DialogThemeData()

```dart
DialogThemeData({Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, AlignmentGeometry? alignment, Color? iconColor, TextStyle? titleTextStyle, TextStyle? contentTextStyle, EdgeInsetsGeometry? actionsPadding, Color? barrierColor, EdgeInsets? insetPadding, Clip? clipBehavior, BoxConstraints? constraints})
```

Creates a dialog theme that can be used for [ThemeData.dialogTheme].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value for [Dialog.backgroundColor].

### elevation

```dart
double? elevation
```

Overrides the default value for [Dialog.elevation].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value for [Dialog.shadowColor].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value for [Dialog.surfaceTintColor].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value for [Dialog.shape].

### alignment

```dart
AlignmentGeometry? alignment
```

Overrides the default value for [Dialog.alignment].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

Overrides the default value for [DefaultTextStyle] for [SimpleDialog.title] and [AlertDialog.title].

### contentTextStyle

```dart
TextStyle? contentTextStyle
```

Overrides the default value for [DefaultTextStyle] for [SimpleDialog.children] and [AlertDialog.content].

### actionsPadding

```dart
EdgeInsetsGeometry? actionsPadding
```

Overrides the default value for [AlertDialog.actionsPadding].

### iconColor

```dart
Color? iconColor
```

Used to configure the [IconTheme] for the [AlertDialog.icon] widget.

### barrierColor

```dart
Color? barrierColor
```

Overrides the default value for [barrierColor] in [showDialog].

### insetPadding

```dart
EdgeInsets? insetPadding
```

Overrides the default value for [Dialog.insetPadding].

### clipBehavior

```dart
Clip? clipBehavior
```

Overrides the default value of [Dialog.clipBehavior].

### constraints

```dart
BoxConstraints? constraints
```

Constrains the size of the [Dialog].

If null, the bottom sheet's size will be unconstrained.

### copyWith()

```dart
DialogThemeData copyWith({Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, AlignmentGeometry? alignment, Color? iconColor, TextStyle? titleTextStyle, TextStyle? contentTextStyle, EdgeInsetsGeometry? actionsPadding, Color? barrierColor, EdgeInsets? insetPadding, Clip? clipBehavior, BoxConstraints? constraints})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
DialogThemeData lerp(DialogThemeData? a, DialogThemeData? b, double t)
```

Linearly interpolate between two [DialogThemeData].

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
