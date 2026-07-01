@docImport 'dart:ui';

@docImport 'package:flutter/widgets.dart';

@docImport 'system_chrome.dart';

# ServicesBinding

```dart
mixin ServicesBinding on BindingBase, SchedulerBinding {}
```

Listens for platform messages and directs them to the [defaultBinaryMessenger].

The [ServicesBinding] also registers a [LicenseEntryCollector] that exposes the licenses found in the `NOTICES` file (or its compressed variant, `NOTICES.Z`) stored at the root of the asset bundle, and implements the `ext.flutter.evict` service extension (see [evict]).

### initInstances()

```dart
void initInstances()
```

### instance

```dart
ServicesBinding get instance
```

The current [ServicesBinding], if one has been created.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### keyboard

```dart
HardwareKeyboard get keyboard
```

The global singleton instance of [HardwareKeyboard], which can be used to query keyboard states.

### keyEventManager

```dart
KeyEventManager get keyEventManager
```

The global singleton instance of [KeyEventManager], which is used internally to dispatch key messages.

This property is deprecated, and will be removed. See [HardwareKeyboard.addHandler] instead.

### defaultBinaryMessenger

```dart
BinaryMessenger get defaultBinaryMessenger
```

The default instance of [BinaryMessenger].

This is used to send messages from the application to the platform, and keeps track of which handlers have been registered on each channel so it may dispatch incoming messages to the registered handler.

The default implementation returns a [BinaryMessenger] that delivers the messages in the same order in which they are sent.

### rootIsolateToken

```dart
ui.RootIsolateToken? get rootIsolateToken
```

A token that represents the root isolate, used for coordinating with background isolates.

This property is primarily intended for use with [BackgroundIsolateBinaryMessenger.ensureInitialized], which takes a [RootIsolateToken] as its argument. The value `null` is returned when executed from background isolates.

### channelBuffers

```dart
ui.ChannelBuffers get channelBuffers
```

The low level buffering and dispatch mechanism for messages sent by plugins on the engine side to their corresponding plugin code on the framework side.

This exposes the [dart:ui.channelBuffers] object. Bindings can override this getter to intercept calls to the [ChannelBuffers] mechanism (for example, for tests).

In production, direct access to this object should not be necessary. Messages are received and dispatched by the [defaultBinaryMessenger]. This object is primarily used to send mock messages in tests, via the [ChannelBuffers.push] method (simulating a plugin sending a message to the framework).

See also:

- [PlatformDispatcher.sendPlatformMessage], which is used for sending messages to plugins from the framework (the opposite of [channelBuffers]).
- [platformDispatcher], the [PlatformDispatcher] singleton.

### createBinaryMessenger()

```dart
BinaryMessenger createBinaryMessenger()
```

Creates a default [BinaryMessenger] instance that can be used for sending platform messages.

Many Flutter framework components that communicate with the platform assume messages are received by the platform in the same order in which they are sent. When overriding this method, be sure the [BinaryMessenger] implementation guarantees FIFO delivery.

### handleMemoryPressure()

```dart
void handleMemoryPressure()
```

Called when the operating system notifies the application of a memory pressure situation.

This method exposes the `memoryPressure` notification from [SystemChannels.system].

### handleSystemMessage()

```dart
Future<void> handleSystemMessage(Object systemMessage)
```

Handler called for messages received on the [SystemChannels.system] message channel.

Other bindings may override this to respond to incoming system messages.

### initLicenses()

```dart
void initLicenses()
```

Adds relevant licenses to the [LicenseRegistry].

By default, the [ServicesBinding]'s implementation of [initLicenses] adds all the licenses collected by the `flutter` tool during compilation.

### initServiceExtensions()

```dart
void initServiceExtensions()
```

### evict()

```dart
void evict(String asset)
```

Called in response to the `ext.flutter.evict` service extension.

This is used by the `flutter` tool during hot reload so that any images that have changed on disk get cleared from caches.

### readInitialLifecycleStateFromNativeWindow()

```dart
void readInitialLifecycleStateFromNativeWindow()
```

Initializes the [lifecycleState] with the [dart:ui.PlatformDispatcher.initialLifecycleState].

Once the [lifecycleState] is populated through any means (including this method), this method will do nothing. This is because the [dart:ui.PlatformDispatcher.initialLifecycleState] may already be stale and it no longer makes sense to use the initial state at dart vm startup as the current state anymore.

The latest state should be obtained by subscribing to [WidgetsBindingObserver.didChangeAppLifecycleState].

### accessibilityFocus

```dart
ValueNotifier<int?> accessibilityFocus
```

Listenable that notifies when the accessibility focus on the system have changed.

### handleViewFocusChanged()

```dart
void handleViewFocusChanged(ui.ViewFocusEvent event)
```

Called whenever the [PlatformDispatcher] receives a notification that the focus state on a view has changed.

The [event] contains the view ID for the view that changed its focus state.

See also:

- [PlatformDispatcher.onViewFocusChange], which calls this method.

### handleRequestAppExit()

