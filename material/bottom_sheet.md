@docImport 'dart:ui';

# BottomSheetDragStartHandler

```dart
typedef BottomSheetDragStartHandler = void Function(DragStartDetails details)
```

A callback for when the user begins dragging the bottom sheet.

Used by [BottomSheet.onDragStart].

# BottomSheetDragEndHandler

```dart
typedef BottomSheetDragEndHandler = void Function(DragEndDetails details, {required bool isClosing})
```

A callback for when the user stops dragging the bottom sheet.

Used by [BottomSheet.onDragEnd].

# BottomSheet

```dart
class BottomSheet extends StatefulWidget {}
```

A Material Design bottom sheet.

There are two kinds of bottom sheets in Material Design:

- _Persistent_. A persistent bottom sheet shows information that supplements the primary content of the app. A persistent bottom sheet remains visible even when the user interacts with other parts of the app. Persistent bottom sheets can be created and displayed with the [ScaffoldState.showBottomSheet] function or by specifying the [Scaffold.bottomSheet] constructor parameter.

- _Modal_. A modal bottom sheet is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app. Modal bottom sheets can be created and displayed with the [showModalBottomSheet] function.

The [BottomSheet] widget itself is rarely used directly. Instead, prefer to create a persistent bottom sheet with [ScaffoldState.showBottomSheet] or [Scaffold.bottomSheet], and a modal bottom sheet with [showModalBottomSheet].

See also:

- [showBottomSheet] and [ScaffoldState.showBottomSheet], for showing non-modal "persistent" bottom sheets.
- [showModalBottomSheet], which can be used to display a modal bottom sheet.
- [BottomSheetThemeData], which can be used to customize the default bottom sheet property values.
- The Material 2 spec at <https://m2.material.io/components/sheets-bottom>.
- The Material 3 spec at <https://m3.material.io/components/bottom-sheets/overview>.

### BottomSheet()

```dart
BottomSheet({dynamic key, AnimationController? animationController, bool enableDrag = true, bool? showDragHandle, Color? dragHandleColor, Size? dragHandleSize, BottomSheetDragStartHandler? onDragStart, BottomSheetDragEndHandler? onDragEnd, Color? backgroundColor, Color? shadowColor, double? elevation, ShapeBorder? shape, Clip? clipBehavior, BoxConstraints? constraints, required VoidCallback onClosing, required WidgetBuilder builder})
```

Creates a bottom sheet.

Typically, bottom sheets are created implicitly by [ScaffoldState.showBottomSheet], for persistent bottom sheets, or by [showModalBottomSheet], for modal bottom sheets.

### animationController

```dart
AnimationController? animationController
```

The animation controller that controls the bottom sheet's entrance and exit animations.

The BottomSheet widget will manipulate the position of this animation, it is not just a passive observer.

### onClosing

```dart
VoidCallback onClosing
```

Called when the bottom sheet begins to close.

A bottom sheet might be prevented from closing (e.g., by user interaction) even after this callback is called. For this reason, this callback might be call multiple times for a given bottom sheet.

### builder

```dart
WidgetBuilder builder
```

A builder for the contents of the sheet.

The bottom sheet will wrap the widget produced by this builder in a [Material] widget.

### enableDrag

```dart
bool enableDrag
```

If true, the bottom sheet can be dragged up and down and dismissed by swiping downwards.

If [showDragHandle] is true, this only applies to the content below the drag handle, because the drag handle is always draggable.

Default is true.

If this is true, the [animationController] must not be null. Use [BottomSheet.createAnimationController] to create one, or provide another AnimationController.

### showDragHandle

```dart
bool? showDragHandle
```

Specifies whether a drag handle is shown.

The drag handle appears at the top of the bottom sheet. The default color is [ColorScheme.onSurfaceVariant] with an opacity of 0.4 and can be customized using [dragHandleColor]. The default size is `Size(32,4)` and can be customized with [dragHandleSize].

If null, then the value of [BottomSheetThemeData.showDragHandle] is used. If that is also null, defaults to false.

