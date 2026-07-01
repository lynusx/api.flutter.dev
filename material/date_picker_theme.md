@docImport 'calendar_date_picker.dart'; @docImport 'date_picker.dart'; @docImport 'dialog.dart'; @docImport 'input_date_picker_form_field.dart'; @docImport 'material.dart'; @docImport 'scaffold.dart';

# DatePickerThemeData

```dart
class DatePickerThemeData with Diagnosticable {}
```

Overrides the default values of visual properties for descendant [DatePickerDialog] widgets.

Descendant widgets obtain the current [DatePickerThemeData] object with [DatePickerTheme.of]. Instances of [DatePickerThemeData] can be customized with [DatePickerThemeData.copyWith].

Typically a [DatePickerTheme] is specified as part of the overall [Theme] with [ThemeData.datePickerTheme].

All [DatePickerThemeData] properties are null by default. When null, the [DatePickerDialog] computes its own default values, typically based on the overall theme's [ThemeData.colorScheme], [ThemeData.textTheme], and [ThemeData.iconTheme].

### DatePickerThemeData()

```dart
DatePickerThemeData({Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, Color? headerBackgroundColor, Color? headerForegroundColor, TextStyle? headerHeadlineStyle, TextStyle? headerHelpStyle, TextStyle? weekdayStyle, TextStyle? dayStyle, WidgetStateProperty<Color?>? dayForegroundColor, WidgetStateProperty<Color?>? dayBackgroundColor, WidgetStateProperty<Color?>? dayOverlayColor, WidgetStateProperty<OutlinedBorder?>? dayShape, WidgetStateProperty<Color?>? todayForegroundColor, WidgetStateProperty<Color?>? todayBackgroundColor, BorderSide? todayBorder, TextStyle? yearStyle, WidgetStateProperty<Color?>? yearForegroundColor, WidgetStateProperty<Color?>? yearBackgroundColor, WidgetStateProperty<Color?>? yearOverlayColor, WidgetStateProperty<OutlinedBorder?>? yearShape, Color? rangePickerBackgroundColor, double? rangePickerElevation, Color? rangePickerShadowColor, Color? rangePickerSurfaceTintColor, ShapeBorder? rangePickerShape, Color? rangePickerHeaderBackgroundColor, Color? rangePickerHeaderForegroundColor, TextStyle? rangePickerHeaderHeadlineStyle, TextStyle? rangePickerHeaderHelpStyle, Color? rangeSelectionBackgroundColor, WidgetStateProperty<Color?>? rangeSelectionOverlayColor, Color? dividerColor, Object? inputDecorationTheme, ButtonStyle? cancelButtonStyle, ButtonStyle? confirmButtonStyle, Locale? locale, TextStyle? toggleButtonTextStyle, Color? subHeaderForegroundColor})
```

Creates a [DatePickerThemeData] that can be used to override default properties in a [DatePickerTheme] widget.

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of [Dialog.backgroundColor].

### elevation

```dart
double? elevation
```

Overrides the default value of [Dialog.elevation].

See also: [Material.elevation], which explains how elevation is related to a component's shadow.

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value of [Dialog.shadowColor].

See also: [Material.shadowColor], which explains how the shadow is rendered.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value of [Dialog.surfaceTintColor].

See also: [Material.surfaceTintColor], which explains how this color is related to [elevation] and [backgroundColor].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value of [Dialog.shape].

If [elevation] is greater than zero then a shadow is shown and the shadow's shape mirrors the shape of the dialog.

### headerBackgroundColor

```dart
Color? headerBackgroundColor
```

Overrides the header's default background fill color.

The dialog's header displays the currently selected date.

### headerForegroundColor

```dart
Color? headerForegroundColor
```

Overrides the header's default color used for text labels and icons.

The dialog's header displays the currently selected date.

This is used instead of the [TextStyle.color] property of [headerHeadlineStyle] and [headerHelpStyle].

### headerHeadlineStyle

```dart
TextStyle? headerHeadlineStyle
```

