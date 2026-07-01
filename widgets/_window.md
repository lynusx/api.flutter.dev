# BaseWindowController

```dart
sealed class BaseWindowController extends ChangeNotifier {}
```

Base class for window controllers.

A [BaseWindowController] is associated with exactly one root [FlutterView].

When the window is destroyed for any reason (either by the caller or by the platform), the content of the controller will thereafter be invalid.

{@template flutter.widgets.windowing.experimental} Do not use this API in production applications or packages published to pub.dev. Flutter will make breaking changes to this API, even in patch versions.

This API throws an [UnsupportedError] error unless Flutter’s windowing feature is enabled by [isWindowingEnabled].

See: https://github.com/flutter/flutter/issues/30701. {@endtemplate}

See also:

- [RegularWindowController], the controller for regular top-level windows.

### contentSize

```dart
Size get contentSize
```

The current size of the drawable area of the window.

This might differ from the requested size.

This might also differ from the actual size of the window if the window has decorations such as title bar, borders, etc.

{@macro flutter.widgets.windowing.experimental}

### destroy()

```dart
void destroy()
```

Destroys this window.

It is permissible to call this method multiple times.

{@macro flutter.widgets.windowing.experimental}

### rootView

```dart
FlutterView get rootView
```

The root view associated to this window, which is unique to each window.

{@macro flutter.widgets.windowing.experimental}

### rootView

```dart
set rootView(FlutterView view)
```

Sets the view associated with this window.

{@macro flutter.widgets.windowing.experimental}

# RegularWindowControllerDelegate

```dart
mixin class RegularWindowControllerDelegate {}
```

Delegate class for regular window controller.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the controller that creates and manages regular windows.
- [RegularWindow], the widget for a regular window.

### onWindowCloseRequested()

```dart
void onWindowCloseRequested(RegularWindowController controller)
```

Invoked when the user attempts to close the window.

The default implementation destroys the window. Subclasses can override the behavior to delay or prevent the window from closing.

{@macro flutter.widgets.windowing.experimental}

See also:

- [onWindowDestroyed], which is invoked after the window is closed.

### onWindowDestroyed()

```dart
void onWindowDestroyed()
```

Invoked after the window is closed.

{@macro flutter.widgets.windowing.experimental}

See also:

- [onWindowCloseRequested], which is invoked when the user attempts to close the window.

# RegularWindowController

```dart
abstract class RegularWindowController extends BaseWindowController {}
```

A controller for a regular window.

A regular window is a traditional window that can be resized, minimized, maximized, and closed. Upon construction, the window is created for the platform with the provided properties.

This class does not interact with the widget tree. Instead, it is typically provided to the [RegularWindow] widget, who does the work of rendering the content inside of this window.

The user of this class is responsible for managing the lifecycle of the window. When the window is no longer needed, the user should call [destroy] on this controller to release the resources associated with the window.

{@tool snippet} An example usage might look like:

```dart
// TODO(mattkae): remove invalid_use_of_internal_member ignore comment when this API is stable.
// ignore_for_file: invalid_use_of_internal_member
import 'package:flutter/widgets.dart';
import 'package:flutter/material.dart';
import 'package:flutter/src/widgets/_window.dart';

void main() {
  runWidget(
    RegularWindow(
      controller: RegularWindowController(
        preferredSize: const Size(800, 600),
        preferredConstraints: const BoxConstraints(minWidth: 640, minHeight: 480),
        title: 'Example Window',
      ),
      child: MaterialApp(home: Container()),
    ),
  );
}
```

{@end-tool}

Children of a [RegularWindow] widget can access the [RegularWindowController] via the [WindowScope] inherited widget.

{@macro flutter.widgets.windowing.experimental}

### RegularWindowController()

```dart
RegularWindowController({required Size preferredSize, BoxConstraints? preferredConstraints, String? title, RegularWindowControllerDelegate? delegate})
```

Creates a [RegularWindowController] with a specific size.

Upon construction, the window is created by the platform with the given [preferredSize].

{@template flutter.widgets.windowing.sizedConstructor}

The [preferredSize] is the preferred content size of the window. The platform will try to apply this size when the window is created, but it might not be honored.

The [preferredConstraints] field enforces the minimum and maximum size of the window. The [preferredSize] must satisfy the [preferredConstraints]. If the user attempts to resize the window beyond these constraints, the platform will enforce the constraints according to its own policy. For example, the platform might clip the content to fit within the resized window, or it might prevent the window from being resized altogether. These constraints might not be honored by the platform. If null, the window will be unconstrained. {@endtemplate}

To create a window that is sized to its content instead, use [RegularWindowController.sizedToContent].

{@template flutter.widgets.windowing.shared} The [title] argument configures the window's title. If omitted, some platforms might fall back to the app's name.

The [delegate] argument can be used to listen to the window's lifecycle. For example, it can be used to save state before a window is closed. {@endtemplate}

{@macro flutter.widgets.windowing.experimental}

### RegularWindowController.sizedToContent()

```dart
RegularWindowController.sizedToContent({bool resizable = false, BoxConstraints? preferredConstraints, String? title, RegularWindowControllerDelegate? delegate})
```

Creates a [RegularWindowController] that sizes the window to its content.

{@template flutter.widgets.windowing.sizedToContentConstructor} The window is created by the platform and initially sized to fit its content.

The [resizable] property determines how the window behaves after that initial sizing:

- If `false`, the window remains fixed to its content size. If the content changes size, the window will automatically resize to match, subject to [preferredConstraints]. This is the default.
- If `true`, the user can manually resize the window, subject to [preferredConstraints]. After the initial automatic sizing, the window will no longer track the size of its content.

The [preferredConstraints] field enforces the minimum and maximum size of the window. If the user attempts to resize the window beyond these constraints, the platform will enforce the constraints according to its own policy. For example, the platform might clip the content to fit within the resized window, or it might prevent the window from being resized altogether. These constraints might not be honored by the platform. If null, the window will be unconstrained. {@endtemplate}

To create a window with a specific size instead, use the default [RegularWindowController] constructor.

{@macro flutter.widgets.windowing.shared}

{@macro flutter.widgets.windowing.experimental}

### RegularWindowController.empty()

```dart
RegularWindowController.empty()
```

Creates an empty [RegularWindowController].

This method is only intended to be used by subclasses of the [RegularWindowController].

Users who want to instantiate a new [RegularWindowController] should always use the factory method to create a controller that is valid for their particular platform.

