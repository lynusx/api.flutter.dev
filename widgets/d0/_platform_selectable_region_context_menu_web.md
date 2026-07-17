# RegisterViewFactory

```dart
typedef RegisterViewFactory = void Function(String, Object Function(int viewId), {bool isVisible})
```

Function signature for `ui_web.platformViewRegistry.registerViewFactory`.

# PlatformSelectableRegionContextMenu

```dart
class PlatformSelectableRegionContextMenu extends StatelessWidget {}
```

See `_platform_selectable_region_context_menu_io.dart` for full documentation.

### PlatformSelectableRegionContextMenu()

```dart
PlatformSelectableRegionContextMenu({required Widget child, dynamic key})
```

See `_platform_selectable_region_context_menu_io.dart`.

### child

```dart
Widget child
```

See `_platform_selectable_region_context_menu_io.dart`.

### attach()

```dart
void attach(SelectionContainerDelegate client)
```

See `_platform_selectable_region_context_menu_io.dart`.

### detach()

```dart
void detach(SelectionContainerDelegate client)
```

See `_platform_selectable_region_context_menu_io.dart`.

### debugOverrideRegisterViewFactory

```dart
RegisterViewFactory? debugOverrideRegisterViewFactory
```

Override this to provide a custom implementation of [ui_web.platformViewRegistry.registerViewFactory].

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
