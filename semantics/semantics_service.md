@docImport 'package:flutter/widgets.dart';

# SemanticsService

```dart
abstract final class SemanticsService {}
```

Allows access to the platform's accessibility services.

Events sent by this service are handled by the platform-specific accessibility bridge in Flutter's engine.

When possible, prefer using mechanisms like [Semantics] to implicitly trigger announcements over using this event.

### announce()

```dart
Future<void> announce(String message, TextDirection textDirection, {Assertiveness assertiveness = Assertiveness.polite})
```

Sends a semantic announcement.

This method is deprecated. Prefer using [sendAnnouncement] instead.

{@template flutter.semantics.service.announce} This should be used for announcement that are not seamlessly announced by the system as a result of a UI state change.

For example a camera application can use this method to make accessibility announcements regarding objects in the viewfinder.

The assertiveness level of the announcement is determined by [assertiveness]. Currently, this is only supported by the web engine and has no effect on other platforms. The default mode is [Assertiveness.polite].

Not all platforms support announcements. Check to see if it is supported using [MediaQuery.supportsAnnounceOf] before calling this method.

### Android

Android has [deprecated announcement events][1] due to its disruptive behavior with TalkBack forcing it to clear its speech queue and speak the provided text. Instead, use mechanisms like [Semantics] to implicitly trigger announcements.

[1]: https://developer.android.com/reference/android/view/View#announceForAccessibility(java.lang.CharSequence) {@endtemplate}

### sendAnnouncement()

```dart
Future<void> sendAnnouncement(FlutterView view, String message, TextDirection textDirection, {Assertiveness assertiveness = Assertiveness.polite})
```

Sends a semantic announcement for a particular view.

One can use [View.of] to get the current [FlutterView].

{@macro flutter.semantics.service.announce}

### tooltip()

```dart
Future<void> tooltip(String message)
```

Sends a semantic announcement of a tooltip.

Currently only honored on Android. The contents of [message] will be read by TalkBack.
