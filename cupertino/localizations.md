@docImport 'bottom_tab_bar.dart'; @docImport 'date_picker.dart'; @docImport 'expansion_tile.dart'; @docImport 'nav_bar.dart'; @docImport 'search_field.dart';

# DatePickerDateTimeOrder

```dart
enum DatePickerDateTimeOrder {}
```

Determines the order of the columns inside [CupertinoDatePicker] in time and date time mode.

Order of the columns, from left to right: date, hour, minute, am/pm.

Example: Fri Aug 31 | 02 | 08 | PM.

Order of the columns, from left to right: date, am/pm, hour, minute.

Example: Fri Aug 31 | PM | 02 | 08.

Order of the columns, from left to right: hour, minute, am/pm, date.

Example: 02 | 08 | PM | Fri Aug 31.

Order of the columns, from left to right: am/pm, hour, minute, date.

Example: PM | 02 | 08 | Fri Aug 31.

# DatePickerDateOrder

```dart
enum DatePickerDateOrder {}
```

Determines the order of the columns inside [CupertinoDatePicker] in date mode.

Order of the columns, from left to right: day, month, year.

Example: 12 | March | 1996.

Order of the columns, from left to right: month, day, year.

Example: March | 12 | 1996.

Order of the columns, from left to right: year, month, day.

Example: 1996 | March | 12.

Order of the columns, from left to right: year, day, month.

Example: 1996 | 12 | March.

# CupertinoLocalizations

```dart
abstract class CupertinoLocalizations {}
```

Defines the localized resource values used by the Cupertino widgets.

See also:

- [DefaultCupertinoLocalizations], the default, English-only, implementation of this interface.

### datePickerYear()

```dart
String datePickerYear(int yearIndex)
```

Year that is shown in [CupertinoDatePicker] spinner corresponding to the given year index.

Examples: datePickerYear(1) in:

- US English: 2018
- Korean: 2018년

### datePickerMonth()

```dart
String datePickerMonth(int monthIndex)
```

Month that is shown in [CupertinoDatePicker] spinner corresponding to the given month index.

Examples: datePickerMonth(1) in:

- US English: January
- Korean: 1월
- Russian: января

### datePickerStandaloneMonth()

```dart
String datePickerStandaloneMonth(int monthIndex)
```

Month that is shown in [CupertinoDatePicker] spinner corresponding to the given month index in [CupertinoDatePickerMode.monthYear] mode.

This is distinct from [datePickerMonth] because in some languages, like Russian, the name of a month takes a different form depending on whether it is preceded by a day or whether it stands alone.

Examples: datePickerMonth(1) in:

- US English: January
- Korean: 1월
- Russian: Январь

### datePickerDayOfMonth()

```dart
String datePickerDayOfMonth(int dayIndex, [int? weekDay])
```

Day of month that is shown in [CupertinoDatePicker] spinner corresponding to the given day index.

If weekDay is provided then it will also show weekday name alongside the numerical day.

Examples: datePickerDayOfMonth(1) in:

- US English: 1
- Korean: 1일 Examples: datePickerDayOfMonth(1, 1) in:

- US English: Mon 1

### datePickerMediumDate()

```dart
String datePickerMediumDate(DateTime date)
```

The medium-width date format that is shown in [CupertinoDatePicker] spinner. Abbreviates month and days of week.

Examples:

- US English: Wed Sep 27
- Russian: ср сент. 27

### datePickerHour()

```dart
String datePickerHour(int hour)
```

Hour that is shown in [CupertinoDatePicker] spinner corresponding to the given hour value.

Examples: datePickerHour(1) in:

- US English: 1
- Arabic: ٠١

### datePickerHourSemanticsLabel()

```dart
String? datePickerHourSemanticsLabel(int hour)
```

Semantics label for the given hour value in [CupertinoDatePicker].

### datePickerMinute()

```dart
String datePickerMinute(int minute)
```

Minute that is shown in [CupertinoDatePicker] spinner corresponding to the given minute value.

Examples: datePickerMinute(1) in:

- US English: 01
- Arabic: ٠١

### datePickerMinuteSemanticsLabel()

```dart
String? datePickerMinuteSemanticsLabel(int minute)
```

Semantics label for the given minute value in [CupertinoDatePicker].

### datePickerDateOrder

```dart
DatePickerDateOrder get datePickerDateOrder
```

The order of the date elements that will be shown in [CupertinoDatePicker].

### datePickerDateTimeOrder

```dart
DatePickerDateTimeOrder get datePickerDateTimeOrder
```

The order of the time elements that will be shown in [CupertinoDatePicker].

### anteMeridiemAbbreviation

```dart
String get anteMeridiemAbbreviation
```

The abbreviation for ante meridiem (before noon) shown in the time picker.

### postMeridiemAbbreviation

```dart
String get postMeridiemAbbreviation
```

The abbreviation for post meridiem (after noon) shown in the time picker.

### todayLabel

```dart
String get todayLabel
```

Label shown in date pickers when the date is today.

### alertDialogLabel

```dart
String get alertDialogLabel
```

The term used by the system to announce dialog alerts.

