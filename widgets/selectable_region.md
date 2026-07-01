@docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

@docImport 'editable_text.dart'; @docImport 'text.dart';

# SelectableRegion

```dart
class SelectableRegion extends StatefulWidget {}
```

A widget that introduces an area for user selections.

Flutter widgets are not selectable by default. Wrapping a widget subtree with a [SelectableRegion] widget enables selection for widgets in the subtree that participate in selection. For example, [Text] widgets automatically look for selectable regions to enable selection, while widgets such as [RichText] must be configured with a [SelectionRegistrar] and [RichText.selectionColor]. The wrapped subtree can be selected by users using mouse or touch gestures, e.g. users can select widgets by holding the mouse left-click and dragging across widgets, or they can use long press gestures to select words on touch devices.

A [SelectableRegion] widget requires configuration; in particular specific [selectionControls] must be provided.

The [SelectionArea] widget from the [material] library configures a [SelectableRegion] in a platform-specific manner (e.g. using a Material toolbar on Android, a Cupertino toolbar on iOS), and it may therefore be simpler to use that widget rather than using [SelectableRegion] directly.

## An overview of the selection system.

Every [Selectable] under the [SelectableRegion] can be selected. They form a selection tree structure to handle the selection.

The [SelectableRegion] is a wrapper over [SelectionContainer]. It listens to user gestures and sends corresponding [SelectionEvent]s to the [SelectionContainer] it creates.

A [SelectionContainer] is a single [Selectable] that handles [SelectionEvent]s on behalf of child [Selectable]s in the subtree. It creates a [SelectionRegistrarScope] with its [SelectionContainer.delegate] to collect child [Selectable]s and sends the [SelectionEvent]s it receives from the parent [SelectionRegistrar] to the appropriate child [Selectable]s. It creates an abstraction for the parent [SelectionRegistrar] as if it is interacting with a single [Selectable].

The [SelectionContainer] created by [SelectableRegion] is the root node of a selection tree. Each non-leaf node in the tree is a [SelectionContainer], and the leaf node is a leaf widget whose render object implements [Selectable]. They are connected through [SelectionRegistrarScope]s created by [SelectionContainer]s.

Both [SelectionContainer]s and the leaf [Selectable]s need to register themselves to the [SelectionRegistrar] from the [SelectionContainer.maybeOf] if they want to participate in the selection. The [BuildContext] used with [SelectionContainer.maybeOf] must be below the [SelectionContainer], [SelectableRegion], or [SelectionArea] that provides the registrar in the widget tree.

An example selection tree will look like:

{@tool snippet}

```dart
MaterialApp(
  home: SelectableRegion(
    selectionControls: materialTextSelectionControls,
    child: Scaffold(
      appBar: AppBar(title: const Text('Flutter Code Sample')),
      body: ListView(
        children: const <Widget>[
          Text('Item 0', style: TextStyle(fontSize: 50.0)),
          Text('Item 1', style: TextStyle(fontSize: 50.0)),
        ],
      ),
    ),
  ),
)
```

{@end-tool}

SelectionContainer (SelectableRegion) / \ / \ / \ Selectable \ ("Flutter Code Sample") \ \ SelectionContainer (ListView) / \ / \ / \ Selectable Selectable ("Item 0") ("Item 1")

## Making a widget selectable

Some leaf widgets, such as [Text], have all of the selection logic wired up automatically and can be selected as long as they are under a [SelectableRegion].

To make a custom selectable widget, its render object needs to mix in [Selectable] and implement the required APIs to handle [SelectionEvent]s as well as paint appropriate selection highlights.

The render object also needs to register itself to a [SelectionRegistrar]. For the most cases, one can use [SelectionRegistrant] to auto-register itself with the register returned from [SelectionContainer.maybeOf] as seen in the example below.

{@tool dartpad} This sample demonstrates how to create an adapter widget that makes any child widget selectable.

** See code in examples/api/lib/material/selectable_region/selectable_region.0.dart ** {@end-tool}

