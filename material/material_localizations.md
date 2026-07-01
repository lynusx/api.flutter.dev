@docImport 'package:flutter/services.dart'; @docImport 'package:flutter_localizations/flutter_localizations.dart';

@docImport 'about.dart'; @docImport 'action_buttons.dart'; @docImport 'app.dart'; @docImport 'app_bar.dart'; @docImport 'bottom_sheet.dart'; @docImport 'calendar_date_picker.dart'; @docImport 'chip.dart'; @docImport 'date_picker.dart'; @docImport 'expand_icon.dart'; @docImport 'expansion_tile.dart'; @docImport 'input_date_picker_form_field.dart'; @docImport 'paginated_data_table.dart'; @docImport 'popup_menu.dart'; @docImport 'refresh_indicator.dart'; @docImport 'reorderable_list.dart'; @docImport 'search_anchor.dart'; @docImport 'tabs.dart'; @docImport 'text_field.dart'; @docImport 'text_theme.dart'; @docImport 'theme_data.dart'; @docImport 'time_picker.dart'; @docImport 'user_accounts_drawer_header.dart';

# MaterialLocalizations

```dart
abstract class MaterialLocalizations {}
```

Defines the localized resource values used by the Material widgets.

See also:

- [DefaultMaterialLocalizations], the default, English-only, implementation of this interface.
- [GlobalMaterialLocalizations], which provides material localizations for many languages.

### openAppDrawerTooltip

```dart
String get openAppDrawerTooltip
```

The tooltip for the leading [AppBar] menu (a.k.a. 'hamburger') button.

### backButtonTooltip

```dart
String get backButtonTooltip
```

The [BackButton]'s tooltip.

### clearButtonTooltip

```dart
String get clearButtonTooltip
```

The tooltip for the clear button to clear text on [SearchAnchor]'s search view.

### closeButtonTooltip

```dart
String get closeButtonTooltip
```

The [CloseButton]'s tooltip.

### deleteButtonTooltip

```dart
String get deleteButtonTooltip
```

The tooltip for the delete button on a [Chip].

### moreButtonTooltip

```dart
String get moreButtonTooltip
```

The tooltip for the more button on an overflowing text selection menu.

### nextMonthTooltip

```dart
String get nextMonthTooltip
```

The tooltip for the [CalendarDatePicker]'s "next month" button.

### previousMonthTooltip

```dart
String get previousMonthTooltip
```

The tooltip for the [CalendarDatePicker]'s "previous month" button.

### firstPageTooltip

```dart
String get firstPageTooltip
```

The tooltip for the [PaginatedDataTable]'s "first page" button.

### lastPageTooltip

```dart
String get lastPageTooltip
```

The tooltip for the [PaginatedDataTable]'s "last page" button.

### nextPageTooltip

```dart
String get nextPageTooltip
```

The tooltip for the [PaginatedDataTable]'s "next page" button.

### previousPageTooltip

```dart
String get previousPageTooltip
```

The tooltip for the [PaginatedDataTable]'s "previous page" button.

### showMenuTooltip

```dart
String get showMenuTooltip
```

The default [PopupMenuButton] tooltip.

### aboutListTileTitle()

```dart
String aboutListTileTitle(String applicationName)
```

The default title for [AboutListTile].

### licensesPageTitle

```dart
String get licensesPageTitle
```

Title for the [LicensePage] widget.

### licensesPackageDetailText()

```dart
String licensesPackageDetailText(int licenseCount)
```

Subtitle for a package in the [LicensePage] widget.

### pageRowsInfoTitle()

```dart
String pageRowsInfoTitle(int firstRow, int lastRow, int rowCount, bool rowCountIsApproximate)
```

Title for the [PaginatedDataTable]'s row info footer.

### rowsPerPageTitle

```dart
String get rowsPerPageTitle
```

Title for the [PaginatedDataTable]'s "rows per page" footer.

### tabLabel()

```dart
String tabLabel({required int tabIndex, required int tabCount})
```

The accessibility label used on a tab in a [TabBar].

This message describes the index of the selected tab and how many tabs there are, e.g. 'Tab 1 of 2' in United States English.

`tabIndex` and `tabCount` must be greater than or equal to one.

### selectedRowCountTitle()

```dart
String selectedRowCountTitle(int selectedRowCount)
```

Title for the [PaginatedDataTable]'s selected row count header.

### cancelButtonLabel

```dart
String get cancelButtonLabel
```

Label for "cancel" buttons and menu items.

### closeButtonLabel

```dart
String get closeButtonLabel
```

Label for "close" buttons and menu items.

### continueButtonLabel

```dart
String get continueButtonLabel
```

Label for "continue" buttons and menu items.

### copyButtonLabel

```dart
String get copyButtonLabel
```

Label for "copy" edit buttons and menu items.

### cutButtonLabel

```dart
String get cutButtonLabel
```

Label for "cut" edit buttons and menu items.

### scanTextButtonLabel

```dart
String get scanTextButtonLabel
```

Label for "scan text" OCR edit buttons and menu items.

