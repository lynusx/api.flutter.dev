@docImport 'package:flutter/widgets.dart';

# DebugPrintCallback

```dart
typedef DebugPrintCallback = void Function(String? message, {int? wrapWidth})
```

Signature for [debugPrint] implementations.

If a [wrapWidth] is provided, each line of the [message] is word-wrapped to that width. (Lines may be separated by newline characters, as in '\n'.)

By default, this function very crudely attempts to throttle the rate at which messages are sent to avoid data loss on Android. This means that interleaving calls to this function (directly or indirectly via, e.g., [debugDumpRenderTree] or [debugDumpApp]) and to the Dart [print] method can result in out-of-order messages in the logs.

The implementation of this function can be replaced by setting the [debugPrint] variable to a new implementation that matches the [DebugPrintCallback] signature. For example, flutter_test does this.

The default value is [debugPrintThrottled]. For a version that acts identically but does not throttle, use [debugPrintSynchronously].

# debugPrint

```dart
DebugPrintCallback debugPrint
```

Prints a message to the console, which you can access using the "flutter" tool's "logs" command ("flutter logs").

The [debugPrint] function logs to console even in [release mode](https://docs.flutter.dev/testing/build-modes#release). As per convention, calls to [debugPrint] should be within a debug mode check or an assert:

```dart
if (kDebugMode) {
  debugPrint('A useful message');
}
```

See also:

- [DebugPrintCallback], for function parameters and usage details.
- [debugPrintThrottled], the default implementation.
- [ErrorToConsoleDumper], for error messages dumped to the console.

# debugPrintSynchronously()

```dart
void debugPrintSynchronously(String? message, {int? wrapWidth})
```

Alternative implementation of [debugPrint] that does not throttle.

Used by tests.

# debugPrintThrottled()

```dart
void debugPrintThrottled(String? message, {int? wrapWidth})
```

Implementation of [debugPrint] that throttles messages.

This avoids dropping messages on platforms that rate-limit their logging (for example, Android).

If `wrapWidth` is not null, the message is wrapped using [debugWordWrap].

# debugPrintDone

```dart
Future<void> get debugPrintDone
```

A Future that resolves when there is no longer any buffered content being printed by [debugPrintThrottled] (which is the default implementation for [debugPrint], which is used to report errors to the console).

# debugWordWrap()

```dart
Iterable<String> debugWordWrap(String message, int width, {String wrapIndent = ''})
```

Wraps the given string at the given width.

The `message` should not contain newlines (`\n`, U+000A). Strings that may contain newlines should be [String.split] before being wrapped.

Wrapping occurs at space characters (U+0020). Lines that start with an octothorpe ("#", U+0023) are not wrapped (so for example, Dart stack traces won't be wrapped).

Subsequent lines attempt to duplicate the indentation of the first line, for example if the first line starts with multiple spaces. In addition, if a `wrapIndent` argument is provided, each line after the first is prefixed by that string.

This is not suitable for use with arbitrary Unicode text. For example, it doesn't implement UAX #14, can't handle ideographic text, doesn't hyphenate, and so forth. It is only intended for formatting error messages.

The default [debugPrint] implementation uses this for its line wrapping.
