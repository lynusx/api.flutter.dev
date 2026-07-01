@docImport 'package:flutter/services.dart';

@docImport 'app_bar.dart'; @docImport 'drawer.dart'; @docImport 'material.dart';

# BackButtonIcon

```dart
class BackButtonIcon extends StatelessWidget {}
```

A "back" icon that's appropriate for the current [TargetPlatform].

The current platform is determined by querying for the ambient [Theme].

See also:

- [BackButton], an [IconButton] with a [BackButtonIcon] that calls [Navigator.maybePop] to return to the previous route.
- [IconButton], which is a more general widget for creating buttons with icons.
- [Icon], a Material Design icon.
- [ThemeData.platform], which specifies the current platform.

### BackButtonIcon()

```dart
BackButtonIcon({dynamic key})
```

Creates an icon that shows the appropriate "back" image for the current platform (as obtained from the [Theme]).

### build()

```dart
Widget build(BuildContext context)
```

# BackButton

```dart
class BackButton extends _ActionButton {}
```

A Material Design back icon button.

A [BackButton] is an [IconButton] with a "back" icon appropriate for the current [TargetPlatform]. When pressed, the back button calls [Navigator.maybePop] to return to the previous route unless a custom [onPressed] callback is provided.

The [onPressed] callback can, for instance, be used to pop the platform's navigation stack via [SystemNavigator] instead of Flutter's [Navigator] in add-to-app situations.

In Material Design 3, both [style]'s [ButtonStyle.iconColor] and [color] are used to override the default icon color of [BackButton]. If both exist, the [ButtonStyle.iconColor] will override [color] for states where [ButtonStyle.foregroundColor] resolves to non-null.

When deciding to display a [BackButton], consider using `ModalRoute.canPopOf(context)` to check whether the current route can be popped. If that value is false (e.g., because the current route is the initial route), the [BackButton] will not have any effect when pressed, which could frustrate the user.

Requires one of its ancestors to be a [Material] widget.

See also:

- [AppBar], which automatically uses a [BackButton] in its [AppBar.leading] slot when the [Scaffold] has no [Drawer] and the current [Route] is not the [Navigator]'s first route.
- [BackButtonIcon], which is useful if you need to create a back button that responds differently to being pressed.
- [IconButton], which is a more general widget for creating buttons with icons.
- [CloseButton], an alternative which may be more appropriate for leaf node pages in the navigation tree.

### BackButton()

```dart
BackButton({dynamic key, dynamic color, ButtonStyle? style, dynamic onPressed})
```

Creates an [IconButton] with the appropriate "back" icon for the current target platform.

# CloseButtonIcon

```dart
class CloseButtonIcon extends StatelessWidget {}
```

A "close" icon that's appropriate for the current [TargetPlatform].

The current platform is determined by querying for the ambient [Theme].

See also:

- [CloseButton], an [IconButton] with a [CloseButtonIcon] that calls [Navigator.maybePop] to return to the previous route.
- [IconButton], which is a more general widget for creating buttons with icons.
- [Icon], a Material Design icon.
- [ThemeData.platform], which specifies the current platform.

### CloseButtonIcon()

```dart
CloseButtonIcon({dynamic key})
```

Creates an icon that shows the appropriate "close" image for the current platform (as obtained from the [Theme]).

### build()

```dart
Widget build(BuildContext context)
```

# CloseButton

```dart
class CloseButton extends _ActionButton {}
```

A Material Design close icon button.

A [CloseButton] is an [IconButton] with a "close" icon. When pressed, the close button calls [Navigator.maybePop] to return to the previous route.

The [onPressed] callback can, for instance, be used to pop the platform's navigation stack via [SystemNavigator] instead of Flutter's [Navigator] in add-to-app situations.

In Material Design 3, both [style]'s [ButtonStyle.iconColor] and [color] are used to override the default icon color of [CloseButton]. If both exist, the [ButtonStyle.iconColor] will override [color] for states where [ButtonStyle.foregroundColor] resolves to non-null.

Use a [CloseButton] instead of a [BackButton] on fullscreen dialogs or pages that may solicit additional actions to close.

See also:

- [AppBar], which automatically uses a [CloseButton] in its [AppBar.leading] slot when appropriate.
- [BackButton], which is more appropriate for middle nodes in the navigation tree or where pages can be popped instantaneously with no user data consequence.
- [IconButton], to create other Material Design icon buttons.

### CloseButton()

```dart
CloseButton({dynamic key, dynamic color, dynamic onPressed, ButtonStyle? style})
```

Creates a Material Design close icon button.

# DrawerButtonIcon

```dart
class DrawerButtonIcon extends StatelessWidget {}
```

A "drawer" icon that's appropriate for the current [TargetPlatform].

The current platform is determined by querying for the ambient [Theme].

See also:

- [DrawerButton], an [IconButton] with a [DrawerButtonIcon] that calls [ScaffoldState.openDrawer] to open the [Scaffold.drawer].
- [EndDrawerButton], an [IconButton] with an [EndDrawerButtonIcon] that calls [ScaffoldState.openEndDrawer] to open the [Scaffold.endDrawer].
- [IconButton], which is a more general widget for creating buttons with icons.
- [Icon], a Material Design icon.
- [ThemeData.platform], which specifies the current platform.

### DrawerButtonIcon()

```dart
DrawerButtonIcon({dynamic key})
```

Creates an icon that shows the appropriate "close" image for the current platform (as obtained from the [Theme]).

### build()

```dart
Widget build(BuildContext context)
```

# DrawerButton

```dart
class DrawerButton extends _ActionButton {}
```

A Material Design drawer icon button.

A [DrawerButton] is an [IconButton] with a "drawer" icon. When pressed, the close button calls [ScaffoldState.openDrawer] to the [Scaffold.drawer].

The default behaviour on press can be overridden with [onPressed].

See also:

- [EndDrawerButton], an [IconButton] with an [EndDrawerButtonIcon] that calls [ScaffoldState.openEndDrawer] to open the [Scaffold.endDrawer].
- [IconButton], which is a more general widget for creating buttons with icons.
- [Icon], a Material Design icon.
- [ThemeData.platform], which specifies the current platform.

### DrawerButton()

```dart
DrawerButton({dynamic key, dynamic color, ButtonStyle? style, dynamic onPressed})
```

Creates a Material Design drawer icon button.

# EndDrawerButtonIcon

```dart
class EndDrawerButtonIcon extends StatelessWidget {}
```

A "end drawer" icon that's appropriate for the current [TargetPlatform].

The current platform is determined by querying for the ambient [Theme].

See also:

- [DrawerButton], an [IconButton] with a [DrawerButtonIcon] that calls [ScaffoldState.openDrawer] to open the [Scaffold.drawer].
- [EndDrawerButton], an [IconButton] with an [EndDrawerButtonIcon] that calls [ScaffoldState.openEndDrawer] to open the [Scaffold.endDrawer]
- [IconButton], which is a more general widget for creating buttons with icons.
- [Icon], a Material Design icon.
- [ThemeData.platform], which specifies the current platform.

### EndDrawerButtonIcon()

```dart
EndDrawerButtonIcon({dynamic key})
```

Creates an icon that shows the appropriate "end drawer" image for the current platform (as obtained from the [Theme]).

### build()

```dart
Widget build(BuildContext context)
```

# EndDrawerButton

```dart
class EndDrawerButton extends _ActionButton {}
```

A Material Design end drawer icon button.

A [EndDrawerButton] is an [IconButton] with a "drawer" icon. When pressed, the end drawer button calls [ScaffoldState.openEndDrawer] to open the [Scaffold.endDrawer].

The default behaviour on press can be overridden with [onPressed].

See also:

- [DrawerButton], an [IconButton] with a [DrawerButtonIcon] that calls [ScaffoldState.openDrawer] to open a drawer.
- [IconButton], which is a more general widget for creating buttons with icons.
- [Icon], a Material Design icon.
- [ThemeData.platform], which specifies the current platform.

### EndDrawerButton()

```dart
EndDrawerButton({dynamic key, dynamic color, ButtonStyle? style, dynamic onPressed})
```

Creates a Material Design end drawer icon button.
