@docImport 'package:flutter/gestures.dart'; @docImport 'package:flutter/material.dart';

# SelectionResult

```dart
enum SelectionResult {}
```

The result after handling a [SelectionEvent].

[SelectionEvent]s are sent from [SelectionRegistrar] to be handled by [SelectionHandler.dispatchSelectionEvent]. The subclasses of [SelectionHandler] or [Selectable] must return appropriate [SelectionResult]s after handling the events.

This is used by the [SelectionContainer] to determine how a selection expands across its [Selectable] children.

There is nothing left to select forward in this [Selectable], and further selection should extend to the next [Selectable] in screen order.

{@template flutter.rendering.selection.SelectionResult.footNote} This is used after subclasses [SelectionHandler] or [Selectable] handled [SelectionEdgeUpdateEvent]. {@endtemplate}

Selection does not reach this [Selectable] and is located before it in screen order.

{@macro flutter.rendering.selection.SelectionResult.footNote}

Selection ends in this [Selectable].

Part of the [Selectable] may or may not be selected, but there is still content to select forward or backward.

{@macro flutter.rendering.selection.SelectionResult.footNote}

The result can't be determined in this frame.

This is typically used when the subtree is scrolling to reveal more content.

{@macro flutter.rendering.selection.SelectionResult.footNote}

There is no result for the selection event.

This is used when a selection result is not applicable, e.g. [SelectAllSelectionEvent], [ClearSelectionEvent], and [SelectWordSelectionEvent].

# SelectionHandler

```dart
abstract class SelectionHandler implements ValueListenable<SelectionGeometry> {}
```

The abstract interface to handle [SelectionEvent]s.

This interface is extended by [Selectable] and [SelectionContainerDelegate] and is typically not used directly.

{@template flutter.rendering.SelectionHandler} This class returns a [SelectionGeometry] as its [value], and is responsible to notify its listener when its selection geometry has changed as the result of receiving selection events. {@endtemplate}

### pushHandleLayers()

```dart
void pushHandleLayers(LayerLink? startHandle, LayerLink? endHandle)
```

Marks this handler to be responsible for pushing [LeaderLayer]s for the selection handles.

This handler is responsible for pushing the leader layers with the given layer links if they are not null. It is possible that only one layer is non-null if this handler is only responsible for pushing one layer link.

The `startHandle` needs to be placed at the visual location of selection start, the `endHandle` needs to be placed at the visual location of selection end. Typically, the visual locations should be the same as [SelectionGeometry.startSelectionPoint] and [SelectionGeometry.endSelectionPoint].

### getSelectedContent()

```dart
SelectedContent? getSelectedContent()
```

Gets the selected content in this object.

Return `null` if nothing is selected.

### getSelection()

```dart
SelectedContentRange? getSelection()
```

Gets the [SelectedContentRange] representing the selected range in this object.

When nothing is selected, subclasses should return `null`.

### dispatchSelectionEvent()

```dart
SelectionResult dispatchSelectionEvent(SelectionEvent event)
```

Handles the [SelectionEvent] sent to this object.

The subclasses need to update their selections or delegate the [SelectionEvent]s to their subtrees.

The `event`s are subclasses of [SelectionEvent]. Check [SelectionEvent.type] to determine what kinds of event are dispatched to this handler and handle them accordingly.

See also:

- [SelectionEventType], which contains all of the possible types.

### contentLength

```dart
int get contentLength
```

The length of the content in this object.

# SelectedContentRange

```dart
class SelectedContentRange with Diagnosticable {}
```

This class stores the range information of the selection under a [Selectable] or [SelectionHandler].

The [SelectedContentRange] for a given [Selectable] or [SelectionHandler] can be retrieved by calling [SelectionHandler.getSelection].

### SelectedContentRange()

```dart
SelectedContentRange({required int startOffset, required int endOffset})
```

Creates a [SelectedContentRange] with the given values.

### startOffset

```dart
int startOffset
```

The start of the selection relative to the start of the content.

{@template flutter.rendering.selection.SelectedContentRange.selectionOffsets} For example a [Text] widget's content is in the format of an [TextSpan] tree.

Take the [Text] widget and [TextSpan] tree below:

{@tool snippet}

```dart
const Text.rich(
  TextSpan(
    text: 'Hello world, ',
    children: <InlineSpan>[
      WidgetSpan(
        child: Text('how are you today? '),
      ),
      TextSpan(
        text: 'Good, thanks for asking.',
      ),
    ],
  ),
)
```

{@end-tool}