### okButtonLabel

```dart
String get okButtonLabel
```

Label for OK buttons and menu items.

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

Label for "paste" edit buttons and menu items.

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

Label for "select all" edit buttons and menu items.

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

Label for "look up" edit buttons and menu items.

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

Label for "search web" edit buttons and menu items.

### shareButtonLabel

```dart
String get shareButtonLabel
```

Label for "share" edit buttons and menu items.

### viewLicensesButtonLabel

```dart
String get viewLicensesButtonLabel
```

Label for the [AboutDialog] button that shows the [LicensePage].

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

### timePickerHourModeAnnouncement

```dart
String get timePickerHourModeAnnouncement
```

The text-to-speech announcement made when a time picker invoked using [showTimePicker] is set to the hour picker mode.

### timePickerMinuteModeAnnouncement

```dart
String get timePickerMinuteModeAnnouncement
```

The text-to-speech announcement made when a time picker invoked using [showTimePicker] is set to the minute picker mode.

### modalBarrierDismissLabel

```dart
String get modalBarrierDismissLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) for a modal barrier to indicate that a tap dismisses the barrier.

A modal barrier can for example be found behind an alert or popup to block user interaction with elements behind it.

### menuDismissLabel

```dart
String get menuDismissLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) for a context menu to indicate that a tap dismisses the context menu.

### drawerLabel

```dart
String get drawerLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) when a drawer widget is opened.

### popupMenuLabel

```dart
String get popupMenuLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) when a popup menu widget is opened.

### menuBarMenuLabel

```dart
String get menuBarMenuLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) when a MenuBarMenu widget is opened.

### dialogLabel

```dart
String get dialogLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) when a dialog widget is opened.

### alertDialogLabel

```dart
String get alertDialogLabel
```

Label read out by accessibility tools (TalkBack or VoiceOver) when an alert dialog widget is opened.

### searchFieldLabel

```dart
String get searchFieldLabel
```

Label indicating that a text field is a search field. This will be used as a hint text in the text field.

### currentDateLabel

```dart
String get currentDateLabel
```

Label indicating that a given date is the current date.

### selectedDateLabel

```dart
String get selectedDateLabel
```

The semantics label to describe the selected date in the calendar picker invoked using [showDatePicker].

### scrimLabel

```dart
String get scrimLabel
```

Label for the scrim rendered underneath a [BottomSheet].

### bottomSheetLabel

```dart
String get bottomSheetLabel
```

Label for a [BottomSheet], used as the `modalRouteContentName` of the [scrimOnTapHint].

### scrimOnTapHint()

```dart
String scrimOnTapHint(String modalRouteContentName)
```

Hint text announced when tapping on the scrim underneath the content of a modal route.

### timeOfDayFormat()

```dart
TimeOfDayFormat timeOfDayFormat({bool alwaysUse24HourFormat = false})
```

The format used to lay out the time picker.

The documentation for [TimeOfDayFormat] enum values provides details on each supported layout.

### scriptCategory

```dart
ScriptCategory get scriptCategory
```

Defines the localized [TextStyle] geometry for [ThemeData.textTheme].

The [scriptCategory] defines the overall geometry of a [TextTheme] for the [Typography.geometryThemeFor] method in terms of the three language categories defined in https://material.io/go/design-typography.

Generally speaking, font sizes for `ScriptCategory.tall` and `ScriptCategory.dense` scripts - for text styles that are smaller than the title style - are one unit larger than they are for `ScriptCategory.englishLike` scripts.

### formatDecimal()

```dart
String formatDecimal(int number)
```

Formats [number] as a decimal, inserting locale-appropriate thousands separators as necessary.

### formatHour()

```dart
String formatHour(TimeOfDay timeOfDay, {bool alwaysUse24HourFormat = false})
```

Formats [TimeOfDay.hour] in the given time of day according to the value of [timeOfDayFormat].

If [alwaysUse24HourFormat] is true, formats hour using [HourFormat.HH] rather than the default for the current locale.

### formatMinute()

```dart
String formatMinute(TimeOfDay timeOfDay)
```

Formats [TimeOfDay.minute] in the given time of day according to the value of [timeOfDayFormat].

### formatTimeOfDay()

```dart
String formatTimeOfDay(TimeOfDay timeOfDay, {bool alwaysUse24HourFormat = false})
```

Formats [timeOfDay] according to the value of [timeOfDayFormat].

If [alwaysUse24HourFormat] is true, formats hour using [HourFormat.HH] rather than the default for the current locale. This value is usually passed from [MediaQueryData.alwaysUse24HourFormat], which has platform- specific behavior.

### formatYear()

```dart
String formatYear(DateTime date)
```

Full unabbreviated year format, e.g. 2017 rather than 17.

### formatCompactDate()

```dart
String formatCompactDate(DateTime date)
```

Formats the date in a compact format.

Usually just the numeric values for the for day, month and year are used.

Examples:

- US English: 02/21/2019
- Russian: 21.02.2019

See also:

- [parseCompactDate], which will convert a compact date string to a [DateTime].

### formatShortDate()

```dart
String formatShortDate(DateTime date)
```

Formats the date using a short-width format.

Includes the abbreviation of the month, the day and year.

Examples:

- US English: Feb 21, 2019
- Russian: 21 февр. 2019 г.

### formatMediumDate()

```dart
String formatMediumDate(DateTime date)
```

Formats the date using a medium-width format.

Abbreviates month and days of week. This appears in the header of the date picker invoked using [showDatePicker].

Examples:

- US English: Wed, Sep 27
- Russian: ср, сент. 27

### formatFullDate()

```dart
String formatFullDate(DateTime date)
```

Formats day of week, month, day of month and year in a long-width format.

Does not abbreviate names. Appears in spoken announcements of the date picker invoked using [showDatePicker], when accessibility mode is on.

Examples:

- US English: Wednesday, September 27, 2017
- Russian: Среда, Сентябрь 27, 2017

### formatMonthYear()

```dart
String formatMonthYear(DateTime date)
```

Formats the month and the year of the given [date].

The returned string does not contain the day of the month. This appears in the date picker invoked using [showDatePicker].

### formatShortMonthDay()

```dart
String formatShortMonthDay(DateTime date)
```

Formats the month and day of the given [date].

Examples:

- US English: Feb 21
- Russian: 21 февр.

### parseCompactDate()

```dart
DateTime? parseCompactDate(String? inputString)
```

Converts the given compact date formatted string into a [DateTime].

The format of the string must be a valid compact date format for the given locale. If the text doesn't represent a valid date, `null` will be returned.

See also:

- [formatCompactDate], which will convert a [DateTime] into a string in the compact format.

### narrowWeekdays

```dart
List<String> get narrowWeekdays
```

List of week day names in narrow format, usually 1- or 2-letter abbreviations of full names.

The list begins with the value corresponding to Sunday and ends with Saturday. Use [firstDayOfWeekIndex] to find the first day of week in this list.

Examples:

- US English: S, M, T, W, T, F, S
- Russian: вс, пн, вт, ср, чт, пт, сб - notice that the list begins with вс (Sunday) even though the first day of week for Russian is Monday.

### firstDayOfWeekIndex

```dart
int get firstDayOfWeekIndex
```

Index of the first day of week, where 0 points to Sunday, and 6 points to Saturday.

This getter is compatible with [narrowWeekdays]. For example:

```dart
 MaterialLocalizations localizations = MaterialLocalizations.of(context);
// The name of the first day of week for the current locale.
String firstDayOfWeek = localizations.narrowWeekdays[localizations.firstDayOfWeekIndex];
```

### dateSeparator

```dart
String get dateSeparator
```

The character string used to separate the parts of a compact date format (i.e. mm/dd/yyyy has a separator of '/').

### dateHelpText

```dart
String get dateHelpText
```

The help text used on an empty [InputDatePickerFormField] to indicate to the user the date format being asked for.

### selectYearSemanticsLabel

```dart
String get selectYearSemanticsLabel
```

The semantic label used to announce when the user has entered the year selection mode of the [CalendarDatePicker] which is used in the data picker dialog created with [showDatePicker].

### unspecifiedDate

```dart
String get unspecifiedDate
```

The label used to indicate a date that has not been entered or selected yet in the date picker.

### unspecifiedDateRange

```dart
String get unspecifiedDateRange
```

The label used to indicate a date range that has not been entered or selected yet in the date range picker.

### dateInputLabel

```dart
String get dateInputLabel
```

The label used to describe the text field used in an [InputDatePickerFormField].

### dateRangeStartLabel

```dart
String get dateRangeStartLabel
```

The label used for the starting date input field in the date range picker created with [showDateRangePicker].

### dateRangeEndLabel

```dart
String get dateRangeEndLabel
```

The label used for the ending date input field in the date range picker created with [showDateRangePicker].

### dateRangeStartDateSemanticLabel()

```dart
String dateRangeStartDateSemanticLabel(String formattedDate)
```

The semantics label used for the selected start date in the date range picker's day grid.

### dateRangeEndDateSemanticLabel()

```dart
String dateRangeEndDateSemanticLabel(String formattedDate)
```

The semantics label used for the selected end date in the date range picker's day grid.

### invalidDateFormatLabel

```dart
String get invalidDateFormatLabel
```

Error message displayed to the user when they have entered a text string in an [InputDatePickerFormField] that is not in a valid date format.

### invalidDateRangeLabel

```dart
String get invalidDateRangeLabel
```

Error message displayed to the user when they have entered an invalid date range in the input mode of the date range picker created with [showDateRangePicker].

### dateOutOfRangeLabel

```dart
String get dateOutOfRangeLabel
```

Error message displayed to the user when they have entered a date that is outside the valid range for the date picker. [showDateRangePicker].

### saveButtonLabel

```dart
String get saveButtonLabel
```

Label for a 'SAVE' button. Currently used by the full screen mode of the date range picker.

### datePickerHelpText

