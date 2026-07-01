@docImport 'scroll_delegate.dart'; @docImport 'scroll_view.dart';

# AutomaticKeepAlive

```dart
class AutomaticKeepAlive extends StatefulWidget {}
```

Allows subtrees to request to be kept alive in lazy lists.

This widget is like [KeepAlive] but instead of being explicitly configured, it listens to [KeepAliveNotification] messages from the [child] and other descendants.

The subtree is kept alive whenever there is one or more descendant that has sent a [KeepAliveNotification] and not yet triggered its [KeepAliveNotification.handle].

To send these notifications, consider using [AutomaticKeepAliveClientMixin].

The [SliverChildBuilderDelegate] and [SliverChildListDelegate] delegates, used with [SliverList] and [SliverGrid], as well as the scroll view counterparts [ListView] and [GridView], have an `addAutomaticKeepAlives` feature, which is enabled by default. This feature inserts [AutomaticKeepAlive] widgets around each child, which in turn configure [KeepAlive] widgets in response to [KeepAliveNotification]s.

The same `addAutomaticKeepAlives` feature is supported by [TwoDimensionalChildBuilderDelegate] and [TwoDimensionalChildListDelegate].

{@tool dartpad} This sample demonstrates how to use the [AutomaticKeepAlive] widget in combination with the [AutomaticKeepAliveClientMixin] to selectively preserve the state of individual items in a scrollable list.

Normally, widgets in a lazily built list like [ListView.builder] are disposed of when they leave the visible area to maintain performance. This means that any state inside a [StatefulWidget] would be lost unless explicitly preserved.

In this example, each list item is a [StatefulWidget] that includes a counter and an increment button. To preserve the state of selected items (based on their index), the [AutomaticKeepAlive] widget and [AutomaticKeepAliveClientMixin] are used:

- The `wantKeepAlive` getter in the item’s state class returns true for even-indexed items, indicating that their state should be preserved.
- For odd-indexed items, `wantKeepAlive` returns false, so their state is not preserved when scrolled out of view.

** See code in examples/api/lib/widgets/keep_alive/automatic_keep_alive.0.dart ** {@end-tool}

See also:

- [AutomaticKeepAliveClientMixin], which is a mixin with convenience methods for clients of [AutomaticKeepAlive]. Used with [State] subclasses.
- [KeepAlive] which marks a child as needing to stay alive even when it's in a lazy list that would otherwise remove it.

### AutomaticKeepAlive()

```dart
AutomaticKeepAlive({dynamic key, required Widget child})
```

