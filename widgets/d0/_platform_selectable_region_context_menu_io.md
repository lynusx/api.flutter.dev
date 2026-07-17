# RegisterViewFactory

```dart
typedef RegisterViewFactory = void Function(String, Object Function(int viewId), {bool isVisible})
```

Function signature for `ui_web.platformViewRegistry.registerViewFactory`.

# PlatformSelectableRegionContextMenu

```dart
class PlatformSelectableRegionContextMenu extends StatelessWidget {}
```

A widget that provides native selection context menu for its child subtree.

This widget currently only supports Flutter web. Using this widget in non-web platforms will throw [UnimplementedError]s.

In web platform, this widget registers a singleton platform view, i.e. a HTML DOM element. The created platform view will be shared between all [PlatformSelectableRegionContextMenu]s.

Only one [SelectionContainerDelegate] can attach to the [PlatformSelectableRegionContextMenu] at a time. Use [attach] method to make a [SelectionContainerDelegate] to be the active client.

### PlatformSelectableRegionContextMenu()

```dart
PlatformSelectableRegionContextMenu({required Widget child, dynamic key})
```

Creates a [PlatformSelectableRegionContextMenu]

### attach()

```dart
void attach(SelectionContainerDelegate client)
```

Attaches the `client` to be able to open platform-appropriate context menus.

### detach()

```dart
void detach(SelectionContainerDelegate client)
```

Detaches the `client` from the platform-appropriate selection context menus.

### debugOverrideRegisterViewFactory

```dart
RegisterViewFactory? debugOverrideRegisterViewFactory
```

Override this to provide a custom implementation of `ui_web.platformViewRegistry.registerViewFactory`.

This should only be used for testing.

### debugResetRegistry()

```dart
void debugResetRegistry()
```

Resets the view factory registration to its initial state.

### build()

```dart
Widget build(BuildContext context)
```
