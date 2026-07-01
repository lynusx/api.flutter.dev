@docImport 'tab_scaffold.dart'; @docImport 'tab_view.dart';

# CupertinoTabBar

```dart
class CupertinoTabBar extends StatelessWidget implements PreferredSizeWidget {}
```

An iOS-styled bottom navigation tab bar.

Displays multiple tabs using [BottomNavigationBarItem] with one tab being active, the first tab by default.

This [StatelessWidget] doesn't store the active tab itself. You must listen to the [onTap] callbacks and call `setState` with a new [currentIndex] for the new selection to reflect. This can also be done automatically by wrapping this with a [CupertinoTabScaffold].

Tab changes typically trigger a switch between [Navigator]s, each with its own navigation stack, per standard iOS design. This can be done by using [CupertinoTabView]s inside each tab builder in [CupertinoTabScaffold].

If the given [backgroundColor]'s opacity is not 1.0 (which is the case by default), it will produce a blurring effect to the content behind it.

When used as [CupertinoTabScaffold.tabBar], by default [CupertinoTabBar] disables text scaling to match the native iOS behavior. To override this behavior, wrap each of the `navigationBar`'s components inside a [MediaQuery] with the desired [TextScaler].

{@tool dartpad} This example shows a [CupertinoTabBar] placed in a [CupertinoTabScaffold].

** See code in examples/api/lib/cupertino/bottom_tab_bar/cupertino_tab_bar.0.dart ** {@end-tool}

See also:

- [CupertinoTabScaffold], which hosts the [CupertinoTabBar] at the bottom.
- [BottomNavigationBarItem], an item in a [CupertinoTabBar].
- <https://developer.apple.com/design/human-interface-guidelines/ios/bars/tab-bars/>

### CupertinoTabBar()

```dart
CupertinoTabBar({dynamic key, required List<BottomNavigationBarItem> items, ValueChanged<int>? onTap, int currentIndex = 0, Color? backgroundColor, Color? activeColor, Color inactiveColor = _kDefaultTabBarInactiveColor, double iconSize = 30.0, double height = _kTabBarHeight, Border? border = const Border(top: BorderSide(color: _kDefaultTabBarBorderColor, width: 0.0))})
```

Creates a tab bar in the iOS style.

### items

```dart
List<BottomNavigationBarItem> items
```

The interactive items laid out within the bottom navigation bar.

### onTap

```dart
ValueChanged<int>? onTap
```

The callback that is called when a item is tapped.

The widget creating the bottom navigation bar needs to keep track of the current index and call `setState` to rebuild it with the newly provided index.

### currentIndex

```dart
int currentIndex
```

The index into [items] of the current active item.

Must be between 0 and the number of tabs minus 1, inclusive.

### backgroundColor

```dart
Color? backgroundColor
```

The background color of the tab bar. If it contains transparency, the tab bar will automatically produce a blurring effect to the content behind it.

Defaults to [CupertinoTheme]'s `barBackgroundColor` when null.

### activeColor

```dart
Color? activeColor
```

The foreground color of the icon and title for the [BottomNavigationBarItem] of the selected tab.

Defaults to [CupertinoTheme]'s `primaryColor` if null.

### inactiveColor

```dart
Color inactiveColor
```

The foreground color of the icon and title for the [BottomNavigationBarItem]s in the unselected state.

Defaults to a [CupertinoDynamicColor] that matches the disabled foreground color of the native `UITabBar` component.

### iconSize

```dart
double iconSize
```

The size of all of the [BottomNavigationBarItem] icons.

This value is used to configure the [IconTheme] for the navigation bar. When a [BottomNavigationBarItem.icon] widget is not an [Icon] the widget should configure itself to match the icon theme's size and color.

### height

```dart
double height
```

The height of the [CupertinoTabBar].

Defaults to 50.

### border

```dart
Border? border
```

The border of the [CupertinoTabBar].

The default value is a one physical pixel top border with grey color.

### preferredSize

```dart
Size get preferredSize
```

### opaque()

```dart
bool opaque(BuildContext context)
```

Indicates whether the tab bar is fully opaque or can have contents behind it show through it.

### build()

```dart
Widget build(BuildContext context)
```

### copyWith()

```dart
CupertinoTabBar copyWith({Key? key, List<BottomNavigationBarItem>? items, Color? backgroundColor, Color? activeColor, Color? inactiveColor, double? iconSize, double? height, Border? border, int? currentIndex, ValueChanged<int>? onTap})
```

Create a clone of the current [CupertinoTabBar] but with provided parameters overridden.