If this is true, the [animationController] must not be null. Use [BottomSheet.createAnimationController] to create one, or provide another AnimationController.

### dragHandleColor

```dart
Color? dragHandleColor
```

The bottom sheet drag handle's color.

Defaults to [BottomSheetThemeData.dragHandleColor]. If that is also null, defaults to [ColorScheme.onSurfaceVariant].

### dragHandleSize

```dart
Size? dragHandleSize
```

Defaults to [BottomSheetThemeData.dragHandleSize]. If that is also null, defaults to Size(32, 4).

### onDragStart

```dart
BottomSheetDragStartHandler? onDragStart
```

Called when the user begins dragging the bottom sheet vertically, if [enableDrag] is true.

Would typically be used to change the bottom sheet animation curve so that it tracks the user's finger accurately.

### onDragEnd

```dart
BottomSheetDragEndHandler? onDragEnd
```

Called when the user stops dragging the bottom sheet, if [enableDrag] is true.

Would typically be used to reset the bottom sheet animation curve, so that it animates non-linearly. Called before [onClosing] if the bottom sheet is closing.

### backgroundColor

```dart
Color? backgroundColor
```

The bottom sheet's background color.

Defines the bottom sheet's [Material.color].

Defaults to null and falls back to [Material]'s default.

### shadowColor

```dart
Color? shadowColor
```

The color of the shadow below the sheet.

If this property is null, then [BottomSheetThemeData.shadowColor] of [ThemeData.bottomSheetTheme] is used. If that is also null, the default value is transparent.

See also:

- [elevation], which defines the size of the shadow below the sheet.
- [shape], which defines the shape of the sheet and its shadow.

### elevation

```dart
double? elevation
```

The z-coordinate at which to place this material relative to its parent.

This controls the size of the shadow below the material.

Defaults to 0. The value is non-negative.

### shape

```dart
ShapeBorder? shape
```

The shape of the bottom sheet.

Defines the bottom sheet's [Material.shape].

Defaults to null and falls back to [Material]'s default.

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defines the bottom sheet's [Material.clipBehavior].

Use this property to enable clipping of content when the bottom sheet has a custom [shape] and the content can extend past this shape. For example, a bottom sheet with rounded corners and an edge-to-edge [Image] at the top.

If this property is null then [BottomSheetThemeData.clipBehavior] of [ThemeData.bottomSheetTheme] is used. If that's null then the behavior will be [Clip.none].

### constraints

```dart
BoxConstraints? constraints
```

Defines minimum and maximum sizes for a [BottomSheet].

If null, then the ambient [ThemeData.bottomSheetTheme]'s [BottomSheetThemeData.constraints] will be used. If that is null and [ThemeData.useMaterial3] is true, then the bottom sheet will have a max width of 640dp. If [ThemeData.useMaterial3] is false, then the bottom sheet's size will be constrained by its parent (usually a [Scaffold]). In this case, consider limiting the width by setting smaller constraints for large screens.

If constraints are specified (either in this property or in the theme), the bottom sheet will be aligned to the bottom-center of the available space. Otherwise, no alignment is applied.

### createState()

```dart
State<BottomSheet> createState()
```

### createAnimationController()

```dart
AnimationController createAnimationController(TickerProvider vsync, {AnimationStyle? sheetAnimationStyle})
```

Creates an [AnimationController] suitable for a [BottomSheet.animationController].

This API is available as a convenience for a Material compliant bottom sheet animation. If alternative animation durations are required, a different animation controller could be provided.

# ModalBottomSheetRoute

```dart
class ModalBottomSheetRoute<T> extends PopupRoute<T> {}
```

A route that represents a Material Design modal bottom sheet.

{@template flutter.material.ModalBottomSheetRoute} A modal bottom sheet is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app.

A closely related widget is a persistent bottom sheet, which shows information that supplements the primary content of the app without preventing the user from interacting with the app. Persistent bottom sheets can be created and displayed with the [showBottomSheet] function or the [ScaffoldState.showBottomSheet] method.

