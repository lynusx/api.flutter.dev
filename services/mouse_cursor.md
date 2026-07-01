@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart';

# MouseCursorManager

```dart
class MouseCursorManager {}
```

Maintains the state of mouse cursors and manages how cursors are searched for.

This is typically created as a global singleton and owned by [MouseTracker].

### MouseCursorManager()

```dart
MouseCursorManager(MouseCursor fallbackMouseCursor)
```

Create a [MouseCursorManager] by specifying the fallback cursor.

The `fallbackMouseCursor` must not be [MouseCursor.defer] (typically [SystemMouseCursors.basic]).

### fallbackMouseCursor

```dart
MouseCursor fallbackMouseCursor
```

The mouse cursor to use if all cursor candidates choose to defer.

See also:

- [MouseCursor.defer], the mouse cursor object to use to defer.

### debugDeviceActiveCursor()

```dart
MouseCursor? debugDeviceActiveCursor(int device)
```

Returns the active mouse cursor of a device.

The return value is the last [MouseCursor] activated onto this device, even if the activation failed.

Only valid when asserts are enabled. In release builds, always returns null.

### handleDeviceCursorUpdate()

```dart
void handleDeviceCursorUpdate(int device, PointerEvent? triggeringEvent, Iterable<MouseCursor> cursorCandidates)
```

Handles the changes that cause a pointer device to have a new list of mouse cursor candidates.

This change can be caused by a pointer event, in which case `triggeringEvent` should not be null, or by other changes, such as when a widget has moved under a still mouse, which is detected after the current frame is complete. In either case, `cursorCandidates` should be the list of cursors at the location of the mouse in hit-test order.

# MouseCursorSession

```dart
abstract class MouseCursorSession {}
```

Manages the duration that a pointing device should display a specific mouse cursor.

While [MouseCursor] classes describe the kind of cursors, [MouseCursorSession] classes represents a continuous use of the cursor on a pointing device. The [MouseCursorSession] classes can be stateful. For example, a cursor that needs to load resources might want to set a temporary cursor first, then switch to the correct cursor after the load is completed.

A [MouseCursorSession] has the following lifecycle:

- When a pointing device should start displaying a cursor, [MouseTracker] creates a session by calling [MouseCursor.createSession] on the target cursor, and stores it in a table associated with the device.
- [MouseTracker] then immediately calls the session's [activate], where the session should fetch resources and make system calls.
- When the pointing device should start displaying a different cursor, [MouseTracker] calls [dispose] on this session. After [dispose], this session will no longer be used in the future.

### MouseCursorSession()

```dart
MouseCursorSession(MouseCursor cursor, int device)
```

Create a session.

### cursor

```dart
MouseCursor cursor
```

The cursor that created this session.

### device

```dart
int device
```

The device ID of the pointing device.

### activate()

```dart
Future<void> activate()
```

Override this method to do the work of changing the cursor of the device.

Called right after this session is created.

This method has full control over the cursor until the [dispose] call, and can make system calls to change the pointer cursor as many times as necessary (usually through [SystemChannels.mouseCursor]). It can also collect resources, and store the result in this object.

### dispose()

```dart
void dispose()
```

Called when device stops displaying the cursor.

After this call, this session instance will no longer be used in the future.

When implementing this method in subclasses, you should release resources and prevent [activate] from causing side effects after disposal.

# MouseCursor

```dart
abstract class MouseCursor with Diagnosticable {}
```

An interface for mouse cursor definitions.

A mouse cursor is a graphical image on the screen that echoes the movement of a pointing device, such as a mouse or a stylus. A [MouseCursor] object defines a kind of mouse cursor, such as an arrow, a pointing hand, or an I-beam.

During the painting phase, [MouseCursor] objects are assigned to regions on the screen via annotations. Later during a device update (e.g. when a mouse moves), [MouseTracker] finds the _active cursor_ of each mouse device, which is the front-most region associated with the position of each mouse cursor, or defaults to [SystemMouseCursors.basic] if no cursors are associated with the position. [MouseTracker] changes the cursor of the pointer if the new active cursor is different from the previous active cursor, whose effect is defined by the session created by [createSession].