{@macro flutter.widgets.windowing.experimental}

### title

```dart
String get title
```

The current title of the window.

The title shown in the window is controlled by the platform and may differ from the `title` set by the constructor or `setTitle`.

{@macro flutter.widgets.windowing.experimental}

### isActivated

```dart
bool get isActivated
```

Whether the window is currently activated.

If `true` this means that the window is currently focused and can receive user input.

{@macro flutter.widgets.windowing.experimental}

### isMaximized

```dart
bool get isMaximized
```

Whether or not the window is currently maximized.

{@macro flutter.widgets.windowing.experimental}

### isMinimized

```dart
bool get isMinimized
```

Whether or not window is currently minimized.

{@macro flutter.widgets.windowing.experimental}

### isFullscreen

```dart
bool get isFullscreen
```

Whether or not the window is currently in fullscreen mode.

{@macro flutter.widgets.windowing.experimental}

### setSize()

```dart
void setSize(Size size)
```

Request change to the content size of the window.

The [size] describes the new requested window size. If the size disagrees with the current constraints placed upon the window, the platform might clamp the size within the constraints.

The platform is free to ignore this request.

{@macro flutter.widgets.windowing.experimental}

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

Request change to the constraints of the window.

The [constraints] describes the new constraints that the window should satisfy. If the constraints disagree with the current size of the window, the platform might resize the window to satisfy the new constraints.

The platform is free to ignore this request.

{@macro flutter.widgets.windowing.experimental}

### setTitle()

```dart
void setTitle(String title)
```

Request change for the window title.

{@macro flutter.widgets.windowing.experimental}

### activate()

```dart
void activate()
```

Requests that the window be displayed in its current size and position.

The platform may also give the window input focus and bring it to the top of the window stack. However, this behavior is platform-dependent.

If the window is minimized, the window returns to the size and position that it had before that state was applied. The window will also be brought to the top of the window stack.

{@macro flutter.widgets.windowing.experimental}

### setMaximized()

```dart
void setMaximized(bool maximized)
```

Requests the window to be maximized.

This has no effect if the window is currently full screen or minimized, but might affect the window size upon restoring it from minimized or full screen state.

{@macro flutter.widgets.windowing.experimental}

### setMinimized()

```dart
void setMinimized(bool minimized)
```

Requests window to be minimized.

{@macro flutter.widgets.windowing.experimental}

### setFullscreen()

```dart
void setFullscreen(bool fullscreen, {Display? display})
```

Request change for the window to enter or exit fullscreen state.

If [fullscreen] is set to true, the platform will attempt to change the state of the window to fullscreen. If false, the window will return to a previous non-hidden state. Both cases might not be honored by the platform.

The [display] specifies an optional [Display] on which the window would like to be fullscreened. This might not be honored by the platform. The [display] argument is ignored if [fullscreen] is `false`.

When [fullscreen] is set to false, it is up to the platform as to which display the window will be restored to. The platform might restore the window to the display on which it was previously fullscreened, or it might restore the window to the display on which it was last active.

{@macro flutter.widgets.windowing.experimental}

# DialogWindowControllerDelegate

```dart
mixin class DialogWindowControllerDelegate {}
```

Delegate class for dialog window controller.

{@macro flutter.widgets.windowing.experimental}

See also:

- [DialogWindowController], the controller that creates and manages dialog windows.
- [DialogWindow], the widget for a dialog window.
- [RegularWindowControllerDelegate], the delegate for regular window controllers.

### onWindowCloseRequested()

```dart
void onWindowCloseRequested(DialogWindowController controller)
```

Invoked when the user attempts to close the window.

The default implementation destroys the window. Subclasses can override the behavior to delay or prevent the window from closing.

{@macro flutter.widgets.windowing.experimental}

See also:

- [onWindowDestroyed], which is invoked after the window is closed.

### onWindowDestroyed()

```dart
void onWindowDestroyed()
```

Invoked after the window is closed.

{@macro flutter.widgets.windowing.experimental}

See also:

- [onWindowCloseRequested], which is invoked when the user attempts to close the window.

# DialogWindowController

```dart
abstract class DialogWindowController extends BaseWindowController {}
```

A controller for a dialog window.

Two types of dialogs are supported:

- Modal dialogs: created with a non-null parent. These dialogs are modal to the parent, do not have a system menu, and are not selectable from the window switcher.
- Modeless dialogs: created with a null parent. These dialogs can be minimized (but not maximized), and have a disabled close button.

This class does not interact with the widget tree. Instead, it is typically provided to the [DialogWindow] widget, which renders the content inside the dialog window.

The user of this class is responsible for managing the lifecycle of the window. When the window is no longer needed, the user should call [destroy] on this controller to release the resources associated with the window.

{@tool snippet} An example usage might look like:

```dart
// TODO(mattkae): remove invalid_use_of_internal_member ignore comment when this API is stable.
// ignore_for_file: invalid_use_of_internal_member
import 'package:flutter/widgets.dart';
import 'package:flutter/material.dart';
import 'package:flutter/src/widgets/_window.dart';

void main() {
  runWidget(
    RegularWindow(
      controller: RegularWindowController(
        preferredSize: const Size(800, 600),
        preferredConstraints: const BoxConstraints(minWidth: 640, minHeight: 480),
        title: 'Example Window',
      ),
      child: const MyApp()
    )
  );
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: DialogWindow(
        controller: DialogWindowController(
          preferredSize: const Size(400, 300),
          parent: WindowScope.of(context),
          title: 'Example Dialog'
        ),
        child: const Text('Hello, World!')
      )
    );
  }
}
```

{@end-tool}

Children of a [DialogWindow] widget can access the [DialogWindowController] via the [WindowScope] inherited widget.

{@macro flutter.widgets.windowing.experimental}

### DialogWindowController()

```dart
DialogWindowController({required Size preferredSize, BoxConstraints? preferredConstraints, BaseWindowController? parent, String? title, DialogWindowControllerDelegate? delegate})
```

Creates a [DialogWindowController] with a specific size.

Upon construction, the window is created by the platform with the given [preferredSize].

{@macro flutter.widgets.windowing.sizedConstructor}

To create a dialog that is sized to its content instead, use [DialogWindowController.sizedToContent].

{@template flutter.widgets.windowing.dialogParent} The [parent] argument specifies the parent window of this dialog.

If the [parent] is null, then the dialog is modeless. Such dialogs can be minimized but not maximized. They also have a disabled close button.