```dart
String get datePickerHelpText
```

Label used in the header of the date picker dialog created with [showDatePicker].

### dateRangePickerHelpText

```dart
String get dateRangePickerHelpText
```

Label used in the header of the date range picker dialog created with [showDateRangePicker].

### calendarModeButtonLabel

```dart
String get calendarModeButtonLabel
```

Tooltip used for the calendar mode button of the date pickers.

### inputDateModeButtonLabel

```dart
String get inputDateModeButtonLabel
```

Tooltip used for the text input mode button of the date pickers.

### timePickerDialHelpText

```dart
String get timePickerDialHelpText
```

Label used in the header of the time picker dialog created with [showTimePicker] when in [TimePickerEntryMode.dial].

### timePickerInputHelpText

```dart
String get timePickerInputHelpText
```

Label used in the header of the time picker dialog created with [showTimePicker] when in [TimePickerEntryMode.input].

### timePickerHourLabel

```dart
String get timePickerHourLabel
```

Label used below the hour text field of the time picker dialog created with [showTimePicker] when in [TimePickerEntryMode.input].

### timePickerMinuteLabel

```dart
String get timePickerMinuteLabel
```

Label used below the minute text field of the time picker dialog created with [showTimePicker] when in [TimePickerEntryMode.input].

### invalidTimeLabel

```dart
String get invalidTimeLabel
```

Error message for the time picker dialog created with [showTimePicker] when in [TimePickerEntryMode.input].

### dialModeButtonLabel

```dart
String get dialModeButtonLabel
```

Tooltip used to put the time picker into [TimePickerEntryMode.dial].

### inputTimeModeButtonLabel

```dart
String get inputTimeModeButtonLabel
```

Tooltip used to put the time picker into [TimePickerEntryMode.input].

### signedInLabel

```dart
String get signedInLabel
```

The semantics label used to indicate which account is signed in the [UserAccountsDrawerHeader] widget.

### hideAccountsLabel

```dart
String get hideAccountsLabel
```

The semantics label used for the button on [UserAccountsDrawerHeader] that hides the list of accounts.

### showAccountsLabel

```dart
String get showAccountsLabel
```

The semantics label used for the button on [UserAccountsDrawerHeader] that shows the list of accounts.

### reorderItemToStart

```dart
String get reorderItemToStart
```

The semantics label used for [ReorderableListView] to reorder an item in the list to the start of the list.

### reorderItemToEnd

```dart
String get reorderItemToEnd
```

The semantics label used for [ReorderableListView] to reorder an item in the list to the end of the list.

### reorderItemUp

```dart
String get reorderItemUp
```

The semantics label used for [ReorderableListView] to reorder an item in the list one space up the list.

### reorderItemDown

```dart
String get reorderItemDown
```

The semantics label used for [ReorderableListView] to reorder an item in the list one space down the list.

### reorderItemLeft

```dart
String get reorderItemLeft
```

The semantics label used for [ReorderableListView] to reorder an item in the list one space left in the list.

### reorderItemRight

```dart
String get reorderItemRight
```

The semantics label used for [ReorderableListView] to reorder an item in the list one space right in the list.

### expandedIconTapHint

```dart
String get expandedIconTapHint
```

The semantics hint to describe the tap action on an expanded [ExpandIcon].

### collapsedIconTapHint

```dart
String get collapsedIconTapHint
```

The semantics hint to describe the tap action on a collapsed [ExpandIcon].

### expansionTileExpandedHint

```dart
String get expansionTileExpandedHint
```

The semantics hint to describe the tap action on an expanded [ExpansionTile] on iOS and macOS. This is appended to the [collapsedHint] hint to provide a more detailed description of the action, e.g. "Expanded double tap to collapse".

### expansionTileCollapsedHint

```dart
String get expansionTileCollapsedHint
```

The semantics hint to describe the tap action on a collapsed [ExpansionTile] on iOS and macOS. This is appended to the [expandedHint] hint to provide a more detailed description of the action, e.g. "Collapsed double tap to expand".

### expansionTileExpandedTapHint

```dart
String get expansionTileExpandedTapHint
```

The semantics hint to describe the tap action on an expanded [ExpansionTile].

### expansionTileCollapsedTapHint

```dart
String get expansionTileCollapsedTapHint
```

The semantics hint to describe the tap action on a collapsed [ExpansionTile].

### expandedHint

```dart
String get expandedHint
```

The semantics hint to describe the [ExpansionTile] expanded state.

### collapsedHint

```dart
String get collapsedHint
```

The semantics hint to describe the [ExpansionTile] collapsed state.

### remainingTextFieldCharacterCount()

```dart
String remainingTextFieldCharacterCount(int remaining)
```

The label for the [TextField]'s character counter.

### refreshIndicatorSemanticLabel

```dart
String get refreshIndicatorSemanticLabel
```

The default semantics label for a [RefreshIndicator].

### keyboardKeyAlt

```dart
String get keyboardKeyAlt
```

The shortcut label for the keyboard key [LogicalKeyboardKey.alt].

