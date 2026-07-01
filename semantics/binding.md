@docImport 'package:flutter/widgets.dart';

@docImport 'semantics.dart';

# SemanticsBinding

```dart
mixin SemanticsBinding on BindingBase {}
```

The glue between the semantics layer and the Flutter engine.

### initInstances()

```dart
void initInstances()
```

### instance

```dart
SemanticsBinding get instance
```

The current [SemanticsBinding], if one has been created.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### semanticsEnabled

```dart
bool get semanticsEnabled
```

Whether semantics information must be collected.

Returns true if either the platform has requested semantics information to be generated or if [ensureSemantics] has been called otherwise.

To get notified when this value changes register a listener with [addSemanticsEnabledListener].

### addSemanticsEnabledListener()

```dart
void addSemanticsEnabledListener(VoidCallback listener)
```

Adds a `listener` to be called when [semanticsEnabled] changes.

See also:

- [removeSemanticsEnabledListener] to remove the listener again.
- [ValueNotifier.addListener], which documents how and when listeners are called.

### removeSemanticsEnabledListener()

```dart
void removeSemanticsEnabledListener(VoidCallback listener)
```

Removes a `listener` added by [addSemanticsEnabledListener].

See also:

- [ValueNotifier.removeListener], which documents how listeners are removed.

### addSemanticsActionListener()

```dart
void addSemanticsActionListener(ValueSetter<ui.SemanticsActionEvent> listener)
```

Adds a listener that is called for every [ui.SemanticsActionEvent] received.

The listeners are called before [performSemanticsAction] is invoked.

To remove the listener, call [removeSemanticsActionListener].

### removeSemanticsActionListener()

```dart
void removeSemanticsActionListener(ValueSetter<ui.SemanticsActionEvent> listener)
```

Removes a listener previously added with [addSemanticsActionListener].

### getRectOfSemanticsNodeInViewCoordinates()

```dart
ui.Rect? getRectOfSemanticsNodeInViewCoordinates(int viewId, int nodeId)
```

Returns the global rect for the semantics node with the given [nodeId] in the view with the given [viewId].

The rect is in the global coordinate space of the view's render tree, in logical pixels. This is useful for widgets that react to semantics actions and need the on-screen position of the semantics node that received the action.

Asserts in non-release builds and returns null if the view is unknown, the view has no semantics owner, or the node cannot be found. Callers should only invoke this in response to a semantics action, in which case all three lookups are expected to succeed.

### debugOutstandingSemanticsHandles

```dart
int get debugOutstandingSemanticsHandles
```

The number of clients registered to listen for semantics.

The number is increased whenever [ensureSemantics] is called and decreased when [SemanticsHandle.dispose] is called.

### ensureSemantics()

```dart
SemanticsHandle ensureSemantics()
```

Creates a new [SemanticsHandle] and requests the collection of semantics information.

Semantics information are only collected when there are clients interested in them. These clients express their interest by holding a [SemanticsHandle].

Clients can close their [SemanticsHandle] by calling [SemanticsHandle.dispose]. Once all outstanding [SemanticsHandle] objects are closed, semantics information are no longer collected.

### performSemanticsAction()

```dart
void performSemanticsAction(ui.SemanticsActionEvent action)
```

Called whenever the platform requests an action to be performed on a [SemanticsNode].

This callback is invoked when a user interacts with the app via an accessibility service (e.g. TalkBack and VoiceOver) and initiates an action on the focused node.

Bindings that mixin the [SemanticsBinding] must implement this method and perform the given `action` on the [SemanticsNode] specified by [ui.SemanticsActionEvent.nodeId].

See [dart:ui.PlatformDispatcher.onSemanticsActionEvent].

### accessibilityFeatures

```dart
ui.AccessibilityFeatures get accessibilityFeatures
```

The currently active set of [ui.AccessibilityFeatures].

This is set when the binding is first initialized and updated whenever a flag is changed.

To listen to changes to accessibility features, create a [WidgetsBindingObserver] and listen to [WidgetsBindingObserver.didChangeAccessibilityFeatures].

### handleAccessibilityFeaturesChanged()

```dart
void handleAccessibilityFeaturesChanged()
```

Called when the platform accessibility features change.

See [dart:ui.PlatformDispatcher.onAccessibilityFeaturesChanged].

### createSemanticsUpdateBuilder()

```dart
ui.SemanticsUpdateBuilder createSemanticsUpdateBuilder()
```

Creates an empty semantics update builder.

The caller is responsible for filling out the semantics node updates.

This method is used by the [SemanticsOwner] to create builder for all its semantics updates.

### disableAnimations

```dart
bool get disableAnimations
```

The platform is requesting that animations be disabled or simplified.

This setting can be overridden for testing or debugging by setting [debugSemanticsDisableAnimations].

# SemanticsHandle

```dart
class SemanticsHandle {}
```

A reference to the semantics information generated by the framework.

Semantics information are only collected when there are clients interested in them. These clients express their interest by holding a [SemanticsHandle]. When the client no longer needs the semantics information, it must call [dispose] on the [SemanticsHandle] to close it. When all open [SemanticsHandle]s are disposed, the framework will stop updating the semantics information.

To obtain a [SemanticsHandle], call [SemanticsBinding.ensureSemantics].

### dispose()

```dart
void dispose()
```

Closes the semantics handle.

When all the outstanding [SemanticsHandle] objects are closed, the framework will stop generating semantics information.