## Complex layout

By default, the screen order is used as the selection order. If a group of [Selectable]s needs to select differently, consider wrapping them with a [SelectionContainer] to customize its selection behavior.

{@tool dartpad} This sample demonstrates how to create a [SelectionContainer] that only allows selecting everything or nothing with no partial selection.

** See code in examples/api/lib/material/selection_container/selection_container.0.dart ** {@end-tool}

In the case where a group of widgets should be excluded from selection under a [SelectableRegion], consider wrapping that group of widgets using [SelectionContainer.disabled].

{@tool dartpad} This sample demonstrates how to disable selection for a Text in a Column.

** See code in examples/api/lib/material/selection_container/selection_container_disabled.0.dart ** {@end-tool}

To create a separate selection system from its parent selection area, wrap part of the subtree with another [SelectableRegion]. The selection of the child selection area can not extend past its subtree, and the selection of the parent selection area can not extend inside the child selection area.

## Selection status

A [SelectableRegion]s [SelectableRegionSelectionStatus] is used to indicate whether the [SelectableRegion] is actively changing the selection, or has finalized it. For example, during a mouse click + drag, the [SelectableRegionSelectionStatus] will be set to [SelectableRegionSelectionStatus.changing], and when the mouse click is released the status will be set to [SelectableRegionSelectionStatus.finalized].

The default value of [SelectableRegion]s selection status is [SelectableRegionSelectionStatus.finalized].

To access the [SelectableRegionSelectionStatus] of a parent [SelectableRegion] use [SelectableRegionSelectionStatusScope.maybeOf] and retrieve the value from the [ValueListenable].

One can also listen for changes to the [SelectableRegionSelectionStatus] by adding a listener to the [ValueListenable] retrieved from [SelectableRegionSelectionStatusScope.maybeOf] through [ValueListenable.addListener]. In Stateful widgets this is typically done in [State.didChangeDependencies]. Remove the listener when no longer needed, typically in your Stateful widgets [State.dispose] method through [ValueListenable.removeListener].

## Tests

In a test, a region can be selected either by faking drag events (e.g. using [WidgetTester.dragFrom]) or by sending intents to a widget inside the region that has been given a [GlobalKey], e.g.:

```dart
Actions.invoke(key.currentContext!, const SelectAllTextIntent(SelectionChangedCause.keyboard));
```

See also:

- [SelectionArea], which creates a [SelectableRegion] with platform-adaptive selection controls.
- [SelectableText], which enables selection on a single run of text.
- [SelectionHandler], which contains APIs to handle selection events from the [SelectableRegion].
- [Selectable], which provides API to participate in the selection system.
- [SelectionRegistrar], which [Selectable] needs to subscribe to receive selection events.
- [SelectionContainer], which collects selectable widgets in the subtree and provides api to dispatch selection event to the collected widget.
- [SelectionListener], which enables accessing the [SelectionDetails] of the selectable subtree it wraps.

### SelectableRegion()

```dart
SelectableRegion({dynamic key, SelectableRegionContextMenuBuilder? contextMenuBuilder, FocusNode? focusNode, TextMagnifierConfiguration magnifierConfiguration = TextMagnifierConfiguration.disabled, ValueChanged<SelectedContent?>? onSelectionChanged, required TextSelectionControls selectionControls, required Widget child})
```

Create a new [SelectableRegion] widget.

The [selectionControls] are used for building the selection handles and toolbar for mobile devices.

### magnifierConfiguration

```dart
TextMagnifierConfiguration magnifierConfiguration
```

The configuration for the magnifier used with selections in this region.

By default, [SelectableRegion]'s [TextMagnifierConfiguration] is disabled. For a version of [SelectableRegion] that adapts automatically to the current platform, consider [SelectionArea].

{@macro flutter.widgets.magnifier.intro}

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### child

```dart
Widget child
```

The child widget this selection area applies to.

{@macro flutter.widgets.ProxyWidget.child}

### contextMenuBuilder

```dart
SelectableRegionContextMenuBuilder? contextMenuBuilder
```

