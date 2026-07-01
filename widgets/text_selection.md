@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# ToolbarBuilder

```dart
typedef ToolbarBuilder = Widget Function(BuildContext context, Widget child)
```

The type for a Function that builds a toolbar's container with the given child.

See also:

- [TextSelectionToolbar.toolbarBuilder], which is of this type. type.
- [CupertinoTextSelectionToolbar.toolbarBuilder], which is similar, but for a Cupertino-style toolbar.

# ToolbarItemsParentData

```dart
class ToolbarItemsParentData extends ContainerBoxParentData<RenderBox> {}
```

ParentData that determines whether or not to paint the corresponding child.

Used in the layout of the Cupertino and Material text selection menus, which decide whether or not to paint their buttons after laying them out and determining where they overflow.

### shouldPaint

```dart
bool shouldPaint
```

Whether or not this child is painted.

Children in the selection toolbar may be laid out for measurement purposes but not painted. This allows these children to be identified.

### toString()

```dart
String toString()
```

# TextSelectionControls

```dart
abstract class TextSelectionControls {}
```

An interface for building the selection UI, to be provided by the implementer of the toolbar widget.

Parts of this class, including [buildToolbar], have been deprecated in favor of [EditableText.contextMenuBuilder], which is now the preferred way to customize the context menus.

## Use with [EditableText.contextMenuBuilder]

For backwards compatibility during the deprecation period, when [EditableText.selectionControls] is set to an object that does not mix in [TextSelectionHandleControls], [EditableText.contextMenuBuilder] is ignored in favor of the deprecated [buildToolbar].

To migrate code from [buildToolbar] to the preferred [EditableText.contextMenuBuilder], while still using [buildHandle], mix in [TextSelectionHandleControls] into the [TextSelectionControls] subclass when moving any toolbar code to a callback passed to [EditableText.contextMenuBuilder].

In due course, [buildToolbar] will be removed, and the mixin will no longer be necessary as a way to flag to the framework that the code has been migrated and does not expect [buildToolbar] to be called.

For more information, see <https://docs.flutter.dev/release/breaking-changes/context-menus>.

See also:

- [SelectionArea], which selects appropriate text selection controls based on the current platform.

### buildHandle()

```dart
Widget buildHandle(BuildContext context, TextSelectionHandleType type, double textLineHeight, [VoidCallback? onTap])
```

Builds a selection handle of the given `type`.

The top left corner of this widget is positioned at the bottom of the selection position.

The supplied [onTap] should be invoked when the handle is tapped, if such interaction is allowed. As a counterexample, the default selection handle on iOS [cupertinoTextSelectionControls] does not call [onTap] at all, since its handles are not meant to be tapped.

### getHandleAnchor()

```dart
Offset getHandleAnchor(TextSelectionHandleType type, double textLineHeight)
```

Get the anchor point of the handle relative to itself. The anchor point is the point that is aligned with a specific point in the text. A handle often visually "points to" that location.

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

Builds a toolbar near a text selection.

Typically displays buttons for copying and pasting text.

The [globalEditableRegion] parameter is the TextField size of the global coordinate system in logical pixels.

The [textLineHeight] parameter is the [RenderEditable.preferredLineHeight] of the [RenderEditable] we are building a toolbar for.

The [selectionMidpoint] parameter is a general calculation midpoint parameter of the toolbar. More detailed position information is computable from the [endpoints] parameter.

### getHandleSize()

```dart
Size getHandleSize(double textLineHeight)
```

Returns the size of the selection handle.

### canCut()

```dart
bool canCut(TextSelectionDelegate delegate)
```

Whether the current selection of the text field managed by the given `delegate` can be removed from the text field and placed into the [Clipboard].

By default, false is returned when nothing is selected in the text field.

Subclasses can use this to decide if they should expose the cut functionality to the user.

### canCopy()

```dart
bool canCopy(TextSelectionDelegate delegate)
```

Whether the current selection of the text field managed by the given `delegate` can be copied to the [Clipboard].

By default, false is returned when nothing is selected in the text field.

Subclasses can use this to decide if they should expose the copy functionality to the user.

### canPaste()

```dart
bool canPaste(TextSelectionDelegate delegate)
```

Whether the text field managed by the given `delegate` supports pasting from the clipboard.

Subclasses can use this to decide if they should expose the paste functionality to the user.

This does not consider the contents of the clipboard. Subclasses may want to, for example, disallow pasting when the clipboard contains an empty string.

### canSelectAll()

```dart
bool canSelectAll(TextSelectionDelegate delegate)
```

Whether the current selection of the text field managed by the given `delegate` can be extended to include the entire content of the text field.

Subclasses can use this to decide if they should expose the select all functionality to the user.

### handleCut()

```dart
void handleCut(TextSelectionDelegate delegate)
```

Call [TextSelectionDelegate.cutSelection] to cut current selection.

This is called by subclasses when their cut affordance is activated by the user.

### handleCopy()

```dart
void handleCopy(TextSelectionDelegate delegate)
```

Call [TextSelectionDelegate.copySelection] to copy current selection.

This is called by subclasses when their copy affordance is activated by the user.

### handlePaste()

```dart
Future<void> handlePaste(TextSelectionDelegate delegate)
```

Call [TextSelectionDelegate.pasteText] to paste text.

This is called by subclasses when their paste affordance is activated by the user.

This function is asynchronous since interacting with the clipboard is asynchronous. Race conditions may exist with this API as currently implemented.

### handleSelectAll()

```dart
void handleSelectAll(TextSelectionDelegate delegate)
```

Call [TextSelectionDelegate.selectAll] to set the current selection to contain the entire text value.

Does not hide the toolbar.

