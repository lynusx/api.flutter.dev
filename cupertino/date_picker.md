@docImport 'route.dart'; @docImport 'text_theme.dart';

# SelectionOverlayBuilder

```dart
typedef SelectionOverlayBuilder = Widget? Function(BuildContext context, {required int columnCount, required int selectedIndex})
```

Defines a function signature for creating a widget that serves as a selection overlay, given the current context, the selected item's index, and the total number of columns.

# CupertinoDatePickerMode

```dart
enum CupertinoDatePickerMode {}
```

Different display modes of [CupertinoDatePicker].

See also:

- [CupertinoDatePicker], the class that implements different display modes of the iOS-style date picker.
- [CupertinoPicker], the class that implements a content agnostic spinner UI.

Mode that shows the date in hour, minute, and (optional) an AM/PM designation. The AM/PM designation is shown only if [CupertinoDatePicker] does not use 24h format. Column order is subject to internationalization.

Example: `4 | 14 | PM`.

Mode that shows the date in month, day of month, and year. Name of month is spelled in full. Column order is subject to internationalization.

Example: `July | 13 | 2012`.

Mode that shows the date as day of the week, month, day of month and the time in hour, minute, and (optional) an AM/PM designation. The AM/PM designation is shown only if [CupertinoDatePicker] does not use 24h format. Column order is subject to internationalization.

Example: `Fri Jul 13 | 4 | 14 | PM`

Mode that shows the date in month and year. Name of month is spelled in full. Column order is subject to internationalization.

Example: `July | 2012`.

# CupertinoDatePicker

```dart
class CupertinoDatePicker extends StatefulWidget {}
```

A date picker widget in iOS style.

There are several modes of the date picker listed in [CupertinoDatePickerMode].

The class will display its children as consecutive columns. Its children order is based on internationalization, or the [dateOrder] property if specified.

Example of the picker in date mode:

- US-English: `| July | 13 | 2012 |`
- Vietnamese: `| 13 | Tháng 7 | 2012 |`

Can be used with [showCupertinoModalPopup] to display the picker modally at the bottom of the screen.

Sizes itself to its parent and may not render correctly if not given the full screen width. Content texts are shown with [CupertinoTextThemeData.dateTimePickerTextStyle].

{@tool dartpad} This sample shows how to implement CupertinoDatePicker with different picker modes. We can provide initial dateTime value for the picker to display. When user changes the drag the date or time wheels, the picker will call onDateTimeChanged callback.

CupertinoDatePicker can be displayed directly on a screen or in a popup.

** See code in examples/api/lib/cupertino/date_picker/cupertino_date_picker.0.dart ** {@end-tool}

See also:

- [CupertinoTimerPicker], the class that implements the iOS-style timer picker.
- [CupertinoPicker], the class that implements a content agnostic spinner UI.
- <https://developer.apple.com/design/human-interface-guidelines/ios/controls/pickers/>

### CupertinoDatePicker()

```dart
CupertinoDatePicker({dynamic key, CupertinoDatePickerMode mode = CupertinoDatePickerMode.dateAndTime, required ValueChanged<DateTime> onDateTimeChanged, DateTime? initialDateTime, DateTime? minimumDate, DateTime? maximumDate, int minimumYear = 1, int? maximumYear, int minuteInterval = 1, bool use24hFormat = false, DatePickerDateOrder? dateOrder, Color? backgroundColor, bool showDayOfWeek = false, bool showTimeSeparator = false, double itemExtent = _kItemExtent, SelectionOverlayBuilder? selectionOverlayBuilder, SelectableDayPredicate? selectableDayPredicate, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate})
```

Constructs an iOS style date picker.

[mode] is one of the mode listed in [CupertinoDatePickerMode] and defaults to [CupertinoDatePickerMode.dateAndTime].

[onDateTimeChanged] is the callback called when the selected date or time changes. When in [CupertinoDatePickerMode.time] mode, the year, month and day will be the same as [initialDateTime]. When in [CupertinoDatePickerMode.date] mode, this callback will always report the start time of the currently selected day. When in [CupertinoDatePickerMode.monthYear] mode, the day and time will be the start time of the first day of the month.

[initialDateTime] is the initial date time of the picker. Defaults to the present date and time. The present must conform to the intervals set in [minimumDate], [maximumDate], [minimumYear], and [maximumYear].

