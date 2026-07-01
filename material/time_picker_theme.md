@docImport 'color_scheme.dart'; @docImport 'dialog.dart'; @docImport 'icon_button.dart'; @docImport 'text_field.dart'; @docImport 'text_theme.dart'; @docImport 'time_picker.dart';

# TimePickerThemeData

```dart
class TimePickerThemeData with Diagnosticable {}
```

Defines the visual properties of the widget displayed with [showTimePicker].

Descendant widgets obtain the current [TimePickerThemeData] object using [TimePickerTheme.of]. Instances of [TimePickerThemeData] can be customized with [TimePickerThemeData.copyWith].

Typically a [TimePickerThemeData] is specified as part of the overall [Theme] with [ThemeData.timePickerTheme].

All [TimePickerThemeData] properties are `null` by default. When null, [showTimePicker] will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.
- [TimePickerTheme], which describes the actual configuration of a time picker theme.

### TimePickerThemeData()

```dart
TimePickerThemeData({Color? backgroundColor, ButtonStyle? cancelButtonStyle, ButtonStyle? confirmButtonStyle, BorderSide? dayPeriodBorderSide, Color? dayPeriodColor, OutlinedBorder? dayPeriodShape, Color? dayPeriodTextColor, TextStyle? dayPeriodTextStyle, Color? dialBackgroundColor, Color? dialHandColor, Color? dialTextColor, TextStyle? dialTextStyle, double? elevation, Color? entryModeIconColor, TextStyle? helpTextStyle, Color? hourMinuteColor, ShapeBorder? hourMinuteShape, Color? hourMinuteTextColor, TextStyle? hourMinuteTextStyle, Object? inputDecorationTheme, EdgeInsetsGeometry? padding, ShapeBorder? shape, WidgetStateProperty<Color?>? timeSelectorSeparatorColor, WidgetStateProperty<TextStyle?>? timeSelectorSeparatorTextStyle})
```

Creates a theme that can be used for [TimePickerTheme] or [ThemeData.timePickerTheme].

### backgroundColor

```dart
Color? backgroundColor
```

The background color of a time picker.

If this is null, the time picker defaults to the overall theme's [ColorScheme.surfaceContainerHigh].

### cancelButtonStyle

```dart
ButtonStyle? cancelButtonStyle
```

The style of the cancel button of a [TimePickerDialog].

### confirmButtonStyle

```dart
ButtonStyle? confirmButtonStyle
```

The style of the confirm (OK) button of a [TimePickerDialog].

### dayPeriodBorderSide

```dart
BorderSide? dayPeriodBorderSide
```

The color and weight of the day period's outline.

If this is null, the time picker defaults to:

```dart
BorderSide(
  color: Color.alphaBlend(
    Theme.of(context).colorScheme.onSurface.withValues(alpha: 0.38),
    Theme.of(context).colorScheme.surface,
  ),
),
```

### dayPeriodColor

```dart
Color? get dayPeriodColor
```

The background color of the AM/PM toggle.

If [dayPeriodColor] is a [WidgetStateColor], then the effective background color can depend on the [WidgetState.selected] state, i.e. if the segment is selected or not.

By default, if the segment is selected, the overall theme's `ColorScheme.primary.withValues(alpha: 0.12)` is used when the overall theme's brightness is [Brightness.light] and `ColorScheme.primary.withValues(alpha: 0.24)` is used when the overall theme's brightness is [Brightness.dark]. If the segment is not selected, [Colors.transparent] is used to allow the [Dialog]'s color to be used.

### dayPeriodShape

```dart
OutlinedBorder? dayPeriodShape
```

The shape of the day period that the time picker uses.

If this is null, the time picker defaults to:

```dart
const RoundedRectangleBorder(
  borderRadius: BorderRadius.all(Radius.circular(4.0)),
  side: BorderSide(),
)
```

### dayPeriodTextColor

```dart
Color? dayPeriodTextColor
```

The color of the day period text that represents AM/PM.

