@docImport 'bottom_sheet.dart'; @docImport 'material.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart';

# BottomSheetThemeData

```dart
class BottomSheetThemeData with Diagnosticable {}
```

Defines default property values for [BottomSheet]'s [Material].

Descendant widgets obtain the current [BottomSheetThemeData] object using `Theme.of(context).bottomSheetTheme`. Instances of [BottomSheetThemeData] can be customized with [BottomSheetThemeData.copyWith].

Typically a [BottomSheetThemeData] is specified as part of the overall [Theme] with [ThemeData.bottomSheetTheme].

All [BottomSheetThemeData] properties are `null` by default. When null, the [BottomSheet] will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### BottomSheetThemeData()

```dart
BottomSheetThemeData({Color? backgroundColor, Color? surfaceTintColor, double? elevation, Color? modalBackgroundColor, Color? modalBarrierColor, Color? shadowColor, double? modalElevation, ShapeBorder? shape, bool? showDragHandle, Color? dragHandleColor, Size? dragHandleSize, Clip? clipBehavior, BoxConstraints? constraints})
```

Creates a theme that can be used for [ThemeData.bottomSheetTheme].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value for [BottomSheet.backgroundColor].

If null, [BottomSheet] defaults to [Material]'s default.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value for surfaceTintColor.

If null, [BottomSheet] will not display an overlay color.

See [Material.surfaceTintColor] for more details.

### elevation

```dart
double? elevation
```

Overrides the default value for [BottomSheet.elevation].

{@macro flutter.material.material.elevation}

If null, [BottomSheet] defaults to 0.0.

### modalBackgroundColor

```dart
Color? modalBackgroundColor
```

Value for [BottomSheet.backgroundColor] when the Bottom sheet is presented as a modal bottom sheet.

### modalBarrierColor

```dart
Color? modalBarrierColor
```

Overrides the default value for barrier color when the Bottom sheet is presented as a modal bottom sheet.

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value for [BottomSheet.shadowColor].

### modalElevation

```dart
double? modalElevation
```

Value for [BottomSheet.elevation] when the Bottom sheet is presented as a modal bottom sheet.

### shape

```dart
ShapeBorder? shape
```

Overrides the default value for [BottomSheet.shape].

If null, no overriding shape is specified for [BottomSheet], so the [BottomSheet] is rectangular.

### showDragHandle

```dart
bool? showDragHandle
```

Overrides the default value for [BottomSheet.showDragHandle].

### dragHandleColor

```dart
Color? dragHandleColor
```

Overrides the default value for [BottomSheet.dragHandleColor].

### dragHandleSize

```dart
Size? dragHandleSize
```

Overrides the default value for [BottomSheet.dragHandleSize].

### clipBehavior

```dart
Clip? clipBehavior
```

Overrides the default value for [BottomSheet.clipBehavior].

If null, [BottomSheet] uses [Clip.none].

### constraints

```dart
BoxConstraints? constraints
```

Constrains the size of the [BottomSheet].

If null, the bottom sheet's size will be unconstrained.

### copyWith()

```dart
BottomSheetThemeData copyWith({Color? backgroundColor, Color? surfaceTintColor, double? elevation, Color? modalBackgroundColor, Color? modalBarrierColor, Color? shadowColor, double? modalElevation, ShapeBorder? shape, bool? showDragHandle, Color? dragHandleColor, Size? dragHandleSize, Clip? clipBehavior, BoxConstraints? constraints})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
BottomSheetThemeData? lerp(BottomSheetThemeData? a, BottomSheetThemeData? b, double t)
```

Linearly interpolate between two bottom sheet themes.

If both arguments are null then null is returned.

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
