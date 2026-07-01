@docImport 'events.dart';

# GestureDisposition

```dart
enum GestureDisposition {}
```

Whether the gesture was accepted or rejected.

This gesture was accepted as the interpretation of the user's input.

This gesture was rejected as the interpretation of the user's input.

# GestureArenaMember

```dart
abstract class GestureArenaMember {}
```

Represents an object participating in an arena.

Receives callbacks from the GestureArena to notify the object when it wins or loses a gesture negotiation. Exactly one of [acceptGesture] or [rejectGesture] will be called for each arena this member was added to, regardless of what caused the arena to be resolved. For example, if a member resolves the arena itself, that member still receives an [acceptGesture] callback.

### acceptGesture()

```dart
void acceptGesture(int pointer)
```

Called when this member wins the arena for the given pointer id.

### rejectGesture()

```dart
void rejectGesture(int pointer)
```

Called when this member loses the arena for the given pointer id.

# GestureArenaEntry

```dart
class GestureArenaEntry {}
```

An interface to pass information to an arena.

A given [GestureArenaMember] can have multiple entries in multiple arenas with different pointer ids.

### resolve()

```dart
void resolve(GestureDisposition disposition)
```

Call this member to claim victory (with accepted) or admit defeat (with rejected).

It's fine to attempt to resolve a gesture recognizer for an arena that is already resolved.

# GestureArenaManager

```dart
class GestureArenaManager {}
```

Used for disambiguating the meaning of sequences of pointer events.

{@youtube 560 315 https://www.youtube.com/watch?v=Q85LBtBdi0U}

The first member to accept or the last member to not reject wins.

See <https://flutter.dev/to/gesture-disambiguation> for more information about the role this class plays in the gesture system.

To debug problems with gestures, consider using [debugPrintGestureArenaDiagnostics].

### add()

```dart
GestureArenaEntry add(int pointer, GestureArenaMember member)
```

Adds a new member (e.g., gesture recognizer) to the arena.

### close()

```dart
void close(int pointer)
```

Prevents new members from entering the arena.

Called after the framework has finished dispatching the pointer down event.

### sweep()

```dart
void sweep(int pointer)
```

Forces resolution of the arena, giving the win to the first member.

Sweep is typically after all the other processing for a [PointerUpEvent] have taken place. It ensures that multiple passive gestures do not cause a stalemate that prevents the user from interacting with the app.

Recognizers that wish to delay resolving an arena past [PointerUpEvent] should call [hold] to delay sweep until [release] is called.

See also:

- [hold]
- [release]

### hold()

```dart
void hold(int pointer)
```

Prevents the arena from being swept.

Typically, a winner is chosen in an arena after all the other [PointerUpEvent] processing by [sweep]. If a recognizer wishes to delay resolving an arena past [PointerUpEvent], the recognizer can [hold] the arena open using this function. To release such a hold and let the arena resolve, call [release].

See also:

- [sweep]
- [release]

### release()

```dart
void release(int pointer)
```

Releases a hold, allowing the arena to be swept.

If a sweep was attempted on a held arena, the sweep will be done on release.

See also:

- [sweep]
- [hold]
