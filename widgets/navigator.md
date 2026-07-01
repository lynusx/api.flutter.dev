@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'form.dart'; @docImport 'pages.dart'; @docImport 'pop_scope.dart'; @docImport 'router.dart'; @docImport 'will_pop_scope.dart';

# RouteFactory

```dart
typedef RouteFactory = Route<dynamic>? Function(RouteSettings settings)
```

Creates a route for the given route settings.

Used by [Navigator.onGenerateRoute].

See also:

- [Navigator], which is where all the [Route]s end up.

# RouteListFactory

```dart
typedef RouteListFactory = List<Route<dynamic>> Function(NavigatorState navigator, String initialRoute)
```

Creates a series of one or more routes.

Used by [Navigator.onGenerateInitialRoutes].

# RestorableRouteBuilder

```dart
typedef RestorableRouteBuilder<T> = Route<T> Function(BuildContext context, Object? arguments)
```

Creates a [Route] that is to be added to a [Navigator].

The route can be configured with the provided `arguments`. The provided `context` is the `BuildContext` of the [Navigator] to which the route is added.

Used by the restorable methods of the [Navigator] that add anonymous routes (e.g. [NavigatorState.restorablePush]). For this use case, the [RestorableRouteBuilder] must be static function annotated with `@pragma('vm:entry-point')`. The [Navigator] will call it again during state restoration to re-create the route.

# RoutePredicate

```dart
typedef RoutePredicate = bool Function(Route<dynamic> route)
```

Signature for the [Navigator.popUntil] predicate argument.

# WillPopCallback

```dart
typedef WillPopCallback = Future<bool> Function()
```

Signature for a callback that verifies that it's OK to call [Navigator.pop].

Used by [Form.onWillPop], [ModalRoute.addScopedWillPopCallback], [ModalRoute.removeScopedWillPopCallback], and [WillPopScope].

# PopPageCallback

```dart
typedef PopPageCallback = bool Function(Route<dynamic> route, dynamic result)
```

Signature for the [Navigator.onPopPage] callback.

This callback must call [Route.didPop] on the specified route and must properly update the pages list the next time it is passed into [Navigator.pages] so that it no longer includes the corresponding [Page]. (Otherwise, the page will be interpreted as a new page to show when the [Navigator.pages] list is next updated.)

# DidRemovePageCallback

```dart
typedef DidRemovePageCallback = void Function(Page<Object?> page)
```

Signature for the [Navigator.onDidRemovePage] callback.

This must properly update the pages list the next time it is passed into [Navigator.pages] so that it no longer includes the input `page`. (Otherwise, the page will be interpreted as a new page to show when the [Navigator.pages] list is next updated.)

# RoutePopDisposition

```dart
enum RoutePopDisposition {}
```

Indicates whether the current route should be popped.

Used as the return value for [Route.willPop].

See also:

- [WillPopScope], a widget that hooks into the route's [Route.willPop] mechanism.

Pop the route.

If [Route.willPop] or [Route.popDisposition] return [pop] then the back button will actually pop the current route.

Do not pop the route.

If [Route.willPop] or [Route.popDisposition] return [doNotPop] then the back button will be ignored.

Delegate this to the next level of navigation.

If [Route.willPop] or [Route.popDisposition] return [bubble] then the back button will be handled by the [SystemNavigator], which will usually close the application.

# Route

```dart
abstract class Route<T> extends _RoutePlaceholder {}
```

An abstraction for an entry managed by a [Navigator].

This class defines an abstract interface between the navigator and the "routes" that are pushed on and popped off the navigator. Most routes have visual affordances, which they place in the navigators [Overlay] using one or more [OverlayEntry] objects.

See [Navigator] for more explanation of how to use a [Route] with navigation, including code examples.

See [MaterialPageRoute] for a route that replaces the entire screen with a platform-adaptive transition.

A route can belong to a page if the [settings] are a subclass of [Page]. A page-based route, as opposed to a pageless route, is created from [Page.createRoute] during [Navigator.pages] updates. The page associated with this route may change during the lifetime of the route. If the [Navigator] updates the page of this route, it calls [changedInternalState] to notify the route that the page has been updated.

The type argument `T` is the route's return type, as used by [currentResult], [popped], and [didPop]. The type `void` may be used if the route does not return a value.

### Route()

```dart
Route({RouteSettings? settings, bool? requestFocus})
```

Initialize the [Route].

If the [settings] are not provided, an empty [RouteSettings] object is used instead.

{@template flutter.widgets.navigator.Route.requestFocus} If [requestFocus] is not provided, the value of [Navigator.requestFocus] is used instead. {@endtemplate}

### requestFocus

```dart
bool get requestFocus
```

When the route state is updated, request focus if the current route is at the top.

If not provided in the constructor, [Navigator.requestFocus] is used instead.

### navigator

```dart
NavigatorState? get navigator
```

The navigator that the route is in, if any.

### settings

```dart
RouteSettings get settings
```

The settings for this route.

See [RouteSettings] for details.

The settings can change during the route's lifetime. If the settings change, the route's overlays will be marked dirty (see [changedInternalState]).

If the route is created from a [Page] in the [Navigator.pages] list, then this will be a [Page] subclass, and it will be updated each time its corresponding [Page] in the [Navigator.pages] has changed. Once the [Route] is removed from the history, this value stops updating (and remains with its last value).

### restorationScopeId

```dart
ValueListenable<String?> get restorationScopeId
```

The restoration scope ID to be used for the [RestorationScope] surrounding this route.

The restoration scope ID is null if restoration is currently disabled for this route.

If the restoration scope ID changes (e.g. because restoration is enabled or disabled) during the life of the route, the [ValueListenable] notifies its listeners. As an example, the ID changes to null while the route is transitioning off screen, which triggers a notification on this field. At that point, the route is considered as no longer present for restoration purposes and its state will not be restored.

### overlayEntries

```dart
List<OverlayEntry> get overlayEntries
```

The overlay entries of this route.

These are typically populated by [install]. The [Navigator] is in charge of adding them to and removing them from the [Overlay].

There must be at least one entry in this list after [install] has been invoked.

The [Navigator] will take care of keeping the entries together if the route is moved in the history.

### install()

```dart
void install()
```

Called when the route is inserted into the navigator.

Uses this to populate [overlayEntries]. There must be at least one entry in this list after [install] has been invoked. The [Navigator] will be in charge to add them to the [Overlay] or remove them from it by calling [OverlayEntry.remove].

### didPush()

```dart
TickerFuture didPush()
```

Called after [install] when the route is pushed onto the navigator.

The returned value resolves when the push transition is complete.

The [didAdd] method will be called instead of [didPush] when the route immediately appears on screen without any push transition.

The [didChangeNext] and [didChangePrevious] methods are typically called immediately after this method is called.

### didAdd()

```dart
void didAdd()
```

Called after [install] when the route is added to the navigator.

This method is called instead of [didPush] when the route immediately appears on screen without any push transition.

The [didChangeNext] and [didChangePrevious] methods are typically called immediately after this method is called.

### didReplace()

```dart
void didReplace(Route<dynamic>? oldRoute)
```

Called after [install] when the route replaced another in the navigator.

The [didChangeNext] and [didChangePrevious] methods are typically called immediately after this method is called.

### willPop()

```dart
Future<RoutePopDisposition> willPop()
```

Returns whether calling [Navigator.maybePop] when this [Route] is current ([isCurrent]) should do anything.

[Navigator.maybePop] is usually used instead of [Navigator.pop] to handle the system back button.

By default, if a [Route] is the first route in the history (i.e., if [isFirst]), it reports that pops should be bubbled ([RoutePopDisposition.bubble]). This behavior prevents the user from popping the first route off the history and being stranded at a blank screen; instead, the larger scope is popped (e.g. the application quits, so that the user returns to the previous application).

In other cases, the default behavior is to accept the pop ([RoutePopDisposition.pop]).

The third possible value is [RoutePopDisposition.doNotPop], which causes the pop request to be ignored entirely.

See also:

- [Form], which provides a [Form.onWillPop] callback that uses this mechanism.
- [WillPopScope], another widget that provides a way to intercept the back button.

### popDisposition

```dart
RoutePopDisposition get popDisposition
```

Returns whether calling [Navigator.maybePop] when this [Route] is current ([isCurrent]) should do anything.

[Navigator.maybePop] is usually used instead of [Navigator.pop] to handle the system back button, when it hasn't been disabled via [SystemNavigator.setFrameworkHandlesBack].

By default, if a [Route] is the first route in the history (i.e., if [isFirst]), it reports that pops should be bubbled ([RoutePopDisposition.bubble]). This behavior prevents the user from popping the first route off the history and being stranded at a blank screen; instead, the larger scope is popped (e.g. the application quits, so that the user returns to the previous application).

In other cases, the default behavior is to accept the pop ([RoutePopDisposition.pop]).

The third possible value is [RoutePopDisposition.doNotPop], which causes the pop request to be ignored entirely.

See also:

- [Form], which provides a [Form.canPop] boolean that is similar.
- [PopScope], a widget that provides a way to intercept the back button.
- [Page.canPop], a way for [Page] to affect this property.

### onPopInvoked()

```dart
void onPopInvoked(bool didPop)
```

Called after a route pop was handled.

Even when the pop is canceled, for example by a [PopScope] widget, this will still be called. The `didPop` parameter indicates whether or not the back navigation actually happened successfully.

### onPopInvokedWithResult()

```dart
void onPopInvokedWithResult(bool didPop, T? result)
```

{@template flutter.widgets.navigator.onPopInvokedWithResult} Called after a route pop was handled.

Even when the pop is canceled, for example by a [PopScope] widget, this will still be called. The `didPop` parameter indicates whether or not the back navigation actually happened successfully. {@endtemplate}

### willHandlePopInternally

```dart
bool get willHandlePopInternally
```

Whether calling [didPop] would return false.

### currentResult

```dart
T? get currentResult
```

When this route is popped (see [Navigator.pop]) if the result isn't specified or if it's null, this value will be used instead.

This fallback is implemented by [didComplete]. This value is used if the argument to that method is null.

### popped

```dart
Future<T?> get popped
```

A future that completes when this route is popped off the navigator.

The future completes with the value given to [Navigator.pop], if any, or else the value of [currentResult]. See [didComplete] for more discussion on this topic.

### didPop()

```dart
bool didPop(T? result)
```

A request was made to pop this route. If the route can handle it internally (e.g. because it has its own stack of internal state) then return false, otherwise return true (by returning the value of calling `super.didPop`). Returning false will prevent the default behavior of [NavigatorState.pop].

When this function returns true, the navigator removes this route from the history but does not yet call [dispose]. Instead, it is the route's responsibility to call [NavigatorState.finalizeRoute], which will in turn call [dispose] on the route. This sequence lets the route perform an exit animation (or some other visual effect) after being popped but prior to being disposed.

This method should call [didComplete] to resolve the [popped] future (and this is all that the default implementation does); routes should not wait for their exit animation to complete before doing so.

See [popped], [didComplete], and [currentResult] for a discussion of the `result` argument.

### didComplete()

```dart
void didComplete(T? result)
```

The route was popped or is otherwise being removed somewhat gracefully.

This is called by [didPop] and in response to [NavigatorState.pushReplacement]. If [didPop] was not called, then the [NavigatorState.finalizeRoute] method must be called immediately, and no exit animation will run.

The [popped] future is completed by this method. The `result` argument specifies the value that this future is completed with, unless it is null, in which case [currentResult] is used instead.

