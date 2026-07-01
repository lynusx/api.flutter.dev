# ShortcutSerialization

```dart
class ShortcutSerialization {}
```

A class used by [MenuSerializableShortcut] to describe the shortcut for serialization to send to the platform for rendering a [PlatformMenuBar].

See also:

- [PlatformMenuBar], a widget that defines a menu bar for the platform to render natively.
- [MenuSerializableShortcut], a mixin allowing a [ShortcutActivator] to provide data for serialization of the shortcut for sending to the platform.

### ShortcutSerialization.character()

```dart
ShortcutSerialization.character(String character, {bool alt = false, bool control = false, bool meta = false})
```

Creates a [ShortcutSerialization] representing a single character.

This is used by a [CharacterActivator] to serialize itself.

### ShortcutSerialization.modifier()

```dart
ShortcutSerialization.modifier(LogicalKeyboardKey trigger, {bool alt = false, bool control = false, bool meta = false, bool shift = false})
```

Creates a [ShortcutSerialization] representing a specific [LogicalKeyboardKey] and modifiers.

This is used by a [SingleActivator] to serialize itself.

### trigger

```dart
LogicalKeyboardKey? get trigger
```

The keyboard key that triggers this shortcut, if any.

### character

```dart
String? get character
```

The character that triggers this shortcut, if any.

### alt

```dart
bool? get alt
```

If this shortcut has a [trigger], this indicates whether or not the alt modifier needs to be down or not.

### control

```dart
bool? get control
```

If this shortcut has a [trigger], this indicates whether or not the control modifier needs to be down or not.

### meta

```dart
bool? get meta
```

If this shortcut has a [trigger], this indicates whether or not the meta (also known as the Windows or Command key) modifier needs to be down or not.

### shift

```dart
bool? get shift
```

If this shortcut has a [trigger], this indicates whether or not the shift modifier needs to be down or not.

### toChannelRepresentation()

```dart
Map<String, Object?> toChannelRepresentation()
```

Converts the internal representation to the format needed for a [PlatformMenuItem] to include it in its serialized form for sending to the platform.

# MenuSerializableShortcut

```dart
mixin MenuSerializableShortcut implements ShortcutActivator {}
```

A mixin allowing a [ShortcutActivator] to provide data for serialization of the shortcut when sending to the platform.

This is meant for those who have written their own [ShortcutActivator] subclass, and would like to have it work for menus in a [PlatformMenuBar] as well.

Keep in mind that there are limits to the capabilities of the platform APIs, and not all kinds of [ShortcutActivator]s will work with them.

See also:

- [SingleActivator], a [ShortcutActivator] which implements this mixin.
- [CharacterActivator], another [ShortcutActivator] which implements this mixin.

### serializeForMenu()

```dart
ShortcutSerialization serializeForMenu()
```

Implement this in a [ShortcutActivator] subclass to allow it to be serialized for use in a [PlatformMenuBar].

# PlatformMenuDelegate

```dart
abstract class PlatformMenuDelegate {}
```

An abstract delegate class that can be used to set [WidgetsBinding.platformMenuDelegate] to provide for managing platform menus.

This can be subclassed to provide a different menu plugin than the default system-provided plugin for managing [PlatformMenuBar] menus.

The [setMenus] method allows for setting of the menu hierarchy when the [PlatformMenuBar] menu hierarchy changes.

This delegate doesn't handle the results of clicking on a menu item, which is left to the implementor of subclasses of [PlatformMenuDelegate] to handle for their implementation.

This delegate typically knows how to serialize a [PlatformMenu] hierarchy, send it over a channel, and register for calls from the channel when a menu is invoked or a submenu is opened or closed.

See [DefaultPlatformMenuDelegate] for an example of implementing one of these.

See also:

- [PlatformMenuBar], the widget that adds a platform menu bar to an application, and uses [setMenus] to send the menus to the platform.
- [PlatformMenu], the class that describes a menu item with children that appear in a cascading menu.
- [PlatformMenuItem], the class that describes the leaves of a menu hierarchy.

### PlatformMenuDelegate()

```dart
PlatformMenuDelegate()
```

A const constructor so that subclasses can have const constructors.

### setMenus()

