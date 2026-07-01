@docImport 'input_decorator.dart';

# InputBorder

```dart
abstract class InputBorder extends ShapeBorder {}
```

Defines the appearance of an [InputDecorator]'s border.

An input decorator's border is specified by [InputDecoration.border].

The border is drawn relative to the input decorator's "container" which is the optionally filled area above the decorator's helper, error, and counter.

Input border's are decorated with a line whose weight and color are defined by [borderSide]. The input decorator's renderer animates the input border's appearance in response to state changes, like gaining or losing the focus, by creating new copies of its input border with [copyWith].

See also:

- [UnderlineInputBorder], the default [InputDecorator] border which draws a horizontal line at the bottom of the input decorator's container.
- [OutlineInputBorder], an [InputDecorator] border which draws a rounded rectangle around the input decorator's container.
- [InputDecoration], which is used to configure an [InputDecorator].

### InputBorder()

```dart
InputBorder({BorderSide borderSide = BorderSide.none})
```

Creates a border for an [InputDecorator].

Applications typically do not specify a [borderSide] parameter because the [InputDecorator] substitutes its own, using [copyWith], based on the current theme and [InputDecorator.isFocused].

### none

```dart
InputBorder none
```

No input border.

Use this value with [InputDecoration.border] to specify that no border should be drawn. The [InputDecoration.collapsed] constructor sets its border to this value.

### borderSide

```dart
BorderSide borderSide
```

Defines the border line's color and weight.

The [InputDecorator] creates copies of its input border, using [copyWith], based on the current theme and [InputDecorator.isFocused].

### copyWith()

```dart
InputBorder copyWith({BorderSide? borderSide})
```

Creates a copy of this input border with the specified `borderSide`.

### isOutline

```dart
bool get isOutline
```

True if this border will enclose the [InputDecorator]'s container.

This property affects the alignment of container's contents. For example when an input decorator is configured with an [OutlineInputBorder] its label is centered with its container.

### paint()

```dart
void paint(Canvas canvas, Rect rect, {double? gapStart, double gapExtent = 0.0, double gapPercentage = 0.0, TextDirection? textDirection})
```

Paint this input border on [canvas].

The [rect] parameter bounds the [InputDecorator]'s container.

The additional `gap` parameters reflect the state of the [InputDecorator]'s floating label. When an input decorator gains the focus, its label animates upwards, to make room for the input child. The [gapStart] and [gapExtent] parameters define a floating label width interval, and [gapPercentage] defines the animation's progress (0.0 to 1.0).

# UnderlineInputBorder

```dart
class UnderlineInputBorder extends InputBorder {}
```

Draws a horizontal line at the bottom of an [InputDecorator]'s container and defines the container's shape.

The input decorator's "container" is the optionally filled area above the decorator's helper, error, and counter.

See also:

- [OutlineInputBorder], an [InputDecorator] border which draws a rounded rectangle around the input decorator's container.
- [InputDecoration], which is used to configure an [InputDecorator].

### UnderlineInputBorder()

```dart
UnderlineInputBorder({dynamic borderSide = const BorderSide(), BorderRadius borderRadius = const BorderRadius.only(topLeft: Radius.circular(4.0), topRight: Radius.circular(4.0))})
```

Creates an underline border for an [InputDecorator].

The [borderSide] parameter defaults to [BorderSide.none] (it must not be null). Applications typically do not specify a [borderSide] parameter because the input decorator substitutes its own, using [copyWith], based on the current theme and [InputDecorator.isFocused].

The [borderRadius] parameter defaults to a value where the top left and right corners have a circular radius of 4.0.

### borderRadius

```dart
BorderRadius borderRadius
```

The radii of the border's rounded rectangle corners.

When this border is used with a filled input decorator, see [InputDecoration.filled], the border radius defines the shape of the background fill as well as the bottom left and right edges of the underline itself.