This should be called before the pop animation, if any, takes place, though in some cases the animation may be driven by the user before the route is committed to being popped; this can in particular happen with the iOS-style back gesture. See [NavigatorState.didStartUserGesture].

### didPopNext()

```dart
void didPopNext(Route<dynamic> nextRoute)
```

The given route, which was above this one, has been popped off the navigator.

This route is now the current route ([isCurrent] is now true), and there is no next route.

### didChangeNext()

```dart
void didChangeNext(Route<dynamic>? nextRoute)
```

This route's next route has changed to the given new route.

This is called on a route whenever the next route changes for any reason, so long as it is in the history, including when a route is first added to a [Navigator] (e.g. by [Navigator.push]), except for cases when [didPopNext] would be called.

The `nextRoute` argument will be null if there's no new next route (i.e. if [isCurrent] is true).

### didChangePrevious()

```dart
void didChangePrevious(Route<dynamic>? previousRoute)
```

This route's previous route has changed to the given new route.

This is called on a route whenever the previous route changes for any reason, so long as it is in the history, except for immediately after the route itself has been pushed (in which case [didPush] or [didReplace] will be called instead).

The `previousRoute` argument will be null if there's no previous route (i.e. if [isFirst] is true).

### changedInternalState()

```dart
void changedInternalState()
```

Called whenever the internal state of the route has changed.

This should be called whenever [willHandlePopInternally], [didPop], [ModalRoute.offstage], or other internal state of the route changes value. It is used by [ModalRoute], for example, to report the new information via its inherited widget to any children of the route.

See also:

- [changedExternalState], which is called when the [Navigator] has updated in some manner that might affect the routes.

### changedExternalState()

```dart
void changedExternalState()
```

Called whenever the [Navigator] has updated in some manner that might affect routes, to indicate that the route may wish to rebuild as well.

This is called by the [Navigator] whenever the [NavigatorState]'s [State.widget] changes (as in [State.didUpdateWidget]), for example because the [MaterialApp] has been rebuilt. This ensures that routes that directly refer to the state of the widget that built the [MaterialApp] will be notified when that widget rebuilds, since it would otherwise be difficult to notify the routes that state they depend on may have changed.

It is also called whenever the [Navigator]'s dependencies change (as in [State.didChangeDependencies]). This allows routes to use the [Navigator]'s context ([NavigatorState.context]), for example in [ModalRoute.barrierColor], and update accordingly.

The [ModalRoute] subclass overrides this to force the barrier overlay to rebuild.

See also:

- [changedInternalState], the equivalent but for changes to the internal state of the route.

### dispose()

```dart
void dispose()
```

Discards any resources used by the object.

This method should not remove its [overlayEntries] from the [Overlay]. The object's owner is in charge of doing that.

After this is called, the object is not in a usable state and should be discarded.

This method should only be called by the object's owner; typically the [Navigator] owns a route and so will call this method when the route is removed, after which the route is no longer referenced by the navigator.

### isCurrent

```dart
bool get isCurrent
```

Whether this route is the top-most route on the navigator.

If this is true, then [isActive] is also true.

### isFirst

```dart
bool get isFirst
```

Whether this route is the bottom-most active route on the navigator.

If [isFirst] and [isCurrent] are both true then this is the only route on the navigator (and [isActive] will also be true).

### hasActiveRouteBelow

```dart
bool get hasActiveRouteBelow
```

Whether there is at least one active route underneath this route.

### isActive

```dart
bool get isActive
```

Whether this route is on the navigator.

If the route is not only active, but also the current route (the top-most route), then [isCurrent] will also be true. If it is the first route (the bottom-most route), then [isFirst] will also be true.

If a higher route is entirely opaque, then the route will be active but not rendered. It is even possible for the route to be active but for the stateful widgets within the route to not be instantiated. See [ModalRoute.maintainState].

# RouteSettings

```dart
class RouteSettings {}
```

Data that might be useful in constructing a [Route].

### RouteSettings()

```dart
RouteSettings({String? name, Object? arguments})
```

Creates data used to construct routes.

### name

```dart
String? name
```

The name of the route (e.g., "/settings").

If null, the route is anonymous.

### arguments

```dart
Object? arguments
```

The arguments passed to this route.

May be used when building the route, e.g. in [Navigator.onGenerateRoute].

### toString()

```dart
String toString()
```

# Page

```dart
abstract class Page<T> extends RouteSettings {}
```

Describes the configuration of a [Route].

The type argument `T` is the corresponding [Route]'s return type, as used by [Route.currentResult], [Route.popped], and [Route.didPop].

The [canPop] and [onPopInvoked] are used for intercepting pops.

{@tool dartpad} This sample demonstrates how to use this [canPop] and [onPopInvoked] to intercept pops.

** See code in examples/api/lib/widgets/page/page_can_pop.0.dart ** {@end-tool}

See also:

- [Navigator.pages], which accepts a list of [Page]s and updates its routes history.

### Page()

```dart
Page({LocalKey? key, String? name, Object? arguments, String? restorationId, bool canPop = true, PopInvokedWithResultCallback<T> onPopInvoked = _defaultPopInvokedHandler})
```

Creates a page and initializes [key] for subclasses.

### key

```dart
LocalKey? key
```

The key associated with this page.

This key will be used for comparing pages in [canUpdate].

### restorationId

```dart
String? restorationId
```

Restoration ID to save and restore the state of the [Route] configured by this page.

If no restoration ID is provided, the [Route] will not restore its state.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### onPopInvoked

```dart
PopInvokedWithResultCallback<T> onPopInvoked
```

Called after a pop on the associated route was handled.

It's not possible to prevent the pop from happening at the time that this method is called; the pop has already happened. Use [canPop] to disable pops in advance.

This will still be called even when the pop is canceled. A pop is canceled when the associated [Route.popDisposition] returns false, or when [canPop] is set to false. The `didPop` parameter indicates whether or not the back navigation actually happened successfully.

### canPop

```dart
bool canPop
```

When false, blocks the associated route from being popped.

If this is set to false for first page in the Navigator. It prevents Flutter app from exiting.

If there are any [PopScope] widgets in a route's widget subtree, each of their `canPop` must be `true`, in addition to this canPop, in order for the route to be able to pop.

### canUpdate()

```dart
bool canUpdate(Page<dynamic> other)
```

Whether this page can be updated with the [other] page.

Two pages are consider updatable if they have same the [runtimeType] and [key].

### createRoute()

```dart
Route<T> createRoute(BuildContext context)
```

Creates the [Route] that corresponds to this page.

The created [Route] must have its [Route.settings] property set to this [Page].

### toString()

```dart
String toString()
```

# NavigatorObserver

```dart
class NavigatorObserver {}
```

An interface for observing the behavior of a [Navigator].

### navigator

```dart
NavigatorState? get navigator
```

The navigator that the observer is observing, if any.

### didPush()

```dart
void didPush(Route<dynamic> route, Route<dynamic>? previousRoute)
```

The [Navigator] pushed `route`.

The route immediately below that one, and thus the previously active route, is `previousRoute`.

### didPop()

```dart
void didPop(Route<dynamic> route, Route<dynamic>? previousRoute)
```

The [Navigator] popped `route`.

The route immediately below that one, and thus the newly active route, is `previousRoute`.

### didRemove()

```dart
void didRemove(Route<dynamic> route, Route<dynamic>? previousRoute)
```

The [Navigator] removed `route`.

If only one route is being removed, then the route immediately below that one, if any, is `previousRoute`.

If multiple routes are being removed, then the route below the bottommost route being removed, if any, is `previousRoute`, and this method will be called once for each removed route, from the topmost route to the bottommost route.

### didReplace()

```dart
void didReplace({Route<dynamic>? newRoute, Route<dynamic>? oldRoute})
```

The [Navigator] replaced `oldRoute` with `newRoute`.

### didChangeTop()

```dart
void didChangeTop(Route<dynamic> topRoute, Route<dynamic>? previousTopRoute)
```

The top most route has changed.

The `topRoute` is the new top most route. This can be a new route pushed on top of the screen, or an existing route that becomes the new top-most route because the previous top-most route has been popped.

The `previousTopRoute` was the top most route before the change. This can be a route that was popped off the screen, or a route that will be covered by the `topRoute`. This can also be null if this is the first build.

### didStartUserGesture()

```dart
void didStartUserGesture(Route<dynamic> route, Route<dynamic>? previousRoute)
```

The [Navigator]'s routes are being moved by a user gesture.

For example, this is called when an iOS back gesture starts, and is used to disable hero animations during such interactions.

### didStopUserGesture()

```dart
void didStopUserGesture()
```

User gesture is no longer controlling the [Navigator].

Paired with an earlier call to [didStartUserGesture].

# HeroControllerScope

```dart
class HeroControllerScope extends InheritedWidget {}
```

An inherited widget to host a hero controller.

The hosted hero controller will be picked up by the navigator in the [child] subtree. Once a navigator picks up this controller, the navigator will bar any navigator below its subtree from receiving this controller.

The hero controller inside the [HeroControllerScope] can only subscribe to one navigator at a time. An assertion will be thrown if the hero controller subscribes to more than one navigators. This can happen when there are multiple navigators under the same [HeroControllerScope] in parallel.

### HeroControllerScope()

```dart
HeroControllerScope({dynamic key, required HeroController? controller, required Widget child})
```

Creates a widget to host the input [controller].

### HeroControllerScope.none()

```dart
HeroControllerScope.none({dynamic key, required Widget child})
```

Creates a widget to prevent the subtree from receiving the hero controller above.

### controller

```dart
HeroController? controller
```

The hero controller that is hosted inside this widget.

### maybeOf()

```dart
HeroController? maybeOf(BuildContext context)
```

Retrieves the [HeroController] from the closest [HeroControllerScope] ancestor, or null if none exists.

Calling this method will create a dependency on the closest [HeroControllerScope] in the [context], if there is one.

See also:

- [HeroControllerScope.of], which is similar to this method, but asserts if no [HeroControllerScope] ancestor is found.

### of()

```dart
HeroController of(BuildContext context)
```

Retrieves the [HeroController] from the closest [HeroControllerScope] ancestor.

If no ancestor is found, this method will assert in debug mode, and throw an exception in release mode.

Calling this method will create a dependency on the closest [HeroControllerScope] in the [context].

See also:

- [HeroControllerScope.maybeOf], which is similar to this method, but returns null if no [HeroControllerScope] ancestor is found.

### updateShouldNotify()

```dart
bool updateShouldNotify(HeroControllerScope oldWidget)
```

# RouteTransitionRecord

```dart
abstract class RouteTransitionRecord {}
```

A [Route] wrapper interface that can be staged for [TransitionDelegate] to decide how its underlying [Route] should transition on or off screen.

### route

```dart
Route<dynamic> get route
```

Retrieves the wrapped [Route].

### isWaitingForEnteringDecision

```dart
bool get isWaitingForEnteringDecision
```

Whether this route is waiting for the decision on how to enter the screen.

If this property is true, this route requires an explicit decision on how to transition into the screen. Such a decision should be made in the [TransitionDelegate.resolve].

### isWaitingForExitingDecision

```dart
bool get isWaitingForExitingDecision
```

Whether this route is waiting for the decision on how to exit the screen.

If this property is true, this route requires an explicit decision on how to transition off the screen. Such a decision should be made in the [TransitionDelegate.resolve].

### markForPush()

```dart
void markForPush()
```

Marks the [route] to be pushed with transition.

During [TransitionDelegate.resolve], this can be called on an entering route (where [RouteTransitionRecord.isWaitingForEnteringDecision] is true) in indicate that the route should be pushed onto the [Navigator] with an animated transition.

