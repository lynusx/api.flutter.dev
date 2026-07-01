# SliverLayoutWidgetBuilder

```dart
typedef SliverLayoutWidgetBuilder = Widget Function(BuildContext context, SliverConstraints constraints)
```

The signature of the [SliverLayoutBuilder] builder function.

# SliverLayoutBuilder

```dart
class SliverLayoutBuilder extends ConstrainedLayoutBuilder<SliverConstraints> {}
```

Builds a sliver widget tree that can depend on its own [SliverConstraints].

Similar to the [LayoutBuilder] widget except its builder should return a sliver widget, and [SliverLayoutBuilder] is itself a sliver. The framework calls the [builder] function at layout time and provides the current [SliverConstraints]. The [SliverLayoutBuilder]'s final [SliverGeometry] will match the [SliverGeometry] of its child.

{@macro flutter.widgets.ConstrainedLayoutBuilder}

See also:

- [LayoutBuilder], the non-sliver version of this widget.

### SliverLayoutBuilder()

```dart
SliverLayoutBuilder({dynamic key, required Widget Function(BuildContext, InvalidType) builder})
```

Creates a sliver widget that defers its building until layout.

### createRenderObject()

```dart
RenderConstrainedLayoutBuilder<SliverConstraints, RenderSliver> createRenderObject(BuildContext context)
```