If we select from the beginning of 'world' to the end of the '.' at the end of the [TextSpan] tree, the [SelectedContentRange] from [SelectionHandler.getSelection] will be relative to the text of the [TextSpan] tree, with [WidgetSpan] content being flattened. The [startOffset] will be 6, and [endOffset] will be 56. This takes into account the length of the content in the [WidgetSpan], which is 19, making the overall length of the content 56. {@endtemplate}

### endOffset

```dart
int endOffset
```

The end of the selection relative to the start of the content.

{@macro flutter.rendering.selection.SelectedContentRange.selectionOffsets}

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

# SelectedContent

```dart
class SelectedContent with Diagnosticable {}
```

The selected content in a [Selectable] or [SelectionHandler].

### SelectedContent()

```dart
SelectedContent({required String plainText})
```

Creates a selected content object.

Only supports plain text.

### plainText

```dart
String plainText
```

The selected content in plain text format.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Selectable

```dart
mixin Selectable implements SelectionHandler {}
```

A mixin that can be selected by users when under a [SelectionArea] widget.

This object receives selection events and the [value] must reflect the current selection in this [Selectable]. The object must also notify its listener if the [value] ever changes.

This object is responsible for drawing the selection highlight.

In order to receive the selection event, the mixer needs to register itself to [SelectionRegistrar]s. Use [SelectionContainer.maybeOf] to get the selection registrar, and mix the [SelectionRegistrant] to subscribe to the [SelectionRegistrar] automatically.

This mixin is typically mixed by [RenderObject]s. The [RenderObject.paint] methods are responsible to push the [LayerLink]s provided to [pushHandleLayers].

{@macro flutter.rendering.SelectionHandler}

See also:

- [SelectableRegion], which provides an overview of selection system.

### getTransformTo()

```dart
Matrix4 getTransformTo(RenderObject? ancestor)
```

{@macro flutter.rendering.RenderObject.getTransformTo}

### size

```dart
Size get size
```

The size of this [Selectable].

### boundingBoxes

```dart
List<Rect> get boundingBoxes
```

A list of [Rect]s that represent the bounding box of this [Selectable] in local coordinates.

### dispose()

```dart
void dispose()
```

Disposes resources held by the mixer.

# SelectionRegistrant

```dart
mixin SelectionRegistrant on Selectable {}
```

A mixin to auto-register the mixer to the [registrar].

To use this mixin, the mixer needs to set the [registrar] to the [SelectionRegistrar] it wants to register to.

This mixin only registers the mixer with the [registrar] if the [SelectionGeometry.hasContent] returned by the mixer is true.

### registrar

```dart
SelectionRegistrar? get registrar
```

The [SelectionRegistrar] the mixer will be or is registered to.

This [Selectable] only registers the mixer if the [SelectionGeometry.hasContent] returned by the [Selectable] is true.

### registrar

```dart
set registrar(SelectionRegistrar? value)
```

### dispose()

```dart
void dispose()
```

# SelectionUtils

```dart
abstract final class SelectionUtils {}
```

A utility class that provides useful methods for handling selection events.

### getResultBasedOnRect()

```dart
SelectionResult getResultBasedOnRect(Rect targetRect, Offset point)
```

Determines [SelectionResult] purely based on the target rectangle.

This method returns [SelectionResult.end] if the `point` is inside the `targetRect`. Returns [SelectionResult.previous] if the `point` is considered to be lower than `targetRect` in screen order. Returns [SelectionResult.next] if the point is considered to be higher than `targetRect` in screen order.

### adjustDragOffset()

```dart
Offset adjustDragOffset(Rect targetRect, Offset point, {TextDirection direction = TextDirection.ltr})
```

Adjusts the dragging offset based on the target rect.

This method moves the offsets to be within the target rect in case they are outside the rect.

This is used in the case where a drag happens outside of the rectangle of a [Selectable].