Overrides the header's default headline text style.

The dialog's header displays the currently selected date.

The [TextStyle.color] of the [headerHeadlineStyle] is not used, [headerForegroundColor] is used instead.

### headerHelpStyle

```dart
TextStyle? headerHelpStyle
```

Overrides the header's default help text style.

The help text (also referred to as "supporting text" in the Material spec) is usually a prompt to the user at the top of the header (i.e. 'Select date').

The [TextStyle.color] of the [headerHelpStyle] is not used, [headerForegroundColor] is used instead.

See also: [DatePickerDialog.helpText], which specifies the help text.

### weekdayStyle

```dart
TextStyle? weekdayStyle
```

Overrides the default text style used for the row of weekday labels at the top of the date picker grid.

### dayStyle

```dart
TextStyle? dayStyle
```

Overrides the default text style used for each individual day label in the grid of the date picker.

The [TextStyle.color] of the [dayStyle] is not used, [dayForegroundColor] is used instead.

### dayForegroundColor

```dart
WidgetStateProperty<Color?>? dayForegroundColor
```

Overrides the default color used to paint the day labels in the grid of the date picker.

This will be used instead of the color provided in [dayStyle].

This supports different colors based on the [WidgetState]s of the day button, such as `WidgetState.selected`, `WidgetState.hovered`, `WidgetState.focused`, and `WidgetState.disabled`.

```dart
dayBackgroundColor: WidgetStateProperty.resolveWith((Set<WidgetState> states) {
  if (states.contains(WidgetState.selected)) {
    return Theme.of(context).colorScheme.primary;
  }
  return null; // Use the default color.
})
```

See also:

- [dayOverlayColor] which applies an overlay over the day labels depending on the [WidgetState].

### dayBackgroundColor

```dart
WidgetStateProperty<Color?>? dayBackgroundColor
```

Overrides the default color used to paint the background of the day labels in the grid of the date picker.

This supports different colors based on the [WidgetState]s of the day button, such as `WidgetState.selected`, `WidgetState.hovered`, `WidgetState.focused`, and `WidgetState.disabled`.

```dart
dayBackgroundColor: WidgetStateProperty.resolveWith((Set<WidgetState> states) {
  if (states.contains(WidgetState.selected)) {
    return Theme.of(context).colorScheme.primary;
  }
  return null; // Use the default color.
})
```

See also:

- [dayOverlayColor] which applies an overlay over the day labels depending on the [WidgetState].

### dayOverlayColor

```dart
WidgetStateProperty<Color?>? dayOverlayColor
```

Overrides the default highlight color that's typically used to indicate that a day in the grid is focused, hovered, or pressed.

This supports different colors based on the [WidgetState]s of the day button. The overlay color is usually used with an opacity to create hover, focus, and press effects.

```dart
dayOverlayColor: WidgetStateProperty.resolveWith((Set<WidgetState> states) {
  if (states.contains(WidgetState.pressed)) {
    return Colors.blue.withValues(alpha: 0.12);
  }
  if (states.contains(WidgetState.hovered)) {
    return Colors.blue.withValues(alpha: 0.08);
  }
  if (states.contains(WidgetState.focused)) {
    return Colors.blue.withValues(alpha: 0.12);
  }
  return null; // Use the default color.
})
```

### dayShape

```dart
WidgetStateProperty<OutlinedBorder?>? dayShape
```

Overrides the default shape used to paint the shape decoration of the day labels in the grid of the date picker.

If the selected day is the current day, the provided shape with the value of [todayBackgroundColor] is used to paint the shape decoration of the day label and the value of [todayBorder] and [todayForegroundColor] is used to paint the border.

If the selected day is not the current day, the provided shape with the value of [dayBackgroundColor] is used to paint the shape decoration of the day label.

{@tool dartpad} This sample demonstrates how to customize the day selector shape decoration using the [dayShape], [todayForegroundColor], [todayBackgroundColor], and [todayBorder] properties.

