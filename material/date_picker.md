@docImport 'dart:ui';

@docImport 'app.dart'; @docImport 'time_picker.dart';

# showDatePicker()

```dart
Future<DateTime?> showDatePicker({required BuildContext context, DateTime? initialDate, required DateTime firstDate, required DateTime lastDate, DateTime? currentDate, DatePickerEntryMode initialEntryMode = DatePickerEntryMode.calendar, SelectableDayPredicate? selectableDayPredicate, String? helpText, String? cancelText, String? confirmText, Locale? locale, bool barrierDismissible = true, Color? barrierColor, String? barrierLabel, bool useRootNavigator = true, RouteSettings? routeSettings, TextDirection? textDirection, TransitionBuilder? builder, DatePickerMode initialDatePickerMode = DatePickerMode.day, String? errorFormatText, String? errorInvalidText, String? fieldHintText, String? fieldLabelText, TextInputType? keyboardType, Offset? anchorPoint, ValueChanged<DatePickerEntryMode>? onDatePickerModeChange, Icon? switchToInputEntryModeIcon, Icon? switchToCalendarEntryModeIcon, CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

Shows a dialog containing a Material Design date picker.

The returned [Future] resolves to the date selected by the user when the user confirms the dialog. If the user cancels the dialog, null is returned.

When the date picker is first displayed, if [initialDate] is not null, it will show the month of [initialDate], with [initialDate] selected. Otherwise it will show the [currentDate]'s month.

The [firstDate] is the earliest allowable date. The [lastDate] is the latest allowable date. If [initialDate] is not null, it must either fall between these dates, or be equal to one of them. For each of these [DateTime] parameters, only their dates are considered. Their time fields are ignored. They must all be non-null.

The [currentDate] represents the current day (i.e. today). This date will be highlighted in the day grid. If null, the date of [DateTime.now] will be used.

An optional [initialEntryMode] argument can be used to display the date picker in the [DatePickerEntryMode.calendar] (a calendar month grid) or [DatePickerEntryMode.input] (a text input field) mode. It defaults to [DatePickerEntryMode.calendar].

{@template flutter.material.date_picker.switchToInputEntryModeIcon} An optional [switchToInputEntryModeIcon] argument can be used to display a custom Icon in the corner of the dialog when [DatePickerEntryMode] is [DatePickerEntryMode.calendar]. Clicking on icon changes the [DatePickerEntryMode] to [DatePickerEntryMode.input]. If null, `Icon(useMaterial3 ? Icons.edit_outlined : Icons.edit)` is used. {@endtemplate}

{@template flutter.material.date_picker.switchToCalendarEntryModeIcon} An optional [switchToCalendarEntryModeIcon] argument can be used to display a custom Icon in the corner of the dialog when [DatePickerEntryMode] is [DatePickerEntryMode.input]. Clicking on icon changes the [DatePickerEntryMode] to [DatePickerEntryMode.calendar]. If null, `Icon(Icons.calendar_today)` is used. {@endtemplate}

An optional [selectableDayPredicate] function can be passed in to only allow certain days for selection. If provided, only the days that [selectableDayPredicate] returns true for will be selectable. For example, this can be used to only allow weekdays for selection. If provided, it must return true for [initialDate].

{@macro flutter.material.calendar_date_picker.calendarDelegate}

The following optional string parameters allow you to override the default text used for various parts of the dialog:

- [helpText], label displayed at the top of the dialog.
- [cancelText], label on the cancel button.
- [confirmText], label on the ok button.
- [errorFormatText], message used when the input text isn't in a proper date format.
- [errorInvalidText], message used when the input text isn't a selectable date.
- [fieldHintText], text used to prompt the user when no text has been entered in the field.
- [fieldLabelText], label for the date text input field.

An optional [locale] argument can be used to set the locale for the date picker. It defaults to the ambient locale provided by [Localizations].

An optional [textDirection] argument can be used to set the text direction ([TextDirection.ltr] or [TextDirection.rtl]) for the date picker. It defaults to the ambient text direction provided by [Directionality]. If both [locale] and [textDirection] are non-null, [textDirection] overrides the direction chosen for the [locale].

The [context], [barrierDismissible], [barrierColor], [barrierLabel], [useRootNavigator] and [routeSettings] arguments are passed to [showDialog], the documentation for which discusses how it is used.

The [builder] parameter can be used to wrap the dialog widget to add inherited widgets like [Theme].

An optional [initialDatePickerMode] argument can be used to have the calendar date picker initially appear in the [DatePickerMode.year] or [DatePickerMode.day] mode. It defaults to [DatePickerMode.day].

{@macro flutter.widgets.RawDialogRoute}

{@tool dartpad} This sample demonstrates how to create a basic date picker. Tapping the button displays a date picker which returns the selected date.

** See code in examples/api/lib/material/date_picker/show_date_picker.1.dart ** {@end-tool}

### State Restoration

Using this method will not enable state restoration for the date picker. In order to enable state restoration for a date picker, use [Navigator.restorablePush] or [Navigator.restorablePushNamed] with [DatePickerDialog].

For more information about state restoration, see [RestorationManager].

{@macro flutter.widgets.RestorationManager}

{@tool dartpad} This sample demonstrates how to create a restorable Material date picker. This is accomplished by enabling state restoration by specifying [MaterialApp.restorationScopeId] and using [Navigator.restorablePush] to push [DatePickerDialog] when the button is tapped.

** See code in examples/api/lib/material/date_picker/show_date_picker.0.dart ** {@end-tool}

See also:

- [showDateRangePicker], which shows a Material Design date range picker used to select a range of dates.
- [CalendarDatePicker], which provides the calendar grid used by the date picker dialog.
- [InputDatePickerFormField], which provides a text input field for entering dates.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- [showTimePicker], which shows a dialog that contains a Material Design time picker.

# DatePickerDialog

```dart
class DatePickerDialog extends StatefulWidget {}
```

A Material-style date picker dialog.

It is used internally by [showDatePicker] or can be directly pushed onto the [Navigator] stack to enable state restoration. See [showDatePicker] for a state restoration app example.

See also:

- [showDatePicker], which is a way to display the date picker.

### DatePickerDialog()

```dart
DatePickerDialog({dynamic key, DateTime? initialDate, required DateTime firstDate, required DateTime lastDate, DateTime? currentDate, DatePickerEntryMode initialEntryMode = DatePickerEntryMode.calendar, SelectableDayPredicate? selectableDayPredicate, String? cancelText, String? confirmText, String? helpText, DatePickerMode initialCalendarMode = DatePickerMode.day, String? errorFormatText, String? errorInvalidText, String? fieldHintText, String? fieldLabelText, TextInputType? keyboardType, String? restorationId, ValueChanged<DatePickerEntryMode>? onDatePickerModeChange, Icon? switchToInputEntryModeIcon, Icon? switchToCalendarEntryModeIcon, EdgeInsets insetPadding = const EdgeInsets.symmetric(horizontal: 16.0, vertical: 24.0), CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

A Material-style date picker dialog.

### initialDate

```dart
DateTime? initialDate
```

The initially selected [DateTime] that the picker should display.

If this is null, there is no selected date. A date must be selected to submit the dialog.

### firstDate

```dart
DateTime firstDate
```

The earliest allowable [DateTime] that the user can select.

### lastDate

```dart
DateTime lastDate
```

The latest allowable [DateTime] that the user can select.

### currentDate

```dart
DateTime currentDate
```

The [DateTime] representing today. It will be highlighted in the day grid.

### initialEntryMode

```dart
DatePickerEntryMode initialEntryMode
```

The initial mode of date entry method for the date picker dialog.

See [DatePickerEntryMode] for more details on the different data entry modes available.

### selectableDayPredicate

```dart
SelectableDayPredicate? selectableDayPredicate
```

Function to provide full control over which [DateTime] can be selected.

### cancelText

```dart
String? cancelText
```

The text that is displayed on the cancel button.

### confirmText

```dart
String? confirmText
```

The text that is displayed on the confirm button.

### helpText

```dart
String? helpText
```

The text that is displayed at the top of the header.

This is used to indicate to the user what they are selecting a date for.

### initialCalendarMode

```dart
DatePickerMode initialCalendarMode
```

The initial display of the calendar picker.

### errorFormatText

```dart
String? errorFormatText
```

The error text displayed if the entered date is not in the correct format.

### errorInvalidText

```dart
String? errorInvalidText
```

The error text displayed if the date is not valid.

A date is not valid if it is earlier than [firstDate], later than [lastDate], or doesn't pass the [selectableDayPredicate].

### fieldHintText

```dart
String? fieldHintText
```

The hint text displayed in the [TextField].

If this is null, it will default to the date format string. For example, 'mm/dd/yyyy' for en_US.

### fieldLabelText

```dart
String? fieldLabelText
```

The label text displayed in the [TextField].

If this is null, it will default to the words representing the date format string. For example, 'Month, Day, Year' for en_US.

### keyboardType

```dart
TextInputType? keyboardType
```

{@template flutter.material.datePickerDialog} The keyboard type of the [TextField].

If this is null, it will default to [TextInputType.datetime] {@endtemplate}

### restorationId

```dart
String? restorationId
```

Restoration ID to save and restore the state of the [DatePickerDialog].

If it is non-null, the date picker will persist and restore the date selected on the dialog.

The state of this widget is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### onDatePickerModeChange

```dart
ValueChanged<DatePickerEntryMode>? onDatePickerModeChange
```

Called when the [DatePickerDialog] is toggled between [DatePickerEntryMode.calendar],[DatePickerEntryMode.input].

An example of how this callback might be used is an app that saves the user's preferred entry mode and uses it to initialize the `initialEntryMode` parameter the next time the date picker is shown.

### switchToInputEntryModeIcon

```dart
Icon? switchToInputEntryModeIcon
```

{@macro flutter.material.date_picker.switchToInputEntryModeIcon}

### switchToCalendarEntryModeIcon

```dart
Icon? switchToCalendarEntryModeIcon
```

{@macro flutter.material.date_picker.switchToCalendarEntryModeIcon}

### insetPadding

```dart
EdgeInsets insetPadding
```

The amount of padding added to [MediaQueryData.viewInsets] on the outside of the dialog. This defines the minimum space between the screen's edges and the dialog.

Defaults to `EdgeInsets.symmetric(horizontal: 16.0, vertical: 24.0)`.

### calendarDelegate

```dart
CalendarDelegate<DateTime> calendarDelegate
```

{@macro flutter.material.calendar_date_picker.calendarDelegate}

### createState()

```dart
State<DatePickerDialog> createState()
```

# SelectableDayForRangePredicate

```dart
typedef SelectableDayForRangePredicate = bool Function(DateTime day, DateTime? selectedStartDay, DateTime? selectedEndDay)
```

Signature for predicating enabled dates in date range pickers.

The [selectedStartDay] and [selectedEndDay] are the currently selected start and end dates of a date range, which conditionally enables or disables each date in the picker based on the user selection. (Example: in a hostel's room selection, you are not able to select the end date after the next non-selectable day).

See [showDateRangePicker], which has a [SelectableDayForRangePredicate] parameter used to specify allowable days in the date range picker.

# showDateRangePicker()

```dart
Future<DateTimeRange?> showDateRangePicker({required BuildContext context, DateTimeRange? initialDateRange, required DateTime firstDate, required DateTime lastDate, DateTime? currentDate, DatePickerEntryMode initialEntryMode = DatePickerEntryMode.calendar, String? helpText, String? cancelText, String? confirmText, String? saveText, String? errorFormatText, String? errorInvalidText, String? errorInvalidRangeText, String? fieldStartHintText, String? fieldEndHintText, String? fieldStartLabelText, String? fieldEndLabelText, Locale? locale, bool barrierDismissible = true, Color? barrierColor, String? barrierLabel, bool useRootNavigator = true, RouteSettings? routeSettings, TextDirection? textDirection, TransitionBuilder? builder, Offset? anchorPoint, TextInputType keyboardType = TextInputType.datetime, Icon? switchToInputEntryModeIcon, Icon? switchToCalendarEntryModeIcon, SelectableDayForRangePredicate? selectableDayPredicate, CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

Shows a full screen modal dialog containing a Material Design date range picker.

The returned [Future] resolves to the [DateTimeRange] selected by the user when the user saves their selection. If the user cancels the dialog, null is returned.

If [initialDateRange] is non-null, then it will be used as the initially selected date range. If it is provided, `initialDateRange.start` must be before or on `initialDateRange.end`.

The [firstDate] is the earliest allowable date. The [lastDate] is the latest allowable date.

If an initial date range is provided, `initialDateRange.start` and `initialDateRange.end` must both fall between or on [firstDate] and [lastDate]. For all of these [DateTime] values, only their dates are considered. Their time fields are ignored.

The [currentDate] represents the current day (i.e. today). This date will be highlighted in the day grid. If null, the date of `DateTime.now()` will be used.

An optional [initialEntryMode] argument can be used to display the date picker in the [DatePickerEntryMode.calendar] (a scrollable calendar month grid) or [DatePickerEntryMode.input] (two text input fields) mode. It defaults to [DatePickerEntryMode.calendar].

{@macro flutter.material.date_picker.switchToInputEntryModeIcon}

{@macro flutter.material.date_picker.switchToCalendarEntryModeIcon}

{@macro flutter.material.calendar_date_picker.calendarDelegate}

The following optional string parameters allow you to override the default text used for various parts of the dialog:

- [helpText], the label displayed at the top of the dialog.
- [cancelText], the label on the cancel button for the text input mode.
- [confirmText],the label on the ok button for the text input mode.
- [saveText], the label on the save button for the fullscreen calendar mode.
- [errorFormatText], the message used when an input text isn't in a proper date format.
- [errorInvalidText], the message used when an input text isn't a selectable date.
- [errorInvalidRangeText], the message used when the date range is invalid (e.g. start date is after end date).
- [fieldStartHintText], the text used to prompt the user when no text has been entered in the start field.
- [fieldEndHintText], the text used to prompt the user when no text has been entered in the end field.
- [fieldStartLabelText], the label for the start date text input field.
- [fieldEndLabelText], the label for the end date text input field.

An optional [locale] argument can be used to set the locale for the date picker. It defaults to the ambient locale provided by [Localizations].

An optional [textDirection] argument can be used to set the text direction ([TextDirection.ltr] or [TextDirection.rtl]) for the date picker. It defaults to the ambient text direction provided by [Directionality]. If both [locale] and [textDirection] are non-null, [textDirection] overrides the direction chosen for the [locale].

The [context], [barrierDismissible], [barrierColor], [barrierLabel], [useRootNavigator] and [routeSettings] arguments are passed to [showDialog], the documentation for which discusses how it is used.

The [builder] parameter can be used to wrap the dialog widget to add inherited widgets like [Theme].

{@macro flutter.widgets.RawDialogRoute}

### State Restoration

Using this method will not enable state restoration for the date range picker. In order to enable state restoration for a date range picker, use [Navigator.restorablePush] or [Navigator.restorablePushNamed] with [DateRangePickerDialog].

For more information about state restoration, see [RestorationManager].

{@macro flutter.widgets.RestorationManager}

{@tool dartpad} This sample demonstrates how to create a restorable Material date range picker. This is accomplished by enabling state restoration by specifying [MaterialApp.restorationScopeId] and using [Navigator.restorablePush] to push [DateRangePickerDialog] when the button is tapped.

** See code in examples/api/lib/material/date_picker/show_date_range_picker.0.dart ** {@end-tool}

See also:

- [showDatePicker], which shows a Material Design date picker used to select a single date.
- [DateTimeRange], which is used to describe a date range.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.

# DateRangePickerDialog

```dart
class DateRangePickerDialog extends StatefulWidget {}
```

A Material-style date range picker dialog.

It is used internally by [showDateRangePicker] or can be directly pushed onto the [Navigator] stack to enable state restoration. See [showDateRangePicker] for a state restoration app example.

See also:

- [showDateRangePicker], which is a way to display the date picker.

### DateRangePickerDialog()

```dart
DateRangePickerDialog({dynamic key, DateTimeRange? initialDateRange, required DateTime firstDate, required DateTime lastDate, DateTime? currentDate, DatePickerEntryMode initialEntryMode = DatePickerEntryMode.calendar, String? helpText, String? cancelText, String? confirmText, String? saveText, String? errorInvalidRangeText, String? errorFormatText, String? errorInvalidText, String? fieldStartHintText, String? fieldEndHintText, String? fieldStartLabelText, String? fieldEndLabelText, TextInputType keyboardType = TextInputType.datetime, String? restorationId, Icon? switchToInputEntryModeIcon, Icon? switchToCalendarEntryModeIcon, SelectableDayForRangePredicate? selectableDayPredicate, CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

A Material-style date range picker dialog.

### initialDateRange

```dart
DateTimeRange? initialDateRange
```

The date range that the date range picker starts with when it opens.

If an initial date range is provided, `initialDateRange.start` and `initialDateRange.end` must both fall between or on [firstDate] and [lastDate]. For all of these [DateTime] values, only their dates are considered. Their time fields are ignored.

If [initialDateRange] is non-null, then it will be used as the initially selected date range. If it is provided, `initialDateRange.start` must be before or on `initialDateRange.end`.

### firstDate

```dart
DateTime firstDate
```

The earliest allowable date on the date range.

### lastDate

```dart
DateTime lastDate
```

The latest allowable date on the date range.

### currentDate

```dart
DateTime get currentDate
```

The [currentDate] represents the current day (i.e. today).

This date will be highlighted in the day grid.

If `null`, the date of `calendarDelegate.now()` will be used.

### initialEntryMode

```dart
DatePickerEntryMode initialEntryMode
```

The initial date range picker entry mode.

The date range has two main modes: [DatePickerEntryMode.calendar] (a scrollable calendar month grid) or [DatePickerEntryMode.input] (two text input fields) mode.

It defaults to [DatePickerEntryMode.calendar].

### cancelText

```dart
String? cancelText
```

The label on the cancel button for the text input mode.

If null, the localized value of [MaterialLocalizations.cancelButtonLabel] is used.

### confirmText

```dart
String? confirmText
```

The label on the "OK" button for the text input mode.

If null, the localized value of [MaterialLocalizations.okButtonLabel] is used.

### saveText

```dart
String? saveText
```

The label on the save button for the fullscreen calendar mode.

If null, the localized value of [MaterialLocalizations.saveButtonLabel] is used.

### helpText

```dart
String? helpText
```

The label displayed at the top of the dialog.

If null, the localized value of [MaterialLocalizations.dateRangePickerHelpText] is used.

### errorInvalidRangeText

```dart
String? errorInvalidRangeText
```

The message used when the date range is invalid (e.g. start date is after end date).

If null, the localized value of [MaterialLocalizations.invalidDateRangeLabel] is used.

### errorFormatText

```dart
String? errorFormatText
```

The message used when an input text isn't in a proper date format.

If null, the localized value of [MaterialLocalizations.invalidDateFormatLabel] is used.

### errorInvalidText

```dart
String? errorInvalidText
```

The message used when an input text isn't a selectable date.

If null, the localized value of [MaterialLocalizations.dateOutOfRangeLabel] is used.

### fieldStartHintText

```dart
String? fieldStartHintText
```

The text used to prompt the user when no text has been entered in the start field.

If null, the localized value of [MaterialLocalizations.dateHelpText] is used.

### fieldEndHintText

```dart
String? fieldEndHintText
```

The text used to prompt the user when no text has been entered in the end field.

If null, the localized value of [MaterialLocalizations.dateHelpText] is used.

### fieldStartLabelText

```dart
String? fieldStartLabelText
```

The label for the start date text input field.

If null, the localized value of [MaterialLocalizations.dateRangeStartLabel] is used.

### fieldEndLabelText

```dart
String? fieldEndLabelText
```

The label for the end date text input field.

If null, the localized value of [MaterialLocalizations.dateRangeEndLabel] is used.

### keyboardType

```dart
TextInputType keyboardType
```

{@macro flutter.material.datePickerDialog}

### restorationId

```dart
String? restorationId
```

Restoration ID to save and restore the state of the [DateRangePickerDialog].

If it is non-null, the date range picker will persist and restore the date range selected on the dialog.

The state of this widget is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### switchToInputEntryModeIcon

```dart
Icon? switchToInputEntryModeIcon
```

{@macro flutter.material.date_picker.switchToInputEntryModeIcon}

### switchToCalendarEntryModeIcon

```dart
Icon? switchToCalendarEntryModeIcon
```

{@macro flutter.material.date_picker.switchToCalendarEntryModeIcon}

### selectableDayPredicate

```dart
SelectableDayForRangePredicate? selectableDayPredicate
```

Function to provide full control over which [DateTime] can be selected.

### calendarDelegate

```dart
CalendarDelegate<DateTime> calendarDelegate
```

{@macro flutter.material.calendar_date_picker.calendarDelegate}

### createState()

```dart
State<DateRangePickerDialog> createState()
```
