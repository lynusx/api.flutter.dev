# StackFrame

```dart
class StackFrame {}
```

A object representation of a frame from a stack trace.

{@tool snippet}

This example creates a traversable list of parsed [StackFrame] objects from the current [StackTrace].

```dart
final List<StackFrame> currentFrames = StackFrame.fromStackTrace(StackTrace.current);
```

{@end-tool}

### StackFrame()

```dart
StackFrame({required int number, required int column, required int line, required String packageScheme, required String package, required String packagePath, String className = '', required String method, bool isConstructor = false, required String source})
```

Creates a new StackFrame instance.

The [className] may be the empty string if there is no class (e.g. for a top level library method).

### asynchronousSuspension

```dart
StackFrame asynchronousSuspension
```

A stack frame representing an asynchronous suspension.

### stackOverFlowElision

```dart
StackFrame stackOverFlowElision
```

A stack frame representing a Dart elided stack overflow frame.

### fromStackTrace()

```dart
List<StackFrame> fromStackTrace(StackTrace stack)
```

Parses a list of [StackFrame]s from a [StackTrace] object.

This is normally useful with [StackTrace.current].

### fromStackString()

```dart
List<StackFrame> fromStackString(String stack)
```

Parses a list of [StackFrame]s from the [StackTrace.toString] method.

### fromStackTraceLine()

```dart
StackFrame? fromStackTraceLine(String line)
```

Parses a single [StackFrame] from a single line of a [StackTrace].

Returns null if format is not as expected.

### source

```dart
String source
```

The original source of this stack frame.

### number

```dart
int number
```

The zero-indexed frame number.

This value may be -1 to indicate an unknown frame number.

### packageScheme

```dart
String packageScheme
```

The scheme of the package for this frame, e.g. "dart" for dart:core/errors_patch.dart or "package" for package:flutter/src/widgets/text.dart.

The path property refers to the source file.

### package

```dart
String package
```

The package for this frame, e.g. "core" for dart:core/errors_patch.dart or "flutter" for package:flutter/src/widgets/text.dart.

### packagePath

```dart
String packagePath
```

The path of the file for this frame, e.g. "errors_patch.dart" for dart:core/errors_patch.dart or "src/widgets/text.dart" for package:flutter/src/widgets/text.dart.

### line

```dart
int line
```

The source line number.

### column

```dart
int column
```

The source column number.

### className

```dart
String className
```

The class name, if any, for this frame.

This may be null for top level methods in a library or anonymous closure methods.

### method

```dart
String method
```

The method name for this frame.

This will be an empty string if the stack frame is from the default constructor.

### isConstructor

```dart
bool isConstructor
```

Whether or not this was thrown from a constructor.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### toString()

```dart
String toString()
```
