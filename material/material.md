@docImport 'card.dart'; @docImport 'color_scheme.dart'; @docImport 'colors.dart'; @docImport 'ink_decoration.dart'; @docImport 'ink_highlight.dart'; @docImport 'ink_splash.dart'; @docImport 'ink_well.dart'; @docImport 'list_tile.dart'; @docImport 'material_button.dart'; @docImport 'mergeable_material.dart';

# RectCallback

```dart
typedef RectCallback = Rect Function()
```

Signature for the callback used by ink effects to obtain the rectangle for the effect.

Used by [InkHighlight] and [InkSplash], for example.

# MaterialType

```dart
enum MaterialType {}
```

The various kinds of material in Material Design. Used to configure the default behavior of [Material] widgets.

See also:

- [Material], in particular [Material.type].
- [kMaterialEdges]

Rectangle using default theme canvas color.

Rounded edges, card theme color.

A circle, no color by default (used for floating action buttons).

Rounded edges, no color by default (used for [MaterialButton] buttons).

A transparent piece of material that draws ink splashes and highlights.

While the material metaphor describes child widgets as printed on the material itself and do not hide ink effects, in practice the [Material] widget draws child widgets on top of the ink effects. A [Material] with type transparency can be placed on top of opaque widgets to show ink effects on top of them.

Prefer using the [Ink] widget for showing ink effects on top of opaque widgets.

# kMaterialEdges

```dart
Map<MaterialType, BorderRadius?> kMaterialEdges
```

The border radii used by the various kinds of material in Material Design.

See also:

- [MaterialType]
- [Material]

# MaterialInkController

```dart
abstract class MaterialInkController {}
```

An interface for creating [InkSplash]s and [InkHighlight]s on a [Material].

Typically obtained via [Material.of].

### color

```dart
Color? get color
```

The color of the material.

### vsync

```dart
TickerProvider get vsync
```

The ticker provider used by the controller.

Ink features that are added to this controller with [addInkFeature] should use this vsync to drive their animations.

### addInkFeature()

```dart
void addInkFeature(InkFeature feature)
```

Add an [InkFeature], such as an [InkSplash] or an [InkHighlight].

The ink feature will paint as part of this controller.

### markNeedsPaint()

```dart
void markNeedsPaint()
```

Notifies the controller that one of its ink features needs to repaint.

# Material

```dart
class Material extends StatefulWidget {}
```

A piece of material.

The Material widget is responsible for:

1.  Clipping: If [clipBehavior] is not [Clip.none], Material clips its widget sub-tree to the shape specified by [shape], [type], and [borderRadius]. By default, [clipBehavior] is [Clip.none] for performance considerations. See [Ink] for an example of how this affects clipping [Ink] widgets.
2.  Elevation: Material elevates its widget sub-tree on the Z axis by [elevation] pixels, and draws the appropriate shadow.
3.  Ink effects: Material shows ink effects implemented by [InkFeature]s like [InkSplash] and [InkHighlight] below its children.

## The Material Metaphor

Material is the central metaphor in Material Design. Each piece of material exists at a given elevation, which influences how that piece of material visually relates to other pieces of material and how that material casts shadows.

Most user interface elements are either conceptually printed on a piece of material or themselves made of material. Material reacts to user input using [InkSplash] and [InkHighlight] effects. To trigger a reaction on the material, use a [MaterialInkController] obtained via [Material.of].

In general, the features of a [Material] should not change over time (e.g. a [Material] should not change its [color], [shadowColor] or [type]). Changes to [elevation], [shadowColor] and [surfaceTintColor] are animated for [animationDuration]. Changes to [shape] are animated if [type] is not [MaterialType.transparency] and [ShapeBorder.lerp] between the previous and next [shape] values is supported. Shape changes are also animated for [animationDuration].

## Shape

The shape for material is determined by [shape], [type], and [borderRadius].

- If [shape] is non null, it determines the shape.
- If [shape] is null and [borderRadius] is non null, the shape is a rounded rectangle, with corners specified by [borderRadius].
- If [shape] and [borderRadius] are null, [type] determines the shape as follows:
- [MaterialType.canvas]: the default material shape is a rectangle.
- [MaterialType.card]: the default material shape is a rectangle with rounded edges. The edge radii is specified by [kMaterialEdges].
- [MaterialType.circle]: the default material shape is a circle.
- [MaterialType.button]: the default material shape is a rectangle with rounded edges. The edge radii is specified by [kMaterialEdges].
- [MaterialType.transparency]: the default material shape is a rectangle.

## Border

If [shape] is not null, then its border will also be painted (if any).

## Layout change notifications