If the [parent] is non-null, then the dialog is modal to the parent. Such dialogs do not have a system menu. They are also not selectable from the window switcher and they are closed when the parent is closed. {@endtemplate}

{@macro flutter.widgets.windowing.shared}

{@macro flutter.widgets.windowing.experimental}

### DialogWindowController.sizedToContent()

```dart
DialogWindowController.sizedToContent({bool resizable = false, BoxConstraints? preferredConstraints, BaseWindowController? parent, String? title, DialogWindowControllerDelegate? delegate})
```

Creates a [DialogWindowController] that sizes the window to its content.

{@macro flutter.widgets.windowing.sizedToContentConstructor}

To create a dialog with a specific size instead, use the default [DialogWindowController] constructor.

{@macro flutter.widgets.windowing.dialogParent}

{@macro flutter.widgets.windowing.shared}

{@macro flutter.widgets.windowing.experimental}

### DialogWindowController.empty()

```dart
DialogWindowController.empty()
```

Creates an empty [DialogWindowController].

This method is only intended to be used by subclasses of the [DialogWindowController].

Users who want to instantiate a new [DialogWindowController] should always use the factory method to create a controller that is valid for their particular platform.

{@macro flutter.widgets.windowing.experimental}

### parent

```dart
BaseWindowController? get parent
```

The parent controller of this dialog, if any.

If null, this dialog is modeless. If non-null, this dialog is modal to the parent.

{@macro flutter.widgets.windowing.experimental}

### title

```dart
String get title
```

The current title of the window.

The title shown in the window is controlled by the platform and may differ from the `title` set by the constructor or `setTitle`.

{@macro flutter.widgets.windowing.experimental}

### isActivated

```dart
bool get isActivated
```

Whether the window is currently activated.

If `true` this means that the window is currently focused and can receive user input.

{@macro flutter.widgets.windowing.experimental}

### isMinimized

```dart
bool get isMinimized
```

Whether or not window is currently minimized.

{@macro flutter.widgets.windowing.experimental}

### setSize()

```dart
void setSize(Size size)
```

Request change to the content size of the window.

The [size] describes the new requested window size. If the size disagrees with the current constraints placed upon the window, the platform might clamp the size within the constraints.

The platform is free to ignore this request.

{@macro flutter.widgets.windowing.experimental}

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

Request change to the constraints of the window.

The [constraints] describes the new constraints that the window should satisfy. If the constraints disagree with the current size of the window, the platform might resize the window to satisfy the new constraints.

The platform is free to ignore this request.

{@macro flutter.widgets.windowing.experimental}

### setTitle()

```dart
void setTitle(String title)
```

Request change for the window title.

{@macro flutter.widgets.windowing.experimental}

### activate()

```dart
void activate()
```

Requests that the window be displayed in its current size and position.

The platform may also give the window input focus and bring it to the top of the window stack. However, this behavior is platform-dependent.

If the window is minimized, the window returns to the size and position that it had before that state was applied. The window will also be brought to the top of the window stack.

{@macro flutter.widgets.windowing.experimental}

### setMinimized()

```dart
void setMinimized(bool minimized)
```

Requests window to be minimized.

{@macro flutter.widgets.windowing.experimental}

# TooltipWindowControllerDelegate

```dart
mixin class TooltipWindowControllerDelegate {}
```

Delegate class for tooltip window controller.

{@macro flutter.widgets.windowing.experimental}

See also:

- [TooltipWindowController], the controller that creates and manages tooltip windows.
- [TooltipWindow], the widget for a tooltip window.
- [RegularWindowControllerDelegate], the delegate for regular window controllers.

### onWindowDestroyed()

```dart
void onWindowDestroyed()
```

Invoked after the window is closed.

{@macro flutter.widgets.windowing.experimental}

# TooltipWindowController

```dart
abstract class TooltipWindowController extends BaseWindowController {}
```

A controller for a tooltip window.

A tooltip window is a small window that displays brief, informative text when a user hovers over or focuses on a UI element. Tooltip windows are typically used to provide additional context or explanations for UI elements without cluttering the main interface. As such, it may not receive input focus from the user. It will however stay open when another window receives input focus.

This class does not interact with the widget tree. Instead, it is typically provided to the [TooltipWindow] widget, which renders the content inside the tooltip window.

The user of this class is responsible for managing the lifecycle of the window. When the window is no longer needed, the user should call [destroy] on this controller to release the resources associated with the window.

If the parent window of the tooltip is destroyed, then the tooltip will be destroyed as well. The user does not need to explicitly call [destroy] in this case.

{@tool snippet} An example usage of [TooltipWindowController] looks like:

** See code in examples/api/lib/widgets/windows/tooltip.0.dart ** {@end-tool}

Children of a [TooltipWindow] widget can access the [TooltipWindowController] via the [WindowScope] inherited widget.

{@macro flutter.widgets.windowing.experimental}

### TooltipWindowController()

```dart
TooltipWindowController({required BaseWindowController parent, required Rect anchorRect, required WindowPositioner positioner, BoxConstraints preferredConstraints = const BoxConstraints(), TooltipWindowControllerDelegate? delegate})
```

Creates a [TooltipWindowController] with the provided properties.

Upon construction, the window is created by the platform.

The [parent] argument specifies the parent window of this tooltip.

The [anchorRect] argument specifies the rectangle in the parent's coordinate space to which the tooltip is anchored.

The [positioner] argument specifies how the tooltip should be positioned relative to the [anchorRect].

The [preferredConstraints] are the constraints placed upon the size of the window.

{@macro flutter.widgets.windowing.constraints}

The [delegate] argument can be used to listen to the window's lifecycle. For example, it can be used to save state before a window is closed.

{@macro flutter.widgets.windowing.experimental}

### TooltipWindowController.empty()

```dart
TooltipWindowController.empty()
```

Creates an empty [TooltipWindowController].

This method is only intended to be used by subclasses of the [TooltipWindowController].

Users who want to instantiate a new [TooltipWindowController] should always use the factory method to create a controller that is valid for their particular platform.

{@macro flutter.widgets.windowing.experimental}

### parent

```dart
BaseWindowController get parent
```

The parent controller of this tooltip.

The tooltip will be destroyed if its parent is destroyed.

{@macro flutter.widgets.windowing.experimental}

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

Request change to the constraints of the window.

The [constraints] describes the new constraints that the window should satisfy. If the constraints disagree with the current size of the window, the platform might resize the window to satisfy the new constraints.

