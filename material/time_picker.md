@docImport 'date_picker.dart'; @docImport 'text_field.dart';

# TimePickerEntryMode

```dart
enum TimePickerEntryMode {}
```

Interactive input mode of the time picker dialog.

In [TimePickerEntryMode.dial] mode, a clock dial is displayed and the user taps or drags the time they wish to select. In TimePickerEntryMode.input] mode, [TextField]s are displayed and the user types in the time they wish to select.

See also:

- [showTimePicker], a function that shows a [TimePickerDialog] and returns the selected time as a [Future].

User picks time from a clock dial.

Can switch to [input] by activating a mode button in the dialog.

User can input the time by typing it into text fields.

Can switch to [dial] by activating a mode button in the dialog.

User can only pick time from a clock dial.

There is no user interface to switch to another mode.

User can only input the time by typing it into text fields.

There is no user interface to switch to another mode.

# EntryModeChangeCallback

```dart
typedef EntryModeChangeCallback = void Function(TimePickerEntryMode mode)
```

Signature for when the time picker entry mode is changed.

# TimePickerDialog

```dart
class TimePickerDialog extends StatefulWidget {}
```

A Material Design time picker designed to appear inside a popup dialog.

Pass this widget to [showDialog]. The value returned by [showDialog] is the selected [TimeOfDay] if the user taps the "OK" button, or null if the user taps the "CANCEL" button. The selected time is reported by calling [Navigator.pop].

Use [showTimePicker] to show a dialog already containing a [TimePickerDialog].

### TimePickerDialog()

```dart
TimePickerDialog({dynamic key, required TimeOfDay initialTime, String? cancelText, String? confirmText, String? helpText, String? errorInvalidText, String? hourLabelText, String? minuteLabelText, String? restorationId, TimePickerEntryMode initialEntryMode = TimePickerEntryMode.dial, Orientation? orientation, EntryModeChangeCallback? onEntryModeChanged, Icon? switchToInputEntryModeIcon, Icon? switchToTimerEntryModeIcon, bool emptyInitialInput = false})
```

Creates a Material Design time picker.

### initialTime

```dart
TimeOfDay initialTime
```

The time initially selected when the dialog is shown.

### cancelText

```dart
String? cancelText
```

Optionally provide your own text for the cancel button.

If null, the button uses [MaterialLocalizations.cancelButtonLabel].

### confirmText

```dart
String? confirmText
```

Optionally provide your own text for the confirm button.

If null, the button uses [MaterialLocalizations.okButtonLabel].

### helpText

```dart
String? helpText
```

Optionally provide your own help text to the header of the time picker.

### errorInvalidText

```dart
String? errorInvalidText
```

Optionally provide your own validation error text.

### hourLabelText

```dart
String? hourLabelText
```

Optionally provide your own hour label text.

### minuteLabelText

```dart
String? minuteLabelText
```

Optionally provide your own minute label text.

### restorationId

```dart
String? restorationId
```

Restoration ID to save and restore the state of the [TimePickerDialog].

If it is non-null, the time picker will persist and restore the dialog's state.

The state of this widget is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### initialEntryMode

```dart
TimePickerEntryMode initialEntryMode
```

The entry mode for the picker. Whether it's text input or a dial.

### orientation

```dart
Orientation? orientation
```

The optional [orientation] parameter sets the [Orientation] to use when displaying the dialog.

By default, the orientation is derived from the [MediaQueryData.size] of the ambient [MediaQuery]. If the aspect of the size is tall, then [Orientation.portrait] is used, if the size is wide, then [Orientation.landscape] is used.

Use this parameter to override the default and force the dialog to appear in either portrait or landscape mode regardless of the aspect of the [MediaQueryData.size].

### onEntryModeChanged

```dart
EntryModeChangeCallback? onEntryModeChanged
```

Callback called when the selected entry mode is changed.

### switchToInputEntryModeIcon

```dart
Icon? switchToInputEntryModeIcon
```

{@macro flutter.material.time_picker.switchToInputEntryModeIcon}

### switchToTimerEntryModeIcon

```dart
Icon? switchToTimerEntryModeIcon
```

{@macro flutter.material.time_picker.switchToTimerEntryModeIcon}

### emptyInitialInput

```dart
bool emptyInitialInput
```

If true and entry mode is [TimePickerEntryMode.input], the hour and minute fields will be empty on start instead of pre-filled with [initialTime].