The logic works as the following: ![](https://flutter.github.io/assets-for-api-docs/assets/rendering/adjust_drag_offset.png)

For points inside the rect: Their effective locations are unchanged.

For points in Area 1: Move them to top-left of the rect if text direction is ltr, or top-right if rtl.

For points in Area 2: Move them to bottom-right of the rect if text direction is ltr, or bottom-left if rtl.

# SelectionEventType

```dart
enum SelectionEventType {}
```

The type of a [SelectionEvent].

Used by [SelectionEvent.type] to distinguish different types of events.

An event to update the selection start edge.

Used by [SelectionEdgeUpdateEvent].

An event to update the selection end edge.

Used by [SelectionEdgeUpdateEvent].

An event to clear the current selection.

Used by [ClearSelectionEvent].

An event to select all the available content.

Used by [SelectAllSelectionEvent].

An event to select a word at the location [SelectWordSelectionEvent.globalPosition].

Used by [SelectWordSelectionEvent].

An event to select a paragraph at the location [SelectParagraphSelectionEvent.globalPosition].

Used by [SelectParagraphSelectionEvent].

An event that extends the selection by a specific [TextGranularity].

An event that extends the selection in a specific direction.

# TextGranularity

```dart
enum TextGranularity {}
```

The unit of how selection handles move in text.

The [GranularlyExtendSelectionEvent] uses this enum to describe how [Selectable] should extend its selection.

Treats each character as an atomic unit when moving the selection handles.

Treats word as an atomic unit when moving the selection handles.

Treats a paragraph as an atomic unit when moving the selection handles.

Treats each line break as an atomic unit when moving the selection handles.

Treats the entire document as an atomic unit when moving the selection handles.

# SelectionEvent

```dart
abstract class SelectionEvent {}
```

An abstract base class for selection events.

This should not be directly used. To handle a selection event, it should be downcast to a specific subclass. One can use [type] to look up which subclasses to downcast to.

See also:

- [SelectAllSelectionEvent], for events to select all contents.
- [ClearSelectionEvent], for events to clear selections.
- [SelectWordSelectionEvent], for events to select words at the locations.
- [SelectionEdgeUpdateEvent], for events to update selection edges.
- [SelectionEventType], for determining the subclass types.

### type

```dart
SelectionEventType type
```

The type of this selection event.

# SelectAllSelectionEvent

```dart
class SelectAllSelectionEvent extends SelectionEvent {}
```

Selects all selectable contents.

This event can be sent as the result of keyboard select-all, i.e. ctrl + A, or cmd + A in macOS.

### SelectAllSelectionEvent()

```dart
SelectAllSelectionEvent()
```

Creates a select all selection event.

# ClearSelectionEvent

```dart
class ClearSelectionEvent extends SelectionEvent {}
```

Clears the selection from the [Selectable] and removes any existing highlight as if there is no selection at all.

### ClearSelectionEvent()

```dart
ClearSelectionEvent()
```

Create a clear selection event.

# SelectWordSelectionEvent

```dart
class SelectWordSelectionEvent extends SelectionEvent {}
```

Selects the whole word at the location.

This event can be sent as the result of mobile long press selection.

### SelectWordSelectionEvent()

```dart
SelectWordSelectionEvent({required Offset globalPosition})
```

Creates a select word event at the [globalPosition].

### globalPosition

```dart
Offset globalPosition
```

The position in global coordinates to select word at.

# SelectParagraphSelectionEvent

```dart
class SelectParagraphSelectionEvent extends SelectionEvent {}
```

Selects the entire paragraph at the location.

This event can be sent as the result of a triple click to select.

### SelectParagraphSelectionEvent()

```dart
SelectParagraphSelectionEvent({required Offset globalPosition, bool absorb = false})
```

Creates a select paragraph event at the [globalPosition].

### globalPosition

```dart
Offset globalPosition
```

The position in global coordinates to select paragraph at.

### absorb

```dart
bool absorb
```

Whether the selectable receiving the event should be absorbed into an encompassing paragraph.

# SelectionEdgeUpdateEvent

```dart
class SelectionEdgeUpdateEvent extends SelectionEvent {}
```

Updates a selection edge.

An active selection contains two edges, start and end. Use the [type] to determine which edge this event applies to. If the [type] is [SelectionEventType.startEdgeUpdate], the event updates start edge. If the [type] is [SelectionEventType.endEdgeUpdate], the event updates end edge.

The [globalPosition] contains the new offset of the edge.

The [granularity] contains the granularity that the selection edge should move by. Only [TextGranularity.character] and [TextGranularity.word] are currently supported.

This event is dispatched when the framework detects [TapDragStartDetails] in [SelectionArea]'s gesture recognizers for mouse devices, or the selection handles have been dragged to new locations.

### SelectionEdgeUpdateEvent.forStart()

```dart
SelectionEdgeUpdateEvent.forStart({required Offset globalPosition, TextGranularity? granularity})
```

Creates a selection start edge update event.

The [globalPosition] contains the location of the selection start edge.

The [granularity] contains the granularity which the selection edge should move by. This value defaults to [TextGranularity.character].

### SelectionEdgeUpdateEvent.forEnd()

```dart
SelectionEdgeUpdateEvent.forEnd({required Offset globalPosition, TextGranularity? granularity})
```

Creates a selection end edge update event.

The [globalPosition] contains the new location of the selection end edge.

The [granularity] contains the granularity which the selection edge should move by. This value defaults to [TextGranularity.character].

### globalPosition

```dart
Offset globalPosition
```

The new location of the selection edge.

### granularity

```dart
TextGranularity granularity
```

The granularity for which the selection moves.

Only [TextGranularity.character] and [TextGranularity.word] are currently supported.

Defaults to [TextGranularity.character].

# GranularlyExtendSelectionEvent

```dart
class GranularlyExtendSelectionEvent extends SelectionEvent {}
```

Extends the start or end of the selection by a given [TextGranularity].

To handle this event, move the associated selection edge, as dictated by [isEnd], according to the [granularity].

### GranularlyExtendSelectionEvent()

```dart
GranularlyExtendSelectionEvent({required bool forward, required bool isEnd, required TextGranularity granularity})
```

Creates a [GranularlyExtendSelectionEvent].

### forward

```dart
bool forward
```

Whether to extend the selection forward.

### isEnd

```dart
bool isEnd
```

Whether this event is updating the end selection edge.

### granularity

```dart
TextGranularity granularity
```

The granularity for which the selection extend.

# SelectionExtendDirection

```dart
enum SelectionExtendDirection {}
```

The direction to extend a selection.

The [DirectionallyExtendSelectionEvent] uses this enum to describe how [Selectable] should extend their selection.

Move one edge of the selection vertically to the previous adjacent line.

For text selection, it should consider both soft and hard linebreak.

See [DirectionallyExtendSelectionEvent.dx] on how to calculate the horizontal offset.

Move one edge of the selection vertically to the next adjacent line.

For text selection, it should consider both soft and hard linebreak.

See [DirectionallyExtendSelectionEvent.dx] on how to calculate the horizontal offset.

Move the selection edges forward to a certain horizontal offset in the same line.

If there is no on-going selection, the selection must start with the first line (or equivalence of first line in a non-text selectable) and select toward the horizontal offset in the same line.

The selectable that receives [DirectionallyExtendSelectionEvent] with this enum must return [SelectionResult.end].

See [DirectionallyExtendSelectionEvent.dx] on how to calculate the horizontal offset.

Move the selection edges backward to a certain horizontal offset in the same line.

If there is no on-going selection, the selection must start with the last line (or equivalence of last line in a non-text selectable) and select backward the horizontal offset in the same line.

The selectable that receives [DirectionallyExtendSelectionEvent] with this enum must return [SelectionResult.end].

See [DirectionallyExtendSelectionEvent.dx] on how to calculate the horizontal offset.

# DirectionallyExtendSelectionEvent

```dart
class DirectionallyExtendSelectionEvent extends SelectionEvent {}
```

Extends the current selection with respect to a [direction].

To handle this event, move the associated selection edge, as dictated by [isEnd], according to the [direction].

The movements are always based on [dx]. The value is in global coordinates and is the horizontal offset the selection edge should move to when moving to across lines.

### DirectionallyExtendSelectionEvent()

```dart
DirectionallyExtendSelectionEvent({required double dx, required bool isEnd, required SelectionExtendDirection direction})
```

Creates a [DirectionallyExtendSelectionEvent].

### dx

```dart
double dx
```

The horizontal offset the selection should move to.

The offset is in global coordinates.

### isEnd

```dart
bool isEnd
```

Whether this event is updating the end selection edge.

### direction

```dart
SelectionExtendDirection direction
```

The directional movement of this event.

See also:

- [SelectionExtendDirection], which explains how to handle each enum.

### copyWith()

```dart
DirectionallyExtendSelectionEvent copyWith({double? dx, bool? isEnd, SelectionExtendDirection? direction})
```

Makes a copy of this object with its property replaced with the new values.

# SelectionRegistrar

```dart
abstract class SelectionRegistrar {}
```

A registrar that keeps track of [Selectable]s in the subtree.

A [Selectable] is only included in the [SelectableRegion] if they are registered with a [SelectionRegistrar]. Once a [Selectable] is registered, it will receive [SelectionEvent]s in [SelectionHandler.dispatchSelectionEvent].

Use [SelectionContainer.maybeOf] to get the immediate [SelectionRegistrar] in the ancestor chain above the build context.

See also:

- [SelectableRegion], which provides an overview of the selection system.
- [SelectionRegistrarScope], which hosts the [SelectionRegistrar] for the subtree.
- [SelectionRegistrant], which auto registers the object with the mixin to [SelectionRegistrar].

### add()

```dart
void add(Selectable selectable)
```

Adds the [selectable] into the registrar.

A [Selectable] must register with the [SelectionRegistrar] in order to receive selection events.

### remove()

```dart
void remove(Selectable selectable)
```

Removes the [selectable] from the registrar.

A [Selectable] must unregister itself if it is removed from the rendering tree.

# SelectionStatus

```dart
enum SelectionStatus {}
```

The status that indicates whether there is a selection and whether the selection is collapsed.

A collapsed selection means the selection starts and ends at the same location.

The selection is not collapsed.

For example if `{}` represent the selection edges: 'ab{cd}', the collapsing status is [uncollapsed]. '{abcd}', the collapsing status is [uncollapsed].

The selection is collapsed.

For example if `{}` represent the selection edges: 'ab{}cd', the collapsing status is [collapsed]. '{}abcd', the collapsing status is [collapsed]. 'abcd{}', the collapsing status is [collapsed].

No selection.

# SelectionGeometry

```dart
class SelectionGeometry with Diagnosticable {}
```

The geometry of the current selection.

This includes details such as the locations of the selection start and end, line height, the rects that encompass the selection, etc. This information is used for drawing selection controls for mobile platforms.

The positions in geometry are in local coordinates of the [SelectionHandler] or [Selectable].

### SelectionGeometry()

```dart
SelectionGeometry({SelectionPoint? startSelectionPoint, SelectionPoint? endSelectionPoint, List<Rect> selectionRects = const <Rect>[], required SelectionStatus status, required bool hasContent})
```

Creates a selection geometry object.

If any of the [startSelectionPoint] and [endSelectionPoint] is not null, the [status] must not be [SelectionStatus.none].

### startSelectionPoint

```dart
SelectionPoint? startSelectionPoint
```

The geometry information at the selection start.

This information is used for drawing mobile selection controls. The [SelectionPoint.localPosition] of the selection start is typically at the start of the selection highlight at where the start selection handle should be drawn.

The [SelectionPoint.handleType] should be [TextSelectionHandleType.left] for forward selection or [TextSelectionHandleType.right] for backward selection in most cases.

Can be null if the selection start is offstage, for example, when the selection is outside of the viewport or is kept alive by a scrollable.

### endSelectionPoint

```dart
SelectionPoint? endSelectionPoint
```

The geometry information at the selection end.

This information is used for drawing mobile selection controls. The [SelectionPoint.localPosition] of the selection end is typically at the end of the selection highlight at where the end selection handle should be drawn.

The [SelectionPoint.handleType] should be [TextSelectionHandleType.right] for forward selection or [TextSelectionHandleType.left] for backward selection in most cases.

Can be null if the selection end is offstage, for example, when the selection is outside of the viewport or is kept alive by a scrollable.

### status

```dart
SelectionStatus status
```

The status of ongoing selection in the [Selectable] or [SelectionHandler].

### selectionRects

```dart
List<Rect> selectionRects
```

The rects in the local coordinates of the containing [Selectable] that represent the selection if there is any.

### hasContent

```dart
bool hasContent
```

Whether there is any selectable content in the [Selectable] or [SelectionHandler].

### hasSelection

```dart
bool get hasSelection
```

Whether there is an ongoing selection.

### copyWith()

```dart
SelectionGeometry copyWith({SelectionPoint? startSelectionPoint, SelectionPoint? endSelectionPoint, List<Rect>? selectionRects, SelectionStatus? status, bool? hasContent})
```

Makes a copy of this object with the given values updated.

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

# SelectionPoint

```dart
class SelectionPoint with Diagnosticable {}
```

The geometry information of a selection point.

### SelectionPoint()

```dart
SelectionPoint({required Offset localPosition, required double lineHeight, required TextSelectionHandleType handleType})
```

Creates a selection point object.

### localPosition

```dart
Offset localPosition
```

The position of the selection point in the local coordinates of the containing [Selectable].

### lineHeight

```dart
double lineHeight
```

The line height at the selection point.

### handleType

```dart
TextSelectionHandleType handleType
```

The selection handle type that should be used at the selection point.

This is used for building the mobile selection handle.

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

# TextSelectionHandleType

```dart
enum TextSelectionHandleType {}
```

The type of selection handle to be displayed.

With mixed-direction text, both handles may be the same type. Examples:

- LTR text: 'the &lt;quick brown&gt; fox':

The '&lt;' is drawn with the [left] type, the '&gt;' with the [right]

- RTL text: 'XOF &lt;NWORB KCIUQ&gt; EHT':

Same as above.

- mixed text: '&lt;the NWOR&lt;B KCIUQ fox'

Here 'the QUICK B' is selected, but 'QUICK BROWN' is RTL. Both are drawn with the [left] type.

See also:

- [TextDirection], which discusses left-to-right and right-to-left text in more detail.

The selection handle is to the left of the selection end point.

The selection handle is to the right of the selection end point.

The start and end of the selection are co-incident at this point.