The [isScrollControlled] parameter specifies whether this is a route for a bottom sheet that will utilize [DraggableScrollableSheet]. Consider setting this parameter to true if this bottom sheet has a scrollable child, such as a [ListView] or a [GridView], to have the bottom sheet be draggable.

The [isDismissible] parameter specifies whether the bottom sheet will be dismissed when user taps on the scrim.

The [enableDrag] parameter specifies whether the bottom sheet can be dragged up and down and dismissed by swiping downwards.

The [useSafeArea] parameter specifies whether the sheet will avoid system intrusions on the top, left, and right. If false, no [SafeArea] is added; and [MediaQuery.removePadding] is applied to the top, so that system intrusions at the top will not be avoided by a [SafeArea] inside the bottom sheet either. Defaults to false.

The optional [backgroundColor], [elevation], [shape], [clipBehavior], [constraints] and [transitionAnimationController] parameters can be passed in to customize the appearance and behavior of modal bottom sheets (see the documentation for these on [BottomSheet] for more details).

The [transitionAnimationController] controls the bottom sheet's entrance and exit animations. It's up to the owner of the controller to call [AnimationController.dispose] when the controller is no longer needed.

The optional `settings` parameter sets the [RouteSettings] of the modal bottom sheet sheet. This is particularly useful in the case that a user wants to observe [PopupRoute]s within a [NavigatorObserver]. {@endtemplate}

{@macro flutter.widgets.RawDialogRoute}

See also:

- [showModalBottomSheet], which is a way to display a ModalBottomSheetRoute.
- [BottomSheet], which becomes the parent of the widget returned by the function passed as the `builder` argument to [showModalBottomSheet].
- [showBottomSheet] and [ScaffoldState.showBottomSheet], for showing non-modal bottom sheets.
- [DraggableScrollableSheet], creates a bottom sheet that grows and then becomes scrollable once it reaches its maximum size.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- The Material 2 spec at <https://m2.material.io/components/sheets-bottom>.
- The Material 3 spec at <https://m3.material.io/components/bottom-sheets/overview>.

### ModalBottomSheetRoute()

```dart
ModalBottomSheetRoute({required WidgetBuilder builder, CapturedThemes? capturedThemes, String? barrierLabel, String? barrierOnTapHint, Color? backgroundColor, double? elevation, ShapeBorder? shape, Clip? clipBehavior, BoxConstraints? constraints, Color? modalBarrierColor, bool isDismissible = true, bool enableDrag = true, bool? showDragHandle, required bool isScrollControlled, double scrollControlDisabledMaxHeightRatio = _kDefaultScrollControlDisabledMaxHeightRatio, dynamic settings, dynamic requestFocus, AnimationController? transitionAnimationController, Offset? anchorPoint, bool useSafeArea = false, AnimationStyle? sheetAnimationStyle})
```

A modal bottom sheet route.

### builder

```dart
WidgetBuilder builder
```

A builder for the contents of the sheet.

The bottom sheet will wrap the widget produced by this builder in a [Material] widget.

### capturedThemes

```dart
CapturedThemes? capturedThemes
```

Stores a list of captured [InheritedTheme]s that are wrapped around the bottom sheet.

Consider setting this attribute when the [ModalBottomSheetRoute] is created through [Navigator.push] and its friends.

### isScrollControlled

```dart
bool isScrollControlled
```

Specifies whether this is a route for a bottom sheet that will utilize [DraggableScrollableSheet].

Consider setting this parameter to true if this bottom sheet has a scrollable child, such as a [ListView] or a [GridView], to have the bottom sheet be draggable.

### scrollControlDisabledMaxHeightRatio

```dart
double scrollControlDisabledMaxHeightRatio
```

The max height constraint ratio for the bottom sheet when [isScrollControlled] is set to false, no ratio will be applied when [isScrollControlled] is set to true.

Defaults to 9 / 16.

### backgroundColor

```dart
Color? backgroundColor
```

The bottom sheet's background color.

Defines the bottom sheet's [Material.color].