## Cursor classes

A [SystemMouseCursor] is a cursor that is natively supported by the platform that the program is running on. All supported system mouse cursors are enumerated in [SystemMouseCursors].

## Using cursors

A [MouseCursor] object is used by being assigned to a [MouseRegion] or another widget that exposes the [MouseRegion] API, such as [InkResponse.mouseCursor].

{@tool dartpad} This sample creates a rectangular region that is wrapped by a [MouseRegion] with a system mouse cursor. The mouse pointer becomes an I-beam when hovering over the region.

** See code in examples/api/lib/services/mouse_cursor/mouse_cursor.0.dart ** {@end-tool}

Assigning regions with mouse cursors on platforms that do not support mouse cursors, or when there are no mice connected, will have no effect.

## Related classes

[MouseCursorSession] represents the duration when a pointing device displays a cursor, and defines the states and behaviors of the cursor. Every mouse cursor class usually has a corresponding [MouseCursorSession] class.

[MouseCursorManager] is a class that adds the feature of changing cursors to [MouseTracker], which tracks the relationship between mouse devices and annotations. [MouseCursorManager] is usually used as a part of [MouseTracker].

### MouseCursor()

```dart
MouseCursor()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### createSession()

```dart
MouseCursorSession createSession(int device)
```

Associate a pointing device to this cursor.

A mouse cursor class usually has a corresponding [MouseCursorSession] class, and instantiates such class in this method.

This method is called each time a pointing device starts displaying this cursor. A given cursor can be displayed by multiple devices at the same time, in which case this method will be called separately for each device.

### debugDescription

```dart
String get debugDescription
```

A very short description of the mouse cursor.

The [debugDescription] should be a few words that can describe this cursor to make debug information more readable. It is returned as the [toString] when the diagnostic level is at or above [DiagnosticLevel.info].

The [debugDescription] must not be empty.

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### defer

```dart
MouseCursor defer
```

A special class that indicates that the region with this cursor defers the choice of cursor to the next region behind it.

When an event occurs, [MouseTracker] will update each pointer's cursor by finding the list of regions that contain the pointer's location, from front to back in hit-test order. The pointer's cursor will be the first cursor in the list that is not a [MouseCursor.defer].

### uncontrolled

```dart
MouseCursor uncontrolled
```

A special value that doesn't change cursor by itself, but make a region that blocks other regions behind it from changing the cursor.

When a pointer enters a region with a cursor of [uncontrolled], the pointer retains its previous cursor and keeps so until it moves out of the region. Technically, this region absorb the mouse cursor hit test without changing the pointer's cursor.

This is useful in a region that displays a platform view, which let the operating system handle pointer events and change cursors accordingly. To achieve this, the region's cursor must not be any Flutter cursor, since that might overwrite the system request upon pointer entering; the cursor must not be null either, since that allows the widgets behind the region to change cursors.

# SystemMouseCursor

```dart
class SystemMouseCursor extends MouseCursor {}
```

A mouse cursor that is natively supported on the platform that the application is running on.

System cursors can be used without external resources, and their appearances match the experience of native apps. Examples of system cursors are a pointing arrow, a pointing hand, a double arrow for resizing, or a text I-beam, etc.

An instance of [SystemMouseCursor] refers to one cursor from each platform that represents the same concept, such as being text, being clickable, or being a forbidden operation. Since the set of system cursors supported by each platform varies, multiple instances can correspond to the same system cursor.

Each cursor is noted with its corresponding native cursors on each platform:

- Android: API name in Java
- Web: CSS cursor
- Windows: Win32 API
- Windows UWP: WinRT API, `winrt::Windows::UI::Core::CoreCursorType`
- Linux: GDK, `gdk_cursor_new_from_name`
- macOS: API name in Objective C

If the platform that the application is running on is not listed for a cursor, using this cursor falls back to [SystemMouseCursors.basic].

[SystemMouseCursors] enumerates the complete set of system cursors supported by Flutter, which are hard-coded in the engine. Therefore, manually instantiating this class is not supported.

### kind

```dart
String kind
```

A string that identifies the kind of the cursor.

The interpretation of [kind] is platform-dependent.

### debugDescription

```dart
String get debugDescription
```

### createSession()

```dart
MouseCursorSession createSession(int device)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SystemMouseCursors

