@docImport 'package:flutter/material.dart';

@docImport 'basic.dart';

# View

```dart
class View extends StatefulWidget {}
```

Bootstraps a render tree that is rendered into the provided [FlutterView].

The content rendered into that view is determined by the provided [child]. Descendants within the same [LookupBoundary] can look up the view they are rendered into via [View.of] and [View.maybeOf].

The provided [child] is wrapped in a [MediaQuery] constructed from the given [view], a [FocusScope], and a [RawView] widget.

For most use cases, using [MediaQuery.of], or its associated "...Of" methods are a more appropriate way of obtaining the information that a [FlutterView] exposes. For example, using [MediaQuery.sizeOf] will expose the _logical_ device size ([MediaQueryData.size]) rather than the physical size ([FlutterView.physicalSize]). Similarly, while [FlutterView.padding] conveys the information from the operating system, the [MediaQueryData.padding] attribute (obtained from [MediaQuery.paddingOf]) further adjusts this information to be aware of the context of the widget; e.g. the [Scaffold] widget adjusts the values for its various children.

Each [FlutterView] can be associated with at most one [View] or [RawView] widget in the widget tree. Two or more [View] or [RawView] widgets configured with the same [FlutterView] must never exist within the same widget tree at the same time. This limitation is enforced by a [GlobalObjectKey] that derives its identity from the [view] provided to this widget.

Since the [View] widget bootstraps its own independent render tree using its embedded [RawView], neither it nor any of its descendants will insert a [RenderObject] into an existing render tree. Therefore, the [View] widget can only be used in those parts of the widget tree where it is not required to participate in the construction of the surrounding render tree. In other words, the widget may only be used in a non-rendering zone of the widget tree (see [WidgetsBinding] for a definition of rendering and non-rendering zones).

In practical terms, the widget is typically used at the root of the widget tree outside of any other [View] or [RawView] widget, as a child of a [ViewCollection] widget, or in the [ViewAnchor.view] slot of a [ViewAnchor] widget. It is not required to be a direct child, though, since other non-[RenderObjectWidget]s (e.g. [InheritedWidget]s, [Builder]s, or [StatefulWidget]s/[StatelessWidget]s that only produce non-[RenderObjectWidget]s) are allowed to be present between those widgets and the [View] widget.

See also:

- [RawView], the workhorse that [View] uses to create the render tree, but without the [MediaQuery] and [FocusScope] that [View] adds.
- [Element.debugExpectsRenderObjectForSlot], which defines whether a [View] widget is allowed in a given child slot.

### View()

```dart
View({dynamic key, required FlutterView view, PipelineOwner? deprecatedDoNotUseWillBeRemovedWithoutNoticePipelineOwner, RenderView? deprecatedDoNotUseWillBeRemovedWithoutNoticeRenderView, required Widget child})
```

Create a [View] widget to bootstrap a render tree that is rendered into the provided [FlutterView].

The content rendered into that [view] is determined by the given [child] widget.

### view

```dart
FlutterView view
```

The [FlutterView] into which [child] is drawn.

### child

```dart
Widget child
```

The widget below this widget in the tree, which will be drawn into the [view].

{@macro flutter.widgets.ProxyWidget.child}

### maybeOf()

```dart
FlutterView? maybeOf(BuildContext context)
```

Returns the [FlutterView] that the provided `context` will render into.

Returns null if the `context` is not associated with a [FlutterView].

The method creates a dependency on the `context`, which will be informed when the identity of the [FlutterView] changes (i.e. the `context` is moved to render into a different [FlutterView] then before). The context will not be informed when the _properties_ on the [FlutterView] itself change their values. To access the property values of a [FlutterView] it is best practice to use [MediaQuery.maybeOf] instead, which will ensure that the `context` is informed when the view properties change.

See also:

- [View.of], which throws instead of returning null if no [FlutterView] is found.

### of()

```dart
FlutterView of(BuildContext context)
```

Returns the [FlutterView] that the provided `context` will render into.

Throws if the `context` is not associated with a [FlutterView].

The method creates a dependency on the `context`, which will be informed when the identity of the [FlutterView] changes (i.e. the `context` is moved to render into a different [FlutterView] then before). The context will not be informed when the _properties_ on the [FlutterView] itself change their values. To access the property values of a [FlutterView] prefer using the access methods on [MediaQuery], such as [MediaQuery.sizeOf], which will ensure that the `context` is informed when the view properties change.

See also:

- [View.maybeOf], which throws instead of returning null if no [FlutterView] is found.

### pipelineOwnerOf()

```dart
PipelineOwner pipelineOwnerOf(BuildContext context)
```

Returns the [PipelineOwner] parent to which a child [View] should attach its [PipelineOwner] to.

If `context` has a [View] ancestor, it returns the [PipelineOwner] responsible for managing the render tree of that view. If there is no [View] ancestor, [RendererBinding.rootPipelineOwner] is returned instead.

### createState()

```dart
State<View> createState()
```

# RawView

```dart
class RawView extends StatelessWidget {}
```

The lower level workhorse widget for [View] that bootstraps a render tree for a view.