[minimumDate] is the minimum selectable [DateTime] of the picker. When set to null, the picker does not limit the minimum [DateTime] the user can pick. In [CupertinoDatePickerMode.time] mode, [minimumDate] should typically be on the same date as [initialDateTime], as the picker will not limit the minimum time the user can pick if it's set to a date earlier than that.

[maximumDate] is the maximum selectable [DateTime] of the picker. When set to null, the picker does not limit the maximum [DateTime] the user can pick. In [CupertinoDatePickerMode.time] mode, [maximumDate] should typically be on the same date as [initialDateTime], as the picker will not limit the maximum time the user can pick if it's set to a date later than that.

[minimumYear] is the minimum year that the picker can be scrolled to in [CupertinoDatePickerMode.date] mode. Defaults to 1.

[maximumYear] is the maximum year that the picker can be scrolled to in [CupertinoDatePickerMode.date] mode. Null if there's no limit.

[minuteInterval] is the granularity of the minute spinner. Must be a positive integer factor of 60.

[use24hFormat] decides whether 24 hour format is used. Defaults to false.

[dateOrder] determines the order of the columns inside [CupertinoDatePicker] in [CupertinoDatePickerMode.date] and [CupertinoDatePickerMode.monthYear] mode. When using monthYear mode, both [DatePickerDateOrder.dmy] and [DatePickerDateOrder.mdy] will result in the month|year order. Defaults to the locale's default date format/order.

### mode

```dart
CupertinoDatePickerMode mode
```

The mode of the date picker as one of [CupertinoDatePickerMode]. Defaults to [CupertinoDatePickerMode.dateAndTime]. Value cannot change after initial build.

### initialDateTime

```dart
DateTime initialDateTime
```

The initial date and/or time of the picker. Defaults to the present date and time. The present must conform to the intervals set in [minimumDate], [maximumDate], [minimumYear], and [maximumYear].

Changing this value after the initial build will not affect the currently selected date time.

### minimumDate

```dart
DateTime? minimumDate
```

The minimum selectable date that the picker can settle on.

When non-null, the user can still scroll the picker to [DateTime]s earlier than [minimumDate], but the [onDateTimeChanged] will not be called on these [DateTime]s. Once let go, the picker will scroll back to [minimumDate].

In [CupertinoDatePickerMode.time] mode, a time becomes unselectable if the [DateTime] produced by combining that particular time and the date part of [initialDateTime] is earlier than [minimumDate]. So typically [minimumDate] needs to be set to a [DateTime] that is on the same date as [initialDateTime].

Defaults to null. When set to null, the picker does not impose a limit on the earliest [DateTime] the user can select.

### maximumDate

```dart
DateTime? maximumDate
```

The maximum selectable date that the picker can settle on.

When non-null, the user can still scroll the picker to [DateTime]s later than [maximumDate], but the [onDateTimeChanged] will not be called on these [DateTime]s. Once let go, the picker will scroll back to [maximumDate].

In [CupertinoDatePickerMode.time] mode, a time becomes unselectable if the [DateTime] produced by combining that particular time and the date part of [initialDateTime] is later than [maximumDate]. So typically [maximumDate] needs to be set to a [DateTime] that is on the same date as [initialDateTime].

Defaults to null. When set to null, the picker does not impose a limit on the latest [DateTime] the user can select.

### minimumYear

```dart
int minimumYear
```

Minimum year that the picker can be scrolled to in [CupertinoDatePickerMode.date] mode. Defaults to 1.

### maximumYear

```dart
int? maximumYear
```

Maximum year that the picker can be scrolled to in [CupertinoDatePickerMode.date] mode. Null if there's no limit.

### minuteInterval

```dart
int minuteInterval
```

The granularity of the minutes spinner, if it is shown in the current mode. Must be an integer factor of 60.

### use24hFormat

```dart
bool use24hFormat
```

Whether to use 24 hour format. Defaults to false.

### dateOrder

```dart
DatePickerDateOrder? dateOrder
```

Determines the order of the columns inside [CupertinoDatePicker] in [CupertinoDatePickerMode.date] and [CupertinoDatePickerMode.monthYear] mode. When using monthYear mode, both [DatePickerDateOrder.dmy] and [DatePickerDateOrder.mdy] will result in the month|year order. Defaults to the locale's default date format/order.

### onDateTimeChanged

