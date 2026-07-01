@docImport 'scroll_view.dart';

# ScrollNotificationCallback

```dart
typedef ScrollNotificationCallback = void Function(ScrollNotification notification)
```

A [ScrollNotification] listener for [ScrollNotificationObserver].

[ScrollNotificationObserver] is similar to [NotificationListener]. It supports a listener list instead of just a single listener and its listeners run unconditionally, they do not require a gating boolean return value.

# ScrollNotificationObserver

```dart
class ScrollNotificationObserver extends StatefulWidget {}
```

Notifies its listeners when a descendant scrolls.

To add a listener to a [ScrollNotificationObserver] ancestor:

```dart
ScrollNotificationObserver.of(context).addListener(_listener);
```

To remove the listener from a [ScrollNotificationObserver] ancestor:

```dart
ScrollNotificationObserver.of(context).removeListener(_listener);
```

Stateful widgets that share an ancestor [ScrollNotificationObserver] typically add a listener in [State.didChangeDependencies] (removing the old one if necessary) and remove the listener in their [State.dispose] method.

Any function with the [ScrollNotificationCallback] signature can act as a listener:

```dart
// (e.g. in a stateful widget)
void _listener(ScrollNotification notification) {
  // Do something, maybe setState()
}
```

This widget is similar to [NotificationListener]. It supports a listener list instead of just a single listener and its listeners run unconditionally, they do not require a gating boolean return value.

{@tool dartpad} This sample shows a "Scroll to top" button that uses [ScrollNotificationObserver] to listen for scroll notifications from [ListView]. The button is only visible when the user has scrolled down. When pressed, the button animates the scroll position of the [ListView] back to the top.

** See code in examples/api/lib/widgets/scroll_notification_observer/scroll_notification_observer.0.dart ** {@end-tool}

### ScrollNotificationObserver()

```dart
ScrollNotificationObserver({dynamic key, required Widget child})
```

Create a [ScrollNotificationObserver].

### child

```dart
Widget child
```

The subtree below this widget.

### maybeOf()

```dart
ScrollNotificationObserverState? maybeOf(BuildContext context)
```

The closest instance of this class that encloses the given context.

If there is no enclosing [ScrollNotificationObserver] widget, then null is returned.

Calling this method will create a dependency on the closest [ScrollNotificationObserver] in the [context], if there is one.

See also:

- [ScrollNotificationObserver.of], which is similar to this method, but asserts if no [ScrollNotificationObserver] ancestor is found.

### of()

```dart
ScrollNotificationObserverState of(BuildContext context)
```

The closest instance of this class that encloses the given context.

If no ancestor is found, this method will assert in debug mode, and throw an exception in release mode.

Calling this method will create a dependency on the closest [ScrollNotificationObserver] in the [context].

See also:

- [ScrollNotificationObserver.maybeOf], which is similar to this method, but returns null if no [ScrollNotificationObserver] ancestor is found.

### createState()

```dart
ScrollNotificationObserverState createState()
```

# ScrollNotificationObserverState

```dart
class ScrollNotificationObserverState extends State<ScrollNotificationObserver> {}
```

The listener list state for a [ScrollNotificationObserver] returned by [ScrollNotificationObserver.of].

[ScrollNotificationObserver] is similar to [NotificationListener]. It supports a listener list instead of just a single listener and its listeners run unconditionally, they do not require a gating boolean return value.

### addListener()

```dart
void addListener(ScrollNotificationCallback listener)
```

Add a [ScrollNotificationCallback] that will be called each time a descendant scrolls.

### removeListener()

```dart
void removeListener(ScrollNotificationCallback listener)
```

Remove the specified [ScrollNotificationCallback].

### build()

```dart
Widget build(BuildContext context)
```

### dispose()

```dart
void dispose()
```
