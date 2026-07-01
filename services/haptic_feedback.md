# HapticFeedback

```dart
abstract final class HapticFeedback {}
```

Allows access to the haptic feedback interface on the device.

This API is intentionally terse since it calls default platform behavior. It is not suitable for precise control of the system's haptic feedback module.

See also:

- [Human Interface Haptics Guidelines](https://developer.apple.com/design/human-interface-guidelines/playing-haptics)

### vibrate()

```dart
Future<void> vibrate()
```

Provides vibration haptic feedback to the user for a short duration.

On iOS devices that support haptic feedback, this uses the default system vibration value (`kSystemSoundID_Vibrate`).

On Android, this uses the platform haptic feedback API to simulate a response to a long press (`HapticFeedbackConstants.LONG_PRESS`).

### lightImpact()

```dart
Future<void> lightImpact()
```

Provides a haptic feedback corresponding a collision impact with a light mass.

On iOS versions 10 and above, this uses a `UIImpactFeedbackGenerator` with `UIImpactFeedbackStyleLight`. This call has no effects on iOS versions below 10.

On Android, this uses `HapticFeedbackConstants.VIRTUAL_KEY`.

{@template flutter.services.HapticFeedback.impact} See also:

- [Human Interface Selection Playing Impact Haptic](https://developer.apple.com/design/human-interface-guidelines/playing-haptics#Impact) {@endtemplate}

### mediumImpact()

```dart
Future<void> mediumImpact()
```

Provides a haptic feedback corresponding a collision impact with a medium mass.

On iOS versions 10 and above, this uses a `UIImpactFeedbackGenerator` with `UIImpactFeedbackStyleMedium`. This call has no effects on iOS versions below 10.

On Android, this uses `HapticFeedbackConstants.KEYBOARD_TAP`.

{@macro flutter.services.HapticFeedback.impact}

### heavyImpact()

```dart
Future<void> heavyImpact()
```

Provides a haptic feedback corresponding a collision impact with a heavy mass.

On iOS versions 10 and above, this uses a `UIImpactFeedbackGenerator` with `UIImpactFeedbackStyleHeavy`. This call has no effects on iOS versions below 10.

On Android, this uses `HapticFeedbackConstants.CONTEXT_CLICK` on API levels 23 and above. This call has no effects on Android API levels below 23.

{@macro flutter.services.HapticFeedback.impact}

### selectionClick()

```dart
Future<void> selectionClick()
```

Provides a haptic feedback indication selection changing through discrete values.

On iOS versions 10 and above, this uses a `UISelectionFeedbackGenerator`. This call has no effects on iOS versions below 10.

On Android, this uses `HapticFeedbackConstants.CLOCK_TICK`.

See also:

- [Human Interface Selection Playing Selection Haptics](https://developer.apple.com/design/human-interface-guidelines/playing-haptics#Selection)

### successNotification()

```dart
Future<void> successNotification()
```

Provides a haptic feedback indicating that a task or action has completed successfully.

On iOS, this uses a `UINotificationFeedbackGenerator` with `UINotificationFeedbackTypeSuccess`.

On Android, this uses `HapticFeedbackConstants.CONFIRM` on API levels 30 and above. This call has no effects on Android API levels below 30.

{@template flutter.services.HapticFeedback.notification} See also:

- [Human Interface Guidelines Playing Haptics](https://developer.apple.com/design/human-interface-guidelines/playing-haptics#Notification) {@endtemplate}

### warningNotification()

```dart
Future<void> warningNotification()
```

Provides a haptic feedback indicating that a task or action has produced a warning.

On iOS, this uses a `UINotificationFeedbackGenerator` with `UINotificationFeedbackTypeWarning`.

On Android, this uses `HapticFeedbackConstants.KEYBOARD_TAP` on API levels 30 and above. This call has no effects on Android API levels below 30.

{@macro flutter.services.HapticFeedback.notification}

### errorNotification()

```dart
Future<void> errorNotification()
```

Provides a haptic feedback indicating that a task or action has failed.

On iOS, this uses a `UINotificationFeedbackGenerator` with `UINotificationFeedbackTypeError`.

On Android, this uses `HapticFeedbackConstants.REJECT` on API levels 30 and above. This call has no effects on Android API levels below 30.

{@macro flutter.services.HapticFeedback.notification}
