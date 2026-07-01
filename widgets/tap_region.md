@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'gesture_detector.dart';

# TapRegionCallback

```dart
typedef TapRegionCallback = void Function(PointerDownEvent event)
```

Signature for a callback called for a [PointerDownEvent] relative to a [TapRegion].

See also:

- [TapRegion.onTapOutside], which is of this type.
- [TapRegion.onTapInside], which is of this type.
- [TapRegionUpCallback], which is similar but for [PointerUpEvent]s.

# TapRegionUpCallback

```dart
typedef TapRegionUpCallback = void Function(PointerUpEvent event)
```

Signature for a callback called for a [PointerUpEvent] relative to a [TapRegion].

See also:

- [TapRegion.onTapUpOutside], which is of this type.
- [TapRegion.onTapUpInside], which is of this type.
- [TapRegionCallback], which is similar but for [PointerDownEvent]s.

# TapRegionRegistry

```dart
abstract class TapRegionRegistry {}
```

An interface for registering and unregistering a [RenderTapRegion] (typically created with a [TapRegion] widget) with a [RenderTapRegionSurface] (typically created with a [TapRegionSurface] widget).

### registerTapRegion()

```dart
void registerTapRegion(RenderTapRegion region)
```

Register the given [RenderTapRegion] with the registry.

### unregisterTapRegion()

```dart
void unregisterTapRegion(RenderTapRegion region)
```

Unregister the given [RenderTapRegion] with the registry.

### of()

```dart
TapRegionRegistry of(BuildContext context)
```

Allows finding of the nearest [TapRegionRegistry], such as a [RenderTapRegionSurface].

Will throw if a [TapRegionRegistry] isn't found.

### maybeOf()

```dart
TapRegionRegistry? maybeOf(BuildContext context)
```

Allows finding of the nearest [TapRegionRegistry], such as a [RenderTapRegionSurface].

# TapRegionSurface

```dart
class TapRegionSurface extends SingleChildRenderObjectWidget {}
```