```dart
abstract final class SystemMouseCursors {}
```

A collection of system [MouseCursor]s.

System cursors are standard mouse cursors that are provided by the current platform. They don't require external resources.

[SystemMouseCursors] is a superset of the system cursors of every platform that Flutter supports, therefore some of these objects might map to the same result, or fallback to the [basic] arrow. This mapping is defined by the Flutter engine.

The cursors should be named based on the cursors' use cases instead of their appearance, because different platforms might (although not commonly) use different shapes for the same use case.

### none

```dart
SystemMouseCursor none
```

Hide the cursor.

Any cursor other than [none] or [MouseCursor.uncontrolled] unhides the cursor.

### basic

```dart
SystemMouseCursor basic
```

The platform-dependent basic cursor.

Typically the shape of an arrow.

Corresponds to:

- Android: TYPE_DEFAULT, TYPE_ARROW
- Web: default
- Windows: IDC_ARROW
- Windows UWP: CoreCursorType::Arrow
- Linux: default
- macOS: arrowCursor

### click

```dart
SystemMouseCursor click
```

A cursor that emphasizes an element being clickable, such as a hyperlink.

Typically the shape of a pointing hand.

Corresponds to:

- Android: TYPE_HAND
- Web: pointer
- Windows: IDC_HAND
- Windows UWP: CoreCursorType::Hand
- Linux: pointer
- macOS: pointingHandCursor

### forbidden

```dart
SystemMouseCursor forbidden
```

A cursor indicating an operation that will not be carried out.

Typically the shape of a circle with a diagonal line. May fall back to [noDrop].

Corresponds to:

- Android: TYPE_NO_DROP
- Web: not-allowed
- Windows: IDC_NO
- Windows UWP: CoreCursorType::UniversalNo
- Linux: not-allowed
- macOS: operationNotAllowedCursor

See also:

- [noDrop], which indicates somewhere that the current item may not be dropped.

### wait

```dart
SystemMouseCursor wait
```

A cursor indicating the status that the program is busy and therefore can not be interacted with.

Typically the shape of an hourglass or a watch.

This cursor is not available as a system cursor on macOS. Although macOS displays a "spinning ball" cursor when busy, it's handled by the OS and not exposed for applications to choose.

Corresponds to:

- Android: TYPE_WAIT
- Windows: IDC_WAIT
- Web: wait
- Linux: wait

See also:

- [progress], which is similar to [wait] but the program can still be interacted with.

### progress

```dart
SystemMouseCursor progress
```

A cursor indicating the status that the program is busy but can still be interacted with.

Typically the shape of an arrow with an hourglass or a watch at the corner. Does _not_ fall back to [wait] if unavailable.

Corresponds to:

- Web: progress
- Windows: IDC_APPSTARTING
- Linux: progress

See also:

- [wait], which is similar to [progress] but the program can not be interacted with.

### contextMenu

```dart
SystemMouseCursor contextMenu
```

A cursor indicating somewhere the user can trigger a context menu.

Typically the shape of an arrow with a small menu at the corner.

Corresponds to:

- Android: TYPE_CONTEXT_MENU
- Web: context-menu
- Linux: context-menu
- macOS: contextualMenuCursor

### help

```dart
SystemMouseCursor help
```

A cursor indicating help information.

Typically the shape of a question mark, or an arrow therewith.

Corresponds to:

