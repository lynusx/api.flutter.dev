@docImport 'dart:convert'; @docImport 'dart:ui';

@docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/scheduler.dart'; @docImport 'package:flutter/services.dart'; @docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# ServiceExtensionCallback

```dart
typedef ServiceExtensionCallback = Future<Map<String, dynamic>> Function(Map<String, String> parameters)
```

Signature for service extensions.

The returned map must not contain the keys "type" or "method", as they will be replaced before the value is sent to the client. The "type" key will be set to the string `_extensionType` to indicate that this is a return value from a service extension, and the "method" key will be set to the full name of the method.

# BindingBase

```dart
abstract class BindingBase {}
```

Base class for mixins that provide singleton services.

The Flutter engine ([dart:ui]) exposes some low-level services, but these are typically not suitable for direct use, for example because they only provide a single callback which an application may wish to multiplex to allow multiple listeners.

Bindings provide the glue between these low-level APIs and the higher-level framework APIs. They _bind_ the two together, whence the name.

## Implementing a binding mixin

A library would typically create a new binding mixin to expose a feature in [dart:ui]. This is rare in general, but it is something that an alternative framework would do, e.g. if a framework were to replace the [widgets] library with an alternative API but still wished to leverage the [services] and [foundation] libraries.

To create a binding mixin, declare a mixin `on` the [BindingBase] class and whatever other bindings the concrete binding must implement for this binding mixin to be useful.

The mixin is guaranteed to only be constructed once in the lifetime of the app; this is handled by [initInstances].

A binding mixin must at a minimum implement the following features:

- The [initInstances] method, which must call `super.initInstances` and set an `_instance` static field to `this`.
- An `instance` static getter, which must return that field using [checkInstance].

In addition, it should implement whatever singleton features the library needs.

As a general rule, the less can be placed in the binding, the better. Prefer having APIs that takes objects rather than having them refer to global singletons. Bindings are best limited to exposing features that literally only exist once, for example, the APIs in [dart:ui].

{@tool snippet}

Here is a basic example of a binding that implements these features. It relies on another fictional binding called `BarBinding`.

```dart
mixin FooBinding on BindingBase, BarBinding {
  @override
  void initInstances() {
    super.initInstances();
    _instance = this;
    // ...binding initialization...
  }

  static FooBinding get instance => BindingBase.checkInstance(_instance);
  static FooBinding? _instance;

  // ...binding features...
}
```

{@end-tool}

## Implementing a binding class

The top-most layer used to write the application (e.g. the Flutter [widgets] library) will have a concrete class that inherits from [BindingBase] and uses all the various [BindingBase] mixins (such as [ServicesBinding]). The [widgets] library in Flutter introduces a binding called [WidgetsFlutterBinding].

A binding _class_ should mix in the relevant bindings from each layer that it wishes to expose, and should have an `ensureInitialized` method that constructs the class if that layer's mixin's `_instance` field is null. This allows the binding to be overridden by developers who have more specific needs, while still allowing other code to call `ensureInitialized` when a binding is needed.

{@tool snippet}

A typical binding class is shown below. The `ensureInitialized` method's return type is the library's binding mixin, rather than the concrete class.

```dart
// continuing from previous example...
class FooLibraryBinding extends BindingBase with BarBinding, FooBinding {
  static FooBinding ensureInitialized() {
    if (FooBinding._instance == null) {
      FooLibraryBinding();
    }
    return FooBinding.instance;
  }
}
```

{@end-tool}

### BindingBase()

```dart
BindingBase()
```

Default abstract constructor for bindings.

First calls [initInstances] to have bindings initialize their instance pointers and other state, then calls [initServiceExtensions] to have bindings initialize their VM service extensions, if any.

### window

```dart
ui.SingletonFlutterWindow get window
```

Deprecated; will be removed in a future version of Flutter.

This property has been deprecated to prepare for Flutter's upcoming support for multiple views and multiple windows.

It represents the main view for applications where there is only one view, such as applications designed for single-display mobile devices. If the embedder supports multiple views, it points to the first view created which is assumed to be the main view. It throws if no view has been created yet or if the first view has been removed again.

The following options exists to migrate code that relies on accessing this deprecated property:

If a [BuildContext] is available, consider looking up the current [FlutterView] associated with that context via [View.of]. It gives access to the same functionality as this deprecated property. However, the platform-specific functionality has moved to the [PlatformDispatcher], which may be accessed from the view returned by [View.of] via [FlutterView.platformDispatcher]. Using [View.of] with a [BuildContext] is the preferred option to migrate away from this deprecated [window] property.

