@docImport 'package:flutter/material.dart';

@docImport 'list_section.dart';

# ExpansionTileTransitionMode

```dart
enum ExpansionTileTransitionMode {}
```

Defines how a [CupertinoExpansionTile] should transition its child between its collapsed state and its expanded state.

Transition by fading a fully extended [CupertinoExpansionTile.child].

When the [CupertinoExpansionTile] expands, the child appears fully extended and fades into view. When the [CupertinoExpansionTile] collapses, the child remains fully extended and fades out of view.

Transition by scrolling [CupertinoExpansionTile.child] under the header.

When the [CupertinoExpansionTile] expands, the child scrolls from under the header until it becomes fully extended. When the [CupertinoExpansionTile] collapses, the child scrolls under the header until it is fully collapsed.

# CupertinoExpansionTile

```dart
class CupertinoExpansionTile extends StatefulWidget {}
```

A single-line [CupertinoListTile] with an expansion arrow icon that expands or collapses the tile to reveal or hide the [child].

{@tool dartpad} This example shows how to use [CupertinoExpansionTile] with different transition modes.

** See code in examples/api/lib/cupertino/expansion_tile/cupertino_expansion_tile.0.dart ** {@end-tool}

See also:

- [ExpansionTile], the Material Design equivalent.
- [CupertinoListSection], useful for creating an expansion tile [child].
- [CupertinoListTile], the header of a [CupertinoExpansionTile].
- <https://developer.apple.com/design/human-interface-guidelines/disclosure-controls/>

### CupertinoExpansionTile()

```dart
CupertinoExpansionTile({dynamic key, required Widget title, required Widget child, ExpansibleController? controller, ExpansionTileTransitionMode transitionMode = ExpansionTileTransitionMode.fade})
```

Creates a single-line [CupertinoListTile] with an expansion arrow icon that expands or collapses the tile to reveal or hide the [child].

### title

```dart
Widget title
```

Used to convey the central information.

Usually a [Text].

### controller

```dart
ExpansibleController? controller
```

Programmatically expands and collapses the [CupertinoExpansionTile].

In cases where control over the tile's state is needed from a callback triggered by a widget within the tile, [ExpansibleController.of] may be more convenient than supplying a controller.

### child

```dart
Widget child
```

The body of the [CupertinoExpansionTile].

### transitionMode

```dart
ExpansionTileTransitionMode transitionMode
```

How the [CupertinoExpansionTile] should transition its child between its collapsed state and its expanded state.

Defaults to [ExpansionTileTransitionMode.fade].

### createState()

```dart
State<CupertinoExpansionTile> createState()
```
