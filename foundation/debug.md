@docImport 'dart:developer';

@docImport 'package:flutter/foundation.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/widgets.dart';

# debugAssertAllFoundationVarsUnset()

```dart
bool debugAssertAllFoundationVarsUnset(String reason, {DebugPrintCallback debugPrintOverride = debugPrintThrottled})
```

Returns true if none of the foundation library debug variables have been changed.

This function is used by the test framework to ensure that debug variables haven't been inadvertently changed.

The `debugPrintOverride` argument can be specified to indicate the expected value of the [debugPrint] variable. This is useful for test frameworks that override [debugPrint] themselves and want to check that their own custom value wasn't overridden by a test.

See [the foundation library](foundation/foundation-library.html) for a complete list.

# debugInstrumentationEnabled

```dart
bool debugInstrumentationEnabled
```

Boolean value indicating whether [debugInstrumentAction] will instrument actions in debug builds.

The framework does not use [debugInstrumentAction] internally, so this does not enable any additional instrumentation for the framework itself.

See also:

- [debugProfileBuildsEnabled], which enables additional tracing of builds in [Widget]s.
- [debugProfileLayoutsEnabled], which enables additional tracing of layout events in [RenderObject]s.
- [debugProfilePaintsEnabled], which enables additional tracing of paint events in [RenderObject]s.

# debugInstrumentAction()

```dart
Future<T> debugInstrumentAction<T>(String description, Future<T> Function() action)
```

Runs the specified [action], timing how long the action takes in debug builds when [debugInstrumentationEnabled] is true.

The instrumentation will be printed to the logs using [debugPrint]. In non-debug builds, or when [debugInstrumentationEnabled] is false, this will run [action] without any instrumentation.

Returns the result of running [action].

See also:

- [Timeline], which is used to record synchronous tracing events for visualization in Chrome's tracing format. This method does not implicitly add any timeline events.

# debugDoublePrecision

```dart
int? debugDoublePrecision
```

Configure [debugFormatDouble] using [num.toStringAsPrecision].

Defaults to null, which uses the default logic of [debugFormatDouble].

# debugFormatDouble()

```dart
String debugFormatDouble(double? value)
```

Formats a double to have standard formatting.

This behavior can be overridden by [debugDoublePrecision].

# debugBrightnessOverride

```dart
ui.Brightness? debugBrightnessOverride
```

A setting that can be used to override the platform [Brightness] exposed from [BindingBase.platformDispatcher].

See also:

- [WidgetsApp], which uses the [debugBrightnessOverride] setting in debug mode to construct a [MediaQueryData].

# activeDevToolsServerAddress

```dart
String? activeDevToolsServerAddress
```

The address for the active DevTools server used for debugging this application.

# connectedVmServiceUri

```dart
String? connectedVmServiceUri
```

The uri for the connected vm service protocol.

# debugMaybeDispatchCreated()

```dart
bool debugMaybeDispatchCreated(String flutterLibrary, String className, Object object)
```

If memory allocation tracking is enabled, dispatch Flutter object creation.

This method is not member of FlutterMemoryAllocations, because [FlutterMemoryAllocations] should not increase size of the Flutter application if memory allocations are disabled.

The [flutterLibrary] argument is the name of the Flutter library where the object is declared. For example, 'widgets' for widgets.dart.

Should be called only from within an assert and only inside Flutter Framework.

Returns true to make it easier to be wrapped into `assert`.

# debugMaybeDispatchDisposed()

```dart
bool debugMaybeDispatchDisposed(Object object)
```

If memory allocations tracking is enabled, dispatch object disposal.

Should be called only from within an assert.

Returns true to make it easier to be wrapped into `assert`.
