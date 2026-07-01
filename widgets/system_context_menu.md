@docImport 'package:flutter/material.dart';

# SystemContextMenu

```dart
class SystemContextMenu extends StatefulWidget {}
```

Displays the system context menu on top of the Flutter view.

Currently, only supports iOS 16.0 and above and displays nothing on other platforms.

The context menu is the menu that appears, for example, when doing text selection. Flutter typically draws this menu itself, but this class deals with the platform-rendered context menu instead.

There can only be one system context menu visible at a time. Building this widget when the system context menu is already visible will hide the old one and display this one. A system context menu that is hidden is informed via [onSystemHide].

Pass [items] to specify the buttons that will appear in the menu. Any items without a title will be given a default title from [WidgetsLocalizations].

By default, [items] will be set to the result of [getDefaultItems]. This method considers the state of the [EditableTextState] so that, for example, it will only include [IOSSystemContextMenuItemCopy] if there is currently a selection to copy.

To check if the current device supports showing the system context menu, call [isSupported].

{@tool dartpad} This example shows how to create a [TextField] that uses the system context menu where supported and does not show a system notification when the user presses the "Paste" button.

** See code in examples/api/lib/widgets/system_context_menu/system_context_menu.0.dart ** {@end-tool}

See also:

- [SystemContextMenuController], which directly controls the hiding and showing of the system context menu.

### SystemContextMenu.editableText()

```dart
SystemContextMenu.editableText({Key? key, required EditableTextState editableTextState, List<IOSSystemContextMenuItem>? items})
```

Creates an instance of [SystemContextMenu] for the field indicated by the given [EditableTextState].

### anchor

```dart
Rect anchor
```

The [Rect] that the context menu should point to.

### items

```dart
List<IOSSystemContextMenuItem> items
```

A list of the items to be displayed in the system context menu.

When passed, items will be shown regardless of the state of text input. For example, [IOSSystemContextMenuItemCopy] will produce a copy button even when there is no selection to copy. Use [EditableTextState] and/or the result of [getDefaultItems] to add and remove items based on the state of the input.

Defaults to the result of [getDefaultItems].

To add custom menu items, pass [IOSSystemContextMenuItemCustom] instances in the [items] list. Each custom item requires a title and an onPressed callback.

See also:

- [IOSSystemContextMenuItemCustom], which creates custom menu items.

### onSystemHide

```dart
VoidCallback? onSystemHide
```

Called when the system hides this context menu.

For example, tapping outside of the context menu typically causes the system to hide the menu.

This is not called when showing a new system context menu causes another to be hidden.

### isSupported()

```dart
bool isSupported(BuildContext context)
```

Whether the current device supports showing the system context menu.

Currently, this is only supported on newer versions of iOS.

See also:

- [isSupportedByField], which uses this method and determines whether an individual [EditableTextState] supports the system context menu.

### isSupportedByField()

```dart
bool isSupportedByField(EditableTextState editableTextState)
```

Whether the given field supports showing the system context menu.

Currently [SystemContextMenu] is only supported with an active [TextInputConnection]. In cases where this isn't possible, such as in a read-only field, fall back to using a Flutter-rendered context menu like [AdaptiveTextSelectionToolbar].

See also:

- [isSupported], which is used by this method and determines whether the platform in general supports showing the system context menu.

### getDefaultItems()

```dart
List<IOSSystemContextMenuItem> getDefaultItems(EditableTextState editableTextState)
```

The default [items] for the given [EditableTextState].

For example, [IOSSystemContextMenuItemCopy] will only be included when the field represented by the [EditableTextState] has a selection.

See also:

- [EditableTextState.contextMenuButtonItems], which provides the default [ContextMenuButtonItem]s for the Flutter-rendered context menu.

### createState()

```dart
State<SystemContextMenu> createState()
```

# IOSSystemContextMenuItem

```dart
sealed class IOSSystemContextMenuItem {}
```

Describes a context menu button that will be rendered in the iOS system context menu and not by Flutter itself.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemData], which performs a similar role but at the method channel level and mirrors the requirements of the method channel API.
- [ContextMenuButtonItem], which performs a similar role for Flutter-drawn context menus.

### IOSSystemContextMenuItem()

```dart
IOSSystemContextMenuItem()
```

### title

```dart
String? get title
```

The text to display to the user.

Not exposed for some built-in menu items whose title is always set by the platform.

### getData()

```dart
IOSSystemContextMenuItemData getData(WidgetsLocalizations localizations)
```

Returns the representation of this class used by method channels.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

# IOSSystemContextMenuItemCopy

```dart
final class IOSSystemContextMenuItemCopy extends IOSSystemContextMenuItem {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in copy button.

Should only appear when there is a selection that can be copied.

The title and action are both handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataCopy], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemCopy()

```dart
IOSSystemContextMenuItemCopy()
```

Creates an instance of [IOSSystemContextMenuItemCopy].

### getData()

```dart
IOSSystemContextMenuItemDataCopy getData(WidgetsLocalizations localizations)
```

# IOSSystemContextMenuItemCut

```dart
final class IOSSystemContextMenuItemCut extends IOSSystemContextMenuItem {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in cut button.

Should only appear when there is a selection that can be cut.

The title and action are both handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataCut], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemCut()

