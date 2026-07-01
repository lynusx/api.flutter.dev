# ErrorToConsoleDumper

```dart
class ErrorToConsoleDumper {}
```

Dumps error messages to the console.

### dump()

```dart
void dump(String message)
```

Dumps the given error [message] to the console.

### addWebDumpListener()

```dart
void addWebDumpListener(void Function(String message) listener)
```

Adds a listener that captures error messages being dumped on the web.

### clearWebDumpListeners()

```dart
void clearWebDumpListeners()
```

Clears all listeners that capture error messages being dumped on the web.
