@docImport 'package:flutter/material.dart';

# SizeChangedLayoutNotification

```dart
class SizeChangedLayoutNotification extends LayoutChangedNotification {}
```

Indicates that the size of one of the descendants of the object receiving this notification has changed, and that therefore any assumptions about that layout are no longer valid.

For example, sent by the [SizeChangedLayoutNotifier] widget whenever that widget changes size.

This notification can be used for triggering repaints, but if you use this notification to trigger rebuilds or relayouts, you'll create a backwards dependency in the frame pipeline because [SizeChangedLayoutNotification]s are generated during layout, which is after the build phase and in the middle of the layout phase. This backwards dependency can lead to visual corruption or lags.

See [LayoutChangedNotification] for additional discussion of layout notifications such as this one.

See also:

- [SizeChangedLayoutNotifier], which sends this notification.
- [LayoutChangedNotification], of which this is a subclass.

### SizeChangedLayoutNotification()

```dart
SizeChangedLayoutNotification()
```

Create a new [SizeChangedLayoutNotification].

# SizeChangedLayoutNotifier

```dart
class SizeChangedLayoutNotifier extends SingleChildRenderObjectWidget {}
```

A widget that automatically dispatches a [SizeChangedLayoutNotification] when the layout dimensions of its child change.

The notification is not sent for the initial layout (since the size doesn't change in that case, it's just established).

To listen for the notification dispatched by this widget, use a [NotificationListener<SizeChangedLayoutNotification>].

The [Material] class listens for [LayoutChangedNotification]s, including [SizeChangedLayoutNotification]s, to repaint [InkResponse] and [InkWell] ink effects. When a widget is likely to change size, wrapping it in a [SizeChangedLayoutNotifier] will cause the ink effects to correctly repaint when the child changes size.

See also:

- [Notification], the base class for notifications that bubble through the widget tree.

### SizeChangedLayoutNotifier()

```dart
SizeChangedLayoutNotifier({dynamic key, Widget? child})
```

Creates a [SizeChangedLayoutNotifier] that dispatches layout changed notifications when [child] changes layout size.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```