- Android: TYPE_HELP
- Windows: IDC_HELP
- Windows UWP: CoreCursorType::Help
- Web: help
- Linux: help

### text

```dart
SystemMouseCursor text
```

A cursor indicating selectable text.

Typically the shape of a capital I.

Corresponds to:

- Android: TYPE_TEXT
- Web: text
- Windows: IDC_IBEAM
- Windows UWP: CoreCursorType::IBeam
- Linux: text
- macOS: IBeamCursor

### verticalText

```dart
SystemMouseCursor verticalText
```

A cursor indicating selectable vertical text.

Typically the shape of a capital I rotated to be horizontal. May fall back to [text].

Corresponds to:

- Android: TYPE_VERTICAL_TEXT
- Web: vertical-text
- Linux: vertical-text
- macOS: IBeamCursorForVerticalLayout

### cell

```dart
SystemMouseCursor cell
```

A cursor indicating selectable table cells.

Typically the shape of a hollow plus sign.

Corresponds to:

- Android: TYPE_CELL
- Web: cell
- Linux: cell

### precise

```dart
SystemMouseCursor precise
```

A cursor indicating precise selection, such as selecting a pixel in a bitmap.

Typically the shape of a crosshair.

Corresponds to:

- Android: TYPE_CROSSHAIR
- Web: crosshair
- Windows: IDC_CROSS
- Windows UWP: CoreCursorType::Cross
- Linux: crosshair
- macOS: crosshairCursor

### move

```dart
SystemMouseCursor move
```

A cursor indicating moving something.

Typically the shape of four-way arrow. May fall back to [allScroll].

Corresponds to:

- Android: TYPE_ALL_SCROLL
- Windows: IDC_SIZEALL
- Windows UWP: CoreCursorType::SizeAll
- Web: move
- Linux: move

### grab

```dart
SystemMouseCursor grab
```

A cursor indicating something that can be dragged.

Typically the shape of an open hand.

Corresponds to:

- Android: TYPE_GRAB
- Web: grab
- Linux: grab
- macOS: openHandCursor

### grabbing

```dart
SystemMouseCursor grabbing
```

A cursor indicating something that is being dragged.

Typically the shape of a closed hand.

Corresponds to:

- Android: TYPE_GRABBING
- Web: grabbing
- Linux: grabbing
- macOS: closedHandCursor

### noDrop

```dart
SystemMouseCursor noDrop
```

A cursor indicating somewhere that the current item may not be dropped.

Typically the shape of a hand with a [forbidden] sign at the corner. May fall back to [forbidden].

Corresponds to:

- Android: TYPE_NO_DROP
- Web: no-drop
- Windows: IDC_NO
- Windows UWP: CoreCursorType::UniversalNo
- Linux: no-drop
- macOS: operationNotAllowedCursor

See also:

- [forbidden], which indicates an action that will not be carried out.

### alias

```dart
SystemMouseCursor alias
```

A cursor indicating that the current operation will create an alias of, or a shortcut of the item.

Typically the shape of an arrow with a shortcut icon at the corner.

Corresponds to:

- Android: TYPE_ALIAS
- Web: alias
- Linux: alias
- macOS: dragLinkCursor

### copy

```dart
SystemMouseCursor copy
```

A cursor indicating that the current operation will copy the item.

Typically the shape of an arrow with a boxed plus sign at the corner.

Corresponds to:

- Android: TYPE_COPY
- Web: copy
- Linux: copy
- macOS: dragCopyCursor

### disappearing

```dart
SystemMouseCursor disappearing
```

A cursor indicating that the current operation will result in the disappearance of the item.

Typically the shape of an arrow with a cloud of smoke at the corner.

Corresponds to:

- macOS: disappearingItemCursor

### allScroll

```dart
SystemMouseCursor allScroll
```

A cursor indicating scrolling in any direction.

Typically the shape of a dot surrounded by 4 arrows.

Corresponds to:

- Android: TYPE_ALL_SCROLL
- Windows: IDC_SIZEALL
- Windows UWP: CoreCursorType::SizeAll
- Web: all-scroll
- Linux: all-scroll

See also:

- [move], which indicates moving in any direction.

### resizeLeftRight

```dart
SystemMouseCursor resizeLeftRight
```

A cursor indicating resizing an object bidirectionally from its left or right edge.

Typically the shape of a bidirectional arrow pointing left and right.

Corresponds to:

- Android: TYPE_HORIZONTAL_DOUBLE_ARROW
- Web: ew-resize
- Windows: IDC_SIZEWE
- Windows UWP: CoreCursorType::SizeWestEast
- Linux: ew-resize
- macOS: resizeLeftRightCursor

### resizeUpDown

```dart
SystemMouseCursor resizeUpDown
```

A cursor indicating resizing an object bidirectionally from its top or bottom edge.

Typically the shape of a bidirectional arrow pointing up and down.

Corresponds to:

- Android: TYPE_VERTICAL_DOUBLE_ARROW
- Web: ns-resize
- Windows: IDC_SIZENS
- Windows UWP: CoreCursorType::SizeNorthSouth
- Linux: ns-resize
- macOS: resizeUpDownCursor

### resizeUpLeftDownRight

```dart
SystemMouseCursor resizeUpLeftDownRight
```

A cursor indicating resizing an object bidirectionally from its top left or bottom right corner.

Typically the shape of a bidirectional arrow pointing upper left and lower right.

Corresponds to:

- Android: TYPE_TOP_LEFT_DIAGONAL_DOUBLE_ARROW
- Web: nwse-resize
- Windows: IDC_SIZENWSE
- Windows UWP: CoreCursorType::SizeNorthwestSoutheast
- Linux: nwse-resize

### resizeUpRightDownLeft

```dart
SystemMouseCursor resizeUpRightDownLeft
```

A cursor indicating resizing an object bidirectionally from its top right or bottom left corner.

Typically the shape of a bidirectional arrow pointing upper right and lower left.

Corresponds to:

- Android: TYPE_TOP_RIGHT_DIAGONAL_DOUBLE_ARROW
- Windows: IDC_SIZENESW
- Windows UWP: CoreCursorType::SizeNortheastSouthwest
- Web: nesw-resize
- Linux: nesw-resize

### resizeUp

```dart
SystemMouseCursor resizeUp
```

A cursor indicating resizing an object from its top edge.

Typically the shape of an arrow pointing up. May fallback to [resizeUpDown].

Corresponds to:

- Android: TYPE_VERTICAL_DOUBLE_ARROW
- Web: n-resize
- Windows: IDC_SIZENS
- Windows UWP: CoreCursorType::SizeNorthSouth
- Linux: n-resize
- macOS: resizeUpCursor

### resizeDown

```dart
SystemMouseCursor resizeDown
```

A cursor indicating resizing an object from its bottom edge.

Typically the shape of an arrow pointing down. May fallback to [resizeUpDown].

Corresponds to:

- Android: TYPE_VERTICAL_DOUBLE_ARROW
- Web: s-resize
- Windows: IDC_SIZENS
- Windows UWP: CoreCursorType::SizeNorthSouth
- Linux: s-resize
- macOS: resizeDownCursor

### resizeLeft

```dart
SystemMouseCursor resizeLeft
```

A cursor indicating resizing an object from its left edge.

Typically the shape of an arrow pointing left. May fallback to [resizeLeftRight].

Corresponds to:

- Android: TYPE_HORIZONTAL_DOUBLE_ARROW
- Web: w-resize
- Windows: IDC_SIZEWE
- Windows UWP: CoreCursorType::SizeWestEast
- Linux: w-resize
- macOS: resizeLeftCursor

### resizeRight

```dart
SystemMouseCursor resizeRight
```

A cursor indicating resizing an object from its right edge.

Typically the shape of an arrow pointing right. May fallback to [resizeLeftRight].

