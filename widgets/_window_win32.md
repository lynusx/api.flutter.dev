# HWND

```dart
typedef HWND = ffi.Pointer<ffi.Void>
```

A Win32 window handle.

{@macro flutter.widgets.windowing.experimental}

# WindowingOwnerWin32

```dart
class WindowingOwnerWin32 extends WindowingOwner {}
```

[WindowingOwner] implementation for Windows.

If [Platform.isWindows] is false, then the constructor will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowingOwner], the abstract class that manages native windows.

### WindowingOwnerWin32()

```dart
WindowingOwnerWin32()
```

Creates a new [WindowingOwnerWin32] instance.

If [Platform.isWindows] is false, then this constructor will throw an [UnsupportedError]

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowingOwner], the abstract class that manages native windows.

### allocator

```dart
ffi.Allocator allocator
```

The [Allocator] used for allocating native memory in this owner.

This can be overridden via the [WindowingOwnerWin32.test] constructor.

{@macro flutter.widgets.windowing.experimental}

### createRegularWindowController()

```dart
RegularWindowController createRegularWindowController({Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, String? title, required RegularWindowControllerDelegate delegate})
```

### createDialogWindowController()

```dart
DialogWindowController createDialogWindowController({required DialogWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, BaseWindowController? parent, String? title})
```

### createTooltipWindowController()

```dart
TooltipWindowController createTooltipWindowController({required TooltipWindowControllerDelegate delegate, required BoxConstraints preferredConstraints, required Rect anchorRect, required WindowPositioner positioner, required BaseWindowController parent})
```

### createPopupWindowController()

```dart
PopupWindowController createPopupWindowController({required PopupWindowControllerDelegate delegate, required BoxConstraints preferredConstraints, required Rect anchorRect, required WindowPositioner positioner, required BaseWindowController parent})
```

### createSatelliteWindowController()

```dart
SatelliteWindowController createSatelliteWindowController({required SatelliteWindowControllerDelegate delegate, required BaseWindowController parent, required WindowPositioner initialPositioner, Rect? initialAnchorRect, Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, String? title})
```

# WindowControllerWin32

```dart
abstract mixin class WindowControllerWin32 {}
```

Platform specific functionality for all window controllers on Windows.

{@macro flutter.widgets.windowing.experimental}

### windowHandle

```dart
HWND get windowHandle
```

Returns the underlying HWND for this window.

Using this handle implies the user is aware of any side effects changes may have to Flutter behavior.

The handle is only valid for the lifetime of the window. Once the window is destroyed, this handle becomes invalid and must not be used.

{@macro flutter.widgets.windowing.experimental}

# RegularWindowControllerWin32

```dart
class RegularWindowControllerWin32 extends RegularWindowController with WindowControllerWin32 {}
```

Implementation of [RegularWindowController] for the Windows platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the base class for regular windows.

### RegularWindowControllerWin32()

```dart
RegularWindowControllerWin32({required WindowingOwnerWin32 owner, required RegularWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, String? title, required bool resizable})
```

Creates a new regular window controller for Win32.

When this constructor completes the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the base class for regular windows.

### contentSize

```dart
Size get contentSize
```

### title

```dart
String get title
```

### isActivated

```dart
bool get isActivated
```

### isMaximized

```dart
bool get isMaximized
```

### isMinimized

```dart
bool get isMinimized
```

### isFullscreen

```dart
bool get isFullscreen
```

### setSize()

```dart
void setSize(Size? size)
```

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

### setTitle()

```dart
void setTitle(String title)
```

### activate()

```dart
void activate()
```

### setMaximized()

```dart
void setMaximized(bool maximized)
```

### setMinimized()

```dart
void setMinimized(bool minimized)
```

### setFullscreen()

```dart
void setFullscreen(bool fullscreen, {Display? display})
```

### windowHandle

```dart
HWND get windowHandle
```

Returns HWND pointer to the top level window.

### destroy()

```dart
void destroy()
```

# DialogWindowControllerWin32

```dart
class DialogWindowControllerWin32 extends DialogWindowController with WindowControllerWin32 {}
```

Implementation of [DialogWindowController] for the Windows platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [DialogWindowController], the base class for dialog windows.

### DialogWindowControllerWin32()

```dart
DialogWindowControllerWin32({required WindowingOwnerWin32 owner, required DialogWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, String? title, BaseWindowController? parent, required bool resizable})
```

Creates a new dialog window controller for Win32.

When this constructor completes the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [DialogWindowController], the base class for dialog windows.

### contentSize

```dart
Size get contentSize
```

### title

```dart
String get title
```

### isActivated

```dart
bool get isActivated
```

### isMinimized

```dart
bool get isMinimized
```

### setSize()

```dart
void setSize(Size? size)
```

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

### setTitle()

```dart
void setTitle(String title)
```

### activate()

```dart
void activate()
```

### setMinimized()

```dart
void setMinimized(bool minimized)
```

### parent

```dart
BaseWindowController? get parent
```

### windowHandle

```dart
HWND get windowHandle
```

Returns HWND pointer to the top level window.

### destroy()

```dart
void destroy()
```

# TooltipWindowControllerWin32

```dart
class TooltipWindowControllerWin32 extends TooltipWindowController with WindowControllerWin32 implements _WindowsMessageHandler {}
```

Implementation of [TooltipWindowController] for the Windows platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [TooltipWindowController], the base class for tooltip windows.

### TooltipWindowControllerWin32()

```dart
TooltipWindowControllerWin32({required WindowingOwnerWin32 owner, required TooltipWindowControllerDelegate delegate, required BoxConstraints contentSizeConstraints, required BaseWindowController parent, required Rect anchorRect, required WindowPositioner positioner})
```

Creates a new tooltip window controller for Win32.

When this constructor completes, the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [TooltipWindowController], the base class for tooltip windows.

### windowHandle

```dart
HWND get windowHandle
```

Returns HWND pointer to the top level window.

### contentSize

```dart
Size get contentSize
```

### destroy()

```dart
void destroy()
```

### updatePosition()

```dart
void updatePosition({Rect? anchorRect, WindowPositioner? positioner})
```

### handleWindowsMessage()

```dart
int? handleWindowsMessage(FlutterView view, HWND windowHandle, int message, int wParam, int lParam)
```

### parent

```dart
BaseWindowController get parent
```

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

# PopupWindowControllerWin32

```dart
class PopupWindowControllerWin32 extends PopupWindowController implements _WindowsMessageHandler {}
```

Implementation of [PopupWindowController] for the Windows platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [PopupWindowController], the base class for popup windows.

### PopupWindowControllerWin32()

```dart
PopupWindowControllerWin32({required WindowingOwnerWin32 owner, required PopupWindowControllerDelegate delegate, required BoxConstraints contentSizeConstraints, required BaseWindowController parent, required Rect anchorRect, required WindowPositioner positioner})
```

Creates a new popup window controller for Win32.

When this constructor completes, the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [PopupWindowController], the base class for popup windows.

### getWindowHandle()

```dart
HWND getWindowHandle()
```

Returns HWND pointer to the top level window.

### contentSize

```dart
Size get contentSize
```

### destroy()

```dart
void destroy()
```

### updatePosition()

```dart
void updatePosition({Rect? anchorRect, WindowPositioner? positioner})
```

### offsetFromParent

```dart
Offset get offsetFromParent
```

### handleWindowsMessage()

```dart
int? handleWindowsMessage(FlutterView view, HWND windowHandle, int message, int wParam, int lParam)
```

### parent

```dart
BaseWindowController get parent
```

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

### activate()

```dart
void activate()
```

### isActivated

```dart
bool get isActivated
```