```dart
Future<ui.AppExitResponse> handleRequestAppExit()
```

Handles any requests for application exit that may be received on the [SystemChannels.platform] method channel.

By default, returns [ui.AppExitResponse.exit].

{@template flutter.services.binding.ServicesBinding.requestAppExit} Not all exits are cancelable, so not all exits will call this function. Do not rely on this function as a place to save critical data, because you will be disappointed. There are a number of ways that the application can exit without letting the application know first: power can be unplugged, the battery removed, the application can be killed in a task manager or command line, or the device could have a rapid unplanned disassembly (i.e. it could explode). In all of those cases (and probably others), no notification will be given to the application that it is about to exit. {@endtemplate}

{@tool sample} This examples shows how an application can cancel (or not) OS requests for quitting an application. Currently this is only supported on macOS and Linux.

** See code in examples/api/lib/services/binding/handle_request_app_exit.0.dart ** {@end-tool}

See also:

- [WidgetsBindingObserver.didRequestAppExit], which can be overridden to respond to this message.
- [WidgetsBinding.handleRequestAppExit] which overrides this method to notify its observers.

### exitApplication()

```dart
Future<ui.AppExitResponse> exitApplication(ui.AppExitType exitType, [int exitCode = 0])
```

Exits the application by calling the native application API method for exiting an application cleanly.

This differs from calling `dart:io`'s [exit] function in that it gives the engine a chance to clean up resources so that it doesn't crash on exit, so calling this is always preferred over calling [exit]. It also optionally gives handlers of [handleRequestAppExit] a chance to cancel the application exit.

The [exitType] indicates what kind of exit to perform. For [ui.AppExitType.cancelable] exits, the application is queried through a call to [handleRequestAppExit], where the application can optionally cancel the request for exit. If the [exitType] is [ui.AppExitType.required], then the application exits immediately without querying the application.

For [ui.AppExitType.cancelable] exits, the returned response value is the response obtained from the application as to whether the exit was canceled or not. Practically, the response will never be [ui.AppExitResponse.exit], since the application will have already exited by the time the result would have been received.

The optional [exitCode] argument will be used as the application exit code on platforms where an exit code is supported. On other platforms it may be ignored. It defaults to zero.

See also:

- [WidgetsBindingObserver.didRequestAppExit] for a handler you can override on a [WidgetsBindingObserver] to receive exit requests.

### restorationManager

```dart
RestorationManager get restorationManager
```

The [RestorationManager] synchronizes the restoration data between engine and framework.

See the docs for [RestorationManager] for a discussion of restoration state and how it is organized in Flutter.

To use a different [RestorationManager] subclasses can override [createRestorationManager], which is called to create the instance returned by this getter.

### createRestorationManager()

```dart
RestorationManager createRestorationManager()
```

Creates the [RestorationManager] instance available via [restorationManager].

Can be overridden in subclasses to create a different [RestorationManager].

### setSystemUiChangeCallback()

```dart
void setSystemUiChangeCallback(SystemUiChangeCallback? callback)
```

Sets the callback for the `SystemChrome.systemUIChange` method call received on the [SystemChannels.platform] channel.

This is typically not called directly. System UI changes that this method responds to are associated with [SystemUiMode]s, which are configured using [SystemChrome]. Use [SystemChrome.setSystemUIChangeCallback] to configure along with other SystemChrome settings.

See also:

- [SystemChrome.setEnabledSystemUIMode], which specifies the [SystemUiMode] to have visible when the application is running.

### initializationComplete()

```dart
Future<void> initializationComplete()
```

Alert the engine that the binding is registered. This instructs the engine to register its top level window handler on Windows. This signals that the app is able to process "System.requestAppExit" signals from the engine.

### systemContextMenuClient

```dart
set systemContextMenuClient(SystemContextMenuClient? client)
```

Registers a [SystemContextMenuClient] that will receive system context menu calls from the engine.

To unregister, set to null.

# SystemUiChangeCallback

```dart
typedef SystemUiChangeCallback = Future<void> Function(bool systemOverlaysAreVisible)
```

Signature for listening to changes in the [SystemUiMode].

Set by [SystemChrome.setSystemUIChangeCallback].

# SystemContextMenuClient

```dart
mixin SystemContextMenuClient {}
```

An interface to receive calls related to the system context menu from the engine.

Currently this is only supported on iOS 16+.

See also:

- [SystemContextMenuController], which uses this to provide a fully featured way to control the system context menu.
- [ServicesBinding.systemContextMenuClient], which can be set to a [SystemContextMenuClient] to register it to receive events, or null to unregister.
- [MediaQuery.maybeSupportsShowingSystemContextMenu], which indicates whether the system context menu is supported.
- [SystemContextMenu], which provides a widget interface for displaying the system context menu.

### handleSystemHide()

```dart
void handleSystemHide()
```

Handles the system hiding a context menu.

Called only on the single active instance registered with [ServicesBinding.systemContextMenuClient].

### handleCustomContextMenuAction()

```dart
void handleCustomContextMenuAction(String actionId)
```

Called when a custom context menu action is triggered.