If no context is available to look up a [FlutterView], the [platformDispatcher] exposed by this binding can be used directly for platform-specific functionality. It also maintains a list of all available [FlutterView]s in [PlatformDispatcher.views] to access view-specific functionality without a context.

See also:

- [View.of] to access view-specific functionality on the [FlutterView] associated with the provided [BuildContext].
- [FlutterView.platformDispatcher] to access platform-specific functionality from a given [FlutterView].
- [platformDispatcher] on this binding to access the [PlatformDispatcher], which provides platform-specific functionality.

### platformDispatcher

```dart
ui.PlatformDispatcher get platformDispatcher
```

The [ui.PlatformDispatcher] to which this binding is bound.

A number of additional bindings are defined as extensions of [BindingBase], e.g., [ServicesBinding], [RendererBinding], and [WidgetsBinding]. Each of these bindings define behaviors that interact with a [ui.PlatformDispatcher], e.g., [ServicesBinding] registers listeners with the [ChannelBuffers], [RendererBinding] registers [ui.PlatformDispatcher.onMetricsChanged], [ui.PlatformDispatcher.onTextScaleFactorChanged], and [SemanticsBinding] registers [ui.PlatformDispatcher.onSemanticsEnabledChanged], [ui.PlatformDispatcher.onSemanticsActionEvent], and [ui.PlatformDispatcher.onAccessibilityFeaturesChanged] handlers.

Each of these other bindings could individually access a [ui.PlatformDispatcher] statically, but that would preclude the ability to test these behaviors with a fake platform dispatcher for verification purposes. Therefore, [BindingBase] exposes this [ui.PlatformDispatcher] for use by other bindings. A subclass of [BindingBase], such as [TestWidgetsFlutterBinding], can override this accessor to return a different [ui.PlatformDispatcher] implementation.

### initInstances()

```dart
void initInstances()
```

The initialization method.

Subclasses override this method to hook into the platform and otherwise configure their services. Subclasses must call "super.initInstances()".

The binding is not fully initialized when this method runs (for example, other binding mixins may not yet have run their [initInstances] method). For this reason, code in this method should avoid invoking callbacks or synchronously triggering any code that would normally assume that the bindings are ready.

{@tool snippet}

By convention, if the service is to be provided as a singleton, it should be exposed as `MixinClassName.instance`, a static getter with a non-nullable return type that returns `MixinClassName._instance`, a static field that is set by `initInstances()`. To improve the developer experience, the return value should actually be `BindingBase.checkInstance(_instance)` (see [checkInstance]), as in the example below.

```dart
mixin BazBinding on BindingBase {
  @override
  void initInstances() {
    super.initInstances();
    _instance = this;
    // ...binding initialization...
  }

  static BazBinding get instance => BindingBase.checkInstance(_instance);
  static BazBinding? _instance;

  // ...binding features...
}
```

{@end-tool}

### checkInstance()

```dart
T checkInstance<T extends BindingBase>(T? instance)
```

A method that shows a useful error message if the given binding instance is not initialized.

See [initInstances] for advice on using this method.

This method either returns the argument or throws an exception. In release mode it always returns the argument.

The type argument `T` should be the kind of binding mixin (e.g. `SchedulerBinding`) that is calling the method. It is used in error messages.

### debugBindingType()

```dart
Type? debugBindingType()
```

In debug builds, the type of the current binding, if any, or else null.

This may be useful in asserts to verify that the binding has not been initialized before the point in the application code that wants to initialize the binding, or to verify that the binding is the one that is expected.

For example, if an application uses [Zone]s to report uncaught exceptions, it may need to ensure that `ensureInitialized()` has not yet been invoked on any binding at the point where it configures the zone and initializes the binding.

If this returns null, the binding has not been initialized.

If this returns a non-null value, it returns the type of the binding instance.

To obtain the binding itself, consider the `instance` getter on the [BindingBase] subclass or mixin.

This method only returns a useful value in debug builds. In release builds, the return value is always null; to improve startup performance, the type of the binding is not tracked in release builds.

See also:

- [BindingBase], whose class documentation describes the conventions for dealing with bindings.
- [initInstances], whose documentation details how to create a binding mixin.

### debugZoneErrorsAreFatal

```dart
bool debugZoneErrorsAreFatal
```