If this property is not provided, it falls back to [Material]'s default.

### elevation

```dart
double? elevation
```

The z-coordinate at which to place this material relative to its parent.

This controls the size of the shadow below the material.

Defaults to 0, must not be negative.

### shape

```dart
ShapeBorder? shape
```

The shape of the bottom sheet.

Defines the bottom sheet's [Material.shape].

If this property is not provided, it falls back to [Material]'s default.

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defines the bottom sheet's [Material.clipBehavior].

Use this property to enable clipping of content when the bottom sheet has a custom [shape] and the content can extend past this shape. For example, a bottom sheet with rounded corners and an edge-to-edge [Image] at the top.

If this property is null, the [BottomSheetThemeData.clipBehavior] of [ThemeData.bottomSheetTheme] is used. If that's null, the behavior defaults to [Clip.none] will be [Clip.none].

### constraints

```dart
BoxConstraints? constraints
```

Defines minimum and maximum sizes for a [BottomSheet].

If null, the ambient [ThemeData.bottomSheetTheme]'s [BottomSheetThemeData.constraints] will be used. If that is null and [ThemeData.useMaterial3] is true, then the bottom sheet will have a max width of 640dp. If [ThemeData.useMaterial3] is false, then the bottom sheet's size will be constrained by its parent (usually a [Scaffold]). In this case, consider limiting the width by setting smaller constraints for large screens.

If constraints are specified (either in this property or in the theme), the bottom sheet will be aligned to the bottom-center of the available space. Otherwise, no alignment is applied.

### modalBarrierColor

```dart
Color? modalBarrierColor
```

Specifies the color of the modal barrier that darkens everything below the bottom sheet.

Defaults to `Colors.black54` if not provided.

### isDismissible

```dart
bool isDismissible
```

Specifies whether the bottom sheet will be dismissed when user taps on the scrim.

If true, the bottom sheet will be dismissed when user taps on the scrim.

Defaults to true.

### enableDrag

```dart
bool enableDrag
```

Specifies whether the bottom sheet can be dragged up and down and dismissed by swiping downwards.

If true, the bottom sheet can be dragged up and down and dismissed by swiping downwards.

This applies to the content below the drag handle, if showDragHandle is true.

Defaults is true.

### showDragHandle

```dart
bool? showDragHandle
```

Specifies whether a drag handle is shown.

The drag handle appears at the top of the bottom sheet. The default color is [ColorScheme.onSurfaceVariant] with an opacity of 0.4 and can be customized using dragHandleColor. The default size is `Size(32,4)` and can be customized with dragHandleSize.

If null, then the value of [BottomSheetThemeData.showDragHandle] is used. If that is also null, defaults to false.

### transitionAnimationController

```dart
AnimationController? transitionAnimationController
```

The animation controller that controls the bottom sheet's entrance and exit animations.

The BottomSheet widget will manipulate the position of this animation, it is not just a passive observer.

### anchorPoint

```dart
Offset? anchorPoint
```

{@macro flutter.widgets.DisplayFeatureSubScreen.anchorPoint}

### useSafeArea

```dart
bool useSafeArea
```

Whether to avoid system intrusions on the top, left, and right.

If true, a [SafeArea] is inserted to keep the bottom sheet away from system intrusions at the top, left, and right sides of the screen.

If false, the bottom sheet will extend through any system intrusions at the top, left, and right.

If false, then moreover [MediaQuery.removePadding] will be used to remove top padding, so that a [SafeArea] widget inside the bottom sheet will have no effect at the top edge. If this is undesired, consider setting [useSafeArea] to true. Alternatively, wrap the [SafeArea] in a [MediaQuery] that restates an ambient [MediaQueryData] from outside [builder].

In either case, the bottom sheet extends all the way to the bottom of the screen, including any system intrusions.

The default is false.

### sheetAnimationStyle

```dart
AnimationStyle? sheetAnimationStyle
```

Used to override the modal bottom sheet animation duration and reverse animation duration.