{@macro flutter.widgets.EditableText.contextMenuBuilder}

### selectionControls

```dart
TextSelectionControls selectionControls
```

The delegate to build the selection handles and toolbar for mobile devices.

The [emptyTextSelectionControls] global variable provides a default [TextSelectionControls] implementation with no controls.

### onSelectionChanged

```dart
ValueChanged<SelectedContent?>? onSelectionChanged
```

Called when the selected content changes.

### getSelectableButtonItems()

```dart
List<ContextMenuButtonItem> getSelectableButtonItems({required SelectionGeometry selectionGeometry, required VoidCallback onCopy, required VoidCallback onSelectAll, required VoidCallback? onShare})
```

Returns the [ContextMenuButtonItem]s representing the buttons in this platform's default selection menu.

For example, [SelectableRegion] uses this to generate the default buttons for its context menu.

See also:

- [SelectableRegionState.contextMenuButtonItems], which gives the [ContextMenuButtonItem]s for a specific SelectableRegion.
- [EditableText.getEditableButtonItems], which performs a similar role but for content that is both selectable and editable.
- [AdaptiveTextSelectionToolbar], which builds the toolbar itself, and can take a list of [ContextMenuButtonItem]s with [AdaptiveTextSelectionToolbar.buttonItems].
- [AdaptiveTextSelectionToolbar.getAdaptiveButtons], which builds the button Widgets for the current platform given [ContextMenuButtonItem]s.

### createState()

```dart
State<StatefulWidget> createState()
```

# SelectableRegionState

```dart
class SelectableRegionState extends State<SelectableRegion> with TextSelectionDelegate implements SelectionRegistrar {}
```

State for a [SelectableRegion].

### selectionOverlay

```dart
SelectionOverlay? get selectionOverlay
```

The [SelectionOverlay] that is currently visible on the screen.

Can be null if there is no visible [SelectionOverlay].

### initState()

```dart
void initState()
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(SelectableRegion oldWidget)
```

### clearSelection()

```dart
void clearSelection()
```

Removes the ongoing selection for this [SelectableRegion].

### contextMenuAnchors

```dart
TextSelectionToolbarAnchors get contextMenuAnchors
```

{@macro flutter.widgets.EditableText.getAnchors}

See also:

- [contextMenuButtonItems], which provides the [ContextMenuButtonItem]s for the default context menu buttons.

### contextMenuButtonItems

```dart
List<ContextMenuButtonItem> get contextMenuButtonItems
```

Returns the [ContextMenuButtonItem]s representing the buttons in this platform's default selection menu.

See also:

- [SelectableRegion.getSelectableButtonItems], which performs a similar role, but for any selectable text, not just specifically SelectableRegion.
- [EditableTextState.contextMenuButtonItems], which performs a similar role but for content that is not just selectable but also editable.
- [contextMenuAnchors], which provides the anchor points for the default context menu.
- [AdaptiveTextSelectionToolbar], which builds the toolbar itself, and can take a list of [ContextMenuButtonItem]s with [AdaptiveTextSelectionToolbar.buttonItems].
- [AdaptiveTextSelectionToolbar.getAdaptiveButtons], which builds the button Widgets for the current platform given [ContextMenuButtonItem]s.

### startGlyphHeight

```dart
double get startGlyphHeight
```

The line height at the start of the current selection.

### endGlyphHeight

```dart
double get endGlyphHeight
```

The line height at the end of the current selection.

### selectionEndpoints

```dart
List<TextSelectionPoint> get selectionEndpoints
```

Returns the local coordinates of the endpoints of the current selection.

### cutEnabled

```dart
bool get cutEnabled
```

### pasteEnabled

```dart
bool get pasteEnabled
```

### hideToolbar()

```dart
void hideToolbar([bool hideHandles = true])
```

### selectAll()

```dart
void selectAll([SelectionChangedCause? cause])
```

### copySelection()

```dart
void copySelection(SelectionChangedCause cause)
```

