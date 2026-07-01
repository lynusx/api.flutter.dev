@docImport 'package:flutter/services.dart';

@docImport 'app.dart'; @docImport 'bottom_app_bar.dart'; @docImport 'bottom_navigation_bar.dart'; @docImport 'bottom_sheet_theme.dart'; @docImport 'drawer_theme.dart'; @docImport 'icon_button.dart'; @docImport 'tab_controller.dart'; @docImport 'tabs.dart'; @docImport 'text_button.dart';

# ScaffoldMessenger

```dart
class ScaffoldMessenger extends StatefulWidget {}
```

Manages [SnackBar]s and [MaterialBanner]s for descendant [Scaffold]s.

{@youtube 560 315 https://www.youtube.com/watch?v=lytQi-slT5Y}

This class provides APIs for showing snack bars and material banners at the bottom and top of the screen, respectively.

To display one of these notifications, obtain the [ScaffoldMessengerState] for the current [BuildContext] via [ScaffoldMessenger.of] and use the [ScaffoldMessengerState.showSnackBar] or the [ScaffoldMessengerState.showMaterialBanner] functions.

When the [ScaffoldMessenger] has nested [Scaffold] descendants, the ScaffoldMessenger will only present the notification to the root Scaffold of the subtree of Scaffolds. In order to show notifications for the inner, nested Scaffolds, set a new scope by instantiating a new ScaffoldMessenger in between the levels of nesting.

{@tool dartpad} Here is an example of showing a [SnackBar] when the user presses a button.

** See code in examples/api/lib/material/scaffold/scaffold_messenger.0.dart ** {@end-tool}

See also:

- [SnackBar], which is a temporary notification typically shown near the bottom of the app using the [ScaffoldMessengerState.showSnackBar] method.
- [MaterialBanner], which is a temporary notification typically shown at the top of the app using the [ScaffoldMessengerState.showMaterialBanner] method.
- [debugCheckHasScaffoldMessenger], which asserts that the given context has a [ScaffoldMessenger] ancestor.
- Cookbook: [Display a SnackBar](https://docs.flutter.dev/cookbook/design/snackbars)

### ScaffoldMessenger()

```dart
ScaffoldMessenger({dynamic key, required Widget child})
```

Creates a widget that manages [SnackBar]s for [Scaffold] descendants.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### of()

```dart
ScaffoldMessengerState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

{@tool dartpad} Typical usage of the [ScaffoldMessenger.of] function is to call it in response to a user gesture or an application state change.

** See code in examples/api/lib/material/scaffold/scaffold_messenger.of.0.dart ** {@end-tool}

A less elegant but more expedient solution is to assign a [GlobalKey] to the [ScaffoldMessenger], then use the `key.currentState` property to obtain the [ScaffoldMessengerState] rather than using the [ScaffoldMessenger.of] function. The [MaterialApp.scaffoldMessengerKey] refers to the root ScaffoldMessenger that is provided by default.

{@tool dartpad} Sometimes [SnackBar]s are produced by code that doesn't have ready access to a valid [BuildContext]. One such example of this is when you show a SnackBar from a method outside of the `build` function. In these cases, you can assign a [GlobalKey] to the [ScaffoldMessenger]. This example shows a key being used to obtain the [ScaffoldMessengerState] provided by the [MaterialApp].

** See code in examples/api/lib/material/scaffold/scaffold_messenger.of.1.dart ** {@end-tool}

If there is no [ScaffoldMessenger] in scope, then this will assert in debug mode, and throw an exception in release mode.

See also:

- [maybeOf], which is a similar function but will return null instead of throwing if there is no [ScaffoldMessenger] ancestor.
- [debugCheckHasScaffoldMessenger], which asserts that the given context has a [ScaffoldMessenger] ancestor.

### maybeOf()

```dart
ScaffoldMessengerState? maybeOf(BuildContext context)
```

The state from the closest instance of this class that encloses the given context, if any.

Will return null if a [ScaffoldMessenger] is not found in the given context.

See also:

- [of], which is a similar function, except that it will throw an exception if a [ScaffoldMessenger] is not found in the given context.

### createState()

```dart
ScaffoldMessengerState createState()
```

# ScaffoldMessengerState

```dart
class ScaffoldMessengerState extends State<ScaffoldMessenger> with TickerProviderStateMixin {}
```

State for a [ScaffoldMessenger].

A [ScaffoldMessengerState] object can be used to [showSnackBar] or [showMaterialBanner] for every registered [Scaffold] that is a descendant of the associated [ScaffoldMessenger]. Scaffolds will register to receive [SnackBar]s and [MaterialBanner]s from their closest ScaffoldMessenger ancestor.

Typically obtained via [ScaffoldMessenger.of].

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### showSnackBar()

```dart
ScaffoldFeatureController<SnackBar, SnackBarClosedReason> showSnackBar(SnackBar snackBar, {AnimationStyle? snackBarAnimationStyle})
```

Shows a [SnackBar] across all registered [Scaffold]s. Scaffolds register to receive snack bars from their closest [ScaffoldMessenger] ancestor. If there are several registered scaffolds the snack bar is shown simultaneously on all of them.

A scaffold can show at most one snack bar at a time. If this function is called while another snack bar is already visible, the given snack bar will be added to a queue and displayed after the earlier snack bars have closed.

To control how long a [SnackBar] remains visible, use [SnackBar.duration].

To remove the [SnackBar] with an exit animation, use [hideCurrentSnackBar] or call [ScaffoldFeatureController.close] on the returned [ScaffoldFeatureController]. To remove a [SnackBar] suddenly (without an animation), use [removeCurrentSnackBar].

See [ScaffoldMessenger.of] for information about how to obtain the [ScaffoldMessengerState].

{@tool dartpad} Here is an example of showing a [SnackBar] when the user presses a button.

** See code in examples/api/lib/material/scaffold/scaffold_messenger_state.show_snack_bar.0.dart ** {@end-tool}

## Relative positioning of floating SnackBars

A [SnackBar] with [SnackBar.behavior] set to [SnackBarBehavior.floating] is positioned above the widgets provided to [Scaffold.floatingActionButton], [Scaffold.persistentFooterButtons], and [Scaffold.bottomNavigationBar]. If some or all of these widgets take up enough space such that the SnackBar would not be visible when positioned above them, an error will be thrown. In this case, consider constraining the size of these widgets to allow room for the SnackBar to be visible.

{@tool dartpad} Here is an example showing how to display a [SnackBar] with [showSnackBar]

** See code in examples/api/lib/material/scaffold/scaffold_messenger_state.show_snack_bar.0.dart ** {@end-tool}

{@tool dartpad} Here is an example showing that a floating [SnackBar] appears above [Scaffold.floatingActionButton].

** See code in examples/api/lib/material/scaffold/scaffold_messenger_state.show_snack_bar.1.dart ** {@end-tool}

If [AnimationStyle.duration] is provided in the [snackBarAnimationStyle] parameter, it will be used to override the snackbar show animation duration. Otherwise, defaults to 250ms.

If [AnimationStyle.reverseDuration] is provided in the [snackBarAnimationStyle] parameter, it will be used to override the snackbar hide animation duration. Otherwise, defaults to 250ms.

To disable the snackbar animation, use [AnimationStyle.noAnimation].

{@tool dartpad} This sample showcases how to override [SnackBar] show and hide animation duration using [AnimationStyle] in [ScaffoldMessengerState.showSnackBar].

** See code in examples/api/lib/material/scaffold/scaffold_messenger_state.show_snack_bar.2.dart ** {@end-tool}

### removeCurrentSnackBar()

```dart
void removeCurrentSnackBar({SnackBarClosedReason reason = SnackBarClosedReason.remove})
```

Removes the current [SnackBar] (if any) immediately from registered [Scaffold]s.

The removed snack bar does not run its normal exit animation. If there are any queued snack bars, they begin their entrance animation immediately.

### hideCurrentSnackBar()

```dart
void hideCurrentSnackBar({SnackBarClosedReason reason = SnackBarClosedReason.hide})
```

Removes the current [SnackBar] by running its normal exit animation.

The closed completer is called after the animation is complete.

### clearSnackBars()

```dart
void clearSnackBars()
```

Removes all the snackBars currently in queue by clearing the queue and running normal exit animation on the current snackBar.

### showMaterialBanner()

```dart
ScaffoldFeatureController<MaterialBanner, MaterialBannerClosedReason> showMaterialBanner(MaterialBanner materialBanner)
```

Shows a [MaterialBanner] across all registered [Scaffold]s. Scaffolds register to receive material banners from their closest [ScaffoldMessenger] ancestor. If there are several registered scaffolds the material banner is shown simultaneously on all of them.

A scaffold can show at most one material banner at a time. If this function is called while another material banner is already visible, the given material banner will be added to a queue and displayed after the earlier material banners have closed.

To remove the [MaterialBanner] with an exit animation, use [hideCurrentMaterialBanner] or call [ScaffoldFeatureController.close] on the returned [ScaffoldFeatureController]. To remove a [MaterialBanner] suddenly (without an animation), use [removeCurrentMaterialBanner].

See [ScaffoldMessenger.of] for information about how to obtain the [ScaffoldMessengerState].

{@tool dartpad} Here is an example of showing a [MaterialBanner] when the user presses a button.

** See code in examples/api/lib/material/scaffold/scaffold_messenger_state.show_material_banner.0.dart ** {@end-tool}

### removeCurrentMaterialBanner()

```dart
void removeCurrentMaterialBanner({MaterialBannerClosedReason reason = MaterialBannerClosedReason.remove})
```

Removes the current [MaterialBanner] (if any) immediately from registered [Scaffold]s.

The removed material banner does not run its normal exit animation. If there are any queued material banners, they begin their entrance animation immediately.

### hideCurrentMaterialBanner()

```dart
void hideCurrentMaterialBanner({MaterialBannerClosedReason reason = MaterialBannerClosedReason.hide})
```

Removes the current [MaterialBanner] by running its normal exit animation.

The closed completer is called after the animation is complete.

### clearMaterialBanners()

```dart
void clearMaterialBanners()
```

Removes all the [MaterialBanner]s currently in queue by clearing the queue and running normal exit animation on the current [MaterialBanner].

### build()

```dart
Widget build(BuildContext context)
```

### dispose()

```dart
void dispose()
```

# ScaffoldPrelayoutGeometry

```dart
class ScaffoldPrelayoutGeometry {}
```

The geometry of the [Scaffold] after all its contents have been laid out except the [FloatingActionButton].

The [Scaffold] passes this pre-layout geometry to its [FloatingActionButtonLocation], which produces an [Offset] that the [Scaffold] uses to position the [FloatingActionButton].

For a description of the [Scaffold]'s geometry after it has finished laying out, see the [ScaffoldGeometry].

### ScaffoldPrelayoutGeometry()

```dart
ScaffoldPrelayoutGeometry({required Size bottomSheetSize, required double contentBottom, required double contentTop, required Size floatingActionButtonSize, required EdgeInsets minInsets, required EdgeInsets minViewPadding, required Size scaffoldSize, required Size snackBarSize, required Size materialBannerSize, required TextDirection textDirection})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### floatingActionButtonSize

```dart
Size floatingActionButtonSize
```

The [Size] of [Scaffold.floatingActionButton].

If [Scaffold.floatingActionButton] is null, this will be [Size.zero].

### bottomSheetSize

```dart
Size bottomSheetSize
```

The [Size] of the [Scaffold]'s [BottomSheet].

If the [Scaffold] is not currently showing a [BottomSheet], this will be [Size.zero].

### contentBottom

```dart
double contentBottom
```

The vertical distance from the Scaffold's origin to the bottom of [Scaffold.body].

This is useful in a [FloatingActionButtonLocation] designed to place the [FloatingActionButton] at the bottom of the screen, while keeping it above the [BottomSheet], the [Scaffold.bottomNavigationBar], or the keyboard.

The [Scaffold.body] is laid out with respect to [minInsets] already. This means that a [FloatingActionButtonLocation] does not need to factor in [EdgeInsets.bottom] of [minInsets] when aligning a [FloatingActionButton] to [contentBottom].

### contentTop

```dart
double contentTop
```

The vertical distance from the [Scaffold]'s origin to the top of [Scaffold.body].

This is useful in a [FloatingActionButtonLocation] designed to place the [FloatingActionButton] at the top of the screen, while keeping it below the [Scaffold.appBar].

The [Scaffold.body] is laid out with respect to [minInsets] already. This means that a [FloatingActionButtonLocation] does not need to factor in [EdgeInsets.top] of [minInsets] when aligning a [FloatingActionButton] to [contentTop].

### minInsets

```dart
EdgeInsets minInsets
```

The minimum padding to inset the [FloatingActionButton] by for it to remain visible.

This value is the result of calling [MediaQueryData.padding] in the [Scaffold]'s [BuildContext], and is useful for insetting the [FloatingActionButton] to avoid features like the system status bar or the keyboard.

If [Scaffold.resizeToAvoidBottomInset] is set to false, [EdgeInsets.bottom] of [minInsets] will be 0.0.

### minViewPadding

```dart
EdgeInsets minViewPadding
```

The minimum padding to inset interactive elements to be within a safe, un-obscured space.

This value reflects the [MediaQueryData.viewPadding] of the [Scaffold]'s [BuildContext] when [Scaffold.resizeToAvoidBottomInset] is false or and the [MediaQueryData.viewInsets] > 0.0. This helps distinguish between different types of obstructions on the screen, such as software keyboards and physical device notches.

### scaffoldSize

```dart
Size scaffoldSize
```

The [Size] of the whole [Scaffold].

If the [Size] of the [Scaffold]'s contents is modified by values such as [Scaffold.resizeToAvoidBottomInset] or the keyboard opening, then the [scaffoldSize] will not reflect those changes.

This means that [FloatingActionButtonLocation]s designed to reposition the [FloatingActionButton] based on events such as the keyboard popping up should use [minInsets] to make sure that the [FloatingActionButton] is inset by enough to remain visible.

See [minInsets] and [MediaQueryData.padding] for more information on the appropriate insets to apply.

### snackBarSize

```dart
Size snackBarSize
```

The [Size] of the [Scaffold]'s [SnackBar].

If the [Scaffold] is not showing a [SnackBar], this will be [Size.zero].

### materialBannerSize

```dart
Size materialBannerSize
```

The [Size] of the [Scaffold]'s [MaterialBanner].

If the [Scaffold] is not showing a [MaterialBanner], this will be [Size.zero].

### textDirection

```dart
TextDirection textDirection
```

The [TextDirection] of the [Scaffold]'s [BuildContext].

# ScaffoldGeometry

```dart
class ScaffoldGeometry {}
```

Geometry information for [Scaffold] components after layout is finished.

To get a [ValueNotifier] for the scaffold geometry of a given [BuildContext], use [Scaffold.geometryOf].

The ScaffoldGeometry is only available during the paint phase, because its value is computed during the animation and layout phases prior to painting.

For an example of using the [ScaffoldGeometry], see the [BottomAppBar], which uses the [ScaffoldGeometry] to paint a notch around the [FloatingActionButton].

For information about the [Scaffold]'s geometry that is used while laying out the [FloatingActionButton], see [ScaffoldPrelayoutGeometry].

### ScaffoldGeometry()

```dart
ScaffoldGeometry({double? bottomNavigationBarTop, Rect? floatingActionButtonArea})
```

Create an object that describes the geometry of a [Scaffold].

### bottomNavigationBarTop

```dart
double? bottomNavigationBarTop
```

The distance from the [Scaffold]'s top edge to the top edge of the rectangle in which the [Scaffold.bottomNavigationBar] bar is laid out.

Null if [Scaffold.bottomNavigationBar] is null.

### floatingActionButtonArea

```dart
Rect? floatingActionButtonArea
```

The [Scaffold.floatingActionButton]'s bounding rectangle.

This is null when there is no floating action button showing.

### copyWith()

```dart
ScaffoldGeometry copyWith({double? bottomNavigationBarTop, Rect? floatingActionButtonArea})
```

Creates a copy of this [ScaffoldGeometry] but with the given fields replaced with the new values.

# Scaffold

```dart
class Scaffold extends StatefulWidget {}
```

Implements the basic Material Design visual layout structure.

This class provides APIs for showing drawers and bottom sheets.

To display a persistent bottom sheet, obtain the [ScaffoldState] for the current [BuildContext] via [Scaffold.of] and use the [ScaffoldState.showBottomSheet] function.

{@tool dartpad} This example shows a [Scaffold] with a [body] and [FloatingActionButton]. The [body] is a [Text] placed in a [Center] in order to center the text within the [Scaffold]. The [FloatingActionButton] is connected to a callback that increments a counter.

** See code in examples/api/lib/material/scaffold/scaffold.0.dart ** {@end-tool}

{@tool dartpad} This example shows a [Scaffold] with a blueGrey [backgroundColor], [body] and [FloatingActionButton]. The [body] is a [Text] placed in a [Center] in order to center the text within the [Scaffold]. The [FloatingActionButton] is connected to a callback that increments a counter.

![](https://flutter.github.io/assets-for-api-docs/assets/material/scaffold_background_color.png)

** See code in examples/api/lib/material/scaffold/scaffold.1.dart ** {@end-tool}

{@tool dartpad} This example shows a [Scaffold] with an [AppBar], a [BottomAppBar] and a [FloatingActionButton]. The [body] is a [Text] placed in a [Center] in order to center the text within the [Scaffold]. The [FloatingActionButton] is centered and docked within the [BottomAppBar] using [FloatingActionButtonLocation.centerDocked]. The [FloatingActionButton] is connected to a callback that increments a counter.

![](https://flutter.github.io/assets-for-api-docs/assets/material/scaffold_bottom_app_bar.png)

** See code in examples/api/lib/material/scaffold/scaffold.2.dart ** {@end-tool}

## Scaffold layout, the keyboard, and display "notches"

The scaffold will expand to fill the available space. That usually means that it will occupy its entire window or device screen. When the device's keyboard appears the Scaffold's ancestor [MediaQuery] widget's [MediaQueryData.viewInsets] changes and the Scaffold will be rebuilt. By default the scaffold's [body] is resized to make room for the keyboard. To prevent the resize set [resizeToAvoidBottomInset] to false. In either case the focused widget will be scrolled into view if it's within a scrollable container.

The [MediaQueryData.padding] value defines areas that might not be completely visible, like the display "notch" on the iPhone X. The scaffold's [body] is not inset by this padding value although an [appBar] or [bottomNavigationBar] will typically cause the body to avoid the padding. The [SafeArea] widget can be used within the scaffold's body to avoid areas like display notches.

## Floating action button with a draggable scrollable bottom sheet

If [Scaffold.bottomSheet] is a [DraggableScrollableSheet], [Scaffold.floatingActionButton] is set, and the bottom sheet is dragged to cover greater than 70% of the Scaffold's height, two things happen in parallel:

- Scaffold starts to show scrim (see [ScaffoldState.showBodyScrim]), and
- [Scaffold.floatingActionButton] is scaled down through an animation with a [Curves.easeIn], and disappears when the bottom sheet covers the entire Scaffold.

And as soon as the bottom sheet is dragged down to cover less than 70% of the [Scaffold], the scrim disappears and [Scaffold.floatingActionButton] animates back to its normal size.

## Troubleshooting

### Nested Scaffolds

The Scaffold is designed to be a top level container for a [MaterialApp]. This means that adding a Scaffold to each route on a Material app will provide the app with Material's basic visual layout structure.

It is typically not necessary to nest Scaffolds. For example, in a tabbed UI, where the [bottomNavigationBar] is a [TabBar] and the body is a [TabBarView], you might be tempted to make each tab bar view a scaffold with a differently titled AppBar. Rather, it would be better to add a listener to the [TabController] that updates the AppBar

{@tool snippet} Add a listener to the app's tab controller so that the [AppBar] title of the app's one and only scaffold is reset each time a new tab is selected.

```dart
TabController(vsync: tickerProvider, length: tabCount)..addListener(() {
  if (!tabController.indexIsChanging) {
    setState(() {
      // Rebuild the enclosing scaffold with a new AppBar title
      appBarTitle = 'Tab ${tabController.index}';
    });
  }
})
```

{@end-tool}

Although there are some use cases, like a presentation app that shows embedded flutter content, where nested scaffolds are appropriate, it's best to avoid nesting scaffolds.

See also:

- [AppBar], which is a horizontal bar typically shown at the top of an app using the [appBar] property.
- [BottomAppBar], which is a horizontal bar typically shown at the bottom of an app using the [bottomNavigationBar] property.
- [FloatingActionButton], which is a circular button typically shown in the bottom right corner of the app using the [floatingActionButton] property.
- [Drawer], which is a vertical panel that is typically displayed to the left of the body (and often hidden on phones) using the [drawer] property.
- [BottomNavigationBar], which is a horizontal array of buttons typically shown along the bottom of the app using the [bottomNavigationBar] property.
- [BottomSheet], which is an overlay typically shown near the bottom of the app. A bottom sheet can either be persistent, in which case it is shown using the [ScaffoldState.showBottomSheet] method, or modal, in which case it is shown using the [showModalBottomSheet] function.
- [SnackBar], which is a lightweight message with an optional action which briefly displays at the bottom of the screen. Use the [ScaffoldMessengerState.showSnackBar] method to show snack bars.
- [MaterialBanner], which displays an important, succinct message, at the top of the screen, below the app bar. Use the [ScaffoldMessengerState.showMaterialBanner] method to show material banners.
- [ScaffoldState], which is the state associated with this widget.
- <https://material.io/design/layout/responsive-layout-grid.html>
- Cookbook: [Add a Drawer to a screen](https://docs.flutter.dev/cookbook/design/drawer)

### Scaffold()

```dart
Scaffold({dynamic key, PreferredSizeWidget? appBar, Widget? body, Widget? floatingActionButton, FloatingActionButtonLocation? floatingActionButtonLocation, FloatingActionButtonAnimator? floatingActionButtonAnimator, List<Widget>? persistentFooterButtons, AlignmentDirectional persistentFooterAlignment = AlignmentDirectional.centerEnd, BoxDecoration? persistentFooterDecoration, Widget? drawer, DrawerCallback? onDrawerChanged, Widget? endDrawer, DrawerCallback? onEndDrawerChanged, Widget? bottomNavigationBar, Widget? bottomSheet, Color? backgroundColor, bool? resizeToAvoidBottomInset, bool primary = true, DragStartBehavior drawerDragStartBehavior = DragStartBehavior.start, bool extendBody = false, bool drawerBarrierDismissible = true, bool extendBodyBehindAppBar = false, Color? drawerScrimColor, Widget? Function(BuildContext, Animation<double>) bottomSheetScrimBuilder = _defaultBottomSheetScrimBuilder, double? drawerEdgeDragWidth, bool drawerEnableOpenDragGesture = true, bool endDrawerEnableOpenDragGesture = true, String? restorationId})
```

Creates a visual scaffold for Material Design widgets.

### extendBody

```dart
bool extendBody
```

If true, and [bottomNavigationBar] or [persistentFooterButtons] is specified, then the [body] extends to the bottom of the Scaffold, instead of only extending to the top of the [bottomNavigationBar] or the [persistentFooterButtons].

If true, a [MediaQuery] widget whose bottom padding matches the height of the [bottomNavigationBar] will be added above the scaffold's [body].

This property is often useful when the [bottomNavigationBar] has a non-rectangular shape, like [CircularNotchedRectangle], which adds a [FloatingActionButton] sized notch to the top edge of the bar. In this case specifying `extendBody: true` ensures that scaffold's body will be visible through the bottom navigation bar's notch.

See also:

- [extendBodyBehindAppBar], which extends the height of the body to the top of the scaffold.

### drawerBarrierDismissible

```dart
bool drawerBarrierDismissible
```

Whether the drawer can be dismissed by tapping on the barrier.

If false, and a [drawer] is specified, then the barrier behind the drawer will not respond to a tap event and thus remains open.

Defaults to true, in which case the drawer will close upon the user tapping on the barrier.

### extendBodyBehindAppBar

```dart
bool extendBodyBehindAppBar
```

If true, and an [appBar] is specified, then the height of the [body] is extended to include the height of the app bar and the top of the body is aligned with the top of the app bar.

This is useful if the app bar's [AppBar.backgroundColor] is not completely opaque.

This property is false by default.

See also:

- [extendBody], which extends the height of the body to the bottom of the scaffold.

### appBar

```dart
PreferredSizeWidget? appBar
```

An app bar to display at the top of the scaffold.

### body

```dart
Widget? body
```

The primary content of the scaffold.

Displayed below the [appBar], above the bottom of the ambient [MediaQuery]'s [MediaQueryData.viewInsets], and behind the [floatingActionButton] and [drawer]. If [resizeToAvoidBottomInset] is false then the body is not resized when the onscreen keyboard appears, i.e. it is not inset by `viewInsets.bottom`.

The widget in the body of the scaffold is positioned at the top-left of the available space between the app bar and the bottom of the scaffold. To center this widget instead, consider putting it in a [Center] widget and having that be the body. To expand this widget instead, consider putting it in a [SizedBox.expand].

If you have a column of widgets that should normally fit on the screen, but may overflow and would in such cases need to scroll, consider using a [ListView] as the body of the scaffold. This is also a good choice for the case where your body is a scrollable list.

### floatingActionButton

```dart
Widget? floatingActionButton
```

A button displayed floating above [body], in the bottom right corner.

Typically a [FloatingActionButton].

### floatingActionButtonLocation

```dart
FloatingActionButtonLocation? floatingActionButtonLocation
```

Responsible for determining where the [floatingActionButton] should go.

If null, the [ScaffoldState] will use the default location, [FloatingActionButtonLocation.endFloat].

### floatingActionButtonAnimator

```dart
FloatingActionButtonAnimator? floatingActionButtonAnimator
```

Animator to move the [floatingActionButton] to a new [floatingActionButtonLocation].

If null, the [ScaffoldState] will use the default animator, [FloatingActionButtonAnimator.scaling].

### persistentFooterButtons

```dart
List<Widget>? persistentFooterButtons
```

A set of buttons that are displayed at the bottom of the scaffold.

Typically this is a list of [TextButton] widgets. These buttons are persistently visible, even if the [body] of the scaffold scrolls.

These widgets will be wrapped in an [OverflowBar].

The [persistentFooterButtons] are rendered above the [bottomNavigationBar] but below the [body].

### persistentFooterAlignment

```dart
AlignmentDirectional persistentFooterAlignment
```

The alignment of the [persistentFooterButtons] inside the [OverflowBar].

Defaults to [AlignmentDirectional.centerEnd].

### persistentFooterDecoration

```dart
BoxDecoration? persistentFooterDecoration
```

Decoration for the container that holds the [persistentFooterButtons].

By default, this container has a top border with a width of 1.0, created by [Divider.createBorderSide].

See also:

- [persistentFooterButtons], which defines the buttons to show in the footer.
- [persistentFooterAlignment], which defines the alignment of the footer buttons.

### drawer

```dart
Widget? drawer
```

A panel displayed to the side of the [body], often hidden on mobile devices. Swipes in from either left-to-right ([TextDirection.ltr]) or right-to-left ([TextDirection.rtl])

Typically a [Drawer].

To open the drawer, use the [ScaffoldState.openDrawer] function.

To close the drawer, use either [ScaffoldState.closeDrawer], [Navigator.pop] or press the escape key on the keyboard.

{@tool dartpad} To disable the drawer edge swipe on mobile, set the [Scaffold.drawerEnableOpenDragGesture] to false. Then, use [ScaffoldState.openDrawer] to open the drawer and [Navigator.pop] to close it.

** See code in examples/api/lib/material/scaffold/scaffold.drawer.0.dart ** {@end-tool}

### onDrawerChanged

```dart
DrawerCallback? onDrawerChanged
```

Optional callback that is called when the [Scaffold.drawer] is opened or closed.

### endDrawer

```dart
Widget? endDrawer
```

A panel displayed to the side of the [body], often hidden on mobile devices. Swipes in from right-to-left ([TextDirection.ltr]) or left-to-right ([TextDirection.rtl])

Typically a [Drawer].

To open the drawer, use the [ScaffoldState.openEndDrawer] function.

To close the drawer, use either [ScaffoldState.closeEndDrawer], [Navigator.pop] or press the escape key on the keyboard.

{@tool dartpad} To disable the drawer edge swipe, set the [Scaffold.endDrawerEnableOpenDragGesture] to false. Then, use [ScaffoldState.openEndDrawer] to open the drawer and [Navigator.pop] to close it.

** See code in examples/api/lib/material/scaffold/scaffold.end_drawer.0.dart ** {@end-tool}

### onEndDrawerChanged

```dart
DrawerCallback? onEndDrawerChanged
```

Optional callback that is called when the [Scaffold.endDrawer] is opened or closed.

### drawerScrimColor

```dart
Color? drawerScrimColor
```

The color to use for the scrim that obscures primary content while a drawer is open.

If this is null, then [DrawerThemeData.scrimColor] is used. If that is also null, then it defaults to [Colors.black54].

### bottomSheetScrimBuilder

```dart
Widget? Function(BuildContext, Animation<double>) bottomSheetScrimBuilder
```

A builder for the widget that obscures primary content while a bottom sheet is open.

The builder receives the current [BuildContext] and an [Animation] as parameters. The [Animation] ranges from 0.0 to 1.0 based on how much the bottom sheet covers the screen. A value of 0.0 represents when the bottom sheet covers 70% of the screen, and 1.0 represents when the bottom sheet fully covers the screen.

If this is null, then a non-dismissable [ModalBarrier] with [Colors.black] is used. The barrier is animated to fade in and out as the bottom sheet is opened and closed.

If the builder returns null, then no scrim is shown.

### backgroundColor

```dart
Color? backgroundColor
```

The color of the [Material] widget that underlies the entire Scaffold.

The theme's [ThemeData.scaffoldBackgroundColor] by default.

### bottomNavigationBar

```dart
Widget? bottomNavigationBar
```

A bottom navigation bar to display at the bottom of the scaffold.

Snack bars slide from underneath the bottom navigation bar while bottom sheets are stacked on top.

The [bottomNavigationBar] is rendered below the [persistentFooterButtons] and the [body].

### bottomSheet

```dart
Widget? bottomSheet
```

The persistent bottom sheet to display.

A persistent bottom sheet shows information that supplements the primary content of the app. A persistent bottom sheet remains visible even when the user interacts with other parts of the app.

A closely related widget is a modal bottom sheet, which is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app. Modal bottom sheets can be created and displayed with the [showModalBottomSheet] function.

Unlike the persistent bottom sheet displayed by [showBottomSheet] this bottom sheet is not a [LocalHistoryEntry] and cannot be dismissed with the scaffold appbar's back button.

If a persistent bottom sheet created with [showBottomSheet] is already visible, it must be closed before building the Scaffold with a new [bottomSheet].

The value of [bottomSheet] can be any widget at all. It's unlikely to actually be a [BottomSheet], which is used by the implementations of [showBottomSheet] and [showModalBottomSheet]. Typically it's a widget that includes [Material].

See also:

- [showBottomSheet], which displays a bottom sheet as a route that can be dismissed with the scaffold's back button.
- [showModalBottomSheet], which displays a modal bottom sheet.
- [BottomSheetThemeData], which can be used to customize the default bottom sheet property values when using a [BottomSheet].

### resizeToAvoidBottomInset

```dart
bool? resizeToAvoidBottomInset
```

If true the [body] and the scaffold's floating widgets should size themselves to avoid the onscreen keyboard whose height is defined by the ambient [MediaQuery]'s [MediaQueryData.viewInsets] `bottom` property.

For example, if there is an onscreen keyboard displayed above the scaffold, the body can be resized to avoid overlapping the keyboard, which prevents widgets inside the body from being obscured by the keyboard.

Defaults to true.

### primary

```dart
bool primary
```

Whether this scaffold is being displayed at the top of the screen.

If true then the height of the [appBar] will be extended by the height of the screen's status bar, i.e. the top padding for [MediaQuery].

If true, on iOS and macOS, tapping the status bar scrolls the app's [PrimaryScrollController] to the top.

The default value of this property, like the default value of [AppBar.primary], is true.

### drawerDragStartBehavior

```dart
DragStartBehavior drawerDragStartBehavior
```

{@macro flutter.material.DrawerController.dragStartBehavior}

### drawerEdgeDragWidth

```dart
double? drawerEdgeDragWidth
```

The width of the area within which a horizontal swipe will open the drawer.

By default, the value used is 20.0 added to the padding edge of `MediaQuery.paddingOf(context)` that corresponds to the surrounding [TextDirection]. This ensures that the drag area for notched devices is not obscured. For example, if `TextDirection.of(context)` is set to [TextDirection.ltr], 20.0 will be added to `MediaQuery.paddingOf(context).left`.

### drawerEnableOpenDragGesture

```dart
bool drawerEnableOpenDragGesture
```

Determines if the [Scaffold.drawer] can be opened with a drag gesture on mobile.

On desktop platforms, the drawer is not draggable.

By default, the drag gesture is enabled on mobile.

### endDrawerEnableOpenDragGesture

```dart
bool endDrawerEnableOpenDragGesture
```

Determines if the [Scaffold.endDrawer] can be opened with a gesture on mobile.

On desktop platforms, the drawer is not draggable.

By default, the drag gesture is enabled on mobile.

### restorationId

```dart
String? restorationId
```

Restoration ID to save and restore the state of the [Scaffold].

If it is non-null, the scaffold will persist and restore whether the [drawer] and [endDrawer] was open or closed.

The state of this widget is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### of()

```dart
ScaffoldState of(BuildContext context)
```

Finds the [ScaffoldState] from the closest instance of this class that encloses the given context.

If no instance of this class encloses the given context, will cause an assert in debug mode, and throw an exception in release mode.

This method can be expensive (it walks the element tree).

{@tool dartpad} Typical usage of the [Scaffold.of] function is to call it from within the `build` method of a child of a [Scaffold].

** See code in examples/api/lib/material/scaffold/scaffold.of.0.dart ** {@end-tool}

{@tool dartpad} When the [Scaffold] is actually created in the same `build` function, the `context` argument to the `build` function can't be used to find the [Scaffold] (since it's "above" the widget being returned in the widget tree). In such cases, the following technique with a [Builder] can be used to provide a new scope with a [BuildContext] that is "under" the [Scaffold]:

** See code in examples/api/lib/material/scaffold/scaffold.of.1.dart ** {@end-tool}

A more efficient solution is to split your build function into several widgets. This introduces a new context from which you can obtain the [Scaffold]. In this solution, you would have an outer widget that creates the [Scaffold] populated by instances of your new inner widgets, and then in these inner widgets you would use [Scaffold.of].

A less elegant but more expedient solution is assign a [GlobalKey] to the [Scaffold], then use the `key.currentState` property to obtain the [ScaffoldState] rather than using the [Scaffold.of] function.

If there is no [Scaffold] in scope, then this will throw an exception. To return null if there is no [Scaffold], use [maybeOf] instead.

### maybeOf()

```dart
ScaffoldState? maybeOf(BuildContext context)
```

Finds the [ScaffoldState] from the closest instance of this class that encloses the given context.

If no instance of this class encloses the given context, will return null. To throw an exception instead, use [of] instead of this function.

This method can be expensive (it walks the element tree).

See also:

- [of], a similar function to this one that throws if no instance encloses the given context. Also includes some sample code in its documentation.

### geometryOf()

```dart
ValueListenable<ScaffoldGeometry> geometryOf(BuildContext context)
```

Returns a [ValueListenable] for the [ScaffoldGeometry] for the closest [Scaffold] ancestor of the given context.

The [ValueListenable.value] is only available at paint time.

Notifications are guaranteed to be sent before the first paint pass with the new geometry, but there is no guarantee whether a build or layout passes are going to happen between the notification and the next paint pass.

The closest [Scaffold] ancestor for the context might change, e.g when an element is moved from one scaffold to another. For [StatefulWidget]s using this listenable, a change of the [Scaffold] ancestor will trigger a [State.didChangeDependencies].

A typical pattern for listening to the scaffold geometry would be to call [Scaffold.geometryOf] in [State.didChangeDependencies], compare the return value with the previous listenable, if it has changed, unregister the listener, and register a listener to the new [ScaffoldGeometry] listenable.

### hasDrawer()

```dart
bool hasDrawer(BuildContext context, {bool registerForUpdates = true})
```

Whether the Scaffold that most tightly encloses the given context has a drawer.

If this is being used during a build (for example to decide whether to show an "open drawer" button), set the `registerForUpdates` argument to true. This will then set up an [InheritedWidget] relationship with the [Scaffold] so that the client widget gets rebuilt whenever the [hasDrawer] value changes.

This method can be expensive (it walks the element tree).

See also:

- [Scaffold.of], which provides access to the [ScaffoldState] object as a whole, from which you can show bottom sheets, and so forth.

### createState()

```dart
ScaffoldState createState()
```

# ScaffoldState

```dart
class ScaffoldState extends State<Scaffold> with TickerProviderStateMixin, RestorationMixin, WidgetsBindingObserver {}
```

State for a [Scaffold].

Can display [BottomSheet]s. Retrieve a [ScaffoldState] from the current [BuildContext] using [Scaffold.of].

### restorationId

```dart
String? get restorationId
```

### restoreState()

```dart
void restoreState(RestorationBucket? oldBucket, bool initialRestore)
```

### hasAppBar

```dart
bool get hasAppBar
```

Whether this scaffold has a non-null [Scaffold.appBar].

### hasDrawer

```dart
bool get hasDrawer
```

Whether this scaffold has a non-null [Scaffold.drawer].

### hasEndDrawer

```dart
bool get hasEndDrawer
```

Whether this scaffold has a non-null [Scaffold.endDrawer].

### hasFloatingActionButton

```dart
bool get hasFloatingActionButton
```

Whether this scaffold has a non-null [Scaffold.floatingActionButton].

### appBarMaxHeight

```dart
double? get appBarMaxHeight
```

The max height the [Scaffold.appBar] uses.

This is based on the appBar preferred height plus the top padding.

### isDrawerOpen

```dart
bool get isDrawerOpen
```

Whether the [Scaffold.drawer] is opened.

See also:

- [ScaffoldState.openDrawer], which opens the [Scaffold.drawer] of a [Scaffold].

### isDrawerBarrierDismissible

```dart
bool get isDrawerBarrierDismissible
```

Whether the [Scaffold.drawerBarrierDismissible] flag is set.

### isEndDrawerOpen

```dart
bool get isEndDrawerOpen
```

Whether the [Scaffold.endDrawer] is opened.

See also:

- [ScaffoldState.openEndDrawer], which opens the [Scaffold.endDrawer] of a [Scaffold].

### openDrawer()

```dart
void openDrawer()
```

Opens the [Drawer] (if any).

If the scaffold has a non-null [Scaffold.drawer], this function will cause the drawer to begin its entrance animation.

Normally this is not needed since the [Scaffold] automatically shows an appropriate [IconButton], and handles the edge-swipe gesture, to show the drawer.

To close the drawer, use either [ScaffoldState.closeDrawer] or [Navigator.pop].

See [Scaffold.of] for information about how to obtain the [ScaffoldState].

### openEndDrawer()

```dart
void openEndDrawer()
```

Opens the end side [Drawer] (if any).

If the scaffold has a non-null [Scaffold.endDrawer], this function will cause the end side drawer to begin its entrance animation.

Normally this is not needed since the [Scaffold] automatically shows an appropriate [IconButton], and handles the edge-swipe gesture, to show the drawer.

To close the drawer, use either [ScaffoldState.closeEndDrawer] or [Navigator.pop].

See [Scaffold.of] for information about how to obtain the [ScaffoldState].

### closeDrawer()

```dart
void closeDrawer()
```

Closes [Scaffold.drawer] if it is currently opened.

See [Scaffold.of] for information about how to obtain the [ScaffoldState].

### closeEndDrawer()

```dart
void closeEndDrawer()
```

Closes [Scaffold.endDrawer] if it is currently opened.

See [Scaffold.of] for information about how to obtain the [ScaffoldState].

### showBottomSheet()

```dart
PersistentBottomSheetController showBottomSheet(WidgetBuilder builder, {Color? backgroundColor, double? elevation, ShapeBorder? shape, Clip? clipBehavior, BoxConstraints? constraints, bool? enableDrag, bool? showDragHandle, AnimationController? transitionAnimationController, AnimationStyle? sheetAnimationStyle})
```

Shows a Material Design bottom sheet in the nearest [Scaffold]. To show a persistent bottom sheet, use the [Scaffold.bottomSheet].

Returns a controller that can be used to close and otherwise manipulate the bottom sheet.

To rebuild the bottom sheet (e.g. if it is stateful), call [PersistentBottomSheetController.setState] on the controller returned by this method.

The new bottom sheet becomes a [LocalHistoryEntry] for the enclosing [ModalRoute] and a back button is added to the app bar of the [Scaffold] that closes the bottom sheet.

The [transitionAnimationController] controls the bottom sheet's entrance and exit animations. It's up to the owner of the controller to call [AnimationController.dispose] when the controller is no longer needed.

To create a persistent bottom sheet that is not a [LocalHistoryEntry] and does not add a back button to the enclosing Scaffold's app bar, use the [Scaffold.bottomSheet] constructor parameter.

A persistent bottom sheet shows information that supplements the primary content of the app. A persistent bottom sheet remains visible even when the user interacts with other parts of the app.

A closely related widget is a modal bottom sheet, which is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app. Modal bottom sheets can be created and displayed with the [showModalBottomSheet] function.

{@tool dartpad} This example demonstrates how to use [showBottomSheet] to display a bottom sheet when a user taps a button. It also demonstrates how to close a bottom sheet using the Navigator.

** See code in examples/api/lib/material/scaffold/scaffold_state.show_bottom_sheet.0.dart ** {@end-tool}

The [sheetAnimationStyle] parameter is used to override the bottom sheet animation duration and reverse animation duration.

If [AnimationStyle.duration] is provided, it will be used to override the bottom sheet animation duration in the underlying [BottomSheet.createAnimationController].

If [AnimationStyle.reverseDuration] is provided, it will be used to override the bottom sheet reverse animation duration in the underlying [BottomSheet.createAnimationController].

To disable the bottom sheet animation, use [AnimationStyle.noAnimation].

{@tool dartpad} This sample showcases how to override the [showBottomSheet] animation duration and reverse animation duration using [AnimationStyle].

** See code in examples/api/lib/material/scaffold/scaffold_state.show_bottom_sheet.1.dart ** {@end-tool} See also:

- [BottomSheet], which becomes the parent of the widget returned by the `builder`.
- [showBottomSheet], which calls this method given a [BuildContext].
- [showModalBottomSheet], which can be used to display a modal bottom sheet.
- [Scaffold.of], for information about how to obtain the [ScaffoldState].
- The Material 2 spec at <https://m2.material.io/components/sheets-bottom>.
- The Material 3 spec at <https://m3.material.io/components/bottom-sheets/overview>.
- [AnimationStyle], which is used to override the modal bottom sheet animation duration and reverse animation duration.

### handleStatusBarTap()

```dart
void handleStatusBarTap()
```

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(Scaffold oldWidget)
```

### didChangeDependencies()

```dart
void didChangeDependencies()
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

### showBodyScrim()

```dart
void showBodyScrim(bool value, double animationValue)
```

Updates the state of the body scrim.

This method is used to show or hide the body scrim and to set the animation value.

### build()

```dart
Widget build(BuildContext context)
```

# ScaffoldFeatureController

```dart
class ScaffoldFeatureController<T extends Widget, U> {}
```

An interface for controlling a feature of a [Scaffold].

Commonly obtained from [ScaffoldMessengerState.showSnackBar] or [ScaffoldState.showBottomSheet].

### closed

```dart
Future<U> get closed
```

Completes when the feature controlled by this object is no longer visible.

### close

```dart
VoidCallback close
```

Remove the feature (e.g., bottom sheet, snack bar, or material banner) from the scaffold.

### setState

```dart
StateSetter? setState
```

Mark the feature (e.g., bottom sheet or snack bar) as needing to rebuild.

# PersistentBottomSheetController

```dart
class PersistentBottomSheetController extends ScaffoldFeatureController<_StandardBottomSheet, void> {}
```

A [ScaffoldFeatureController] for standard bottom sheets.

This is the type of objects returned by [ScaffoldState.showBottomSheet].

This controller is used to display both standard and persistent bottom sheets. A bottom sheet is only persistent if it is set as the [Scaffold.bottomSheet].