** See code in examples/api/lib/material/date_picker/date_picker_theme_day_shape.0.dart ** {@end-tool}

### todayForegroundColor

```dart
WidgetStateProperty<Color?>? todayForegroundColor
```

Overrides the default color used to paint the [DatePickerDialog.currentDate] label in the grid of the dialog's [CalendarDatePicker] and the corresponding year in the dialog's [YearPicker].

This will be used instead of the [TextStyle.color] provided in [dayStyle].

{@tool dartpad} This sample demonstrates how to customize the day selector shape decoration using the [dayShape], [todayForegroundColor], [todayBackgroundColor], and [todayBorder] properties.

** See code in examples/api/lib/material/date_picker/date_picker_theme_day_shape.0.dart ** {@end-tool}

### todayBackgroundColor

```dart
WidgetStateProperty<Color?>? todayBackgroundColor
```

Overrides the default color used to paint the background of the [DatePickerDialog.currentDate] label in the grid of the date picker.

### todayBorder

```dart
BorderSide? todayBorder
```

Overrides the border used to paint the [DatePickerDialog.currentDate] label in the grid of the date picker.

If the border side's [BorderSide.color] is transparent (has 0 opacity), [todayForegroundColor] is used instead. Otherwise, the border's color is used as specified. To omit the border entirely, set [todayBorder] to [BorderSide.none].

{@tool dartpad} This sample demonstrates how to customize the day selector shape decoration using the [dayShape], [todayForegroundColor], [todayBackgroundColor], and [todayBorder] properties.

** See code in examples/api/lib/material/date_picker/date_picker_theme_day_shape.0.dart ** {@end-tool}

### yearStyle

```dart
TextStyle? yearStyle
```

Overrides the default text style used to paint each of the year entries in the year selector of the date picker.

The [TextStyle.color] of the [yearStyle] is not used, [yearForegroundColor] is used instead.

### yearForegroundColor

```dart
WidgetStateProperty<Color?>? yearForegroundColor
```

Overrides the default color used to paint the year labels in the year selector of the date picker.

This will be used instead of the color provided in [yearStyle].

### yearBackgroundColor

```dart
WidgetStateProperty<Color?>? yearBackgroundColor
```

Overrides the default color used to paint the background of the year labels in the year selector of the of the date picker.

### yearOverlayColor

```dart
WidgetStateProperty<Color?>? yearOverlayColor
```

Overrides the default highlight color that's typically used to indicate that a year in the year selector is focused, hovered, or pressed.

### yearShape

```dart
WidgetStateProperty<OutlinedBorder?>? yearShape
```

Overrides the default shape used to paint the shape decoration of the year labels in the list of the year picker.

If the selected year is the current year, the provided shape with the value of [todayBackgroundColor] is used to paint the shape decoration of the year label and the value of [todayBorder] and [todayForegroundColor] is used to paint the border.

If the selected year is not the current year, the provided shape with the value of [yearBackgroundColor] is used to paint the shape decoration of the year label.

### rangePickerBackgroundColor

```dart
Color? rangePickerBackgroundColor
```

Overrides the default [Scaffold.backgroundColor] for [DateRangePickerDialog].

### rangePickerElevation

```dart
double? rangePickerElevation
```

Overrides the default elevation of the full screen [DateRangePickerDialog].

See also: [Material.elevation], which explains how elevation is related to a component's shadow.

### rangePickerShadowColor

```dart
Color? rangePickerShadowColor
```

Overrides the color of the shadow painted below a full screen [DateRangePickerDialog].

See also: [Material.shadowColor], which explains how the shadow is rendered.

### rangePickerSurfaceTintColor

```dart
Color? rangePickerSurfaceTintColor
```

Overrides the default color of the surface tint overlay applied to the [backgroundColor] of a full screen [DateRangePickerDialog]'s to indicate elevation.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

See also: [Material.surfaceTintColor], which explains how this color is related to [elevation].

### rangePickerShape

```dart
ShapeBorder? rangePickerShape
```