If [dayPeriodTextColor] is a [WidgetStateColor], then the effective text color can depend on the [WidgetState.selected] state, i.e. if the text is selected or not.

By default the overall theme's [ColorScheme.primary] color is used when the text is selected and `ColorScheme.onSurface.withOpacity(0.60)` when it's not selected.

### dayPeriodTextStyle

```dart
TextStyle? dayPeriodTextStyle
```

Used to configure the [TextStyle]s for the day period control.

If this is null, the time picker defaults to the overall theme's [TextTheme.titleMedium].

### dialBackgroundColor

```dart
Color? dialBackgroundColor
```

The background color of the time picker dial when the entry mode is [TimePickerEntryMode.dial] or [TimePickerEntryMode.dialOnly].

If this is null and [ThemeData.useMaterial3] is true, the time picker dial background color defaults [ColorScheme.surfaceContainerHighest] color.

If this is null and [ThemeData.useMaterial3] is false, the time picker dial background color defaults to [ColorScheme.onSurface] color with an opacity of 0.08 when the overall theme's brightness is [Brightness.light] and [ColorScheme.onSurface] color with an opacity of 0.12 when the overall theme's brightness is [Brightness.dark].

### dialHandColor

```dart
Color? dialHandColor
```

The color of the time picker dial's hand when the entry mode is [TimePickerEntryMode.dial] or [TimePickerEntryMode.dialOnly].

If this is null, the time picker defaults to the overall theme's [ColorScheme.primary].

### dialTextColor

```dart
Color? dialTextColor
```

The color of the dial text that represents specific hours and minutes.

If [dialTextColor] is a [WidgetStateColor], then the effective text color can depend on the [WidgetState.selected] state, i.e. if the text is selected or not.

If this color is null then the dial's text colors are based on the theme's [ThemeData.colorScheme].

### dialTextStyle

```dart
TextStyle? dialTextStyle
```

The [TextStyle] for the numbers on the time selection dial.

If [dialTextStyle]'s [TextStyle.color] is a [WidgetStateColor], then the effective text color can depend on the [WidgetState.selected] state, i.e. if the text is selected or not.

If this style is null then the dial's text style is based on the theme's [ThemeData.textTheme].

### elevation

```dart
double? elevation
```

The Material elevation for the time picker dialog.

### entryModeIconColor

```dart
Color? entryModeIconColor
```

The color of the entry mode [IconButton].

If this is null, the time picker defaults to:

```dart
Theme.of(context).colorScheme.onSurface.withValues(
  alpha: Theme.of(context).colorScheme.brightness == Brightness.dark
    ? 1.0
    : 0.6,
)
```

### helpTextStyle

```dart
TextStyle? helpTextStyle
```

Used to configure the [TextStyle]s for the helper text in the header.

If this is null, the time picker defaults to the overall theme's [TextTheme.labelSmall].

### hourMinuteColor

```dart
Color? hourMinuteColor
```

The background color of the hour and minute header segments.

If [hourMinuteColor] is a [WidgetStateColor], then the effective background color can depend on the [WidgetState.selected] state, i.e. if the segment is selected or not.

By default, if the segment is selected, the overall theme's `ColorScheme.primary.withValues(alpha: 0.12)` is used when the overall theme's brightness is [Brightness.light] and `ColorScheme.primary.withValues(alpha: 0.24)` is used when the overall theme's brightness is [Brightness.dark]. If the segment is not selected, the overall theme's `ColorScheme.onSurface.withValues(alpha: 0.12)` is used.

### hourMinuteShape

```dart
ShapeBorder? hourMinuteShape
```

The shape of the hour and minute controls that the time picker uses.

If this is null, the time picker defaults to `RoundedRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(4.0)))`.

### hourMinuteTextColor

```dart
Color? hourMinuteTextColor
```

The color of the header text that represents hours and minutes.

If [hourMinuteTextColor] is a [WidgetStateColor], then the effective text color can depend on the [WidgetState.selected] state, i.e. if the text is selected or not.

By default the overall theme's [ColorScheme.primary] color is used when the text is selected and [ColorScheme.onSurface] when it's not selected.

