@docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'nav_bar.dart';

# RefreshIndicatorMode

```dart
enum RefreshIndicatorMode {}
```

The current state of the refresh control.

Passed into the [RefreshControlIndicatorBuilder] builder function so users can show different UI in different modes.

Initial state, when not being overscrolled into, or after the overscroll is canceled or after done and the sliver retracted away.

While being overscrolled but not far enough yet to trigger the refresh.

Dragged far enough that the onRefresh callback will run and the dragged displacement is not yet at the final refresh resting state.

While the onRefresh task is running.

While the indicator is animating away after refreshing.

# RefreshControlIndicatorBuilder

```dart
typedef RefreshControlIndicatorBuilder = Widget Function(BuildContext context, RefreshIndicatorMode refreshState, double pulledExtent, double refreshTriggerPullDistance, double refreshIndicatorExtent)
```

Signature for a builder that can create a different widget to show in the refresh indicator space depending on the current state of the refresh control and the space available.

The `refreshTriggerPullDistance` and `refreshIndicatorExtent` parameters are the same values passed into the [CupertinoSliverRefreshControl].

The `pulledExtent` parameter is the currently available space either from overscrolling or as held by the sliver during refresh.

# RefreshCallback

```dart
typedef RefreshCallback = Future<void> Function()
```

A callback function that's invoked when the [CupertinoSliverRefreshControl] is pulled a `refreshTriggerPullDistance`. Must return a [Future]. Upon completion of the [Future], the [CupertinoSliverRefreshControl] enters the [RefreshIndicatorMode.done] state and will start to go away.

# CupertinoSliverRefreshControl

```dart
class CupertinoSliverRefreshControl extends StatefulWidget {}
```

A sliver widget implementing the iOS-style pull to refresh content control.

When inserted as the first sliver in a scroll view or behind other slivers that still lets the scrollable overscroll in front of this sliver (such as the [CupertinoSliverNavigationBar], this widget will:

- Let the user draw inside the overscrolled area via the passed in [builder].
- Trigger the provided [onRefresh] function when overscrolled far enough to pass [refreshTriggerPullDistance].
- Continue to hold [refreshIndicatorExtent] amount of space for the [builder] to keep drawing inside of as the [Future] returned by [onRefresh] processes.
- Scroll away once the [onRefresh] [Future] completes.

The [builder] function will be informed of the current [RefreshIndicatorMode] when invoking it, except in the [RefreshIndicatorMode.inactive] state when no space is available and nothing needs to be built. The [builder] function will otherwise be continuously invoked as the amount of space available changes from overscroll, as the sliver scrolls away after the [onRefresh] task is done, etc.

Only one refresh can be triggered until the previous refresh has completed and the indicator sliver has retracted at least 90% of the way back.

Can only be used in downward-scrolling vertical lists that overscrolls. In other words, refreshes can't be triggered with [Scrollable]s using [ClampingScrollPhysics] which is the default on Android. To allow overscroll on Android, use an overscrolling physics such as [BouncingScrollPhysics]. This can be done via:

- Providing a [BouncingScrollPhysics] (possibly in combination with a [AlwaysScrollableScrollPhysics]) while constructing the scrollable.
- By inserting a [ScrollConfiguration] with [BouncingScrollPhysics] above the scrollable.
- By using [CupertinoApp], which always uses a [ScrollConfiguration] with [BouncingScrollPhysics] regardless of platform.

In a typical application, this sliver should be inserted between the app bar sliver such as [CupertinoSliverNavigationBar] and your main scrollable content's sliver.

{@tool dartpad} When the user scrolls past [refreshTriggerPullDistance], this sample shows the default iOS pull to refresh indicator for 1 second and adds a new item to the top of the list view.

** See code in examples/api/lib/cupertino/refresh/cupertino_sliver_refresh_control.0.dart ** {@end-tool}

See also:

- [CustomScrollView], a typical sliver holding scroll view this control should go into.
- <https://developer.apple.com/ios/human-interface-guidelines/controls/refresh-content-controls/>
- [RefreshIndicator], a Material Design version of the pull-to-refresh paradigm. This widget works differently than [RefreshIndicator] because instead of being an overlay on top of the scrollable, the [CupertinoSliverRefreshControl] is part of the scrollable and actively occupies scrollable space.

### CupertinoSliverRefreshControl()

```dart
CupertinoSliverRefreshControl({dynamic key, double refreshTriggerPullDistance = _defaultRefreshTriggerPullDistance, double refreshIndicatorExtent = _defaultRefreshIndicatorExtent, RefreshControlIndicatorBuilder? builder = buildRefreshIndicator, RefreshCallback? onRefresh})
```

Create a new refresh control for inserting into a list of slivers.

The [refreshTriggerPullDistance] and [refreshIndicatorExtent] arguments must be greater than or equal to 0.

The [builder] argument may be null, in which case no indicator UI will be shown but the [onRefresh] will still be invoked. By default, [builder] shows a [CupertinoActivityIndicator].

The [onRefresh] argument will be called when pulled far enough to trigger a refresh.

### refreshTriggerPullDistance

```dart
double refreshTriggerPullDistance
```

The amount of overscroll the scrollable must be dragged to trigger a reload.

Must be larger than zero and larger than [refreshIndicatorExtent]. Defaults to 100 pixels when not specified.

When overscrolled past this distance, [onRefresh] will be called if not null and the [builder] will build in the [RefreshIndicatorMode.armed] state.

### refreshIndicatorExtent

```dart
double refreshIndicatorExtent
```

The amount of space the refresh indicator sliver will keep holding while [onRefresh]'s [Future] is still running.

Must be a positive number, but can be zero, in which case the sliver will start retracting back to zero as soon as the refresh is started. Defaults to 60 pixels when not specified.

Must be smaller than [refreshTriggerPullDistance], since the sliver shouldn't grow further after triggering the refresh.

### builder

```dart
RefreshControlIndicatorBuilder? builder
```

A builder that's called as this sliver's size changes, and as the state changes.

Can be set to null, in which case nothing will be drawn in the overscrolled space.

Will not be called when the available space is zero such as before any overscroll.

### onRefresh

```dart
RefreshCallback? onRefresh
```

Callback invoked when pulled by [refreshTriggerPullDistance].

If provided, must return a [Future] which will keep the indicator in the [RefreshIndicatorMode.refresh] state until the [Future] completes.

Can be null, in which case a single frame of [RefreshIndicatorMode.armed] state will be drawn before going immediately to the [RefreshIndicatorMode.done] where the sliver will start retracting.

### state()

```dart
RefreshIndicatorMode state(BuildContext context)
```

Retrieve the current state of the CupertinoSliverRefreshControl. The same as the state that gets passed into the [builder] function. Used for testing.

### buildRefreshIndicator()

```dart
Widget buildRefreshIndicator(BuildContext context, RefreshIndicatorMode refreshState, double pulledExtent, double refreshTriggerPullDistance, double refreshIndicatorExtent)
```

Builds a refresh indicator that reflects the standard iOS pull-to-refresh behavior. Specifically, this entails presenting an activity indicator that changes depending on the current refreshState. As the user initially drags down, the indicator will gradually reveal individual ticks until the refresh becomes armed. At this point, the animated activity indicator will begin rotating. Once the refresh has completed, the activity indicator shrinks away as the space allocation animates back to closed.

### createState()

```dart
State<CupertinoSliverRefreshControl> createState()
```