```dart
void setMenus(List<PlatformMenuItem> topLevelMenus)
```

Sets the entire menu hierarchy for a platform-rendered menu bar.

The `topLevelMenus` argument is the list of menus that appear in the menu bar, which themselves can have children.

To update the menu hierarchy or menu item state, call [setMenus] with the modified hierarchy, and it will overwrite the previous menu state.

See also:

- [PlatformMenuBar], the widget that adds a platform menu bar to an application.
- [PlatformMenu], the class that describes a menu item with children that appear in a cascading menu.
- [PlatformMenuItem], the class that describes the leaves of a menu hierarchy.

### clearMenus()

```dart
void clearMenus()
```

Clears any existing platform-rendered menus and leaves the application with no menus.

It is not necessary to call this before updating the menu with [setMenus].

### debugLockDelegate()

```dart
bool debugLockDelegate(BuildContext context)
```

This is called by [PlatformMenuBar] when it is initialized, to be sure that only one is active at a time.

The [debugLockDelegate] function should be called before the first call to [setMenus].

If the lock is successfully acquired, [debugLockDelegate] will return true.

If your implementation of a [PlatformMenuDelegate] can have only limited active instances, enforce it when you override this function.

See also:

- [debugUnlockDelegate], where the delegate is unlocked.

### debugUnlockDelegate()

```dart
bool debugUnlockDelegate(BuildContext context)
```

This is called by [PlatformMenuBar] when it is disposed, so that another one can take over.

If the [debugUnlockDelegate] successfully unlocks the delegate, it will return true.

See also:

- [debugLockDelegate], where the delegate is locked.

# MenuItemSerializableIdGenerator

```dart
typedef MenuItemSerializableIdGenerator = int Function(PlatformMenuItem item)
```

The signature for a function that generates unique menu item IDs for serialization of a [PlatformMenuItem].

# DefaultPlatformMenuDelegate

```dart
class DefaultPlatformMenuDelegate extends PlatformMenuDelegate {}
```

The platform menu delegate that handles the built-in macOS platform menu generation using the 'flutter/menu' channel.

An instance of this class is set on [WidgetsBinding.platformMenuDelegate] by default when the [WidgetsBinding] is initialized.

See also:

- [PlatformMenuBar], the widget that adds a platform menu bar to an application.
- [PlatformMenu], the class that describes a menu item with children that appear in a cascading menu.
- [PlatformMenuItem], the class that describes the leaves of a menu hierarchy.

### DefaultPlatformMenuDelegate()

```dart
DefaultPlatformMenuDelegate({MethodChannel? channel})
```

Creates a const [DefaultPlatformMenuDelegate].

The optional [channel] argument defines the channel used to communicate with the platform. It defaults to [SystemChannels.menu] if not supplied.

### clearMenus()

```dart
void clearMenus()
```

### setMenus()

```dart
void setMenus(List<PlatformMenuItem> topLevelMenus)
```

### channel

```dart
MethodChannel channel
```

Defines the channel that the [DefaultPlatformMenuDelegate] uses to communicate with the platform.

Defaults to [SystemChannels.menu].

### debugLockDelegate()

```dart
bool debugLockDelegate(BuildContext context)
```

### debugUnlockDelegate()

```dart
bool debugUnlockDelegate(BuildContext context)
```

# PlatformMenuBar

```dart
class PlatformMenuBar extends StatefulWidget with DiagnosticableTreeMixin {}
```

A menu bar that uses the platform's native APIs to construct and render a menu described by a [PlatformMenu]/[PlatformMenuItem] hierarchy.

This widget is especially useful on macOS, where a system menu is a required part of every application. Flutter only includes support for macOS out of the box, but support for other platforms may be provided via plugins that set [WidgetsBinding.platformMenuDelegate] in their initialization.

The [menus] member contains [PlatformMenuItem]s, which configure the properties of the menus on the platform menu bar.

As far as Flutter is concerned, this widget has no visual representation, and intercepts no events: it just returns the [child] from its build function. This is because all of the rendering, shortcuts, and event handling for the menu is handled by the plugin on the host platform. It is only part of the widget tree to provide a convenient refresh mechanism for the menu data.