```dart
IOSSystemContextMenuItemCut()
```

Creates an instance of [IOSSystemContextMenuItemCut].

### getData()

```dart
IOSSystemContextMenuItemDataCut getData(WidgetsLocalizations localizations)
```

# IOSSystemContextMenuItemPaste

```dart
final class IOSSystemContextMenuItemPaste extends IOSSystemContextMenuItem {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in paste button.

Should only appear when the field can receive pasted content.

The title and action are both handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataPaste], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemPaste()

```dart
IOSSystemContextMenuItemPaste()
```

Creates an instance of [IOSSystemContextMenuItemPaste].

### getData()

```dart
IOSSystemContextMenuItemDataPaste getData(WidgetsLocalizations localizations)
```

# IOSSystemContextMenuItemSelectAll

```dart
final class IOSSystemContextMenuItemSelectAll extends IOSSystemContextMenuItem {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in select all button.

Should only appear when the field can have its selection changed.

The title and action are both handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataSelectAll], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemSelectAll()

```dart
IOSSystemContextMenuItemSelectAll()
```

Creates an instance of [IOSSystemContextMenuItemSelectAll].

### getData()

```dart
IOSSystemContextMenuItemDataSelectAll getData(WidgetsLocalizations localizations)
```

# IOSSystemContextMenuItemLookUp

```dart
final class IOSSystemContextMenuItemLookUp extends IOSSystemContextMenuItem with Diagnosticable {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in look up button.

Should only appear when content is selected.

The [title] is optional, but it must be specified before being sent to the platform. Typically it should be set to [WidgetsLocalizations.lookUpButtonLabel].

The action is handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataLookUp], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemLookUp()

```dart
IOSSystemContextMenuItemLookUp({String? title})
```

Creates an instance of [IOSSystemContextMenuItemLookUp].

### title

```dart
String? title
```

### getData()

```dart
IOSSystemContextMenuItemDataLookUp getData(WidgetsLocalizations localizations)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IOSSystemContextMenuItemSearchWeb

```dart
final class IOSSystemContextMenuItemSearchWeb extends IOSSystemContextMenuItem with Diagnosticable {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in search web button.

Should only appear when content is selected.

The [title] is optional, but it must be specified before being sent to the platform. Typically it should be set to [WidgetsLocalizations.searchWebButtonLabel].

The action is handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataSearchWeb], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemSearchWeb()

```dart
IOSSystemContextMenuItemSearchWeb({String? title})
```

Creates an instance of [IOSSystemContextMenuItemSearchWeb].

### title

```dart
String? title
```

### getData()

```dart
IOSSystemContextMenuItemDataSearchWeb getData(WidgetsLocalizations localizations)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IOSSystemContextMenuItemShare

```dart
final class IOSSystemContextMenuItemShare extends IOSSystemContextMenuItem with Diagnosticable {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in share button.

Opens the system share dialog.

Should only appear when shareable content is selected.

The [title] is optional, but it must be specified before being sent to the platform. Typically it should be set to [WidgetsLocalizations.shareButtonLabel].

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataShare], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemShare()

```dart
IOSSystemContextMenuItemShare({String? title})
```

Creates an instance of [IOSSystemContextMenuItemShare].

### title

```dart
String? title
```

### getData()

```dart
IOSSystemContextMenuItemDataShare getData(WidgetsLocalizations localizations)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IOSSystemContextMenuItemLiveText

```dart
final class IOSSystemContextMenuItemLiveText extends IOSSystemContextMenuItem {}
```

Creates an instance of [IOSSystemContextMenuItem] for the system's built-in Live Text button.

The title and action are both handled by the platform.

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataLiveText], which specifies the data to be sent to the platform for this same button.

### IOSSystemContextMenuItemLiveText()

```dart
IOSSystemContextMenuItemLiveText()
```

Creates an instance of [IOSSystemContextMenuItemLiveText].

### getData()

```dart
IOSSystemContextMenuItemData getData(WidgetsLocalizations localizations)
```

# IOSSystemContextMenuItemCustom

```dart
class IOSSystemContextMenuItemCustom extends IOSSystemContextMenuItem with Diagnosticable {}
```

Creates an instance of [IOSSystemContextMenuItem] for custom action buttons defined by the developer.

Only supported on iOS 16.0 and above.

The [title] and [onPressed] callback must be provided.

{@tool dartpad} This example shows how to add custom menu items to the iOS system context menu.

** See code in examples/api/lib/widgets/system_context_menu/system_context_menu.1.dart ** {@end-tool}

See also:

- [SystemContextMenu], a widget that can be used to display the system context menu.
- [IOSSystemContextMenuItemDataCustom], which specifies the data to be sent to the platform for this button.

### IOSSystemContextMenuItemCustom()

```dart
IOSSystemContextMenuItemCustom({required String title, required VoidCallback onPressed})
```

Creates an instance of [IOSSystemContextMenuItemCustom].

### title

```dart
String title
```

### onPressed

```dart
VoidCallback onPressed
```

The callback that is called when the button is pressed.

### getData()

```dart
IOSSystemContextMenuItemData getData(WidgetsLocalizations localizations)
```

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