Has no effect in dial mode.

### createState()

```dart
State<TimePickerDialog> createState()
```

# showTimePicker()

```dart
Future<TimeOfDay?> showTimePicker({required BuildContext context, required TimeOfDay initialTime, TransitionBuilder? builder, bool barrierDismissible = true, Color? barrierColor, String? barrierLabel, bool useRootNavigator = true, TimePickerEntryMode initialEntryMode = TimePickerEntryMode.dial, String? cancelText, String? confirmText, String? helpText, String? errorInvalidText, String? hourLabelText, String? minuteLabelText, RouteSettings? routeSettings, EntryModeChangeCallback? onEntryModeChanged, Offset? anchorPoint, Orientation? orientation, Icon? switchToInputEntryModeIcon, Icon? switchToTimerEntryModeIcon, bool emptyInitialInput = false})
```

Shows a dialog containing a Material Design time picker.

The returned Future resolves to the time selected by the user when the user closes the dialog. If the user cancels the dialog, null is returned.

{@tool snippet} Show a dialog with [initialTime] equal to the current time.

```dart
Future<TimeOfDay?> selectedTime = showTimePicker(
  initialTime: TimeOfDay.now(),
  context: context,
);
```

{@end-tool}

The [context], [barrierDismissible], [barrierColor], [barrierLabel], [useRootNavigator] and [routeSettings] arguments are passed to [showDialog], the documentation for which discusses how it is used.

The [builder] parameter can be used to wrap the dialog widget to add inherited widgets like [Localizations.override], [Directionality], or [MediaQuery].

The `initialEntryMode` parameter can be used to determine the initial time entry selection of the picker (either a clock dial or text input).

Optional strings for the [helpText], [cancelText], [errorInvalidText], [hourLabelText], [minuteLabelText] and [confirmText] can be provided to override the default values.

The optional [orientation] parameter sets the [Orientation] to use when displaying the dialog. By default, the orientation is derived from the [MediaQueryData.size] of the ambient [MediaQuery]: wide sizes use the landscape orientation, and tall sizes use the portrait orientation. Use this parameter to override the default and force the dialog to appear in either portrait or landscape mode.

{@template flutter.material.time_picker.switchToInputEntryModeIcon} The optional [switchToInputEntryModeIcon] argument can be used to customize the input method icon that is shown when the [TimePickerEntryMode] is [TimePickerEntryMode.dial].

Defaults to an [Icon] widget with [Icons.keyboard_outlined] as icon. {@endtemplate}

{@template flutter.material.time_picker.switchToTimerEntryModeIcon} The optional [switchToTimerEntryModeIcon] argument can be used to customize the input method icon that is shown when the [TimePickerEntryMode] is [TimePickerEntryMode.input].

Defaults to an [Icon] widget with [Icons.access_time] as icon. {@endtemplate}

{@macro flutter.widgets.RawDialogRoute}

By default, the time picker gets its colors from the overall theme's [ColorScheme]. The time picker can be further customized by providing a [TimePickerThemeData] to the overall theme.

{@tool snippet} Show a dialog with the text direction overridden to be [TextDirection.rtl].

```dart
Future<TimeOfDay?> selectedTimeRTL = showTimePicker(
  context: context,
  initialTime: TimeOfDay.now(),
  builder: (BuildContext context, Widget? child) {
    return Directionality(
      textDirection: TextDirection.rtl,
      child: child!,
    );
  },
);
```

{@end-tool}

{@tool snippet} Show a dialog with time unconditionally displayed in 24 hour format.

```dart
Future<TimeOfDay?> selectedTime24Hour = showTimePicker(
  context: context,
  initialTime: const TimeOfDay(hour: 10, minute: 47),
  builder: (BuildContext context, Widget? child) {
    return MediaQuery(
      data: MediaQuery.of(context).copyWith(alwaysUse24HourFormat: true),
      child: child!,
    );
  },
);
```

{@end-tool}

{@tool dartpad} This example illustrates how to open a time picker, and allows exploring some of the variations in the types of time pickers that may be shown.

** See code in examples/api/lib/material/time_picker/show_time_picker.0.dart ** {@end-tool}

See also:

- [showDatePicker], which shows a dialog that contains a Material Design date picker.
- [TimePickerThemeData], which allows you to customize the colors, typography, and shape of the time picker.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
