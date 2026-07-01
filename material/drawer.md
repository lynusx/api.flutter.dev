@docImport 'package:flutter/gestures.dart'; @docImport 'package:flutter/semantics.dart';

@docImport 'about.dart'; @docImport 'app_bar.dart'; @docImport 'color_scheme.dart'; @docImport 'drawer_header.dart'; @docImport 'icon_button.dart'; @docImport 'navigation_drawer.dart'; @docImport 'scaffold.dart';

# DrawerAlignment

```dart
enum DrawerAlignment {}
```

The possible alignments of a [Drawer].

Denotes that the [Drawer] is at the start side of the [Scaffold].

This corresponds to the left side when the text direction is left-to-right and the right side when the text direction is right-to-left.

Denotes that the [Drawer] is at the end side of the [Scaffold].

This corresponds to the right side when the text direction is left-to-right and the left side when the text direction is right-to-left.

# Drawer

```dart
class Drawer extends StatelessWidget {}
```

A Material Design panel that slides in horizontally from the edge of a [Scaffold] to show navigation links in an application.

There is a Material 3 version of this component, [NavigationDrawer], that's preferred for applications that are configured for Material 3 (see [ThemeData.useMaterial3]).

{@youtube 560 315 https://www.youtube.com/watch?v=WRj86iHihgY}

Drawers are typically used with the [Scaffold.drawer] property. The child of the drawer is usually a [ListView] whose first child is a [DrawerHeader] that displays status information about the current user. The remaining drawer children are often constructed with [ListTile]s, often concluding with an [AboutListTile].

The [AppBar] automatically displays an appropriate [IconButton] to show the [Drawer] when a [Drawer] is available in the [Scaffold]. The [Scaffold] automatically handles the edge-swipe gesture to show the drawer.

{@animation 350 622 https://flutter.github.io/assets-for-api-docs/assets/material/drawer.mp4}

## Updating to [NavigationDrawer]

There is a Material 3 version of this component, [NavigationDrawer], that's preferred for applications that are configured for Material 3 (see [ThemeData.useMaterial3]). The [NavigationDrawer] widget's visual are a little bit different, see the Material 3 spec at <https://m3.material.io/components/navigation-drawer/overview> for more details. While the [Drawer] widget can have only one child, the [NavigationDrawer] widget can have a list of widgets, which typically contains [NavigationDrawerDestination] widgets and/or customized widgets like headlines and dividers.

{@tool dartpad} This example shows how to create a [Scaffold] that contains an [AppBar] and a [Drawer]. A user taps the "menu" icon in the [AppBar] to open the [Drawer]. The [Drawer] displays four items: A header and three menu items. The [Drawer] displays the four items using a [ListView], which allows the user to scroll through the items if need be.

** See code in examples/api/lib/material/drawer/drawer.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to migrate the above [Drawer] to a [NavigationDrawer].

** See code in examples/api/lib/material/navigation_drawer/navigation_drawer.0.dart ** {@end-tool}

An open drawer may be closed with a swipe to close gesture, pressing the escape key, by tapping the scrim, or by calling pop route function such as [Navigator.pop]. For example a drawer item might close the drawer when tapped:

```dart
ListTile(
  leading: const Icon(Icons.change_history),
  title: const Text('Change history'),
  onTap: () {
    // change app state...
    Navigator.pop(context); // close the drawer
  },
);
```

See also:

- [Scaffold.drawer], where one specifies a [Drawer] so that it can be shown.
- [Scaffold.of], to obtain the current [ScaffoldState], which manages the display and animation of the drawer.
- [ScaffoldState.openDrawer], which displays its [Drawer], if any.
- <https://material.io/design/components/navigation-drawer.html>

### Drawer()

```dart
Drawer({dynamic key, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, double? width, Widget? child, String? semanticLabel, Clip? clipBehavior})
```

Creates a Material Design drawer.

Typically used in the [Scaffold.drawer] property.

The [elevation] must be non-negative.

### backgroundColor

```dart
Color? backgroundColor
```

Sets the color of the [Material] that holds all of the [Drawer]'s contents.

If this is null, then [DrawerThemeData.backgroundColor] is used. If that is also null, then it falls back to [Material]'s default.

### elevation

```dart
double? elevation
```

The z-coordinate at which to place this drawer relative to its parent.

This controls the size of the shadow below the drawer.

If this is null, then [DrawerThemeData.elevation] is used. If that is also null, then it defaults to 16.0.

### shadowColor

```dart
Color? shadowColor
```

The color used to paint a drop shadow under the drawer's [Material], which reflects the drawer's [elevation].

If null and [ThemeData.useMaterial3] is true then no drop shadow will be rendered.

If null and [ThemeData.useMaterial3] is false then it will default to [ThemeData.shadowColor].

See also:

- [Material.shadowColor], which describes how the drop shadow is painted.
- [elevation], which affects how the drop shadow is painted.
- [surfaceTintColor], which can be used to indicate elevation through tinting the background color.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The color used as a surface tint overlay on the drawer's background color, which reflects the drawer's [elevation].

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

To disable this feature, set [surfaceTintColor] to [Colors.transparent].

Defaults to [Colors.transparent].

See also:

- [Material.surfaceTintColor], which describes how the surface tint will be applied to the background color of the drawer.
- [elevation], which affects the opacity of the surface tint.
- [shadowColor], which can be used to indicate elevation through a drop shadow.

### shape

```dart
ShapeBorder? shape
```

The shape of the drawer.

Defines the drawer's [Material.shape].

If this is null, then [DrawerThemeData.shape] is used. If that is also null, then it falls back to [Material]'s default.

### width

```dart
double? width
```

The width of the drawer.

If this is null, then [DrawerThemeData.width] is used. If that is also null, then it falls back to the Material spec's default (304.0).

### child

```dart
Widget? child
```

The widget below this widget in the tree.

Typically a [ListView].

{@macro flutter.widgets.ProxyWidget.child}

### semanticLabel

```dart
String? semanticLabel
```

The semantic label of the drawer used by accessibility frameworks to announce screen transitions when the drawer is opened and closed.

If this label is not provided, it will default to [MaterialLocalizations.drawerLabel].

See also:

- [SemanticsConfiguration.namesRoute], for a description of how this value is used.

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

The [clipBehavior] argument specifies how to clip the drawer's [shape].

If the drawer has a [shape], it defaults to [Clip.hardEdge]. Otherwise, defaults to [Clip.none].

### build()

```dart
Widget build(BuildContext context)
```

# DrawerCallback

```dart
typedef DrawerCallback = void Function(bool isOpened)
```

Signature for the callback that's called when a [DrawerController] is opened or closed.

# DrawerController

```dart
class DrawerController extends StatefulWidget {}
```

Provides interactive behavior for [Drawer] widgets.

Rarely used directly. Drawer controllers are typically created automatically by [Scaffold] widgets.

The drawer controller provides the ability to open and close a drawer, either via an animation or via user interaction. When closed, the drawer collapses to a translucent gesture detector that can be used to listen for edge swipes.

See also:

- [Drawer], a container with the default width of a drawer.
- [Scaffold.drawer], the [Scaffold] slot for showing a drawer.

### DrawerController()

```dart
DrawerController({GlobalKey? key, required Widget child, required DrawerAlignment alignment, bool isDrawerOpen = false, DrawerCallback? drawerCallback, DragStartBehavior dragStartBehavior = DragStartBehavior.start, Color? scrimColor, double? edgeDragWidth, bool enableOpenDragGesture = true, bool drawerBarrierDismissible = true})
```

Creates a controller for a [Drawer].

Rarely used directly.

The [child] argument is typically a [Drawer].

### child

```dart
Widget child
```

The widget below this widget in the tree.

Typically a [Drawer].

### alignment

```dart
DrawerAlignment alignment
```

The alignment of the [Drawer].

This controls the direction in which the user should swipe to open and close the drawer.

### drawerCallback

```dart
DrawerCallback? drawerCallback
```

Optional callback that is called when a [Drawer] is opened or closed.

### drawerBarrierDismissible

```dart
bool drawerBarrierDismissible
```

Whether tapping the barrier behind the [Drawer] dismisses it.

Defaults to true.

If false, tapping the barrier will not dismiss the drawer.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@template flutter.material.DrawerController.dragStartBehavior} Determines the way that drag start behavior is handled.

If set to [DragStartBehavior.start], the drag behavior used for opening and closing a drawer will begin at the position where the drag gesture won the arena. If set to [DragStartBehavior.down] it will begin at the position where a down event is first detected.

In general, setting this to [DragStartBehavior.start] will make drag animation smoother and setting it to [DragStartBehavior.down] will make drag behavior feel slightly more reactive.

By default, the drag start behavior is [DragStartBehavior.start].

See also:

- [DragGestureRecognizer.dragStartBehavior], which gives an example for the different behaviors.

{@endtemplate}

### scrimColor

```dart
Color? scrimColor
```

The color to use for the scrim that obscures the underlying content while a drawer is open.

If this is null, then [DrawerThemeData.scrimColor] is used. If that is also null, then it defaults to [Colors.black54].

### enableOpenDragGesture

```dart
bool enableOpenDragGesture
```

Determines if the [Drawer] can be opened with a drag gesture.

By default, the drag gesture is enabled.

### edgeDragWidth

```dart
double? edgeDragWidth
```

The width of the area within which a horizontal swipe will open the drawer.

By default, the value used is 20.0 added to the padding edge of `MediaQuery.paddingOf(context)` that corresponds to [alignment]. This ensures that the drag area for notched devices is not obscured. For example, if [alignment] is set to [DrawerAlignment.start] and `TextDirection.of(context)` is set to [TextDirection.ltr], 20.0 will be added to `MediaQuery.paddingOf(context).left`.

### isDrawerOpen

```dart
bool isDrawerOpen
```

Whether or not the drawer is opened or closed.

This parameter is primarily used by the state restoration framework to restore the drawer's animation controller to the open or closed state depending on what was last saved to the target platform before the application was killed.

### maybeOf()

```dart
DrawerController? maybeOf(BuildContext context)
```

The closest instance of [DrawerController] that encloses the given context, or null if none is found.

{@tool snippet} Typical usage is as follows:

```dart
DrawerController? controller = DrawerController.maybeOf(context);
```

{@end-tool}

Calling this method will create a dependency on the closest [DrawerController] in the [context], if there is one.

See also:

- [DrawerController.of], which is similar to this method, but asserts if no [DrawerController] ancestor is found.

### of()

```dart
DrawerController of(BuildContext context)
```

The closest instance of [DrawerController] that encloses the given context.

If no instance is found, this method will assert in debug mode and throw an exception in release mode.

Calling this method will create a dependency on the closest [DrawerController] in the [context].

{@tool snippet} Typical usage is as follows:

```dart
DrawerController controller = DrawerController.of(context);
```

{@end-tool}

### createState()

```dart
DrawerControllerState createState()
```

# DrawerControllerState

```dart
class DrawerControllerState extends State<DrawerController> with SingleTickerProviderStateMixin {}
```

State for a [DrawerController].

Typically used by a [Scaffold] to [open] and [close] the drawer.

### initState()

```dart
void initState()
```

### dispose()

```dart
void dispose()
```

### didUpdateWidget()

```dart
void didUpdateWidget(DrawerController oldWidget)
```

### open()

```dart
void open()
```

Starts an animation to open the drawer.

Typically called by [ScaffoldState.openDrawer].

### close()

```dart
void close()
```

Starts an animation to close the drawer.

### build()

```dart
Widget build(BuildContext context)
```
