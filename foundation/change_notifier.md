@docImport 'package:flutter/animation.dart'; @docImport 'package:flutter/widgets.dart';

# Listenable

```dart
abstract class Listenable {}
```

An object that maintains a list of listeners.

The listeners are typically used to notify clients that the object has been updated.

There are two variants of this interface:

- [ValueListenable], an interface that augments the [Listenable] interface with the concept of a _current value_.

- [Animation], an interface that augments the [ValueListenable] interface to add the concept of direction (forward or reverse).

Many classes in the Flutter API use or implement these interfaces. The following subclasses are especially relevant:

- [ChangeNotifier], which can be subclassed or mixed in to create objects that implement the [Listenable] interface.

- [ValueNotifier], which implements the [ValueListenable] interface with a mutable value that triggers the notifications when modified.

The terms "notify clients", "send notifications", "trigger notifications", and "fire notifications" are used interchangeably.

See also:

- [AnimatedBuilder], a widget that uses a builder callback to rebuild whenever a given [Listenable] triggers its notifications. This widget is commonly used with [Animation] subclasses, hence its name, but is by no means limited to animations, as it can be used with any [Listenable]. It is a subclass of [AnimatedWidget], which can be used to create widgets that are driven from a [Listenable].
- [ValueListenableBuilder], a widget that uses a builder callback to rebuild whenever a [ValueListenable] object triggers its notifications, providing the builder with the value of the object.
- [InheritedNotifier], an abstract superclass for widgets that use a [Listenable]'s notifications to trigger rebuilds in descendant widgets that declare a dependency on them, using the [InheritedWidget] mechanism.
- [Listenable.merge], which creates a [Listenable] that triggers notifications whenever any of a list of other [Listenable]s trigger their notifications.

### Listenable()

```dart
Listenable()
```

This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### Listenable.merge()

```dart
Listenable.merge(Iterable<Listenable?> listenables)
```

Return a [Listenable] that triggers when any of the given [Listenable]s themselves trigger.

Once the factory is called, items must not be added or removed from the iterable. Doing so will lead to memory leaks or exceptions.

The iterable may contain nulls; they are ignored.

### addListener()

```dart
void addListener(VoidCallback listener)
```

Register a closure to be called when the object notifies its listeners.

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

Remove a previously registered closure from the list of closures that the object notifies.

# ValueListenable

```dart
abstract class ValueListenable<T> extends Listenable {}
```

An interface for subclasses of [Listenable] that expose a [value].

This interface is implemented by [ValueNotifier<T>] and [Animation<T>], and allows other APIs to accept either of those implementations interchangeably.

See also:

- [ValueListenableBuilder], a widget that uses a builder callback to rebuild whenever a [ValueListenable] object triggers its notifications, providing the builder with the value of the object.

### ValueListenable()

```dart
ValueListenable()
```

This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### value

```dart
T get value
```

The current value of the object.

When the value changes, the callbacks registered with [addListener] will be invoked.

# ChangeNotifier

```dart
mixin class ChangeNotifier implements Listenable {}
```

A class that can be extended or mixed in that provides a change notification API using [VoidCallback] for notifications.

It is O(1) for adding listeners and O(N) for removing listeners and dispatching notifications (where N is the number of listeners).

## Using ChangeNotifier subclasses for data models

A data structure can extend or mix in [ChangeNotifier] to implement the [Listenable] interface and thus become usable with widgets that listen for changes to [Listenable]s, such as [ListenableBuilder].

{@tool dartpad} The following example implements a simple counter that utilizes a [ListenableBuilder] to limit rebuilds to only the [Text] widget containing the count. The current count is stored in a [ChangeNotifier] subclass, which rebuilds the [ListenableBuilder]'s contents when its value is changed.

** See code in examples/api/lib/widgets/transitions/listenable_builder.2.dart ** {@end-tool}

{@tool dartpad} In this case, the [ChangeNotifier] subclass encapsulates a list, and notifies the clients any time an item is added to the list. This example only supports adding items; as an exercise, consider adding buttons to remove items from the list as well.

** See code in examples/api/lib/widgets/transitions/listenable_builder.3.dart ** {@end-tool}

See also:

- [ValueNotifier], which is a [ChangeNotifier] that wraps a single value.

### debugAssertNotDisposed()

```dart
bool debugAssertNotDisposed(ChangeNotifier notifier)
```

Used by subclasses to assert that the [ChangeNotifier] has not yet been disposed.

{@tool snippet} The [debugAssertNotDisposed] function should only be called inside of an assert, as in this example.

```dart
class MyNotifier with ChangeNotifier {
  void doUpdate() {
    assert(ChangeNotifier.debugAssertNotDisposed(this));
    // ...
  }
}
```

{@end-tool}

### hasListeners

```dart
bool get hasListeners
```

Whether any listeners are currently registered.