This is called by subclasses when their select-all affordance is activated by the user.

# EmptyTextSelectionControls

```dart
class EmptyTextSelectionControls extends TextSelectionControls {}
```

Text selection controls that do not show any toolbars or handles.

This is a placeholder, suitable for temporary use during development, but not practical for production. For example, it provides no way for the user to interact with selections: no context menus on desktop, no toolbars or drag handles on mobile, etc. For production, consider using [MaterialTextSelectionControls] or creating a custom subclass of [TextSelectionControls].

The [emptyTextSelectionControls] global variable has a suitable instance of this class.

### getHandleSize()

```dart
Size getHandleSize(double textLineHeight)
```

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

### buildHandle()

```dart
Widget buildHandle(BuildContext context, TextSelectionHandleType type, double textLineHeight, [VoidCallback? onTap])
```

### getHandleAnchor()

```dart
Offset getHandleAnchor(TextSelectionHandleType type, double textLineHeight)
```

# emptyTextSelectionControls

```dart
TextSelectionControls emptyTextSelectionControls
```

Text selection controls that do not show any toolbars or handles.

This is a placeholder, suitable for temporary use during development, but not practical for production. For example, it provides no way for the user to interact with selections: no context menus on desktop, no toolbars or drag handles on mobile, etc. For production, consider using [materialTextSelectionControls] or creating a custom subclass of [TextSelectionControls].

# TextSelectionOverlay

```dart
class TextSelectionOverlay {}
```

An object that manages a pair of text selection handles for a [RenderEditable].

This class is a wrapper of [SelectionOverlay] to provide APIs specific for [RenderEditable]s. To manage selection handles for custom widgets, use [SelectionOverlay] instead.

### TextSelectionOverlay()

```dart
TextSelectionOverlay({required TextEditingValue value, required BuildContext context, Widget? debugRequiredFor, required LayerLink toolbarLayerLink, required LayerLink startHandleLayerLink, required LayerLink endHandleLayerLink, required RenderEditable renderObject, TextSelectionControls? selectionControls, bool handlesVisible = false, required TextSelectionDelegate selectionDelegate, DragStartBehavior dragStartBehavior = DragStartBehavior.start, VoidCallback? onSelectionHandleTapped, ClipboardStatusNotifier? clipboardStatus, WidgetBuilder? contextMenuBuilder, required TextMagnifierConfiguration magnifierConfiguration})
```

Creates an object that manages overlay entries for selection handles.

The [context] must have an [Overlay] as an ancestor.

### context

```dart
BuildContext context
```

{@template flutter.widgets.SelectionOverlay.context} The context in which the selection UI should appear.

This context must have an [Overlay] as an ancestor because this object will display the text selection handles in that [Overlay]. {@endtemplate}

### renderObject

```dart
RenderEditable renderObject
```

The editable line in which the selected text is being displayed.

### selectionControls

```dart
TextSelectionControls? selectionControls
```

{@macro flutter.widgets.SelectionOverlay.selectionControls}

### selectionDelegate

```dart
TextSelectionDelegate selectionDelegate
```

{@macro flutter.widgets.SelectionOverlay.selectionDelegate}

### contextMenuBuilder

```dart
WidgetBuilder? contextMenuBuilder
```

{@macro flutter.widgets.EditableText.contextMenuBuilder}

If not provided, no context menu will be built.

### value

```dart
TextEditingValue get value
```

Retrieve current value.

### handlesVisible

```dart
bool get handlesVisible
```

Whether selection handles are visible.

Set to false if you want to hide the handles. Use this property to show or hide the handle without rebuilding them.

Defaults to false.

### handlesVisible

```dart
set handlesVisible(bool visible)
```

### showHandles()

```dart
void showHandles()
```

{@macro flutter.widgets.SelectionOverlay.showHandles}

### hideHandles()

```dart
void hideHandles()
```

{@macro flutter.widgets.SelectionOverlay.hideHandles}

### showToolbar()

```dart
void showToolbar()
```

{@macro flutter.widgets.SelectionOverlay.showToolbar}

This method requires a fully laid-out render tree (as it calls [RenderBox.localToGlobal]), so it should not be called during the build or layout phases.

### showSpellCheckSuggestionsToolbar()

```dart
void showSpellCheckSuggestionsToolbar(WidgetBuilder spellCheckSuggestionsToolbarBuilder)
```

Shows toolbar with spell check suggestions of misspelled words that are available for click-and-replace.

### showMagnifier()

```dart
void showMagnifier(Offset positionToShow)
```

{@macro flutter.widgets.SelectionOverlay.showMagnifier}

### updateMagnifier()

```dart
void updateMagnifier(Offset positionToShow)
```

{@macro flutter.widgets.SelectionOverlay.updateMagnifier}

### hideMagnifier()

```dart
void hideMagnifier()
```

{@macro flutter.widgets.SelectionOverlay.hideMagnifier}

### update()

```dart
void update(TextEditingValue newValue)
```

Updates the overlay after the selection has changed.

If this method is called while the [SchedulerBinding.schedulerPhase] is [SchedulerPhase.persistentCallbacks], i.e. during the build, layout, or paint phases (see [WidgetsBinding.drawFrame]), then the update is delayed until the post-frame callbacks phase. Otherwise the update is done synchronously. This means that it is safe to call during builds, but also that if you do call this during a build, the UI will not update until the next frame (i.e. many milliseconds later).

### updateForScroll()

```dart
void updateForScroll()
```

Causes the overlay to update its rendering.

This is intended to be called when the [renderObject] may have changed its text metrics (e.g. because the text was scrolled).

### handlesAreVisible

```dart
bool get handlesAreVisible
```

Whether the handles are currently visible.

### toolbarIsVisible

