@docImport 'dart:ui';

@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/services.dart';

@docImport 'app.dart'; @docImport 'button.dart'; @docImport 'dialog.dart'; @docImport 'nav_bar.dart'; @docImport 'page_scaffold.dart'; @docImport 'tab_scaffold.dart';

# kCupertinoModalBarrierColor

```dart
Color kCupertinoModalBarrierColor
```

Barrier color for a Cupertino modal barrier.

Extracted from https://developer.apple.com/design/resources/.

# CupertinoRouteTransitionMixin

```dart
mixin CupertinoRouteTransitionMixin<T> on PageRoute<T> {}
```

A mixin that replaces the entire screen with an iOS transition for a [PageRoute].

{@template flutter.cupertino.cupertinoRouteTransitionMixin} The page slides in from the right and exits in reverse. The page also shifts to the left in parallax when another page enters to cover it.

The page slides in from the bottom and exits in reverse with no parallax effect for fullscreen dialogs. {@endtemplate}

See also:

- [MaterialRouteTransitionMixin], which is a mixin that provides platform-appropriate transitions for a [PageRoute].
- [CupertinoPageRoute], which is a [PageRoute] that leverages this mixin.

### buildContent()

```dart
Widget buildContent(BuildContext context)
```

Builds the primary contents of the route.

### title

```dart
String? get title
```

{@template flutter.cupertino.CupertinoRouteTransitionMixin.title} A title string for this route.

Used to auto-populate [CupertinoNavigationBar] and [CupertinoSliverNavigationBar]'s `middle`/`largeTitle` widgets when one is not manually supplied. {@endtemplate}

### previousTitle

```dart
ValueListenable<String?> get previousTitle
```

The title string of the previous [CupertinoPageRoute].

The [ValueListenable]'s value is readable after the route is installed onto a [Navigator]. The [ValueListenable] will also notify its listeners if the value changes (such as by replacing the previous route).

The [ValueListenable] itself will be null before the route is installed. Its content value will be null if the previous route has no title or is not a [CupertinoPageRoute].

See also:

- [ValueListenableBuilder], which can be used to listen and rebuild widgets based on a ValueListenable.

### dispose()

```dart
void dispose()
```

### didChangePrevious()

```dart
void didChangePrevious(Route<dynamic>? previousRoute)
```

### kTransitionDuration

```dart
Duration kTransitionDuration
```

The duration of the page transition.

A relatively rigorous eyeball estimation.

### transitionDuration

```dart
Duration get transitionDuration
```

### barrierColor

```dart
Color? get barrierColor
```

### barrierLabel

```dart
String? get barrierLabel
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

### buildPageTransitions()

```dart
Widget buildPageTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

Returns a [CupertinoFullscreenDialogTransition] if [route] is a full screen dialog, otherwise a [CupertinoPageTransition] is returned.

Used by [CupertinoPageRoute.buildTransitions].

This method can be applied to any [PageRoute], not just [CupertinoPageRoute]. It's typically used to provide a Cupertino style horizontal transition for material widgets when the target platform is [TargetPlatform.iOS].

See also:

- [CupertinoPageTransitionsBuilder], which uses this method to define a [PageTransitionsBuilder] for the [PageTransitionsTheme].

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# CupertinoPageRoute

```dart
class CupertinoPageRoute<T> extends PageRoute<T> with CupertinoRouteTransitionMixin<T> {}
```

A modal route that replaces the entire screen with an iOS transition.

{@macro flutter.cupertino.cupertinoRouteTransitionMixin}

By default, when a modal route is replaced by another, the previous route remains in memory. To free all the resources when this is not necessary, set [maintainState] to false.

The type `T` specifies the return type of the route which can be supplied as the route is popped from the stack via [Navigator.pop] when an optional `result` can be provided.

If `barrierDismissible` is true, then pressing the escape key on the keyboard will cause the current route to be popped with null as the value.

See also:

- [CupertinoRouteTransitionMixin], for a mixin that provides iOS transition for this modal route.
- [MaterialPageRoute], for an adaptive [PageRoute] that uses a platform-appropriate transition.
- [CupertinoPageScaffold], for applications that have one page with a fixed navigation bar on top.
- [CupertinoTabScaffold], for applications that have a tab bar at the bottom with multiple pages.
- [CupertinoPage], for a [Page] version of this class.

### CupertinoPageRoute()

```dart
CupertinoPageRoute({required WidgetBuilder builder, String? title, dynamic settings, dynamic requestFocus, bool maintainState = true, dynamic fullscreenDialog, dynamic allowSnapshotting = true, dynamic barrierDismissible = false})
```

Creates a page route for use in an iOS designed app.

The [builder], [maintainState], and [fullscreenDialog] arguments must not be null.

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

### builder

```dart
WidgetBuilder builder
```

Builds the primary contents of the route.

### buildContent()

```dart
Widget buildContent(BuildContext context)
```

### title

```dart
String? title
```

### maintainState

```dart
bool maintainState
```

### debugLabel

```dart
String get debugLabel
```

# CupertinoPage

```dart
class CupertinoPage<T> extends Page<T> {}
```

A page that creates a cupertino style [PageRoute].

{@macro flutter.cupertino.cupertinoRouteTransitionMixin}

By default, when a created modal route is replaced by another, the previous route remains in memory. To free all the resources when this is not necessary, set [maintainState] to false.

The type `T` specifies the return type of the route which can be supplied as the route is popped from the stack via [Navigator.transitionDelegate] by providing the optional `result` argument to the [RouteTransitionRecord.markForPop] in the [TransitionDelegate.resolve].

See also:

- [CupertinoPageRoute], for a [PageRoute] version of this class.

### CupertinoPage()

```dart
CupertinoPage({required Widget child, bool maintainState = true, String? title, bool fullscreenDialog = false, bool allowSnapshotting = true, dynamic canPop, dynamic onPopInvoked, dynamic key, dynamic name, dynamic arguments, dynamic restorationId})
```

Creates a cupertino page.

### child

```dart
Widget child
```

The content to be shown in the [Route] created by this page.

### title

```dart
String? title
```

{@macro flutter.cupertino.CupertinoRouteTransitionMixin.title}

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

# CupertinoPageTransition

```dart
class CupertinoPageTransition extends StatefulWidget {}
```

Provides an iOS-style page transition animation.

The page slides in from the right and exits in reverse. It also shifts to the left in a parallax motion when another page enters to cover it.

### CupertinoPageTransition()

```dart
CupertinoPageTransition({dynamic key, required Animation<double> primaryRouteAnimation, required Animation<double> secondaryRouteAnimation, required Widget child, required bool linearTransition})
```

Creates an iOS-style page transition.

### child

```dart
Widget child
```

The widget below this widget in the tree.

### primaryRouteAnimation

```dart
Animation<double> primaryRouteAnimation
```

- `primaryRouteAnimation` is a linear route animation from 0.0 to 1.0 when this screen is being pushed.

### secondaryRouteAnimation

```dart
Animation<double> secondaryRouteAnimation
```

- `secondaryRouteAnimation` is a linear route animation from 0.0 to 1.0 when another screen is being pushed on top of this one.

### linearTransition

```dart
bool linearTransition
```

- `linearTransition` is whether to perform the transitions linearly. Used to precisely track back gesture drags.

### delegatedTransition()

```dart
Widget? delegatedTransition(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, bool allowSnapshotting, Widget? child)
```

The Cupertino styled [DelegatedTransitionBuilder] provided to the previous route.

{@macro flutter.widgets.delegatedTransition}

### createState()

```dart
State<CupertinoPageTransition> createState()
```

# CupertinoFullscreenDialogTransition

```dart
class CupertinoFullscreenDialogTransition extends StatefulWidget {}
```

An iOS-style transition used for summoning fullscreen dialogs.

For example, used when creating a new calendar event by bringing in the next screen from the bottom.