Overrides the default overall shape of a full screen [DateRangePickerDialog].

If [elevation] is greater than zero then a shadow is shown and the shadow's shape mirrors the shape of the dialog.

[Material.surfaceTintColor], which explains how this color is related to [elevation].

### rangePickerHeaderBackgroundColor

```dart
Color? rangePickerHeaderBackgroundColor
```

Overrides the default background fill color for [DateRangePickerDialog].

The dialog's header displays the currently selected date range.

### rangePickerHeaderForegroundColor

```dart
Color? rangePickerHeaderForegroundColor
```

Overrides the default color used for text labels and icons in the header of a full screen [DateRangePickerDialog]

The dialog's header displays the currently selected date range.

This is used instead of any colors provided by [rangePickerHeaderHeadlineStyle] or [rangePickerHeaderHelpStyle].

### rangePickerHeaderHeadlineStyle

```dart
TextStyle? rangePickerHeaderHeadlineStyle
```

Overrides the default text style used for the headline text in the header of a full screen [DateRangePickerDialog].

The dialog's header displays the currently selected date range.

The [TextStyle.color] of [rangePickerHeaderHeadlineStyle] is not used, [rangePickerHeaderForegroundColor] is used instead.

### rangePickerHeaderHelpStyle

```dart
TextStyle? rangePickerHeaderHelpStyle
```

Overrides the default text style used for the help text of the header of a full screen [DateRangePickerDialog].

The help text (also referred to as "supporting text" in the Material spec) is usually a prompt to the user at the top of the header (i.e. 'Select date').

The [TextStyle.color] of the [rangePickerHeaderHelpStyle] is not used, [rangePickerHeaderForegroundColor] is used instead.

See also: [DateRangePickerDialog.helpText], which specifies the help text.

### rangeSelectionBackgroundColor

```dart
Color? rangeSelectionBackgroundColor
```

Overrides the default background color used to paint days selected between the start and end dates in a [DateRangePickerDialog].

### rangeSelectionOverlayColor

```dart
WidgetStateProperty<Color?>? rangeSelectionOverlayColor
```

Overrides the default highlight color that's typically used to indicate that a date in the selected range of a [DateRangePickerDialog] is focused, hovered, or pressed.

### dividerColor

```dart
Color? dividerColor
```

Overrides the default color used to paint the horizontal divider below the header text when dialog is in portrait orientation and vertical divider when the dialog is in landscape orientation.

### inputDecorationTheme

```dart
InputDecorationThemeData? get inputDecorationTheme
```

Overrides the [InputDatePickerFormField]'s input decoration theme. If this is null, [ThemeData.inputDecorationTheme] is used instead.

### cancelButtonStyle

```dart
ButtonStyle? cancelButtonStyle
```

Overrides the default style of the cancel button of a [DatePickerDialog].

### confirmButtonStyle

```dart
ButtonStyle? confirmButtonStyle
```

Overrides the default style of the confirm (OK) button of a [DatePickerDialog].

### locale

```dart
Locale? locale
```

An optional [locale] argument can be used to set the locale for the date picker. It defaults to the ambient locale provided by [Localizations].

### toggleButtonTextStyle

```dart
TextStyle? toggleButtonTextStyle
```

Overrides the default text style used for the text of toggle mode button.

If no [TextStyle.color] is given, [subHeaderForegroundColor] will be used.

### subHeaderForegroundColor

```dart
Color? subHeaderForegroundColor
```

Overrides the default color used for text labels and icons of sub header foreground.

This is used in [TextStyle.color] property of [toggleButtonTextStyle] if no color is given.

### copyWith()