```dart
bool get toolbarIsVisible
```

{@macro flutter.widgets.SelectionOverlay.toolbarIsVisible}

See also:

- [spellCheckToolbarIsVisible], which is only whether the spell check menu specifically is visible.

### magnifierIsVisible

```dart
bool get magnifierIsVisible
```

{@macro flutter.widgets.SelectionOverlay.magnifierIsVisible}

### magnifierExists

```dart
bool get magnifierExists
```

{@macro flutter.widgets.SelectionOverlay.magnifierExists}

### spellCheckToolbarIsVisible

```dart
bool get spellCheckToolbarIsVisible
```

Whether the spell check menu is currently visible.

See also:

- [toolbarIsVisible], which is whether any toolbar is visible.

### hide()

```dart
void hide()
```

{@macro flutter.widgets.SelectionOverlay.hide}

### hideToolbar()

```dart
void hideToolbar()
```

{@macro flutter.widgets.SelectionOverlay.hideToolbar}

### dispose()

```dart
void dispose()
```

{@macro flutter.widgets.SelectionOverlay.dispose}

# SelectionOverlay

```dart
class SelectionOverlay {}
```

An object that manages a pair of selection handles and a toolbar.

The selection handles are displayed in the [Overlay] that most closely encloses the given [BuildContext].

### SelectionOverlay()

```dart
SelectionOverlay({required BuildContext context, Widget? debugRequiredFor, required TextSelectionHandleType startHandleType, required double lineHeightAtStart, ValueListenable<bool>? startHandlesVisible, ValueChanged<DragStartDetails>? onStartHandleDragStart, ValueChanged<DragUpdateDetails>? onStartHandleDragUpdate, ValueChanged<DragEndDetails>? onStartHandleDragEnd, required TextSelectionHandleType endHandleType, required double lineHeightAtEnd, ValueListenable<bool>? endHandlesVisible, ValueChanged<DragStartDetails>? onEndHandleDragStart, ValueChanged<DragUpdateDetails>? onEndHandleDragUpdate, ValueChanged<DragEndDetails>? onEndHandleDragEnd, ValueListenable<bool>? toolbarVisible, required List<TextSelectionPoint> selectionEndpoints, required TextSelectionControls? selectionControls, required TextSelectionDelegate? selectionDelegate, required ClipboardStatusNotifier? clipboardStatus, required LayerLink startHandleLayerLink, required LayerLink endHandleLayerLink, required LayerLink toolbarLayerLink, DragStartBehavior dragStartBehavior = DragStartBehavior.start, VoidCallback? onSelectionHandleTapped, Offset? toolbarLocation, TextMagnifierConfiguration magnifierConfiguration = TextMagnifierConfiguration.disabled})
```

Creates an object that manages overlay entries for selection handles.

The [context] must have an [Overlay] as an ancestor.

### context

```dart
BuildContext context
```

{@macro flutter.widgets.SelectionOverlay.context}

### magnifierConfiguration

```dart
TextMagnifierConfiguration magnifierConfiguration
```

The configuration for the magnifier.

By default, [SelectionOverlay]'s [TextMagnifierConfiguration] is disabled.

{@macro flutter.widgets.magnifier.intro}

### toolbarIsVisible

```dart
bool get toolbarIsVisible
```

{@template flutter.widgets.SelectionOverlay.toolbarIsVisible} Whether the toolbar is currently visible.

Includes both the text selection toolbar and the spell check menu. {@endtemplate}

### magnifierIsVisible

```dart
bool get magnifierIsVisible
```

{@template flutter.widgets.SelectionOverlay.magnifierIsVisible} Whether the magnifier is currently visible. {@endtemplate}

### magnifierExists

```dart
bool get magnifierExists
```

{@template flutter.widgets.SelectionOverlay.magnifierExists} Whether the magnifier currently exists.

This differs from [magnifierIsVisible] in that the magnifier may exist in the overlay, but not be shown. {@endtemplate}

### showMagnifier()

```dart
void showMagnifier(MagnifierInfo initialMagnifierInfo)
```

{@template flutter.widgets.SelectionOverlay.showMagnifier} Shows the magnifier, and hides the toolbar if it was showing when [showMagnifier] was called. This is safe to call on platforms not mobile, since a magnifierBuilder will not be provided, or the magnifierBuilder will return null on platforms not mobile.

This is NOT the source of truth for if the magnifier is up or not, since magnifiers may hide themselves. If this info is needed, check [MagnifierController.shown]. {@endtemplate}

### hideMagnifier()

```dart
void hideMagnifier()
```

{@template flutter.widgets.SelectionOverlay.hideMagnifier} Hide the current magnifier.

This does nothing if there is no magnifier. {@endtemplate}

### startHandleType

```dart
TextSelectionHandleType get startHandleType
```

The type of start selection handle.

Changing the value while the handles are visible causes them to rebuild.

### startHandleType

```dart
set startHandleType(TextSelectionHandleType value)
```

### lineHeightAtStart

```dart
double get lineHeightAtStart
```

The line height at the selection start.

This value is used for calculating the size of the start selection handle.

Changing the value while the handles are visible causes them to rebuild.

### lineHeightAtStart

```dart
set lineHeightAtStart(double value)
```

### isDraggingStartHandle

```dart
bool get isDraggingStartHandle
```

Whether the selection start handle is currently being dragged.

### startHandlesVisible

```dart
ValueListenable<bool>? startHandlesVisible
```

Whether the start handle is visible.

If the value changes, the start handle uses [FadeTransition] to transition itself on and off the screen.

If this is null, the start selection handle will always be visible.

### onStartHandleDragStart

```dart
ValueChanged<DragStartDetails>? onStartHandleDragStart
```