### CupertinoFullscreenDialogTransition()

```dart
CupertinoFullscreenDialogTransition({dynamic key, required Animation<double> primaryRouteAnimation, required Animation<double> secondaryRouteAnimation, required Widget child, required bool linearTransition})
```

Creates an iOS-style transition used for summoning fullscreen dialogs.

### primaryRouteAnimation

```dart
Animation<double> primaryRouteAnimation
```

- `primaryRouteAnimation` is a linear route animation from 0.0 to 1.0 when this screen is being pushed.

### secondaryRouteAnimation

```dart
Animation<double> secondaryRouteAnimation
```

- `secondaryRouteAnimation` is a linear route animation from 0.0 to 1.0 when another screen is being pushed on top of this one.

### linearTransition

```dart
bool linearTransition
```

- `linearTransition` is whether to perform the transitions linearly. Used to precisely track back gesture drags.

### child

```dart
Widget child
```

The widget below this widget in the tree.

### createState()

```dart
State<CupertinoFullscreenDialogTransition> createState()
```

# CupertinoModalPopupRoute

```dart
class CupertinoModalPopupRoute<T> extends PopupRoute<T> {}
```

A route that shows a modal iOS-style popup that slides up from the bottom of the screen.

Such a popup is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app.

It is used internally by [showCupertinoModalPopup] or can be directly pushed onto the [Navigator] stack to enable state restoration. See [showCupertinoModalPopup] for a state restoration app example.

The `barrierColor` argument determines the [Color] of the barrier underneath the popup. When unspecified, the barrier color defaults to a light opacity black scrim based on iOS's dialog screens. To correctly have iOS resolve to the appropriate modal colors, pass in `CupertinoDynamicColor.resolve(kCupertinoModalBarrierColor, context)`.

The `barrierDismissible` argument determines whether clicking outside the popup results in dismissal. It is `true` by default.

The `semanticsDismissible` argument is used to determine whether the semantics of the modal barrier are included in the semantics tree.

The `routeSettings` argument is used to provide [RouteSettings] to the created Route.

{@macro flutter.widgets.RawDialogRoute}

See also:

- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- [CupertinoActionSheet], which is the widget usually returned by the `builder` argument.
- <https://developer.apple.com/design/human-interface-guidelines/ios/views/action-sheets/>

### CupertinoModalPopupRoute()

```dart
CupertinoModalPopupRoute({required WidgetBuilder builder, String barrierLabel = 'Dismiss', Color? barrierColor = kCupertinoModalBarrierColor, bool barrierDismissible = true, bool semanticsDismissible = false, dynamic filter, dynamic settings, dynamic requestFocus, Offset? anchorPoint})
```

A route that shows a modal iOS-style popup that slides up from the bottom of the screen.

### builder

```dart
WidgetBuilder builder
```

A builder that builds the widget tree for the [CupertinoModalPopupRoute].

The [builder] argument typically builds a [CupertinoActionSheet] widget.

Content below the widget is dimmed with a [ModalBarrier]. The widget built by the [builder] does not share a context with the route it was originally built from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the widget needs to update dynamically.

### barrierLabel

```dart
String barrierLabel
```

### barrierColor

```dart
Color? barrierColor
```

### barrierDismissible

```dart
bool get barrierDismissible
```

### semanticsDismissible

```dart
bool get semanticsDismissible
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

### createSimulation()

```dart
Simulation createSimulation({required bool forward})
```

### buildPage()

```dart
Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# showCupertinoModalPopup()

```dart
Future<T?> showCupertinoModalPopup<T>({required BuildContext context, required WidgetBuilder builder, ImageFilter? filter, Color barrierColor = kCupertinoModalBarrierColor, bool barrierDismissible = true, bool useRootNavigator = true, bool semanticsDismissible = false, RouteSettings? routeSettings, Offset? anchorPoint, bool? requestFocus})
```

Shows a modal iOS-style popup that slides up from the bottom of the screen.