```dart
ValueChanged<DateTime> onDateTimeChanged
```

Callback called when the selected date and/or time changes. If the new selected [DateTime] is not valid, or is not in the [minimumDate] through [maximumDate] range, this callback will not be called.

The timing of this callback is controlled by [changeReportingBehavior].

### backgroundColor

```dart
Color? backgroundColor
```

Background color of date picker.

Defaults to null, which disables background painting entirely.

### showDayOfWeek

```dart
bool showDayOfWeek
```

Whether to show the day of week alongside the day in [CupertinoDatePickerMode.date] mode.

Defaults to false.

### showTimeSeparator

```dart
bool showTimeSeparator
```

Whether to show the time separator between hour and minute in the time [CupertinoDatePickerMode.time] and datetime [CupertinoDatePickerMode.dateAndTime] picker modes.

Throws an error if set to true in [CupertinoDatePickerMode.date] and [CupertinoDatePickerMode.monthYear] mode.

Defaults to false.

### selectableDayPredicate

```dart
SelectableDayPredicate? selectableDayPredicate
```

Function to provide full control over which [DateTime] can be selected.

### itemExtent

```dart
double itemExtent
```

{@macro flutter.cupertino.picker.itemExtent}

Defaults to a value that matches the default iOS date picker wheel.

### selectionOverlayBuilder

```dart
SelectionOverlayBuilder? selectionOverlayBuilder
```

A function that returns a widget that is overlaid on the picker to highlight the currently selected entry.

If unspecified, it defaults to a [CupertinoPickerDefaultSelectionOverlay] which is a gray rounded rectangle overlay in iOS 14 style.

If the selection overlay builder returns null, no overlay will be drawn.

{@tool snippet}

This example shows how to recreate the default selection overlay with selectionOverlayBuilder.

```dart
CupertinoDatePicker(
  onDateTimeChanged: (DateTime newDateTime) {},
  mode: CupertinoDatePickerMode.date,
  initialDateTime: DateTime(2018, 9, 15),
  selectionOverlayBuilder: (
    BuildContext context, {
    required int selectedIndex,
    required int columnCount,
  }) {
    if (selectedIndex == 0) {
      return const CupertinoPickerDefaultSelectionOverlay(
        capEndEdge: false,
      );
    } else if (selectedIndex == columnCount - 1) {
      return const CupertinoPickerDefaultSelectionOverlay(
        capStartEdge: false,
      );
    }
    return const CupertinoPickerDefaultSelectionOverlay(
      capStartEdge: false,
      capEndEdge: false,
    );
  },
)
```

{@end-tool}

### changeReportingBehavior

```dart
ChangeReportingBehavior changeReportingBehavior
```

The behavior of reporting the selected date.

This determines when the [onDateTimeChanged] callback is called.

Native iOS 18 behavior is [ChangeReportingBehavior.onScrollEnd], which calls the callback only when the scrolling stops.

Defaults to [ChangeReportingBehavior.onScrollUpdate].

### createState()

```dart
State<StatefulWidget> createState()
```

### getColumnWidth()

```dart
double getColumnWidth({required List<String> texts, required BuildContext context, TextStyle? textStyle})
```

Returns the width of column in the picker.

This method is intended for testing only. It calculates the width of the widest column in the picker based on the provided list of texts and the given [BuildContext].

# CupertinoTimerPickerMode

```dart
enum CupertinoTimerPickerMode {}
```

Different modes of [CupertinoTimerPicker].

See also:

- [CupertinoTimerPicker], the class that implements the iOS-style timer picker.
- [CupertinoPicker], the class that implements a content agnostic spinner UI.

Mode that shows the timer duration in hour and minute.

Examples: 16 hours | 14 min.

Mode that shows the timer duration in minute and second.

Examples: 14 min | 43 sec.

Mode that shows the timer duration in hour, minute, and second.

Examples: 16 hours | 14 min | 43 sec.

# CupertinoTimerPicker

```dart
class CupertinoTimerPicker extends StatefulWidget {}
```

A countdown timer picker in iOS style.

This picker shows a countdown duration with hour, minute and second spinners. The duration is bound between 0 and 23 hours 59 minutes 59 seconds.

There are several modes of the timer picker listed in [CupertinoTimerPickerMode].

The picker has a fixed size of 320 x 216, in logical pixels, with the exception of [CupertinoTimerPickerMode.hms], which is 330 x 216. If the parent widget provides more space than it needs, the picker will position itself according to its [alignment] property.