### tabSemanticsLabel()

```dart
String tabSemanticsLabel({required int tabIndex, required int tabCount})
```

The accessibility label used on a tab in a [CupertinoTabBar].

This message describes the index of the selected tab and how many tabs there are, e.g. 'tab, 1 of 2' in United States English.

`tabIndex` and `tabCount` must be greater than or equal to one.

### timerPickerHour()

```dart
String timerPickerHour(int hour)
```

Hour that is shown in [CupertinoTimerPicker] corresponding to the given hour value.

Examples: timerPickerHour(1) in:

- US English: 1
- Arabic: ١

### timerPickerMinute()

```dart
String timerPickerMinute(int minute)
```

Minute that is shown in [CupertinoTimerPicker] corresponding to the given minute value.

Examples: timerPickerMinute(1) in:

- US English: 1
- Arabic: ١

### timerPickerSecond()

```dart
String timerPickerSecond(int second)
```

Second that is shown in [CupertinoTimerPicker] corresponding to the given second value.

Examples: timerPickerSecond(1) in:

- US English: 1
- Arabic: ١

### timerPickerHourLabel()

```dart
String? timerPickerHourLabel(int hour)
```

Label that appears next to the hour picker in [CupertinoTimerPicker] when selected hour value is `hour`. This function will deal with pluralization based on the `hour` parameter.

### timerPickerHourLabels

```dart
List<String> get timerPickerHourLabels
```

All possible hour labels that appears next to the hour picker in [CupertinoTimerPicker]

### timerPickerMinuteLabel()

```dart
String? timerPickerMinuteLabel(int minute)
```

Label that appears next to the minute picker in [CupertinoTimerPicker] when selected minute value is `minute`. This function will deal with pluralization based on the `minute` parameter.

### timerPickerMinuteLabels

```dart
List<String> get timerPickerMinuteLabels
```

All possible minute labels that appears next to the minute picker in [CupertinoTimerPicker]

### timerPickerSecondLabel()

```dart
String? timerPickerSecondLabel(int second)
```

Label that appears next to the minute picker in [CupertinoTimerPicker] when selected minute value is `second`. This function will deal with pluralization based on the `second` parameter.

### timerPickerSecondLabels

```dart
List<String> get timerPickerSecondLabels
```

All possible second labels that appears next to the second picker in [CupertinoTimerPicker]

### cutButtonLabel

```dart
String get cutButtonLabel
```

The term used for cutting.

### copyButtonLabel

```dart
String get copyButtonLabel
```

The term used for copying.

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

The term used for pasting.

### clearButtonLabel

```dart
String get clearButtonLabel
```

The term used for clearing a field.

### noSpellCheckReplacementsLabel

```dart
String get noSpellCheckReplacementsLabel
```

Label that appears in the Cupertino toolbar when the spell checker couldn't find any replacements for the current word.

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

The term used for selecting everything.

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

The term used for looking up a selection.

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

The term used for launching a web search on a selection.

### shareButtonLabel

```dart
String get shareButtonLabel
```

The term used for launching a web search on a selection.

### searchTextFieldPlaceholderLabel

```dart
String get searchTextFieldPlaceholderLabel
```

The default placeholder used in [CupertinoSearchTextField].

### modalBarrierDismissLabel

```dart
String get modalBarrierDismissLabel
```

Label read out by accessibility tools (VoiceOver) for a modal barrier to indicate that a tap dismisses the barrier.

A modal barrier can for example be found behind an alert or popup to block user interaction with elements behind it.

### menuDismissLabel

```dart
String get menuDismissLabel
```

Label read out by accessibility tools (VoiceOver) for a context menu to indicate that a tap outside dismisses the context menu.

### cancelButtonLabel

```dart
String get cancelButtonLabel
```

The label for the cancel button in modal views, used in [CupertinoNavigationBar] and [CupertinoSliverNavigationBar].

### backButtonLabel

```dart
String get backButtonLabel
```

The label for the back button, used in [CupertinoNavigationBar] and [CupertinoSliverNavigationBar].

### expansionTileExpandedHint

```dart
String get expansionTileExpandedHint
```

The semantics hint to describe the tap action on an expanded [CupertinoExpansionTile] on iOS and macOS. This is appended to the [collapsedHint] hint to provide a more detailed description of the action, e.g. "Expanded double tap to collapse".

### expansionTileCollapsedHint

```dart
String get expansionTileCollapsedHint
```

The semantics hint to describe the tap action on a collapsed [CupertinoExpansionTile] on iOS and macOS. This is appended to the [expandedHint] hint to provide a more detailed description of the action, e.g. "Collapsed double tap to expand".

### expansionTileExpandedTapHint

```dart
String get expansionTileExpandedTapHint
```

The semantics hint to describe the tap action on an expanded [CupertinoExpansionTile].

### expansionTileCollapsedTapHint

```dart
String get expansionTileCollapsedTapHint
```

The semantics hint to describe the tap action on a collapsed [CupertinoExpansionTile].

### expandedHint

```dart
String get expandedHint
```

The semantics hint to describe the [CupertinoExpansionTile] expanded state.