Whether [debugCheckZone] should throw (true) or just report the error (false).

Setting this to true makes it easier to catch cases where the zones are misconfigured, by allowing debuggers to stop at the point of error.

Currently this defaults to false, to avoid suddenly breaking applications that are affected by this check but appear to be working today. Applications are encouraged to resolve any issues that cause the [debugCheckZone] message to appear, as even if they appear to be working today, they are likely to be hiding hard-to-find bugs, and are more brittle (likely to collect bugs in the future).

To silence the message displayed by [debugCheckZone], ensure that the same zone is used when calling `ensureInitialized()` as when calling the framework in any other context (e.g. via [runApp]).

### debugCheckZone()

```dart
bool debugCheckZone(String entryPoint)
```

Checks that the current [Zone] is the same as that which was used to initialize the binding.

If the current zone ([Zone.current]) is not the zone that was active when the binding was initialized, then this method generates a [FlutterError] exception with detailed information. The exception is either thrown directly, or reported via [FlutterError.reportError], depending on the value of [BindingBase.debugZoneErrorsAreFatal].

To silence the message displayed by [debugCheckZone], ensure that the same zone is used when calling `ensureInitialized()` as when calling the framework in any other context (e.g. via [runApp]). For example, consider keeping a reference to the zone used to initialize the binding, and using [Zone.run] to use it again when calling into the framework.

## Usage

The binding is considered initialized once [BindingBase.initInstances] has run; if this is called before then, it will throw an [AssertionError].

The `entryPoint` parameter is the name of the API that is checking the zones are consistent, for example, `'runApp'`.

This function always returns true (if it does not throw). It is expected to be invoked via the binding instance, e.g.:

```dart
void startup() {
  WidgetsBinding binding = WidgetsFlutterBinding.ensureInitialized();
  assert(binding.debugCheckZone('startup'));
  // ...
}
```

If the binding expects to be used with multiple zones, it should override this method to return true always without throwing. (For example, the bindings used with [flutter_test] do this as they make heavy use of zones to drive the framework with an artificial clock and to catch errors and report them as test failures.)

### initServiceExtensions()

```dart
void initServiceExtensions()
```

Called when the binding is initialized, to register service extensions.

Bindings that want to expose service extensions should overload this method to register them using calls to [registerSignalServiceExtension], [registerBoolServiceExtension], [registerNumericServiceExtension], and [registerServiceExtension] (in increasing order of complexity).

Implementations of this method must call their superclass implementation.

{@macro flutter.foundation.BindingBase.registerServiceExtension}

See also:

- <https://github.com/dart-lang/sdk/blob/main/runtime/vm/service/service.md#rpcs-requests-and-responses>

### locked

```dart
bool get locked
```

Whether [lockEvents] is currently locking events.

Binding subclasses that fire events should check this first, and if it is set, queue events instead of firing them.

Events should be flushed when [unlocked] is called.

### lockEvents()

```dart
Future<void> lockEvents(Future<void> Function() callback)
```

Locks the dispatching of asynchronous events and callbacks until the callback's future completes.

This causes input lag and should therefore be avoided when possible. It is primarily intended for use during non-user-interactive time such as to allow [reassembleApplication] to block input while it walks the tree (which it partially does asynchronously).

The [Future] returned by the `callback` argument is returned by [lockEvents].

The [gestures] binding wraps [PlatformDispatcher.onPointerDataPacket] in logic that honors this event locking mechanism. Similarly, tasks queued using [SchedulerBinding.scheduleTask] will only start when events are not [locked].

### unlocked()

```dart
void unlocked()
```

Called by [lockEvents] when events get unlocked.

This should flush any events that were queued while [locked] was true.

### reassembleApplication()

```dart
Future<void> reassembleApplication()
```

Cause the entire application to redraw, e.g. after a hot reload.

This is used by development tools when the application code has changed, to cause the application to pick up any changed code. It can be triggered manually by sending the `ext.flutter.reassemble` service extension signal.

This method is very computationally expensive and should not be used in production code. There is never a valid reason to cause the entire application to repaint in production. All aspects of the Flutter framework know how to redraw when necessary. It is only necessary in development when the code is literally changed on the fly (e.g. in hot reload) or when debug flags are being toggled.

While this method runs, events are locked (e.g. pointer events are not dispatched).

Subclasses (binding classes) should override [performReassemble] to react to this method being called. This method itself should not be overridden.