### keyboardKeyAltGraph

```dart
String get keyboardKeyAltGraph
```

The shortcut label for the keyboard key [LogicalKeyboardKey.altGraph].

### keyboardKeyBackspace

```dart
String get keyboardKeyBackspace
```

The shortcut label for the keyboard key [LogicalKeyboardKey.backspace].

### keyboardKeyCapsLock

```dart
String get keyboardKeyCapsLock
```

The shortcut label for the keyboard key [LogicalKeyboardKey.capsLock].

### keyboardKeyChannelDown

```dart
String get keyboardKeyChannelDown
```

The shortcut label for the keyboard key [LogicalKeyboardKey.channelDown].

### keyboardKeyChannelUp

```dart
String get keyboardKeyChannelUp
```

The shortcut label for the keyboard key [LogicalKeyboardKey.channelUp].

### keyboardKeyControl

```dart
String get keyboardKeyControl
```

The shortcut label for the keyboard key [LogicalKeyboardKey.control].

### keyboardKeyDelete

```dart
String get keyboardKeyDelete
```

The shortcut label for the keyboard key [LogicalKeyboardKey.delete].

### keyboardKeyEject

```dart
String get keyboardKeyEject
```

The shortcut label for the keyboard key [LogicalKeyboardKey.eject].

### keyboardKeyEnd

```dart
String get keyboardKeyEnd
```

The shortcut label for the keyboard key [LogicalKeyboardKey.end].

### keyboardKeyEscape

```dart
String get keyboardKeyEscape
```

The shortcut label for the keyboard key [LogicalKeyboardKey.escape].

### keyboardKeyFn

```dart
String get keyboardKeyFn
```

The shortcut label for the keyboard key [LogicalKeyboardKey.fn].

### keyboardKeyHome

```dart
String get keyboardKeyHome
```

The shortcut label for the keyboard key [LogicalKeyboardKey.home].

### keyboardKeyInsert

```dart
String get keyboardKeyInsert
```

The shortcut label for the keyboard key [LogicalKeyboardKey.insert].

### keyboardKeyMeta

```dart
String get keyboardKeyMeta
```

The shortcut label for the keyboard key [LogicalKeyboardKey.meta].

### keyboardKeyMetaMacOs

```dart
String get keyboardKeyMetaMacOs
```

The shortcut label for the keyboard key [LogicalKeyboardKey.meta] on macOS.

### keyboardKeyMetaWindows

```dart
String get keyboardKeyMetaWindows
```

The shortcut label for the keyboard key [LogicalKeyboardKey.meta] on Windows.

### keyboardKeyNumLock

```dart
String get keyboardKeyNumLock
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numLock].

### keyboardKeyNumpad1

```dart
String get keyboardKeyNumpad1
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad1].

### keyboardKeyNumpad2

```dart
String get keyboardKeyNumpad2
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad2].

### keyboardKeyNumpad3

```dart
String get keyboardKeyNumpad3
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad3].

### keyboardKeyNumpad4

```dart
String get keyboardKeyNumpad4
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad4].

### keyboardKeyNumpad5

```dart
String get keyboardKeyNumpad5
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad5].

### keyboardKeyNumpad6

```dart
String get keyboardKeyNumpad6
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad6].

### keyboardKeyNumpad7

```dart
String get keyboardKeyNumpad7
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad7].

### keyboardKeyNumpad8

```dart
String get keyboardKeyNumpad8
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad8].

### keyboardKeyNumpad9

```dart
String get keyboardKeyNumpad9
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad9].

### keyboardKeyNumpad0

```dart
String get keyboardKeyNumpad0
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpad0].

### keyboardKeyNumpadAdd

```dart
String get keyboardKeyNumpadAdd
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadAdd].

### keyboardKeyNumpadComma

```dart
String get keyboardKeyNumpadComma
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadComma].

### keyboardKeyNumpadDecimal

```dart
String get keyboardKeyNumpadDecimal
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadDecimal].

### keyboardKeyNumpadDivide

```dart
String get keyboardKeyNumpadDivide
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadDivide].

### keyboardKeyNumpadEnter

```dart
String get keyboardKeyNumpadEnter
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadEnter].

### keyboardKeyNumpadEqual

```dart
String get keyboardKeyNumpadEqual
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadEqual].

### keyboardKeyNumpadMultiply

```dart
String get keyboardKeyNumpadMultiply
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadMultiply].

### keyboardKeyNumpadParenLeft

```dart
String get keyboardKeyNumpadParenLeft
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadParenLeft].

### keyboardKeyNumpadParenRight

```dart
String get keyboardKeyNumpadParenRight
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadParenRight].

### keyboardKeyNumpadSubtract

```dart
String get keyboardKeyNumpadSubtract
```

The shortcut label for the keyboard key [LogicalKeyboardKey.numpadSubtract].

### keyboardKeyPageDown

```dart
String get keyboardKeyPageDown
```

The shortcut label for the keyboard key [LogicalKeyboardKey.pageDown].