Called when the users start dragging the start selection handles.

### onStartHandleDragUpdate

```dart
ValueChanged<DragUpdateDetails>? onStartHandleDragUpdate
```

Called when the users drag the start selection handles to new locations.

### onStartHandleDragEnd

```dart
ValueChanged<DragEndDetails>? onStartHandleDragEnd
```

Called when the users lift their fingers after dragging the start selection handles.

### endHandleType

```dart
TextSelectionHandleType get endHandleType
```

The type of end selection handle.

Changing the value while the handles are visible causes them to rebuild.

### endHandleType

```dart
set endHandleType(TextSelectionHandleType value)
```

### lineHeightAtEnd

```dart
double get lineHeightAtEnd
```

The line height at the selection end.

This value is used for calculating the size of the end selection handle.

Changing the value while the handles are visible causes them to rebuild.

### lineHeightAtEnd

```dart
set lineHeightAtEnd(double value)
```

### isDraggingEndHandle

```dart
bool get isDraggingEndHandle
```

Whether the selection end handle is currently being dragged.

### endHandlesVisible

```dart
ValueListenable<bool>? endHandlesVisible
```

Whether the end handle is visible.

If the value changes, the end handle uses [FadeTransition] to transition itself on and off the screen.

If this is null, the end selection handle will always be visible.

### onEndHandleDragStart

```dart
ValueChanged<DragStartDetails>? onEndHandleDragStart
```

Called when the users start dragging the end selection handles.

### onEndHandleDragUpdate

```dart
ValueChanged<DragUpdateDetails>? onEndHandleDragUpdate
```

Called when the users drag the end selection handles to new locations.

### onEndHandleDragEnd

```dart
ValueChanged<DragEndDetails>? onEndHandleDragEnd
```

Called when the users lift their fingers after dragging the end selection handles.

### toolbarVisible

```dart
ValueListenable<bool>? toolbarVisible
```

Whether the toolbar is visible.

If the value changes, the toolbar uses [FadeTransition] to transition itself on and off the screen.

If this is null the toolbar will always be visible.

### selectionEndpoints

```dart
List<TextSelectionPoint> get selectionEndpoints
```

The text selection positions of selection start and end.

### selectionEndpoints

```dart
set selectionEndpoints(List<TextSelectionPoint> value)
```

### debugRequiredFor

```dart
Widget? debugRequiredFor
```

Debugging information for explaining why the [Overlay] is required.

### toolbarLayerLink

```dart
LayerLink toolbarLayerLink
```

The object supplied to the [CompositedTransformTarget] that wraps the text field.

### startHandleLayerLink

```dart
LayerLink startHandleLayerLink
```

The objects supplied to the [CompositedTransformTarget] that wraps the location of start selection handle.

### endHandleLayerLink

```dart
LayerLink endHandleLayerLink
```

The objects supplied to the [CompositedTransformTarget] that wraps the location of end selection handle.

### selectionControls

```dart
TextSelectionControls? selectionControls
```

{@template flutter.widgets.SelectionOverlay.selectionControls} Builds text selection handles and toolbar. {@endtemplate}

### selectionDelegate

```dart
TextSelectionDelegate? selectionDelegate
```

{@template flutter.widgets.SelectionOverlay.selectionDelegate} The delegate for manipulating the current selection in the owning text field. {@endtemplate}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

Determines the way that drag start behavior is handled.

If set to [DragStartBehavior.start], handle drag behavior will begin at the position where the drag gesture won the arena. If set to [DragStartBehavior.down] it will begin at the position where a down event is first detected.

In general, setting this to [DragStartBehavior.start] will make drag animation smoother and setting it to [DragStartBehavior.down] will make drag behavior feel slightly more reactive.

By default, the drag start behavior is [DragStartBehavior.start].

See also:

- [DragGestureRecognizer.dragStartBehavior], which gives an example for the different behaviors.

### onSelectionHandleTapped

```dart
VoidCallback? onSelectionHandleTapped
```

{@template flutter.widgets.SelectionOverlay.onSelectionHandleTapped} A callback that's optionally invoked when a selection handle is tapped.

The [TextSelectionControls.buildHandle] implementation the text field uses decides where the handle's tap "hotspot" is, or whether the selection handle supports tap gestures at all. For instance, [MaterialTextSelectionControls] calls [onSelectionHandleTapped] when the selection handle's "knob" is tapped, while [CupertinoTextSelectionControls] builds a handle that's not sufficiently large for tapping (as it's not meant to be tapped) so it does not call [onSelectionHandleTapped] even when tapped. {@endtemplate}

### clipboardStatus

```dart
ClipboardStatusNotifier? clipboardStatus
```

Maintains the status of the clipboard for determining if its contents can be pasted or not.

Useful because the actual value of the clipboard can only be checked asynchronously (see [Clipboard.getData]).

### toolbarLocation

```dart
Offset? get toolbarLocation
```

The location of where the toolbar should be drawn in relative to the location of [toolbarLayerLink].

If this is null, the toolbar is drawn based on [selectionEndpoints] and the rect of render object of [context].

This is useful for displaying toolbars at the mouse right-click locations in desktop devices.

### toolbarLocation

```dart
set toolbarLocation(Offset? value)
```

### fadeDuration

```dart
Duration fadeDuration
```

Controls the fade-in and fade-out animations for the toolbar and handles.

### showHandles()

```dart
void showHandles()
```

{@template flutter.widgets.SelectionOverlay.showHandles} Builds the handles by inserting them into the [context]'s overlay. {@endtemplate}

### hideHandles()

```dart
void hideHandles()
```

{@template flutter.widgets.SelectionOverlay.hideHandles} Destroys the handles by removing them from overlay. {@endtemplate}