Typically, the [View] widget is used instead of a [RawView] widget to create a view, since, in addition to creating a view, it also adds some useful widgets, such as a [MediaQuery] and [FocusScope]. The [RawView] widget is only used directly if it is not desirable to have these additional widgets around the resulting widget tree. The [View] widget uses the [RawView] widget internally to manage its [FlutterView].

This widget can be used at the root of the widget tree outside of any other [View] or [RawView] widget, as a child to a [ViewCollection], or in the [ViewAnchor.view] slot of a [ViewAnchor] widget. It is not required to be a direct child of those widgets; other non-[RenderObjectWidget]s may appear in between the two (such as an [InheritedWidget]).

Each [FlutterView] can be associated with at most one [View] or [RawView] widget in the widget tree. Two or more [View] or [RawView] widgets configured with the same [FlutterView] must never exist within the same widget tree at the same time. This limitation is enforced by a [GlobalObjectKey] that derives its identity from the [view] provided to this widget.

Since the [RawView] widget bootstraps its own independent render tree, neither it nor any of its descendants will insert a [RenderObject] into an existing render tree. Therefore, the [RawView] widget can only be used in those parts of the widget tree where it is not required to participate in the construction of the surrounding render tree. In other words, the widget may only be used in a non-rendering zone of the widget tree (see [WidgetsBinding] for a definition of rendering and non-rendering zones).

To find the [FlutterView] associated with a [BuildContext], use [View.of] or [View.maybeOf], even if the view was created using [RawView] instead of [View].

See also:

- [View] for a higher level interface that also sets up a [MediaQuery] and [FocusScope] for the view's widget tree.

### RawView()

```dart
RawView({dynamic key, required FlutterView view, PipelineOwner? deprecatedDoNotUseWillBeRemovedWithoutNoticePipelineOwner, RenderView? deprecatedDoNotUseWillBeRemovedWithoutNoticeRenderView, required Widget child})
```

Creates a [RawView] widget.

### view

```dart
FlutterView view
```

The [FlutterView] into which [child] is drawn.

### child

```dart
Widget child
```

The widget below this widget in the tree, which will be drawn into the [view].

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# ViewCollection

```dart
class ViewCollection extends _MultiChildComponentWidget {}
```

A collection of sibling [View]s.

This widget can only be used in places were a [View] widget is allowed, i.e. in a non-rendering zone of the widget tree. In practical terms, it can be used at the root of the widget tree outside of any [View] widget, as a child to a another [ViewCollection], or in the [ViewAnchor.view] slot of a [ViewAnchor] widget. It is not required to be a direct child of those widgets; other non-[RenderObjectWidget]s may appear in between the two (such as an [InheritedWidget]).

Similarly, the [views] children of this widget must be [View]s, but they may be wrapped in additional non-[RenderObjectWidget]s (e.g. [InheritedWidget]s).

See also:

- [WidgetsBinding] for an explanation of rendering and non-rendering zones.

### ViewCollection()

```dart
ViewCollection({dynamic key, required List<Widget> views})
```

Creates a [ViewCollection] widget.

### views

```dart
List<Widget> get views
```

The [View] descendants of this widget.

The [View]s may be wrapped in other non-[RenderObjectWidget]s (e.g. [InheritedWidget]s). However, no [RenderObjectWidget] is allowed to appear between the [ViewCollection] and the next [View] widget.

# ViewAnchor

```dart
class ViewAnchor extends StatelessWidget {}
```

Decorates a [child] widget with a side [View].

This widget must have a [View] ancestor, into which the [child] widget is rendered.

Typically, a [View] or [ViewCollection] widget is used in the [view] slot to define the content of the side view(s). Those widgets may be wrapped in other non-[RenderObjectWidget]s (e.g. [InheritedWidget]s). However, no [RenderObjectWidget] is allowed to appear between the [ViewAnchor] and the next [View] widget in the [view] slot. The widgets in the [view] slot have access to all [InheritedWidget]s above the [ViewAnchor] in the tree.

In technical terms, the [ViewAnchor] can only be used in a rendering zone of the widget tree and the [view] slot marks the start of a new non-rendering zone (see [WidgetsBinding] for a definition of these zones). Typically, it is occupied by a [View] widget, which will start a new rendering zone.

{@template flutter.widgets.ViewAnchor} An example use case for this widget is a tooltip for a button. The tooltip should be able to extend beyond the bounds of the main view. For this, the tooltip can be implemented as a separate [View], which is anchored to the button in the main view by wrapping that button with a [ViewAnchor]. In this example, the [view] slot is configured with the tooltip [View] and the [child] is the button widget rendered into the surrounding view. {@endtemplate}

### ViewAnchor()

```dart
ViewAnchor({dynamic key, Widget? view, required Widget child})
```

Creates a [ViewAnchor] widget.

### view

```dart
Widget? view
```

The widget that defines the view anchored to this widget.

Typically, a [View] or [ViewCollection] widget is used, which may be wrapped in other non-[RenderObjectWidget]s (e.g. [InheritedWidget]s).

{@macro flutter.widgets.ViewAnchor}

### child

```dart
Widget child
```

The widget below this widget in the tree.

It is rendered into the surrounding view, not in the view defined by [view].

{@macro flutter.widgets.ViewAnchor}

### build()

```dart
Widget build(BuildContext context)
```