If the layout changes (e.g. because there's a list on the material, and it's been scrolled), a [LayoutChangedNotification] must be dispatched at the relevant subtree. This in particular means that transitions (e.g. [SlideTransition]) should not be placed inside [Material] widgets so as to move subtrees that contain [InkResponse]s, [InkWell]s, [Ink]s, or other widgets that use the [InkFeature] mechanism. Otherwise, in-progress ink features (e.g., ink splashes and ink highlights) won't move to account for the new layout.

## Painting over the material

Material widgets will often trigger reactions on their nearest material ancestor. For example, [ListTile.hoverColor] triggers a reaction on the tile's material when a pointer is hovering over it. These reactions will be obscured if any widget in between them and the material paints in such a way as to obscure the material (such as setting a [BoxDecoration.color] on a [DecoratedBox]). To avoid this behavior, use [InkDecoration] to decorate the material itself.

See also:

- [MergeableMaterial], a piece of material that can split and re-merge.
- [Card], a wrapper for a [Material] of [type] [MaterialType.card].
- <https://material.io/design/>
- <https://m3.material.io/styles/color/the-color-system/color-roles>

### Material()

```dart
Material({dynamic key, MaterialType type = MaterialType.canvas, double elevation = 0.0, Color? color, Color? shadowColor, Color? surfaceTintColor, TextStyle? textStyle, BorderRadiusGeometry? borderRadius, ShapeBorder? shape, bool borderOnForeground = true, Clip clipBehavior = Clip.none, Duration animationDuration = kThemeChangeDuration, Widget? child, bool animateColor = false})
```

Creates a piece of material.

The [elevation] must be non-negative.

If a [shape] is specified, then the [borderRadius] property must be null and the [type] property must not be [MaterialType.circle]. If the [borderRadius] is specified, then the [type] property must not be [MaterialType.circle]. In both cases, these restrictions are intended to catch likely errors.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### type

```dart
MaterialType type
```

The kind of material to show (e.g., card or canvas). This affects the shape of the widget, the roundness of its corners if the shape is rectangular, and the default color.

### animateColor

```dart
bool animateColor
```

Whether the color should be animated.

### elevation

```dart
double elevation
```

{@template flutter.material.material.elevation} The z-coordinate at which to place this material relative to its parent.

This controls the size of the shadow below the material and the opacity of the elevation overlay color if it is applied.

If this is non-zero, the contents of the material are clipped, because the widget conceptually defines an independent printed piece of material.

Defaults to 0. Changing this value will cause the shadow and the elevation overlay or surface tint to animate over [Material.animationDuration].

The value is non-negative.

See also:

- [ThemeData.useMaterial3] which defines whether a surface tint or elevation overlay is used to indicate elevation.
- [ThemeData.applyElevationOverlayColor] which controls the whether an overlay color will be applied to indicate elevation.
- [Material.color] which may have an elevation overlay applied.
- [Material.shadowColor] which will be used for the color of a drop shadow.
- [Material.surfaceTintColor] which will be used as the overlay tint to show elevation. {@endtemplate}

### color

```dart
Color? color
```

The color to paint the material.

Must be opaque. To create a transparent piece of material, use [MaterialType.transparency].

If [ThemeData.useMaterial3] is true then an optional [surfaceTintColor] overlay may be applied on top of this color to indicate elevation.

If [ThemeData.useMaterial3] is false and [ThemeData.applyElevationOverlayColor] is true and [ThemeData.brightness] is [Brightness.dark] then a semi-transparent overlay color will be composited on top of this color to indicate the elevation. This is no longer needed for Material Design 3, which uses [surfaceTintColor].

By default, the color is derived from the [type] of material.

### shadowColor

```dart
Color? shadowColor
```

The color to paint the shadow below the material.

{@template flutter.material.material.shadowColor} If null and [ThemeData.useMaterial3] is true then [ThemeData]'s [ColorScheme.shadow] will be used. If [ThemeData.useMaterial3] is false then [ThemeData.shadowColor] will be used.

To remove the drop shadow when [elevation] is greater than 0, set [shadowColor] to [Colors.transparent].

See also:

- [ThemeData.useMaterial3], which determines the default value for this property if it is null.
- [ThemeData.applyElevationOverlayColor], which turns elevation overlay on or off for dark themes. {@endtemplate}

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The color of the surface tint overlay applied to the material color to indicate elevation.

{@template flutter.material.material.surfaceTintColor} Material Design 3 introduced a new way for some components to indicate their elevation by using a surface tint color overlay on top of the base material [color]. This overlay is painted with an opacity that is related to the [elevation] of the material.

If [ThemeData.useMaterial3] is false, then this property is not used.

