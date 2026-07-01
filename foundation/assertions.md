@docImport 'package:flutter/widgets.dart';

# FlutterExceptionHandler

```dart
typedef FlutterExceptionHandler = void Function(FlutterErrorDetails details)
```

Signature for [FlutterError.onError] handler.

# DiagnosticPropertiesTransformer

```dart
typedef DiagnosticPropertiesTransformer = Iterable<DiagnosticsNode> Function(Iterable<DiagnosticsNode> properties)
```

Signature for [DiagnosticPropertiesBuilder] transformer.

# InformationCollector

```dart
typedef InformationCollector = Iterable<DiagnosticsNode> Function()
```

Signature for [FlutterErrorDetails.informationCollector] callback and other callbacks that collect information describing an error.

# StackTraceDemangler

```dart
typedef StackTraceDemangler = StackTrace Function(StackTrace details)
```

Signature for a function that demangles [StackTrace] objects into a format that can be parsed by [StackFrame].

See also:

- [FlutterError.demangleStackTrace], which shows an example implementation.

# PartialStackFrame

```dart
class PartialStackFrame {}
```

Partial information from a stack frame for stack filtering purposes.

See also:

- [RepetitiveStackFrameFilter], which uses this class to compare against [StackFrame]s.

### PartialStackFrame()

```dart
PartialStackFrame({required Pattern package, required String className, required String method})
```

Creates a new [PartialStackFrame] instance.

### asynchronousSuspension

```dart
PartialStackFrame asynchronousSuspension
```

An `<asynchronous suspension>` line in a stack trace.

### package

```dart
Pattern package
```

The package to match, e.g. `package:flutter/src/foundation/assertions.dart`, or `dart:ui/window.dart`.

### className

```dart
String className
```

The class name for the method.

On web, this is ignored, since class names are not available.

On all platforms, top level methods should use the empty string.

### method

```dart
String method
```

The method name for this frame line.

On web, private methods are wrapped with `[]`.

### matches()

```dart
bool matches(StackFrame stackFrame)
```

Tests whether the [StackFrame] matches the information in this [PartialStackFrame].

# StackFilter

```dart
abstract class StackFilter {}
```

A class that filters stack frames for additional filtering on [FlutterError.defaultStackFilter].

### StackFilter()

```dart
StackFilter()
```

This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### filter()

```dart
void filter(List<StackFrame> stackFrames, List<String?> reasons)
```

Filters the list of [StackFrame]s by updating corresponding indices in `reasons`.

To elide a frame or number of frames, set the string.

# RepetitiveStackFrameFilter

```dart
class RepetitiveStackFrameFilter extends StackFilter {}
```

A [StackFilter] that filters based on repeating lists of [PartialStackFrame]s.

See also:

- [FlutterError.addDefaultStackFilter], a method to register additional stack filters for [FlutterError.defaultStackFilter].
- [StackFrame], a class that can help with parsing stack frames.
- [PartialStackFrame], a class that helps match partial method information to a stack frame.

### RepetitiveStackFrameFilter()

```dart
RepetitiveStackFrameFilter({required List<PartialStackFrame> frames, required String replacement})
```

Creates a new RepetitiveStackFrameFilter.

### frames

```dart
List<PartialStackFrame> frames
```

The shape of this repetitive stack pattern.

### numFrames

```dart
int get numFrames
```

The number of frames in this pattern.

### replacement

```dart
String replacement
```

The string to replace the frames with.

If the same replacement string is used multiple times in a row, the [FlutterError.defaultStackFilter] will insert a repeat count after this line rather than repeating it.

### filter()

```dart
void filter(List<StackFrame> stackFrames, List<String?> reasons)
```

# ErrorDescription

```dart
class ErrorDescription extends _ErrorDiagnostic {}
```

An explanation of the problem and its cause, any information that may help track down the problem, background information, etc.

Use [ErrorDescription] for any part of an error message where neither [ErrorSummary] or [ErrorHint] is appropriate.

