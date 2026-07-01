@docImport 'button.dart'; @docImport 'nav_bar.dart'; @docImport 'route.dart'; @docImport 'tab_scaffold.dart';

# CupertinoPageScaffold

```dart
class CupertinoPageScaffold extends StatefulWidget {}
```

Implements a single iOS application page's layout.

The scaffold lays out the navigation bar on top and the content between or behind the navigation bar.

When tapping a status bar at the top of the CupertinoPageScaffold, an animation will complete for the current primary [ScrollView], scrolling to the beginning. This is done using the [PrimaryScrollController] that encloses the [ScrollView]. The [ScrollView.primary] flag is used to connect a [ScrollView] to the enclosing [PrimaryScrollController].

{@tool dartpad} This example shows a [CupertinoPageScaffold] with a [Center] as a [child]. The [CupertinoButton] is connected to a callback that increments a counter. The [backgroundColor] can be changed.

** See code in examples/api/lib/cupertino/page_scaffold/cupertino_page_scaffold.0.dart ** {@end-tool}

See also:

- [CupertinoTabScaffold], a similar widget for tabbed applications.
- [CupertinoPageRoute], a modal page route that typically hosts a [CupertinoPageScaffold] with support for iOS-style page transitions.

### CupertinoPageScaffold()

```dart
CupertinoPageScaffold({dynamic key, ObstructingPreferredSizeWidget? navigationBar, Color? backgroundColor, bool resizeToAvoidBottomInset = true, required Widget child})
```

Creates a layout for pages with a navigation bar at the top.

### navigationBar

```dart
ObstructingPreferredSizeWidget? navigationBar
```

The [navigationBar], typically a [CupertinoNavigationBar], is drawn at the top of the screen.

If translucent, the main content may slide behind it. Otherwise, the main content's top margin will be offset by its height.

The scaffold assumes the navigation bar will account for the [MediaQuery] top padding, also consume it if the navigation bar is opaque.

By default [navigationBar] disables text scaling to match the native iOS behavior. To override such behavior, wrap each of the [navigationBar]'s components inside a [MediaQuery] with the desired [TextScaler].

### child

```dart
Widget child
```

Widget to show in the main content area.

Content can slide under the [navigationBar] when they're translucent. In that case, the child's [BuildContext]'s [MediaQuery] will have a top padding indicating the area of obstructing overlap from the [navigationBar].

### backgroundColor

```dart
Color? backgroundColor
```

The color of the widget that underlies the entire scaffold.

By default uses [CupertinoTheme]'s `scaffoldBackgroundColor` when null.

### resizeToAvoidBottomInset

```dart
bool resizeToAvoidBottomInset
```

Whether the [child] should size itself to avoid the window's bottom inset.

For example, if there is an onscreen keyboard displayed above the scaffold, the body can be resized to avoid overlapping the keyboard, which prevents widgets inside the body from being obscured by the keyboard.

Defaults to true.

### createState()

```dart
State<CupertinoPageScaffold> createState()
```

# CupertinoPageScaffoldBackgroundColor

```dart
class CupertinoPageScaffoldBackgroundColor extends InheritedWidget {}
```

[InheritedWidget] indicating what the current scaffold background color is for its children.

This is used by the [CupertinoNavigationBar] and the [CupertinoSliverNavigationBar] widgets to paint themselves with the parent page scaffold color when no content is scrolled under.

### CupertinoPageScaffoldBackgroundColor()

```dart
CupertinoPageScaffoldBackgroundColor({required dynamic child, required Color color, dynamic key})
```

Constructs a new [CupertinoPageScaffoldBackgroundColor].

### color

```dart
Color color
```

The background color defined in [CupertinoPageScaffold].

### updateShouldNotify()

```dart
bool updateShouldNotify(CupertinoPageScaffoldBackgroundColor oldWidget)
```

### maybeOf()

```dart
Color? maybeOf(BuildContext context)
```

Retrieve the [CupertinoPageScaffold] background color from the context.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ObstructingPreferredSizeWidget

```dart
abstract class ObstructingPreferredSizeWidget implements PreferredSizeWidget {}
```

Widget that has a preferred size and reports whether it fully obstructs widgets behind it.

Used by [CupertinoPageScaffold] to either shift away fully obstructed content or provide a padding guide to partially obstructed content.

### shouldFullyObstruct()

```dart
bool shouldFullyObstruct(BuildContext context)
```

If true, this widget fully obstructs widgets behind it by the specified size.

If false, this widget partially obstructs.
