@docImport 'package:flutter/services.dart';

# ContextMenuController

```dart
class ContextMenuController {}
```

Builds and manages a context menu at a given location.

There can only ever be one context menu shown at a given time in the entire app. Calling [show] on one instance of this class will hide any other shown instances.

{@tool dartpad} This example shows how to use a GestureDetector to show a context menu anywhere in a widget subtree that receives a right click or long press.

** See code in examples/api/lib/material/context_menu/context_menu_controller.0.dart ** {@end-tool}

See also:

- [BrowserContextMenu], which allows the browser's context menu on web to be disabled and Flutter-rendered context menus to appear.

### ContextMenuController()

```dart
ContextMenuController({VoidCallback? onRemove})
```

Creates a context menu that can be shown with [show].

### onRemove

```dart
VoidCallback? onRemove
```

Called when this menu is removed.

### show()

```dart
void show({required BuildContext context, required WidgetBuilder contextMenuBuilder, Widget? debugRequiredFor})
```

Shows the given context menu.

Since there can only be one shown context menu at a time, calling this will also remove any other context menu that is visible.

### removeAny()

```dart
void removeAny()
```

Remove the currently shown context menu from the UI.

Does nothing if no context menu is currently shown.

If a menu is removed, and that menu provided an [onRemove] callback when it was created, then that callback will be called.

See also:

- [remove], which removes only the current instance.

### isShown

```dart
bool get isShown
```

True if and only if this menu is currently being shown.

### markNeedsBuild()

```dart
void markNeedsBuild()
```

Cause the underlying [OverlayEntry] to rebuild during the next pipeline flush.

It's necessary to call this function if the output of `contextMenuBuilder` has changed.

Errors if the context menu is not currently shown.

See also:

- [OverlayEntry.markNeedsBuild]

### remove()

```dart
void remove()
```

Remove this menu from the UI.

Does nothing if this instance is not currently shown. In other words, if another context menu is currently shown, that menu will not be removed.

This method should only be called once. The instance cannot be shown again after removing. Create a new instance.

If an [onRemove] method was given to this instance, it will be called.

See also:

- [removeAny], which removes any shown instance of the context menu.