By default the top right and top left corners have a circular radius of 4.0.

### isOutline

```dart
bool get isOutline
```

### copyWith()

```dart
UnderlineInputBorder copyWith({BorderSide? borderSide, BorderRadius? borderRadius})
```

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

### scale()

```dart
UnderlineInputBorder scale(double t)
```

### getInnerPath()

```dart
Path getInnerPath(Rect rect, {TextDirection? textDirection})
```

### getOuterPath()

```dart
Path getOuterPath(Rect rect, {TextDirection? textDirection})
```

### paintInterior()

```dart
void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection})
```

### preferPaintInterior

```dart
bool get preferPaintInterior
```

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

### paint()

```dart
void paint(Canvas canvas, Rect rect, {double? gapStart, double gapExtent = 0.0, double gapPercentage = 0.0, TextDirection? textDirection})
```

Draw a horizontal line at the bottom of [rect].

The [borderSide] defines the line's color and weight. The `textDirection` `gap` and `textDirection` parameters are ignored.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# OutlineInputBorder

```dart
class OutlineInputBorder extends InputBorder {}
```

Draws a rounded rectangle around an [InputDecorator]'s container.

When the input decorator's label is floating, for example because its input child has the focus, the label appears in a gap in the border outline.

The input decorator's "container" is the optionally filled area above the decorator's helper, error, and counter.

See also:

- [UnderlineInputBorder], the default [InputDecorator] border which draws a horizontal line at the bottom of the input decorator's container.
- [ShapedInputBorder], an [InputDecorator] border which draws a custom [ShapeBorder] around the input decorator's container.
- [InputDecoration], which is used to configure an [InputDecorator].

### OutlineInputBorder()

```dart
OutlineInputBorder({dynamic borderSide = const BorderSide(), BorderRadius borderRadius = const BorderRadius.all(Radius.circular(4.0)), double gapPadding = 4.0})
```

Creates a rounded rectangle outline border for an [InputDecorator].

If the [borderSide] parameter is [BorderSide.none], it will not draw a border. However, it will still define a shape (which you can see if [InputDecoration.filled] is true).

If an application does not specify a [borderSide] parameter of value [BorderSide.none], the input decorator substitutes its own, using [copyWith], based on the current theme and [InputDecorator.isFocused].

The [borderRadius] parameter defaults to a value where all four corners have a circular radius of 4.0. The corner radii must be circular, i.e. their [Radius.x] and [Radius.y] values must be the same.

See also:

- [InputDecoration.floatingLabelBehavior], which should be set to [FloatingLabelBehavior.never] when the [borderSide] is [BorderSide.none]. If left as [FloatingLabelBehavior.auto], the label will extend beyond the container as if the border were still being drawn.

### gapPadding

```dart
double gapPadding
```

Horizontal padding on either side of the border's [InputDecoration.labelText] width gap.

This value is used by the [paint] method to compute the actual gap width.

### borderRadius

```dart
BorderRadius borderRadius
```

The radii of the border's rounded rectangle corners.

The corner radii must be circular, i.e. their [Radius.x] and [Radius.y] values must be the same.

### isOutline

```dart
bool get isOutline
```

### copyWith()

```dart
OutlineInputBorder copyWith({BorderSide? borderSide, BorderRadius? borderRadius, double? gapPadding})
```

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

### scale()

```dart
OutlineInputBorder scale(double t)
```

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

### getInnerPath()

```dart
Path getInnerPath(Rect rect, {TextDirection? textDirection})
```

### getOuterPath()

```dart
Path getOuterPath(Rect rect, {TextDirection? textDirection})
```

### paintInterior()

```dart
void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection})
```

### preferPaintInterior

```dart
bool get preferPaintInterior
```

### paint()

```dart
void paint(Canvas canvas, Rect rect, {double? gapStart, double gapExtent = 0.0, double gapPercentage = 0.0, TextDirection? textDirection})
```

