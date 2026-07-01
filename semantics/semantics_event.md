@docImport 'package:flutter/services.dart'; @docImport 'package:flutter/widgets.dart';

# Assertiveness

```dart
enum Assertiveness {}
```

Determines the assertiveness level of the accessibility announcement.

It is used by [AnnounceSemanticsEvent] to determine the priority with which assistive technology should treat announcements.

The assistive technology will speak changes whenever the user is idle.

The assistive technology will interrupt any announcement that it is currently making to notify the user about the change.

It should only be used for time-sensitive/critical notifications.

# SemanticsEvent

```dart
abstract class SemanticsEvent {}
```

An event sent by the application to notify interested listeners that something happened to the user interface (e.g. a view scrolled).

These events are usually interpreted by assistive technologies to give the user additional clues about the current state of the UI.

### SemanticsEvent()

```dart
SemanticsEvent(String type)
```

Initializes internal fields.

[type] is a string that identifies this class of [SemanticsEvent]s.

### type

```dart
String type
```

The type of this event.

The type is used by the engine to translate this event into the appropriate native event (`UIAccessibility*Notification` on iOS and `AccessibilityEvent` on Android).

### toMap()

```dart
Map<String, dynamic> toMap({int? nodeId})
```

Converts this event to a Map that can be encoded with [StandardMessageCodec].

[nodeId] is the unique identifier of the semantics node associated with the event, or null if the event is not associated with a semantics node.

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

Returns the event's data object.

### toString()

```dart
String toString()
```

# AnnounceSemanticsEvent

```dart
class AnnounceSemanticsEvent extends SemanticsEvent {}
```

An event for a semantic announcement.

This should be used for announcement that are not seamlessly announced by the system as a result of a UI state change.

For example a camera application can use this method to make accessibility announcements regarding objects in the viewfinder.

When possible, prefer using mechanisms like [Semantics] to implicitly trigger announcements over using this event.

### Android

Android has [deprecated announcement events][1] due to its disruptive behavior with TalkBack forcing it to clear its speech queue and speak the provided text. Instead, use mechanisms like [Semantics] to implicitly trigger announcements.

[1]: https://developer.android.com/reference/android/view/View#announceForAccessibility(java.lang.CharSequence)

### AnnounceSemanticsEvent()

```dart
AnnounceSemanticsEvent(String message, TextDirection textDirection, int viewId, {Assertiveness assertiveness = Assertiveness.polite})
```

Constructs an event that triggers an announcement by the platform for the provided view.

### viewId

```dart
int viewId
```

The view that this announcement is on.

### message

```dart
String message
```

The message to announce.

### textDirection

```dart
TextDirection textDirection
```

Text direction for [message].

### assertiveness

```dart
Assertiveness assertiveness
```

Determines whether the announcement should interrupt any existing announcement, or queue after it.

On the web this option uses the aria-live level to set the assertiveness of the announcement. On iOS, Android, Windows, Linux, macOS, and Fuchsia this option currently has no effect.

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# TooltipSemanticsEvent

```dart
class TooltipSemanticsEvent extends SemanticsEvent {}
```

An event for a semantic announcement of a tooltip.

This is only used by Android to announce tooltip values.

### TooltipSemanticsEvent()

```dart
TooltipSemanticsEvent(String message)
```

Constructs an event that triggers a tooltip announcement by the platform.

### message

```dart
String message
```

The text content of the tooltip.

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# LongPressSemanticsEvent

```dart
class LongPressSemanticsEvent extends SemanticsEvent {}
```

An event which triggers long press semantic feedback.

Currently only honored on Android. Triggers a long-press specific sound when TalkBack is enabled.

### LongPressSemanticsEvent()

```dart
LongPressSemanticsEvent()
```

Constructs an event that triggers a long-press semantic feedback by the platform.

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# TapSemanticEvent

```dart
class TapSemanticEvent extends SemanticsEvent {}
```

An event which triggers tap semantic feedback.

Currently only honored on Android. Triggers a tap specific sound when TalkBack is enabled.

### TapSemanticEvent()

```dart
TapSemanticEvent()
```

Constructs an event that triggers a long-press semantic feedback by the platform.

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# FocusSemanticEvent

```dart
class FocusSemanticEvent extends SemanticsEvent {}
```

An event to move the accessibility focus.

Using this API is generally not recommended, as it may break a users' expectation of how a11y focus works and therefore should be used very carefully.

One possible use case: For example, the currently focused rendering object is replaced by another rendering object. In general, such design should be avoided if possible. If not, one may want to refocus the newly added rendering object.

One example that is not recommended: When a new popup or dropdown opens, moving the focus in these cases may confuse users and make it less accessible.

{@tool snippet}

The following code snippet shows how one can request focus on a certain widget.

```dart
class MyWidget extends StatefulWidget {
  const MyWidget({super.key});

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  final GlobalKey mykey = GlobalKey();

  @override
  void initState() {
    super.initState();
    // Using addPostFrameCallback because changing focus need to wait for the widget to finish rendering.
    WidgetsBinding.instance.addPostFrameCallback((_) {
      mykey.currentContext?.findRenderObject()?.sendSemanticsEvent(const FocusSemanticEvent());
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('example'),
      ),
      body: Column(
        children: <Widget>[
          const Text('Hello World'),
          const SizedBox(height: 50),
          Text('set focus here', key: mykey),
        ],
      ),
    );
  }
}
```

{@end-tool}

This currently only supports Android and iOS.

### FocusSemanticEvent()

```dart
FocusSemanticEvent()
```

Constructs an event that triggers a focus change by the platform.

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```