### showToolbar()

```dart
void showToolbar({BuildContext? context, WidgetBuilder? contextMenuBuilder})
```

{@template flutter.widgets.SelectionOverlay.showToolbar} Shows the toolbar by inserting it into the [context]'s overlay. {@endtemplate}

### showSpellCheckSuggestionsToolbar()

```dart
void showSpellCheckSuggestionsToolbar({BuildContext? context, required WidgetBuilder builder})
```

Shows toolbar with spell check suggestions of misspelled words that are available for click-and-replace.

### markNeedsBuild()

```dart
void markNeedsBuild()
```

Rebuilds the selection toolbar or handles if they are present.

### hide()

```dart
void hide()
```

{@template flutter.widgets.SelectionOverlay.hide} Hides the entire overlay including the toolbar and the handles. {@endtemplate}

### hideToolbar()

```dart
void hideToolbar()
```

{@template flutter.widgets.SelectionOverlay.hideToolbar} Hides the toolbar part of the overlay.

To hide the whole overlay, see [hide]. {@endtemplate}

### dispose()

```dart
void dispose()
```

{@template flutter.widgets.SelectionOverlay.dispose} Disposes this object and release resources. {@endtemplate}

### updateMagnifier()

```dart
void updateMagnifier(MagnifierInfo magnifierInfo)
```

{@template flutter.widgets.SelectionOverlay.updateMagnifier} Update the current magnifier with new selection data, so the magnifier can respond accordingly.

If the magnifier is not shown, this still updates the magnifier position because the magnifier may have hidden itself and is looking for a cue to reshow itself.

If there is no magnifier in the overlay, this does nothing. {@endtemplate}

# TextSelectionGestureDetectorBuilderDelegate

```dart
abstract class TextSelectionGestureDetectorBuilderDelegate {}
```

Delegate interface for the [TextSelectionGestureDetectorBuilder].

The interface is usually implemented by the [State] of text field implementations wrapping [EditableText], so that they can use a [TextSelectionGestureDetectorBuilder] to build a [TextSelectionGestureDetector] for their [EditableText]. The delegate provides the builder with information about the current state of the text field. Based on that information, the builder adds the correct gesture handlers to the gesture detector.

See also:

- [TextField], which implements this delegate for the Material text field.
- [CupertinoTextField], which implements this delegate for the Cupertino text field.

### editableTextKey

```dart
GlobalKey<EditableTextState> get editableTextKey
```

[GlobalKey] to the [EditableText] for which the [TextSelectionGestureDetectorBuilder] will build a [TextSelectionGestureDetector].

### forcePressEnabled

```dart
bool get forcePressEnabled
```

Whether the text field should respond to force presses.

### selectionEnabled

```dart
bool get selectionEnabled
```

Whether the user may select text in the text field.

# TextSelectionGestureDetectorBuilder

```dart
class TextSelectionGestureDetectorBuilder {}
```

Builds a [TextSelectionGestureDetector] to wrap an [EditableText].

The class implements sensible defaults for many user interactions with an [EditableText] (see the documentation of the various gesture handler methods, e.g. [onTapDown], [onForcePressStart], etc.). Subclasses of [TextSelectionGestureDetectorBuilder] can change the behavior performed in responds to these gesture events by overriding the corresponding handler methods of this class.

The resulting [TextSelectionGestureDetector] to wrap an [EditableText] is obtained by calling [buildGestureDetector].

A [TextSelectionGestureDetectorBuilder] must be provided a [TextSelectionGestureDetectorBuilderDelegate], from which information about the [EditableText] may be obtained. Typically, the [State] of the widget that builds the [EditableText] implements this interface, and then passes itself as the [delegate].

See also:

- [TextField], which uses a subclass to implement the Material-specific gesture logic of an [EditableText].
- [CupertinoTextField], which uses a subclass to implement the Cupertino-specific gesture logic of an [EditableText].

### TextSelectionGestureDetectorBuilder()

```dart
TextSelectionGestureDetectorBuilder({required TextSelectionGestureDetectorBuilderDelegate delegate})
```

Creates a [TextSelectionGestureDetectorBuilder].

### delegate

```dart
TextSelectionGestureDetectorBuilderDelegate delegate
```

The delegate for this [TextSelectionGestureDetectorBuilder].

The delegate provides the builder with information about what actions can currently be performed on the text field. Based on this, the builder adds the correct gesture handlers to the gesture detector.

Typically implemented by a [State] of a widget that builds an [EditableText].

### shouldShowSelectionToolbar

```dart
bool get shouldShowSelectionToolbar
```

Whether to show the selection toolbar.

It is based on the signal source when [onTapDown], [onSecondaryTapDown], [onDragSelectionStart], or [onForcePressStart] is called. This getter will return true if the current [onTapDown], or [onDragSelectionStart] event is triggered by a touch or a stylus. It will always return true for the current [onSecondaryTapDown] or [onForcePressStart] event.

### shouldShowSelectionHandles

```dart
bool get shouldShowSelectionHandles
```

Whether to show the selection handles.

It is based on the signal source when [onTapDown], [onSecondaryTapDown], [onDragSelectionStart], is called. This getter will return true if the current [onTapDown], [onSecondaryTapDown], or [onDragSelectionStart] event is triggered by a touch or a stylus.

### editableText

```dart
EditableTextState get editableText
```

The [State] of the [EditableText] for which the builder will provide a [TextSelectionGestureDetector].

### renderEditable

```dart
RenderEditable get renderEditable
```

The [RenderObject] of the [EditableText] for which the builder will provide a [TextSelectionGestureDetector].

### onTapTrackStart()

```dart
void onTapTrackStart()
```