Draw a rounded rectangle around [rect] using [borderRadius].

The [borderSide] defines the line's color and weight.

The top side of the rounded rectangle may be interrupted by a single gap if [gapExtent] is non-null. In that case the gap begins at `gapStart - gapPadding` (assuming that the [textDirection] is [TextDirection.ltr]). The gap's width is `(gapPadding + gapExtent + gapPadding) * gapPercentage`.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# ShapedInputBorder

```dart
class ShapedInputBorder extends InputBorder {}
```

Draws a custom shape around an [InputDecorator]'s container.

This border allows any [ShapeBorder] to be used as an input decorator border. This provides maximum flexibility for custom border shapes while maintaining the gap functionality for floating labels.

When the input decorator's label is floating, for example because its input child has the focus, the label appears in a gap in the border outline.

The input decorator's "container" is the optionally filled area above the decorator's helper, error, and counter.

{@tool dartpad} This sample shows how to use [ShapedInputBorder] with different [ShapeBorder] implementations.

** See code in examples/api/lib/material/shaped_input_border/shaped_input_border.0.dart ** {@end-tool}

See also:

- [OutlineInputBorder], a traditional rounded rectangle border.
- [UnderlineInputBorder], the default [InputDecorator] border which draws a horizontal line at the bottom of the input decorator's container.
- [RoundedSuperellipseBorder], which can be used with this border for iOS-style shapes.
- [InputDecoration], which is used to configure an [InputDecorator].

### ShapedInputBorder()

```dart
ShapedInputBorder({dynamic borderSide = const BorderSide(), required ShapeBorder shape, double gapPadding = 4.0})
```

Creates a shaped outline border for an [InputDecorator].

The [shape] parameter defines the custom border shape. It can be any [ShapeBorder] such as [RoundedSuperellipseBorder], [StadiumBorder], [BeveledRectangleBorder], or a custom shape.

If the [borderSide] parameter is [BorderSide.none], it will not draw a border. However, it will still define a shape (which you can see if [InputDecoration.filled] is true).

If an application does not specify a [borderSide] parameter of value [BorderSide.none], the input decorator substitutes its own, using [copyWith], based on the current theme and [InputDecorator.isFocused].

See also:

- [InputDecoration.floatingLabelBehavior], which should be set to [FloatingLabelBehavior.never] when the [borderSide] is [BorderSide.none]. If left as [FloatingLabelBehavior.auto], the label will extend beyond the container as if the border were still being drawn.

### gapPadding

```dart
double gapPadding
```

Horizontal padding on either side of the border's [InputDecoration.labelText] width gap.

This value is used by the [paint] method to compute the actual gap width.

### shape

```dart
ShapeBorder shape
```

The shape of the border.

### isOutline

```dart
bool get isOutline
```

### copyWith()

```dart
ShapedInputBorder copyWith({BorderSide? borderSide, ShapeBorder? shape, double? gapPadding})
```

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

### scale()

```dart
ShapedInputBorder scale(double t)
```

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

### getInnerPath()

```dart
Path getInnerPath(Rect rect, {TextDirection? textDirection})
```

### getOuterPath()

```dart
Path getOuterPath(Rect rect, {TextDirection? textDirection})
```

### paintInterior()

```dart
void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection})
```

### preferPaintInterior

```dart
bool get preferPaintInterior
```

### paint()

```dart
void paint(Canvas canvas, Rect rect, {double? gapStart, double gapExtent = 0.0, double gapPercentage = 0.0, TextDirection? textDirection})
```

Draw the custom shape around [rect].

The [borderSide] defines the line's color and weight.

The top side of the border may be interrupted by a single gap if [gapExtent] is non-null. In that case the gap begins at `gapStart - gapPadding` (assuming that the [textDirection] is [TextDirection.ltr]). The gap's width is `(gapPadding + gapExtent + gapPadding) * gapPercentage`.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```