Clients should not depend on this value for their behavior, because having one listener's logic change when another listener happens to start or stop listening will lead to extremely hard-to-track bugs. Subclasses might use this information to determine whether to do any work when there are no listeners, however; for example, resuming a [Stream] when a listener is added and pausing it when a listener is removed.

Typically this is used by overriding [addListener], checking if [hasListeners] is false before calling `super.addListener()`, and if so, starting whatever work is needed to determine when to call [notifyListeners]; and similarly, by overriding [removeListener], checking if [hasListeners] is false after calling `super.removeListener()`, and if so, stopping that same work.

This method returns false if [dispose] has been called.

### maybeDispatchObjectCreation()

```dart
void maybeDispatchObjectCreation(ChangeNotifier object)
```

Dispatches event of the [object] creation to [FlutterMemoryAllocations.instance].

If the event was already dispatched or [kFlutterMemoryAllocationsEnabled] is false, the method is noop.

Tools like leak_tracker use the event of object creation to help developers identify the owner of the object, for troubleshooting purposes, by taking stack trace at the moment of the event.

But, as [ChangeNotifier] is mixin, it does not have its own constructor. So, it communicates object creation in first `addListener`, that results in the stack trace pointing to `addListener`, not to constructor.

To make debugging easier, invoke [ChangeNotifier.maybeDispatchObjectCreation] in constructor of the class. It will help to identify the owner.

Make sure to invoke it with condition `if (kFlutterMemoryAllocationsEnabled) ...` so that the method is tree-shaken away when the flag is false.

### addListener()

```dart
void addListener(VoidCallback listener)
```

Register a closure to be called when the object changes.

If the given closure is already registered, an additional instance is added, and must be removed the same number of times it is added before it will stop being called.

This method must not be called after [dispose] has been called.

{@template flutter.foundation.ChangeNotifier.addListener} If a listener is added twice, and is removed once during an iteration (e.g. in response to a notification), it will still be called again. If, on the other hand, it is removed as many times as it was registered, then it will no longer be called. This odd behavior is the result of the [ChangeNotifier] not being able to determine which listener is being removed, since they are identical, therefore it will conservatively still call all the listeners when it knows that any are still registered.

This surprising behavior can be unexpectedly observed when registering a listener on two separate objects which are both forwarding all registrations to a common upstream object. {@endtemplate}

See also:

- [removeListener], which removes a previously registered closure from the list of closures that are notified when the object changes.

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

Remove a previously registered closure from the list of closures that are notified when the object changes.

If the given listener is not registered, the call is ignored.

This method returns immediately if [dispose] has been called.

{@macro flutter.foundation.ChangeNotifier.addListener}

See also:

- [addListener], which registers a closure to be called when the object changes.

### dispose()

```dart
void dispose()
```

Discards any resources used by the object.

After this is called, the object is not in a usable state and should be discarded (calls to [addListener] will throw after the object is disposed).

This method should only be called by the object's owner.

This method does not notify listeners, and clears the listener list once it is called. Consumers of this class must decide on whether to notify listeners or not immediately before disposal.

### notifyListeners()

```dart
void notifyListeners()
```

Call all the registered listeners.

Call this method whenever the object changes, to notify any clients the object may have changed. Listeners that are added during this iteration will not be visited. Listeners that are removed during this iteration will not be visited after they are removed.

Exceptions thrown by listeners will be caught and reported using [FlutterError.reportError].

This method must not be called after [dispose] has been called.

Surprising behavior can result when reentrantly removing a listener (e.g. in response to a notification) that has been registered multiple times. See the discussion at [removeListener].

# ValueNotifier

```dart
class ValueNotifier<T> extends ChangeNotifier implements ValueListenable<T> {}
```

A [ChangeNotifier] that holds a single value.

When [value] is replaced with a new value that is **not equal** to the old value as evaluated by the equality operator (`==`), this class notifies its listeners.

## Limitations

Notifications are triggered based on **equality (`==`)**, not on mutations within the value itself. As a result, changes to mutable objects that do not affect their equality will not cause listeners to be notified.

For example, a `ValueNotifier<List<int>>` will not notify listeners when the contents of the existing list are modified in-place; it only notifies when a new value is assigned to the `value` property (i.e. `value = newValue`), where equality is determined by `==`.

Because of this behavior, [ValueNotifier] is best used with immutable data types.

For mutable data types, consider extending [ChangeNotifier] directly and calling [notifyListeners] manually when changes occur.

### ValueNotifier()

```dart
ValueNotifier(T _value)
```

Creates a [ChangeNotifier] that wraps this value.

### value

```dart
T get value
```

The current value stored in this notifier.

When the value is replaced with something that is not equal to the old value as evaluated by the equality operator ==, this class notifies its listeners.

### value

```dart
set value(T newValue)
```

### toString()

```dart
String toString()
```