The platform is free to ignore this request.

{@macro flutter.widgets.windowing.experimental}

### updatePosition()

```dart
void updatePosition({Rect? anchorRect, WindowPositioner? positioner})
```

Updates the position of the tooltip.

This requests that the tooltip be repositioned according to the new [anchorRect] and/or [positioner].

On Linux due to a platform limitation this has no effect and only the positioner passed in the constructor is used. This means that tooltips that resize on Linux will remain in their original location.

{@macro flutter.widgets.windowing.experimental}

# PopupWindowControllerDelegate

```dart
mixin class PopupWindowControllerDelegate {}
```

Delegate class for popup window controller.

{@macro flutter.widgets.windowing.experimental}

See also:

- [PopupWindowController], the controller that creates and manages popup windows.
- [PopupWindow], the widget for a popup window.
- [RegularWindowControllerDelegate], the delegate for regular window controllers.

### onWindowDestroyed()

```dart
void onWindowDestroyed()
```

Invoked after the window is closed.

{@macro flutter.widgets.windowing.experimental}

# PopupWindowController

```dart
abstract class PopupWindowController extends BaseWindowController {}
```

A controller for a popup window.

A popup window is a transient window that is used for menus and context menus. Popups may receive input focus. When another window receives input focus, the popup is closed.

This class does not interact with the widget tree. Instead, it is typically provided to the [PopupWindow] widget, which renders the content inside the popup window.

The user of this class is responsible for managing the lifecycle of the window. When the window is no longer needed, the user should call [destroy] on this controller to release the resources associated with the window.

If the parent window of the popup is destroyed, then the popup will be destroyed as well. The user does not need to explicitly call [destroy] in this case.

{@tool snippet} An example usage of [PopupWindowController] looks like:

** See code in examples/api/lib/widgets/windows/popup.0.dart ** {@end-tool}

Children of a [PopupWindow] widget can access the [PopupWindowController] via the [WindowScope] [InheritedWidget].

{@macro flutter.widgets.windowing.experimental}

### PopupWindowController()

```dart
PopupWindowController({required BaseWindowController parent, required Rect anchorRect, required WindowPositioner positioner, BoxConstraints? preferredConstraints, PopupWindowControllerDelegate? delegate})
```

Creates a [PopupWindowController] with the provided properties.

Upon construction, the window is created by the platform.

The [parent] argument specifies the parent window of this popup.

The [anchorRect] argument specifies the rectangle in the parent's coordinate space to which the popup is anchored.

The [positioner] argument specifies how the popup should be positioned relative to the [anchorRect].

{@macro flutter.widgets.windowing.constraints}

The [delegate] argument can be used to listen to the window's lifecycle. For example, it can be used to save state before a window is closed.

{@macro flutter.widgets.windowing.experimental}

### PopupWindowController.empty()

```dart
PopupWindowController.empty()
```

Creates an empty [PopupWindowController].

This method is only intended to be used by subclasses of the [PopupWindowController].

Users who want to instantiate a new [PopupWindowController] should always use the factory method to create a controller that is valid for their particular platform.

{@macro flutter.widgets.windowing.experimental}

### parent

```dart
BaseWindowController get parent
```

The parent controller of this popup.

The popup will be destroyed if its parent is destroyed.

{@macro flutter.widgets.windowing.experimental}

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

Request change to the constraints of the window.

The [constraints] describes the new constraints that the window should satisfy. If the constraints disagree with the current size of the window, the platform might resize the window to satisfy the new constraints.

{@macro flutter.widgets.windowing.experimental}

### updatePosition()

```dart
void updatePosition({Rect? anchorRect, WindowPositioner? positioner})
```

Updates the position of the popup.

This requests that the popup be repositioned according to the new [anchorRect] and/or [positioner].

{@macro flutter.widgets.windowing.experimental}

### offsetFromParent

```dart
Offset get offsetFromParent
```

Returns the offset of the popup's top-left corner in the parent window client area.

The offset is in logical coordinates.

{@macro flutter.widgets.windowing.experimental}

### activate()

```dart
void activate()
```

Request activations of the window hierarchy to which this popup belongs.

The popup window will receive keyboard input when the closest regular or dialog window is active and a focus node within this popup window is focused.

{@macro flutter.widgets.windowing.experimental}

### isActivated

```dart
bool get isActivated
```

Whether the window this popup belongs to is currently activated.

{@macro flutter.widgets.windowing.experimental}

# SatelliteWindowControllerDelegate

```dart
mixin class SatelliteWindowControllerDelegate {}
```

Delegate class for satellite window controller.

{@macro flutter.widgets.windowing.experimental}

See also:

- [SatelliteWindowController], the controller that creates and manages a satellite window.
- [SatelliteWindow], the widget for a satellite window.

### onWindowCloseRequested()

```dart
void onWindowCloseRequested(SatelliteWindowController controller)
```

Invoked when the user attempts to close the window.

The default implementation destroys the window. Subclasses can override the behavior to delay or prevent the window from closing.

{@macro flutter.widgets.windowing.experimental}

See also:

- [onWindowDestroyed], which is invoked after the window is closed.

### onWindowDestroyed()

```dart
void onWindowDestroyed()
```

Invoked after the window is closed.

{@macro flutter.widgets.windowing.experimental}

See also:

- [onWindowCloseRequested], which is invoked when the user attempts to close the window.

# SatelliteWindowController

```dart
abstract class SatelliteWindowController extends BaseWindowController {}
```

A controller for a satellite window.

A satellite window is an auxiliary window to a regular or dialog window. Satellite windows are initiially placed using a [WindowPositioner]. Afterwards, the satellite window maintains its position relative to its parent. It is hidden if the application becomes fullscreen or maximized.

Satellite windows may be resized and moved by the user. After being moved by the user, the satellite window will retain its new position relative to its parent such that when its parent moves, the satellite will be moved by the same offset.

A satellite may be reparented. For example, if an application has two documents open, the satellite may choose to reparent to the active document such that closing one document will not cause the satellite to close. This behavior may be implemented at the library level, such as in the Material API. Reparenting a satellite will not change the current absolute position of the satellite.

Upon construction, the window is created for the platform with the provided properties.

This class does not interact with the widget tree. Instead, it is typically provided to the [SatelliteWindow] widget, who does the work of rendering the content inside of this window.

The user of this class is responsible for managing the lifecycle of the window. When the window is no longer needed, the user should call [destroy] on this controller to release the resources associated with the window.