### performReassemble()

```dart
Future<void> performReassemble()
```

This method is called by [reassembleApplication] to actually cause the application to reassemble, e.g. after a hot reload.

Bindings are expected to use this method to re-register anything that uses closures, so that they do not keep pointing to old code, and to flush any caches of previously computed values, in case the new code would compute them differently. For example, the rendering layer triggers the entire application to repaint when this is called.

Do not call this method directly. Instead, use [reassembleApplication].

### registerSignalServiceExtension()

```dart
void registerSignalServiceExtension({required String name, required AsyncCallback callback})
```

Registers a service extension method with the given name (full name "ext.flutter.name"), which takes no arguments and returns no value.

Calls the `callback` callback when the service extension is called.

{@macro flutter.foundation.BindingBase.registerServiceExtension}

### registerBoolServiceExtension()

```dart
void registerBoolServiceExtension({required String name, required AsyncValueGetter<bool> getter, required AsyncValueSetter<bool> setter})
```

Registers a service extension method with the given name (full name "ext.flutter.name"), which takes a single argument "enabled" which can have the value "true" or the value "false" or can be omitted to read the current value. (Any value other than "true" is considered equivalent to "false". Other arguments are ignored.)

Calls the `getter` callback to obtain the value when responding to the service extension method being called.

Calls the `setter` callback with the new value when the service extension method is called with a new value.

{@macro flutter.foundation.BindingBase.registerServiceExtension}

### registerNumericServiceExtension()

```dart
void registerNumericServiceExtension({required String name, required AsyncValueGetter<double> getter, required AsyncValueSetter<double> setter})
```

Registers a service extension method with the given name (full name "ext.flutter.name"), which takes a single argument with the same name as the method which, if present, must have a value that can be parsed by [double.parse], and can be omitted to read the current value. (Other arguments are ignored.)

Calls the `getter` callback to obtain the value when responding to the service extension method being called.

Calls the `setter` callback with the new value when the service extension method is called with a new value.

{@macro flutter.foundation.BindingBase.registerServiceExtension}

### postEvent()

```dart
void postEvent(String eventKind, Map<String, dynamic> eventData)
```

All events dispatched by a [BindingBase] use this method instead of calling [developer.postEvent] directly so that tests for [BindingBase] can track which events were dispatched by overriding this method.

This is unrelated to the events managed by [lockEvents].

### registerStringServiceExtension()

```dart
void registerStringServiceExtension({required String name, required AsyncValueGetter<String> getter, required AsyncValueSetter<String> setter})
```

Registers a service extension method with the given name (full name "ext.flutter.name"), which optionally takes a single argument with the name "value". If the argument is omitted, the value is to be read, otherwise it is to be set. Returns the current value.

Calls the `getter` callback to obtain the value when responding to the service extension method being called.

Calls the `setter` callback with the new value when the service extension method is called with a new value.

{@macro flutter.foundation.BindingBase.registerServiceExtension}

### registerServiceExtension()

```dart
void registerServiceExtension({required String name, required ServiceExtensionCallback callback})
```

Registers a service extension method with the given name (full name "ext.flutter.name").

The given callback is called when the extension method is called. The callback must return a [Future] that either eventually completes to a return value in the form of a name/value map where the values can all be converted to JSON using `json.encode()` (see [JsonEncoder]), or fails. In case of failure, the failure is reported to the remote caller and is dumped to the logs.

The returned map will be mutated.

{@template flutter.foundation.BindingBase.registerServiceExtension} A registered service extension can only be activated if the vm-service is included in the build, which only happens in debug and profile mode. Although a service extension cannot be used in release mode its code may still be included in the Dart snapshot and blow up binary size if it is not wrapped in a guard that allows the tree shaker to remove it (see sample code below).

{@tool snippet} The following code registers a service extension that is only included in debug builds.

```dart
void myRegistrationFunction() {
  assert(() {
    // Register your service extension here.
    return true;
  }());
}
```

{@end-tool}

{@tool snippet} A service extension registered with the following code snippet is available in debug and profile mode.

```dart
void myOtherRegistrationFunction() {
  // kReleaseMode is defined in the 'flutter/foundation.dart' package.
  if (!kReleaseMode) {
    // Register your service extension here.
  }
}
```

{@end-tool}

Both guards ensure that Dart's tree shaker can remove the code for the service extension in release builds. {@endtemplate}

### toString()

```dart
String toString()
```
