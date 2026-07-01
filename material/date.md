@docImport 'calendar_date_picker.dart'; @docImport 'date_picker.dart'; @docImport 'text_field.dart';

# CalendarDelegate

```dart
abstract class CalendarDelegate<T extends DateTime> {}
```

Controls the calendar system used in the date picker.

A [CalendarDelegate] defines how dates are interpreted, formatted, and navigated within the picker. Different calendar systems (e.g., Gregorian, Nepali, Hijri, Buddhist) can be supported by providing custom implementations.

{@tool dartpad} This example demonstrates how a [CalendarDelegate] is used to implement a custom calendar system in the date picker.

** See code in examples/api/lib/material/date_picker/custom_calendar_date_picker.0.dart ** {@end-tool}

See also:

- [GregorianCalendarDelegate], the default implementation for the Gregorian calendar.
- [CalendarDatePicker], which uses this delegate to manage calendar-specific behavior.

### CalendarDelegate()

```dart
CalendarDelegate()
```

Creates a calendar delegate.

### now()

```dart
T now()
```

Returns a [DateTime] representing the current date and time.

### dateOnly()

```dart
T dateOnly(T date)
```

{@macro flutter.material.date.dateOnly}

### datesOnly()

```dart
DateTimeRange<T> datesOnly(DateTimeRange<T> range)
```

{@macro flutter.material.date.datesOnly}

### isSameDay()

```dart
bool isSameDay(T? dateA, T? dateB)
```

{@macro flutter.material.date.isSameDay}

### isSameMonth()

```dart
bool isSameMonth(T? dateA, T? dateB)
```

{@macro flutter.material.date.isSameMonth}

### monthDelta()

```dart
int monthDelta(T startDate, T endDate)
```

{@macro flutter.material.date.monthDelta}

### addMonthsToMonthDate()

```dart
T addMonthsToMonthDate(T monthDate, int monthsToAdd)
```

{@macro flutter.material.date.addMonthsToMonthDate}

### addDaysToDate()

```dart
T addDaysToDate(T date, int days)
```

{@macro flutter.material.date.addDaysToDate}

### firstDayOffset()

```dart
int firstDayOffset(int year, int month, MaterialLocalizations localizations)
```

{@macro flutter.material.date.firstDayOffset}

### getDaysInMonth()

```dart
int getDaysInMonth(int year, int month)
```

Returns the number of days in a month, according to the calendar system.

### getMonth()

```dart
T getMonth(int year, int month)
```

Returns a [DateTime] with the given [year] and [month].

### getDay()

```dart
T getDay(int year, int month, int day)
```

Returns a [DateTime] with the given [year], [month], and [day].

### formatMonthYear()

```dart
String formatMonthYear(T date, MaterialLocalizations localizations)
```

Formats the month and the year of the given [date].

The returned string does not contain the day of the month. This appears in the date picker invoked using [showDatePicker].

### formatYear()

```dart
String formatYear(int year, MaterialLocalizations localizations)
```

Full unabbreviated year format, e.g. 2017 rather than 17.

### formatMediumDate()

```dart
String formatMediumDate(T date, MaterialLocalizations localizations)
```

Formats the date using a medium-width format.

Abbreviates month and days of week. This appears in the header of the date picker invoked using [showDatePicker].

Examples:

- US English: Wed, Sep 27
- Russian: ср, сент. 27

### formatShortMonthDay()

```dart
String formatShortMonthDay(T date, MaterialLocalizations localizations)
```

Formats the month and day of the given [date].

Examples:

- US English: Feb 21
- Russian: 21 февр.

### formatShortDate()

```dart
String formatShortDate(T date, MaterialLocalizations localizations)
```

Formats the date using a short-width format.

Includes the abbreviation of the month, the day and year.

Examples:

- US English: Feb 21, 2019
- Russian: 21 февр. 2019 г.

### formatFullDate()

```dart
String formatFullDate(T date, MaterialLocalizations localizations)
```

Formats day of week, month, day of month and year in a long-width format.

Does not abbreviate names. Appears in spoken announcements of the date picker invoked using [showDatePicker], when accessibility mode is on.

Examples:

- US English: Wednesday, September 27, 2017
- Russian: Среда, Сентябрь 27, 2017

### formatCompactDate()

```dart
String formatCompactDate(T date, MaterialLocalizations localizations)
```

Formats the date in a compact format.

Usually just the numeric values for the for day, month and year are used.