If the parent window of the satellite is destroyed, then the satellite will be destroyed as well. The user does not need to explicitly call [destroy] in this case.

[SatelliteWindowControllerDelegate.onWindowDestroyed] will be called when the window is destroyed.

{@tool snippet} An example usage of [SatelliteWindowController] looks like:

** See code in examples/api/lib/widgets/windows/satellite.0.dart ** {@end-tool}

Children of a [SatelliteWindow] widget can access the [SatelliteWindowController] via the [WindowScope] inherited widget.

{@macro flutter.widgets.windowing.experimental}

### SatelliteWindowController()

```dart
SatelliteWindowController({required BaseWindowController parent, required WindowPositioner initialPositioner, Rect? initialAnchorRect, Size? preferredSize, BoxConstraints? preferredConstraints, String? title, SatelliteWindowControllerDelegate? delegate})
```

Creates a [SatelliteWindowController] with the provided properties.

Upon construction, the window is created by the platform with the given [preferredSize].

{@template flutter.widgets.windowing.satelliteConstructorCommon} The [parent] argument specifies the parent window of this satellite.

The [initialPositioner] argument specifies how the satellite should be positioned relative to the [initialAnchorRect]. The positioner is only applied the first time that the window is shown. Afterwards, the user may move and resize the window to their preference. If the [parent] of the satellite moves, the satellite is moved relative to its parent. The satellite will always retain its current offset from its parent unless it is moved independently.

The [initialAnchorRect] argument specifies the rectangle in the parent's coordinate space to which the tooltip is anchored. If it is `null`, then the satellite is position relative to the parent window, including its decorations. {@endtemplate}

{@macro flutter.widgets.windowing.sizedConstructor}

The [title] argument configures the window's title. If omitted, some platforms might fall back to the app's name.

The [delegate] argument can be used to listen to the window's lifecycle. For example, it can be used to save state before a window is closed.

{@macro flutter.widgets.windowing.experimental}

### SatelliteWindowController.sizedToContent()

```dart
SatelliteWindowController.sizedToContent({required BaseWindowController parent, required WindowPositioner initialPositioner, Rect? initialAnchorRect, bool resizable = false, BoxConstraints? preferredConstraints, String? title, SatelliteWindowControllerDelegate? delegate})
```

Creates a [SatelliteWindowController] that sizes the window to its content.

{@macro flutter.widgets.windowing.satelliteConstructorCommon}

{@macro flutter.widgets.windowing.sizedToContentConstructor}

To create a dialog with a specific size instead, use the default [SatelliteWindowController] constructor.

{@macro flutter.widgets.windowing.shared}

{@macro flutter.widgets.windowing.experimental}

### SatelliteWindowController.empty()

```dart
SatelliteWindowController.empty()
```

Creates an empty [SatelliteWindowController].

This method is only intended to be used by subclasses of the [SatelliteWindowController].

Users who want to instantiate a new [SatelliteWindowController] should always use the factory method to create a controller that is valid for their particular platform.

{@macro flutter.widgets.windowing.experimental}

### parent

```dart
BaseWindowController get parent
```

The parent controller of this satellite.

The satellite will be destroyed if its parent is destroyed.

{@macro flutter.widgets.windowing.experimental}

### title

```dart
String get title
```

The current title of the window.

The title shown in the window is controlled by the platform and may differ from the `title` set by the constructor or `setTitle`.

{@macro flutter.widgets.windowing.experimental}

### isActivated

```dart
bool get isActivated
```

Whether the window is currently activated.

If `true` this means that the window is currently focused and can receive user input.

{@macro flutter.widgets.windowing.experimental}

### setParent()

```dart
void setParent(BaseWindowController parent)
```

Request to change the parent of the window.

The satellite will maintain its current position after being reparented.

{@macro flutter.widgets.windowing.experimental}

### setSize()

```dart
void setSize(Size size)
```

Request change to the content size of the window.

The [size] describes the new requested window size. If the size disagrees with the current constraints placed upon the window, the platform might clamp the size within the constraints.

{@macro flutter.widgets.windowing.experimental}

### setConstraints()

```dart
void setConstraints(BoxConstraints constraints)
```

Request change to the constraints of the window.

The [constraints] describes the new constraints that the window should satisfy. If the constraints disagree with the current size of the window, the platform might resize the window to satisfy the new constraints.

{@macro flutter.widgets.windowing.experimental}

### setTitle()

```dart
void setTitle(String title)
```

Request change for the window title.

{@macro flutter.widgets.windowing.experimental}

### activate()

```dart
void activate()
```

Requests that the window be displayed in its current size and position.

The platform may also give the window input focus and bring it to the top of the window stack. However, this behavior is platform-dependent.

If the window is minimized, the window returns to the size and position that it had before that state was applied. The window will also be brought to the top of the window stack.

{@macro flutter.widgets.windowing.experimental}

# WindowingOwner

```dart
abstract class WindowingOwner {}
```

[WindowingOwner] is responsible for creating and managing window controllers.

A custom implementation can be provided by setting [WidgetsBinding.windowingOwner].

{@macro flutter.widgets.windowing.experimental}

### createRegularWindowController()

```dart
RegularWindowController createRegularWindowController({required RegularWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, String? title})
```

Creates a [RegularWindowController] with the provided properties.

Most app developers should use [RegularWindowController]'s constructor instead of calling this method directly. This method allows platforms to inject platform-specific logic.

{@macro flutter.widgets.windowing.experimental}

### createDialogWindowController()

```dart
DialogWindowController createDialogWindowController({required DialogWindowControllerDelegate delegate, Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, BaseWindowController? parent, String? title})
```

Creates a [DialogWindowController] with the provided properties.

Most app developers should use [DialogWindowController]'s constructor instead of calling this method directly. This method allows platforms to inject platform-specific logic.

{@macro flutter.widgets.windowing.experimental}

### createTooltipWindowController()

```dart
TooltipWindowController createTooltipWindowController({required TooltipWindowControllerDelegate delegate, required BoxConstraints preferredConstraints, required Rect anchorRect, required WindowPositioner positioner, required BaseWindowController parent})
```

Creates a [TooltipWindowController] with the provided properties.

Most app developers should use [TooltipWindowController]'s constructor instead of calling this method directly. This method allows platforms to inject platform-specific logic.

{@macro flutter.widgets.windowing.experimental}

### createPopupWindowController()