### textEditingValue

```dart
TextEditingValue textEditingValue
```

### bringIntoView()

```dart
void bringIntoView(TextPosition position)
```

### cutSelection()

```dart
void cutSelection(SelectionChangedCause cause)
```

### userUpdateTextEditingValue()

```dart
void userUpdateTextEditingValue(TextEditingValue value, SelectionChangedCause cause)
```

### pasteText()

```dart
Future<void> pasteText(SelectionChangedCause cause)
```

### add()

```dart
void add(Selectable selectable)
```

### remove()

```dart
void remove(Selectable selectable)
```

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```

# StaticSelectionContainerDelegate

```dart
class StaticSelectionContainerDelegate extends MultiSelectableSelectionContainerDelegate {}
```

A delegate that manages updating multiple [Selectable] children where the [Selectable]s do not change or move around frequently.

This delegate keeps track of the [Selectable]s that received start or end [SelectionEvent]s and the global locations of those events to accurately synthesize [SelectionEvent]s for children [Selectable]s when needed.

When a new [SelectionEdgeUpdateEvent] is dispatched to a [Selectable], this delegate checks whether the [Selectable] has already received a selection update for each edge that currently exists, and synthesizes an event for the edges that have not yet received an update. This synthesized event is dispatched before dispatching the new event.

For example, if we have an existing start edge for this delegate and a [Selectable] child receives an end [SelectionEdgeUpdateEvent] and the child hasn't received a start [SelectionEdgeUpdateEvent], we synthesize a start [SelectionEdgeUpdateEvent] for the child [Selectable] and dispatch it before dispatching the original end [SelectionEdgeUpdateEvent].

See also:

- [MultiSelectableSelectionContainerDelegate], for the class that provides the main implementation details of this [SelectionContainerDelegate].

### didReceiveSelectionEventFor()

```dart
void didReceiveSelectionEventFor({required Selectable selectable, bool? forEnd})
```

Tracks whether a selection edge update event for a given [Selectable] was received.

When `forEnd` is true, the [Selectable] will be registered as having received an end event. When false, the [Selectable] is registered as having received a start event.

When `forEnd` is null, the [Selectable] will be registered as having received both start and end events.

Call this method when a [SelectionEvent] is dispatched to a child selectable managed by this delegate.

Subclasses should call [clearInternalSelectionStateForSelectable] to clean up any state added by this method, for example when removing a [Selectable] from this delegate.

### didReceiveSelectionBoundaryEvents()

```dart
void didReceiveSelectionBoundaryEvents()
```

Updates the internal selection state after a [SelectionEvent] that selects a boundary such as: [SelectWordSelectionEvent], [SelectParagraphSelectionEvent], and [SelectAllSelectionEvent].

Call this method after determining the new selection as a result of a [SelectionEvent] that selects a boundary. The [currentSelectionStartIndex] and [currentSelectionEndIndex] should be set to valid values at the time this method is called.

Subclasses should call [clearInternalSelectionStateForSelectable] to clean up any state added by this method, for example when removing a [Selectable] from this delegate.

### updateLastSelectionEdgeLocation()

```dart
void updateLastSelectionEdgeLocation({required Offset globalSelectionEdgeLocation, required bool forEnd})
```

Updates the last selection edge location of the edge specified by `forEnd` to the provided `globalSelectionEdgeLocation`.

### clearInternalSelectionState()

```dart
void clearInternalSelectionState()
```

Clears the internal selection state.

This indicates that no [Selectable] child under this delegate has received start or end events, and resets any tracked global locations for start and end [SelectionEdgeUpdateEvent]s.

### clearInternalSelectionStateForSelectable()

```dart
void clearInternalSelectionStateForSelectable(Selectable selectable)
```

Clears the internal selection state for a given [Selectable].

This indicates that the given `selectable` has neither received a start or end [SelectionEdgeUpdateEvent]s.

Subclasses should call this method to clean up state added in [didReceiveSelectionEventFor] and [didReceiveSelectionBoundaryEvents].

### remove()

```dart
void remove(Selectable selectable)
```

### handleSelectAll()

```dart
SelectionResult handleSelectAll(SelectAllSelectionEvent event)
```

### handleSelectWord()

```dart
SelectionResult handleSelectWord(SelectWordSelectionEvent event)
```

### handleSelectParagraph()

```dart
SelectionResult handleSelectParagraph(SelectParagraphSelectionEvent event)
```

### handleClearSelection()

```dart
SelectionResult handleClearSelection(ClearSelectionEvent event)
```

### handleSelectionEdgeUpdate()

```dart
SelectionResult handleSelectionEdgeUpdate(SelectionEdgeUpdateEvent event)
```

### dispose()

```dart
void dispose()
```

### dispatchSelectionEventToChild()

```dart
SelectionResult dispatchSelectionEventToChild(Selectable selectable, SelectionEvent event)
```

### ensureChildUpdated()

```dart
void ensureChildUpdated(Selectable selectable)
```

Ensures the `selectable` child has received the most up to date selection events.

This method is called when:

1.  A new [Selectable] is added to the delegate, and its screen location falls into the previous selection.
2.  Before a [SelectionEvent] of type [SelectionEventType.startEdgeUpdate], [SelectionEventType.endEdgeUpdate], [SelectionEventType.granularlyExtendSelection], or [SelectionEventType.directionallyExtendSelection] is dispatched to a [Selectable] child.

### didChangeSelectables()

```dart
void didChangeSelectables()
```

# MultiSelectableSelectionContainerDelegate

```dart
abstract class MultiSelectableSelectionContainerDelegate extends SelectionContainerDelegate with ChangeNotifier {}
```

A delegate that handles events and updates for multiple [Selectable] children.

Updates are optimized by tracking which [Selectable]s reside on the edges of a selection. Subclasses should implement [ensureChildUpdated] to describe how a [Selectable] should behave when added to a selection.

### MultiSelectableSelectionContainerDelegate()

```dart
MultiSelectableSelectionContainerDelegate()
```

Creates an instance of [MultiSelectableSelectionContainerDelegate].

### selectables

```dart
List<Selectable> selectables
```

Gets the list of [Selectable]s this delegate is managing.

### currentSelectionEndIndex

```dart
int currentSelectionEndIndex
```

The current [Selectable] that contains the selection end edge.

### currentSelectionStartIndex

```dart
int currentSelectionStartIndex
```

The current [Selectable] that contains the selection start edge.

### add()

```dart
void add(Selectable selectable)
```

### remove()

```dart
void remove(Selectable selectable)
```

### layoutDidChange()

```dart
void layoutDidChange()
```

Notifies this delegate that layout of the container has changed.

### didChangeSelectables()

```dart
void didChangeSelectables()
```

Called when this delegate finishes updating the [Selectable]s.

### value

```dart
SelectionGeometry get value
```

### compareOrder

```dart
Comparator<Selectable> get compareOrder
```

The compare function this delegate used for determining the selection order of the selectables.

Defaults to screen order.

### getSelectionGeometry()

```dart
SelectionGeometry getSelectionGeometry()
```

Gets the combined [SelectionGeometry] for child [Selectable]s.

### pushHandleLayers()

```dart
void pushHandleLayers(LayerLink? startHandle, LayerLink? endHandle)
```

### getSelectedContent()

```dart
SelectedContent? getSelectedContent()
```

Copies the selected contents of all [Selectable]s.

### contentLength

```dart
int get contentLength
```

The total length of the content under this [SelectionContainerDelegate].

This value is derived from the [Selectable.contentLength] of each [Selectable] managed by this delegate.

### getSelection()

```dart
SelectedContentRange? getSelection()
```

Returns a [SelectedContentRange] considering the [SelectedContentRange] from each [Selectable] child managed under this delegate.

When nothing is selected or either selection edge has not been set, this method will return `null`.

### handleSelectAll()

```dart
SelectionResult handleSelectAll(SelectAllSelectionEvent event)
```

Selects all contents of all [Selectable]s.

### handleSelectWord()

```dart
SelectionResult handleSelectWord(SelectWordSelectionEvent event)
```

Selects a word in a [Selectable] at the location [SelectWordSelectionEvent.globalPosition].

### handleSelectParagraph()

```dart
SelectionResult handleSelectParagraph(SelectParagraphSelectionEvent event)
```

Selects a paragraph in a [Selectable] at the location [SelectParagraphSelectionEvent.globalPosition].

### handleClearSelection()

```dart
SelectionResult handleClearSelection(ClearSelectionEvent event)
```

Removes the selection of all [Selectable]s this delegate manages.

### handleGranularlyExtendSelection()

```dart
SelectionResult handleGranularlyExtendSelection(GranularlyExtendSelectionEvent event)
```

Extend current selection in a certain [TextGranularity].

### handleDirectionallyExtendSelection()

```dart
SelectionResult handleDirectionallyExtendSelection(DirectionallyExtendSelectionEvent event)
```

Extend current selection in a certain [TextGranularity].

### handleSelectionEdgeUpdate()

```dart
SelectionResult handleSelectionEdgeUpdate(SelectionEdgeUpdateEvent event)
```

Updates the selection edges.

### dispatchSelectionEvent()

```dart
SelectionResult dispatchSelectionEvent(SelectionEvent event)
```

### dispose()

```dart
void dispose()
```

### ensureChildUpdated()

```dart
void ensureChildUpdated(Selectable selectable)
```

Ensures the [Selectable] child has received up to date selection event.

This method is called when a new [Selectable] is added to the delegate, and its screen location falls into the previous selection.

Subclasses are responsible for updating the selection of this newly added [Selectable].

### dispatchSelectionEventToChild()

```dart
SelectionResult dispatchSelectionEventToChild(Selectable selectable, SelectionEvent event)
```

Dispatches a selection event to a specific [Selectable].

Override this method if subclasses need to generate additional events or treatments prior to sending the [SelectionEvent].

# SelectableRegionContextMenuBuilder

```dart
typedef SelectableRegionContextMenuBuilder = Widget Function(BuildContext context, SelectableRegionState selectableRegionState)
```

Signature for a widget builder that builds a context menu for the given [SelectableRegionState].

See also:

- [EditableTextContextMenuBuilder], which performs the same role for [EditableText].

# SelectableRegionSelectionStatus

```dart
enum SelectableRegionSelectionStatus {}
```

The status of the selection under a [SelectableRegion].

This value can be accessed for a [SelectableRegion] by using [SelectableRegionSelectionStatusScope.maybeOf].

This value under a [SelectableRegion] is updated frequently during selection gestures such as clicks and taps to select and keyboard shortcuts.

Indicates that the selection under a [SelectableRegion] is changing.

A [SelectableRegion]s selection is changing when it is being updated by user through selection gestures and keyboard shortcuts. For example, during a text selection drag with a click + drag, a [SelectableRegion]s selection is considered changing until the user releases the click, then it will be considered finalized.

Indicates that the selection under a [SelectableRegion] is finalized.

A [SelectableRegion]s selection is finalized when it is no longer being updated by the user through selection gestures or keyboard shortcuts. For example, the selection will be finalized on a mouse drag end, touch long press drag end, a single click to collapse the selection, a double click/tap to select a word, ctrl + A / cmd + A to select all, or a triple click/tap to select a paragraph.

# SelectableRegionSelectionStatusScope

```dart
final class SelectableRegionSelectionStatusScope extends InheritedWidget {}
```

Notifies its listeners when the selection under a [SelectableRegion] or [SelectionArea] is being changed or finalized.

Use [SelectableRegionSelectionStatusScope.maybeOf], to access the [ValueListenable] of type [SelectableRegionSelectionStatus] under a [SelectableRegion]. Its listeners will be called even when the value of the [SelectableRegionSelectionStatus] does not change.

### selectionStatusNotifier

```dart
ValueListenable<SelectableRegionSelectionStatus> selectionStatusNotifier
```

Tracks updates to the [SelectableRegionSelectionStatus] of the owning [SelectableRegion].

Listeners will be called even when the value of the [SelectableRegionSelectionStatus] does not change. The selection under the [SelectableRegion] still may have changed.

### maybeOf()

```dart
ValueListenable<SelectableRegionSelectionStatus>? maybeOf(BuildContext context)
```

The closest instance of this class that encloses the given context.

If there is no enclosing [SelectableRegion] or [SelectionArea] widget, then null is returned.

Calling this method will create a dependency on the closest [SelectableRegionSelectionStatusScope] in the [context], if there is one.

### updateShouldNotify()

```dart
bool updateShouldNotify(SelectableRegionSelectionStatusScope oldWidget)
```

# SelectionListener

```dart
class SelectionListener extends StatefulWidget {}
```

A [SelectionContainer] that allows the user to access the [SelectionDetails] and listen to selection changes for the child subtree it wraps under a [SelectionArea] or [SelectableRegion].

The selection updates are provided through the [selectionNotifier], to listen to these updates attach a listener through [SelectionListenerNotifier.addListener].

This widget does not listen to selection changes of nested [SelectionArea]s or [SelectableRegion]s in its subtree because those widgets are self-contained and do not bubble up their selection. To listen to selection changes of a [SelectionArea] or [SelectableRegion] under this [SelectionListener], add an additional [SelectionListener] under each one.

{@tool dartpad} This example shows how to use [SelectionListener] to access the [SelectionDetails] under a [SelectionArea] or [SelectableRegion].

** See code in examples/api/lib/material/selection_area/selection_area.1.dart ** {@end-tool}

{@tool dartpad} This example shows how to color the active selection red under a [SelectionArea] or [SelectableRegion].

** See code in examples/api/lib/material/selection_area/selection_area.2.dart ** {@end-tool}

See also:

- [SelectableRegion], which provides an overview of the selection system.

### SelectionListener()

```dart
SelectionListener({dynamic key, required SelectionListenerNotifier selectionNotifier, required Widget child})
```

Create a new [SelectionListener] widget.

### selectionNotifier

```dart
SelectionListenerNotifier selectionNotifier
```

Notifies listeners when the selection has changed.

### child

```dart
Widget child
```

The child widget this selection listener applies to.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<SelectionListener> createState()
```