There can only be one [PlatformMenuBar] at a time using the same [PlatformMenuDelegate]. It will assert if more than one is detected.

When calling [toStringDeep] on this widget, it will give a tree of [PlatformMenuItem]s, not a tree of widgets.

{@tool sample} This example shows a [PlatformMenuBar] that contains a single top level menu, containing three items for "About", a toggleable menu item for showing a message, a cascading submenu with message choices, and "Quit".

**This example will only work on macOS.**

** See code in examples/api/lib/material/platform_menu_bar/platform_menu_bar.0.dart ** {@end-tool}

The menus could just as effectively be managed without using the widget tree by using the following code, but mixing this usage with [PlatformMenuBar] is not recommended, since it will overwrite the menu configuration when it is rebuilt:

```dart
List<PlatformMenuItem> menus = <PlatformMenuItem>[ /* Define menus... */ ];
WidgetsBinding.instance.platformMenuDelegate.setMenus(menus);
```

### PlatformMenuBar()

```dart
PlatformMenuBar({dynamic key, required List<PlatformMenuItem> menus, Widget? child})
```

Creates a const [PlatformMenuBar].

The [child] and [menus] attributes are required.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### menus

```dart
List<PlatformMenuItem> menus
```

The list of menu items that are the top level children of the [PlatformMenuBar].

The [menus] member contains [PlatformMenuItem]s. They will not be part of the widget tree, since they are not widgets. They are provided to configure the properties of the menus on the platform menu bar.

Also, a Widget in Flutter is immutable, so directly modifying the [menus] with `List` APIs such as `somePlatformMenuBarWidget.menus.add(...)` will result in incorrect behaviors. Whenever the menus list is modified, a new list object should be provided.

### createState()

