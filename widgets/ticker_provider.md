@docImport 'package:flutter/animation.dart';

# TickerMode

```dart
class TickerMode extends StatefulWidget {}
```

Enables or disables tickers (and thus animation controllers) in the widget subtree.

This only works if [AnimationController] objects are created using widget-aware ticker providers. For example, using a [TickerProviderStateMixin] or a [SingleTickerProviderStateMixin].

### TickerMode()

```dart
TickerMode({dynamic key, required bool enabled, required Widget child, bool forceFrames = false})
```

Creates a widget that enables or disables tickers and optionally forces frames.

### enabled

```dart
bool enabled
```

The requested ticker mode for this subtree.

The effective ticker mode of this subtree may differ from this value if there is an ancestor [TickerMode] with this field set to false.

If true and all ancestor [TickerMode]s are also enabled, then tickers in this subtree will tick.

If false, then tickers in this subtree will not tick regardless of any ancestor [TickerMode]s. Animations driven by such tickers are not paused, they just don't call their callbacks. Time still elapses.

### forceFrames

```dart
bool forceFrames
```

If true, tickers in this subtree will force frames even if frames would normally not be scheduled (e.g. even if the device's screen is turned off).

Use sparingly as this will cause significantly higher battery usage when the device should be idle.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### of()

```dart
bool of(BuildContext context)
```

Whether tickers in the given subtree should be enabled or disabled.

This is used automatically by [TickerProviderStateMixin] and [SingleTickerProviderStateMixin] to decide if their tickers should be enabled or disabled.

In the absence of a [TickerMode] widget, this function defaults to true.

Typical usage is as follows:

```dart
// ignore: deprecated_member_use
bool tickingEnabled = TickerMode.of(context);
```

### getNotifier()

```dart
ValueListenable<bool> getNotifier(BuildContext context)
```

Obtains a [ValueListenable] from the [TickerMode] surrounding the `context`, which indicates whether tickers are enabled in the given subtree.

When that [TickerMode] enables or disables tickers, the listenable notifies its listeners.

While the [ValueListenable] is stable for the lifetime of the surrounding [TickerMode], calling this method does not establish a dependency between the `context` and the [TickerMode] and the widget owning the `context` does not rebuild when the ticker mode changes from true to false or vice versa. This is preferable when the ticker mode does not impact what is currently rendered on screen, e.g. because it is only used to mute/unmute a [Ticker]. Since no dependency is established, the widget owning the `context` is also not informed when it is moved to a new location in the tree where it may have a different [TickerMode] ancestor. When this happens, the widget must manually unsubscribe from the old listenable, obtain a new one from the new ancestor [TickerMode] by calling this method again, and re-subscribe to it. [StatefulWidget]s can, for example, do this in [State.activate], which is called after the widget has been moved to a new location.

Alternatively, [of] can be used instead of this method to create a dependency between the provided `context` and the ancestor [TickerMode]. In this case, the widget automatically rebuilds when the ticker mode changes or when it is moved to a new [TickerMode] ancestor, which simplifies the management cost in the widget at the expense of some potential unnecessary rebuilds.

In the absence of a [TickerMode] widget, this function returns a [ValueListenable], whose [ValueListenable.value] is always true.

### valuesOf()

```dart
TickerModeData valuesOf(BuildContext context)
```

Returns the requested ticker mode values for this subtree and establishes a dependency on the ancestor [TickerMode], if any.

This is used automatically by [TickerProviderStateMixin] and [SingleTickerProviderStateMixin] to decide if their tickers should be enabled or disabled.

In the absence of a [TickerMode] widget, this defaults to enabled tickers that don't force frames.

Typical usage is as follows:

```dart
bool tickingEnabled = TickerMode.valuesOf(context).enabled;
```

### getValuesNotifier()

```dart
ValueListenable<TickerModeData> getValuesNotifier(BuildContext context)
```

Obtains a [ValueListenable] from the [TickerMode] surrounding the `context`, which indicates whether tickers are enabled in the given subtree.

When that [TickerMode] enabled or disabled tickers, the listenable notifies its listeners.

While the [ValueListenable] is stable for the lifetime of the surrounding [TickerMode], calling this method does not establish a dependency between the `context` and the [TickerMode] and the widget owning the `context` does not rebuild when the ticker mode data changes. This is preferable when the ticker mode does not impact what is currently rendered on screen, e.g. because it is only used to mute/unmute a [Ticker]. Since no dependency is established, the widget owning the `context` is also not informed when it is moved to a new location in the tree where it may have a different [TickerMode] ancestor. When this happens, the widget must manually unsubscribe from the old listenable, obtain a new one from the new ancestor [TickerMode] by calling this method again, and re-subscribe to it. [StatefulWidget]s can, for example, do this in [State.activate], which is called after the widget has been moved to a new location.

Alternatively, [of] can be used instead of this method to create a dependency between the provided `context` and the ancestor [TickerMode]. In this case, the widget automatically rebuilds when the ticker mode changes or when it is moved to a new [TickerMode] ancestor, which simplifies the management cost in the widget at the expensive of some potential unnecessary rebuilds.

In the absence of a [TickerMode] widget, this function returns a [ValueListenable], whose [ValueListenable.value] is [TickerModeData.fallback].

### merge()

```dart
Widget merge({Key? key, bool? enabled, bool? forceFrames, required Widget child})
```

Creates a [TickerMode] that overrides the ambient ticker mode values.

The given `enabled` and `forceFrames` override the ambient values when not null; otherwise the ambient values are preserved.

### createState()

```dart
State<TickerMode> createState()
```

# SingleTickerProviderStateMixin

```dart
mixin SingleTickerProviderStateMixin<T extends StatefulWidget> on State<T> implements TickerProvider {}
```

Provides a single [Ticker] that is configured to only tick while the current tree is enabled, as defined by [TickerMode].

To create the [AnimationController] in a [State] that only uses a single [AnimationController], mix in this class, then pass `vsync: this` to the animation controller constructor.

This mixin only supports vending a single ticker. If you might have multiple [AnimationController] objects over the lifetime of the [State], use a full [TickerProviderStateMixin] instead.

### createTicker()

```dart
Ticker createTicker(TickerCallback onTick)
```

### dispose()

```dart
void dispose()
```

### activate()

```dart
void activate()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TickerProviderStateMixin

```dart
mixin TickerProviderStateMixin<T extends StatefulWidget> on State<T> implements TickerProvider {}
```

Provides [Ticker] objects that are configured to only tick while the current tree is enabled, as defined by [TickerMode].

To create an [AnimationController] in a class that uses this mixin, pass `vsync: this` to the animation controller constructor whenever you create a new animation controller.

If you only have a single [Ticker] (for example only a single [AnimationController]) for the lifetime of your [State], then using a [SingleTickerProviderStateMixin] is more efficient. This is the common case.

When creating multiple [AnimationController]s, using a single state with [TickerProviderStateMixin] as vsync for all [AnimationController]s is more efficient than creating multiple states with [SingleTickerProviderStateMixin].

### createTicker()

```dart
Ticker createTicker(TickerCallback onTick)
```

### activate()

```dart
void activate()
```

### dispose()

```dart
void dispose()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TickerModeData

```dart
class TickerModeData {}
```

Immutable compound values that describe the effective ticker behavior for a subtree.

Instances of this class are produced by [TickerMode.valuesOf] and [TickerMode.getValuesNotifier] and reflect the values that apply at a given location in the widget tree after taking ancestor [TickerMode] widgets into account.

Semantics of the fields:

- [enabled]: A ticker is considered enabled only if all ancestor [TickerMode.enabled] values and the local [TickerMode.enabled] are true (logical AND). When false, tickers are muted (time still elapses but callbacks are not invoked).
- [forceFrames]: When true, tickers in the subtree request frames using [SchedulerBinding.scheduleForcedFrame] while active. This value is combined across ancestors using logical OR, so any ancestor requesting forced frames enables it for the subtree.

For most widgets, reading these values is unnecessary; mixins such as [SingleTickerProviderStateMixin] and [TickerProviderStateMixin] apply them automatically to the [Ticker]s they vend. Use this class when you need to observe or react to ticker policy explicitly.

### TickerModeData()

```dart
TickerModeData({required bool enabled, required bool forceFrames})
```

Creates a [TickerModeData].

### fallback

```dart
TickerModeData fallback
```

Fallback values used when there is no ancestor [TickerMode].

This corresponds to tickers being enabled and not forcing frames.

### enabled

```dart
bool enabled
```

Whether tickers are enabled (not muted) for the subtree.

Effective value is the logical AND of all ancestor and local [TickerMode.enabled] values.

### forceFrames

```dart
bool forceFrames
```

Whether tickers should request forced frames while active.

Effective value is the logical OR of all ancestor and local [TickerMode.forceFrames] values. Forcing frames may increase battery usage, so use sparingly.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```