If [AnimationStyle.duration] is provided, it will be used to override the modal bottom sheet animation duration in the underlying [BottomSheet.createAnimationController].

If [AnimationStyle.reverseDuration] is provided, it will be used to override the modal bottom sheet reverse animation duration in the underlying [BottomSheet.createAnimationController].

To disable the modal bottom sheet animation, use [AnimationStyle.noAnimation].

### barrierOnTapHint

```dart
String? barrierOnTapHint
```

{@template flutter.material.ModalBottomSheetRoute.barrierOnTapHint} The semantic hint text that informs users what will happen if they tap on the widget. Announced in the format of 'Double tap to ...'.

If the field is null, the default hint will be used, which results in announcement of 'Double tap to activate'. {@endtemplate}

See also:

- [barrierDismissible], which controls the behavior of the barrier when tapped.
- [ModalBarrier], which uses this field as onTapHint when it has an onTap action.

### dispose()

```dart
void dispose()
```

### transitionDuration

```dart
Duration get transitionDuration
```

### reverseTransitionDuration

```dart
Duration get reverseTransitionDuration
```

### barrierDismissible

```dart
bool get barrierDismissible
```

### barrierLabel

```dart
String? barrierLabel
```

### barrierColor

```dart
Color get barrierColor
```

### createAnimationController()

```dart
AnimationController createAnimationController()
```

### buildPage()

```dart
Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation)
```

### buildModalBarrier()

```dart
Widget buildModalBarrier()
```

# showModalBottomSheet()

```dart
Future<T?> showModalBottomSheet<T>({required BuildContext context, required WidgetBuilder builder, Color? backgroundColor, String? barrierLabel, double? elevation, ShapeBorder? shape, Clip? clipBehavior, BoxConstraints? constraints, Color? barrierColor, bool isScrollControlled = false, double scrollControlDisabledMaxHeightRatio = _kDefaultScrollControlDisabledMaxHeightRatio, bool useRootNavigator = false, bool isDismissible = true, bool enableDrag = true, bool? showDragHandle, bool useSafeArea = false, RouteSettings? routeSettings, AnimationController? transitionAnimationController, Offset? anchorPoint, AnimationStyle? sheetAnimationStyle, bool? requestFocus})
```

Shows a modal Material Design bottom sheet.

{@macro flutter.material.ModalBottomSheetRoute}

{@macro flutter.widgets.RawDialogRoute}

The `context` argument is used to look up the [Navigator] and [Theme] for the bottom sheet. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the bottom sheet is closed.

The `useRootNavigator` parameter ensures that the root navigator is used to display the [BottomSheet] when set to `true`. This is useful in the case that a modal [BottomSheet] needs to be displayed above all other content but the caller is inside another [Navigator].

Returns a `Future` that resolves to the value (if any) that was passed to [Navigator.pop] when the modal bottom sheet was closed.

The 'barrierLabel' parameter can be used to set a custom barrier label. Will default to [MaterialLocalizations.modalBarrierDismissLabel] of context if not set.

{@tool dartpad} This example demonstrates how to use [showModalBottomSheet] to display a bottom sheet that obscures the content behind it when a user taps a button. It also demonstrates how to close the bottom sheet using the [Navigator] when a user taps on a button inside the bottom sheet.

** See code in examples/api/lib/material/bottom_sheet/show_modal_bottom_sheet.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of [showModalBottomSheet], as described in: https://m3.material.io/components/bottom-sheets/overview

** See code in examples/api/lib/material/bottom_sheet/show_modal_bottom_sheet.1.dart ** {@end-tool}

The [sheetAnimationStyle] parameter is used to override the modal bottom sheet animation duration and reverse animation duration.

The [requestFocus] parameter is used to specify whether the bottom sheet should request focus when shown. {@macro flutter.widgets.navigator.Route.requestFocus}

If [AnimationStyle.duration] is provided, it will be used to override the modal bottom sheet animation duration in the underlying [BottomSheet.createAnimationController].

If [AnimationStyle.reverseDuration] is provided, it will be used to override the modal bottom sheet reverse animation duration in the underlying [BottomSheet.createAnimationController].