# SelectionDetails

```dart
abstract final class SelectionDetails {}
```

A read-only interface for accessing the details of a selection under a [SelectionListener].

This includes information such as the status of the selection indicating if it is collapsed or uncollapsed, the [SelectedContentRange] that includes the start and end offsets of the selection local to the [SelectionListener] that reports this object.

This object is typically accessed by providing a [SelectionListenerNotifier] to a [SelectionListener] and retrieving the value from [SelectionListenerNotifier.selection].

### range

```dart
SelectedContentRange? get range
```

The computed selection range of the owning [SelectionListener]s subtree.

Returns `null` if there is nothing selected.

### status

```dart
SelectionStatus get status
```

The status that indicates whether there is a selection and whether the selection is collapsed.

# SelectionListenerNotifier

```dart
final class SelectionListenerNotifier extends ChangeNotifier {}
```

Notifies listeners when the selection under a [SelectionListener] has been changed.

This object is typically provided to a [SelectionListener].

### selection

```dart
SelectionDetails get selection
```

The details of the selection under the [SelectionListener] that owns this notifier.

Throws an exception if this notifier has not been registered to a [SelectionListener]. To check if a notifier has been registered to a [SelectionListener] use [registered].

### registered

```dart
bool get registered
```

Whether this [SelectionListenerNotifier] has been registered to a [SelectionListener].

### dispose()

```dart
void dispose()
```

### addListener()

```dart
void addListener(VoidCallback listener)
```

Calls the listener every time the [SelectionGeometry] of the selection changes under a [SelectionListener].

Listeners can be removed with [removeListener].
