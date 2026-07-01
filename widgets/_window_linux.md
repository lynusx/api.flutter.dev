# WindowingOwnerLinux

```dart
class WindowingOwnerLinux extends WindowingOwner {}
```

[WindowingOwner] implementation for Linux.

If [Platform.isLinux] is false, then the constructor will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowingOwner], the abstract class that manages native windows.

### WindowingOwnerLinux()

```dart
WindowingOwnerLinux()
```

Creates a new [WindowingOwnerLinux] instance.

If [Platform.isLinux] is false, then this constructor will throw an [UnsupportedError]

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowingOwner], the abstract class that manages native windows.

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
SatelliteWindowController createSatelliteWindowController({required SatelliteWindowControllerDelegate delegate, required BaseWindowController parent, required WindowPositioner initialPositioner, Rect? initialAnchorRect, Size? preferredSize, BoxConstraints? preferredConstraints, bool resizable = false, String? title})
```

# WindowControllerLinux

```dart
abstract interface class WindowControllerLinux {}
```

Platform specific functionality for all window controllers on Linux.

{@macro flutter.widgets.windowing.experimental}

### windowHandle

```dart
ffi.Pointer<ffi.Void> get windowHandle
```

Returns pointer to the underlying [GtkWindow](https://docs.gtk.org/gtk3/class.Window.html).

Using this pointer implies the user is aware of any side effects changes may have to Flutter behavior.

The handle is only valid for the lifetime of the window. Once the window is destroyed, this handle becomes invalid and must not be used.

{@macro flutter.widgets.windowing.experimental}

### flutterViewHandle

```dart
ffi.Pointer<ffi.Void> get flutterViewHandle
```

Returns pointer to the [FlView](https://github.com/flutter/flutter/blob/main/engine/src/flutter/shell/platform/linux/public/flutter_linux/fl_view.h) that renders the Flutter content in this window.

Using this pointer implies the user is aware of any side effects changes may have to Flutter behavior.

The handle is only valid for the lifetime of the window. Once the window is destroyed, this handle becomes invalid and must not be used.

{@macro flutter.widgets.windowing.experimental}

# RegularWindowControllerLinux

```dart
class RegularWindowControllerLinux extends RegularWindowController implements WindowControllerLinux {}
```

Implementation of [RegularWindowController] for the Linux platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the base class for regular windows.

### RegularWindowControllerLinux()

```dart
RegularWindowControllerLinux({required WindowingOwnerLinux owner, required RegularWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, String? title, bool decorated = true})
```

Creates a new regular window controller for Linux.

When this constructor completes the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the base class for regular windows.

### contentSize

```dart
Size get contentSize
```

### destroy()

```dart
void destroy()
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
void setSize(Size size)
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
ffi.Pointer<ffi.Void> get windowHandle
```

### flutterViewHandle

```dart
ffi.Pointer<ffi.Void> get flutterViewHandle
```

# DialogWindowControllerLinux

```dart
class DialogWindowControllerLinux extends DialogWindowController implements WindowControllerLinux {}
```

Implementation of [DialogWindowController] for the Linux platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [DialogWindowController], the base class for dialog windows.

### DialogWindowControllerLinux()

```dart
DialogWindowControllerLinux({required WindowingOwnerLinux owner, required DialogWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, BaseWindowController? parent, String? title, bool decorated = true})
```

Creates a new dialog window controller for Linux.

When this constructor completes the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [DialogWindowController], the base class for dialog windows.

### contentSize

```dart
Size get contentSize
```

### destroy()

```dart
void destroy()
```

### parent

```dart
BaseWindowController? get parent
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
void setSize(Size size)
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

### windowHandle

```dart
ffi.Pointer<ffi.Void> get windowHandle
```

### flutterViewHandle

```dart
ffi.Pointer<ffi.Void> get flutterViewHandle
```

# TooltipWindowControllerLinux

```dart
class TooltipWindowControllerLinux extends TooltipWindowController implements WindowControllerLinux {}
```

Implementation of [TooltipWindowController] for the Linux platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [TooltipWindowController], the base class for tooltip windows.

### TooltipWindowControllerLinux()

```dart
TooltipWindowControllerLinux({required WindowingOwnerLinux owner, required TooltipWindowControllerDelegate delegate, required BoxConstraints preferredConstraints, required Rect anchorRect, required WindowPositioner positioner, required BaseWindowController parent})
```

Creates a new tooltip window controller for Linux.

When this constructor completes the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [TooltipWindowController], the base class for tooltip windows.

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

### parent

```dart
BaseWindowController get parent
```

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

### windowHandle

```dart
ffi.Pointer<ffi.Void> get windowHandle
```

### flutterViewHandle

```dart
ffi.Pointer<ffi.Void> get flutterViewHandle
```

# PopupWindowControllerLinux

```dart
class PopupWindowControllerLinux extends PopupWindowController {}
```

Implementation of [PopupWindowController] for the Linux platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [PopupWindowController], the base class for popup windows.

### PopupWindowControllerLinux()

```dart
PopupWindowControllerLinux({required WindowingOwnerLinux owner, required PopupWindowControllerDelegate delegate, required BoxConstraints preferredConstraints, required Rect anchorRect, required WindowPositioner positioner, required BaseWindowController parent})
```

Creates a new popup window controller for Linux.

When this constructor completes the native window has been created and has a view associated with it.

{@macro flutter.widgets.windowing.experimental}

See also:

- [PopupWindowController], the base class for popup windows.

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

### parent

```dart
BaseWindowController get parent
```

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```
