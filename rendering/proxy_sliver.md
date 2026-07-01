# RenderProxySliver

```dart
abstract class RenderProxySliver extends RenderSliver with RenderObjectWithChildMixin<RenderSliver> {}
```

A base class for sliver render objects that resemble their children.

A proxy sliver has a single child and mimics all the properties of that child by calling through to the child for each function in the render sliver protocol. For example, a proxy sliver determines its geometry by asking its sliver child to layout with the same constraints and then matching the geometry.

A proxy sliver isn't useful on its own because you might as well just replace the proxy sliver with its child. However, RenderProxySliver is a useful base class for render objects that wish to mimic most, but not all, of the properties of their sliver child.

See also:

- [RenderProxyBox], a base class for render boxes that resemble their children.

### RenderProxySliver()

```dart
RenderProxySliver([RenderSliver? child])
```

Creates a proxy render sliver.

Proxy render slivers aren't created directly because they proxy the render sliver protocol to their sliver [child]. Instead, use one of the subclasses.

### semanticBounds

```dart
Rect get semanticBounds
```

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### performLayout()

```dart
void performLayout()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderSliver child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

# RenderSliverOpacity

```dart
class RenderSliverOpacity extends RenderProxySliver {}
```

Makes its sliver child partially transparent.

This class paints its sliver child into an intermediate buffer and then blends the sliver child back into the scene, partially transparent.

For values of opacity other than 0.0 and 1.0, this class is relatively expensive, because it requires painting the sliver child into an intermediate buffer. For the value 0.0, the sliver child is not painted at all. For the value 1.0, the sliver child is painted immediately without an intermediate buffer.

### RenderSliverOpacity()

```dart
RenderSliverOpacity({double opacity = 1.0, bool alwaysIncludeSemantics = false, RenderSliver? sliver})
```

Creates a partially transparent render object.

The [opacity] argument must be between 0.0 and 1.0, inclusive.

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### opacity

```dart
double get opacity
```

The fraction to scale the child's alpha value.

An opacity of one is fully opaque. An opacity of zero is fully transparent (i.e. invisible).

Values one and zero are painted with a fast path. Other values require painting the child into an intermediate buffer, which is expensive.

### opacity

```dart
set opacity(double value)
```

### alwaysIncludeSemantics

```dart
bool get alwaysIncludeSemantics
```

Whether child semantics are included regardless of the opacity.

If false, semantics are excluded when [opacity] is 0.0.

Defaults to false.

### alwaysIncludeSemantics

```dart
set alwaysIncludeSemantics(bool value)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverIgnorePointer

```dart
class RenderSliverIgnorePointer extends RenderProxySliver {}
```

A render object that is invisible during hit testing.

When [ignoring] is true, this render object (and its subtree) is invisible to hit testing. It still consumes space during layout and paints its sliver child as usual. It just cannot be the target of located events, because its render object returns false from [hitTest].

## Semantics

Using this class may also affect how the semantics subtree underneath is collected.

{@macro flutter.widgets.IgnorePointer.semantics}

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

### RenderSliverIgnorePointer()

```dart
RenderSliverIgnorePointer({RenderSliver? sliver, bool ignoring = true, bool? ignoringSemantics})
```

Creates a render object that is invisible to hit testing.

### ignoring

```dart
bool get ignoring
```

Whether this render object is ignored during hit testing.

Regardless of whether this render object is ignored during hit testing, it will still consume space during layout and be visible during painting.

{@macro flutter.widgets.IgnorePointer.semantics}

### ignoring

```dart
set ignoring(bool value)
```

### ignoringSemantics

```dart
bool? get ignoringSemantics
```

Whether the semantics of this render object is ignored when compiling the semantics tree.

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

### ignoringSemantics

```dart
set ignoringSemantics(bool? value)
```

### hitTest()

```dart
bool hitTest(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverOffstage

```dart
class RenderSliverOffstage extends RenderProxySliver {}
```

Lays the sliver child out as if it was in the tree, but without painting anything, without making the sliver child available for hit testing, and without taking any room in the parent.

### RenderSliverOffstage()

```dart
RenderSliverOffstage({bool offstage = true, RenderSliver? sliver})
```

Creates an offstage render object.

### offstage

```dart
bool get offstage
```

Whether the sliver child is hidden from the rest of the tree.

If true, the sliver child is laid out as if it was in the tree, but without painting anything, without making the sliver child available for hit testing, and without taking any room in the parent.

If false, the sliver child is included in the tree as normal.

### offstage

```dart
set offstage(bool value)
```

### performLayout()

```dart
void performLayout()
```

### hitTest()

```dart
bool hitTest(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# RenderSliverAnimatedOpacity

```dart
class RenderSliverAnimatedOpacity extends RenderProxySliver with RenderAnimatedOpacityMixin<RenderSliver> {}
```

Makes its sliver child partially transparent, driven from an [Animation].

This is a variant of [RenderSliverOpacity] that uses an [Animation<double>] rather than a [double] to control the opacity.

### RenderSliverAnimatedOpacity()

```dart
RenderSliverAnimatedOpacity({required Animation<double> opacity, bool alwaysIncludeSemantics = false, RenderSliver? sliver})
```

Creates a partially transparent render object.

# RenderSliverConstrainedCrossAxis

```dart
class RenderSliverConstrainedCrossAxis extends RenderProxySliver {}
```

Applies a cross-axis constraint to its sliver child.

This render object takes a [maxExtent] parameter and uses the smaller of [maxExtent] and the parent's [SliverConstraints.crossAxisExtent] as the cross axis extent of the [SliverConstraints] passed to the sliver child.

### RenderSliverConstrainedCrossAxis()

```dart
RenderSliverConstrainedCrossAxis({required double maxExtent})
```

Creates a render object that constrains the cross axis extent of its sliver child.

The [maxExtent] parameter must be nonnegative.

### maxExtent

```dart
double get maxExtent
```

The cross axis extent to apply to the sliver child.

This value must be nonnegative.

### maxExtent

```dart
set maxExtent(double value)
```

### performLayout()

```dart
void performLayout()
```

# RenderSliverSemanticsAnnotations

```dart
class RenderSliverSemanticsAnnotations extends RenderProxySliver with SemanticsAnnotationsMixin {}
```

Add annotations to the [SemanticsNode] for this subtree.

### RenderSliverSemanticsAnnotations()

```dart
RenderSliverSemanticsAnnotations({RenderSliver? child, required SemanticsProperties properties, bool container = false, bool explicitChildNodes = false, bool excludeSemantics = false, bool blockUserActions = false, Locale? localeForSubtree, TextDirection? textDirection})
```

Creates a render object that attaches a semantic annotation.

If the [SemanticsProperties.attributedLabel] is not null, the [textDirection] must also not be null.
