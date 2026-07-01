# WindowingOwnerMacOS

```dart
class WindowingOwnerMacOS extends WindowingOwner {}
```

[WindowingOwner] implementation for macOS.

If [Platform.isMacOS] is false, then the constructor will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowingOwner], the abstract class that manages native windows.

### WindowingOwnerMacOS()

```dart
WindowingOwnerMacOS()
```

Creates a new [WindowingOwnerMacOS] instance.

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowingOwner], the abstract class that manages native windows.

### createRegularWindowController()

```dart
RegularWindowController createRegularWindowController({required RegularWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, String? title})
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

### getWindowHandle()

```dart
Pointer<Void> getWindowHandle(FlutterView view)
```

Returns the window handle for the given [view], or null is the window handle is not available.

The window handle is a pointer to the NSWindow instance.

### createSatelliteWindowController()

```dart
SatelliteWindowController createSatelliteWindowController({required SatelliteWindowControllerDelegate delegate, required BaseWindowController parent, required WindowPositioner initialPositioner, Rect? initialAnchorRect, Size? preferredSize, BoxConstraints? preferredConstraints, bool resizable = false, String? title})
```

# WindowControllerMacOS

```dart
abstract interface class WindowControllerMacOS {}
```

Platform specific functionality for all window controllers on macOS.

{@macro flutter.widgets.windowing.experimental}

### windowHandle

```dart
Pointer<Void> get windowHandle
```

Returns pointer to the underlying NSWindow.

Using this pointer implies the user is aware of any side effects changes may have to Flutter behavior.

The handle is only valid for the lifetime of the window. Once the window is destroyed, this handle becomes invalid and must not be used.

{@macro flutter.widgets.windowing.experimental}

# TooltipWindowControllerMacOS

```dart
class TooltipWindowControllerMacOS extends TooltipWindowController with _WindowControllerMixin {}
```

MacOS specific implementation of [TooltipWindowController].

{@macro flutter.widgets.windowing.experimental}

### TooltipWindowControllerMacOS()

```dart
TooltipWindowControllerMacOS({required WindowingOwnerMacOS owner, required TooltipWindowControllerDelegate delegate, required BoxConstraints contentSizeConstraints, required BaseWindowController parent, required Rect anchorRect, required WindowPositioner positioner})
```

Creates a new tooltip window controller for macOS.

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

# PopupWindowControllerMacOS

```dart
class PopupWindowControllerMacOS extends PopupWindowController with _WindowControllerMixin {}
```

MacOS specific implementation of [PopupWindowController].

{@macro flutter.widgets.windowing.experimental}

### PopupWindowControllerMacOS()

```dart
PopupWindowControllerMacOS({required WindowingOwnerMacOS owner, required PopupWindowControllerDelegate delegate, required BoxConstraints contentSizeConstraints, required BaseWindowController parent, required Rect anchorRect, required WindowPositioner positioner})
```

Creates a new tooltip window controller for macOS.

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

# RegularWindowControllerMacOS

```dart
class RegularWindowControllerMacOS extends RegularWindowController with _WindowControllerMixin {}
```

Implementation of [RegularWindowController] for the macOS platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the base class for regular windows.

### RegularWindowControllerMacOS()

```dart
RegularWindowControllerMacOS({required WindowingOwnerMacOS owner, required RegularWindowControllerDelegate delegate, required Size? preferredSize, BoxConstraints? preferredConstraints, String? title})
```

Creates a new regular window controller for macOS. When this constructor completes the FlutterView is created and framework is aware of it.

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

### contentSize

```dart
Size get contentSize
```

### activate()

```dart
void activate()
```

### setMaximized()

```dart
void setMaximized(bool maximized)
```

### isMaximized

```dart
bool get isMaximized
```

### setMinimized()

```dart
void setMinimized(bool minimized)
```

### isMinimized

```dart
bool get isMinimized
```

### setFullscreen()

```dart
void setFullscreen(bool fullscreen, {Display? display})
```

### isFullscreen

```dart
bool get isFullscreen
```

### isActivated

```dart
bool get isActivated
```

### title

```dart
String get title
```

# DialogWindowControllerMacOS

```dart
class DialogWindowControllerMacOS extends DialogWindowController with _WindowControllerMixin {}
```

Implementation of [DialogWindowController] for the macOS platform.

{@macro flutter.widgets.windowing.experimental}

See also:

- [DialogWindowController], the base class for dialog windows.

### DialogWindowControllerMacOS()

```dart
DialogWindowControllerMacOS({required WindowingOwnerMacOS owner, required DialogWindowControllerDelegate delegate, required Size? preferredSize, BaseWindowController? parent, BoxConstraints? preferredConstraints, String? title})
```

Creates a new regular window controller for macOS. When this constructor completes the FlutterView is created and framework is aware of it.

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

### contentSize

```dart
Size get contentSize
```

### activate()

```dart
void activate()
```

### setMinimized()

```dart
void setMinimized(bool minimized)
```

### isMinimized

```dart
bool get isMinimized
```

### isActivated

```dart
bool get isActivated
```

### title

```dart
String get title
```

### parent

```dart
BaseWindowController? parent
```
