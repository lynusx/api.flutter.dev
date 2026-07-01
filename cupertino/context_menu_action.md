# CupertinoContextMenuAction

```dart
class CupertinoContextMenuAction extends StatefulWidget {}
```

A button in a _ContextMenuSheet.

A typical use case is to pass a [Text] as the [child] here, but be sure to use [TextOverflow.ellipsis] for the [Text.overflow] field if the text may be long, as without it the text will wrap to the next line.

### CupertinoContextMenuAction()

```dart
CupertinoContextMenuAction({dynamic key, required Widget child, bool isDefaultAction = false, bool isDestructiveAction = false, VoidCallback? onPressed, IconData? trailingIcon})
```

Construct a CupertinoContextMenuAction.

### child

```dart
Widget child
```

The widget that will be placed inside the action.

### isDefaultAction

```dart
bool isDefaultAction
```

Indicates whether this action should receive the style of an emphasized, default action.

### isDestructiveAction

```dart
bool isDestructiveAction
```

Indicates whether this action should receive the style of a destructive action.

### onPressed

```dart
VoidCallback? onPressed
```

Called when the action is pressed.

### trailingIcon

```dart
IconData? trailingIcon
```

An optional icon to display to the right of the child.

Will be colored in the same way as the [TextStyle] used for [child] (for example, if using [isDestructiveAction]).

### createState()

```dart
State<CupertinoContextMenuAction> createState()
```