```dart
PopupWindowController createPopupWindowController({required PopupWindowControllerDelegate delegate, required BoxConstraints preferredConstraints, required Rect anchorRect, required WindowPositioner positioner, required BaseWindowController parent})
```

Creates a [PopupWindowController] with the provided properties.

Most app developers should use [PopupWindowController]'s constructor instead of calling this method directly. This method allows platforms to inject platform-specific logic.

{@macro flutter.widgets.windowing.experimental}

### createSatelliteWindowController()

```dart
SatelliteWindowController createSatelliteWindowController({required SatelliteWindowControllerDelegate delegate, required BaseWindowController parent, required WindowPositioner initialPositioner, Rect? initialAnchorRect, Size? preferredSize, BoxConstraints? preferredConstraints, required bool resizable, String? title})
```

Creates a [SatelliteWindowController] with the provided properties.

Most app developers should use [SatelliteWindowController]'s constructor instead of calling this method directly. This method allows platforms to inject platform-specific logic.

{@macro flutter.widgets.windowing.experimental}

# createDefaultWindowingOwner()

```dart
WindowingOwner createDefaultWindowingOwner()
```

Creates default windowing owner for standard desktop embedders.

{@macro flutter.widgets.windowing.experimental}

# RegularWindow

```dart
class RegularWindow extends StatelessWidget {}
```

The [RegularWindow] widget provides a way to render a regular window in the widget tree.

The provided [controller] creates the native window that backs the widget. The [child] widget is rendered into this newly created window.

When a [RegularWindow] widget is removed from the tree, the window that was created by the [controller] remains valid until the caller destroys it by calling [RegularWindowController.destroy].

Widgets in the same tree as the [child] widget will have access to the [RegularWindowController] via the [WindowScope] widget.

{@tool snippet} An example usage might look like:

```dart
// TODO(mattkae): remove invalid_use_of_internal_member ignore comment when this API is stable.
// ignore_for_file: invalid_use_of_internal_member
import 'package:flutter/widgets.dart';
import 'package:flutter/material.dart';
import 'package:flutter/src/widgets/_window.dart';

void main() {
  runWidget(
    RegularWindow(
      controller: RegularWindowController(
        preferredSize: const Size(800, 600),
        preferredConstraints: const BoxConstraints(minWidth: 640, minHeight: 480),
        title: 'Example Window',
      ),
      child: MaterialApp(home: Container()),
    ),
  );
}
```

{@end-tool}

{@macro flutter.widgets.windowing.experimental}

### RegularWindow()

```dart
RegularWindow({dynamic key, required RegularWindowController controller, required Widget child})
```

Creates a regular window widget.

The [controller] creates the native backing window into which the [child] widget is rendered.

It is up to the caller to destroy the window by calling [RegularWindowController.destroy] when the window is no longer needed.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
RegularWindowController controller
```

Controller for this widget.

{@macro flutter.widgets.windowing.experimental}

### child

```dart
Widget child
```

The content rendered into this window.

{@macro flutter.widgets.windowing.experimental}

### build()

```dart
Widget build(BuildContext context)
```

{@macro flutter.widgets.windowing.experimental}

# DialogWindow

```dart
class DialogWindow extends StatelessWidget {}
```

The [DialogWindow] widget provides a way to render a dialog window in the widget tree.

The provided [controller] creates the native window that backs the widget. The [child] widget is rendered into this newly created window.

When a [DialogWindow] widget is removed from the tree, the window that was created by the [controller] remains valid until the caller destroys it by calling [DialogWindowController.destroy].

Widgets in the same tree as the [child] widget will have access to the [DialogWindowController] via the [WindowScope] widget.

{@tool snippet} An example usage might look like:

```dart
// TODO(mattkae): remove invalid_use_of_internal_member ignore comment when this API is stable.
// ignore_for_file: invalid_use_of_internal_member
import 'package:flutter/widgets.dart';
import 'package:flutter/material.dart';
import 'package:flutter/src/widgets/_window.dart';

void main() {
  runWidget(
    RegularWindow(
      controller: RegularWindowController(
        preferredSize: const Size(800, 600),
        preferredConstraints: const BoxConstraints(minWidth: 640, minHeight: 480),
        title: 'Example Window',
      ),
      child: const MyApp()
    )
  );
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: DialogWindow(
        controller: DialogWindowController(
          preferredSize: const Size(400, 300),
          parent: WindowScope.of(context),
          title: 'Example Dialog'
        ),
        child: const Text('Hello, World!')
      )
    );
  }
}
```

{@end-tool}

{@macro flutter.widgets.windowing.experimental}

### DialogWindow()

```dart
DialogWindow({dynamic key, required DialogWindowController controller, required Widget child})
```

Creates a dialog window widget.

The [controller] creates the native backing window into which the [child] widget is rendered.

It is up to the caller to destroy the window by calling [DialogWindowController.destroy] when the window is no longer needed.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
DialogWindowController controller
```

Controller for this widget.

{@macro flutter.widgets.windowing.experimental}

### child

```dart
Widget child
```

The content rendered into this window.

{@macro flutter.widgets.windowing.experimental}

### build()

```dart
Widget build(BuildContext context)
```

{@macro flutter.widgets.windowing.experimental}

# TooltipWindow

```dart
class TooltipWindow extends StatelessWidget {}
```

### TooltipWindow()

```dart
TooltipWindow({dynamic key, required TooltipWindowController controller, required Widget child})
```

Creates a tooltip window widget.

The [controller] creates the native backing window into which the [child] widget is rendered.

It is up to the caller to destroy the window by calling [TooltipWindowController.destroy] when the window is no longer needed.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
TooltipWindowController controller
```

Controller for this widget.

{@macro flutter.widgets.windowing.experimental}

### child

```dart
Widget child
```

The content rendered into this window.

{@macro flutter.widgets.windowing.experimental}

### build()

```dart
Widget build(BuildContext context)
```

{@macro flutter.widgets.windowing.experimental}

# PopupWindow

```dart
class PopupWindow extends StatelessWidget {}
```

The [PopupWindow] widget provides a way to render a popup window in the widget tree.

The provided [controller] creates the native window that backs the widget. The [child] widget is rendered into this newly created window.

When a [PopupWindow] widget is removed from the tree, the window that was created by the [controller] remains valid until the caller destroys it by calling [PopupWindowController.destroy].

Widgets in the same tree as the [child] widget will have access to the [PopupWindowController] via the [WindowScope] widget.

{@tool snippet} An example usage of [PopupWindow] looks like:

** See code in examples/api/lib/widgets/windows/popup.0.dart ** {@end-tool} {@macro flutter.widgets.windowing.experimental}

See also:

- [PopupWindowController], the controller that creates and manages popup windows.

### PopupWindow()

```dart
PopupWindow({dynamic key, required PopupWindowController controller, required Widget child})
```

Creates a popup window widget.

The [controller] creates the native backing window into which the [child] widget is rendered.

It is up to the caller to destroy the window by calling [PopupWindowController.destroy] when the window is no longer needed.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
PopupWindowController controller
```