Such a popup is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app.

The `context` argument is used to look up the [Navigator] for the popup. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the popup is closed.

The `barrierColor` argument determines the [Color] of the barrier underneath the popup. When unspecified, the barrier color defaults to a light opacity black scrim based on iOS's dialog screens.

The `barrierDismissible` argument determines whether clicking outside the popup results in dismissal. It is `true` by default.

The `useRootNavigator` argument is used to determine whether to push the popup to the [Navigator] furthest from or nearest to the given `context`. It is `true` by default.

The `semanticsDismissible` argument is used to determine whether the semantics of the modal barrier are included in the semantics tree.

The `routeSettings` argument is used to provide [RouteSettings] to the created Route.

The `builder` argument typically builds a [CupertinoActionSheet] widget. Content below the widget is dimmed with a [ModalBarrier]. The widget built by the `builder` does not share a context with the location that [showCupertinoModalPopup] is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the widget needs to update dynamically.

The [requestFocus] parameter is used to specify whether the popup should request focus when shown. {@macro flutter.widgets.navigator.Route.requestFocus}

{@macro flutter.widgets.RawDialogRoute}

Returns a `Future` that resolves to the value that was passed to [Navigator.pop] when the popup was closed.

### State Restoration in Modals

Using this method will not enable state restoration for the modal. In order to enable state restoration for a modal, use [Navigator.restorablePush] or [Navigator.restorablePushNamed] with [CupertinoModalPopupRoute].

For more information about state restoration, see [RestorationManager].

{@tool dartpad} This sample demonstrates how to create a restorable Cupertino modal route. This is accomplished by enabling state restoration by specifying [CupertinoApp.restorationScopeId] and using [Navigator.restorablePush] to push [CupertinoModalPopupRoute] when the [CupertinoButton] is tapped.

{@macro flutter.widgets.RestorationManager}

** See code in examples/api/lib/cupertino/route/show_cupertino_modal_popup.0.dart ** {@end-tool}

See also:

- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- [CupertinoActionSheet], which is the widget usually returned by the `builder` argument to [showCupertinoModalPopup].
- <https://developer.apple.com/design/human-interface-guidelines/ios/views/action-sheets/>

# showCupertinoDialog()

```dart
Future<T?> showCupertinoDialog<T>({required BuildContext context, required WidgetBuilder builder, String? barrierLabel, Color? barrierColor, bool useRootNavigator = true, bool barrierDismissible = false, RouteSettings? routeSettings, Offset? anchorPoint, bool? requestFocus})
```

Displays an iOS-style dialog above the current contents of the app, with iOS-style entrance and exit animations, modal barrier color, and modal barrier behavior (by default, the dialog is not dismissible with a tap on the barrier).

This function takes a `builder` which typically builds a [CupertinoAlertDialog] widget. Content below the dialog is dimmed with a [ModalBarrier]. The widget returned by the `builder` does not share a context with the location that [showCupertinoDialog] is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the dialog needs to update dynamically.

The `context` argument is used to look up the [Navigator] for the dialog. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the dialog is closed.

The `useRootNavigator` argument is used to determine whether to push the dialog to the [Navigator] furthest from or nearest to the given `context`. By default, `useRootNavigator` is `true` and the dialog route created by this method is pushed to the root navigator.

{@macro flutter.material.dialog.requestFocus} {@macro flutter.widgets.navigator.Route.requestFocus}

{@macro flutter.widgets.RawDialogRoute}

If the application has multiple [Navigator] objects, it may be necessary to call `Navigator.of(context, rootNavigator: true).pop(result)` to close the dialog rather than just `Navigator.pop(context, result)`.

Returns a [Future] that resolves to the value (if any) that was passed to [Navigator.pop] when the dialog was closed.

### State Restoration in Dialogs

Using this method will not enable state restoration for the dialog. In order to enable state restoration for a dialog, use [Navigator.restorablePush] or [Navigator.restorablePushNamed] with [CupertinoDialogRoute].