### collapsedHint

```dart
String get collapsedHint
```

The semantics hint to describe the [CupertinoExpansionTile] collapsed state.

### of()

```dart
CupertinoLocalizations of(BuildContext context)
```

The `CupertinoLocalizations` from the closest [Localizations] instance that encloses the given context.

If no [CupertinoLocalizations] are available in the given `context`, this method throws an exception.

This method is just a convenient shorthand for: `Localizations.of<CupertinoLocalizations>(context, CupertinoLocalizations)!`.

References to the localized resources defined by this class are typically written in terms of this method. For example:

```dart
CupertinoLocalizations.of(context).anteMeridiemAbbreviation;
```

# DefaultCupertinoLocalizations

```dart
class DefaultCupertinoLocalizations implements CupertinoLocalizations {}
```

US English strings for the Cupertino widgets.

### DefaultCupertinoLocalizations()

```dart
DefaultCupertinoLocalizations()
```

Constructs an object that defines the cupertino widgets' localized strings for US English (only).

[LocalizationsDelegate] implementations typically call the static [load] function, rather than constructing this class directly.

### datePickerYear()

```dart
String datePickerYear(int yearIndex)
```

### datePickerMonth()

```dart
String datePickerMonth(int monthIndex)
```

### datePickerStandaloneMonth()

```dart
String datePickerStandaloneMonth(int monthIndex)
```

### datePickerDayOfMonth()

```dart
String datePickerDayOfMonth(int dayIndex, [int? weekDay])
```

### datePickerHour()

```dart
String datePickerHour(int hour)
```

### datePickerHourSemanticsLabel()

```dart
String datePickerHourSemanticsLabel(int hour)
```

### datePickerMinute()

```dart
String datePickerMinute(int minute)
```

### datePickerMinuteSemanticsLabel()

```dart
String datePickerMinuteSemanticsLabel(int minute)
```

### datePickerMediumDate()

```dart
String datePickerMediumDate(DateTime date)
```

### datePickerDateOrder

```dart
DatePickerDateOrder get datePickerDateOrder
```

### datePickerDateTimeOrder

```dart
DatePickerDateTimeOrder get datePickerDateTimeOrder
```

### anteMeridiemAbbreviation

```dart
String get anteMeridiemAbbreviation
```

### postMeridiemAbbreviation

```dart
String get postMeridiemAbbreviation
```

### todayLabel

```dart
String get todayLabel
```

### alertDialogLabel

```dart
String get alertDialogLabel
```

### tabSemanticsLabel()

```dart
String tabSemanticsLabel({required int tabIndex, required int tabCount})
```

### timerPickerHour()

```dart
String timerPickerHour(int hour)
```

### timerPickerMinute()

```dart
String timerPickerMinute(int minute)
```

### timerPickerSecond()

```dart
String timerPickerSecond(int second)
```

### timerPickerHourLabel()

```dart
String timerPickerHourLabel(int hour)
```

### timerPickerHourLabels

```dart
List<String> get timerPickerHourLabels
```

### timerPickerMinuteLabel()

```dart
String timerPickerMinuteLabel(int minute)
```

### timerPickerMinuteLabels

```dart
List<String> get timerPickerMinuteLabels
```

### timerPickerSecondLabel()

```dart
String timerPickerSecondLabel(int second)
```

### timerPickerSecondLabels

```dart
List<String> get timerPickerSecondLabels
```

### cutButtonLabel

```dart
String get cutButtonLabel
```

### copyButtonLabel

```dart
String get copyButtonLabel
```

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

### clearButtonLabel

```dart
String get clearButtonLabel
```

### noSpellCheckReplacementsLabel

```dart
String get noSpellCheckReplacementsLabel
```

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

### shareButtonLabel

```dart
String get shareButtonLabel
```

### searchTextFieldPlaceholderLabel

```dart
String get searchTextFieldPlaceholderLabel
```

### modalBarrierDismissLabel

```dart
String get modalBarrierDismissLabel
```

### menuDismissLabel

```dart
String get menuDismissLabel
```

### cancelButtonLabel

```dart
String get cancelButtonLabel
```

### backButtonLabel

```dart
String get backButtonLabel
```

### expansionTileExpandedHint

```dart
String get expansionTileExpandedHint
```

### expansionTileCollapsedHint

```dart
String get expansionTileCollapsedHint
```

### expansionTileExpandedTapHint

```dart
String get expansionTileExpandedTapHint
```

### expansionTileCollapsedTapHint

```dart
String get expansionTileCollapsedTapHint
```

### expandedHint

```dart
String get expandedHint
```

### collapsedHint

```dart
String get collapsedHint
```

### load()

```dart
Future<CupertinoLocalizations> load(Locale locale)
```

Creates an object that provides US English resource values for the cupertino library widgets.

The [locale] parameter is ignored.

This method is typically used to create a [LocalizationsDelegate].

### delegate

```dart
LocalizationsDelegate<CupertinoLocalizations> delegate
```

A [LocalizationsDelegate] that uses [DefaultCupertinoLocalizations.load] to create an instance of this class.