Controller for this widget.

{@macro flutter.widgets.windowing.experimental}

### child

```dart
Widget child
```

The content rendered into this window.

{@macro flutter.widgets.windowing.experimental}

### build()

```dart
Widget build(BuildContext context)
```

{@macro flutter.widgets.windowing.experimental}

# SatelliteWindow

```dart
class SatelliteWindow extends StatelessWidget {}
```

The [SatelliteWindow] widget provides a way to render a satellite window in the widget tree.

The provided [controller] creates the native window that backs the widget. The [child] widget is rendered into this newly created window.

When a [SatelliteWindow] widget is removed from the tree, the window that was created by the [controller] remains valid until the caller destroys it by calling [SatelliteWindowController.destroy].

Widgets in the same tree as the [child] widget will have access to the [SatelliteWindowController] via the [WindowScope] widget.

{@macro flutter.widgets.windowing.experimental}

See also:

- [SatelliteWindowController], the controller that creates and manages satellite windows.

### SatelliteWindow()

```dart
SatelliteWindow({dynamic key, required SatelliteWindowController controller, required Widget child})
```

Creates a satellite window widget.

The [controller] creates the native backing window into which the [child] widget is rendered.

It is up to the caller to destroy the window by calling [SatelliteWindowController.destroy] when the window is no longer needed.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
SatelliteWindowController controller
```

Controller for this widget.

{@macro flutter.widgets.windowing.experimental}

### child

```dart
Widget child
```

The content rendered into this window.

{@macro flutter.widgets.windowing.experimental}

### build()

```dart
Widget build(BuildContext context)
```

{@macro flutter.widgets.windowing.experimental}

# WindowScope

```dart
class WindowScope extends InheritedModel<_WindowControllerAspect> {}
```

Provides descendants with access to the [BaseWindowController] associated with the window that is being rendered.

Windows created using native APIs do not have a [WindowScope]. This includes the initial window created by the native entrypoint that [runApp] attaches to.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindow], the widget to create a regular window.
- [DialogWindow], the widget to create a dialog window.

### WindowScope()

```dart
WindowScope({dynamic key, required BaseWindowController controller, required Widget child})
```

Creates a new [WindowScope].

This widget is used by the window widgets to provide widgets in a window's subtree with access to information about the window.

The [controller] is the controller associated with this window, and the [child] is the widget tree that will have access to this context.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
BaseWindowController controller
```

The controller associated with this window.

{@macro flutter.widgets.windowing.experimental}

### of()

```dart
BaseWindowController of(BuildContext context)
```

Returns the [BaseWindowController] for the window that hosts the given context.

{@template flutter.widgets.windowing.WindowScope.of} If there is no [WindowScope] in scope, this method will throw a [TypeError] exception in release builds, and throws a descriptive [FlutterError] in debug builds.

Windows creating using native APIs do not have a [WindowScope]. This includes the initial window created by the native entrypoint that [runApp] attaches to. {@endtemplate}

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the controller for regular top-level windows.
- [DialogWindowController], the controller for dialog windows.
- [RegularWindow], the widget for a regular window.
- [DialogWindow], the widget for a dialog window.
- [maybeOf], which doesn't throw or assert if it doesn't find a [WindowScope] ancestor. It returns null instead.

### maybeOf()

```dart
BaseWindowController? maybeOf(BuildContext context)
```

Returns the [BaseWindowController] if one exists, otherwise null.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController], the controller for regular top-level windows.
- [DialogWindowController], the controller for dialog windows.
- [RegularWindow], the widget for a regular window.
- [DialogWindow], the widget for a dialog window.
- [of], which will throw if it doesn't find a [WindowScope] ancestor, instead of returning null.

### contentSizeOf()

```dart
Size contentSizeOf(BuildContext context)
```

Returns [BaseWindowController.contentSize] of the nearest [WindowScope].

{@macro flutter.widgets.windowing.windowScope.of}

{@macro flutter.widgets.windowing.experimental}

See also:

- [BaseWindowController.contentSize], which returns the current content size of the window.
- [of], which returns the [BaseWindowController] associated with the window.

### maybeContentSizeOf()

```dart
Size? maybeContentSizeOf(BuildContext context)
```

Returns [BaseWindowController.contentSize] of the nearest [WindowScope], or null if not found.

{@macro flutter.widgets.windowing.experimental}

See also:

- [BaseWindowController.contentSize], which returns the current content size of the window.
- [maybeOf], which returns the [BaseWindowController] associated with the window, or null if not found.

### titleOf()

```dart
String titleOf(BuildContext context)
```

Returns the title of the controller in the nearest [WindowScope].

{@macro flutter.widgets.windowing.windowScope.of}

If the window associated with the controller does not support titles, this method will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.title], which returns the current title of the window.
- [of], which returns the [BaseWindowController] associated with the window.

### maybeTitleOf()

```dart
String? maybeTitleOf(BuildContext context)
```

Returns title of the nearest [WindowScope], or null if not found.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.title], which returns the current title of the window.
- [maybeOf], which returns the [BaseWindowController] associated with the window, or null if not found.

### isActivatedOf()

```dart
bool isActivatedOf(BuildContext context)
```

Returns the activation status of the nearest [WindowScope].

{@macro flutter.widgets.windowing.windowScope.of}

If the window associated with the controller does not support activation, this method will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isActivated], which returns the current activation status of the window.
- [of], which returns the [BaseWindowController] associated with the window.

### maybeIsActivatedOf()

```dart
bool? maybeIsActivatedOf(BuildContext context)
```

Returns the activation status of the nearest [WindowScope], or null if not found.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isActivated], which returns the current activation status of the window.
- [maybeOf], which returns the [BaseWindowController] associated with the window, or null if not found.

### isMinimizedOf()

```dart
bool isMinimizedOf(BuildContext context)
```