### markForAdd()

```dart
void markForAdd()
```

Marks the [route] to be added without transition.

During [TransitionDelegate.resolve], this can be called on an entering route (where [RouteTransitionRecord.isWaitingForEnteringDecision] is true) in indicate that the route should be added onto the [Navigator] without an animated transition.

### markForPop()

```dart
void markForPop([dynamic result])
```

Marks the [route] to be popped with transition.

During [TransitionDelegate.resolve], this can be called on an exiting route to indicate that the route should be popped off the [Navigator] with an animated transition.

### markForComplete()

```dart
void markForComplete([dynamic result])
```

Marks the [route] to be completed without transition.

During [TransitionDelegate.resolve], this can be called on an exiting route to indicate that the route should be completed with the provided result and removed from the [Navigator] without an animated transition.

### markForRemove()

```dart
void markForRemove()
```

Marks the [route] to be removed without transition.

During [TransitionDelegate.resolve], this can be called on an exiting route to indicate that the route should be removed from the [Navigator] without completing and without an animated transition.

# TransitionDelegate

```dart
abstract class TransitionDelegate<T> {}
```

The delegate that decides how pages added and removed from [Navigator.pages] transition in or out of the screen.

This abstract class implements the API to be called by [Navigator] when it requires explicit decisions on how the routes transition on or off the screen.

To make route transition decisions, subclass must implement [resolve].

{@tool snippet} The following example demonstrates how to implement a subclass that always removes or adds routes without animated transitions and puts the removed routes at the top of the list.

```dart
class NoAnimationTransitionDelegate extends TransitionDelegate<void> {
  @override
  Iterable<RouteTransitionRecord> resolve({
    required List<RouteTransitionRecord> newPageRouteHistory,
    required Map<RouteTransitionRecord?, RouteTransitionRecord> locationToExitingPageRoute,
    required Map<RouteTransitionRecord?, List<RouteTransitionRecord>> pageRouteToPagelessRoutes,
  }) {
    final List<RouteTransitionRecord> results = <RouteTransitionRecord>[];

    for (final RouteTransitionRecord pageRoute in newPageRouteHistory) {
      if (pageRoute.isWaitingForEnteringDecision) {
        pageRoute.markForAdd();
      }
      results.add(pageRoute);

    }
    for (final RouteTransitionRecord exitingPageRoute in locationToExitingPageRoute.values) {
      if (exitingPageRoute.isWaitingForExitingDecision) {
       exitingPageRoute.markForComplete();
       final List<RouteTransitionRecord>? pagelessRoutes = pageRouteToPagelessRoutes[exitingPageRoute];
       if (pagelessRoutes != null) {
         for (final RouteTransitionRecord pagelessRoute in pagelessRoutes) {
            pagelessRoute.markForComplete();
          }
       }
      }
      results.add(exitingPageRoute);

    }
    return results;
  }
}

```

{@end-tool}

See also:

- [Navigator.transitionDelegate], which uses this class to make route transition decisions.
- [DefaultTransitionDelegate], which implements the default way to decide how routes transition in or out of the screen.

### TransitionDelegate()

```dart
TransitionDelegate()
```

Creates a delegate and enables subclass to create a constant class.

### resolve()

```dart
Iterable<RouteTransitionRecord> resolve({required List<RouteTransitionRecord> newPageRouteHistory, required Map<RouteTransitionRecord?, RouteTransitionRecord> locationToExitingPageRoute, required Map<RouteTransitionRecord?, List<RouteTransitionRecord>> pageRouteToPagelessRoutes})
```

A method that will be called by the [Navigator] to decide how routes transition in or out of the screen when [Navigator.pages] is updated.

The `newPageRouteHistory` list contains all page-based routes in the order that will be on the [Navigator]'s history stack after this update completes. If a route in `newPageRouteHistory` has its [RouteTransitionRecord.isWaitingForEnteringDecision] set to true, this route requires explicit decision on how it should transition onto the Navigator. To make a decision, call [RouteTransitionRecord.markForPush] or [RouteTransitionRecord.markForAdd].

The `locationToExitingPageRoute` contains the pages-based routes that are removed from the routes history after page update. This map records page-based routes to be removed with the location of the route in the original route history before the update. The keys are the locations represented by the page-based routes that are directly below the removed routes, and the value are the page-based routes to be removed. The location is null if the route to be removed is the bottom most route. If a route in `locationToExitingPageRoute` has its [RouteTransitionRecord.isWaitingForExitingDecision] set to true, this route requires explicit decision on how it should transition off the Navigator. To make a decision for a removed route, call [RouteTransitionRecord.markForPop], [RouteTransitionRecord.markForComplete]. It is possible that decisions are not required for routes in the `locationToExitingPageRoute`. This can happen if the routes have already been popped in earlier page updates and are still waiting for popping animations to finish. In such case, those routes are still included in the `locationToExitingPageRoute` with their [RouteTransitionRecord.isWaitingForExitingDecision] set to false and no decisions are required.

The `pageRouteToPagelessRoutes` records the page-based routes and their associated pageless routes. If a page-based route is waiting for exiting decision, its associated pageless routes also require explicit decisions on how to transition off the screen.

Once all the decisions have been made, this method must merge the removed routes (whether or not they require decisions) and the `newPageRouteHistory` and return the merged result. The order in the result will be the order the [Navigator] uses for updating the route history. The return list must preserve the same order of routes in `newPageRouteHistory`. The removed routes, however, can be inserted into the return list freely as long as all of them are included.

For example, consider the following case.

`newPageRouteHistory = [A, B, C]`

`locationToExitingPageRoute = {A -> D, C -> E}`

The following outputs are valid.

`result = [A, B ,C ,D ,E]` is valid. `result = [D, A, B ,C ,E]` is also valid because exiting route can be inserted in any place.

The following outputs are invalid.

`result = [B, A, C ,D ,E]` is invalid because B must be after A. `result = [A, B, C ,E]` is invalid because results must include D.

See also:

- [RouteTransitionRecord.markForPush], which makes route enter the screen with an animated transition.
- [RouteTransitionRecord.markForAdd], which makes route enter the screen without an animated transition.
- [RouteTransitionRecord.markForPop], which makes route exit the screen with an animated transition.
- [RouteTransitionRecord.markForComplete], which completes the route and makes it exit the screen without an animated transition.
- [DefaultTransitionDelegate.resolve], which implements the default way to decide how routes transition in or out of the screen.

# DefaultTransitionDelegate

```dart
class DefaultTransitionDelegate<T> extends TransitionDelegate<T> {}
```

The default implementation of [TransitionDelegate] that the [Navigator] will use if its [Navigator.transitionDelegate] is not specified.

This transition delegate follows two rules. Firstly, all the entering routes are placed on top of the exiting routes if they are at the same location. Secondly, the top most route will always transition with an animated transition. All the other routes below will either be completed with [Route.currentResult] or added without an animated transition.

### DefaultTransitionDelegate()

```dart
DefaultTransitionDelegate()
```

Creates a default transition delegate.

### resolve()

```dart
Iterable<RouteTransitionRecord> resolve({required List<RouteTransitionRecord> newPageRouteHistory, required Map<RouteTransitionRecord?, RouteTransitionRecord> locationToExitingPageRoute, required Map<RouteTransitionRecord?, List<RouteTransitionRecord>> pageRouteToPagelessRoutes})
```

# kDefaultRouteTraversalEdgeBehavior

```dart
TraversalEdgeBehavior kDefaultRouteTraversalEdgeBehavior
```

The default value of [Navigator.routeTraversalEdgeBehavior].

{@macro flutter.widgets.navigator.routeTraversalEdgeBehavior}

# kDefaultRouteDirectionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior kDefaultRouteDirectionalTraversalEdgeBehavior
```

The default value of [Navigator.routeDirectionalTraversalEdgeBehavior].

{@macro flutter.widgets.navigator.routeTraversalEdgeBehavior}

# Navigator

```dart
class Navigator extends StatefulWidget {}
```

A widget that manages a set of child widgets with a stack discipline.

Many apps have a navigator near the top of their widget hierarchy in order to display their logical history using an [Overlay] with the most recently visited pages visually on top of the older pages. Using this pattern lets the navigator visually transition from one page to another by moving the widgets around in the overlay. Similarly, the navigator can be used to show a dialog by positioning the dialog widget above the current page.

## Using the Pages API

The [Navigator] will convert its [Navigator.pages] into a stack of [Route]s if it is provided. A change in [Navigator.pages] will trigger an update to the stack of [Route]s. The [Navigator] will update its routes to match the new configuration of its [Navigator.pages]. To use this API, one can create a [Page] subclass and defines a list of [Page]s for [Navigator.pages]. A [Navigator.onPopPage] callback is also required to properly clean up the input pages in case of a pop.

By Default, the [Navigator] will use [DefaultTransitionDelegate] to decide how routes transition in or out of the screen. To customize it, define a [TransitionDelegate] subclass and provide it to the [Navigator.transitionDelegate].

For more information on using the pages API, see the [Router] widget.

## Using the Navigator API

Mobile apps typically reveal their contents via full-screen elements called "screens" or "pages". In Flutter these elements are called routes and they're managed by a [Navigator] widget. The navigator manages a stack of [Route] objects and provides two ways for managing the stack, the declarative API [Navigator.pages] or imperative API [Navigator.push] and [Navigator.pop].

When your user interface fits this paradigm of a stack, where the user should be able to _navigate_ back to an earlier element in the stack, the use of routes and the Navigator is appropriate. On certain platforms, such as Android, the system UI will provide a back button (outside the bounds of your application) that will allow the user to navigate back to earlier routes in your application's stack. On platforms that don't have this built-in navigation mechanism, the use of an [AppBar] (typically used in the [Scaffold.appBar] property) can automatically add a back button for user navigation.

### Displaying a full-screen route

Although you can create a navigator directly, it's most common to use the navigator created by the `Router` which itself is created and configured by a [WidgetsApp] or a [MaterialApp] widget. You can refer to that navigator with [Navigator.of].

A [MaterialApp] is the simplest way to set things up. The [MaterialApp]'s home becomes the route at the bottom of the [Navigator]'s stack. It is what you see when the app is launched.

```dart
void main() {
  runApp(const MaterialApp(home: MyAppHome()));
}
```

To push a new route on the stack you can create an instance of [MaterialPageRoute] with a builder function that creates whatever you want to appear on the screen. For example:

```dart
Navigator.push(context, MaterialPageRoute<void>(
  builder: (BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('My Page')),
      body: Center(
        child: TextButton(
          child: const Text('POP'),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  },
));
```

The route defines its widget with a builder function instead of a child widget because it will be built and rebuilt in different contexts depending on when it's pushed and popped.

As you can see, the new route can be popped, revealing the app's home page, with the Navigator's pop method:

```dart
Navigator.pop(context);
```

It usually isn't necessary to provide a widget that pops the Navigator in a route with a [Scaffold] because the Scaffold automatically adds a 'back' button to its AppBar. Pressing the back button causes [Navigator.pop] to be called. On Android, pressing the system back button does the same thing.

### Using named navigator routes

Mobile apps often manage a large number of routes and it's often easiest to refer to them by name. Route names, by convention, use a path-like structure (for example, '/a/b/c'). The app's home page route is named '/' by default.

The [MaterialApp] can be created with a [Map<String, WidgetBuilder>] which maps from a route's name to a builder function that will create it. The [MaterialApp] uses this map to create a value for its navigator's [onGenerateRoute] callback.

```dart
void main() {
  runApp(MaterialApp(
    home: const MyAppHome(), // becomes the route named '/'
    routes: <String, WidgetBuilder> {
      '/a': (BuildContext context) => const MyPage(title: Text('page A')),
      '/b': (BuildContext context) => const MyPage(title: Text('page B')),
      '/c': (BuildContext context) => const MyPage(title: Text('page C')),
    },
  ));
}
```

To show a route by name:

```dart
Navigator.pushNamed(context, '/b');
```

### Routes can return a value

When a route is pushed to ask the user for a value, the value can be returned via the [pop] method's result parameter.

Methods that push a route return a [Future]. The Future resolves when the route is popped and the [Future]'s value is the [pop] method's `result` parameter.

For example if we wanted to ask the user to press 'OK' to confirm an operation we could `await` the result of [Navigator.push]:

```dart
bool? value = await Navigator.push(context, MaterialPageRoute<bool>(
  builder: (BuildContext context) {
    return Center(
      child: GestureDetector(
        child: const Text('OK'),
        onTap: () { Navigator.pop(context, true); }
      ),
    );
  }
));
```

If the user presses 'OK' then value will be true. If the user backs out of the route, for example by pressing the Scaffold's back button, the value will be null.

When a route is used to return a value, the route's type parameter must match the type of [pop]'s result. That's why we've used `MaterialPageRoute<bool>` instead of `MaterialPageRoute<void>` or just `MaterialPageRoute`. (If you prefer to not specify the types, though, that's fine too.)

### Popup routes

Routes don't have to obscure the entire screen. [PopupRoute]s cover the screen with a [ModalRoute.barrierColor] that can be only partially opaque to allow the current screen to show through. Popup routes are "modal" because they block input to the widgets below.

There are functions which create and show popup routes. For example: [showDialog], [showMenu], and [showModalBottomSheet]. These functions return their pushed route's Future as described above. Callers can await the returned value to take an action when the route is popped, or to discover the route's value.

There are also widgets which create popup routes, like [PopupMenuButton] and [DropdownButton]. These widgets create internal subclasses of PopupRoute and use the Navigator's push and pop methods to show and dismiss them.

### Custom routes

You can create your own subclass of one of the widget library route classes like [PopupRoute], [ModalRoute], or [PageRoute], to control the animated transition employed to show the route, the color and behavior of the route's modal barrier, and other aspects of the route.

The [PageRouteBuilder] class makes it possible to define a custom route in terms of callbacks. Here's an example that rotates and fades its child when the route appears or disappears. This route does not obscure the entire screen because it specifies `opaque: false`, just as a popup route does.

```dart
Navigator.push(context, PageRouteBuilder<void>(
  opaque: false,
  pageBuilder: (BuildContext context, _, _) {
    return const Center(child: Text('My PageRoute'));
  },
  transitionsBuilder: (_, Animation<double> animation, _, Widget child) {
    return FadeTransition(
      opacity: animation,
      child: RotationTransition(
        turns: Tween<double>(begin: 0.5, end: 1.0).animate(animation),
        child: child,
      ),
    );
  }
));
```

The page route is built in two parts, the "page" and the "transitions". The page becomes a descendant of the child passed to the `transitionsBuilder` function. Typically the page is only built once, because it doesn't depend on its animation parameters (elided with `_` in this example). The transition is built on every frame for its duration.

(In this example, `void` is used as the return type for the route, because it does not return a value.)

### Nesting Navigators

An app can use more than one [Navigator]. Nesting one [Navigator] below another [Navigator] can be used to create an "inner journey" such as tabbed navigation, user registration, store checkout, or other independent journeys that represent a subsection of your overall application.

#### Example

It is standard practice for iOS apps to use tabbed navigation where each tab maintains its own navigation history. Therefore, each tab has its own [Navigator], creating a kind of "parallel navigation."

In addition to the parallel navigation of the tabs, it is still possible to launch full-screen pages that completely cover the tabs. For example: an on-boarding flow, or an alert dialog. Therefore, there must exist a "root" [Navigator] that sits above the tab navigation. As a result, each of the tab's [Navigator]s are actually nested [Navigator]s sitting below a single root [Navigator].

In practice, the nested [Navigator]s for tabbed navigation sit in the [WidgetsApp] and [CupertinoTabView] widgets and do not need to be explicitly created or managed.

{@tool sample} The following example demonstrates how a nested [Navigator] can be used to present a standalone user registration journey.

Even though this example uses two [Navigator]s to demonstrate nested [Navigator]s, a similar result is possible using only a single [Navigator].

Run this example with `flutter run --route=/signup` to start it with the signup flow instead of on the home page.

** See code in examples/api/lib/widgets/navigator/navigator.0.dart ** {@end-tool}

[Navigator.of] operates on the nearest ancestor [Navigator] from the given [BuildContext]. Be sure to provide a [BuildContext] below the intended [Navigator], especially in large `build` methods where nested [Navigator]s are created. The [Builder] widget can be used to access a [BuildContext] at a desired location in the widget subtree.

### Finding the enclosing route

In the common case of a modal route, the enclosing route can be obtained from inside a build method using [ModalRoute.of]. To determine if the enclosing route is the active route (e.g. so that controls can be dimmed when the route is not active), the [Route.isCurrent] property can be checked on the returned route.

## State Restoration

If provided with a [restorationScopeId] and when surrounded by a valid [RestorationScope] the [Navigator] will restore its state by recreating the current history stack of [Route]s during state restoration and by restoring the internal state of those [Route]s. However, not all [Route]s on the stack can be restored:

- [Page]-based routes restore their state if [Page.restorationId] is provided.
- [Route]s added with the classic imperative API ([push], [pushNamed], and friends) can never restore their state.
- A [Route] added with the restorable imperative API ([restorablePush], [restorablePushNamed], and all other imperative methods with "restorable" in their name) restores its state if all routes below it up to and including the first [Page]-based route below it are restored. If there is no [Page]-based route below it, it only restores its state if all routes below it restore theirs.

If a [Route] is deemed restorable, the [Navigator] will set its [Route.restorationScopeId] to a non-null value. Routes can use that ID to store and restore their own state. As an example, the [ModalRoute] will use this ID to create a [RestorationScope] for its content widgets.

### Navigator()

```dart
Navigator({dynamic key, List<Page<dynamic>> pages = const <Page<dynamic>>[], PopPageCallback? onPopPage, String? initialRoute, RouteListFactory onGenerateInitialRoutes = Navigator.defaultGenerateInitialRoutes, RouteFactory? onGenerateRoute, RouteFactory? onUnknownRoute, TransitionDelegate<dynamic> transitionDelegate = const DefaultTransitionDelegate<dynamic>(), bool reportsRouteUpdateToEngine = false, Clip clipBehavior = Clip.hardEdge, List<NavigatorObserver> observers = const <NavigatorObserver>[], bool requestFocus = true, String? restorationScopeId, TraversalEdgeBehavior routeTraversalEdgeBehavior = kDefaultRouteTraversalEdgeBehavior, TraversalEdgeBehavior routeDirectionalTraversalEdgeBehavior = kDefaultRouteDirectionalTraversalEdgeBehavior, DidRemovePageCallback? onDidRemovePage})
```

Creates a widget that maintains a stack-based history of child widgets.

If the [pages] is not empty, the [onPopPage] must not be null.

### pages

```dart
List<Page<dynamic>> pages
```

The list of pages with which to populate the history.

Pages are turned into routes using [Page.createRoute] in a manner analogous to how [Widget]s are turned into [Element]s (and [State]s or [RenderObject]s) using [Widget.createElement] (and [StatefulWidget.createState] or [RenderObjectWidget.createRenderObject]).

When this list is updated, the new list is compared to the previous list and the set of routes is updated accordingly.

Some [Route]s do not correspond to [Page] objects, namely, those that are added to the history using the [Navigator] API ([push] and friends). A [Route] that does not correspond to a [Page] object is called a pageless route and is tied to the [Route] that _does_ correspond to a [Page] object that is below it in the history.

Pages that are added or removed may be animated as controlled by the [transitionDelegate]. If a page is removed that had other pageless routes pushed on top of it using [push] and friends, those pageless routes are also removed with or without animation as determined by the [transitionDelegate].

To use this API, an [onPopPage] callback must also be provided to properly clean up this list if a page has been popped.

If [initialRoute] is non-null when the widget is first created, then [onGenerateInitialRoutes] is used to generate routes that are above those corresponding to [pages] in the initial history.

### onPopPage

```dart
PopPageCallback? onPopPage
```

This is deprecated and replaced by [onDidRemovePage].

Called when [pop] is invoked but the current [Route] corresponds to a [Page] found in the [pages] list.

The `result` argument is the value with which the route is to complete (e.g. the value returned from a dialog).

This callback is responsible for calling [Route.didPop] and returning whether this pop is successful.

The [Navigator] widget should be rebuilt with a [pages] list that does not contain the [Page] for the given [Route]. The next time the [pages] list is updated, if the [Page] corresponding to this [Route] is still present, it will be interpreted as a new route to display.

### onDidRemovePage

```dart
DidRemovePageCallback? onDidRemovePage
```

Called when the [Route] associated with the given [Page] has been removed from the Navigator.

This can happen when the route is removed or completed through [Navigator.pop], [Navigator.pushReplacement], or its friends.

This callback is responsible for removing the given page from the list of [pages].

The [Navigator] widget should be rebuilt with a [pages] list that does not contain the given page [Page]. The next time the [pages] list is updated, if the given [Page] is still present, it will be interpreted as a new page to display.

### transitionDelegate

```dart
TransitionDelegate<dynamic> transitionDelegate
```

The delegate used for deciding how routes transition in or off the screen during the [pages] updates.

Defaults to [DefaultTransitionDelegate].

### initialRoute

```dart
String? initialRoute
```

The name of the first route to show.

Defaults to [Navigator.defaultRouteName].

The value is interpreted according to [onGenerateInitialRoutes], which defaults to [defaultGenerateInitialRoutes].

Changing the [initialRoute] will have no effect, as it only controls the _initial_ route. To change the route while the application is running, use the static functions on this class, such as [push] or [replace].

### onGenerateRoute

```dart
RouteFactory? onGenerateRoute
```

Called to generate a route for a given [RouteSettings].

### onUnknownRoute

```dart
RouteFactory? onUnknownRoute
```

Called when [onGenerateRoute] fails to generate a route.

This callback is typically used for error handling. For example, this callback might always generate a "not found" page that describes the route that wasn't found.

Unknown routes can arise either from errors in the app or from external requests to push routes, such as from Android intents.

### observers

```dart
List<NavigatorObserver> observers
```

A list of observers for this navigator.

### restorationScopeId

```dart
String? restorationScopeId
```

Restoration ID to save and restore the state of the navigator, including its history.

{@template flutter.widgets.navigator.restorationScopeId} If a restoration ID is provided, the navigator will persist its internal state (including the route history as well as the restorable state of the routes) and restore it during state restoration.

If no restoration ID is provided, the route history stack will not be restored and state restoration is disabled for the individual routes as well.

The state is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID. Within that bucket, the [Navigator] also creates a new [RestorationScope] for its children (the [Route]s).

See also:

- [RestorationManager], which explains how state restoration works in Flutter.
- [RestorationMixin], which contains a runnable code sample showcasing state restoration in Flutter.
- [Navigator], which explains under the heading "state restoration" how and under what conditions the navigator restores its state.
- [Navigator.restorablePush], which includes an example showcasing how to push a restorable route onto the navigator. {@endtemplate}

### routeTraversalEdgeBehavior

```dart
TraversalEdgeBehavior routeTraversalEdgeBehavior
```

Controls the transfer of focus beyond the first and the last items of a focus scope that defines focus traversal of widgets within a route.

{@template flutter.widgets.navigator.routeTraversalEdgeBehavior} The focus inside routes installed in the top of the app affects how the app behaves with respect to the platform content surrounding it. For example, on the web, an app is at a minimum surrounded by browser UI, such as the address bar, browser tabs, and more. The user should be able to reach browser UI using normal focus shortcuts. Similarly, if the app is embedded within an `<iframe>` or inside a custom element, it should be able to participate in the overall focus traversal, including elements not rendered by Flutter. {@endtemplate}

### routeDirectionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior routeDirectionalTraversalEdgeBehavior
```

Controls the directional transfer of focus beyond the first and the last items of a focus scope that defines focus traversal of widgets within a route.

{@macro flutter.widgets.navigator.routeTraversalEdgeBehavior}

### defaultRouteName

```dart
String defaultRouteName
```

The name for the default route of the application.

See also:

- [dart:ui.PlatformDispatcher.defaultRouteName], which reflects the route that the application was started with.

### onGenerateInitialRoutes

```dart
RouteListFactory onGenerateInitialRoutes
```

Called when the widget is created to generate the initial list of [Route] objects if [initialRoute] is not null.

Defaults to [defaultGenerateInitialRoutes].

The [NavigatorState] and [initialRoute] will be passed to the callback. The callback must return a list of [Route] objects with which the history will be primed.

When parsing the initialRoute, if there's any chance that it may contain complex characters, it's best to use the [characters](https://pub.dev/packages/characters) API. This will ensure that extended grapheme clusters and surrogate pairs are treated as single characters by the code, the same way that they appear to the user. For example, the string "👨‍👩‍👦" appears to the user as a single character and `string.characters.length` intuitively returns 1. On the other hand, `string.length` returns 8, and `string.runes.length` returns 5!

### reportsRouteUpdateToEngine

```dart
bool reportsRouteUpdateToEngine
```

Whether this navigator should report route update message back to the engine when the top-most route changes.

If the property is set to true, this navigator automatically sends the route update message to the engine when it detects top-most route changes. The messages are used by the web engine to update the browser URL bar.

If the property is set to true when the [Navigator] is first created, single-entry history mode is requested using [SystemNavigator.selectSingleEntryHistory]. This means this property should not be used at the same time as [PlatformRouteInformationProvider] is used with a [Router] (including when used with [MaterialApp.router], for example).

If there are multiple navigators in the widget tree, at most one of them can set this property to true (typically, the top-most one created from the [WidgetsApp]). Otherwise, the web engine may receive multiple route update messages from different navigators and fail to update the URL bar.

Defaults to false.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

In cases where clipping is not desired, consider setting this property to [Clip.none].

Defaults to [Clip.hardEdge].

### requestFocus

```dart
bool requestFocus
```

Whether or not the navigator and it's new topmost route should request focus when the new route is pushed onto the navigator.

If [Route.requestFocus] is set on the topmost route, that will take precedence over this value.

Defaults to true.

### pushNamed()

```dart
Future<T?> pushNamed<T extends Object?>(BuildContext context, String routeName, {Object? arguments})
```

Push a named route onto the navigator that most tightly encloses the given context.

{@template flutter.widgets.navigator.pushNamed} The route name will be passed to the [Navigator.onGenerateRoute] callback. The returned route will be pushed into the navigator.

The new route and the previous route (if any) are notified (see [Route.didPush] and [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didPush]).

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the route.

To use [pushNamed], an [Navigator.onGenerateRoute] callback must be provided, {@endtemplate}

{@template flutter.widgets.navigator.pushNamed.returnValue} Returns a [Future] that completes to the `result` value passed to [pop] when the pushed route is popped off the navigator. {@endtemplate}

{@template flutter.widgets.Navigator.pushNamed} The provided `arguments` are passed to the pushed route via [RouteSettings.arguments]. Any object can be passed as `arguments` (e.g. a [String], [int], or an instance of a custom `MyRouteArguments` class). Often, a [Map] is used to pass key-value pairs.

The `arguments` may be used in [Navigator.onGenerateRoute] or [Navigator.onUnknownRoute] to construct the route. {@endtemplate}

{@tool snippet}

Typical usage is as follows:

```dart
void _didPushButton() {
  Navigator.pushNamed(context, '/settings');
}
```

{@end-tool}

{@tool snippet}

The following example shows how to pass additional `arguments` to the route:

```dart
void _showBerlinWeather() {
  Navigator.pushNamed(
    context,
    '/weather',
    arguments: <String, String>{
      'city': 'Berlin',
      'country': 'Germany',
    },
  );
}
```

{@end-tool}

{@tool snippet}

The following example shows how to pass a custom Object to the route:

```dart
class WeatherRouteArguments {
  WeatherRouteArguments({ required this.city, required this.country });
  final String city;
  final String country;

  bool get isGermanCapital {
    return country == 'Germany' && city == 'Berlin';
  }
}

void _showWeather() {
  Navigator.pushNamed(
    context,
    '/weather',
    arguments: WeatherRouteArguments(city: 'Berlin', country: 'Germany'),
  );
}
```

{@end-tool}

See also:

- [restorablePushNamed], which pushes a route that can be restored during state restoration.

### restorablePushNamed()

```dart
String restorablePushNamed<T extends Object?>(BuildContext context, String routeName, {Object? arguments})
```

Push a named route onto the navigator that most tightly encloses the given context.

{@template flutter.widgets.navigator.restorablePushNamed} Unlike [Route]s pushed via [pushNamed], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed}

{@template flutter.widgets.Navigator.restorablePushNamed.arguments} The provided `arguments` are passed to the pushed route via [RouteSettings.arguments]. Any object that is serializable via the [StandardMessageCodec] can be passed as `arguments`. Often, a Map is used to pass key-value pairs.

The arguments may be used in [Navigator.onGenerateRoute] or [Navigator.onUnknownRoute] to construct the route. {@endtemplate}

{@template flutter.widgets.Navigator.restorablePushNamed.returnValue} The method returns an opaque ID for the pushed route that can be used by the [RestorableRouteFuture] to gain access to the actual [Route] object added to the navigator and its return value. You can ignore the return value of this method, if you do not care about the route object or the route's return value. {@endtemplate}

{@tool snippet}

Typical usage is as follows:

```dart
void _showParisWeather() {
  Navigator.restorablePushNamed(
    context,
    '/weather',
    arguments: <String, String>{
      'city': 'Paris',
      'country': 'France',
    },
  );
}
```

{@end-tool}

### pushReplacementNamed()

```dart
Future<T?> pushReplacementNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

Replace the current route of the navigator that most tightly encloses the given context by pushing the route named [routeName] and then disposing the previous route once the new route has finished animating in.

{@template flutter.widgets.navigator.pushReplacementNamed} If non-null, `result` will be used as the result of the route that is removed; the future that had been returned from pushing that old route will complete with `result`. Routes such as dialogs or popup menus typically use this mechanism to return the value selected by the user to the widget that created their route. The type of `result`, if provided, must match the type argument of the class of the old route (`TO`).

The route name will be passed to the [Navigator.onGenerateRoute] callback. The returned route will be pushed into the navigator.

The new route and the route below the removed route are notified (see [Route.didPush] and [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didReplace]). The removed route is notified once the new route has finished animating (see [Route.didComplete]). The removed route's exit animation is not run (see [popAndPushNamed] for a variant that animates the removed route).

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the new route, and `TO` is the type of the return value of the old route.

To use [pushReplacementNamed], a [Navigator.onGenerateRoute] callback must be provided. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _switchToBrightness() {
  Navigator.pushReplacementNamed(context, '/settings/brightness');
}
```

{@end-tool}

See also:

- [restorablePushReplacementNamed], which pushes a replacement route that can be restored during state restoration.

### restorablePushReplacementNamed()

```dart
String restorablePushReplacementNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

Replace the current route of the navigator that most tightly encloses the given context by pushing the route named [routeName] and then disposing the previous route once the new route has finished animating in.

{@template flutter.widgets.navigator.restorablePushReplacementNamed} Unlike [Route]s pushed via [pushReplacementNamed], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.pushReplacementNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _switchToAudioVolume() {
  Navigator.restorablePushReplacementNamed(context, '/settings/volume');
}
```

{@end-tool}

### popAndPushNamed()

```dart
Future<T?> popAndPushNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

Pop the current route off the navigator that most tightly encloses the given context and push a named route in its place.

{@template flutter.widgets.navigator.popAndPushNamed} The popping of the previous route is handled as per [pop].

The new route's name will be passed to the [Navigator.onGenerateRoute] callback. The returned route will be pushed into the navigator.

The new route, the old route, and the route below the old route (if any) are all notified (see [Route.didPop], [Route.didComplete], [Route.didPopNext], [Route.didPush], and [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didPop] and [NavigatorObserver.didPush]). The animations for the pop and the push are performed simultaneously, so the route below may be briefly visible even if both the old route and the new route are opaque (see [TransitionRoute.opaque]).

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the new route, and `TO` is the return value type of the old route.

To use [popAndPushNamed], a [Navigator.onGenerateRoute] callback must be provided. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _selectAccessibility() {
  Navigator.popAndPushNamed(context, '/settings/accessibility');
}
```

{@end-tool}

See also:

- [restorablePopAndPushNamed], which pushes a new route that can be restored during state restoration.

### restorablePopAndPushNamed()

```dart
String restorablePopAndPushNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

Pop the current route off the navigator that most tightly encloses the given context and push a named route in its place.

{@template flutter.widgets.navigator.restorablePopAndPushNamed} Unlike [Route]s pushed via [popAndPushNamed], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.popAndPushNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _selectNetwork() {
  Navigator.restorablePopAndPushNamed(context, '/settings/network');
}
```

{@end-tool}

### pushNamedAndRemoveUntil()

```dart
Future<T?> pushNamedAndRemoveUntil<T extends Object?>(BuildContext context, String newRouteName, RoutePredicate predicate, {Object? arguments})
```

Push the route with the given name onto the navigator that most tightly encloses the given context, and then remove all the previous routes until the `predicate` returns true.

{@template flutter.widgets.navigator.pushNamedAndRemoveUntil} The predicate may be applied to the same route more than once if [Route.willHandlePopInternally] is true.

To remove routes until a route with a certain name, use the [RoutePredicate] returned from [ModalRoute.withName].

To remove all the routes below the pushed route, use a [RoutePredicate] that always returns false (e.g. `(Route<dynamic> route) => false`).

The removed routes are removed without being completed, so this method does not take a return value argument.

The new route's name (`routeName`) will be passed to the [Navigator.onGenerateRoute] callback. The returned route will be pushed into the navigator.

The new route and the route below the bottommost removed route (which becomes the route below the new route) are notified (see [Route.didPush] and [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didPush] and [NavigatorObserver.didRemove]). The removed routes are disposed, once the new route has finished animating, and the futures that had been returned from pushing those routes will complete.

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the new route.

To use [pushNamedAndRemoveUntil], an [Navigator.onGenerateRoute] callback must be provided. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _resetToCalendar() {
  Navigator.pushNamedAndRemoveUntil(context, '/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

See also:

- [restorablePushNamedAndRemoveUntil], which pushes a new route that can be restored during state restoration.

### restorablePushNamedAndRemoveUntil()

```dart
String restorablePushNamedAndRemoveUntil<T extends Object?>(BuildContext context, String newRouteName, RoutePredicate predicate, {Object? arguments})
```

Push the route with the given name onto the navigator that most tightly encloses the given context, and then remove all the previous routes until the `predicate` returns true.

{@template flutter.widgets.navigator.restorablePushNamedAndRemoveUntil} Unlike [Route]s pushed via [pushNamedAndRemoveUntil], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamedAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _resetToOverview() {
  Navigator.restorablePushNamedAndRemoveUntil(context, '/overview', ModalRoute.withName('/'));
}
```

{@end-tool}

### push()

```dart
Future<T?> push<T extends Object?>(BuildContext context, Route<T> route)
```

Push the given route onto the navigator that most tightly encloses the given context.

{@template flutter.widgets.navigator.push} The new route and the previous route (if any) are notified (see [Route.didPush] and [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didPush]).

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the route. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _openMyPage() {
  Navigator.push<void>(
    context,
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyPage(),
    ),
  );
}
```

{@end-tool}

See also:

- [restorablePush], which pushes a route that can be restored during state restoration.

### restorablePush()

```dart
String restorablePush<T extends Object?>(BuildContext context, RestorableRouteBuilder<T> routeBuilder, {Object? arguments})
```

Push a new route onto the navigator that most tightly encloses the given context.

{@template flutter.widgets.navigator.restorablePush} Unlike [Route]s pushed via [push], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.push}

{@template flutter.widgets.Navigator.restorablePush} The method takes a [RestorableRouteBuilder] as argument, which must be a _static_ function annotated with `@pragma('vm:entry-point')`. It must instantiate and return a new [Route] object that will be added to the navigator. The provided `arguments` object is passed to the `routeBuilder`. The navigator calls the static `routeBuilder` function again during state restoration to re-create the route object.

Any object that is serializable via the [StandardMessageCodec] can be passed as `arguments`. Often, a Map is used to pass key-value pairs. {@endtemplate}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} Typical usage is as follows:

** See code in examples/api/lib/widgets/navigator/navigator.restorable_push.0.dart ** {@end-tool}

### pushReplacement()

```dart
Future<T?> pushReplacement<T extends Object?, TO extends Object?>(BuildContext context, Route<T> newRoute, {TO? result})
```

Replace the current route of the navigator that most tightly encloses the given context by pushing the given route and then disposing the previous route once the new route has finished animating in.

{@template flutter.widgets.navigator.pushReplacement} If non-null, `result` will be used as the result of the route that is removed; the future that had been returned from pushing that old route will complete with `result`. Routes such as dialogs or popup menus typically use this mechanism to return the value selected by the user to the widget that created their route. The type of `result`, if provided, must match the type argument of the class of the old route (`TO`).

The new route and the route below the removed route are notified (see [Route.didPush] and [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didReplace]). The removed route is notified once the new route has finished animating (see [Route.didComplete]).

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the new route, and `TO` is the type of the return value of the old route. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _completeLogin() {
  Navigator.pushReplacement<void, void>(
    context,
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyHomePage(),
    ),
  );
}
```

{@end-tool}

See also:

- [restorablePushReplacement], which pushes a replacement route that can be restored during state restoration.

### restorablePushReplacement()

```dart
String restorablePushReplacement<T extends Object?, TO extends Object?>(BuildContext context, RestorableRouteBuilder<T> routeBuilder, {TO? result, Object? arguments})
```

Replace the current route of the navigator that most tightly encloses the given context by pushing a new route and then disposing the previous route once the new route has finished animating in.

{@template flutter.widgets.navigator.restorablePushReplacement} Unlike [Route]s pushed via [pushReplacement], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.pushReplacement}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} Typical usage is as follows:

** See code in examples/api/lib/widgets/navigator/navigator.restorable_push_replacement.0.dart ** {@end-tool}

### pushAndRemoveUntil()

```dart
Future<T?> pushAndRemoveUntil<T extends Object?>(BuildContext context, Route<T> newRoute, RoutePredicate predicate)
```

Push the given route onto the navigator that most tightly encloses the given context, and then remove all the previous routes until the `predicate` returns true.

{@template flutter.widgets.navigator.pushAndRemoveUntil} The predicate may be applied to the same route more than once if [Route.willHandlePopInternally] is true.

To remove routes until a route with a certain name, use the [RoutePredicate] returned from [ModalRoute.withName].

To remove all the routes below the pushed route, use a [RoutePredicate] that always returns false (e.g. `(Route<dynamic> route) => false`).

The removed routes are removed without being completed, so this method does not take a return value argument.

The newly pushed route and its preceding route are notified for [Route.didPush]. After removal, the new route and its new preceding route, (the route below the bottommost removed route) are notified through [Route.didChangeNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didPush] and [NavigatorObserver.didRemove]). The removed routes are disposed of and notified, once the new route has finished animating. The futures that had been returned from pushing those routes will complete.

Ongoing gestures within the current route are canceled when a new route is pushed.

The `T` type argument is the type of the return value of the new route. {@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _finishAccountCreation() {
  Navigator.pushAndRemoveUntil<void>(
    context,
    MaterialPageRoute<void>(builder: (BuildContext context) => const MyHomePage()),
    ModalRoute.withName('/'),
  );
}
```