Creates a widget that listens to [KeepAliveNotification]s and maintains a [KeepAlive] widget appropriately.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<AutomaticKeepAlive> createState()
```

# KeepAliveNotification

```dart
class KeepAliveNotification extends Notification {}
```

Indicates that the subtree through which this notification bubbles must be kept alive even if it would normally be discarded as an optimization.

For example, a focused text field might fire this notification to indicate that it should not be disposed even if the user scrolls the field off screen.

Each [KeepAliveNotification] is configured with a [handle] that consists of a [Listenable] that is triggered when the subtree no longer needs to be kept alive.

The [handle] should be triggered any time the sending widget is removed from the tree (in [State.deactivate]). If the widget is then rebuilt and still needs to be kept alive, it should immediately send a new notification (possible with the very same [Listenable]) during build.

This notification is listened to by the [AutomaticKeepAlive] widget, which is added to the tree automatically by [SliverList] (and [ListView]) and [SliverGrid] (and [GridView]) widgets.

Failure to trigger the [handle] in the manner described above will likely cause the [AutomaticKeepAlive] to lose track of whether the widget should be kept alive or not, leading to memory leaks or lost data. For example, if the widget that requested keepalive is removed from the subtree but doesn't trigger its [Listenable] on the way out, then the subtree will continue to be kept alive until the list itself is disposed. Similarly, if the [Listenable] is triggered while the widget needs to be kept alive, but a new [KeepAliveNotification] is not immediately sent, then the widget risks being garbage collected while it wants to be kept alive.

It is an error to use the same [handle] in two [KeepAliveNotification]s within the same [AutomaticKeepAlive] without triggering that [handle] before the second notification is sent.

For a more convenient way to interact with [AutomaticKeepAlive] widgets, consider using [AutomaticKeepAliveClientMixin], which uses [KeepAliveNotification] internally.

### KeepAliveNotification()

```dart
KeepAliveNotification(Listenable handle)
```

Creates a notification to indicate that a subtree must be kept alive.

### handle

```dart
Listenable handle
```

A [Listenable] that will inform its clients when the widget that fired the notification no longer needs to be kept alive.

The [Listenable] should be triggered any time the sending widget is removed from the tree (in [State.deactivate]). If the widget is then rebuilt and still needs to be kept alive, it should immediately send a new notification (possible with the very same [Listenable]) during build.

See also:

- [KeepAliveHandle], a convenience class for use with this property.

# KeepAliveHandle

```dart
class KeepAliveHandle extends ChangeNotifier {}
```

A [Listenable] which can be manually triggered.

Used with [KeepAliveNotification] objects as their [KeepAliveNotification.handle].

For a more convenient way to interact with [AutomaticKeepAlive] widgets, consider using [AutomaticKeepAliveClientMixin], which uses a [KeepAliveHandle] internally.

### dispose()

```dart
void dispose()
```

# AutomaticKeepAliveClientMixin

```dart
mixin AutomaticKeepAliveClientMixin<T extends StatefulWidget> on State<T> {}
```

A mixin with convenience methods for clients of [AutomaticKeepAlive]. It is used with [State] subclasses to manage keep-alive behavior in lazily built lists.

This mixin simplifies interaction with [AutomaticKeepAlive] by automatically sending [KeepAliveNotification]s when necessary. Subclasses must implement [wantKeepAlive] to indicate whether the widget should be kept alive and call [updateKeepAlive] whenever its value changes.

The mixin internally manages a [KeepAliveHandle], which is used to notify the nearest [AutomaticKeepAlive] ancestor of changes in keep-alive requirements. [AutomaticKeepAlive] listens for [KeepAliveNotification]s sent by this mixin and dynamically wraps the subtree in a [KeepAlive] widget to preserve its state when it is no longer visible in the viewport.

Subclasses must implement [wantKeepAlive], and their [build] methods must call `super.build` (though the return value should be ignored).

Then, whenever [wantKeepAlive]'s value changes (or might change), the subclass should call [updateKeepAlive].

The type argument `T` is the type of the [StatefulWidget] subclass of the [State] into which this class is being mixed.

The [SliverChildBuilderDelegate] and [SliverChildListDelegate] delegates, used with [SliverList] and [SliverGrid], as well as the scroll view counterparts [ListView] and [GridView], have an `addAutomaticKeepAlives` feature, which is enabled by default. This feature inserts [AutomaticKeepAlive] widgets around each child, which in turn configure [KeepAlive] widgets in response to [KeepAliveNotification]s.

The same `addAutomaticKeepAlives` feature is supported by [TwoDimensionalChildBuilderDelegate] and [TwoDimensionalChildListDelegate].

{@tool dartpad} This example demonstrates how to use the [AutomaticKeepAliveClientMixin] to keep the state of a widget alive even when it is scrolled out of view.

** See code in examples/api/lib/widgets/keep_alive/automatic_keep_alive_client_mixin.0.dart ** {@end-tool}

See also:

- [AutomaticKeepAlive], which listens to messages from this mixin.
- [KeepAliveNotification], the notifications sent by this mixin.
- [KeepAlive] which marks a child as needing to stay alive even when it's in a lazy list that would otherwise remove it.

### wantKeepAlive

```dart
bool get wantKeepAlive
```

Whether the current instance should be kept alive.

Call [updateKeepAlive] whenever this getter's value changes.

### updateKeepAlive()

```dart
void updateKeepAlive()
```

Ensures that any [AutomaticKeepAlive] ancestors are in a good state, by firing a [KeepAliveNotification] or triggering the [KeepAliveHandle] as appropriate.

### initState()

```dart
void initState()
```

### deactivate()

```dart
void deactivate()
```

### build()

```dart
Widget build(BuildContext context)
```
