@docImport 'basic.dart'; @docImport 'single_child_scroll_view.dart'; @docImport 'sliver_layout_builder.dart';

# LayoutWidgetBuilder

```dart
typedef LayoutWidgetBuilder = Widget Function(BuildContext context, BoxConstraints constraints)
```

The signature of the [LayoutBuilder] builder function.

# AbstractLayoutBuilder

```dart
abstract class AbstractLayoutBuilder<LayoutInfoType> extends RenderObjectWidget {}
```

An abstract superclass for widgets that defer their building until layout.

Similar to the [Builder] widget except that the implementation calls the [builder] function at layout time and provides the [LayoutInfoType] that is required to configure the child widget subtree.

This is useful when the child widget tree relies on information that are only available during layout, and doesn't depend on the child's intrinsic size.

The [LayoutInfoType] should typically be immutable. The equality of the [LayoutInfoType] type is used by the implementation to avoid unnecessary rebuilds: if the new [LayoutInfoType] computed during layout is the same as (defined by `LayoutInfoType.==`) the previous [LayoutInfoType], the implementation will try to avoid calling the [builder] again unless [updateShouldRebuild] returns true. The corresponding [RenderObject] produced by this widget retains the most up-to-date [LayoutInfoType] for this purpose, which may keep a [LayoutInfoType] object in memory until the widget is removed from the tree.

Subclasses must return a [RenderObject] that mixes in [RenderAbstractLayoutBuilderMixin].

### AbstractLayoutBuilder()

```dart
AbstractLayoutBuilder({dynamic key})
```

Creates a widget that defers its building until layout.

### builder

```dart
Widget Function(BuildContext context, LayoutInfoType layoutInfo) get builder
```

Called at layout time to construct the widget tree.

The builder must not return null.

### createElement()

```dart
RenderObjectElement createElement()
```

### updateShouldRebuild()

```dart
bool updateShouldRebuild(AbstractLayoutBuilder<LayoutInfoType> oldWidget)
```

Whether [builder] needs to be called again even if the layout constraints are the same.

When this widget's configuration is updated, the [builder] callback most likely needs to be called to build this widget's child. However, subclasses may provide ways in which the widget can be updated without needing to rebuild the child. Such subclasses can use this method to tell the framework when the child widget should be rebuilt.

When this method is called by the framework, the newly configured widget is asked if it requires a rebuild, and it is passed the old widget as a parameter.

See also:

- [State.setState] and [State.didUpdateWidget], which talk about widget configuration changes and how they're triggered.
- [Element.update], the method that actually updates the widget's configuration.

### createRenderObject()

```dart
RenderAbstractLayoutBuilderMixin<LayoutInfoType, RenderObject> createRenderObject(BuildContext context)
```

# ConstrainedLayoutBuilder

```dart
abstract class ConstrainedLayoutBuilder<ConstraintType extends Constraints> extends AbstractLayoutBuilder<ConstraintType> {}
```

A specialized [AbstractLayoutBuilder] whose widget subtree depends on the incoming [ConstraintType] that will be imposed on the widget.

{@template flutter.widgets.ConstrainedLayoutBuilder} The [builder] function is called in the following situations:

- The first time the widget is laid out.
- When the parent widget passes different layout constraints.
- When the parent widget updates this widget and [updateShouldRebuild] returns `true`.
- When the dependencies that the [builder] function subscribes to change.

The [builder] function is _not_ called during layout if the parent passes the same constraints repeatedly.

In the event that an ancestor skips the layout of this subtree so the constraints become outdated, the `builder` rebuilds with the last known constraints. {@endtemplate}

### ConstrainedLayoutBuilder()

```dart
ConstrainedLayoutBuilder({dynamic key, required Widget Function(BuildContext context, ConstraintType constraints) builder})
```

Creates a widget that defers its building until layout.

### builder

```dart
Widget Function(BuildContext context, ConstraintType constraints) builder
```

# RenderAbstractLayoutBuilderMixin

```dart
mixin RenderAbstractLayoutBuilderMixin<LayoutInfoType, ChildType extends RenderObject> on RenderObjectWithChildMixin<ChildType>, RenderObjectWithLayoutCallbackMixin {}
```

Generic mixin for [RenderObject]s created by an [AbstractLayoutBuilder] with the same `LayoutInfoType`.

Provides a [layoutCallback] implementation which, if needed, invokes [AbstractLayoutBuilder]'s builder callback.

Implementers can override the [layoutInfo] implementation with a value that is safe to access in [layoutCallback], which is called in [performLayout]. The default [layoutInfo] returns the incoming [Constraints].

This mixin replaces [RenderConstrainedLayoutBuilder].

Change the layout callback.

### layoutCallback()

```dart
void layoutCallback()
```

Invokes the builder callback supplied via [AbstractLayoutBuilder] and rebuilds the [AbstractLayoutBuilder]'s widget tree, if needed.

No further work will be done if [layoutInfo] has not changed since the last time this method was called, and [AbstractLayoutBuilder.updateShouldRebuild] returned `false` when the widget was rebuilt.

This method should typically be called as soon as possible in the class's [performLayout] implementation, before any layout work is done.

### layoutInfo

```dart
LayoutInfoType get layoutInfo
```

The information to invoke the [AbstractLayoutBuilder.builder] callback with.

This is typically the information that are only made available in [performLayout], which is inaccessible for regular [Builder] widget, such as the incoming [Constraints], which are the default value.

# RenderConstrainedLayoutBuilder

```dart
typedef RenderConstrainedLayoutBuilder<LayoutInfoType, ChildType extends RenderObject> = RenderAbstractLayoutBuilderMixin<LayoutInfoType, ChildType>
```

Generic mixin for [RenderObject]s created by an [AbstractLayoutBuilder] with the same `LayoutInfoType`.

Use [RenderAbstractLayoutBuilderMixin] instead, which replaces this mixin.

# LayoutBuilder

```dart
class LayoutBuilder extends ConstrainedLayoutBuilder<BoxConstraints> {}
```

Builds a widget tree that can depend on the parent widget's size.

Similar to the [Builder] widget except that the framework calls the [builder] function at layout time and provides the parent widget's constraints. This is useful when the parent constrains the child's size and doesn't depend on the child's intrinsic size. The [LayoutBuilder]'s final size will match its child's size.

{@macro flutter.widgets.ConstrainedLayoutBuilder}

{@youtube 560 315 https://www.youtube.com/watch?v=IYDVcriKjsw}

If the child should be smaller than the parent, consider wrapping the child in an [Align] widget. If the child might want to be bigger, consider wrapping it in a [SingleChildScrollView] or [OverflowBox].

{@tool dartpad} This example uses a [LayoutBuilder] to build a different widget depending on the available width. Resize the DartPad window to see [LayoutBuilder] in action!

** See code in examples/api/lib/widgets/layout_builder/layout_builder.0.dart ** {@end-tool}

See also:

- [SliverLayoutBuilder], the sliver counterpart of this widget.
- [Builder], which calls a `builder` function at build time.
- [StatefulBuilder], which passes its `builder` function a `setState` callback.
- [CustomSingleChildLayout], which positions its child during layout.
- The [catalog of layout widgets](https://flutter.dev/widgets/layout/).

### LayoutBuilder()

```dart
LayoutBuilder({dynamic key, required Widget Function(BuildContext, InvalidType) builder})
```

Creates a widget that defers its building until layout.
