@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# NavigationToolbar

```dart
class NavigationToolbar extends StatelessWidget {}
```

[NavigationToolbar] is a layout helper to position 3 widgets or groups of widgets along a horizontal axis that's sensible for an application's navigation bar such as in Material Design and in iOS.

The [leading] and [trailing] widgets occupy the edges of the widget with reasonable size constraints while the [middle] widget occupies the remaining space in either a center aligned or start aligned fashion.

Either directly use the themed app bars such as the Material [AppBar] or the iOS [CupertinoNavigationBar] or wrap this widget with more theming specifications for your own custom app bar.

### NavigationToolbar()

```dart
NavigationToolbar({dynamic key, Widget? leading, Widget? middle, Widget? trailing, bool centerMiddle = true, double middleSpacing = kMiddleSpacing})
```

Creates a widget that lays out its children in a manner suitable for a toolbar.

### kMiddleSpacing

```dart
double kMiddleSpacing
```

The default spacing around the [middle] widget in dp.

### leading

```dart
Widget? leading
```

Widget to place at the start of the horizontal toolbar.

### middle

```dart
Widget? middle
```

Widget to place in the middle of the horizontal toolbar, occupying as much remaining space as possible.

### trailing

```dart
Widget? trailing
```

Widget to place at the end of the horizontal toolbar.

### centerMiddle

```dart
bool centerMiddle
```

Whether to align the [middle] widget to the center of this widget or next to the [leading] widget when false.

### middleSpacing

```dart
double middleSpacing
```

The spacing around the [middle] widget on horizontal axis.

Defaults to [kMiddleSpacing].

### build()

```dart
Widget build(BuildContext context)
```