Corresponds to:

- Android: TYPE_HORIZONTAL_DOUBLE_ARROW
- Web: e-resize
- Windows: IDC_SIZEWE
- Windows UWP: CoreCursorType::SizeWestEast
- Linux: e-resize
- macOS: resizeRightCursor

### resizeUpLeft

```dart
SystemMouseCursor resizeUpLeft
```

A cursor indicating resizing an object from its top-left corner.

Typically the shape of an arrow pointing upper left. May fallback to [resizeUpLeftDownRight].

Corresponds to:

- Android: TYPE_TOP_LEFT_DIAGONAL_DOUBLE_ARROW
- Web: nw-resize
- Windows: IDC_SIZENWSE
- Windows UWP: CoreCursorType::SizeNorthwestSoutheast
- Linux: nw-resize

### resizeUpRight

```dart
SystemMouseCursor resizeUpRight
```

A cursor indicating resizing an object from its top-right corner.

Typically the shape of an arrow pointing upper right. May fallback to [resizeUpRightDownLeft].

Corresponds to:

- Android: TYPE_TOP_RIGHT_DIAGONAL_DOUBLE_ARROW
- Web: ne-resize
- Windows: IDC_SIZENESW
- Windows UWP: CoreCursorType::SizeNortheastSouthwest
- Linux: ne-resize

### resizeDownLeft

```dart
SystemMouseCursor resizeDownLeft
```

A cursor indicating resizing an object from its bottom-left corner.

Typically the shape of an arrow pointing lower left. May fallback to [resizeUpRightDownLeft].

Corresponds to:

- Android: TYPE_TOP_RIGHT_DIAGONAL_DOUBLE_ARROW
- Web: sw-resize
- Windows: IDC_SIZENESW
- Windows UWP: CoreCursorType::SizeNortheastSouthwest
- Linux: sw-resize

### resizeDownRight

```dart
SystemMouseCursor resizeDownRight
```

A cursor indicating resizing an object from its bottom-right corner.

Typically the shape of an arrow pointing lower right. May fallback to [resizeUpLeftDownRight].

Corresponds to:

- Android: TYPE_TOP_LEFT_DIAGONAL_DOUBLE_ARROW
- Web: se-resize
- Windows: IDC_SIZENWSE
- Windows UWP: CoreCursorType::SizeNorthwestSoutheast
- Linux: se-resize

### resizeColumn

```dart
SystemMouseCursor resizeColumn
```

A cursor indicating resizing a column, or an item horizontally.

Typically the shape of arrows pointing left and right with a vertical bar separating them. May fallback to [resizeLeftRight].

Corresponds to:

- Android: TYPE_HORIZONTAL_DOUBLE_ARROW
- Web: col-resize
- Windows: IDC_SIZEWE
- Windows UWP: CoreCursorType::SizeWestEast
- Linux: col-resize
- macOS: resizeLeftRightCursor

### resizeRow

```dart
SystemMouseCursor resizeRow
```

A cursor indicating resizing a row, or an item vertically.

Typically the shape of arrows pointing up and down with a horizontal bar separating them. May fallback to [resizeUpDown].

Corresponds to:

- Android: TYPE_VERTICAL_DOUBLE_ARROW
- Web: row-resize
- Windows: IDC_SIZENS
- Windows UWP: CoreCursorType::SizeNorthSouth
- Linux: row-resize
- macOS: resizeUpDownCursor

### zoomIn

```dart
SystemMouseCursor zoomIn
```

A cursor indicating zooming in.

Typically a magnifying glass with a plus sign.

Corresponds to:

- Android: TYPE_ZOOM_IN
- Web: zoom-in
- Linux: zoom-in

### zoomOut

```dart
SystemMouseCursor zoomOut
```

A cursor indicating zooming out.

Typically a magnifying glass with a minus sign.

Corresponds to:

- Android: TYPE_ZOOM_OUT
- Web: zoom-out
- Linux: zoom-out