To disable the bottom sheet animation, use [AnimationStyle.noAnimation].

{@tool dartpad} This sample showcases how to override the [showModalBottomSheet] animation duration and reverse animation duration using [AnimationStyle].

** See code in examples/api/lib/material/bottom_sheet/show_modal_bottom_sheet.2.dart ** {@end-tool}

See also:

- [BottomSheet], which becomes the parent of the widget returned by the function passed as the `builder` argument to [showModalBottomSheet].
- [showBottomSheet] and [ScaffoldState.showBottomSheet], for showing non-modal bottom sheets.
- [DraggableScrollableSheet], creates a bottom sheet that grows and then becomes scrollable once it reaches its maximum size.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- The Material 2 spec at <https://m2.material.io/components/sheets-bottom>.
- The Material 3 spec at <https://m3.material.io/components/bottom-sheets/overview>.
- [AnimationStyle], which is used to override the modal bottom sheet animation duration and reverse animation duration.

# showBottomSheet()

```dart
PersistentBottomSheetController showBottomSheet({required BuildContext context, required WidgetBuilder builder, Color? backgroundColor, double? elevation, ShapeBorder? shape, Clip? clipBehavior, BoxConstraints? constraints, bool? enableDrag, bool? showDragHandle, AnimationController? transitionAnimationController, AnimationStyle? sheetAnimationStyle})
```

Shows a Material Design bottom sheet in the nearest [Scaffold] ancestor. To show a persistent bottom sheet, use the [Scaffold.bottomSheet].

Returns a controller that can be used to close and otherwise manipulate the bottom sheet.

The optional [backgroundColor], [elevation], [shape], [clipBehavior], [constraints] and [transitionAnimationController] parameters can be passed in to customize the appearance and behavior of persistent bottom sheets (see the documentation for these on [BottomSheet] for more details).

The [enableDrag] parameter specifies whether the bottom sheet can be dragged up and down and dismissed by swiping downwards.

The [sheetAnimationStyle] parameter is used to override the bottom sheet animation duration and reverse animation duration.

If [AnimationStyle.duration] is provided, it will be used to override the bottom sheet animation duration in the underlying [BottomSheet.createAnimationController].

If [AnimationStyle.reverseDuration] is provided, it will be used to override the bottom sheet reverse animation duration in the underlying [BottomSheet.createAnimationController].

To disable the bottom sheet animation, use [AnimationStyle.noAnimation].

{@tool dartpad} This sample showcases how to override the [showBottomSheet] animation duration and reverse animation duration using [AnimationStyle].

** See code in examples/api/lib/material/bottom_sheet/show_bottom_sheet.0.dart ** {@end-tool}

To rebuild the bottom sheet (e.g. if it is stateful), call [PersistentBottomSheetController.setState] on the controller returned by this method.

The new bottom sheet becomes a [LocalHistoryEntry] for the enclosing [ModalRoute] and a back button is added to the app bar of the [Scaffold] that closes the bottom sheet.

To create a persistent bottom sheet that is not a [LocalHistoryEntry] and does not add a back button to the enclosing Scaffold's app bar, use the [Scaffold.bottomSheet] constructor parameter.

A closely related widget is a modal bottom sheet, which is an alternative to a menu or a dialog and prevents the user from interacting with the rest of the app. Modal bottom sheets can be created and displayed with the [showModalBottomSheet] function.

The `context` argument is used to look up the [Scaffold] for the bottom sheet. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the bottom sheet is closed.

See also:

- [BottomSheet], which becomes the parent of the widget returned by the `builder`.
- [showModalBottomSheet], which can be used to display a modal bottom sheet.
- [Scaffold.of], for information about how to obtain the [BuildContext].
- The Material 2 spec at <https://m2.material.io/components/sheets-bottom>.
- The Material 3 spec at <https://m3.material.io/components/bottom-sheets/overview>.
- [AnimationStyle], which is used to override the bottom sheet animation duration and reverse animation duration.