In debug builds, values interpolated into the `message` are expanded and placed into [value], which is of type [List<Object>]. This allows IDEs to examine values interpolated into error messages.

See also:

- [ErrorSummary], which provides a short (one line) description of the problem that was detected.
- [ErrorHint], which provides specific, non-obvious advice that may be applicable.
- [ErrorSpacer], which renders as a blank line.
- [FlutterError], which is the most common place to use an [ErrorDescription].

### ErrorDescription()

```dart
ErrorDescription(String message)
```

A lint enforces that this constructor can only be called with a string literal to match the limitations of the Dart Kernel transformer that optionally extracts out objects referenced using string interpolation in the message passed in.

The message will display with the same text regardless of whether the kernel transformer is used. The kernel transformer is required so that debugging tools can provide interactive displays of objects described by the error.

# ErrorSummary

```dart
class ErrorSummary extends _ErrorDiagnostic {}
```

A short (one line) description of the problem that was detected.

Error summaries from the same source location should have little variance, so that they can be recognized as related. For example, they shouldn't include hash codes.

A [FlutterError] must start with an [ErrorSummary] and may not contain multiple summaries.

In debug builds, values interpolated into the `message` are expanded and placed into [value], which is of type [List<Object>]. This allows IDEs to examine values interpolated into error messages.

See also:

- [ErrorDescription], which provides an explanation of the problem and its cause, any information that may help track down the problem, background information, etc.
- [ErrorHint], which provides specific, non-obvious advice that may be applicable.
- [FlutterError], which is the most common place to use an [ErrorSummary].

### ErrorSummary()

```dart
ErrorSummary(String message)
```

A lint enforces that this constructor can only be called with a string literal to match the limitations of the Dart Kernel transformer that optionally extracts out objects referenced using string interpolation in the message passed in.

The message will display with the same text regardless of whether the kernel transformer is used. The kernel transformer is required so that debugging tools can provide interactive displays of objects described by the error.

# ErrorHint

```dart
class ErrorHint extends _ErrorDiagnostic {}
```

An [ErrorHint] provides specific, non-obvious advice that may be applicable.

If your message provides obvious advice that is always applicable, it is an [ErrorDescription] not a hint.

In debug builds, values interpolated into the `message` are expanded and placed into [value], which is of type [List<Object>]. This allows IDEs to examine values interpolated into error messages.

See also:

- [ErrorSummary], which provides a short (one line) description of the problem that was detected.
- [ErrorDescription], which provides an explanation of the problem and its cause, any information that may help track down the problem, background information, etc.
- [ErrorSpacer], which renders as a blank line.
- [FlutterError], which is the most common place to use an [ErrorHint].

### ErrorHint()

```dart
ErrorHint(String message)
```

A lint enforces that this constructor can only be called with a string literal to match the limitations of the Dart Kernel transformer that optionally extracts out objects referenced using string interpolation in the message passed in.

The message will display with the same text regardless of whether the kernel transformer is used. The kernel transformer is required so that debugging tools can provide interactive displays of objects described by the error.

# ErrorSpacer

```dart
class ErrorSpacer extends DiagnosticsProperty<void> {}
```

An [ErrorSpacer] creates an empty [DiagnosticsNode], that can be used to tune the spacing between other [DiagnosticsNode] objects.

### ErrorSpacer()

```dart
ErrorSpacer()
```

Creates an empty space to insert into a list of [DiagnosticsNode] objects typically within a [FlutterError] object.

# FlutterErrorDetails

```dart
class FlutterErrorDetails with Diagnosticable {}
```

Class for information provided to [FlutterExceptionHandler] callbacks.

{@tool snippet} This is an example of using [FlutterErrorDetails] when calling [FlutterError.reportError].

```dart
void main() {
  try {
    // Try to do something!
  } catch (error) {
    // Catch & report error.
    FlutterError.reportError(FlutterErrorDetails(
      exception: error,
      library: 'Flutter test framework',
      context: ErrorSummary('while running async test code'),
    ));
  }
}
```

{@end-tool}

See also:

- [FlutterError.onError], which is called whenever the Flutter framework catches an error.