Returns the minimization status of the nearest [WindowScope].

{@macro flutter.widgets.windowing.windowScope.of}

If the window associated with the controller does not support minimization, this method will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isMinimized], which returns the current minimized status of the window.
- [of], which returns the [BaseWindowController] associated with the window.

### maybeIsMinimizedOf()

```dart
bool? maybeIsMinimizedOf(BuildContext context)
```

Returns the minimization status of the nearest [WindowScope], or null if not found.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isMinimized], which returns the current minimized status of the window.
- [maybeOf], which returns the [BaseWindowController] associated with the window, or null if not found.

### isMaximizedOf()

```dart
bool isMaximizedOf(BuildContext context)
```

Returns the maximization status of the nearest [WindowScope].

{@macro flutter.widgets.windowing.windowScope.of}

If the window associated with the controller does not support maximization, this method will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isMaximized], which returns the current maximized status of the window.
- [of], which returns the [BaseWindowController] associated with the window.

### maybeIsMaximizedOf()

```dart
bool? maybeIsMaximizedOf(BuildContext context)
```

Returns the maximization status of the nearest [WindowScope], or null if not found.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isMaximized], which returns the current maximized status of the window.
- [maybeOf], which returns the [BaseWindowController] associated with the window, or null if not found.

### isFullscreenOf()

```dart
bool isFullscreenOf(BuildContext context)
```

Returns the fullscreen status of the nearest [WindowScope].

{@macro flutter.widgets.windowing.windowScope.of}

If the window associated with the controller does not support fullscreen, this method will throw an [UnsupportedError].

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isFullscreen], which returns the current fullscreen status of the window.
- [of], which returns the [BaseWindowController] associated with the window.

### maybeIsFullscreenOf()

```dart
bool? maybeIsFullscreenOf(BuildContext context)
```

Returns the fullscreen status of the nearest [WindowScope], or null if not found.

{@macro flutter.widgets.windowing.experimental}

See also:

- [RegularWindowController.isFullscreen], which returns the current fullscreen status of the window.
- [maybeOf], which returns the [BaseWindowController] associated with the window, or null if not found.

### updateShouldNotify()

```dart
bool updateShouldNotify(WindowScope oldWidget)
```

{@macro flutter.widgets.windowing.experimental}

### updateShouldNotifyDependent()

```dart
bool updateShouldNotifyDependent(WindowScope oldWidget, Set<Object> dependencies)
```

{@macro flutter.widgets.windowing.experimental}

# WindowRegistry

```dart
class WindowRegistry extends ChangeNotifier {}
```

A registry used to render top-level windows.

The registry is often used to render top-level windows that are logically nested under a widget deep in the tree.

The [WindowManager] provides a [WindowRegistry] to its descendents.

Descendents of the manager can use [WindowRegistry.maybeOf] to access the registry. With the registry, they can call [WindowRegistry.register] to add a new window to the registry and [WindowRegistry.unregister] to remove a window from the registry.

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowManager], responsible for listening for new windows and rendering them.

### WindowRegistry()

```dart
WindowRegistry()
```

Creates a window registry.

{@macro flutter.widgets.windowing.experimental}

### windows

```dart
List<WindowEntry> get windows
```

The list of registered windows.

{@macro flutter.widgets.windowing.experimental}

### register()

```dart
void register(WindowEntry entry)
```

Registers a window.

The [entry] parameter specifies the window to register.

{@macro flutter.widgets.windowing.experimental}

### unregister()

```dart
void unregister(WindowEntry entry)
```

Unregisters a window.

The window must be unregistered before it is destroyed. Call [BaseWindowController.destroy] to destroy the window or listen to the onWindowCloseRequested method of the window's delegate.

The [entry] parameter specifies the window to unregister.

{@macro flutter.widgets.windowing.experimental}

### maybeOf()

```dart
WindowRegistry? maybeOf(BuildContext context)
```

Retrieves the [WindowRegistry] from the given [context].

Returns null if no registry is found in the widget tree.

This does not throw when used in a non-windowing environment, as this may be a signal to the owner that windowing itself is unavailable.

{@macro flutter.widgets.windowing.experimental}

### of()

```dart
WindowRegistry of(BuildContext context)
```

Retrieves the [WindowRegistry] from the given [context].

If there is no [WindowRegistry] in scope, this method will throw a [TypeError] exception in release builds, and throws a descriptive [FlutterError] in debug builds.

This method can still be called when windowing is not enabled, as it may be a signal to the owner that windowing itself is unavailable.

{@macro flutter.widgets.windowing.experimental}

# WindowEntry

```dart
class WindowEntry {}
```

Represents an entry for a window such as a dialog.

This class holds the necessary information to build and manage a window within the application.

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowRegistry], where window entries can be registered.

### WindowEntry()

```dart
WindowEntry({required BaseWindowController controller, required WidgetBuilder builder})
```

Creates a window entry.

The [controller] parameter is the controller that manages the window.

The [builder] parameter is a function that builds the content of the window.

{@macro flutter.widgets.windowing.experimental}

### controller

```dart
BaseWindowController controller
```

The controller that manages the window.

{@macro flutter.widgets.windowing.experimental}

### builder

```dart
WidgetBuilder builder
```

The builder function that builds the content of the window.

{@macro flutter.widgets.windowing.experimental}

# WindowManager

```dart
class WindowManager extends StatefulWidget {}
```

The window manager provides a convenient way to render windows at the root of an application.

Descendents of the [WindowManager] may access the [WindowRegistry] via [WindowRegistry.maybeOf] in order to register new windows. [WindowManager] listens on the [WindowRegistry] and renders the new windows using the appropriate window widget as they are added or removed.

If windowing is not enabled, this widgets renders [child] directly and does not provide the [WindowRegistry].

{@tool dartpad} An example usage might look like this, where the window manager wraps the root of the widget tree so that dialogs can be rendered at the same level as a [RegularWindow].

** See code in examples/api/lib/widgets/windows/window_manager.0.dart ** {@end-tool}

{@macro flutter.widgets.windowing.experimental}

See also:

- [WindowRegistry], where window entries can be registered.

### WindowManager()

```dart
WindowManager({dynamic key, required Widget child})
```

Creates a window manager.

The [child] is the content inside of the window manager.

{@macro flutter.widgets.windowing.experimental}

### child

```dart
Widget child
```

The child widget of the window manager.

### createState()

```dart
State<WindowManager> createState()
```
