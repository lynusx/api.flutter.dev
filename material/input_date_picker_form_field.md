@docImport 'date_picker.dart'; @docImport 'text_field.dart';

# InputDatePickerFormField

```dart
class InputDatePickerFormField extends StatefulWidget {}
```

A [TextFormField] configured to accept and validate a date entered by a user.

When the field is saved or submitted, the text will be parsed into a [DateTime] according to the ambient locale's compact date format. If the input text doesn't parse into a date, the [errorFormatText] message will be displayed under the field.

[firstDate], [lastDate], and [selectableDayPredicate] provide constraints on what days are valid. If the input date isn't in the date range or doesn't pass the given predicate, then the [errorInvalidText] message will be displayed under the field.

See also:

- [showDatePicker], which shows a dialog that contains a Material Design date picker which includes support for text entry of dates.
- [MaterialLocalizations.parseCompactDate], which is used to parse the text input into a [DateTime].

### InputDatePickerFormField()

```dart
InputDatePickerFormField({dynamic key, DateTime? initialDate, required DateTime firstDate, required DateTime lastDate, ValueChanged<DateTime>? onDateSubmitted, ValueChanged<DateTime>? onDateSaved, SelectableDayPredicate? selectableDayPredicate, String? errorFormatText, String? errorInvalidText, String? fieldHintText, String? fieldLabelText, TextInputType? keyboardType, bool autofocus = false, bool acceptEmptyDate = false, FocusNode? focusNode, CalendarDelegate<DateTime> calendarDelegate = const GregorianCalendarDelegate()})
```

Creates a [TextFormField] configured to accept and validate a date.

If the optional [initialDate] is provided, then it will be used to populate the text field. If the [fieldHintText] is provided, it will be shown.

If [initialDate] is provided, it must not be before [firstDate] or after [lastDate]. If [selectableDayPredicate] is provided, it must return `true` for [initialDate].

[firstDate] must be on or before [lastDate].

### initialDate

```dart
DateTime? initialDate
```

If provided, it will be used as the default value of the field.

### firstDate

```dart
DateTime firstDate
```

The earliest allowable [DateTime] that the user can input.

### lastDate

```dart
DateTime lastDate
```

The latest allowable [DateTime] that the user can input.

### onDateSubmitted

```dart
ValueChanged<DateTime>? onDateSubmitted
```

An optional method to call when the user indicates they are done editing the text in the field. Will only be called if the input represents a valid [DateTime].

### onDateSaved

```dart
ValueChanged<DateTime>? onDateSaved
```

An optional method to call with the final date when the form is saved via [FormState.save]. Will only be called if the input represents a valid [DateTime].

### selectableDayPredicate

```dart
SelectableDayPredicate? selectableDayPredicate
```

Function to provide full control over which [DateTime] can be selected.

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

The keyboard type of the [TextField].

If this is null, it will default to [TextInputType.datetime]

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.editableText.autofocus}

### acceptEmptyDate

```dart
bool acceptEmptyDate
```

Determines if an empty date would show [errorFormatText] or not.

Defaults to false.

If true, [errorFormatText] is not shown when the date input field is empty.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### calendarDelegate

```dart
CalendarDelegate<DateTime> calendarDelegate
```

{@macro flutter.material.calendar_date_picker.calendarDelegate}

### createState()

```dart
State<InputDatePickerFormField> createState()
```