### keyboardKeyPageUp

```dart
String get keyboardKeyPageUp
```

The shortcut label for the keyboard key [LogicalKeyboardKey.pageUp].

### keyboardKeyPower

```dart
String get keyboardKeyPower
```

The shortcut label for the keyboard key [LogicalKeyboardKey.power].

### keyboardKeyPowerOff

```dart
String get keyboardKeyPowerOff
```

The shortcut label for the keyboard key [LogicalKeyboardKey.powerOff].

### keyboardKeyPrintScreen

```dart
String get keyboardKeyPrintScreen
```

The shortcut label for the keyboard key [LogicalKeyboardKey.printScreen].

### keyboardKeyScrollLock

```dart
String get keyboardKeyScrollLock
```

The shortcut label for the keyboard key [LogicalKeyboardKey.scrollLock].

### keyboardKeySelect

```dart
String get keyboardKeySelect
```

The shortcut label for the keyboard key [LogicalKeyboardKey.select].

### keyboardKeyShift

```dart
String get keyboardKeyShift
```

The shortcut label for the keyboard key [LogicalKeyboardKey.shift].

### keyboardKeySpace

```dart
String get keyboardKeySpace
```

The shortcut label for the keyboard key [LogicalKeyboardKey.space].

### of()

```dart
MaterialLocalizations of(BuildContext context)
```

The `MaterialLocalizations` from the closest [Localizations] instance that encloses the given context.

If no [MaterialLocalizations] are available in the given `context`, this method throws an exception.

This method is just a convenient shorthand for: `Localizations.of<MaterialLocalizations>(context, MaterialLocalizations)!`.

References to the localized resources defined by this class are typically written in terms of this method. For example:

```dart
tooltip: MaterialLocalizations.of(context).backButtonTooltip,
```

# DefaultMaterialLocalizations

```dart
class DefaultMaterialLocalizations implements MaterialLocalizations {}
```

US English strings for the material widgets.

See also:

- [GlobalMaterialLocalizations], which provides material localizations for many languages.
- [MaterialApp.localizationsDelegates], which automatically includes [DefaultMaterialLocalizations.delegate] by default.

### DefaultMaterialLocalizations()

```dart
DefaultMaterialLocalizations()
```

Constructs an object that defines the material widgets' localized strings for US English (only).

[LocalizationsDelegate] implementations typically call the static [load] function, rather than constructing this class directly.

### formatHour()

```dart
String formatHour(TimeOfDay timeOfDay, {bool alwaysUse24HourFormat = false})
```

### formatMinute()

```dart
String formatMinute(TimeOfDay timeOfDay)
```

### formatYear()

```dart
String formatYear(DateTime date)
```

### formatCompactDate()

```dart
String formatCompactDate(DateTime date)
```

### formatShortDate()

```dart
String formatShortDate(DateTime date)
```

### formatMediumDate()

```dart
String formatMediumDate(DateTime date)
```

### formatFullDate()

```dart
String formatFullDate(DateTime date)
```

### formatMonthYear()

```dart
String formatMonthYear(DateTime date)
```

### formatShortMonthDay()

```dart
String formatShortMonthDay(DateTime date)
```

### parseCompactDate()

```dart
DateTime? parseCompactDate(String? inputString)
```

### narrowWeekdays

```dart
List<String> get narrowWeekdays
```

### firstDayOfWeekIndex

```dart
int get firstDayOfWeekIndex
```

### dateSeparator

```dart
String get dateSeparator
```

### dateHelpText

```dart
String get dateHelpText
```

### selectYearSemanticsLabel

```dart
String get selectYearSemanticsLabel
```

### unspecifiedDate

```dart
String get unspecifiedDate
```

### unspecifiedDateRange

```dart
String get unspecifiedDateRange
```

### dateInputLabel

```dart
String get dateInputLabel
```

### dateRangeStartLabel

```dart
String get dateRangeStartLabel
```

### dateRangeEndLabel

```dart
String get dateRangeEndLabel
```

### dateRangeStartDateSemanticLabel()

```dart
String dateRangeStartDateSemanticLabel(String formattedDate)
```

### dateRangeEndDateSemanticLabel()

```dart
String dateRangeEndDateSemanticLabel(String formattedDate)
```

### invalidDateFormatLabel

```dart
String get invalidDateFormatLabel
```

### invalidDateRangeLabel

```dart
String get invalidDateRangeLabel
```

### dateOutOfRangeLabel

```dart
String get dateOutOfRangeLabel
```

### saveButtonLabel

```dart
String get saveButtonLabel
```

### datePickerHelpText

```dart
String get datePickerHelpText
```

### dateRangePickerHelpText

```dart
String get dateRangePickerHelpText
```

### calendarModeButtonLabel

```dart
String get calendarModeButtonLabel
```

### inputDateModeButtonLabel

```dart
String get inputDateModeButtonLabel
```

### timePickerDialHelpText

```dart
String get timePickerDialHelpText
```

### timePickerInputHelpText