If [ThemeData.useMaterial3] is true and [surfaceTintColor] is not null and not [Colors.transparent], then it will be used to overlay the base [color] with an opacity based on the [elevation].

Otherwise, no surface tint will be applied.

See also:

- [ThemeData.useMaterial3], which turns this feature on.
- [ElevationOverlay.applySurfaceTint], which is used to implement the tint.
- https://m3.material.io/styles/color/the-color-system/color-roles which specifies how the overlay is applied. {@endtemplate}

### textStyle

```dart
TextStyle? textStyle
```

The typographical style to use for text within this material.

### shape

```dart
ShapeBorder? shape
```

Defines the material's shape as well its shadow.

{@template flutter.material.material.shape} If shape is non null, the [borderRadius] is ignored and the material's clip boundary and shadow are defined by the shape.

A shadow is only displayed if the [elevation] is greater than zero. {@endtemplate}

### borderOnForeground

```dart
bool borderOnForeground
```

Whether to paint the [shape] border in front of the [child].

The default value is true. If false, the border will be painted behind the [child].

### clipBehavior

```dart
Clip clipBehavior
```

{@template flutter.material.Material.clipBehavior} The content will be clipped (or not) according to this option.

See the enum [Clip] for details of all possible options and their common use cases. {@endtemplate}

Defaults to [Clip.none].

### animationDuration

```dart
Duration animationDuration
```

Defines the duration of animated changes for [shape], [elevation], [shadowColor], [surfaceTintColor] and the elevation overlay if it is applied.

The default value is [kThemeChangeDuration].

### borderRadius

```dart
BorderRadiusGeometry? borderRadius
```

If non-null, the corners of this box are rounded by this [BorderRadiusGeometry] value.

Otherwise, the corners specified for the current [type] of material are used.

If [shape] is non null then the border radius is ignored.

Must be null if [type] is [MaterialType.circle].

### maybeOf()

```dart
MaterialInkController? maybeOf(BuildContext context)
```

The ink controller from the closest instance of this class that encloses the given context within the closest [LookupBoundary].

Typical usage is as follows:

```dart
MaterialInkController? inkController = Material.maybeOf(context);
```

This method can be expensive (it walks the element tree).

See also:

- [Material.of], which is similar to this method, but asserts if no [Material] ancestor is found.

### of()

```dart
MaterialInkController of(BuildContext context)
```

The ink controller from the closest instance of [Material] that encloses the given context within the closest [LookupBoundary].

If no [Material] widget ancestor can be found then this method will assert in debug mode, and throw an exception in release mode.

Typical usage is as follows:

```dart
MaterialInkController inkController = Material.of(context);
```

This method can be expensive (it walks the element tree).

See also:

- [Material.maybeOf], which is similar to this method, but returns null if no [Material] ancestor is found.

### createState()

```dart
State<Material> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### defaultSplashRadius

```dart
double defaultSplashRadius
```

The default radius of an ink splash in logical pixels.

# InkFeature

```dart
abstract class InkFeature {}
```

A visual reaction on a piece of [Material].

To add an ink feature to a piece of [Material], obtain the [MaterialInkController] via [Material.of] and call [MaterialInkController.addInkFeature].

### InkFeature()

```dart
InkFeature({required MaterialInkController controller, required RenderBox referenceBox, VoidCallback? onRemoved})
```

Initializes fields for subclasses.

### controller

```dart
MaterialInkController get controller
```

The [MaterialInkController] associated with this [InkFeature].

Typically used by subclasses to call [MaterialInkController.markNeedsPaint] when they need to repaint.

### referenceBox

```dart
RenderBox referenceBox
```

The render box whose visual position defines the frame of reference for this ink feature.

### onRemoved

```dart
VoidCallback? onRemoved
```

Called when the ink feature is no longer visible on the material.

### dispose()

```dart
void dispose()
```

Free up the resources associated with this ink feature.

### paintFeature()

```dart
void paintFeature(Canvas canvas, Matrix4 transform)
```

Override this method to paint the ink feature.

The transform argument gives the coordinate conversion from the coordinate system of the canvas to the coordinate system of the [referenceBox].

### toString()

```dart
String toString()
```

# ShapeBorderTween

```dart
class ShapeBorderTween extends Tween<ShapeBorder?> {}
```

An interpolation between two [ShapeBorder]s.

This class specializes the interpolation of [Tween] to use [ShapeBorder.lerp].

### ShapeBorderTween()

```dart
ShapeBorderTween({dynamic begin, dynamic end})
```

Creates a [ShapeBorder] tween.

the [begin] and [end] properties may be null; see [ShapeBorder.lerp] for the null handling semantics.

### lerp()

```dart
ShapeBorder? lerp(double t)
```

Returns the value this tween has at the given animation clock value.