A widget that provides notification of a tap inside or outside of a set of registered regions, without participating in the [gesture disambiguation](https://flutter.dev/to/gesture-disambiguation) system.

The regions are defined by adding [TapRegion] widgets to the widget tree around the regions of interest, and they will register with this [TapRegionSurface]. Each of the tap regions can optionally belong to a group by assigning a [TapRegion.groupId], where all the regions with the same groupId act as if they were all one region.

When a tap down or tap up outside of a registered region or region group is detected, its [TapRegion.onTapOutside] or [TapRegion.onTapUpOutside] callback is called, respectively. If the tap is outside one member of a group, but inside another, no notification is made.

When a tap down or tap up inside of a registered region or region group is detected, its [TapRegion.onTapInside] or [TapRegion.onTapUpInside] callback is called, respectively. If the tap is inside one member of a group, all members are notified.

The [TapRegionSurface] should be defined at the highest level needed to encompass the entire area where taps should be monitored. This is typically around the entire app. If the entire app isn't covered, then taps outside of the [TapRegionSurface] will be ignored and no [TapRegion.onTapOutside] or [TapRegion.onTapUpOutside] calls will be made for those events. The [WidgetsApp], [MaterialApp] and [CupertinoApp] automatically include a [TapRegionSurface] around their entire app.

[TapRegionSurface] does not participate in the [gesture disambiguation](https://flutter.dev/to/gesture-disambiguation) system, so if multiple [TapRegionSurface]s are active at the same time, they will all fire, and so will any other gestures recognized by a [GestureDetector] or other pointer event handlers.

[TapRegion]s register only with the nearest ancestor [TapRegionSurface].

See also:

- [RenderTapRegionSurface], the render object that is inserted into the render tree by this widget.
- <https://flutter.dev/to/gesture-disambiguation> for more information about the gesture system and how it disambiguates inputs.

### TapRegionSurface()

```dart
TapRegionSurface({dynamic key, required Widget child})
```

Creates a const [RenderTapRegionSurface].

The [child] attribute is required.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderProxyBoxWithHitTestBehavior renderObject)
```

# RenderTapRegionSurface

```dart
class RenderTapRegionSurface extends RenderProxyBoxWithHitTestBehavior implements TapRegionRegistry {}
```

A render object that provides notification of a tap inside or outside of a set of registered regions, without participating in the [gesture disambiguation](https://flutter.dev/to/gesture-disambiguation) system (other than to consume tap down events if [TapRegion.consumeOutsideTaps] is true).

The regions are defined by adding [RenderTapRegion] render objects in the render tree around the regions of interest, and they will register with this [RenderTapRegionSurface]. Each of the tap regions can optionally belong to a group by assigning a [RenderTapRegion.groupId], where all the regions with the same groupId act as if they were all one region.

When a tap down or tap up outside of a registered region or region group is detected, its [TapRegion.onTapOutside] or [TapRegion.onTapUpOutside] callback is called, respectively. If the tap is outside one member of a group, but inside another, no notification is made.

When a tap down or tap up inside of a registered region or region group is detected, its [TapRegion.onTapInside] or [TapRegion.onTapUpInside] callback is called, respectively. If the tap is inside one member of a group, all members are notified.

The [RenderTapRegionSurface] should be defined at the highest level needed to encompass the entire area where taps should be monitored. This is typically around the entire app. If the entire app isn't covered, then taps outside of the [RenderTapRegionSurface] will be ignored and no [RenderTapRegion.onTapOutside] or [RenderTapRegion.onTapUpOutside] calls will be made for those events. The [WidgetsApp], [MaterialApp] and [CupertinoApp] automatically include a [RenderTapRegionSurface] around the entire app.

[RenderTapRegionSurface] does not participate in the [gesture disambiguation](https://flutter.dev/to/gesture-disambiguation) system, so if multiple [RenderTapRegionSurface]s are active at the same time, they will all fire, and so will any other gestures recognized by a [GestureDetector] or other pointer event handlers.

[RenderTapRegion]s register only with the nearest ancestor [RenderTapRegionSurface].

See also:

- [TapRegionSurface], a widget that inserts a [RenderTapRegionSurface] into the render tree.
- [TapRegionRegistry.of], which can find the nearest ancestor [RenderTapRegionSurface], which is a [TapRegionRegistry].

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### registerTapRegion()

```dart
void registerTapRegion(RenderTapRegion region)
```

### unregisterTapRegion()

```dart
void unregisterTapRegion(RenderTapRegion region)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry entry)
```

# TapRegion

```dart
class TapRegion extends SingleChildRenderObjectWidget {}
```

A widget that defines a region that can detect taps inside or outside of itself and any group of regions it belongs to, without participating in the [gesture disambiguation](https://flutter.dev/to/gesture-disambiguation) system (other than to consume tap down events if [consumeOutsideTaps] is true).

This widget indicates to the nearest ancestor [TapRegionSurface] that the region occupied by its child will participate in the tap detection for that surface.

If this region belongs to a group (by virtue of its [groupId]), all the regions in the group will act as one.

If there is no [TapRegionSurface] ancestor, [TapRegion] will do nothing.

[TapRegion] is aware of the [Route]s in the [Navigator], so that [onTapOutside] or [onTapUpOutside] isn't called after the user navigates to a different page.

### TapRegion()

```dart
TapRegion({dynamic key, required Widget? child, bool enabled = true, HitTestBehavior behavior = HitTestBehavior.deferToChild, TapRegionCallback? onTapOutside, TapRegionCallback? onTapInside, TapRegionUpCallback? onTapUpOutside, TapRegionUpCallback? onTapUpInside, Object? groupId, bool consumeOutsideTaps = false, String? debugLabel})
```

Creates a const [TapRegion].

The [child] argument is required.

### enabled

```dart
bool enabled
```

Whether or not this [TapRegion] is enabled as part of the composite region.

### behavior

```dart
HitTestBehavior behavior
```

How to behave during hit testing when deciding how the hit test propagates to children and whether to consider targets behind this [TapRegion].

Defaults to [HitTestBehavior.deferToChild].

See [HitTestBehavior] for the allowed values and their meanings.

### onTapOutside

```dart
TapRegionCallback? onTapOutside
```

A callback to be invoked when a tap down is detected outside of this [TapRegion] and any other region with the same [groupId], if any.

The [PointerDownEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

See also:

- [onTapUpOutside], which is called when a tap up is detected outside of this region.

### onTapInside

```dart
TapRegionCallback? onTapInside
```

A callback to be invoked when a tap down is detected inside of this [TapRegion], or any other tap region with the same [groupId], if any.

The [PointerDownEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

See also:

- [onTapUpInside], which is called when a tap up is detected inside of this region.

### onTapUpOutside

```dart
TapRegionUpCallback? onTapUpOutside
```

A callback to be invoked when a tap up is detected outside of this [TapRegion] and any other region with the same [groupId], if any.

The [PointerUpEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

See also:

- [onTapOutside], which is called when a tap down is detected outside of this region.

### onTapUpInside

```dart
TapRegionUpCallback? onTapUpInside
```

A callback to be invoked when a tap up is detected inside of this [TapRegion], or any other tap region with the same [groupId], if any.

The [PointerUpEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

See also:

- [onTapInside], which is called when a tap down is detected inside of this region.

### groupId

```dart
Object? groupId
```

An optional group ID that groups [TapRegion]s together so that they operate as one region. If any member of a group is hit by a particular tap, then the [onTapOutside] / [onTapUpOutside] will not be called for any members of the group. If any member of the group is hit, then all members will have their [onTapInside] / [onTapUpInside] called.

If the group id is null, then only this region is hit tested.

### consumeOutsideTaps

```dart
bool consumeOutsideTaps
```

If true, then the group that this region belongs to will stop the propagation of all events in the gesture arena.

This is useful if you want to block events from being given to a [GestureDetector] when [onTapOutside] is called.

If other [TapRegion]s with the same [groupId] have [consumeOutsideTaps] set to false, but this one is true, then this one will take precedence, and the event will be consumed.

Defaults to false.

### debugLabel

```dart
String? debugLabel
```

An optional debug label to help with debugging in debug mode.

Will be null in release mode.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderTapRegion renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderTapRegion

```dart
class RenderTapRegion extends RenderProxyBoxWithHitTestBehavior {}
```

A render object that defines a region that can detect taps inside or outside of itself and any group of regions it belongs to, without participating in the [gesture disambiguation](https://flutter.dev/to/gesture-disambiguation) system.

This render object indicates to the nearest ancestor [TapRegionSurface] that the region occupied by its child (or itself if [behavior] is [HitTestBehavior.opaque]) will participate in the tap detection for that surface.

If this region belongs to a group (by virtue of its [groupId]), all the regions in the group will act as one.

If there is no [RenderTapRegionSurface] ancestor in the render tree, [RenderTapRegion] will do nothing.

The [behavior] attribute describes how to behave during hit testing when deciding how the hit test propagates to children and whether to consider targets behind the tap region. Defaults to [HitTestBehavior.deferToChild]. See [HitTestBehavior] for the allowed values and their meanings.

See also:

- [TapRegion], a widget that inserts a [RenderTapRegion] into the render tree.

### RenderTapRegion()

```dart
RenderTapRegion({TapRegionRegistry? registry, bool enabled = true, bool consumeOutsideTaps = false, TapRegionCallback? onTapOutside, TapRegionCallback? onTapInside, TapRegionUpCallback? onTapUpOutside, TapRegionUpCallback? onTapUpInside, dynamic behavior = HitTestBehavior.deferToChild, Object? groupId, String? debugLabel})
```

Creates a [RenderTapRegion].

### onTapOutside

```dart
TapRegionCallback? onTapOutside
```

A callback to be invoked when a tap down is detected outside of this [RenderTapRegion] and any other region with the same [groupId], if any.

The [PointerDownEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

### onTapInside

```dart
TapRegionCallback? onTapInside
```

A callback to be invoked when a tap down is detected inside of this [RenderTapRegion], or any other tap region with the same [groupId], if any.

The [PointerDownEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

### onTapUpOutside

```dart
TapRegionUpCallback? onTapUpOutside
```

A callback to be invoked when a tap up is detected outside of this [RenderTapRegion] and any other region with the same [groupId], if any.

The [PointerUpEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

### onTapUpInside

```dart
TapRegionUpCallback? onTapUpInside
```

A callback to be invoked when a tap up is detected inside of this [RenderTapRegion], or any other tap region with the same [groupId], if any.

The [PointerUpEvent] passed to the function is the event that caused the notification. If this region is part of a group (i.e. [groupId] is set), then it's possible that the event may be outside of this immediate region, although it will be within the region of one of the group members.

### debugLabel

```dart
String? debugLabel
```

A label used in debug builds. Will be null in release builds.

### enabled

```dart
bool get enabled
```

Whether or not this region should participate in the composite region.

### enabled

```dart
set enabled(bool value)
```

### consumeOutsideTaps

```dart
bool get consumeOutsideTaps
```

Whether or not the tap event that triggers a call to [onTapOutside] or [onTapUpOutside] will continue on to participate in the gesture arena.

If any [RenderTapRegion] in the same group has [consumeOutsideTaps] set to true, then the tap down event will be consumed before other gesture recognizers can process them.

### consumeOutsideTaps

```dart
set consumeOutsideTaps(bool value)
```

### groupId

```dart
Object? get groupId
```

An optional group ID that groups [RenderTapRegion]s together so that they operate as one region. If any member of a group is hit by a particular tap, then the [onTapOutside] / [onTapUpOutside] will not be called for any members of the group. If any member of the group is hit, then all members will have their [onTapInside] / [onTapUpInside] called.

If the group id is null, then only this region is hit tested.

### groupId

```dart
set groupId(Object? value)
```

### registry

```dart
TapRegionRegistry? get registry
```

The registry that this [RenderTapRegion] should register with.

If the [registry] is null, then this region will not be registered anywhere, and will not do any tap detection.

A [RenderTapRegionSurface] is a [TapRegionRegistry].

### registry

```dart
set registry(TapRegionRegistry? value)
```

### layout()

```dart
void layout(Constraints constraints, {bool parentUsesSize = false})
```

### dispose()

```dart
void dispose()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TextFieldTapRegion