```dart
String get timePickerInputHelpText
```

### timePickerHourLabel

```dart
String get timePickerHourLabel
```

### timePickerMinuteLabel

```dart
String get timePickerMinuteLabel
```

### invalidTimeLabel

```dart
String get invalidTimeLabel
```

### dialModeButtonLabel

```dart
String get dialModeButtonLabel
```

### inputTimeModeButtonLabel

```dart
String get inputTimeModeButtonLabel
```

### formatDecimal()

```dart
String formatDecimal(int number)
```

### formatTimeOfDay()

```dart
String formatTimeOfDay(TimeOfDay timeOfDay, {bool alwaysUse24HourFormat = false})
```

### openAppDrawerTooltip

```dart
String get openAppDrawerTooltip
```

### backButtonTooltip

```dart
String get backButtonTooltip
```

### clearButtonTooltip

```dart
String get clearButtonTooltip
```

### closeButtonTooltip

```dart
String get closeButtonTooltip
```

### deleteButtonTooltip

```dart
String get deleteButtonTooltip
```

### moreButtonTooltip

```dart
String get moreButtonTooltip
```

### nextMonthTooltip

```dart
String get nextMonthTooltip
```

### previousMonthTooltip

```dart
String get previousMonthTooltip
```

### nextPageTooltip

```dart
String get nextPageTooltip
```

### previousPageTooltip

```dart
String get previousPageTooltip
```

### firstPageTooltip

```dart
String get firstPageTooltip
```

### lastPageTooltip

```dart
String get lastPageTooltip
```

### showMenuTooltip

```dart
String get showMenuTooltip
```

### drawerLabel

```dart
String get drawerLabel
```

### menuBarMenuLabel

```dart
String get menuBarMenuLabel
```

### popupMenuLabel

```dart
String get popupMenuLabel
```

### dialogLabel

```dart
String get dialogLabel
```

### alertDialogLabel

```dart
String get alertDialogLabel
```

### searchFieldLabel

```dart
String get searchFieldLabel
```

### currentDateLabel

```dart
String get currentDateLabel
```

### selectedDateLabel

```dart
String get selectedDateLabel
```

### scrimLabel

```dart
String get scrimLabel
```

### bottomSheetLabel

```dart
String get bottomSheetLabel
```

### scrimOnTapHint()

```dart
String scrimOnTapHint(String modalRouteContentName)
```

### aboutListTileTitle()

```dart
String aboutListTileTitle(String applicationName)
```

### licensesPageTitle

```dart
String get licensesPageTitle
```

### licensesPackageDetailText()

```dart
String licensesPackageDetailText(int licenseCount)
```

### pageRowsInfoTitle()

```dart
String pageRowsInfoTitle(int firstRow, int lastRow, int rowCount, bool rowCountIsApproximate)
```

### rowsPerPageTitle

```dart
String get rowsPerPageTitle
```

### tabLabel()

```dart
String tabLabel({required int tabIndex, required int tabCount})
```

### selectedRowCountTitle()

```dart
String selectedRowCountTitle(int selectedRowCount)
```

### cancelButtonLabel

```dart
String get cancelButtonLabel
```

### closeButtonLabel

```dart
String get closeButtonLabel
```

### continueButtonLabel

```dart
String get continueButtonLabel
```

### copyButtonLabel

```dart
String get copyButtonLabel
```

### cutButtonLabel

```dart
String get cutButtonLabel
```

### scanTextButtonLabel

```dart
String get scanTextButtonLabel
```

### okButtonLabel

```dart
String get okButtonLabel
```

### pasteButtonLabel

```dart
String get pasteButtonLabel
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

### viewLicensesButtonLabel

```dart
String get viewLicensesButtonLabel
```

### anteMeridiemAbbreviation

```dart
String get anteMeridiemAbbreviation
```

### postMeridiemAbbreviation

```dart
String get postMeridiemAbbreviation
```

### timePickerHourModeAnnouncement

```dart
String get timePickerHourModeAnnouncement
```

### timePickerMinuteModeAnnouncement

```dart
String get timePickerMinuteModeAnnouncement
```

### modalBarrierDismissLabel

```dart
String get modalBarrierDismissLabel
```

### menuDismissLabel

```dart
String get menuDismissLabel
```

### scriptCategory

```dart
ScriptCategory get scriptCategory
```

### timeOfDayFormat()

```dart
TimeOfDayFormat timeOfDayFormat({bool alwaysUse24HourFormat = false})
```

### signedInLabel

```dart
String get signedInLabel
```

### hideAccountsLabel

```dart
String get hideAccountsLabel
```

### showAccountsLabel

```dart
String get showAccountsLabel
```

### reorderItemUp

```dart
String get reorderItemUp
```

### reorderItemDown

```dart
String get reorderItemDown
```

### reorderItemLeft

```dart
String get reorderItemLeft
```

### reorderItemRight

```dart
String get reorderItemRight
```

### reorderItemToEnd

```dart
String get reorderItemToEnd
```

### reorderItemToStart

```dart
String get reorderItemToStart
```

### expandedIconTapHint

```dart
String get expandedIconTapHint
```

### collapsedIconTapHint

```dart
String get collapsedIconTapHint
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

