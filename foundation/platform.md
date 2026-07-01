@docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# defaultTargetPlatform

```dart
TargetPlatform get defaultTargetPlatform
```

The [TargetPlatform] that matches the platform on which the framework is currently executing.

This is the default value of [ThemeData.platform] (hence the name). Widgets from the material library should use [Theme.of] to determine the current platform for styling purposes, rather than using [defaultTargetPlatform]. Widgets and render objects at lower layers that try to emulate the underlying platform can depend on [defaultTargetPlatform] directly. The [dart:io.Platform] object should only be used directly when it's critical to actually know the current platform, without any overrides possible (for example, when a system API is about to be called).

In a test environment, the platform returned is [TargetPlatform.android] regardless of the host platform. (Android was chosen because the tests were originally written assuming Android-like behavior, and we added platform adaptations for iOS later). Tests can check iOS behavior by using the platform override APIs (such as [ThemeData.platform] in the material library) or by setting [debugDefaultTargetPlatformOverride] in debug builds.

Tests can also create specific platform tests by and adding a `variant:` argument to the test and using a [TargetPlatformVariant].

See also:

- [kIsWeb], a boolean which is true if the application is running on the web, where [defaultTargetPlatform] returns which platform the browser is running on.

# TargetPlatform

```dart
enum TargetPlatform {}
```

The platform that user interaction should adapt to target.

The [defaultTargetPlatform] getter returns the current platform.

When using the "flutter run" command, the "o" key will toggle between values of this enum when updating [debugDefaultTargetPlatformOverride]. This lets one test how the application will work on various platforms without having to switch emulators or physical devices.

Android: <https://www.android.com/>

Fuchsia: <https://fuchsia.dev/fuchsia-src/concepts>

iOS: <https://www.apple.com/ios/>

Linux: <https://www.linux.org>

macOS: <https://www.apple.com/macos>

Windows: <https://www.windows.com>

# debugDefaultTargetPlatformOverride

```dart
TargetPlatform? get debugDefaultTargetPlatformOverride
```

Override the [defaultTargetPlatform] in debug builds.

Setting this to null returns the [defaultTargetPlatform] to its original value (based on the actual current platform).

Generally speaking this override is only useful for tests. To change the platform that widgets resemble, consider using the platform override APIs (such as [ThemeData.platform] in the material library) instead.

Setting [debugDefaultTargetPlatformOverride] (as opposed to, say, [ThemeData.platform]) will cause unexpected and undesirable effects. For example, setting this to [TargetPlatform.iOS] when the application is running on Android will cause the TalkBack accessibility tool on Android to be confused because it would be receiving data intended for iOS VoiceOver. Similarly, setting it to [TargetPlatform.android] while on iOS will cause certainly widgets to work assuming the presence of a system-wide back button, which will make those widgets unusable since iOS has no such button.

Attempting to override this property in non-debug builds causes an error.

# debugDefaultTargetPlatformOverride

```dart
set debugDefaultTargetPlatformOverride(TargetPlatform? value)
```