### FlutterErrorDetails()

```dart
FlutterErrorDetails({required Object exception, StackTrace? stack, String? library = 'Flutter framework', DiagnosticsNode? context, IterableFilter<String>? stackFilter, InformationCollector? informationCollector, bool silent = false})
```

Creates a [FlutterErrorDetails] object with the given arguments setting the object's properties.

The framework calls this constructor when catching an exception that will subsequently be reported using [FlutterError.onError].

### copyWith()

```dart
FlutterErrorDetails copyWith({DiagnosticsNode? context, Object? exception, InformationCollector? informationCollector, String? library, bool? silent, StackTrace? stack, IterableFilter<String>? stackFilter})
```

Creates a copy of the error details but with the given fields replaced with new values.

### propertiesTransformers

```dart
List<DiagnosticPropertiesTransformer> propertiesTransformers
```

Transformers to transform [DiagnosticsNode] in [DiagnosticPropertiesBuilder] into a more descriptive form.

There are layers that attach certain [DiagnosticsNode] into [FlutterErrorDetails] that require knowledge from other layers to parse. To correctly interpret those [DiagnosticsNode], register transformers in the layers that possess the knowledge.

See also:

- [WidgetsBinding.initInstances], which registers its transformer.

### exception

```dart
Object exception
```

The exception.

Often this will be an [AssertionError], maybe specifically a [FlutterError]. However, this could be any value at all.

### stack

```dart
StackTrace? stack
```

The stack trace from where the [exception] was thrown (as opposed to where it was caught).

StackTrace objects are opaque except for their [toString] function.

If this field is not null, then the [stackFilter] callback, if any, will be called with the result of calling [toString] on this object and splitting that result on line breaks. If there's no [stackFilter] callback, then [FlutterError.defaultStackFilter] is used instead. That function expects the stack to be in the format used by [StackTrace.toString].

### library

```dart
String? library
```

A human-readable brief name describing the library that caught the error message.

This is used by the default error handler in the header dumped to the console.

### context

```dart
DiagnosticsNode? context
```

A [DiagnosticsNode] that provides a human-readable description of where the error was caught (as opposed to where it was thrown).

The node, e.g. an [ErrorDescription], should be in a form that will make sense in English when following the word "thrown", as in "thrown while obtaining the image from the network" (for the context "while obtaining the image from the network").

{@tool snippet} This is an example of using and [ErrorDescription] as the [FlutterErrorDetails.context] when calling [FlutterError.reportError].

```dart
void maybeDoSomething() {
  try {
    // Try to do something!
  } catch (error) {
    // Catch & report error.
    FlutterError.reportError(FlutterErrorDetails(
      exception: error,
      library: 'Flutter test framework',
      context: ErrorDescription('while dispatching notifications for $runtimeType'),
    ));
  }
}
```

{@end-tool}

See also:

- [ErrorDescription], which provides an explanation of the problem and its cause, any information that may help track down the problem, background information, etc.
- [ErrorSummary], which provides a short (one line) description of the problem that was detected.
- [ErrorHint], which provides specific, non-obvious advice that may be applicable.
- [FlutterError], which is the most common place to use [FlutterErrorDetails].

### stackFilter

```dart
IterableFilter<String>? stackFilter
```

A callback which filters the [stack] trace.

Receives an iterable of strings representing the frames encoded in the way that [StackTrace.toString()] provides. Should return an iterable of lines to output for the stack.

If this is not provided, then [FlutterError.dumpErrorToConsole] will use [FlutterError.defaultStackFilter] instead.

If the [FlutterError.defaultStackFilter] behavior is desired, then the callback should manually call that function. That function expects the incoming list to be in the [StackTrace.toString()] format. The output of that function, however, does not always follow this format.

This won't be called if [stack] is null.

### informationCollector

```dart
InformationCollector? informationCollector
```

A callback which will provide information that could help with debugging the problem.

Information collector callbacks can be expensive, so the generated information should be cached by the caller, rather than the callback being called multiple times.

