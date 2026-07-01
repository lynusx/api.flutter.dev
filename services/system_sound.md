# SystemSoundType

```dart
enum SystemSoundType {}
```

A sound provided by the system.

These sounds may be played with [SystemSound.play].

A short indication that a button was pressed.

A short indication that a picker value was changed.

This is ignored on all platforms except iOS.

A short system alert sound indicating the need for user attention.

Desktop platforms are the only platforms that support a system alert sound, so on mobile platforms (Android, iOS), this will be ignored. The web platform does not support playing any sounds, so this will be ignored on the web as well.

# SystemSound

```dart
abstract final class SystemSound {}
```

Provides access to the library of short system specific sounds for common tasks.

### play()

```dart
Future<void> play(SystemSoundType type)
```

Play the specified system sound. If that sound is not present on the system, the call is ignored.

The web platform currently does not support playing sounds, so this call will yield no behavior on that platform.