```dart
State<PlatformMenuBar> createState()
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# PlatformMenu

```dart
class PlatformMenu extends PlatformMenuItem with DiagnosticableTreeMixin {}
```

A class for representing menu items that have child submenus.

See also:

- [PlatformMenuItem], a class representing a leaf menu item in a [PlatformMenuBar].

### PlatformMenu()

```dart
PlatformMenu({required String label, String? tooltip, VoidCallback? onOpen, VoidCallback? onClose, required List<PlatformMenuItem> menus})
```

Creates a const [PlatformMenu].

The [label] and [menus] fields are required.

### onOpen

```dart
VoidCallback? onOpen
```

### onClose

```dart
VoidCallback? onClose
```

### menus

```dart
List<PlatformMenuItem> menus
```

The menu items in the submenu opened by this menu item.

If this is an empty list, this [PlatformMenu] will be disabled.

### descendants

```dart
List<PlatformMenuItem> get descendants
```

Returns all descendant [PlatformMenuItem]s of this item.

### getDescendants()

```dart
List<PlatformMenuItem> getDescendants(PlatformMenu item)
```

Returns all descendants of the given item.

This API is supplied so that implementers of [PlatformMenu] can share this implementation.

### toChannelRepresentation()

```dart
Iterable<Map<String, Object?>> toChannelRepresentation(PlatformMenuDelegate delegate, {required MenuItemSerializableIdGenerator getId})
```

### serialize()

```dart
Map<String, Object?> serialize(PlatformMenu item, PlatformMenuDelegate delegate, MenuItemSerializableIdGenerator getId)
```

Converts the supplied object to the correct channel representation for the 'flutter/menu' channel.

This API is supplied so that implementers of [PlatformMenu] can share this implementation.

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PlatformMenuItemGroup

```dart
class PlatformMenuItemGroup extends PlatformMenuItem {}
```

A class that groups other menu items into sections delineated by dividers.

Visual dividers will be added before and after this group if other menu items appear in the [PlatformMenu], and the leading one omitted if it is first and the trailing one omitted if it is last in the menu.

### PlatformMenuItemGroup()

```dart
PlatformMenuItemGroup({required List<PlatformMenuItem> members})
```

Creates a const [PlatformMenuItemGroup].

The [members] field is required.

### members

```dart
List<PlatformMenuItem> members
```

The [PlatformMenuItem]s that are members of this menu item group.

An assertion will be thrown if there isn't at least one member of the group.

### toChannelRepresentation()

```dart
Iterable<Map<String, Object?>> toChannelRepresentation(PlatformMenuDelegate delegate, {required MenuItemSerializableIdGenerator getId})
```

### serialize()

```dart
Iterable<Map<String, Object?>> serialize(PlatformMenuItem group, PlatformMenuDelegate delegate, {required MenuItemSerializableIdGenerator getId})
```

Converts the supplied object to the correct channel representation for the 'flutter/menu' channel.

This API is supplied so that implementers of [PlatformMenuItemGroup] can share this implementation.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PlatformMenuItem

```dart
class PlatformMenuItem with Diagnosticable {}
```

A class for [PlatformMenuItem]s that do not have submenus (as a [PlatformMenu] would), but can be selected.

These [PlatformMenuItem]s are the leaves of the menu item tree, and [onSelected] will be called when they are selected by clicking on them, or via an optional keyboard [shortcut].

See also:

- [PlatformMenu], a menu item that opens a submenu.

### PlatformMenuItem()

```dart
PlatformMenuItem({required String label, String? tooltip, MenuSerializableShortcut? shortcut, VoidCallback? onSelected, Intent? onSelectedIntent})
```

Creates a const [PlatformMenuItem].

The [label] attribute is required.

### label

```dart
String label
```

The required label used for rendering the menu item.

### tooltip

```dart
String? tooltip
```

The optional tooltip text.

This text is displayed when the user hovers over the menu item.

If null, no tooltip will be displayed.

### shortcut

```dart
MenuSerializableShortcut? shortcut
```

The optional shortcut that selects this [PlatformMenuItem].

This shortcut is only enabled when [onSelected] is set.

### onSelected

```dart
VoidCallback? onSelected
```

An optional callback that is called when this [PlatformMenuItem] is selected.

At most one of [onSelected] and [onSelectedIntent] may be set. If neither field is set, this menu item will be disabled.

### onOpen

```dart
VoidCallback? get onOpen
```

Returns a callback, if any, to be invoked if the platform menu receives a "Menu.opened" method call from the platform for this item.

Only items that have submenus will have this callback invoked.

The default implementation returns null.

### onClose

```dart
VoidCallback? get onClose
```

Returns a callback, if any, to be invoked if the platform menu receives a "Menu.closed" method call from the platform for this item.

Only items that have submenus will have this callback invoked.

The default implementation returns null.

### onSelectedIntent

```dart
Intent? onSelectedIntent
```

An optional intent that is invoked when this [PlatformMenuItem] is selected.

At most one of [onSelected] and [onSelectedIntent] may be set. If neither field is set, this menu item will be disabled.

### descendants

```dart
List<PlatformMenuItem> get descendants
```

Returns all descendant [PlatformMenuItem]s of this item.

Returns an empty list if this type of menu item doesn't have descendants.

### members

```dart
List<PlatformMenuItem> get members
```

Returns the list of group members if this menu item is a "grouping" menu item, such as [PlatformMenuItemGroup].

Defaults to an empty list.

### toChannelRepresentation()

```dart
Iterable<Map<String, Object?>> toChannelRepresentation(PlatformMenuDelegate delegate, {required MenuItemSerializableIdGenerator getId})
```

Converts the representation of this item into a map suitable for sending over the default "flutter/menu" channel used by [DefaultPlatformMenuDelegate].

The `delegate` is the [PlatformMenuDelegate] that is requesting the serialization.

The `getId` parameter is a [MenuItemSerializableIdGenerator] function that generates a unique ID for each menu item, which is to be returned in the "id" field of the menu item data.

### serialize()

```dart
Map<String, Object?> serialize(PlatformMenuItem item, PlatformMenuDelegate delegate, MenuItemSerializableIdGenerator getId)
```

Converts the given [PlatformMenuItem] into a data structure accepted by the 'flutter/menu' method channel method 'Menu.SetMenu'.

This API is supplied so that implementers of [PlatformMenuItem] can share this implementation.

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PlatformProvidedMenuItem

```dart
class PlatformProvidedMenuItem extends PlatformMenuItem {}
```

A class that represents a menu item that is provided by the platform.

This is used to add things like the "About" and "Quit" menu items to a platform menu.

The [type] enum determines which type of platform defined menu will be added.

This is most useful on a macOS platform where there are many different types of platform provided menu items in the standard menu setup.

In order to know if a [PlatformProvidedMenuItem] is available on a particular platform, call [PlatformProvidedMenuItem.hasMenu].

If the platform does not support the given [type], then the menu item will throw an [ArgumentError] when it is sent to the platform.

See also:

- [PlatformMenuBar] which takes these items for inclusion in a platform-rendered menu bar.

### PlatformProvidedMenuItem()

```dart
PlatformProvidedMenuItem({required PlatformProvidedMenuItemType type, bool enabled = true})
```

Creates a const [PlatformProvidedMenuItem] of the appropriate type. Throws if the platform doesn't support the given default menu type.

The [type] argument is required.

### type

```dart
PlatformProvidedMenuItemType type
```

The type of default menu this is.

See [PlatformProvidedMenuItemType] for the different types available. Not all of the types will be available on every platform. Use [hasMenu] to determine if the current platform has a given default menu item.

If the platform does not support the given [type], then the menu item will throw an [ArgumentError] in debug mode.

### enabled

```dart
bool enabled
```

True if this [PlatformProvidedMenuItem] should be enabled or not.

### hasMenu()

```dart
bool hasMenu(PlatformProvidedMenuItemType menu)
```

Checks to see if the given default menu type is supported on this platform.

### toChannelRepresentation()

```dart
Iterable<Map<String, Object?>> toChannelRepresentation(PlatformMenuDelegate delegate, {required MenuItemSerializableIdGenerator getId})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PlatformProvidedMenuItemType

