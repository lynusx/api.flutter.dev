# AnimationLazyListenerMixin

```dart
mixin AnimationLazyListenerMixin {}
```

A mixin that helps listen to another object only when this object has registered listeners.

This mixin provides implementations of [didRegisterListener] and [didUnregisterListener], and therefore can be used in conjunction with mixins that require these methods, [AnimationLocalListenersMixin] and [AnimationLocalStatusListenersMixin].

### didRegisterListener()

```dart
void didRegisterListener()
```

Calls [didStartListening] every time a registration of a listener causes an empty list of listeners to become non-empty.

See also:

- [didUnregisterListener], which may cause the listener list to become empty again, and in turn cause this method to call [didStartListening] again.

### didUnregisterListener()

```dart
void didUnregisterListener()
```

Calls [didStopListening] when an only remaining listener is unregistered, thus making the list empty.

See also:

- [didRegisterListener], which causes the listener list to become non-empty.

### didStartListening()

```dart
void didStartListening()
```

Called when the number of listeners changes from zero to one.

### didStopListening()

```dart
void didStopListening()
```

Called when the number of listeners changes from one to zero.

### isListening

```dart
bool get isListening
```

Whether there are any listeners.

# AnimationEagerListenerMixin

```dart
mixin AnimationEagerListenerMixin {}
```

A mixin that replaces the [didRegisterListener]/[didUnregisterListener] contract with a dispose contract.

This mixin provides implementations of [didRegisterListener] and [didUnregisterListener], and therefore can be used in conjunction with mixins that require these methods, [AnimationLocalListenersMixin] and [AnimationLocalStatusListenersMixin].

### didRegisterListener()

```dart
void didRegisterListener()
```

This implementation ignores listener registrations.

### didUnregisterListener()

```dart
void didUnregisterListener()
```

This implementation ignores listener registrations.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

# AnimationLocalListenersMixin

```dart
mixin AnimationLocalListenersMixin {}
```

A mixin that implements the [addListener]/[removeListener] protocol and notifies all the registered listeners when [notifyListeners] is called.

This mixin requires that the mixing class provide methods [didRegisterListener] and [didUnregisterListener]. Implementations of these methods can be obtained by mixing in another mixin from this library, such as [AnimationLazyListenerMixin].

### didRegisterListener()

```dart
void didRegisterListener()
```

Called immediately before a listener is added via [addListener].

At the time this method is called the registered listener is not yet notified by [notifyListeners].

### didUnregisterListener()

```dart
void didUnregisterListener()
```

Called immediately after a listener is removed via [removeListener].

At the time this method is called the removed listener is no longer notified by [notifyListeners].

### addListener()

```dart
void addListener(VoidCallback listener)
```

Calls the listener every time the value of the animation changes.

Listeners can be removed with [removeListener].

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

Stop calling the listener every time the value of the animation changes.

Listeners can be added with [addListener].

### clearListeners()

```dart
void clearListeners()
```

Removes all listeners added with [addListener].

This method is typically called from the `dispose` method of the class using this mixin if the class also uses the [AnimationEagerListenerMixin].

Calling this method will not trigger [didUnregisterListener].

### notifyListeners()

```dart
void notifyListeners()
```

Calls all the listeners.

If listeners are added or removed during this function, the modifications will not change which listeners are called during this iteration.

# AnimationLocalStatusListenersMixin

```dart
mixin AnimationLocalStatusListenersMixin {}
```

A mixin that implements the addStatusListener/removeStatusListener protocol and notifies all the registered listeners when notifyStatusListeners is called.

This mixin requires that the mixing class provide methods [didRegisterListener] and [didUnregisterListener]. Implementations of these methods can be obtained by mixing in another mixin from this library, such as [AnimationLazyListenerMixin].

### didRegisterListener()

```dart
void didRegisterListener()
```

Called immediately before a status listener is added via [addStatusListener].

At the time this method is called the registered listener is not yet notified by [notifyStatusListeners].

### didUnregisterListener()

```dart
void didUnregisterListener()
```

Called immediately after a status listener is removed via [removeStatusListener].

At the time this method is called the removed listener is no longer notified by [notifyStatusListeners].

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

Calls listener every time the status of the animation changes.

Listeners can be removed with [removeStatusListener].

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

Stops calling the listener every time the status of the animation changes.

Listeners can be added with [addStatusListener].

### clearStatusListeners()

```dart
void clearStatusListeners()
```

Removes all listeners added with [addStatusListener].

This method is typically called from the `dispose` method of the class using this mixin if the class also uses the [AnimationEagerListenerMixin].

Calling this method will not trigger [didUnregisterListener].

### notifyStatusListeners()

```dart
void notifyStatusListeners(AnimationStatus status)
```

Calls all the status listeners.

If listeners are added or removed during this function, the modifications will not change which listeners are called during this iteration.
