@docImport 'dart:ui'; @docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'form.dart'; @docImport 'heroes.dart'; @docImport 'pages.dart'; @docImport 'pop_scope.dart'; @docImport 'will_pop_scope.dart';

# OverlayRoute

```dart
abstract class OverlayRoute<T> extends Route<T> {}
```

A route that displays widgets in the [Navigator]'s [Overlay].

See also:

- [Route], which documents the meaning of the `T` generic type argument.

### OverlayRoute()

```dart
OverlayRoute({RouteSettings? settings, bool? requestFocus})
```

Creates a route that knows how to interact with an [Overlay].

### createOverlayEntries()

```dart
Iterable<OverlayEntry> createOverlayEntries()
```

Subclasses should override this getter to return the builders for the overlay.

### overlayEntries

```dart
List<OverlayEntry> get overlayEntries
```

### install()

```dart
void install()
```

### finishedWhenPopped

```dart
bool get finishedWhenPopped
```

Controls whether [didPop] calls [NavigatorState.finalizeRoute].

If true, this route removes its overlay entries during [didPop]. Subclasses can override this getter if they want to delay finalization (for example to animate the route's exit before removing it from the overlay).

Subclasses that return false from [finishedWhenPopped] are responsible for calling [NavigatorState.finalizeRoute] themselves.

### didPop()

```dart
bool didPop(T? result)
```

### dispose()

```dart
void dispose()
```

# TransitionRoute

```dart
abstract class TransitionRoute<T> extends OverlayRoute<T> implements PredictiveBackRoute {}
```

A route with entrance and exit transitions.

See also:

- [Route], which documents the meaning of the `T` generic type argument.

### TransitionRoute()

```dart
TransitionRoute({RouteSettings? settings, bool? requestFocus})
```

Creates a route that animates itself when it is pushed or popped.

### completed

```dart
Future<T?> get completed
```

This future completes only once the transition itself has finished, after the overlay entries have been removed from the navigator's overlay.

This future completes once the animation has been dismissed. That will be after [popped], because [popped] typically completes before the animation even starts, as soon as the route is popped.

### transitionDuration

```dart
Duration get transitionDuration
```

{@template flutter.widgets.TransitionRoute.transitionDuration} The duration the transition going forwards.

See also:

- [reverseTransitionDuration], which controls the duration of the transition when it is in reverse. {@endtemplate}

### reverseTransitionDuration

```dart
Duration get reverseTransitionDuration
```

{@template flutter.widgets.TransitionRoute.reverseTransitionDuration} The duration the transition going in reverse.

By default, the reverse transition duration is set to the value of the forwards [transitionDuration]. {@endtemplate}

### opaque

```dart
bool get opaque
```

{@template flutter.widgets.TransitionRoute.opaque} Whether the route obscures previous routes when the transition is complete.

When an opaque route's entrance transition is complete, the routes behind the opaque route will not be built to save resources. {@endtemplate}

### allowSnapshotting

```dart
bool get allowSnapshotting
```

{@template flutter.widgets.TransitionRoute.allowSnapshotting} Whether the route transition will prefer to animate a snapshot of the entering/exiting routes.

When this value is true, certain route transitions (such as the Android zoom page transition) will snapshot the entering and exiting routes. These snapshots are then animated in place of the underlying widgets to improve performance of the transition.

Generally this means that animations that occur on the entering/exiting route while the route animation plays may appear frozen - unless they are a hero animation or something that is drawn in a separate overlay. {@endtemplate}

### finishedWhenPopped

```dart
bool get finishedWhenPopped
```

### animation

```dart
Animation<double>? get animation
```

The animation that drives the route's transition and the previous route's forward transition.

### controller

```dart
AnimationController? get controller
```

The animation controller that the route uses to drive the transitions.

The animation itself is exposed by the [animation] property.

### secondaryAnimation

```dart
Animation<double>? get secondaryAnimation
```

The animation for the route being pushed on top of this route. This animation lets this route coordinate with the entrance and exit transition of route pushed on top of this route.

### willDisposeAnimationController

```dart
bool willDisposeAnimationController
```

Whether to takeover the [controller] created by [createAnimationController].

If true, this route will call [AnimationController.dispose] when the controller is no longer needed. If false, the controller should be disposed by whoever owned it.

It defaults to `true`.

### debugTransitionCompleted()

```dart
bool debugTransitionCompleted()
```

Returns true if the transition has completed.

It is equivalent to whether the future returned by [completed] has completed.

This method only works if assert is enabled. Otherwise it always returns false.

### createAnimationController()

```dart
AnimationController createAnimationController()
```

Called to create the animation controller that will drive the transitions to this route from the previous one, and back to the previous route from this one.

The returned controller will be disposed by [AnimationController.dispose] if the [willDisposeAnimationController] is `true`.

### createAnimation()

```dart
Animation<double> createAnimation()
```

Called to create the animation that exposes the current progress of the transition controlled by the animation controller created by [createAnimationController()].

### createSimulation()

```dart
Simulation? createSimulation({required bool forward})
```

Creates the simulation that drives the transition animation for this route.

By default, this method returns null, indicating that the route doesn't use simulations, but initiates the transition by calling either [AnimationController.forward] or [AnimationController.reverse] with [transitionDuration] and the controller's curve.

Subclasses can override this method to return a non-null [Simulation]. In this case, the [controller] will instead use the provided simulation to animate the transition using [AnimationController.animateWith] or [AnimationController.animateBackWith], and the [Simulation.x] is forwarded to the value of [animation]. The [controller]'s curve and [transitionDuration] are ignored.

This method is invoked each time the navigator pushes or pops this route. The `forward` parameter indicates the direction of the transition: true when the route is pushed, and false when it is popped.

### install()

```dart
void install()
```

### didPush()

```dart
TickerFuture didPush()
```

### didAdd()

```dart
void didAdd()
```

### didReplace()

```dart
void didReplace(Route<dynamic>? oldRoute)
```

### didPop()

```dart
bool didPop(T? result)
```

### didPopNext()

```dart
void didPopNext(Route<dynamic> nextRoute)
```

### didChangeNext()

```dart
void didChangeNext(Route<dynamic>? nextRoute)
```

### canTransitionTo()

```dart
bool canTransitionTo(TransitionRoute<dynamic> nextRoute)
```

Returns true if this route supports a transition animation that runs when [nextRoute] is pushed on top of it or when [nextRoute] is popped off of it.

Subclasses can override this method to restrict the set of routes they need to coordinate transitions with.

If true, and `nextRoute.canTransitionFrom()` is true, then the [ModalRoute.buildTransitions] `secondaryAnimation` will run from 0.0 - 1.0 when [nextRoute] is pushed on top of this one. Similarly, if the [nextRoute] is popped off of this route, the `secondaryAnimation` will run from 1.0 - 0.0.

If false, this route's [ModalRoute.buildTransitions] `secondaryAnimation` parameter value will be [kAlwaysDismissedAnimation]. In other words, this route will not animate when [nextRoute] is pushed on top of it or when [nextRoute] is popped off of it.

Returns true by default.

See also:

- [canTransitionFrom], which must be true for [nextRoute] for the [ModalRoute.buildTransitions] `secondaryAnimation` to run.

### canTransitionFrom()

```dart
bool canTransitionFrom(TransitionRoute<dynamic> previousRoute)
```

Returns true if [previousRoute] should animate when this route is pushed on top of it or when then this route is popped off of it.

Subclasses can override this method to restrict the set of routes they need to coordinate transitions with.

If true, and `previousRoute.canTransitionTo()` is true, then the previous route's [ModalRoute.buildTransitions] `secondaryAnimation` will run from 0.0 - 1.0 when this route is pushed on top of it. Similarly, if this route is popped off of [previousRoute] the previous route's `secondaryAnimation` will run from 1.0 - 0.0.

If false, then the previous route's [ModalRoute.buildTransitions] `secondaryAnimation` value will be kAlwaysDismissedAnimation. In other words [previousRoute] will not animate when this route is pushed on top of it or when then this route is popped off of it.

Returns true by default.

See also:

- [canTransitionTo], which must be true for [previousRoute] for its [ModalRoute.buildTransitions] `secondaryAnimation` to run.

### handleStartBackGesture()

```dart
void handleStartBackGesture({double progress = 0.0})
```

### handleUpdateBackGestureProgress()

```dart
void handleUpdateBackGestureProgress({required double progress})
```

### handleCancelBackGesture()

```dart
void handleCancelBackGesture()
```

### handleCommitBackGesture()

```dart
void handleCommitBackGesture()
```

### dispose()

```dart
void dispose()
```

### debugLabel

```dart
String get debugLabel
```

A short description of this route useful for debugging.

### toString()

```dart
String toString()
```

# PredictiveBackRoute

```dart
abstract interface class PredictiveBackRoute {}
```

An interface for a route that supports predictive back gestures.

See also:

- [PredictiveBackPageTransitionsBuilder], which builds page transitions for predictive back.

### isCurrent

```dart
bool get isCurrent
```

Whether this route is the top-most route on the navigator.

### popGestureEnabled

```dart
bool get popGestureEnabled
```

Whether a pop gesture can be started by the user for this route.

### handleStartBackGesture()

```dart
void handleStartBackGesture({double progress = 0.0})
```

Handles a predictive back gesture starting.

The `progress` parameter indicates the progress of the gesture from 0.0 to 1.0, as in [PredictiveBackEvent.progress].

### handleUpdateBackGestureProgress()

```dart
void handleUpdateBackGestureProgress({required double progress})
```

Handles a predictive back gesture updating as the user drags across the screen.

The `progress` parameter indicates the progress of the gesture from 0.0 to 1.0, as in [PredictiveBackEvent.progress].

### handleCommitBackGesture()

```dart
void handleCommitBackGesture()
```

Handles a predictive back gesture ending successfully.

### handleCancelBackGesture()

```dart
void handleCancelBackGesture()
```

Handles a predictive back gesture ending in cancellation.

# LocalHistoryEntry

```dart
class LocalHistoryEntry {}
```

An entry in the history of a [LocalHistoryRoute].

A [LocalHistoryEntry] represents a "mini" navigation state within a route. It allows widgets or UI components to handle the back button or pop operations locally without affecting the main navigator stack.

It is typically used for widgets such as dialogs, bottom sheets, or inline expandable panels that can be dismissed independently of the surrounding route.

When a local history entry is removed (e.g., via the back button), the [onRemove] callback is called first. Only after all local history entries have been removed will the route itself be popped.

{@tool sample} This sample demonstrates how to use a [LocalHistoryEntry] to show a panel that can be dismissed with the back button.

** See code in examples/api/lib/widgets/routes/local_history_entry.0.dart ** {@end-tool}

See also:

- [LocalHistoryRoute], which manages a stack of local history entries.
- [ModalRoute.addLocalHistoryEntry], which adds an entry to a route.
- [showModalBottomSheet], which internally uses local history entries to handle back button behavior.

### LocalHistoryEntry()

```dart
LocalHistoryEntry({VoidCallback? onRemove, bool impliesAppBarDismissal = true})
```

Creates an entry in the history of a [LocalHistoryRoute].

The [impliesAppBarDismissal] defaults to true if not provided.

### onRemove

```dart
VoidCallback? onRemove
```

Called when this entry is removed from the history of its associated [LocalHistoryRoute].

### impliesAppBarDismissal

```dart
bool impliesAppBarDismissal
```

Whether an [AppBar] in the route this entry belongs to should automatically add a back button or close button.

Defaults to true.

### remove()

```dart
void remove()
```

Remove this entry from the history of its associated [LocalHistoryRoute].

# LocalHistoryRoute

```dart
mixin LocalHistoryRoute<T> on Route<T> {}
```

A mixin used by routes to handle back navigations internally by popping a list.

When a [Navigator] is instructed to pop, the current route is given an opportunity to handle the pop internally. A [LocalHistoryRoute] handles the pop internally if its list of local history entries is non-empty. Rather than being removed as the current route, the most recent [LocalHistoryEntry] is removed from the list and its [LocalHistoryEntry.onRemove] is called.

See also:

- [Route], which documents the meaning of the `T` generic type argument.

### addLocalHistoryEntry()

```dart
void addLocalHistoryEntry(LocalHistoryEntry entry)
```

Adds a local history entry to this route.

When asked to pop, if this route has any local history entries, this route will handle the pop internally by removing the most recently added local history entry.

The given local history entry must not already be part of another local history route.

{@tool snippet}

The following example is an app with 2 pages: `HomePage` and `SecondPage`. The `HomePage` can navigate to the `SecondPage`.

The `SecondPage` uses a [LocalHistoryEntry] to implement local navigation within that page. Pressing 'show rectangle' displays a red rectangle and adds a local history entry. At that point, pressing the '< back' button pops the latest route, which is the local history entry, and the red rectangle disappears. Pressing the '< back' button a second time once again pops the latest route, which is the `SecondPage`, itself. Therefore, the second press navigates back to the `HomePage`.

```dart
class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: <String, WidgetBuilder>{
        '/': (BuildContext context) => const HomePage(),
        '/second_page': (BuildContext context) => const SecondPage(),
      },
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: <Widget>[
            const Text('HomePage'),
            // Press this button to open the SecondPage.
            ElevatedButton(
              child: const Text('Second Page >'),
              onPressed: () {
                Navigator.pushNamed(context, '/second_page');
              },
            ),
          ],
        ),
      ),
    );
  }
}

class SecondPage extends StatefulWidget {
  const SecondPage({super.key});

  @override
  State<SecondPage> createState() => _SecondPageState();
}

class _SecondPageState extends State<SecondPage> {

  bool _showRectangle = false;

  Future<void> _navigateLocallyToShowRectangle() async {
    // This local history entry essentially represents the display of the red
    // rectangle. When this local history entry is removed, we hide the red
    // rectangle.
    setState(() => _showRectangle = true);
    ModalRoute.of(context)?.addLocalHistoryEntry(
        LocalHistoryEntry(
            onRemove: () {
              // Hide the red rectangle.
              setState(() => _showRectangle = false);
            }
        )
    );
  }

  @override
  Widget build(BuildContext context) {
    final Widget localNavContent = _showRectangle
      ? Container(
          width: 100.0,
          height: 100.0,
          color: Colors.red,
        )
      : ElevatedButton(
          onPressed: _navigateLocallyToShowRectangle,
          child: const Text('Show Rectangle'),
        );

    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            localNavContent,
            ElevatedButton(
              child: const Text('< Back'),
              onPressed: () {
                // Pop a route. If this is pressed while the red rectangle is
                // visible then it will pop our local history entry, which
                // will hide the red rectangle. Otherwise, the SecondPage will
                // navigate back to the HomePage.
                Navigator.of(context).pop();
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

{@end-tool}

### removeLocalHistoryEntry()

```dart
void removeLocalHistoryEntry(LocalHistoryEntry entry)
```

Remove a local history entry from this route.

The entry's [LocalHistoryEntry.onRemove] callback, if any, will be called synchronously.

### willPop()

```dart
Future<RoutePopDisposition> willPop()
```

### popDisposition

```dart
RoutePopDisposition get popDisposition
```

### didPop()

```dart
bool didPop(T? result)
```

### willHandlePopInternally

```dart
bool get willHandlePopInternally
```

# ModalRoute

```dart
abstract class ModalRoute<T> extends TransitionRoute<T> with LocalHistoryRoute<T> {}
```

A route that blocks interaction with previous routes.

[ModalRoute]s cover the entire [Navigator]. They are not necessarily [opaque], however; for example, a pop-up menu uses a [ModalRoute] but only shows the menu in a small box overlapping the previous route.

The `T` type argument is the return value of the route. If there is no return value, consider using `void` as the return value.

See also:

- [Route], which further documents the meaning of the `T` generic type argument.

### ModalRoute()

```dart
ModalRoute({RouteSettings? settings, bool? requestFocus, ui.ImageFilter? filter, TraversalEdgeBehavior? traversalEdgeBehavior, TraversalEdgeBehavior? directionalTraversalEdgeBehavior})
```

Creates a route that blocks interaction with previous routes.

### filter

```dart
ui.ImageFilter? filter
```

The filter to add to the barrier.

If given, this filter will be applied to the modal barrier using [BackdropFilter]. This allows blur effects, for example.

### traversalEdgeBehavior

```dart
TraversalEdgeBehavior? traversalEdgeBehavior
```

Controls the transfer of focus beyond the first and the last items of a [FocusScopeNode].

If set to null, [Navigator.routeTraversalEdgeBehavior] is used.

### directionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior? directionalTraversalEdgeBehavior
```

Controls the directional transfer of focus beyond the first and the last items of a [FocusScopeNode].

If set to null, [Navigator.routeDirectionalTraversalEdgeBehavior] is used.

### of()

```dart
ModalRoute<T>? of<T extends Object?>(BuildContext context)
```

Returns the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

{@tool snippet}

Typical usage is as follows:

```dart
ModalRoute<int>? route = ModalRoute.of<int>(context);
```

{@end-tool}

The given [BuildContext] will be rebuilt if the state of the route changes while it is visible (specifically, if [isCurrent] or [canPop] change value).

### isCurrentOf()

```dart
bool? isCurrentOf(BuildContext context)
```

Returns [ModalRoute.isCurrent] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Use of this method will cause the given [context] to rebuild any time that the [ModalRoute.isCurrent] property of the ancestor [_ModalScopeStatus] changes.

### canPopOf()

```dart
bool? canPopOf(BuildContext context)
```

Returns [ModalRoute.canPop] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Use of this method will cause the given [context] to rebuild any time that the [ModalRoute.canPop] property of the ancestor [_ModalScopeStatus] changes.

### settingsOf()

```dart
RouteSettings? settingsOf(BuildContext context)
```

Returns [ModalRoute.settings] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Calling this method creates a dependency on the [ModalRoute] associated with the given [context]. As a result, the widget corresponding to [context] will be rebuilt whenever the route's [ModalRoute.settings] changes.

### isActiveOf()

```dart
bool? isActiveOf(BuildContext context)
```

Returns [ModalRoute.isActive] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Calling this method creates a dependency on the [ModalRoute] associated with the given [context]. As a result, the widget corresponding to [context] will be rebuilt whenever the route's [ModalRoute.isActive] changes.

### isFirstOf()

```dart
bool? isFirstOf(BuildContext context)
```

Returns [ModalRoute.isFirst] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Calling this method creates a dependency on the [ModalRoute] associated with the given [context]. As a result, the widget corresponding to [context] will be rebuilt whenever the route's [ModalRoute.isFirst] changes.

### opaqueOf()

```dart
bool? opaqueOf(BuildContext context)
```

Returns [ModalRoute.opaque] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Calling this method creates a dependency on the [ModalRoute] associated with the given [context]. As a result, the widget corresponding to [context] will be rebuilt whenever the route's [ModalRoute.opaque] changes.

### popDispositionOf()

```dart
RoutePopDisposition? popDispositionOf(BuildContext context)
```

Returns [ModalRoute.popDisposition] for the modal route most closely associated with the given context.

Returns null if the given context is not associated with a modal route.

Calling this method creates a dependency on the [ModalRoute] associated with the given [context]. As a result, the widget corresponding to [context] will be rebuilt whenever the route's [ModalRoute.popDisposition] changes.

### setState()

```dart
void setState(VoidCallback fn)
```

Schedule a call to [buildTransitions].

Whenever you need to change internal state for a [ModalRoute] object, make the change in a function that you pass to [setState], as in:

```dart
setState(() { _myState = newValue; });
```

If you just change the state directly without calling [setState], then the route will not be scheduled for rebuilding, meaning that its rendering will not be updated.

### withName()

```dart
RoutePredicate withName(String name)
```

Returns a predicate that's true if the route has the specified name and if popping the route will not yield the same route, i.e. if the route's [willHandlePopInternally] property is false.

This function is typically used with [Navigator.popUntil()].

### buildPage()

```dart
Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

Override this method to build the primary content of this route.

The arguments have the following meanings:

- `context`: The context in which the route is being built.
- [animation]: The animation for this route's transition. When entering, the animation runs forward from 0.0 to 1.0. When exiting, this animation runs backwards from 1.0 to 0.0.
- [secondaryAnimation]: The animation for the route being pushed on top of this route. This animation lets this route coordinate with the entrance and exit transition of routes pushed on top of this route.

This method is only called when the route is first built, and rarely thereafter. In particular, it is not automatically called again when the route's state changes unless it uses [ModalRoute.of]. For a builder that is called every time the route's state changes, consider [buildTransitions]. For widgets that change their behavior when the route's state changes, consider [ModalRoute.of] to obtain a reference to the route; this will cause the widget to be rebuilt each time the route changes state.

In general, [buildPage] should be used to build the page contents, and [buildTransitions] for the widgets that change as the page is brought in and out of view. Avoid using [buildTransitions] for content that never changes; building such content once from [buildPage] is more efficient.

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

Override this method to wrap the [child] with one or more transition widgets that define how the route arrives on and leaves the screen.

By default, the child (which contains the widget returned by [buildPage]) is not wrapped in any transition widgets.

The [buildTransitions] method, in contrast to [buildPage], is called each time the [Route]'s state changes while it is visible (e.g. if the value of [canPop] changes on the active route).

The [buildTransitions] method is typically used to define transitions that animate the new topmost route's comings and goings. When the [Navigator] pushes a route on the top of its stack, the new route's primary [animation] runs from 0.0 to 1.0. When the Navigator pops the topmost route, e.g. because the use pressed the back button, the primary animation runs from 1.0 to 0.0.

{@tool snippet} The following example uses the primary animation to drive a [SlideTransition] that translates the top of the new route vertically from the bottom of the screen when it is pushed on the Navigator's stack. When the route is popped the SlideTransition translates the route from the top of the screen back to the bottom.

We've used [PageRouteBuilder] to demonstrate the [buildTransitions] method here. The body of an override of the [buildTransitions] method would be defined in the same way.

```dart
PageRouteBuilder<void>(
  pageBuilder: (BuildContext context,
      Animation<double> animation,
      Animation<double> secondaryAnimation,
  ) {
    return Scaffold(
      appBar: AppBar(title: const Text('Hello')),
      body: const Center(
        child: Text('Hello World'),
      ),
    );
  },
  transitionsBuilder: (
      BuildContext context,
      Animation<double> animation,
      Animation<double> secondaryAnimation,
      Widget child,
   ) {
    return SlideTransition(
      position: Tween<Offset>(
        begin: const Offset(0.0, 1.0),
        end: Offset.zero,
      ).animate(animation),
      child: child, // child is the value returned by pageBuilder
    );
  },
)
```

{@end-tool}

When the [Navigator] pushes a route on the top of its stack, the [secondaryAnimation] can be used to define how the route that was on the top of the stack leaves the screen. Similarly when the topmost route is popped, the secondaryAnimation can be used to define how the route below it reappears on the screen. When the Navigator pushes a new route on the top of its stack, the old topmost route's secondaryAnimation runs from 0.0 to 1.0. When the Navigator pops the topmost route, the secondaryAnimation for the route below it runs from 1.0 to 0.0.

{@tool snippet} The example below adds a transition that's driven by the [secondaryAnimation]. When this route disappears because a new route has been pushed on top of it, it translates in the opposite direction of the new route. Likewise when the route is exposed because the topmost route has been popped off.

```dart
PageRouteBuilder<void>(
  pageBuilder: (BuildContext context,
      Animation<double> animation,
      Animation<double> secondaryAnimation,
  ) {
    return Scaffold(
      appBar: AppBar(title: const Text('Hello')),
      body: const Center(
        child: Text('Hello World'),
      ),
    );
  },
  transitionsBuilder: (
      BuildContext context,
      Animation<double> animation,
      Animation<double> secondaryAnimation,
      Widget child,
  ) {
    return SlideTransition(
      position: Tween<Offset>(
        begin: const Offset(0.0, 1.0),
        end: Offset.zero,
      ).animate(animation),
      child: SlideTransition(
        position: Tween<Offset>(
          begin: Offset.zero,
          end: const Offset(0.0, 1.0),
        ).animate(secondaryAnimation),
        child: child,
      ),
     );
  },
)
```

{@end-tool}

In practice the `secondaryAnimation` is used pretty rarely.

The arguments to this method are as follows:

- `context`: The context in which the route is being built.
- [animation]: When the [Navigator] pushes a route on the top of its stack, the new route's primary [animation] runs from 0.0 to 1.0. When the [Navigator] pops the topmost route this animation runs from 1.0 to 0.0.
- [secondaryAnimation]: When the Navigator pushes a new route on the top of its stack, the old topmost route's [secondaryAnimation] runs from 0.0 to 1.0. When the [Navigator] pops the topmost route, the [secondaryAnimation] for the route below it runs from 1.0 to 0.0.
- `child`, the page contents, as returned by [buildPage].

See also:

- [buildPage], which is used to describe the actual contents of the page, and whose result is passed to the `child` argument of this method.

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

The [DelegatedTransitionBuilder] provided to the route below this one in the navigation stack.

{@template flutter.widgets.delegatedTransition} Used for the purposes of coordinating transitions between two routes with different route transitions. When a route is added to the stack, the original topmost route will look for this transition, and if available, it will use the `delegatedTransition` from the incoming transition to animate off the screen.

If the return of the [DelegatedTransitionBuilder] is null, then by default the original transition of the routes will be used. This is useful if a route can conditionally provide a transition based on the [BuildContext]. {@endtemplate}

The [ModalRoute] receiving this transition will set it to their [receivedTransition] property.

{@tool dartpad} This sample shows an app that uses three different page transitions, a Material Zoom transition, the standard Cupertino sliding transition, and a custom vertical transition. All of the page routes are able to inform the previous page how to transition off the screen to sync with the new page.

** See code in examples/api/lib/widgets/routes/flexible_route_transitions.0.dart ** {@end-tool}

{@tool dartpad} This sample shows an app that uses the same transitions as the previous sample, this time in a [MaterialApp.router].

** See code in examples/api/lib/widgets/routes/flexible_route_transitions.1.dart ** {@end-tool}

### receivedTransition

```dart
DelegatedTransitionBuilder? receivedTransition
```

The [DelegatedTransitionBuilder] received from the route above this one in the navigation stack.

{@macro flutter.widgets.delegatedTransition}

The `receivedTransition` will use the above route's [delegatedTransition] in order to show the right route transition when the above route either enters or leaves the navigation stack. If not null, the `receivedTransition` will wrap the route content.

### install()

```dart
void install()
```

### didPush()

```dart
TickerFuture didPush()
```

### didAdd()

```dart
void didAdd()
```

### barrierDismissible

```dart
bool get barrierDismissible
```

{@template flutter.widgets.ModalRoute.barrierDismissible} Whether you can dismiss this route by tapping the modal barrier.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

For example, when a dialog is on the screen, the page below the dialog is usually darkened by the modal barrier.

If [barrierDismissible] is true, then tapping this barrier, pressing the escape key on the keyboard, or calling route popping functions such as [Navigator.pop] will cause the current route to be popped with null as the value.

If [barrierDismissible] is false, then tapping the barrier has no effect.

If this getter would ever start returning a different value, either [changedInternalState] or [changedExternalState] should be invoked so that the change can take effect.

It is safe to use `navigator.context` to look up inherited widgets here, because the [Navigator] calls [changedExternalState] whenever its dependencies change, and [changedExternalState] causes the modal barrier to rebuild.

See also:

- [Navigator.pop], which is used to dismiss the route.
- [barrierColor], which controls the color of the scrim for this route.
- [ModalBarrier], the widget that implements this feature. {@endtemplate}

### semanticsDismissible

```dart
bool get semanticsDismissible
```

Whether the semantics of the modal barrier are included in the semantics tree.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

If [semanticsDismissible] is true, then modal barrier semantics are included in the semantics tree.

If [semanticsDismissible] is false, then modal barrier semantics are excluded from the semantics tree and tapping on the modal barrier has no effect.

If this getter would ever start returning a different value, either [changedInternalState] or [changedExternalState] should be invoked so that the change can take effect.

It is safe to use `navigator.context` to look up inherited widgets here, because the [Navigator] calls [changedExternalState] whenever its dependencies change, and [changedExternalState] causes the modal barrier to rebuild.

### barrierColor

```dart
Color? get barrierColor
```

{@template flutter.widgets.ModalRoute.barrierColor} The color to use for the modal barrier. If this is null, the barrier will be transparent.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

For example, when a dialog is on the screen, the page below the dialog is usually darkened by the modal barrier.

The color is ignored, and the barrier made invisible, when [ModalRoute.offstage] is true.

While the route is animating into position, the color is animated from transparent to the specified color. {@endtemplate}

If this getter would ever start returning a different color, one of the [changedInternalState] or [changedExternalState] methods should be invoked so that the change can take effect.

It is safe to use `navigator.context` to look up inherited widgets here, because the [Navigator] calls [changedExternalState] whenever its dependencies change, and [changedExternalState] causes the modal barrier to rebuild.

{@tool snippet}

For example, to make the barrier color use the theme's background color, one could say:

```dart
Color get barrierColor => Theme.of(navigator.context).colorScheme.surface;
```

{@end-tool}

See also:

- [barrierDismissible], which controls the behavior of the barrier when tapped.
- [ModalBarrier], the widget that implements this feature.

### barrierLabel

```dart
String? get barrierLabel
```

{@template flutter.widgets.ModalRoute.barrierLabel} The semantic label used for a dismissible barrier.

If the barrier is dismissible, this label will be read out if accessibility tools (like VoiceOver on iOS) focus on the barrier.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

For example, when a dialog is on the screen, the page below the dialog is usually darkened by the modal barrier. {@endtemplate}

If this getter would ever start returning a different label, either [changedInternalState] or [changedExternalState] should be invoked so that the change can take effect.

It is safe to use `navigator.context` to look up inherited widgets here, because the [Navigator] calls [changedExternalState] whenever its dependencies change, and [changedExternalState] causes the modal barrier to rebuild.

See also:

- [barrierDismissible], which controls the behavior of the barrier when tapped.
- [ModalBarrier], the widget that implements this feature.

### barrierCurve

```dart
Curve get barrierCurve
```

The curve that is used for animating the modal barrier in and out.

The modal barrier is the scrim that is rendered behind each route, which generally prevents the user from interacting with the route below the current route, and normally partially obscures such routes.

For example, when a dialog is on the screen, the page below the dialog is usually darkened by the modal barrier.

While the route is animating into position, the color is animated from transparent to the specified [barrierColor].

If this getter would ever start returning a different curve, either [changedInternalState] or [changedExternalState] should be invoked so that the change can take effect.

It is safe to use `navigator.context` to look up inherited widgets here, because the [Navigator] calls [changedExternalState] whenever its dependencies change, and [changedExternalState] causes the modal barrier to rebuild.

It defaults to [Curves.ease].

See also:

- [barrierColor], which determines the color that the modal transitions to.
- [Curves] for a collection of common curves.
- [AnimatedModalBarrier], the widget that implements this feature.

### maintainState

```dart
bool get maintainState
```

{@template flutter.widgets.ModalRoute.maintainState} Whether the route should remain in memory when it is inactive.

If this is true, then the route is maintained, so that any futures it is holding from the next route will properly resolve when the next route pops. If this is not necessary, this can be set to false to allow the framework to entirely discard the route's widget hierarchy when it is not visible.

Setting [maintainState] to false does not guarantee that the route will be discarded. For instance, it will not be discarded if it is still visible because the next above it is not opaque (e.g. it is a popup dialog). {@endtemplate}

If this getter would ever start returning a different value, the [changedInternalState] should be invoked so that the change can take effect.

See also:

- [OverlayEntry.maintainState], which is the underlying implementation of this property.

### popGestureInProgress

```dart
bool get popGestureInProgress
```

True if a back gesture (iOS-style back swipe or Android predictive back) is currently underway for this route.

See also:

- [popGestureEnabled], which returns true if a user-triggered pop gesture would be allowed.

### popGestureEnabled

```dart
bool get popGestureEnabled
```

Whether a pop gesture can be started by the user for this route.

Returns true if the user can edge-swipe to a previous route.

This should only be used between frames, not during build.

### offstage

```dart
bool get offstage
```

Whether this route is currently offstage.

On the first frame of a route's entrance transition, the route is built [Offstage] using an animation progress of 1.0. The route is invisible and non-interactive, but each widget has its final size and position. This mechanism lets the [HeroController] determine the final local of any hero widgets being animated as part of the transition.

The modal barrier, if any, is not rendered if [offstage] is true (see [barrierColor]).

Whenever this changes value, [changedInternalState] is called.

### offstage

```dart
set offstage(bool value)
```

### subtreeContext

```dart
BuildContext? get subtreeContext
```

The build context for the subtree containing the primary content of this route.

### animation

```dart
Animation<double>? get animation
```

### secondaryAnimation

```dart
Animation<double>? get secondaryAnimation
```

### willPop()

```dart
Future<RoutePopDisposition> willPop()
```

Returns [RoutePopDisposition.doNotPop] if any of callbacks added with [addScopedWillPopCallback] returns either false or null. If they all return true, the base [Route.willPop]'s result will be returned. The callbacks will be called in the order they were added, and will only be called if all previous callbacks returned true.

Typically this method is not overridden because applications usually don't create modal routes directly, they use higher level primitives like [showDialog]. The scoped [WillPopCallback] list makes it possible for ModalRoute descendants to collectively define the value of [willPop].

See also:

- [Form], which provides an `onWillPop` callback that uses this mechanism.
- [addScopedWillPopCallback], which adds a callback to the list this method checks.
- [removeScopedWillPopCallback], which removes a callback from the list this method checks.

### popDisposition

```dart
RoutePopDisposition get popDisposition
```

Returns [RoutePopDisposition.doNotPop] if any of the [PopEntry] instances registered with [registerPopEntry] have [PopEntry.canPopNotifier] set to false.

Typically this method is not overridden because applications usually don't create modal routes directly, they use higher level primitives like [showDialog]. The scoped [PopEntry] list makes it possible for ModalRoute descendants to collectively define the value of [popDisposition].

See also:

- [Form], which provides an `onPopInvokedWithResult` callback that is similar.
- [registerPopEntry], which adds a [PopEntry] to the list this method checks.
- [unregisterPopEntry], which removes a [PopEntry] from the list this method checks.

### onPopInvokedWithResult()

```dart
void onPopInvokedWithResult(bool didPop, T? result)
```

### addScopedWillPopCallback()

```dart
void addScopedWillPopCallback(WillPopCallback callback)
```

Enables this route to veto attempts by the user to dismiss it.

This callback runs asynchronously and it's possible that it will be called after its route has been disposed. The callback should check [State.mounted] before doing anything.

A typical application of this callback would be to warn the user about unsaved [Form] data if the user attempts to back out of the form. In that case, use the [Form.onWillPop] property to register the callback.

See also:

- [WillPopScope], which manages the registration and unregistration process automatically.
- [Form], which provides an `onWillPop` callback that uses this mechanism.
- [willPop], which runs the callbacks added with this method.
- [removeScopedWillPopCallback], which removes a callback from the list that [willPop] checks.

### removeScopedWillPopCallback()

```dart
void removeScopedWillPopCallback(WillPopCallback callback)
```

Remove one of the callbacks run by [willPop].

See also:

- [Form], which provides an `onWillPop` callback that uses this mechanism.
- [addScopedWillPopCallback], which adds callback to the list checked by [willPop].

### registerPopEntry()

```dart
void registerPopEntry(PopEntry<Object?> popEntry)
```

Registers the existence of a [PopEntry] in the route.

[PopEntry] instances registered in this way will have their [PopEntry.onPopInvokedWithResult] callbacks called when a route is popped or a pop is attempted. They will also be able to block pop operations with [PopEntry.canPopNotifier] through this route's [popDisposition] method.

See also:

- [unregisterPopEntry], which performs the opposite operation.

### unregisterPopEntry()

```dart
void unregisterPopEntry(PopEntry<Object?> popEntry)
```

Unregisters a [PopEntry] in the route's widget subtree.

See also:

- [registerPopEntry], which performs the opposite operation.

### hasScopedWillPopCallback

```dart
bool get hasScopedWillPopCallback
```

True if one or more [WillPopCallback] callbacks exist.

This method is used to disable the horizontal swipe pop gesture supported by [MaterialPageRoute] for [TargetPlatform.iOS] and [TargetPlatform.macOS]. If a pop might be vetoed, then the back gesture is disabled.

The [buildTransitions] method will not be called again if this changes, since it can change during the build as descendants of the route add or remove callbacks.

See also:

- [addScopedWillPopCallback], which adds a callback.
- [removeScopedWillPopCallback], which removes a callback.
- [willHandlePopInternally], which reports on another reason why a pop might be vetoed.

### didChangePrevious()

```dart
void didChangePrevious(Route<dynamic>? previousRoute)
```

### didChangeNext()

```dart
void didChangeNext(Route<dynamic>? nextRoute)
```

### didPopNext()

```dart
void didPopNext(Route<dynamic> nextRoute)
```

### changedInternalState()

```dart
void changedInternalState()
```

### changedExternalState()

```dart
void changedExternalState()
```

### canPop

```dart
bool get canPop
```

Whether this route can be popped.

A route can be popped if there is at least one active route below it, or if [willHandlePopInternally] returns true.

When this changes, if the route is visible, the route will rebuild, and any widgets that used [ModalRoute.of] will be notified.

### impliesAppBarDismissal

```dart
bool get impliesAppBarDismissal
```

Whether an [AppBar] in the route should automatically add a back button or close button.

This getter returns true if there is at least one active route below it, or there is at least one [LocalHistoryEntry] with [impliesAppBarDismissal] set to true

### fullscreenDialog

```dart
bool get fullscreenDialog
```

{@macro flutter.widgets.RawDialogRoute.fullscreenDialog}

### buildModalBarrier()

```dart
Widget buildModalBarrier()
```

Build the barrier for this [ModalRoute], subclasses can override this method to create their own barrier with customized features such as color or accessibility focus size.

See also:

- [ModalBarrier], which is typically used to build a barrier.
- [ModalBottomSheetRoute], which overrides this method to build a customized barrier.

### createOverlayEntries()

```dart
Iterable<OverlayEntry> createOverlayEntries()
```

### toString()

```dart
String toString()
```

# PopupRoute

```dart
abstract class PopupRoute<T> extends ModalRoute<T> {}
```

A modal route that overlays a widget over the current route.

{@macro flutter.widgets.ModalRoute.barrierDismissible}

{@tool dartpad} This example shows how to create a dialog box that is dismissible.

** See code in examples/api/lib/widgets/routes/popup_route.0.dart ** {@end-tool}

See also:

- [ModalRoute], which is the base class for this class.
- [Navigator.pop], which is used to dismiss the route.

### PopupRoute()

```dart
PopupRoute({RouteSettings? settings, bool? requestFocus, dynamic filter, TraversalEdgeBehavior? traversalEdgeBehavior, TraversalEdgeBehavior? directionalTraversalEdgeBehavior})
```

Initializes the [PopupRoute].

### opaque

```dart
bool get opaque
```

### maintainState

```dart
bool get maintainState
```

### allowSnapshotting

```dart
bool get allowSnapshotting
```

# RouteObserver

```dart
class RouteObserver<R extends Route<dynamic>> extends NavigatorObserver {}
```

A [Navigator] observer that notifies [RouteAware]s of changes to the state of their [Route].

[RouteObserver] informs subscribers whenever a route of type `R` is pushed on top of their own route of type `R` or popped from it. This is for example useful to keep track of page transitions, e.g. a `RouteObserver<PageRoute>` will inform subscribed [RouteAware]s whenever the user navigates away from the current page route to another page route.

To be informed about route changes of any type, consider instantiating a `RouteObserver<Route>`.

## Type arguments

When using more aggressive [lints](https://dart.dev/lints), in particular lints such as `always_specify_types`, the Dart analyzer will require that certain types be given with their type arguments. Since the [Route] class and its subclasses have a type argument, this includes the arguments passed to this class. Consider using `dynamic` to specify the entire class of routes rather than only specific subtypes. For example, to watch for all [ModalRoute] variants, the `RouteObserver<ModalRoute<dynamic>>` type may be used.

{@tool dartpad} This example demonstrates how to implement a [RouteObserver] that notifies [RouteAware] widget of changes to the state of their [Route].

** See code in examples/api/lib/widgets/routes/route_observer.0.dart ** {@end-tool}

See also:

- [RouteAware], this is used with [RouteObserver] to make a widget aware of changes to the [Navigator]'s session history.

### debugObservingRoute()

```dart
bool debugObservingRoute(R route)
```

Whether this observer is managing changes for the specified route.

If asserts are disabled, this method will throw an exception.

### subscribe()

```dart
void subscribe(RouteAware routeAware, R route)
```

Subscribe [routeAware] to be informed about changes to [route].

Going forward, [routeAware] will be informed about qualifying changes to [route], e.g. when [route] is covered by another route or when [route] is popped off the [Navigator] stack.

### unsubscribe()

```dart
void unsubscribe(RouteAware routeAware)
```

Unsubscribe [routeAware].

[routeAware] is no longer informed about changes to its route. If the given argument was subscribed to multiple types, this will unregister it (once) from each type.

### didPop()

```dart
void didPop(Route<dynamic> route, Route<dynamic>? previousRoute)
```

### didPush()

```dart
void didPush(Route<dynamic> route, Route<dynamic>? previousRoute)
```

# RouteAware

```dart
abstract mixin class RouteAware {}
```

An interface for objects that are aware of their current [Route].

This is used with [RouteObserver] to make a widget aware of changes to the [Navigator]'s session history.

### didPopNext()

```dart
void didPopNext()
```

Called when the top route has been popped off, and the current route shows up.

### didPush()

```dart
void didPush()
```

Called when the current route has been pushed.

### didPop()

```dart
void didPop()
```

Called when the current route has been popped off.

### didPushNext()

```dart
void didPushNext()
```

Called when a new route has been pushed on top of this route, temporarily obscuring it.

This method is called synchronously during the push operation, before the transition animation completes. The current route may still be partially visible as it animates out. To perform actions after the route is fully obscured, consider using [ModalRoute.secondaryAnimation] to listen for animation completion, for example:

{@tool snippet}

```dart
ModalRoute.of(context)?.secondaryAnimation?.addStatusListener((AnimationStatus status) {
  if (status == AnimationStatus.completed) {
    // This route is now fully obscured by the new route.
  }
});
```

{@end-tool}

# RawDialogRoute

```dart
class RawDialogRoute<T> extends PopupRoute<T> {}
```

A general dialog route which allows for customization of the dialog popup.

It is used internally by [showGeneralDialog] or can be directly pushed onto the [Navigator] stack to enable state restoration. See [showGeneralDialog] for a state restoration app example.

This function takes a `pageBuilder`, which typically builds a dialog. Content below the dialog is dimmed with a [ModalBarrier]. The widget returned by the `builder` does not share a context with the location that `showDialog` is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the dialog needs to update dynamically.

The `barrierDismissible` argument is used to indicate whether tapping on the barrier will dismiss the dialog. It is `true` by default and cannot be `null`.

The `barrierColor` argument is used to specify the color of the modal barrier that darkens everything below the dialog. If `null`, the default color `Colors.black54` is used.

The `settings` argument define the settings for this route. See [RouteSettings] for details.

{@template flutter.widgets.RawDialogRoute} A [DisplayFeature] can split the screen into sub-screens. The closest one to [anchorPoint] is used to render the content.

If no [anchorPoint] is provided, then [Directionality] is used:

- for [TextDirection.ltr], [anchorPoint] is `Offset.zero`, which will cause the content to appear in the top-left sub-screen.
- for [TextDirection.rtl], [anchorPoint] is `Offset(double.maxFinite, 0)`, which will cause the content to appear in the top-right sub-screen.

If no [anchorPoint] is provided, and there is no [Directionality] ancestor widget in the tree, then the widget asserts during build in debug mode. {@endtemplate}

See also:

- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- [showGeneralDialog], which is a way to display a RawDialogRoute.
- [showDialog], which is a way to display a DialogRoute.
- [showCupertinoDialog], which displays an iOS-style dialog.

### RawDialogRoute()

```dart
RawDialogRoute({required RoutePageBuilder pageBuilder, bool barrierDismissible = true, Color? barrierColor = const Color(0x80000000), String? barrierLabel, Duration transitionDuration = const Duration(milliseconds: 200), RouteTransitionsBuilder? transitionBuilder, RouteSettings? settings, bool? requestFocus, Offset? anchorPoint, TraversalEdgeBehavior? traversalEdgeBehavior, TraversalEdgeBehavior? directionalTraversalEdgeBehavior, bool fullscreenDialog = false})
```

A general dialog route which allows for customization of the dialog popup.

### barrierDismissible

```dart
bool get barrierDismissible
```

### barrierLabel

```dart
String? get barrierLabel
```

### barrierColor

```dart
Color? get barrierColor
```

### transitionDuration

```dart
Duration get transitionDuration
```

### anchorPoint

```dart
Offset? anchorPoint
```

{@macro flutter.widgets.DisplayFeatureSubScreen.anchorPoint}

### fullscreenDialog

```dart
bool fullscreenDialog
```

{@template flutter.widgets.RawDialogRoute.fullscreenDialog} Whether this route is a full-screen dialog.

In Material and Cupertino, being fullscreen has the effects of making the app bars have a close button instead of a back button. On iOS, dialogs transitions animate differently and are also not closeable with the back swipe gesture. {@endtemplate}

### buildPage()

```dart
Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# showGeneralDialog()

```dart
Future<T?> showGeneralDialog<T extends Object?>({required BuildContext context, required RoutePageBuilder pageBuilder, bool barrierDismissible = false, String? barrierLabel, Color barrierColor = const Color(0x80000000), Duration transitionDuration = const Duration(milliseconds: 200), RouteTransitionsBuilder? transitionBuilder, bool useRootNavigator = true, bool fullscreenDialog = false, RouteSettings? routeSettings, Offset? anchorPoint, bool? requestFocus})
```

Displays a dialog above the current contents of the app.

This function allows for customization of aspects of the dialog popup.

This function takes a `pageBuilder` which is used to build the primary content of the route (typically a dialog widget). Content below the dialog is dimmed with a [ModalBarrier]. The widget returned by the `pageBuilder` does not share a context with the location that [showGeneralDialog] is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the dialog needs to update dynamically.

The `context` argument is used to look up the [Navigator] for the dialog. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the dialog is closed.

The `useRootNavigator` argument is used to determine whether to push the dialog to the [Navigator] furthest from or nearest to the given `context`. By default, `useRootNavigator` is `true` and the dialog route created by this method is pushed to the root navigator.

If the application has multiple [Navigator] objects, it may be necessary to call `Navigator.of(context, rootNavigator: true).pop(result)` to close the dialog rather than just `Navigator.pop(context, result)`.

The `barrierDismissible` argument is used to determine whether this route can be dismissed by tapping the modal barrier. This argument defaults to false. If `barrierDismissible` is true, a non-null `barrierLabel` must be provided.

The `barrierLabel` argument is the semantic label used for a dismissible barrier. This argument defaults to `null`.

The `barrierColor` argument is the color used for the modal barrier. This argument defaults to `Color(0x80000000)`.

The `transitionDuration` argument is used to determine how long it takes for the route to arrive on or leave off the screen. This argument defaults to 200 milliseconds.

The `transitionBuilder` argument is used to define how the route arrives on and leaves off the screen. By default, the transition is a linear fade of the page's contents.

The `routeSettings` will be used in the construction of the dialog's route. See [RouteSettings] for more details.

{@macro flutter.material.dialog.requestFocus} {@macro flutter.widgets.navigator.Route.requestFocus}

{@macro flutter.widgets.RawDialogRoute}

Returns a [Future] that resolves to the value (if any) that was passed to [Navigator.pop] when the dialog was closed.

### State Restoration in Dialogs

Using this method will not enable state restoration for the dialog. In order to enable state restoration for a dialog, use [Navigator.restorablePush] or [Navigator.restorablePushNamed] with [RawDialogRoute].

For more information about state restoration, see [RestorationManager].

{@tool sample} This sample demonstrates how to create a restorable dialog. This is accomplished by enabling state restoration by specifying [WidgetsApp.restorationScopeId] and using [Navigator.restorablePush] to push [RawDialogRoute] when the button is tapped.

{@macro flutter.widgets.RestorationManager}

** See code in examples/api/lib/widgets/routes/show_general_dialog.0.dart ** {@end-tool}

See also:

- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- [showDialog], which displays a Material-style dialog.
- [showCupertinoDialog], which displays an iOS-style dialog.

# RoutePageBuilder

```dart
typedef RoutePageBuilder = Widget Function(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

Signature for the function that builds a route's primary contents. Used in [PageRouteBuilder] and [showGeneralDialog].

See [ModalRoute.buildPage] for complete definition of the parameters.

# RouteTransitionsBuilder

```dart
typedef RouteTransitionsBuilder = Widget Function(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

Signature for the function that builds a route's transitions. Used in [PageRouteBuilder] and [showGeneralDialog].

The [animation] argument drives this route's transition when it is pushed onto or popped off the [Navigator]. The [secondaryAnimation] argument lets this route coordinate with the transition of the route above it: when a new route is pushed on top of this one, this route's [secondaryAnimation] runs from 0.0 to 1.0, and when that route is popped it runs from 1.0 to 0.0.

A route only receives a running [secondaryAnimation] when this route's [TransitionRoute.canTransitionTo] method and the next route's [TransitionRoute.canTransitionFrom] method both return true. Otherwise, [secondaryAnimation] remains [kAlwaysDismissedAnimation].

See [ModalRoute.buildTransitions] for complete definition of the parameters.

# PopInvokedWithResultCallback

```dart
typedef PopInvokedWithResultCallback<T> = void Function(bool didPop, T? result)
```

A callback type for informing that a navigation pop has been invoked, whether or not it was handled successfully.

Accepts a didPop boolean indicating whether or not back navigation succeeded.

The `result` contains the pop result.

# PopEntry

```dart
abstract class PopEntry<T> {}
```

Allows listening to and preventing pops.

Can be registered in [ModalRoute] to listen to pops with [onPopInvokedWithResult] or to enable/disable them with [canPopNotifier].

See also:

- [PopScope], which provides similar functionality in a widget.
- [ModalRoute.registerPopEntry], which unregisters instances of this.
- [ModalRoute.unregisterPopEntry], which unregisters instances of this.

### onPopInvoked()

```dart
void onPopInvoked(bool didPop)
```

{@macro flutter.widgets.PopScope.onPopInvokedWithResult}

### onPopInvokedWithResult()

```dart
void onPopInvokedWithResult(bool didPop, T? result)
```

{@macro flutter.widgets.PopScope.onPopInvokedWithResult}

### canPopNotifier

```dart
ValueListenable<bool> get canPopNotifier
```

{@macro flutter.widgets.PopScope.canPop}

### toString()

```dart
String toString()
```
