@docImport 'binding.dart';

# Priority

```dart
class Priority {}
```

A task priority, as passed to [SchedulerBinding.scheduleTask].

### value

```dart
int get value
```

Integer that describes this Priority value.

### idle

```dart
Priority idle
```

A task to run after all other tasks, when no animations are running.

### animation

```dart
Priority animation
```

A task to run even when animations are running.

### touch

```dart
Priority touch
```

A task to run even when the user is interacting with the device.

### kMaxOffset

```dart
int kMaxOffset
```

Maximum offset by which to clamp relative priorities.

It is still possible to have priorities that are offset by more than this amount by repeatedly taking relative offsets, but that is generally discouraged.

### operator +()

```dart
Priority operator +(int offset)
```

Returns a priority relative to this priority.

A positive [offset] indicates a higher priority.

The parameter [offset] is clamped to ±[kMaxOffset].

### operator -()

```dart
Priority operator -(int offset)
```

Returns a priority relative to this priority.

A positive offset indicates a lower priority.

The parameter [offset] is clamped to ±[kMaxOffset].
