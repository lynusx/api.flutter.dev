@docImport 'platform_channel.dart'; @docImport 'service_extensions.dart';

# debugKeyEventSimulatorTransitModeOverride

```dart
KeyDataTransitMode? debugKeyEventSimulatorTransitModeOverride
```

Override the transit mode with which key events are simulated.

Setting [debugKeyEventSimulatorTransitModeOverride] is a good way to make certain tests simulate the behavior of different type of platforms in terms of their extent of support for keyboard API.

This value is deprecated and will be removed.

# debugPrintKeyboardEvents

```dart
bool debugPrintKeyboardEvents
```

Setting to true will cause extensive logging to occur when key events are received.

Can be used to debug keyboard issues: each time a key event is received on the framework side, the event details and the current pressed state will be printed.

# debugAssertAllServicesVarsUnset()

```dart
bool debugAssertAllServicesVarsUnset(String reason)
```

Returns true if none of the widget library debug variables have been changed.

This function is used by the test framework to ensure that debug variables haven't been inadvertently changed.

See [the services library](services/services-library.html) for a complete list.

# debugProfilePlatformChannels

```dart
bool debugProfilePlatformChannels
```

Controls whether platform channel usage can be debugged in non-release mode.

This value is modified by calls to the [ServicesServiceExtensions.profilePlatformChannels] service extension.

See also:

- [shouldProfilePlatformChannels], which checks both [kProfilePlatformChannels] and [debugProfilePlatformChannels] for the current run mode.
- [kProfilePlatformChannels], which determines whether platform channel usage can be debugged in release mode.