```dart
enum PlatformProvidedMenuItemType {}
```

The list of possible platform provided, prebuilt menus for use in a [PlatformMenuBar].

These are menus that the platform typically provides that cannot be reproduced in Flutter without calling platform functions, but are standard on the platform.

Examples include things like the "Quit" or "Services" menu items on macOS. Not all platforms support all menu item types. Use [PlatformProvidedMenuItem.hasMenu] to know if a particular type is supported on a the current platform.

Add these to your [PlatformMenuBar] using the [PlatformProvidedMenuItem] class.

You can tell if the platform provides the given menu using the [PlatformProvidedMenuItem.hasMenu] method.

The system provided "About" menu item.

On macOS, this is the `orderFrontStandardAboutPanel` default menu.

The system provided "Quit" menu item.

On macOS, this is the `terminate` default menu.

This menu item will exit the application when activated.

The system provided "Services" submenu.

This submenu provides a list of system provided application services.

This default menu is only supported on macOS.

The system provided "Hide" menu item.

This menu item hides the application window.

On macOS, this is the `hide` default menu.

This default menu is only supported on macOS.

The system provided "Hide Others" menu item.

This menu item hides other application windows.

On macOS, this is the `hideOtherApplications` default menu.

This default menu is only supported on macOS.

The system provided "Show All" menu item.

This menu item shows all hidden application windows.

On macOS, this is the `unhideAllApplications` default menu.

This default menu is only supported on macOS.

The system provided "Start Dictation..." menu item.

This menu item tells the system to start the screen reader.

On macOS, this is the `startSpeaking` default menu.

This default menu is currently only supported on macOS.

The system provided "Stop Dictation..." menu item.

This menu item tells the system to stop the screen reader.

On macOS, this is the `stopSpeaking` default menu.

This default menu is currently only supported on macOS.

The system provided "Enter Full Screen" menu item.

This menu item tells the system to toggle full screen mode for the window.

On macOS, this is the `toggleFullScreen` default menu.

This default menu is currently only supported on macOS.

The system provided "Minimize" menu item.

This menu item tells the system to minimize the window.

On macOS, this is the `performMiniaturize` default menu.

This default menu is currently only supported on macOS.

The system provided "Zoom" menu item.

This menu item tells the system to expand the window size.

On macOS, this is the `performZoom` default menu.

This default menu is currently only supported on macOS.

The system provided "Bring To Front" menu item.

This menu item tells the system to stack the window above other windows.

On macOS, this is the `arrangeInFront` default menu.

This default menu is currently only supported on macOS.