The callback is expected to return an iterable of [DiagnosticsNode] objects, typically implemented using `sync*` and `yield`.

{@tool snippet} In this example, the information collector returns two pieces of information, one broadly-applicable statement regarding how the error happened, and one giving a specific piece of information that may be useful in some cases but may also be irrelevant most of the time (an argument to the method).

```dart
void climbElevator(int pid) {
  try {
    // ...
  } catch (error, stack) {
    FlutterError.reportError(FlutterErrorDetails(
      exception: error,
      stack: stack,
      informationCollector: () => <DiagnosticsNode>[
        ErrorDescription('This happened while climbing the space elevator.'),
        ErrorHint('The process ID is: $pid'),
      ],
    ));
  }
}
```

{@end-tool}

The following classes may be of particular use:

- [ErrorDescription], for information that is broadly applicable to the situation being described.
- [ErrorHint], for specific information that may not always be applicable but can be helpful in certain situations.
- [DiagnosticsStackTrace], for reporting stack traces.
- [ErrorSpacer], for adding spaces (a blank line) between other items.

For objects that implement [Diagnosticable] one may consider providing additional information by yielding the output of the object's [Diagnosticable.toDiagnosticsNode] method.

### silent

```dart
bool silent
```

Whether this error should be ignored by the default error reporting behavior in release mode.

If this is false, the default, then the default error handler will always dump this error to the console.

If this is true, then the default error handler would only dump this error to the console in debug mode. In release mode, the error is ignored.

This is used by certain exception handlers that catch errors that could be triggered by environmental conditions (as opposed to logic errors). For example, the HTTP library sets this flag so as to not report every 404 error to the console on end-user devices, while still allowing a custom error handler to see the errors even in release builds.

### exceptionAsString()

```dart
String exceptionAsString()
```

Converts the [exception] to a string.

This applies some additional logic to make [AssertionError] exceptions prettier, to handle exceptions that stringify to empty strings, to handle objects that don't inherit from [Exception] or [Error], and so forth.

### summary

```dart
DiagnosticsNode get summary
```

Returns a short (one line) description of the problem that was detected.

If the exception contains an [ErrorSummary] that summary is used, otherwise the summary is inferred from the string representation of the exception.

In release mode, this always returns a [DiagnosticsNode.message] with a formatted version of the exception.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toStringShort()