{@tool dartpad} This example shows a [CupertinoTimerPicker] that returns a countdown duration.

** See code in examples/api/lib/cupertino/date_picker/cupertino_timer_picker.0.dart ** {@end-tool}

See also:

- [CupertinoDatePicker], the class that implements different display modes of the iOS-style date picker.
- [CupertinoPicker], the class that implements a content agnostic spinner UI.
- <https://developer.apple.com/design/human-interface-guidelines/ios/controls/pickers/>

### CupertinoTimerPicker()

```dart
CupertinoTimerPicker({dynamic key, CupertinoTimerPickerMode mode = CupertinoTimerPickerMode.hms, Duration initialTimerDuration = Duration.zero, int minuteInterval = 1, int secondInterval = 1, AlignmentGeometry alignment = Alignment.center, Color? backgroundColor, double itemExtent = _kItemExtent, required ValueChanged<Duration> onTimerDurationChanged, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, SelectionOverlayBuilder? selectionOverlayBuilder})
```

Constructs an iOS style countdown timer picker.

[mode] is one of the modes listed in [CupertinoTimerPickerMode] and defaults to [CupertinoTimerPickerMode.hms].

[onTimerDurationChanged] is the callback called when the selected duration changes.

[initialTimerDuration] defaults to 0 second and is limited from 0 second to 23 hours 59 minutes 59 seconds.

[minuteInterval] is the granularity of the minute spinner. Must be a positive integer factor of 60.

[secondInterval] is the granularity of the second spinner. Must be a positive integer factor of 60.

### mode

```dart
CupertinoTimerPickerMode mode
```

The mode of the timer picker.

### initialTimerDuration

```dart
Duration initialTimerDuration
```

The initial duration of the countdown timer.

### minuteInterval

```dart
int minuteInterval
```

The granularity of the minute spinner. Must be a positive integer factor of 60.

### secondInterval

```dart
int secondInterval
```

The granularity of the second spinner. Must be a positive integer factor of 60.

### onTimerDurationChanged

```dart
ValueChanged<Duration> onTimerDurationChanged
```

Callback called when the timer duration changes.

The timing of this callback is controlled by [changeReportingBehavior].

### alignment

```dart
AlignmentGeometry alignment
```

Defines how the timer picker should be positioned within its parent.

Defaults to [Alignment.center].

### backgroundColor

```dart
Color? backgroundColor
```

Background color of timer picker.

Defaults to null, which disables background painting entirely.

### itemExtent

```dart
double itemExtent
```

{@macro flutter.cupertino.picker.itemExtent}

Defaults to a value that matches the default iOS timer picker wheel.

### selectionOverlayBuilder

```dart
SelectionOverlayBuilder? selectionOverlayBuilder
```

A function that returns a widget that is overlaid on the picker to highlight the currently selected entry.

If unspecified, it defaults to a [CupertinoPickerDefaultSelectionOverlay] which is a gray rounded rectangle overlay in iOS 14 style.

If the selection overlay builder returns null, no overlay will be drawn.

{@tool snippet}

This example shows how to recreate the default selection overlay with selectionOverlayBuilder.

```dart
CupertinoTimerPicker(
  onTimerDurationChanged: (Duration newDateTime) {},
  selectionOverlayBuilder: (
    BuildContext context, {
    required int selectedIndex,
    required int columnCount,
  }) {
    if (selectedIndex == 0) {
      return const CupertinoPickerDefaultSelectionOverlay(
        capEndEdge: false,
      );
    } else if (selectedIndex == columnCount - 1) {
      return const CupertinoPickerDefaultSelectionOverlay(
        capStartEdge: false,
      );
    }
    return const CupertinoPickerDefaultSelectionOverlay(
      capStartEdge: false,
      capEndEdge: false,
    );
  },
)
```

{@end-tool}

### changeReportingBehavior

```dart
ChangeReportingBehavior changeReportingBehavior
```

The behavior of reporting the selected duration.

This determines when the [onTimerDurationChanged] callback is called.

Native iOS 18 behavior is [ChangeReportingBehavior.onScrollEnd], which calls the callback only when the scrolling stops.

Defaults to [ChangeReportingBehavior.onScrollUpdate].

### createState()

```dart
State<StatefulWidget> createState()
```