For more information about state restoration, see [RestorationManager].

{@tool dartpad} This sample demonstrates how to create a restorable Cupertino dialog. This is accomplished by enabling state restoration by specifying [CupertinoApp.restorationScopeId] and using [Navigator.restorablePush] to push [CupertinoDialogRoute] when the [CupertinoButton] is tapped.

{@macro flutter.widgets.RestorationManager}

** See code in examples/api/lib/cupertino/route/show_cupertino_dialog.0.dart ** {@end-tool}

See also:

- [CupertinoAlertDialog], an iOS-style alert dialog.
- [showDialog], which displays a Material-style dialog.
- [showGeneralDialog], which allows for customization of the dialog popup.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- <https://developer.apple.com/design/human-interface-guidelines/alerts/>

# CupertinoDialogRoute

```dart
class CupertinoDialogRoute<T> extends RawDialogRoute<T> {}
```

A dialog route that shows an iOS-style dialog.

It is used internally by [showCupertinoDialog] or can be directly pushed onto the [Navigator] stack to enable state restoration. See [showCupertinoDialog] for a state restoration app example.

This function takes a `builder` which typically builds a [Dialog] widget. Content below the dialog is dimmed with a [ModalBarrier]. The widget returned by the `builder` does not share a context with the location that `showDialog` is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the dialog needs to update dynamically.

The `context` argument is used to look up [CupertinoLocalizations.modalBarrierDismissLabel], which provides the modal with a localized accessibility label that will be used for the modal's barrier. However, a custom `barrierLabel` can be passed in as well.

The `barrierDismissible` argument is used to indicate whether tapping on the barrier will dismiss the dialog. It is `true` by default and cannot be `null`.

The `barrierColor` argument is used to specify the color of the modal barrier that darkens everything below the dialog. If `null`, then [CupertinoDynamicColor.resolve] is used to compute the modal color.

The `settings` argument define the settings for this route. See [RouteSettings] for details.

{@macro flutter.widgets.RawDialogRoute}

See also:

- [showCupertinoDialog], which is a way to display an iOS-style dialog.
- [showGeneralDialog], which allows for customization of the dialog popup.
- [showDialog], which displays a Material dialog.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.

### CupertinoDialogRoute()

```dart
CupertinoDialogRoute({required WidgetBuilder builder, required BuildContext context, dynamic barrierDismissible, Color? barrierColor, String? barrierLabel, dynamic transitionDuration = const Duration(milliseconds: 250), RouteTransitionsBuilder? transitionBuilder, dynamic settings, dynamic requestFocus, dynamic anchorPoint})
```

A dialog route that shows an iOS-style dialog.

### transitionBuilder

```dart
RouteTransitionsBuilder? transitionBuilder
```

Custom transition builder

### createSimulation()

```dart
Simulation createSimulation({required bool forward})
```

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

### dispose()

```dart
void dispose()
```

# CupertinoPageTransitionsBuilder

```dart
class CupertinoPageTransitionsBuilder extends PageTransitionsBuilder {}
```

A [PageTransitionsBuilder] that provides an iOS-style page transition animation.

The page slides in from the right and exits in reverse. It also shifts to the left in a parallax motion when another page enters to cover it. This transition is commonly seen in native iOS applications.

In a [CupertinoApp], this transition is used automatically when navigating with [CupertinoPageRoute].

See also:

- [CupertinoPageRoute], which uses this transition style by default for Cupertino apps.
- [CupertinoPageTransition], the widget that implements the iOS page transition animation.
- [MaterialPageRoute], an adaptive [PageRoute] that can use this builder through [PageTransitionsTheme].
- [PageTransitionsTheme], which defines the page transitions used by [MaterialPageRoute] for different target platforms.

### CupertinoPageTransitionsBuilder()

```dart
CupertinoPageTransitionsBuilder()
```

Constructs a page transition animation that matches the iOS transition.

### transitionDuration

```dart
Duration get transitionDuration
```

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```