Examples:

- US English: 02/21/2019
- Russian: 21.02.2019

See also:

- [parseCompactDate], which will convert a compact date string to a [DateTime].

### parseCompactDate()

```dart
T? parseCompactDate(String? inputString, MaterialLocalizations localizations)
```

Converts the given compact date formatted string into a [DateTime].

The format of the string must be a valid compact date format for the given locale. If the text doesn't represent a valid date, `null` will be returned.

See also:

- [formatCompactDate], which will convert a [DateTime] into a string in the compact format.

### dateHelpText()

```dart
String dateHelpText(MaterialLocalizations localizations)
```

The help text used on an empty [InputDatePickerFormField] to indicate to the user the date format being asked for.

# GregorianCalendarDelegate

```dart
class GregorianCalendarDelegate extends CalendarDelegate<DateTime> {}
```

A [CalendarDelegate] implementation for the Gregorian calendar system.

The Gregorian calendar is the most widely used civil calendar worldwide. This delegate provides standard date interpretation, formatting, and navigation based on the Gregorian system.

This delegate is the default calendar system for [CalendarDatePicker].

See also:

- [CalendarDelegate], the base class for defining custom calendars.
- [CalendarDatePicker], which uses this delegate for date selection.

### GregorianCalendarDelegate()

```dart
GregorianCalendarDelegate()
```

Creates a calendar delegate that uses the Gregorian calendar and the conventions of the current [MaterialLocalizations].

### now()

```dart
DateTime now()
```

### dateOnly()

```dart
DateTime dateOnly(DateTime date)
```

### monthDelta()

```dart
int monthDelta(DateTime startDate, DateTime endDate)
```

### addMonthsToMonthDate()

```dart
DateTime addMonthsToMonthDate(DateTime monthDate, int monthsToAdd)
```

### addDaysToDate()

```dart
DateTime addDaysToDate(DateTime date, int days)
```

### firstDayOffset()

```dart
int firstDayOffset(int year, int month, MaterialLocalizations localizations)
```

### getDaysInMonth()

```dart
int getDaysInMonth(int year, int month)
```

{@macro flutter.material.date.getDaysInMonth}

### getMonth()

```dart
DateTime getMonth(int year, int month)
```

### getDay()

```dart
DateTime getDay(int year, int month, int day)
```

### formatMonthYear()

```dart
String formatMonthYear(DateTime date, MaterialLocalizations localizations)
```

### formatMediumDate()

```dart
String formatMediumDate(DateTime date, MaterialLocalizations localizations)
```

### formatShortMonthDay()

```dart
String formatShortMonthDay(DateTime date, MaterialLocalizations localizations)
```

### formatShortDate()

```dart
String formatShortDate(DateTime date, MaterialLocalizations localizations)
```

### formatFullDate()

```dart
String formatFullDate(DateTime date, MaterialLocalizations localizations)
```

### formatCompactDate()

```dart
String formatCompactDate(DateTime date, MaterialLocalizations localizations)
```

### parseCompactDate()

```dart
DateTime? parseCompactDate(String? inputString, MaterialLocalizations localizations)
```

### dateHelpText()

```dart
String dateHelpText(MaterialLocalizations localizations)
```

# DateUtils

```dart
abstract final class DateUtils {}
```

Utility functions for working with dates.

### dateOnly()

```dart
DateTime dateOnly(DateTime date)
```

{@template flutter.material.date.dateOnly} Returns a [DateTime] with the date of the original, but time set to midnight. {@endtemplate}

### datesOnly()

```dart
DateTimeRange datesOnly(DateTimeRange range)
```

{@template flutter.material.date.datesOnly} Returns a [DateTimeRange] with the dates of the original, but with times set to midnight.

See also:

- [dateOnly], which does the same thing for a single date. {@endtemplate}

### isSameDay()

```dart
bool isSameDay(DateTime? dateA, DateTime? dateB)
```

{@template flutter.material.date.isSameDay} Returns true if the two [DateTime] objects have the same day, month, and year, or are both null. {@endtemplate}

### isSameMonth()

```dart
bool isSameMonth(DateTime? dateA, DateTime? dateB)
```

{@template flutter.material.date.isSameMonth} Returns true if the two [DateTime] objects have the same month and year, or are both null. {@endtemplate}

### monthDelta()

```dart
int monthDelta(DateTime startDate, DateTime endDate)
```

{@template flutter.material.date.monthDelta} Determines the number of months between two [DateTime] objects.