{@end-tool}

See also:

- [restorablePushAndRemoveUntil], which pushes a route that can be restored during state restoration.

### restorablePushAndRemoveUntil()

```dart
String restorablePushAndRemoveUntil<T extends Object?>(BuildContext context, RestorableRouteBuilder<T> newRouteBuilder, RoutePredicate predicate, {Object? arguments})
```

Push a new route onto the navigator that most tightly encloses the given context, and then remove all the previous routes until the `predicate` returns true.

{@template flutter.widgets.navigator.restorablePushAndRemoveUntil} Unlike [Route]s pushed via [pushAndRemoveUntil], [Route]s pushed with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.pushAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} Typical usage is as follows:

** See code in examples/api/lib/widgets/navigator/navigator.restorable_push_and_remove_until.0.dart ** {@end-tool}

### replace()

```dart
void replace<T extends Object?>(BuildContext context, {required Route<dynamic> oldRoute, required Route<T> newRoute})
```

Replaces a route on the navigator that most tightly encloses the given context with a new route.

{@template flutter.widgets.navigator.replace} The old route must not be currently visible, as this method skips the animations and therefore the removal would be jarring if it was visible. To replace the top-most route, consider [pushReplacement] instead, which _does_ animate the new route, and delays removing the old route until the new route has finished animating.

