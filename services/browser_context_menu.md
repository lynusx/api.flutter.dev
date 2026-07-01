# BrowserContextMenu

```dart
class BrowserContextMenu {}
```

Controls the browser's context menu on the web platform.

The context menu is the menu that appears on right clicking or selecting text in the browser, for example.

On web, by default, the browser's context menu is enabled and Flutter's context menus are hidden.

On all non-web platforms, this does nothing.

### enabled

```dart
bool get enabled
```

Whether showing the browser's context menu is enabled.

When true, any event that the browser typically uses to trigger its context menu (e.g. right click) will do so. When false, the browser's context menu will not show.

It's possible for this to be true but for the browser's context menu to not show due to direct manipulation of the DOM. For example, handlers for the browser's `contextmenu` event could be added/removed in the browser's JavaScript console, and this boolean wouldn't know about it. This boolean only indicates the results of calling [disableContextMenu] and [enableContextMenu] here.

Defaults to true.

### disableContextMenu()

```dart
Future<void> disableContextMenu()
```

Disable the browser's context menu.

By default, when the app starts, the browser's context menu is already enabled.

This is an asynchronous action. The context menu can be considered to be disabled at the time that the Future resolves. [enabled] won't reflect the change until that time.

See also:

- [enableContextMenu], which performs the opposite operation.

### enableContextMenu()

```dart
Future<void> enableContextMenu()
```

Enable the browser's context menu.

By default, when the app starts, the browser's context menu is already enabled. Typically this method would be called after first calling [disableContextMenu].

This is an asynchronous action. The context menu can be considered to be enabled at the time that the Future resolves. [enabled] won't reflect the change until that time.

See also:

- [disableContextMenu], which performs the opposite operation.