For example:

```dart
DateTime date1 = DateTime(2019, 6, 15);
DateTime date2 = DateTime(2020, 1, 15);
int delta = DateUtils.monthDelta(date1, date2);
```

The value for `delta` would be `7`. {@endtemplate}

### addMonthsToMonthDate()

```dart
DateTime addMonthsToMonthDate(DateTime monthDate, int monthsToAdd)
```

{@template flutter.material.date.addMonthsToMonthDate} Returns a [DateTime] that is [monthDate] with the added number of months and the day set to 1 and time set to midnight.

For example:

```dart
DateTime date = DateTime(2019, 1, 15);
DateTime futureDate = DateUtils.addMonthsToMonthDate(date, 3);
```

`date` would be January 15, 2019. `futureDate` would be April 1, 2019 since it adds 3 months. {@endtemplate}

### addDaysToDate()

```dart
DateTime addDaysToDate(DateTime date, int days)
```

{@template flutter.material.date.addDaysToDate} Returns a [DateTime] with the added number of days and time set to midnight. {@endtemplate}

### firstDayOffset()

```dart
int firstDayOffset(int year, int month, MaterialLocalizations localizations)
```

{@template flutter.material.date.firstDayOffset} Computes the offset from the first day of the week that the first day of the [month] falls on.

For example, September 1, 2017 falls on a Friday, which in the calendar localized for United States English appears as:

S M T W T F S _ _ _ _ _ 1 2

The offset for the first day of the months is the number of leading blanks in the calendar, i.e. 5.

The same date localized for the Russian calendar has a different offset, because the first day of week is Monday rather than Sunday:

M T W T F S S _ _ _ _ 1 2 3

So the offset is 4, rather than 5.

This code consolidates the following:

- [DateTime.weekday] provides a 1-based index into days of week, with 1 falling on Monday.
- [MaterialLocalizations.firstDayOfWeekIndex] provides a 0-based index into the [MaterialLocalizations.narrowWeekdays] list.
- [MaterialLocalizations.narrowWeekdays] list provides localized names of days of week, always starting with Sunday and ending with Saturday. {@endtemplate}

### getDaysInMonth()

```dart
int getDaysInMonth(int year, int month)
```

{@template flutter.material.date.getDaysInMonth} Returns the number of days in a month, according to the proleptic Gregorian calendar.

This applies the leap year logic introduced by the Gregorian reforms of 1582. It will not give valid results for dates prior to that time. {@endtemplate}

# DatePickerEntryMode

```dart
enum DatePickerEntryMode {}
```

Mode of date entry method for the date picker dialog.

In [calendar] mode, a calendar grid is displayed and the user taps the day they wish to select. In [input] mode, a [TextField] is displayed and the user types in the date they wish to select.

[calendarOnly] and [inputOnly] are variants of the above that don't allow the user to change to the mode.

See also:

- [showDatePicker] and [showDateRangePicker], which use this to control the initial entry mode of their dialogs.

User picks a date from calendar grid. Can switch to [input] by activating a mode button in the dialog.

User can input the date by typing it into a text field.

Can switch to [calendar] by activating a mode button in the dialog.

User can only pick a date from calendar grid.

There is no user interface to switch to another mode.

User can only input the date by typing it into a text field.

There is no user interface to switch to another mode.

# DatePickerMode

```dart
enum DatePickerMode {}
```

Initial display of a calendar date picker.

Either a grid of available years or a monthly calendar.

See also:

- [showDatePicker], which shows a dialog that contains a Material Design date picker.
- [CalendarDatePicker], widget which implements the Material Design date picker.

Choosing a month and day.

Choosing a year.

# DateTimeRange

```dart
class DateTimeRange<T extends DateTime> {}
```

Encapsulates a start and end [DateTime] that represent the range of dates.

The range includes the [start] and [end] dates. The [start] and [end] dates may be equal to indicate a date range of a single day. The [start] date must not be after the [end] date.

See also:

- [showDateRangePicker], which displays a dialog that allows the user to select a date range.

### DateTimeRange()

```dart
DateTimeRange({required T start, required T end})
```

Creates a date range for the given start and end [DateTime].

### start

```dart
T start
```

The start of the range of dates.

### end

```dart
T end
```

The end of the range of dates.

### duration

```dart
Duration get duration
```

Returns a [Duration] of the time between [start] and [end].

See [DateTime.difference] for more details.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```
