# MaterialPageRoute

```dart
class MaterialPageRoute<T> extends PageRoute<T> with MaterialRouteTransitionMixin<T> {}
```

A modal route that replaces the entire screen with a platform-adaptive transition.

{@macro flutter.material.materialRouteTransitionMixin}

By default, when a modal route is replaced by another, the previous route remains in memory. To free all the resources when this is not necessary, set [maintainState] to false.

The `fullscreenDialog` property specifies whether the incoming route is a fullscreen modal dialog. On iOS, those routes animate from the bottom to the top rather than horizontally.

If `barrierDismissible` is true, then pressing the escape key on the keyboard will cause the current route to be popped with null as the value.

The type `T` specifies the return type of the route which can be supplied as the route is popped from the stack via [Navigator.pop] by providing the optional `result` argument.

See also:

- [MaterialRouteTransitionMixin], which provides the material transition for this route.
- [MaterialPage], which is a [Page] of this class.

### MaterialPageRoute()

```dart
MaterialPageRoute({required WidgetBuilder builder, dynamic settings, dynamic requestFocus, bool maintainState = true, dynamic fullscreenDialog, dynamic allowSnapshotting = true, dynamic barrierDismissible = false, dynamic traversalEdgeBehavior, dynamic directionalTraversalEdgeBehavior})
```

Construct a MaterialPageRoute whose contents are defined by [builder].

### builder

```dart
WidgetBuilder builder
```

Builds the primary contents of the route.

### buildContent()

```dart
Widget buildContent(BuildContext context)
```

### maintainState

```dart
bool maintainState
```

### debugLabel

```dart
String get debugLabel
```

# MaterialRouteTransitionMixin

```dart
mixin MaterialRouteTransitionMixin<T> on PageRoute<T> {}
```

A mixin that provides platform-adaptive transitions for a [PageRoute].

{@template flutter.material.materialRouteTransitionMixin} For Android, the entrance transition for the page zooms in and fades in while the exiting page zooms out and fades out. The exit transition is similar, but in reverse.

For iOS, the page slides in from the right and exits in reverse. The page also shifts to the left in parallax when another page enters to cover it. (These directions are flipped in environments with a right-to-left reading direction.) {@endtemplate}

See also:

- [PageTransitionsTheme], which defines the default page transitions used by the [MaterialRouteTransitionMixin.buildTransitions].
- [ZoomPageTransitionsBuilder], which is the default page transition used by the [PageTransitionsTheme].
- [CupertinoPageTransitionsBuilder], which is the default page transition for iOS and macOS.

### buildContent()

```dart
Widget buildContent(BuildContext context)
```

Builds the primary contents of the route.

### transitionDuration

```dart
Duration get transitionDuration
```

### reverseTransitionDuration

```dart
Duration get reverseTransitionDuration
```

### didPush()

```dart
TickerFuture didPush()
```

### didPop()

```dart
bool didPop(T? result)
```

### barrierColor

```dart
Color? get barrierColor
```

### barrierLabel

```dart
String? get barrierLabel
```

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

### canTransitionTo()

```dart
bool canTransitionTo(TransitionRoute<dynamic> nextRoute)
```

### canTransitionFrom()

```dart
bool canTransitionFrom(TransitionRoute<dynamic> previousRoute)
```

### buildPage()

```dart
Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# MaterialPage

```dart
class MaterialPage<T> extends Page<T> {}
```

A page that creates a material style [PageRoute].

{@macro flutter.material.materialRouteTransitionMixin}

By default, when the created route is replaced by another, the previous route remains in memory. To free all the resources when this is not necessary, set [maintainState] to false.

The `fullscreenDialog` property specifies whether the created route is a fullscreen modal dialog. On iOS, those routes animate from the bottom to the top rather than horizontally.

The type `T` specifies the return type of the route which can be supplied as the route is popped from the stack via [Navigator.transitionDelegate] by providing the optional `result` argument to the [RouteTransitionRecord.markForPop] in the [TransitionDelegate.resolve].

See also:

- [MaterialPageRoute], which is the [PageRoute] version of this class

### MaterialPage()

```dart
MaterialPage({required Widget child, bool maintainState = true, bool fullscreenDialog = false, bool allowSnapshotting = true, dynamic key, dynamic canPop, dynamic onPopInvoked, dynamic name, dynamic arguments, dynamic restorationId})
```

Creates a material page.

### child

```dart
Widget child
```

The content to be shown in the [Route] created by this page.

### maintainState

```dart
bool maintainState
```

{@macro flutter.widgets.ModalRoute.maintainState}

### fullscreenDialog

```dart
bool fullscreenDialog
```

{@macro flutter.widgets.PageRoute.fullscreenDialog}

### allowSnapshotting

```dart
bool allowSnapshotting
```

{@macro flutter.widgets.TransitionRoute.allowSnapshotting}

### createRoute()

```dart
Route<T> createRoute(BuildContext context)
```