The removed route is removed and completed with a `null` value.

The new route, the route below the new route (if any), and the route above the new route, are all notified (see [Route.didReplace], [Route.didChangeNext], and [Route.didChangePrevious]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didReplace]). The removed route is disposed with its future completed.

This can be useful in combination with [removeRouteBelow] when building a non-linear user experience.

The `T` type argument is the type of the return value of the new route. {@endtemplate}

See also:

- [replaceRouteBelow], which is the same but identifies the route to be removed by reference to the route above it, rather than directly.
- [restorableReplace], which adds a replacement route that can be restored during state restoration.

### restorableReplace()

```dart
String restorableReplace<T extends Object?>(BuildContext context, {required Route<dynamic> oldRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

Replaces a route on the navigator that most tightly encloses the given context with a new route.

{@template flutter.widgets.navigator.restorableReplace} Unlike [Route]s added via [replace], [Route]s added with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.replace}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### replaceRouteBelow()

```dart
void replaceRouteBelow<T extends Object?>(BuildContext context, {required Route<dynamic> anchorRoute, required Route<T> newRoute})
```

Replaces a route on the navigator that most tightly encloses the given context with a new route. The route to be replaced is the one below the given `anchorRoute`.

{@template flutter.widgets.navigator.replaceRouteBelow} The old route must not be current visible, as this method skips the animations and therefore the removal would be jarring if it was visible. To replace the top-most route, consider [pushReplacement] instead, which _does_ animate the new route, and delays removing the old route until the new route has finished animating.

The removed route is removed and completed with a `null` value.

The new route, the route below the new route (if any), and the route above the new route, are all notified (see [Route.didReplace], [Route.didChangeNext], and [Route.didChangePrevious]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didReplace]). The removed route is disposed with its future completed.

The `T` type argument is the type of the return value of the new route. {@endtemplate}

See also:

- [replace], which is the same but identifies the route to be removed directly.
- [restorableReplaceRouteBelow], which adds a replacement route that can be restored during state restoration.

### restorableReplaceRouteBelow()

```dart
String restorableReplaceRouteBelow<T extends Object?>(BuildContext context, {required Route<dynamic> anchorRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

Replaces a route on the navigator that most tightly encloses the given context with a new route. The route to be replaced is the one below the given `anchorRoute`.

{@template flutter.widgets.navigator.restorableReplaceRouteBelow} Unlike [Route]s added via [restorableReplaceRouteBelow], [Route]s added with this method are restored during state restoration according to the rules outlined in the "State Restoration" section of [Navigator]. {@endtemplate}

{@macro flutter.widgets.navigator.replaceRouteBelow}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### canPop()

```dart
bool canPop(BuildContext context)
```

Whether the navigator that most tightly encloses the given context can be popped.

{@template flutter.widgets.navigator.canPop} The initial route cannot be popped off the navigator, which implies that this function returns true only if popping the navigator would not remove the initial route.

If there is no [Navigator] in scope, returns false.

Does not consider anything that might externally prevent popping, such as [PopEntry]. {@endtemplate}

See also:

- [Route.isFirst], which returns true for routes for which [canPop] returns false.

### maybePop()

```dart
Future<bool> maybePop<T extends Object?>(BuildContext context, [T? result])
```

Consults the current route's [Route.popDisposition] getter or [Route.willPop] method, and acts accordingly, potentially popping the route as a result; returns whether the pop request should be considered handled.

{@template flutter.widgets.navigator.maybePop} If the [RoutePopDisposition] is [RoutePopDisposition.pop], then the [pop] method is called, and this method returns true, indicating that it handled the pop request.

If the [RoutePopDisposition] is [RoutePopDisposition.doNotPop], then this method returns true, but does not do anything beyond that.

If the [RoutePopDisposition] is [RoutePopDisposition.bubble], then this method returns false, and the caller is responsible for sending the request to the containing scope (e.g. by closing the application).

This method is typically called for a user-initiated [pop]. For example on Android it's called by the binding for the system's back button.

The `T` type argument is the type of the return value of the current route. (Typically this isn't known; consider specifying `dynamic` or `Null`.) {@endtemplate}

See also:

- [Form], which provides an `onWillPop` callback that enables the form to veto a [pop] initiated by the app's back button.
- [ModalRoute], which provides a `scopedWillPopCallback` that can be used to define the route's `willPop` method.

### pop()

```dart
void pop<T extends Object?>(BuildContext context, [T? result])
```

Pop the top-most route off the navigator that most tightly encloses the given context.

{@template flutter.widgets.navigator.pop} The current route's [Route.didPop] method is called first. If that method returns false, then the route remains in the [Navigator]'s history (the route is expected to have popped some internal state; see e.g. [LocalHistoryRoute]). Otherwise, the rest of this description applies.

If non-null, `result` will be used as the result of the route that is popped; the future that had been returned from pushing the popped route will complete with `result`. Routes such as dialogs or popup menus typically use this mechanism to return the value selected by the user to the widget that created their route. The type of `result`, if provided, must match the type argument of the class of the popped route (`T`).

The popped route and the route below it are notified (see [Route.didPop], [Route.didComplete], and [Route.didPopNext]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didPop]).

The `T` type argument is the type of the return value of the popped route.

The type of `result`, if provided, must match the type argument of the class of the popped route (`T`). {@endtemplate}

{@tool snippet}

Typical usage for closing a route is as follows:

```dart
void _close() {
  Navigator.pop(context);
}
```

{@end-tool}

A dialog box might be closed with a result:

```dart
void _accept() {
  Navigator.pop(context, true); // dialog returns true
}
```

### popUntil()

```dart
void popUntil(BuildContext context, RoutePredicate predicate)
```

Calls [pop] repeatedly on the navigator that most tightly encloses the given context until the predicate returns true.

{@template flutter.widgets.navigator.popUntil} The predicate may be applied to the same route more than once if [Route.willHandlePopInternally] is true.

To pop until a route with a certain name, use the [RoutePredicate] returned from [ModalRoute.withName].

The routes are closed with null as their `return` value.

See [pop] for more details of the semantics of popping a route. {@endtemplate}

{@tool snippet}

Typical usage is as follows:

```dart
void _logout() {
  Navigator.popUntil(context, ModalRoute.withName('/login'));
}
```

{@end-tool}

### popUntilWithResult()

```dart
void popUntilWithResult<T extends Object?>(BuildContext context, RoutePredicate predicate, T? result)
```

Calls [pop] repeatedly on the navigator that most tightly encloses the given context until the predicate returns true, returning the [result] to the last popped route.

The `T` type argument is the type of the return value of the last popped route.

{@macro flutter.widgets.navigator.popUntil}

### removeRoute()

```dart
void removeRoute<T extends Object?>(BuildContext context, Route<T> route, [T? result])
```

Immediately remove `route` from the navigator that most tightly encloses the given context, and [Route.dispose] it.

{@template flutter.widgets.navigator.removeRoute} No animations are run as a result of this method call.

The routes below and above the removed route are notified (see [Route.didChangeNext] and [Route.didChangePrevious]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didRemove]). The removed route is disposed with its future completed.

The given `route` must be in the history; this method will throw an exception if it is not.

If non-null, `result` will be used as the result of the route that is removed; the future that had been returned from pushing the removed route will complete with `result`. If provided, must match the type argument of the class of the popped route (`T`).

The `T` type argument is the type of the return value of the popped route.

The type of `result`, if provided, must match the type argument of the class of the removed route (`T`).

Ongoing gestures within the current route are canceled. {@endtemplate}

This method is used, for example, to instantly dismiss dropdown menus that are up when the screen's orientation changes.

### removeRouteBelow()

```dart
void removeRouteBelow<T extends Object?>(BuildContext context, Route<T> anchorRoute, [T? result])
```

Immediately remove a route from the navigator that most tightly encloses the given context, and [Route.dispose] it. The route to be removed is the one below the given `anchorRoute`.

{@template flutter.widgets.navigator.removeRouteBelow} No animations are run as a result of this method call.

The routes below and above the removed route are notified (see [Route.didChangeNext] and [Route.didChangePrevious]). If the [Navigator] has any [Navigator.observers], they will be notified as well (see [NavigatorObserver.didRemove]). The removed route is disposed with its future completed.

The given `anchorRoute` must be in the history and must have a route below it; this method will throw an exception if it is not or does not.

If non-null, `result` will be used as the result of the route that is removed; the future that had been returned from pushing the removed route will complete with `result`. If provided, must match the type argument of the class of the popped route (`T`).

The `T` type argument is the type of the return value of the popped route.

The type of `result`, if provided, must match the type argument of the class of the removed route (`T`).

Ongoing gestures within the current route are canceled. {@endtemplate}

### of()

```dart
NavigatorState of(BuildContext context, {bool rootNavigator = false})
```

The state from the closest instance of this class that encloses the given context.

Typical usage is as follows:

```dart
Navigator.of(context)
  ..pop()
  ..pop()
  ..pushNamed('/settings');
```

If `rootNavigator` is set to true, the state from the furthest instance of this class is given instead. Useful for pushing contents above all subsequent instances of [Navigator].

If there is no [Navigator] in the given `context`, this function will throw a [FlutterError] in debug mode, and an exception in release mode.

This method can be expensive (it walks the element tree).

### maybeOf()

```dart
NavigatorState? maybeOf(BuildContext context, {bool rootNavigator = false})
```

The state from the closest instance of this class that encloses the given context, if any.

Typical usage is as follows:

```dart
NavigatorState? navigatorState = Navigator.maybeOf(context);
if (navigatorState != null) {
  navigatorState
    ..pop()
    ..pop()
    ..pushNamed('/settings');
}
```

If `rootNavigator` is set to true, the state from the furthest instance of this class is given instead. Useful for pushing contents above all subsequent instances of [Navigator].

Will return null if there is no ancestor [Navigator] in the `context`.

This method can be expensive (it walks the element tree).

### defaultGenerateInitialRoutes()

```dart
List<Route<dynamic>> defaultGenerateInitialRoutes(NavigatorState navigator, String initialRouteName)
```

Turn a route name into a set of [Route] objects.

This is the default value of [onGenerateInitialRoutes], which is used if [initialRoute] is not null.

If this string starts with a `/` character and has multiple `/` characters in it, then the string is split on those characters and substrings from the start of the string up to each such character are, in turn, used as routes to push.

For example, if the route `/stocks/HOOLI` was used as the [initialRoute], then the [Navigator] would push the following routes on startup: `/`, `/stocks`, `/stocks/HOOLI`. This enables deep linking while allowing the application to maintain a predictable route history.

### createState()

```dart
NavigatorState createState()
```

# NavigatorState

```dart
class NavigatorState extends State<Navigator> with TickerProviderStateMixin, RestorationMixin {}
```

The state for a [Navigator] widget.

A reference to this class can be obtained by calling [Navigator.of].

### focusNode

```dart
FocusNode focusNode
```

The [FocusNode] for the [Focus] that encloses the routes.

### initState()

```dart
void initState()
```

### restoreState()

```dart
void restoreState(RestorationBucket? oldBucket, bool initialRestore)
```

### didToggleBucket()

```dart
void didToggleBucket(RestorationBucket? oldBucket)
```

### restorationId

```dart
String? get restorationId
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(Navigator oldWidget)
```

### deactivate()

```dart
void deactivate()
```

### activate()

```dart
void activate()
```

### dispose()

```dart
void dispose()
```

### overlay

```dart
OverlayState? get overlay
```

The overlay this navigator uses for its visual presentation.

### pushNamed()

```dart
Future<T?> pushNamed<T extends Object?>(String routeName, {Object? arguments})
```

Push a named route onto the navigator.

{@macro flutter.widgets.navigator.pushNamed}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _aaronBurrSir() {
  navigator.pushNamed('/nyc/1776');
}
```

{@end-tool}

See also:

- [restorablePushNamed], which pushes a route that can be restored during state restoration.

### restorablePushNamed()

```dart
String restorablePushNamed<T extends Object?>(String routeName, {Object? arguments})
```

Push a named route onto the navigator.

{@macro flutter.widgets.navigator.restorablePushNamed}

{@macro flutter.widgets.navigator.pushNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _openDetails() {
  navigator.restorablePushNamed('/nyc/1776');
}
```

{@end-tool}

### pushReplacementNamed()

```dart
Future<T?> pushReplacementNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

Replace the current route of the navigator by pushing the route named [routeName] and then disposing the previous route once the new route has finished animating in.

{@macro flutter.widgets.navigator.pushReplacementNamed}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _startBike() {
  navigator.pushReplacementNamed('/jouett/1781');
}
```

{@end-tool}

See also:

- [restorablePushReplacementNamed], which pushes a replacement route that can be restored during state restoration.

### restorablePushReplacementNamed()

```dart
String restorablePushReplacementNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

Replace the current route of the navigator by pushing the route named [routeName] and then disposing the previous route once the new route has finished animating in.

{@macro flutter.widgets.navigator.restorablePushReplacementNamed}

{@macro flutter.widgets.navigator.pushReplacementNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _startCar() {
  navigator.restorablePushReplacementNamed('/jouett/1781');
}
```

{@end-tool}

### popAndPushNamed()

```dart
Future<T?> popAndPushNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

Pop the current route off the navigator and push a named route in its place.

{@macro flutter.widgets.navigator.popAndPushNamed}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _begin() {
  navigator.popAndPushNamed('/nyc/1776');
}
```

{@end-tool}

See also:

- [restorablePopAndPushNamed], which pushes a new route that can be restored during state restoration.

### restorablePopAndPushNamed()

```dart
String restorablePopAndPushNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

Pop the current route off the navigator and push a named route in its place.

{@macro flutter.widgets.navigator.restorablePopAndPushNamed}

{@macro flutter.widgets.navigator.popAndPushNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _end() {
  navigator.restorablePopAndPushNamed('/nyc/1776');
}
```

{@end-tool}

### pushNamedAndRemoveUntil()

```dart
Future<T?> pushNamedAndRemoveUntil<T extends Object?>(String newRouteName, RoutePredicate predicate, {Object? arguments})
```

Push the route with the given name onto the navigator, and then remove all the previous routes until the `predicate` returns true.

{@macro flutter.widgets.navigator.pushNamedAndRemoveUntil}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

Typical usage is as follows:

```dart
void _handleOpenCalendar() {
  navigator.pushNamedAndRemoveUntil('/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

See also:

- [restorablePushNamedAndRemoveUntil], which pushes a new route that can be restored during state restoration.

### restorablePushNamedAndRemoveUntil()

```dart
String restorablePushNamedAndRemoveUntil<T extends Object?>(String newRouteName, RoutePredicate predicate, {Object? arguments})
```

Push the route with the given name onto the navigator, and then remove all the previous routes until the `predicate` returns true.

{@macro flutter.widgets.navigator.restorablePushNamedAndRemoveUntil}

{@macro flutter.widgets.navigator.pushNamedAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _openCalendar() {
  navigator.restorablePushNamedAndRemoveUntil('/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

### push()

```dart
Future<T?> push<T extends Object?>(Route<T> route)
```

Push the given route onto the navigator.

{@macro flutter.widgets.navigator.push}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _openPage() {
  navigator.push<void>(
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyPage(),
    ),
  );
}
```

{@end-tool}

See also:

- [restorablePush], which pushes a route that can be restored during state restoration.

### restorablePush()

```dart
String restorablePush<T extends Object?>(RestorableRouteBuilder<T> routeBuilder, {Object? arguments})
```

Push a new route onto the navigator.

{@macro flutter.widgets.navigator.restorablePush}

{@macro flutter.widgets.navigator.push}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} Typical usage is as follows:

** See code in examples/api/lib/widgets/navigator/navigator_state.restorable_push.0.dart ** {@end-tool}

### pushReplacement()

```dart
Future<T?> pushReplacement<T extends Object?, TO extends Object?>(Route<T> newRoute, {TO? result})
```

Replace the current route of the navigator by pushing the given route and then disposing the previous route once the new route has finished animating in.

{@macro flutter.widgets.navigator.pushReplacement}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _doOpenPage() {
  navigator.pushReplacement<void, void>(
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyHomePage(),
    ),
  );
}
```

{@end-tool}

See also:

- [restorablePushReplacement], which pushes a replacement route that can be restored during state restoration.

### restorablePushReplacement()

```dart
String restorablePushReplacement<T extends Object?, TO extends Object?>(RestorableRouteBuilder<T> routeBuilder, {TO? result, Object? arguments})
```

Replace the current route of the navigator by pushing a new route and then disposing the previous route once the new route has finished animating in.

{@macro flutter.widgets.navigator.restorablePushReplacement}

{@macro flutter.widgets.navigator.pushReplacement}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} Typical usage is as follows:

** See code in examples/api/lib/widgets/navigator/navigator_state.restorable_push_replacement.0.dart ** {@end-tool}

### pushAndRemoveUntil()

```dart
Future<T?> pushAndRemoveUntil<T extends Object?>(Route<T> newRoute, RoutePredicate predicate)
```

Push the given route onto the navigator, and then remove all the previous routes until the `predicate` returns true.

{@macro flutter.widgets.navigator.pushAndRemoveUntil}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

Typical usage is as follows:

```dart
void _resetAndOpenPage() {
  navigator.pushAndRemoveUntil<void>(
    MaterialPageRoute<void>(builder: (BuildContext context) => const MyHomePage()),
    ModalRoute.withName('/'),
  );
}
```

{@end-tool}

See also:

- [restorablePushAndRemoveUntil], which pushes a route that can be restored during state restoration.

### restorablePushAndRemoveUntil()

```dart
String restorablePushAndRemoveUntil<T extends Object?>(RestorableRouteBuilder<T> newRouteBuilder, RoutePredicate predicate, {Object? arguments})
```

Push a new route onto the navigator, and then remove all the previous routes until the `predicate` returns true.

{@macro flutter.widgets.navigator.restorablePushAndRemoveUntil}

{@macro flutter.widgets.navigator.pushAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} Typical usage is as follows:

** See code in examples/api/lib/widgets/navigator/navigator_state.restorable_push_and_remove_until.0.dart ** {@end-tool}

### replace()

```dart
void replace<T extends Object?>({required Route<dynamic> oldRoute, required Route<T> newRoute})
```

Replaces a route on the navigator with a new route.

{@macro flutter.widgets.navigator.replace}

See also:

- [replaceRouteBelow], which is the same but identifies the route to be removed by reference to the route above it, rather than directly.
- [restorableReplace], which adds a replacement route that can be restored during state restoration.

### restorableReplace()

```dart
String restorableReplace<T extends Object?>({required Route<dynamic> oldRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

Replaces a route on the navigator with a new route.

{@macro flutter.widgets.navigator.restorableReplace}

{@macro flutter.widgets.navigator.replace}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### replaceRouteBelow()

```dart
void replaceRouteBelow<T extends Object?>({required Route<dynamic> anchorRoute, required Route<T> newRoute})
```

Replaces a route on the navigator with a new route. The route to be replaced is the one below the given `anchorRoute`.

{@macro flutter.widgets.navigator.replaceRouteBelow}

See also:

- [replace], which is the same but identifies the route to be removed directly.
- [restorableReplaceRouteBelow], which adds a replacement route that can be restored during state restoration.

### restorableReplaceRouteBelow()

```dart
String restorableReplaceRouteBelow<T extends Object?>({required Route<dynamic> anchorRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

Replaces a route on the navigator with a new route. The route to be replaced is the one below the given `anchorRoute`.

{@macro flutter.widgets.navigator.restorableReplaceRouteBelow}

{@macro flutter.widgets.navigator.replaceRouteBelow}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### canPop()

```dart
bool canPop()
```

Whether the navigator can be popped.

{@macro flutter.widgets.navigator.canPop}

See also:

- [Route.isFirst], which returns true for routes for which [canPop] returns false.

### maybePop()

```dart
Future<bool> maybePop<T extends Object?>([T? result])
```

Consults the current route's [Route.popDisposition] method, and acts accordingly, potentially popping the route as a result; returns whether the pop request should be considered handled.

{@macro flutter.widgets.navigator.maybePop}

See also:

- [Form], which provides a [Form.canPop] boolean that enables the form to prevent any [pop]s initiated by the app's back button.
- [ModalRoute], which provides a `scopedOnPopCallback` that can be used to define the route's `willPop` method.

### pop()

```dart
void pop<T extends Object?>([T? result])
```

Pop the top-most route off the navigator.

{@macro flutter.widgets.navigator.pop}

{@tool snippet}

Typical usage for closing a route is as follows:

```dart
void _handleClose() {
  navigator.pop();
}
```

{@end-tool} {@tool snippet}

A dialog box might be closed with a result:

```dart
void _handleAccept() {
  navigator.pop(true); // dialog returns true
}
```

{@end-tool}

### popUntil()

```dart
void popUntil(RoutePredicate predicate)
```

Calls [pop] repeatedly until the predicate returns true.

{@macro flutter.widgets.navigator.popUntil}

{@tool snippet}

Typical usage is as follows:

```dart
void _doLogout() {
  navigator.popUntil(ModalRoute.withName('/login'));
}
```

{@end-tool}

### popUntilWithResult()

```dart
void popUntilWithResult<T extends Object?>(RoutePredicate predicate, T? result)
```

Calls [pop] repeatedly until the predicate returns true, returning the [result] to the last popped route.

{@macro flutter.widgets.navigator.popUntil}

### removeRoute()

```dart
void removeRoute<T extends Object?>(Route<T> route, [T? result])
```

Immediately remove `route` from the navigator, and [Route.dispose] it.

{@macro flutter.widgets.navigator.removeRoute}

### removeRouteBelow()

```dart
void removeRouteBelow<T extends Object?>(Route<T> anchorRoute, [T? result])
```

Immediately remove a route from the navigator, and [Route.dispose] it. The route to be removed is the one below the given `anchorRoute`.

{@macro flutter.widgets.navigator.removeRouteBelow}

### finalizeRoute()

```dart
void finalizeRoute(Route<dynamic> route)
```

Complete the lifecycle for a route that has been popped off the navigator.

When the navigator pops a route, the navigator retains a reference to the route in order to call [Route.dispose] if the navigator itself is removed from the tree. When the route is finished with any exit animation, the route should call this function to complete its lifecycle (e.g., to receive a call to [Route.dispose]).

The given `route` must have already received a call to [Route.didPop]. This function may be called directly from [Route.didPop] if [Route.didPop] will return true.

### userGestureInProgress

```dart
bool get userGestureInProgress
```

Whether a route is currently being manipulated by the user, e.g. as during an iOS back gesture.

See also:

- [userGestureInProgressNotifier], which notifies its listeners if the value of [userGestureInProgress] changes.

### userGestureInProgressNotifier

```dart
ValueNotifier<bool> userGestureInProgressNotifier
```

Notifies its listeners if the value of [userGestureInProgress] changes.

### didStartUserGesture()

```dart
void didStartUserGesture()
```

The navigator is being controlled by a user gesture.

For example, called when the user beings an iOS back gesture.

When the gesture finishes, call [didStopUserGesture].

### didStopUserGesture()

```dart
void didStopUserGesture()
```

A user gesture completed.

Notifies the navigator that a gesture regarding which the navigator was previously notified with [didStartUserGesture] has completed.

### build()

```dart
Widget build(BuildContext context)
```

# NavigatorFinderCallback

```dart
typedef NavigatorFinderCallback = NavigatorState Function(BuildContext context)
```

A callback that given a [BuildContext] finds a [NavigatorState].

Used by [RestorableRouteFuture.navigatorFinder] to determine the navigator to which a new route should be added.

# RoutePresentationCallback

```dart
typedef RoutePresentationCallback = String Function(NavigatorState navigator, Object? arguments)
```

A callback that given some `arguments` and a `navigator` adds a new restorable route to that `navigator` and returns the opaque ID of that new route.

Usually, this callback calls one of the imperative methods on the Navigator that have "restorable" in the name and returns their return value.

Used by [RestorableRouteFuture.onPresent].

# RouteCompletionCallback

```dart
typedef RouteCompletionCallback<T> = void Function(T result)
```

A callback to handle the result of a completed [Route].

The return value of the route (which can be null for e.g. void routes) is passed to the callback.

Used by [RestorableRouteFuture.onComplete].

# RestorableRouteFuture

```dart
class RestorableRouteFuture<T> extends RestorableProperty<String?> {}
```

Gives access to a [Route] object and its return value that was added to a navigator via one of its "restorable" API methods.

When a [State] object wants access to the return value of a [Route] object it has pushed onto the [Navigator], a [RestorableRouteFuture] ensures that it will also have access to that value after state restoration.

To show a new route on the navigator defined by the [navigatorFinder], call [present], which will invoke the [onPresent] callback. The [onPresent] callback must add a new route to the navigator provided to it using one of the "restorable" API methods. When the newly added route completes, the [onComplete] callback executes. It is given the return value of the route, which may be null.

While the route added via [present] is shown on the navigator, it can be accessed via the [route] getter.

If the property is restored to a state in which [present] had been called on it, but the route has not completed yet, the [RestorableRouteFuture] will obtain the restored route object from the navigator again and call [onComplete] once it completes.

The [RestorableRouteFuture] can only keep track of one active [route]. When [present] has been called to add a route, it may only be called again after the previously added route has completed.

{@tool dartpad} This example uses a [RestorableRouteFuture] in the `_MyHomeState` to push a new `MyCounter` route and to retrieve its return value.

** See code in examples/api/lib/widgets/navigator/restorable_route_future.0.dart ** {@end-tool}

### RestorableRouteFuture()

```dart
RestorableRouteFuture({NavigatorFinderCallback navigatorFinder = _defaultNavigatorFinder, required RoutePresentationCallback onPresent, RouteCompletionCallback<T>? onComplete})
```

Creates a [RestorableRouteFuture].

### navigatorFinder

```dart
NavigatorFinderCallback navigatorFinder
```

A callback that given the [BuildContext] of the [State] object to which this property is registered returns the [NavigatorState] of the navigator to which the route instantiated in [onPresent] is added.

### onPresent

```dart
RoutePresentationCallback onPresent
```

A callback that add a new [Route] to the provided navigator.

The callback must use one of the API methods on the [NavigatorState] that have "restorable" in their name (e.g. [NavigatorState.restorablePush], [NavigatorState.restorablePushNamed], etc.) and return the opaque ID returned by those methods.

This callback is invoked when [present] is called with the `arguments` Object that was passed to that method and the [NavigatorState] obtained from [navigatorFinder].

### onComplete

```dart
RouteCompletionCallback<T>? onComplete
```

A callback that is invoked when the [Route] added via [onPresent] completes.

The return value of that route is passed to this method.

### present()

```dart
void present([Object? arguments])
```

Shows the route created by [onPresent] and invoke [onComplete] when it completes.

The `arguments` object is passed to [onPresent] and can be used to customize the route. It must be serializable via the [StandardMessageCodec]. Often, a [Map] is used to pass key-value pairs.

### isPresent

```dart
bool get isPresent
```

Whether the [Route] created by [present] is currently shown.

Returns true after [present] has been called until the [Route] completes.

### route

```dart
Route<T>? get route
```

The route that [present] added to the Navigator.

Returns null when currently no route is shown

### createDefaultValue()

```dart
String? createDefaultValue()
```

### initWithValue()

```dart
void initWithValue(String? value)
```

### toPrimitives()

```dart
Object? toPrimitives()
```

### fromPrimitives()

```dart
String fromPrimitives(Object? data)
```

### dispose()

```dart
void dispose()
```

### enabled

```dart
bool get enabled
```

# NavigationNotification

```dart
class NavigationNotification extends Notification {}
```

A notification that a change in navigation has taken place.

Specifically, this notification indicates that at least one of the following has occurred:

- That route stack of a [Navigator] has changed in any way.
- The ability to pop has changed, such as controlled by [PopScope].

### NavigationNotification()

```dart
NavigationNotification({required bool canHandlePop})
```

Creates a notification that some change in navigation has happened.

### canHandlePop

```dart
bool canHandlePop
```

Indicates that the originator of this [Notification] is capable of handling a navigation pop.

### toString()

```dart
String toString()
```