Handler for [TextSelectionGestureDetector.onTapTrackStart].

See also:

- [TextSelectionGestureDetector.onTapTrackStart], which triggers this callback.

### onTapTrackReset()

```dart
void onTapTrackReset()
```

Handler for [TextSelectionGestureDetector.onTapTrackReset].

See also:

- [TextSelectionGestureDetector.onTapTrackReset], which triggers this callback.

### onTapDown()

```dart
void onTapDown(TapDragDownDetails details)
```

Handler for [TextSelectionGestureDetector.onTapDown].

By default, it forwards the tap to [RenderEditable.handleTapDown] and sets [shouldShowSelectionToolbar] to true if the tap was initiated by a finger or stylus.

See also:

- [TextSelectionGestureDetector.onTapDown], which triggers this callback.

### onForcePressStart()

```dart
void onForcePressStart(ForcePressDetails details)
```

Handler for [TextSelectionGestureDetector.onForcePressStart].

By default, it selects the word at the position of the force press, if selection is enabled.

This callback is only applicable when force press is enabled.

See also:

- [TextSelectionGestureDetector.onForcePressStart], which triggers this callback.

### onForcePressEnd()

```dart
void onForcePressEnd(ForcePressDetails details)
```

Handler for [TextSelectionGestureDetector.onForcePressEnd].

By default, it selects words in the range specified in [details] and shows toolbar if it is necessary.

This callback is only applicable when force press is enabled.

See also:

- [TextSelectionGestureDetector.onForcePressEnd], which triggers this callback.

### onUserTapAlwaysCalled

```dart
bool get onUserTapAlwaysCalled
```

Whether the provided [onUserTap] callback should be dispatched on every tap or only non-consecutive taps.

Defaults to false.

### onUserTap()

```dart
void onUserTap()
```

Handler for [TextSelectionGestureDetector.onUserTap].

By default, it serves as placeholder to enable subclass override.

See also:

- [TextSelectionGestureDetector.onUserTap], which triggers this callback.
- [TextSelectionGestureDetector.onUserTapAlwaysCalled], which controls whether this callback is called only on the first tap in a series of taps.

### onSingleTapUp()

```dart
void onSingleTapUp(TapDragUpDetails details)
```

Handler for [TextSelectionGestureDetector.onSingleTapUp].

By default, it selects word edge if selection is enabled.

See also:

- [TextSelectionGestureDetector.onSingleTapUp], which triggers this callback.

### onSingleTapCancel()

```dart
void onSingleTapCancel()
```

Handler for [TextSelectionGestureDetector.onSingleTapCancel].

By default, it serves as placeholder to enable subclass override.

See also:

- [TextSelectionGestureDetector.onSingleTapCancel], which triggers this callback.

### onSingleLongTapStart()

```dart
void onSingleLongTapStart(LongPressStartDetails details)
```

Handler for [TextSelectionGestureDetector.onSingleLongTapStart].

By default, it selects text position specified in [details] if selection is enabled.

See also:

- [TextSelectionGestureDetector.onSingleLongTapStart], which triggers this callback.

### onSingleLongTapMoveUpdate()

```dart
void onSingleLongTapMoveUpdate(LongPressMoveUpdateDetails details)
```

Handler for [TextSelectionGestureDetector.onSingleLongTapMoveUpdate].

By default, it updates the selection location specified in [details] if selection is enabled.

See also:

- [TextSelectionGestureDetector.onSingleLongTapMoveUpdate], which triggers this callback.

### onSingleLongTapEnd()

```dart
void onSingleLongTapEnd(LongPressEndDetails details)
```

Handler for [TextSelectionGestureDetector.onSingleLongTapEnd].

By default, it shows toolbar if necessary.

See also:

- [TextSelectionGestureDetector.onSingleLongTapEnd], which triggers this callback.

### onSingleLongTapCancel()

```dart
void onSingleLongTapCancel()
```

Handler for [TextSelectionGestureDetector.onSingleLongTapCancel].

By default, it hides the magnifier and the floating cursor if necessary.

See also:

- [TextSelectionGestureDetector.onSingleLongTapCancel], which triggers this callback.

### onSecondaryTap()

```dart
void onSecondaryTap()
```

Handler for [TextSelectionGestureDetector.onSecondaryTap].

By default, selects the word if possible and shows the toolbar.

### onSecondaryTapDown()

```dart
void onSecondaryTapDown(TapDownDetails details)
```

Handler for [TextSelectionGestureDetector.onSecondaryTapDown].

See also:

- [TextSelectionGestureDetector.onSecondaryTapDown], which triggers this callback.
- [onSecondaryTap], which is typically called after this.

### onDoubleTapDown()

```dart
void onDoubleTapDown(TapDragDownDetails details)
```

Handler for [TextSelectionGestureDetector.onDoubleTapDown].

By default, it selects a word through [RenderEditable.selectWord] if selectionEnabled and shows toolbar if necessary.

See also:

- [TextSelectionGestureDetector.onDoubleTapDown], which triggers this callback.

### onTripleTapDown()

```dart
void onTripleTapDown(TapDragDownDetails details)
```

Handler for [TextSelectionGestureDetector.onTripleTapDown].

By default, it selects a paragraph if [TextSelectionGestureDetectorBuilderDelegate.selectionEnabled] is true and shows the toolbar if necessary.

See also:

- [TextSelectionGestureDetector.onTripleTapDown], which triggers this callback.

### onDragSelectionStart()

```dart
void onDragSelectionStart(TapDragStartDetails details)
```

Handler for [TextSelectionGestureDetector.onDragSelectionStart].

By default, it selects a text position specified in [details].

See also:

- [TextSelectionGestureDetector.onDragSelectionStart], which triggers this callback.

