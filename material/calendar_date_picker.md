@docImport 'date_picker.dart'; @docImport 'time_picker.dart';

# CalendarDatePicker

```dart
class CalendarDatePicker extends StatefulWidget {}
```

Displays a grid of days for a given month and allows the user to select a date.

Days are arranged in a rectangular grid with one column for each day of the week. Controls are provided to change the year and month that the grid is showing.

The calendar picker widget is rarely used directly. Instead, consider using [showDatePicker], which will create a dialog that uses this as well as provides a text entry option.

See also:

- [showDatePicker], which creates a Dialog that contains a [CalendarDatePicker] and provides an optional compact view where the user can enter a date as a line of text.
- [showTimePicker], which shows a dialog that contains a Material Design time picker.

### CalendarDatePicker()

```dart
CalendarDatePicker({dynamic key, required DateTime? initialDate, required DateTime firstDate, required DateTime lastDate, DateTime? currentDate, required ValueChanged<DateTime> onDateChanged, ValueChanged<DateTime>? onDisplayedMonthChanged, DatePickerMode initialCalendarMode = DatePickerMode.day, SelectableDayPredicate? selectableDayPredicate, CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

Creates a calendar date picker.

It will display a grid of days for the [initialDate]'s month, or, if that is null, the [currentDate]'s month. The day indicated by [initialDate] will be selected if it is not null.

The optional [onDisplayedMonthChanged] callback can be used to track the currently displayed month.

The user interface provides a way to change the year of the month being displayed. By default it will show the day grid, but this can be changed to start in the year selection interface with [initialCalendarMode] set to [DatePickerMode.year].

The [lastDate] must be after or equal to [firstDate].

The [initialDate], if provided, must be between [firstDate] and [lastDate] or equal to one of them.

The [currentDate] represents the current day (i.e. today). This date will be highlighted in the day grid. If null, the date of `DateTime.now()` will be used.

If [selectableDayPredicate] and [initialDate] are both non-null, [selectableDayPredicate] must return `true` for the [initialDate].

{@template flutter.material.calendar_date_picker.calendarDelegate} The [calendarDelegate] controls date interpretation, formatting, and navigation within the picker. By providing a custom implementation, you can support alternative calendar systems such as Nepali, Hijri, Buddhist, and more. Defaults to [GregorianCalendarDelegate]. {@endtemplate}

### initialDate

```dart
DateTime? initialDate
```

The initially selected [DateTime] that the picker should display.

Subsequently changing this has no effect. To change the selected date, change the [key] to create a new instance of the [CalendarDatePicker], and provide that widget the new [initialDate]. This will reset the widget's interactive state.

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

### onDateChanged

```dart
ValueChanged<DateTime> onDateChanged
```

Called when the user selects a date in the picker.

### onDisplayedMonthChanged

```dart
ValueChanged<DateTime>? onDisplayedMonthChanged
```

Called when the user navigates to a new month/year in the picker.

### initialCalendarMode

```dart
DatePickerMode initialCalendarMode
```

The initial display of the calendar picker.

Subsequently changing this has no effect. To change the calendar mode, change the [key] to create a new instance of the [CalendarDatePicker], and provide that widget a new [initialCalendarMode]. This will reset the widget's interactive state.

### selectableDayPredicate

```dart
SelectableDayPredicate? selectableDayPredicate
```

Function to provide full control over which dates in the calendar can be selected.

### calendarDelegate

```dart
CalendarDelegate<DateTime> calendarDelegate
```

{@macro flutter.material.calendar_date_picker.calendarDelegate}

### createState()

```dart
State<CalendarDatePicker> createState()
```

# YearPicker

```dart
class YearPicker extends StatefulWidget {}
```

A scrollable grid of years to allow picking a year.

The year picker widget is rarely used directly. Instead, consider using [CalendarDatePicker], or [showDatePicker] which create full date pickers.

See also:

- [CalendarDatePicker], which provides a Material Design date picker interface.

- [showDatePicker], which shows a dialog containing a Material Design date picker.

### YearPicker()

```dart
YearPicker({dynamic key, DateTime? currentDate, required DateTime firstDate, required DateTime lastDate, DateTime? initialDate, required DateTime? selectedDate, required ValueChanged<DateTime> onChanged, DragStartBehavior dragStartBehavior = DragStartBehavior.start, CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

Creates a year picker.

The [lastDate] must be after the [firstDate].

### currentDate

```dart
DateTime currentDate
```

The current date.

This date is subtly highlighted in the picker.

### firstDate

```dart
DateTime firstDate
```

The earliest date the user is permitted to pick.

### lastDate

```dart
DateTime lastDate
```

The latest date the user is permitted to pick.

### selectedDate

```dart
DateTime? selectedDate
```

The currently selected date.

This date is highlighted in the picker.

### onChanged

```dart
ValueChanged<DateTime> onChanged
```

Called when the user picks a year.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### calendarDelegate

```dart
CalendarDelegate<DateTime> calendarDelegate
```

{@macro flutter.material.calendar_date_picker.calendarDelegate}

### createState()

```dart
State<YearPicker> createState()
```