### hourMinuteTextStyle

```dart
TextStyle? hourMinuteTextStyle
```

Used to configure the [TextStyle]s for the hour/minute controls.

If this is null and entry mode is [TimePickerEntryMode.dial], the time picker defaults to the overall theme's [TextTheme.displayLarge] with the value of [hourMinuteTextColor].

If this is null and entry mode is [TimePickerEntryMode.input], the time picker defaults to the overall theme's [TextTheme.displayMedium] with the value of [hourMinuteTextColor].

If this is null and [ThemeData.useMaterial3] is false, the time picker defaults to the overall theme's [TextTheme.displayMedium].

### inputDecorationTheme

```dart
InputDecorationThemeData? get inputDecorationTheme
```

The input decoration theme for the [TextField]s in the time picker.

If this is null, the time picker provides its own defaults.

### padding

```dart
EdgeInsetsGeometry? padding
```

The padding around the time picker dialog when the entry mode is [TimePickerEntryMode.dial] or [TimePickerEntryMode.dialOnly].

### shape

```dart
ShapeBorder? shape
```

The shape of the [Dialog] that the time picker is presented in.

If this is null, the time picker defaults to `RoundedRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(4.0)))`.

### timeSelectorSeparatorColor

```dart
WidgetStateProperty<Color?>? timeSelectorSeparatorColor
```

The color of the time selector separator between the hour and minute controls.

if this is null, the time picker defaults to the overall theme's [ColorScheme.onSurface].

If this is null and [ThemeData.useMaterial3] is false, then defaults to the value of [hourMinuteTextColor].

### timeSelectorSeparatorTextStyle

```dart
WidgetStateProperty<TextStyle?>? timeSelectorSeparatorTextStyle
```

Used to configure the text style for the time selector separator between the hour and minute controls.

If this is null, the time picker defaults to the overall theme's [TextTheme.displayLarge].

If this is null and [ThemeData.useMaterial3] is false, then defaults to the value of [hourMinuteTextStyle].

### copyWith()

```dart
TimePickerThemeData copyWith({Color? backgroundColor, ButtonStyle? cancelButtonStyle, ButtonStyle? confirmButtonStyle, ButtonStyle? dayPeriodButtonStyle, BorderSide? dayPeriodBorderSide, Color? dayPeriodColor, OutlinedBorder? dayPeriodShape, Color? dayPeriodTextColor, TextStyle? dayPeriodTextStyle, Color? dialBackgroundColor, Color? dialHandColor, Color? dialTextColor, TextStyle? dialTextStyle, double? elevation, Color? entryModeIconColor, TextStyle? helpTextStyle, Color? hourMinuteColor, ShapeBorder? hourMinuteShape, Color? hourMinuteTextColor, TextStyle? hourMinuteTextStyle, InputDecorationTheme? inputDecorationTheme, EdgeInsetsGeometry? padding, ShapeBorder? shape, WidgetStateProperty<Color?>? timeSelectorSeparatorColor, WidgetStateProperty<TextStyle?>? timeSelectorSeparatorTextStyle})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
TimePickerThemeData lerp(TimePickerThemeData? a, TimePickerThemeData? b, double t)
```

Linearly interpolate between two time picker themes.

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

# TimePickerTheme

```dart
class TimePickerTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for time pickers displayed using [showTimePicker] in this widget's subtree.

Values specified here are used for time picker properties that are not given an explicit non-null value.

### TimePickerTheme()

```dart
TimePickerTheme({dynamic key, required TimePickerThemeData data, required dynamic child})
```

Creates a time picker theme that controls the configurations for time pickers displayed in its widget subtree.

### data

```dart
TimePickerThemeData data
```

The properties for descendant time picker widgets.

### of()

```dart
TimePickerThemeData of(BuildContext context)
```

The [data] value of the closest [TimePickerTheme] ancestor.

If there is no ancestor, it returns [ThemeData.timePickerTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
TimePickerThemeData theme = TimePickerTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(TimePickerTheme oldWidget)
```
