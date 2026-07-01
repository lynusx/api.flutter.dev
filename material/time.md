@docImport 'time_picker.dart';

# DayPeriod

```dart
enum DayPeriod {}
```

Whether the [TimeOfDay] is before or after noon.

Ante meridiem (before noon).

Post meridiem (after noon).

# TimeOfDay

```dart
class TimeOfDay implements Comparable<TimeOfDay> {}
```

A value representing a time during the day, independent of the date that day might fall on or the time zone.

The time is represented by [hour] and [minute] pair. Once created, both values cannot be changed.

You can create TimeOfDay using the constructor which requires both hour and minute or using [DateTime] object. Hours are specified between 0 and 23, as in a 24-hour clock.

{@tool snippet}

```dart
TimeOfDay now = TimeOfDay.now();
const TimeOfDay releaseTime = TimeOfDay(hour: 15, minute: 0); // 3:00pm
TimeOfDay roomBooked = TimeOfDay.fromDateTime(DateTime.parse('2018-10-20 16:30:04Z')); // 4:30pm
```

{@end-tool}

See also:

- [showTimePicker], which returns this type.
- [MaterialLocalizations], which provides methods for formatting values of this type according to the chosen [Locale].
- [DateTime], which represents date and time, and is subject to eras and time zones.

### TimeOfDay()

```dart
TimeOfDay({required int hour, required int minute})
```

Creates a time of day.

The [hour] argument must be between 0 and 23, inclusive. The [minute] argument must be between 0 and 59, inclusive.

### TimeOfDay.fromDateTime()

```dart
TimeOfDay.fromDateTime(DateTime time)
```

Creates a time of day based on the given time.

The [hour] is set to the time's hour and the [minute] is set to the time's minute in the timezone of the given [DateTime].

### TimeOfDay.now()

```dart
TimeOfDay.now()
```

Creates a time of day based on the current time.

The [hour] is set to the current hour and the [minute] is set to the current minute in the local time zone.

### hoursPerDay

```dart
int hoursPerDay
```

The number of hours in one day, i.e. 24.

### hoursPerPeriod

```dart
int hoursPerPeriod
```

The number of hours in one day period (see also [DayPeriod]), i.e. 12.

### minutesPerHour

```dart
int minutesPerHour
```

The number of minutes in one hour, i.e. 60.

### replacing()

```dart
TimeOfDay replacing({int? hour, int? minute})
```

Returns a new TimeOfDay with the hour and/or minute replaced.

### hour

```dart
int hour
```

The selected hour, in 24 hour time from 0..23.

### minute

```dart
int minute
```

The selected minute.

### period

```dart
DayPeriod get period
```

Whether this time of day is before or after noon.

### hourOfPeriod

```dart
int get hourOfPeriod
```

Which hour of the current period (e.g., am or pm) this time is.

For 12AM (midnight) and 12PM (noon) this returns 12.

### periodOffset

```dart
int get periodOffset
```

The hour at which the current period starts.

### format()

```dart
String format(BuildContext context)
```

Returns the localized string representation of this time of day.

This is a shortcut for [MaterialLocalizations.formatTimeOfDay].

### isBefore()

```dart
bool isBefore(TimeOfDay other)
```

Whether this [TimeOfDay] occurs earlier than [other].

Does not account for day or sub-minute differences. This means that "00:00" of the next day is still before "23:00" of this day.

### isAfter()

```dart
bool isAfter(TimeOfDay other)
```

Whether this [TimeOfDay] occurs later than [other].

Does not account for day or sub-minute differences. This means that "00:00" of the next day is still before "23:00" of this day.

### isAtSameTimeAs()

```dart
bool isAtSameTimeAs(TimeOfDay other)
```

Whether this [TimeOfDay] occurs at the same time as [other].

Does not account for day or sub-minute differences. This means that "00:00" of the next day is still before "23:00" of this day.

### compareTo()

```dart
int compareTo(TimeOfDay other)
```

Compares this [TimeOfDay] object to [other] independent of date.

Does not account for day or sub-minute differences. This means that "00:00" of the next day is still before "23:00" of this day.

A [compareTo] function returns:

- a negative value if this TimeOfDay [isBefore] [other].
- `0` if this DateTime [isAtSameTimeAs] [other], and
- a positive value otherwise (when this TimeOfDay [isAfter] [other]).

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

# RestorableTimeOfDay

```dart
class RestorableTimeOfDay extends RestorableValue<TimeOfDay> {}
```

A [RestorableValue] that knows how to save and restore [TimeOfDay].

{@macro flutter.widgets.RestorableNum}.

### RestorableTimeOfDay()

```dart
RestorableTimeOfDay(TimeOfDay defaultValue)
```

Creates a [RestorableTimeOfDay].

{@macro flutter.widgets.RestorableNum.constructor}

### createDefaultValue()

```dart
TimeOfDay createDefaultValue()
```

### didUpdateValue()

```dart
void didUpdateValue(TimeOfDay? oldValue)
```

### fromPrimitives()

```dart
TimeOfDay fromPrimitives(Object? data)
```

### toPrimitives()

```dart
Object? toPrimitives()
```

# TimeOfDayFormat

```dart
enum TimeOfDayFormat {}
```

Determines how the time picker invoked using [showTimePicker] formats and lays out the time controls.

The time picker provides layout configurations optimized for each of the enum values.

Corresponds to the ICU 'HH:mm' pattern.

This format uses 24-hour two-digit zero-padded hours. Controls are always laid out horizontally. Hours are separated from minutes by one colon character.

Corresponds to the ICU 'HH.mm' pattern.

This format uses 24-hour two-digit zero-padded hours. Controls are always laid out horizontally. Hours are separated from minutes by one dot character.

Corresponds to the ICU "HH 'h' mm" pattern used in Canadian French.

This format uses 24-hour two-digit zero-padded hours. Controls are always laid out horizontally. Hours are separated from minutes by letter 'h'.

Corresponds to the ICU 'H:mm' pattern.

This format uses 24-hour non-padded variable-length hours. Controls are always laid out horizontally. Hours are separated from minutes by one colon character.

Corresponds to the ICU 'h:mm a' pattern.

This format uses 12-hour non-padded variable-length hours with a day period. Controls are laid out horizontally in portrait mode. In landscape mode, the day period appears vertically after (consistent with the ambient [TextDirection]) hour-minute indicator. Hours are separated from minutes by one colon character.

Corresponds to the ICU 'a h:mm' pattern.

This format uses 12-hour non-padded variable-length hours with a day period. Controls are laid out horizontally in portrait mode. In landscape mode, the day period appears vertically before (consistent with the ambient [TextDirection]) hour-minute indicator. Hours are separated from minutes by one colon character.

# HourFormat

```dart
enum HourFormat {}
```

Describes how hours are formatted.

Zero-padded two-digit 24-hour format ranging from "00" to "23".

Non-padded variable-length 24-hour format ranging from "0" to "23".

Non-padded variable-length hour in day period format ranging from "1" to "12".

# hourFormat()

```dart
HourFormat hourFormat({required TimeOfDayFormat of})
```

The [HourFormat] used for the given [TimeOfDayFormat].
