@docImport 'navigator.dart';

# PageRoute

```dart
abstract class PageRoute<T> extends ModalRoute<T> {}
```

A modal route that replaces the entire screen.

The [PageRouteBuilder] subclass provides a way to create a [PageRoute] using callbacks rather than by defining a new class via subclassing.

If `barrierDismissible` is true, then pressing the escape key on the keyboard will cause the current route to be popped with null as the value.

See also:

- [Route], which documents the meaning of the `T` generic type argument.

### PageRoute()

```dart
PageRoute({RouteSettings? settings, bool? requestFocus, TraversalEdgeBehavior? traversalEdgeBehavior, TraversalEdgeBehavior? directionalTraversalEdgeBehavior, bool fullscreenDialog = false, bool allowSnapshotting = true, bool barrierDismissible = false})
```

Creates a modal route that replaces the entire screen.

### fullscreenDialog

```dart
bool fullscreenDialog
```

{@template flutter.widgets.PageRoute.fullscreenDialog} Whether this page route is a full-screen dialog.

In Material and Cupertino, being fullscreen has the effects of making the app bars have a close button instead of a back button. On iOS, dialogs transitions animate differently and are also not closeable with the back swipe gesture. {@endtemplate}

### allowSnapshotting

```dart
bool allowSnapshotting
```

### opaque

```dart
bool get opaque
```

### barrierDismissible

```dart
bool get barrierDismissible
```

### canTransitionTo()

```dart
bool canTransitionTo(TransitionRoute<dynamic> nextRoute)
```

### canTransitionFrom()

```dart
bool canTransitionFrom(TransitionRoute<dynamic> previousRoute)
```

### popGestureEnabled

```dart
bool get popGestureEnabled
```

# PageRouteBuilder

```dart
class PageRouteBuilder<T> extends PageRoute<T> {}
```

A utility class for defining one-off page routes in terms of callbacks.

Callers must define the [pageBuilder] function which creates the route's primary contents. To add transitions define the [transitionsBuilder] function.

The `T` generic type argument corresponds to the type argument of the created [Route] objects.

See also:

- [Route], which documents the meaning of the `T` generic type argument.

### PageRouteBuilder()

```dart
PageRouteBuilder({RouteSettings? settings, bool? requestFocus, required RoutePageBuilder pageBuilder, RouteTransitionsBuilder transitionsBuilder = _defaultTransitionsBuilder, Duration transitionDuration = const Duration(milliseconds: 300), Duration reverseTransitionDuration = const Duration(milliseconds: 300), bool opaque = true, bool barrierDismissible = false, Color? barrierColor, String? barrierLabel, bool maintainState = true, bool fullscreenDialog, bool allowSnapshotting = true})
```

Creates a route that delegates to builder callbacks.

### pageBuilder

```dart
RoutePageBuilder pageBuilder
```

{@template flutter.widgets.pageRouteBuilder.pageBuilder} Used to build the route's primary contents.

See [ModalRoute.buildPage] for complete definition of the parameters. {@endtemplate}

### transitionsBuilder

```dart
RouteTransitionsBuilder transitionsBuilder
```

{@template flutter.widgets.pageRouteBuilder.transitionsBuilder} Used to build the route's transitions.

The [animation] argument drives this route's own entrance and exit transition. The [secondaryAnimation] argument drives transitions for this route when another route is pushed on top of it or popped from above it, if both routes allow transition coordination. See [TransitionRoute.canTransitionTo] and [TransitionRoute.canTransitionFrom].

See [ModalRoute.buildTransitions] for complete definition of the parameters. {@endtemplate}

The default transition is a jump cut (i.e. no animation).

### transitionDuration

```dart
Duration transitionDuration
```

### reverseTransitionDuration

```dart
Duration reverseTransitionDuration
```

### opaque

```dart
bool opaque
```

### barrierDismissible

```dart
bool barrierDismissible
```

### barrierColor

```dart
Color? barrierColor
```

### barrierLabel

```dart
String? barrierLabel
```

### maintainState

```dart
bool maintainState
```

### buildPage()

```dart
Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```