```dart
DatePickerThemeData copyWith({Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, Color? headerBackgroundColor, Color? headerForegroundColor, TextStyle? headerHeadlineStyle, TextStyle? headerHelpStyle, TextStyle? weekdayStyle, TextStyle? dayStyle, WidgetStateProperty<Color?>? dayForegroundColor, WidgetStateProperty<Color?>? dayBackgroundColor, WidgetStateProperty<Color?>? dayOverlayColor, WidgetStateProperty<OutlinedBorder?>? dayShape, WidgetStateProperty<Color?>? todayForegroundColor, WidgetStateProperty<Color?>? todayBackgroundColor, BorderSide? todayBorder, TextStyle? yearStyle, WidgetStateProperty<Color?>? yearForegroundColor, WidgetStateProperty<Color?>? yearBackgroundColor, WidgetStateProperty<Color?>? yearOverlayColor, WidgetStateProperty<OutlinedBorder?>? yearShape, Color? rangePickerBackgroundColor, double? rangePickerElevation, Color? rangePickerShadowColor, Color? rangePickerSurfaceTintColor, ShapeBorder? rangePickerShape, Color? rangePickerHeaderBackgroundColor, Color? rangePickerHeaderForegroundColor, TextStyle? rangePickerHeaderHeadlineStyle, TextStyle? rangePickerHeaderHelpStyle, Color? rangeSelectionBackgroundColor, WidgetStateProperty<Color?>? rangeSelectionOverlayColor, Color? dividerColor, InputDecorationTheme? inputDecorationTheme, ButtonStyle? cancelButtonStyle, ButtonStyle? confirmButtonStyle, Locale? locale, TextStyle? toggleButtonTextStyle, Color? subHeaderForegroundColor})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
DatePickerThemeData lerp(DatePickerThemeData? a, DatePickerThemeData? b, double t)
```

Linearly interpolates between two [DatePickerThemeData].

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

# DatePickerTheme

```dart
class DatePickerTheme extends InheritedTheme {}
```

An inherited widget that defines the visual properties for [DatePickerDialog]s in this widget's subtree.

Values specified here are used for [DatePickerDialog] properties that are not given an explicit non-null value.

### DatePickerTheme()

```dart
DatePickerTheme({dynamic key, required DatePickerThemeData data, required dynamic child})
```

Creates a [DatePickerTheme] that controls visual parameters for descendent [DatePickerDialog]s.

### data

```dart
DatePickerThemeData data
```

Specifies the visual properties used by descendant [DatePickerDialog] widgets.

### of()

```dart
DatePickerThemeData of(BuildContext context)
```

The [data] from the closest instance of this class that encloses the given context.

If there is no [DatePickerTheme] in scope, this will return [ThemeData.datePickerTheme] from the ambient [Theme].

Typical usage is as follows:

```dart
DatePickerThemeData theme = DatePickerTheme.of(context);
```

See also:

- [maybeOf], which returns null if it doesn't find a [DatePickerTheme] ancestor.
- [defaults], which will return the default properties used when no other [DatePickerTheme] has been provided.

### maybeOf()

```dart
DatePickerThemeData? maybeOf(BuildContext context)
```

The data from the closest instance of this class that encloses the given context, if any.

Use this function if you want to allow situations where no [DatePickerTheme] is in scope. Prefer using [DatePickerTheme.of] in situations where a [DatePickerThemeData] is expected to be non-null.

If there is no [DatePickerTheme] in scope, then this function will return null.

Typical usage is as follows:

```dart
DatePickerThemeData? theme = DatePickerTheme.maybeOf(context);
if (theme == null) {
  // Do something else instead.
}
```

See also:

- [of], which will return the data from [ThemeData.datePickerTheme] if it doesn't find a [DatePickerTheme] ancestor, instead of returning null.
- [defaults], which will return the default properties used when no other [DatePickerTheme] has been provided.

### defaults()

```dart
DatePickerThemeData defaults(BuildContext context)
```

A DatePickerThemeData used as the default properties for date pickers.

This is only used for properties not already specified in the ambient [DatePickerTheme.of].

See also:

- [of], which will return the data from [ThemeData.datePickerTheme] if it doesn't find a [DatePickerTheme] ancestor, instead of returning null.
- [maybeOf], which returns null if it doesn't find a [DatePickerTheme] ancestor.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DatePickerTheme oldWidget)
```
