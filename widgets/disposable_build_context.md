# DisposableBuildContext

```dart
class DisposableBuildContext<T extends State> {}
```

Provides non-leaking access to a [BuildContext].

A [BuildContext] is only valid if it is pointing to an active [Element]. Once the [Element] is unmounted, the [BuildContext] should not be accessed further. This class makes it possible for a [StatefulWidget] to share its build context safely with other objects.

Creators of this object must guarantee the following:

1.  They create this object at or after [State.initState] but before [State.dispose]. In particular, do not attempt to create this from the constructor of a state.
2.  They call [dispose] from [State.dispose].

This object will not hold on to the [State] after disposal.

### DisposableBuildContext()

```dart
DisposableBuildContext(T? _state)
```

Creates an object that provides access to a [BuildContext] without leaking a [State].

Creators must call [dispose] when the [State] is disposed.

[State.mounted] must be true.

### context

```dart
BuildContext? get context
```

Provides safe access to the build context.

If [dispose] has been called, will return null.

Otherwise, asserts the [_state] is still mounted and returns its context.

### dispose()

```dart
void dispose()
```

Marks the [BuildContext] as disposed.

Creators of this object must call [dispose] when their [Element] is unmounted, i.e. when [State.dispose] is called.