### refreshIndicatorSemanticLabel

```dart
String get refreshIndicatorSemanticLabel
```

### load()

```dart
Future<MaterialLocalizations> load(Locale locale)
```

Creates an object that provides US English resource values for the material library widgets.

The [locale] parameter is ignored.

This method is typically used to create a [LocalizationsDelegate]. The [MaterialApp] does so by default.

### delegate

```dart
LocalizationsDelegate<MaterialLocalizations> delegate
```

A [LocalizationsDelegate] that uses [DefaultMaterialLocalizations.load] to create an instance of this class.

[MaterialApp] automatically adds this value to [MaterialApp.localizationsDelegates].

### remainingTextFieldCharacterCount()

```dart
String remainingTextFieldCharacterCount(int remaining)
```

### keyboardKeyAlt

```dart
String get keyboardKeyAlt
```

### keyboardKeyAltGraph

```dart
String get keyboardKeyAltGraph
```

### keyboardKeyBackspace

```dart
String get keyboardKeyBackspace
```

### keyboardKeyCapsLock

```dart
String get keyboardKeyCapsLock
```

### keyboardKeyChannelDown

```dart
String get keyboardKeyChannelDown
```

### keyboardKeyChannelUp

```dart
String get keyboardKeyChannelUp
```

### keyboardKeyControl

```dart
String get keyboardKeyControl
```

### keyboardKeyDelete

```dart
String get keyboardKeyDelete
```

### keyboardKeyEject

```dart
String get keyboardKeyEject
```

### keyboardKeyEnd

```dart
String get keyboardKeyEnd
```

### keyboardKeyEscape

```dart
String get keyboardKeyEscape
```

### keyboardKeyFn

```dart
String get keyboardKeyFn
```

### keyboardKeyHome

```dart
String get keyboardKeyHome
```

### keyboardKeyInsert

```dart
String get keyboardKeyInsert
```

### keyboardKeyMeta

```dart
String get keyboardKeyMeta
```

### keyboardKeyMetaMacOs

```dart
String get keyboardKeyMetaMacOs
```

### keyboardKeyMetaWindows

```dart
String get keyboardKeyMetaWindows
```

### keyboardKeyNumLock

```dart
String get keyboardKeyNumLock
```

### keyboardKeyNumpad1

```dart
String get keyboardKeyNumpad1
```

### keyboardKeyNumpad2

```dart
String get keyboardKeyNumpad2
```

### keyboardKeyNumpad3

```dart
String get keyboardKeyNumpad3
```

### keyboardKeyNumpad4

```dart
String get keyboardKeyNumpad4
```

### keyboardKeyNumpad5

```dart
String get keyboardKeyNumpad5
```

### keyboardKeyNumpad6

```dart
String get keyboardKeyNumpad6
```

### keyboardKeyNumpad7

```dart
String get keyboardKeyNumpad7
```

### keyboardKeyNumpad8

```dart
String get keyboardKeyNumpad8
```

### keyboardKeyNumpad9

```dart
String get keyboardKeyNumpad9
```

### keyboardKeyNumpad0

```dart
String get keyboardKeyNumpad0
```

### keyboardKeyNumpadAdd

```dart
String get keyboardKeyNumpadAdd
```

### keyboardKeyNumpadComma

```dart
String get keyboardKeyNumpadComma
```

### keyboardKeyNumpadDecimal

```dart
String get keyboardKeyNumpadDecimal
```

### keyboardKeyNumpadDivide

```dart
String get keyboardKeyNumpadDivide
```

### keyboardKeyNumpadEnter

```dart
String get keyboardKeyNumpadEnter
```

### keyboardKeyNumpadEqual

```dart
String get keyboardKeyNumpadEqual
```

### keyboardKeyNumpadMultiply

```dart
String get keyboardKeyNumpadMultiply
```

### keyboardKeyNumpadParenLeft

```dart
String get keyboardKeyNumpadParenLeft
```

### keyboardKeyNumpadParenRight

```dart
String get keyboardKeyNumpadParenRight
```

### keyboardKeyNumpadSubtract

```dart
String get keyboardKeyNumpadSubtract
```

### keyboardKeyPageDown

```dart
String get keyboardKeyPageDown
```

### keyboardKeyPageUp

```dart
String get keyboardKeyPageUp
```

### keyboardKeyPower

```dart
String get keyboardKeyPower
```

### keyboardKeyPowerOff

```dart
String get keyboardKeyPowerOff
```

### keyboardKeyPrintScreen

```dart
String get keyboardKeyPrintScreen
```

### keyboardKeyScrollLock

```dart
String get keyboardKeyScrollLock
```

### keyboardKeySelect

```dart
String get keyboardKeySelect
```

### keyboardKeyShift

```dart
String get keyboardKeyShift
```

### keyboardKeySpace

```dart
String get keyboardKeySpace
```