```dart
String toStringShort()
```

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style})
```

# FlutterError

```dart
class FlutterError extends Error with DiagnosticableTreeMixin implements AssertionError {}
```

Error class used to report Flutter-specific assertion failures and contract violations.

See also:

- <https://docs.flutter.dev/testing/errors>, more information about error handling in Flutter.

### FlutterError()

```dart
FlutterError(String message)
```

Create an error message from a string.

The message may have newlines in it. The first line should be a terse description of the error, e.g. "Incorrect GlobalKey usage" or "setState() or markNeedsBuild() called during build". Subsequent lines should contain substantial additional information, ideally sufficient to develop a correct solution to the problem.

In some cases, when a [FlutterError] is reported to the user, only the first line is included. For example, Flutter will typically only fully report the first exception at runtime, displaying only the first line of subsequent errors.

All sentences in the error should be correctly punctuated (i.e., do end the error message with a period).

This constructor defers to the [FlutterError.fromParts] constructor. The first line is wrapped in an implied [ErrorSummary], and subsequent lines are wrapped in implied [ErrorDescription]s. Consider using the [FlutterError.fromParts] constructor to provide more detail, e.g. using [ErrorHint]s or other [DiagnosticsNode]s.

### FlutterError.fromParts()

```dart
FlutterError.fromParts(List<DiagnosticsNode> diagnostics)
```

Create an error message from a list of [DiagnosticsNode]s.

By convention, there should be exactly one [ErrorSummary] in the list, and it should be the first entry.

Other entries are typically [ErrorDescription]s (for material that is always applicable for this error) and [ErrorHint]s (for material that may be sometimes useful, but may not always apply). Other [DiagnosticsNode] subclasses, such as [DiagnosticsStackTrace], may also be used.

When using an [ErrorSummary], [ErrorDescription]s, and [ErrorHint]s, in debug builds, values interpolated into the `message` arguments of those classes' constructors are expanded and placed into the [DiagnosticsProperty.value] property of those objects (which is of type [List<Object>]). This allows IDEs to examine values interpolated into error messages.

Alternatively, to include a specific [Diagnosticable] object into the error message and have the object describe itself in detail (see [DiagnosticsNode.toStringDeep]), consider calling [Diagnosticable.toDiagnosticsNode] on that object and using that as one of the values passed to this constructor.

{@tool snippet} In this example, an error is thrown in debug mode if certain conditions are not met. The error message includes a description of an object that implements the [Diagnosticable] interface, `draconis`.

```dart
void controlDraconis() {
  assert(() {
    if (!draconisAlive || !draconisAmulet) {
      throw FlutterError.fromParts(<DiagnosticsNode>[
        ErrorSummary('Cannot control Draconis in current state.'),
        ErrorDescription('Draconis can only be controlled while alive and while the amulet is wielded.'),
        if (!draconisAlive)
          ErrorHint('Draconis is currently not alive.'),
        if (!draconisAmulet)
          ErrorHint('The Amulet of Draconis is currently not wielded.'),
        draconis.toDiagnosticsNode(name: 'Draconis'),
      ]);
    }
    return true;
  }());
  // ...
}
```

{@end-tool}

### diagnostics

```dart
List<DiagnosticsNode> diagnostics
```

The information associated with this error, in structured form.

The first node is typically an [ErrorSummary] giving a short description of the problem, suitable for an index of errors, a log, etc.

Subsequent nodes should give information specific to this error. Typically these will be [ErrorDescription]s or [ErrorHint]s, but they could be other objects also. For instance, an error relating to a timer could include a stack trace of when the timer was scheduled using the [DiagnosticsStackTrace] class.

### message

```dart
String get message
```

The message associated with this error.

This is generated by serializing the [diagnostics].

### onError

```dart
FlutterExceptionHandler? onError
```

Called whenever the Flutter framework catches an error.

The default behavior is to call [presentError].

You can set this to your own function to override this default behavior. For example, you could report all errors to your server. Consider calling [presentError] from your custom error handler in order to see the logs in the console as well.

If the error handler throws an exception, it will not be caught by the Flutter framework.

Set this to null to silently catch and ignore errors. This is not recommended.

Do not call [onError] directly, instead, call [reportError], which forwards to [onError] if it is not null.

See also:

- <https://docs.flutter.dev/testing/errors>, more information about error handling in Flutter.

### demangleStackTrace

```dart
StackTraceDemangler demangleStackTrace
```

Called by the Flutter framework before attempting to parse a [StackTrace].

Some [StackTrace] implementations have a different [toString] format from what the framework expects, like ones from `package:stack_trace`. To make sure we can still parse and filter mangled [StackTrace]s, the framework first calls this function to demangle them.

This should be set in any environment that could propagate an unusual stack trace to the framework. Otherwise, the default behavior is to assume all stack traces are in a format usually generated by Dart.

The following example demangles `package:stack_trace` traces by converting them into VM traces, which the framework is able to parse:

```dart
FlutterError.demangleStackTrace = (StackTrace stack) {
  // Trace and Chain are classes in package:stack_trace
  if (stack is Trace) {
    return stack.vmTrace;
  }
  if (stack is Chain) {
    return stack.toTrace().vmTrace;
  }
  return stack;
};
```

### presentError

```dart
FlutterExceptionHandler presentError
```

Called whenever the Flutter framework wants to present an error to the users.

The default behavior is to call [dumpErrorToConsole].

Plugins can override how an error is to be presented to the user. For example, the structured errors service extension sets its own method when the extension is enabled. If you want to change how Flutter responds to an error, use [onError] instead.

### resetErrorCount()

```dart
void resetErrorCount()
```

Resets the count of errors used by [dumpErrorToConsole] to decide whether to show a complete error message or an abbreviated one.

After this is called, the next error message will be shown in full.

### wrapWidth

```dart
int wrapWidth
```

The width to which [dumpErrorToConsole] will wrap lines.

This can be used to ensure strings will not exceed the length at which they will wrap, e.g. when placing ASCII art diagrams in messages.

### dumpErrorToConsole()

```dart
void dumpErrorToConsole(FlutterErrorDetails details, {bool forceReport = false})
```

Prints the given exception details to the console.

The first time this is called, it dumps a very verbose message to the console using [debugPrint].

Subsequent calls only dump the first line of the exception, unless `forceReport` is set to true (in which case it dumps the verbose message).

Call [resetErrorCount] to cause this method to go back to acting as if it had not been called before (so the next message is verbose again).

The default behavior for the [onError] handler is to call this function.

### addDefaultStackFilter()

```dart
void addDefaultStackFilter(StackFilter filter)
```

Adds a stack filtering function to [defaultStackFilter].

For example, the framework adds common patterns of element building to elide tree-walking patterns in the stack trace.

Added filters are checked in order of addition. The first matching filter wins, and subsequent filters will not be checked.

### defaultStackFilter()

```dart
Iterable<String> defaultStackFilter(Iterable<String> frames)
```

Converts a stack to a string that is more readable by omitting stack frames that correspond to Dart internals.

This is the default filter used by [dumpErrorToConsole] if the [FlutterErrorDetails] object has no [FlutterErrorDetails.stackFilter] callback.

This function expects its input to be in the format used by [StackTrace.toString()]. The output of this function is similar to that format but the frame numbers will not be consecutive (frames are elided) and the final line may be prose rather than a stack frame.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toStringShort()

```dart
String toStringShort()
```

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### reportError()

```dart
void reportError(FlutterErrorDetails details)
```

Calls [onError] with the given details, unless it is null.

{@tool snippet} When calling this from a `catch` block consider annotating the method containing the `catch` block with `@pragma('vm:notify-debugger-on-exception')` to allow an attached debugger to treat the exception as unhandled. This means instead of executing the `catch` block, the debugger can break at the original source location from which the exception was thrown.

```dart
@pragma('vm:notify-debugger-on-exception')
void doSomething() {
  try {
    methodThatMayThrow();
  } catch (exception, stack) {
    FlutterError.reportError(FlutterErrorDetails(
      exception: exception,
      stack: stack,
      library: 'example library',
      context: ErrorDescription('while doing something'),
    ));
  }
}
```

{@end-tool}

# debugPrintStack()

```dart
void debugPrintStack({StackTrace? stackTrace, String? label, int? maxFrames})
```

Dump the stack to the console using [debugPrint] and [FlutterError.defaultStackFilter].

If the `stackTrace` parameter is null, the [StackTrace.current] is used to obtain the stack.

The `maxFrames` argument can be given to limit the stack to the given number of lines before filtering is applied. By default, all stack lines are included.

The `label` argument, if present, will be printed before the stack.

# DiagnosticsStackTrace

```dart
class DiagnosticsStackTrace extends DiagnosticsBlock {}
```

Diagnostic with a [StackTrace] [value] suitable for displaying stack traces as part of a [FlutterError] object.

### DiagnosticsStackTrace()

```dart
DiagnosticsStackTrace(String name, StackTrace? stack, {IterableFilter<String>? stackFilter, bool showSeparator})
```

Creates a diagnostic for a stack trace.

[name] describes a name the stack trace is given, e.g. `When the exception was thrown, this was the stack`. [stackFilter] provides an optional filter to use to filter which frames are included. If no filter is specified, [FlutterError.defaultStackFilter] is used. [showSeparator] indicates whether to include a ':' after the [name].

### DiagnosticsStackTrace.singleFrame()

```dart
DiagnosticsStackTrace.singleFrame(String name, {required String frame, bool showSeparator})
```

Creates a diagnostic describing a single frame from a StackTrace.

### allowTruncate

```dart
bool get allowTruncate
```