### onDragSelectionUpdate()

```dart
void onDragSelectionUpdate(TapDragUpdateDetails details)
```

Handler for [TextSelectionGestureDetector.onDragSelectionUpdate].

By default, it updates the selection location specified in the provided details objects.

See also:

- [TextSelectionGestureDetector.onDragSelectionUpdate], which triggers this callback./lib/src/material/text_field.dart

### onDragSelectionEnd()

```dart
void onDragSelectionEnd(TapDragEndDetails details)
```

Handler for [TextSelectionGestureDetector.onDragSelectionEnd].

By default, it cleans up the state used for handling certain built-in behaviors.

See also:

- [TextSelectionGestureDetector.onDragSelectionEnd], which triggers this callback.

### buildGestureDetector()

```dart
Widget buildGestureDetector({Key? key, HitTestBehavior? behavior, required Widget child})
```

Returns a [TextSelectionGestureDetector] configured with the handlers provided by this builder.

The [child] or its subtree should contain an [EditableText] whose key is the [GlobalKey] provided by the [delegate]'s [TextSelectionGestureDetectorBuilderDelegate.editableTextKey].

# TextSelectionGestureDetector

```dart
class TextSelectionGestureDetector extends StatefulWidget {}
```

A gesture detector to respond to non-exclusive event chains for a text field.

An ordinary [GestureDetector] configured to handle events like tap and double tap will only recognize one or the other. This widget detects both: the first tap and then any subsequent taps that occurs within a time limit after the first.

See also:

- [TextField], a Material text field which uses this gesture detector.
- [CupertinoTextField], a Cupertino text field which uses this gesture detector.

### TextSelectionGestureDetector()

```dart
TextSelectionGestureDetector({dynamic key, VoidCallback? onTapTrackStart, VoidCallback? onTapTrackReset, GestureTapDragDownCallback? onTapDown, GestureForcePressStartCallback? onForcePressStart, GestureForcePressEndCallback? onForcePressEnd, GestureTapCallback? onSecondaryTap, GestureTapDownCallback? onSecondaryTapDown, GestureTapDragUpCallback? onSingleTapUp, GestureCancelCallback? onSingleTapCancel, GestureTapCallback? onUserTap, GestureLongPressStartCallback? onSingleLongTapStart, GestureLongPressMoveUpdateCallback? onSingleLongTapMoveUpdate, GestureLongPressEndCallback? onSingleLongTapEnd, GestureLongPressCancelCallback? onSingleLongTapCancel, GestureTapDragDownCallback? onDoubleTapDown, GestureTapDragDownCallback? onTripleTapDown, GestureTapDragStartCallback? onDragSelectionStart, GestureTapDragUpdateCallback? onDragSelectionUpdate, GestureTapDragEndCallback? onDragSelectionEnd, bool onUserTapAlwaysCalled = false, HitTestBehavior? behavior, required Widget child})
```

Create a [TextSelectionGestureDetector].

Multiple callbacks can be called for one sequence of input gesture.

### onTapTrackStart

```dart
VoidCallback? onTapTrackStart
```

{@template flutter.gestures.selectionrecognizers.TextSelectionGestureDetector.onTapTrackStart} Callback used to indicate that a tap tracking has started upon a [PointerDownEvent]. {@endtemplate}

### onTapTrackReset

```dart
VoidCallback? onTapTrackReset
```

{@template flutter.gestures.selectionrecognizers.TextSelectionGestureDetector.onTapTrackReset} Callback used to indicate that a tap tracking has been reset which happens on the next [PointerDownEvent] after the timer between two taps elapses, the recognizer loses the arena, the gesture is cancelled or the recognizer is disposed of. {@endtemplate}

### onTapDown

```dart
GestureTapDragDownCallback? onTapDown
```

Called for every tap down including every tap down that's part of a double click or a long press, except touches that include enough movement to not qualify as taps (e.g. pans and flings).

### onForcePressStart

```dart
GestureForcePressStartCallback? onForcePressStart
```

Called when a pointer has tapped down and the force of the pointer has just become greater than [ForcePressGestureRecognizer.startPressure].

### onForcePressEnd

```dart
GestureForcePressEndCallback? onForcePressEnd
```

Called when a pointer that had previously triggered [onForcePressStart] is lifted off the screen.

### onSecondaryTap

```dart
GestureTapCallback? onSecondaryTap
```

Called for a tap event with the secondary mouse button.

### onSecondaryTapDown

```dart
GestureTapDownCallback? onSecondaryTapDown
```

Called for a tap down event with the secondary mouse button.

### onSingleTapUp

```dart
GestureTapDragUpCallback? onSingleTapUp
```

Called for the first tap in a series of taps, consecutive taps do not call this method.

For example, if the detector was configured with [onTapDown] and [onDoubleTapDown], three quick taps would be recognized as a single tap down, followed by a tap up, then a double tap down, followed by a single tap down.

### onSingleTapCancel

```dart
GestureCancelCallback? onSingleTapCancel
```

Called for each touch that becomes recognized as a gesture that is not a short tap, such as a long tap or drag. It is called at the moment when another gesture from the touch is recognized.

### onUserTap

```dart
GestureTapCallback? onUserTap
```

Called for the first tap in a series of taps when [onUserTapAlwaysCalled] is disabled, which is the default behavior.

When [onUserTapAlwaysCalled] is enabled, this is called for every tap, including consecutive taps.

### onSingleLongTapStart

```dart
GestureLongPressStartCallback? onSingleLongTapStart
```

Called for a single long tap that's sustained for longer than [kLongPressTimeout] but not necessarily lifted. Not called for a double-tap-hold, which calls [onDoubleTapDown] instead.

### onSingleLongTapMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onSingleLongTapMoveUpdate
```

Called after [onSingleLongTapStart] when the pointer is dragged.

### onSingleLongTapEnd

```dart
GestureLongPressEndCallback? onSingleLongTapEnd
```

Called after [onSingleLongTapStart] when the pointer is lifted.

### onSingleLongTapCancel

```dart
GestureLongPressCancelCallback? onSingleLongTapCancel
```

Called after [onSingleLongTapStart] when the pointer is canceled.

### onDoubleTapDown

```dart
GestureTapDragDownCallback? onDoubleTapDown
```

Called after a momentary hold or a short tap that is close in space and time (within [kDoubleTapTimeout]) to a previous short tap.

### onTripleTapDown

```dart
GestureTapDragDownCallback? onTripleTapDown
```

Called after a momentary hold or a short tap that is close in space and time (within [kDoubleTapTimeout]) to a previous double-tap.

### onDragSelectionStart

```dart
GestureTapDragStartCallback? onDragSelectionStart
```

Called when a mouse starts dragging to select text.

### onDragSelectionUpdate

```dart
GestureTapDragUpdateCallback? onDragSelectionUpdate
```

Called repeatedly as a mouse moves while dragging.

### onDragSelectionEnd

```dart
GestureTapDragEndCallback? onDragSelectionEnd
```

Called when a mouse that was previously dragging is released.

### onUserTapAlwaysCalled

```dart
bool onUserTapAlwaysCalled
```

Whether [onUserTap] will be called for all taps including consecutive taps.

Defaults to false, so [onUserTap] is only called for each distinct tap.

### behavior

```dart
HitTestBehavior? behavior
```

How this gesture detector should behave during hit testing.

This defaults to [HitTestBehavior.deferToChild].

### child

```dart
Widget child
```

Child below this widget.

### createState()

```dart
State<StatefulWidget> createState()
```

# ClipboardStatusNotifier

```dart
class ClipboardStatusNotifier extends ValueNotifier<ClipboardStatus> with WidgetsBindingObserver {}
```

A [ValueNotifier] whose [value] indicates whether the current contents of the clipboard can be pasted.

The contents of the clipboard can only be read asynchronously, via [Clipboard.getData], so this maintains a value that can be used synchronously. Call [update] to asynchronously update value if needed.

### ClipboardStatusNotifier()

```dart
ClipboardStatusNotifier({ClipboardStatus value = ClipboardStatus.unknown})
```

Create a new ClipboardStatusNotifier.

### update()

```dart
Future<void> update()
```

Check the [Clipboard] and update [value] if needed.

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### didChangeAppLifecycleState()

```dart
void didChangeAppLifecycleState(AppLifecycleState state)
```

### dispose()

```dart
void dispose()
```

# ClipboardStatus

```dart
enum ClipboardStatus {}
```

An enumeration of the status of the content on the user's clipboard.

The clipboard content can be pasted, such as a String of nonzero length.

The status of the clipboard is unknown. Since getting clipboard data is asynchronous (see [Clipboard.getData]), this status often exists while waiting to receive the clipboard contents for the first time.

The content on the clipboard is not pasteable, such as when it is empty.

# LiveTextInputStatusNotifier

```dart
class LiveTextInputStatusNotifier extends ValueNotifier<LiveTextInputStatus> with WidgetsBindingObserver {}
```

A [ValueNotifier] whose [value] indicates whether the current device supports the Live Text (OCR) function.

See also:

- [LiveText], where the availability of Live Text input can be obtained.
- [LiveTextInputStatus], an enumeration that indicates whether the current device is available for Live Text input.

Call [update] to asynchronously update [value] if needed.

### LiveTextInputStatusNotifier()

```dart
LiveTextInputStatusNotifier({LiveTextInputStatus value = LiveTextInputStatus.unknown})
```

Create a new LiveTextStatusNotifier.

### update()

```dart
Future<void> update()
```

Check the [LiveTextInputStatus] and update [value] if needed.

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### didChangeAppLifecycleState()

```dart
void didChangeAppLifecycleState(AppLifecycleState state)
```

### dispose()

```dart
void dispose()
```

# LiveTextInputStatus

```dart
enum LiveTextInputStatus {}
```

An enumeration that indicates whether the current device is available for Live Text input.

See also:

- [LiveText], where the availability of Live Text input can be obtained.

This device supports Live Text input currently.

The status of the Live Text input is unknown. Since getting the Live Text input availability is asynchronous (see [LiveText.isLiveTextInputAvailable]), this status often exists while waiting to receive the status value for the first time.

The current device doesn't support Live Text input.

# TextSelectionHandleControls

```dart
mixin TextSelectionHandleControls on TextSelectionControls {}
```

[TextSelectionControls] that specifically do not manage the toolbar in order to leave that to [EditableText.contextMenuBuilder].

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

### canCut()

```dart
bool canCut(TextSelectionDelegate delegate)
```

### canCopy()

```dart
bool canCopy(TextSelectionDelegate delegate)
```

### canPaste()

```dart
bool canPaste(TextSelectionDelegate delegate)
```

### canSelectAll()

```dart
bool canSelectAll(TextSelectionDelegate delegate)
```

### handleCut()

```dart
void handleCut(TextSelectionDelegate delegate, [ClipboardStatusNotifier? clipboardStatus])
```

### handleCopy()

```dart
void handleCopy(TextSelectionDelegate delegate, [ClipboardStatusNotifier? clipboardStatus])
```

### handlePaste()

```dart
Future<void> handlePaste(TextSelectionDelegate delegate)
```

### handleSelectAll()

```dart
void handleSelectAll(TextSelectionDelegate delegate)
```
