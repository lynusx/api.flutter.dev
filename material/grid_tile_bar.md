@docImport 'grid_tile.dart'; @docImport 'icon_button.dart';

# GridTileBar

```dart
class GridTileBar extends StatelessWidget {}
```

A header used in a Material Design [GridTile].

Typically used to add a one or two line header or footer on a [GridTile].

For a one-line header, include a [title] widget. To add a second line, also include a [subtitle] widget. Use [leading] or [trailing] to add an icon.

See also:

- [GridTile]
- <https://material.io/design/components/image-lists.html#anatomy>

### GridTileBar()

```dart
GridTileBar({dynamic key, Color? backgroundColor, Widget? leading, Widget? title, Widget? subtitle, Widget? trailing})
```

Creates a grid tile bar.

Typically used to with [GridTile].

### backgroundColor

```dart
Color? backgroundColor
```

The color to paint behind the child widgets.

Defaults to transparent.

### leading

```dart
Widget? leading
```

A widget to display before the title.

Typically an [Icon] or an [IconButton] widget.

### title

```dart
Widget? title
```

The primary content of the list item.

Typically a [Text] widget.

### subtitle

```dart
Widget? subtitle
```

Additional content displayed below the title.

Typically a [Text] widget.

### trailing

```dart
Widget? trailing
```

A widget to display after the title.

Typically an [Icon] or an [IconButton] widget.

### build()

```dart
Widget build(BuildContext context)
```