```dart
class TextFieldTapRegion extends TapRegion {}
```

A [TapRegion] that adds its children to the tap region group for widgets based on the [EditableText] text editing widget, such as [TextField] and [CupertinoTextField].

Widgets that are wrapped with a [TextFieldTapRegion] are considered to be part of a text field for purposes of unfocus behavior. So, when the user taps on them, the currently focused text field won't be unfocused by default. This allows controls like spinners, copy buttons, and formatting buttons to be associated with a text field without causing the text field to lose focus when they are interacted with.

{@tool dartpad} This example shows how to use a [TextFieldTapRegion] to wrap a set of "spinner" buttons that increment and decrement a value in the text field without causing the text field to lose keyboard focus.

This example includes a generic `SpinnerField<T>` class that you can copy/paste into your own project and customize.

** See code in examples/api/lib/widgets/tap_region/text_field_tap_region.0.dart ** {@end-tool}

See also:

- [TapRegion], the widget that this widget uses to add widgets to the group of text fields.

### TextFieldTapRegion()

```dart
TextFieldTapRegion({dynamic key, required Widget? child, bool enabled, void Function(InvalidType)? onTapOutside, void Function(InvalidType)? onTapInside, void Function(InvalidType)? onTapUpOutside, void Function(InvalidType)? onTapUpInside, bool consumeOutsideTaps, String? debugLabel, Object? groupId = EditableText})
```

Creates a const [TextFieldTapRegion].

The [child] field is required.
