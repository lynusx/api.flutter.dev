@docImport 'package:flutter/material.dart';

@docImport 'text_selection.dart';

# MagnifierBuilder

```dart
typedef MagnifierBuilder = Widget? Function(BuildContext context, MagnifierController controller, ValueNotifier<MagnifierInfo> magnifierInfo)
```

Signature for a builder that builds a [Widget] with a [MagnifierController].

The builder is called exactly once per magnifier.

If the `controller` parameter's [MagnifierController.animationController] field is set (by the builder) to an [AnimationController], the [MagnifierController] will drive the animation during entry and exit.

The `magnifierInfo` parameter is updated with new [MagnifierInfo] instances during the lifetime of the built magnifier, e.g. as the user moves their finger around the text field.

# MagnifierInfo

```dart
class MagnifierInfo {}
```

A data class that contains the geometry information of text layouts and selection gestures, used to position magnifiers.

### MagnifierInfo()

```dart
MagnifierInfo({required Offset globalGesturePosition, required Rect caretRect, required Rect fieldBounds, required Rect currentLineBoundaries})
```

Constructs a [MagnifierInfo] from provided geometry values.

### empty

```dart
MagnifierInfo empty
```

Const [MagnifierInfo] with all values set to 0.

### globalGesturePosition

```dart
Offset globalGesturePosition
```

The offset of the gesture position that the magnifier should be shown at.

### currentLineBoundaries

```dart
Rect currentLineBoundaries
```

The rect of the current line the magnifier should be shown at, without taking into account any padding of the field; only the position of the first and last character.

### caretRect

```dart
Rect caretRect
```

The rect of the handle that the magnifier should follow.

### fieldBounds

```dart
Rect fieldBounds
```

The bounds of the entire text field that the magnifier is bound to.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# TextMagnifierConfiguration

```dart
class TextMagnifierConfiguration {}
```

A configuration object for a magnifier (e.g. in a text field).

In general, most features of the magnifier can be configured by controlling the widgets built by the [magnifierBuilder].

### TextMagnifierConfiguration()

```dart
TextMagnifierConfiguration({MagnifierBuilder? magnifierBuilder, bool shouldDisplayHandlesInMagnifier = true})
```

Constructs a [TextMagnifierConfiguration] from parts.

If [magnifierBuilder] is null, a default [MagnifierBuilder] will be used that does not build a magnifier.

### magnifierBuilder

```dart
MagnifierBuilder get magnifierBuilder
```

The builder callback that creates the widget that renders the magnifier.

### shouldDisplayHandlesInMagnifier

```dart
bool shouldDisplayHandlesInMagnifier
```

Whether a magnifier should show the text editing handles or not.

This flag is used by [SelectionOverlay.showMagnifier] to control the order of layers in the rendering; specifically, whether to place the layer containing the handles above or below the layer containing the magnifier in the [Overlay].

### disabled

```dart
TextMagnifierConfiguration disabled
```

A constant for a [TextMagnifierConfiguration] that is disabled, meaning it never builds anything, regardless of platform.

# MagnifierController

```dart
class MagnifierController {}
```

A controller for a magnifier.

[MagnifierController]'s main benefit over holding a raw [OverlayEntry] is that [MagnifierController] will handle logic around waiting for a magnifier to animate in or out.

If a magnifier chooses to have an entry / exit animation, it should provide the animation controller to [MagnifierController.animationController]. [MagnifierController] will then drive the [AnimationController] and wait for it to be complete before removing it from the [Overlay].

To check the status of the magnifier, see [MagnifierController.shown].

### MagnifierController()

```dart
MagnifierController({AnimationController? animationController})
```

If there is no in / out animation for the magnifier, [animationController] should be left null.

### animationController

```dart
AnimationController? animationController
```

The controller that will be driven in / out when show / hide is triggered, respectively.

### overlayEntry

```dart
OverlayEntry? get overlayEntry
```

The magnifier's [OverlayEntry], if currently in the overlay.

This is exposed so that other overlay entries can be positioned above or below this [overlayEntry]. Anything in the paint order after the [RawMagnifier] in this [OverlayEntry] will not be displayed in the magnifier; if it is desired for an overlay entry to be displayed in the magnifier, it _must_ be positioned below the magnifier.

{@tool snippet}

```dart
void magnifierShowExample(BuildContext context) {
  final MagnifierController myMagnifierController = MagnifierController();

  // Placed below the magnifier, so it will show.
  Overlay.of(context).insert(OverlayEntry(
      builder: (BuildContext context) => const Text('I WILL display in the magnifier')));

  // Will display in the magnifier, since this entry was passed to show.
  final OverlayEntry displayInMagnifier = OverlayEntry(
      builder: (BuildContext context) =>
          const Text('I WILL display in the magnifier'));

  Overlay.of(context)
      .insert(displayInMagnifier);
  myMagnifierController.show(
      context: context,
      below: displayInMagnifier,
      builder: (BuildContext context) => const RawMagnifier(
            size: Size(100, 100),
          ));

  // By default, new entries will be placed over the top entry.
  Overlay.of(context).insert(OverlayEntry(
      builder: (BuildContext context) => const Text('I WILL NOT display in the magnifier')));

  Overlay.of(context).insert(
      below:
          myMagnifierController.overlayEntry, // Explicitly placed below the magnifier.
      OverlayEntry(
          builder: (BuildContext context) => const Text('I WILL display in the magnifier')));
}
```

{@end-tool}

To check if a magnifier is in the overlay, use [shown]. The [overlayEntry] field may be non-null even when the magnifier is not visible.

### shown

```dart
bool get shown
```

Whether the magnifier is currently being shown.

This is false when nothing is in the overlay, when the [animationController] is in the [AnimationStatus.dismissed] state, or when the [animationController] is animating out (i.e. in the [AnimationStatus.reverse] state).

It is true in the opposite cases, i.e. when the overlay is not empty, and either the [animationController] is null, in the [AnimationStatus.completed] state, or in the [AnimationStatus.forward] state.

### show()

```dart
Future<void> show({required BuildContext context, required WidgetBuilder builder, Widget? debugRequiredFor, OverlayEntry? below})
```

Displays the magnifier.

Returns a future that completes when the magnifier is fully shown, i.e. done with its entry animation.

To control what overlays are shown in the magnifier, use `below`. See [overlayEntry] for more details on how to utilize `below`.

If the magnifier already exists (i.e. [overlayEntry] != null), then [show] will replace the old overlay without playing an exit animation. Consider awaiting [hide] first, to animate from the old magnifier to the new one.

### hide()

```dart
Future<void> hide({bool removeFromOverlay = true})
```

Schedules a hide of the magnifier.

If this [MagnifierController] has an [AnimationController], then [hide] reverses the animation controller and waits for the animation to complete. Then, if [removeFromOverlay] is true, remove the magnifier from the overlay.

In general, `removeFromOverlay` should be true, unless the magnifier needs to preserve states between shows / hides.

See also:

- [removeFromOverlay] which removes the [OverlayEntry] from the [Overlay] synchronously.

### removeFromOverlay()

```dart
void removeFromOverlay()
```

Remove the [OverlayEntry] from the [Overlay].

This method removes the [OverlayEntry] synchronously, regardless of exit animation: this leads to abrupt removals of [OverlayEntry]s with animations.

To allow the [OverlayEntry] to play its exit animation, consider calling [hide] instead, with `removeFromOverlay` set to true, and optionally await the returned Future.

### shiftWithinBounds()

```dart
Rect shiftWithinBounds({required Rect rect, required Rect bounds})
```

A utility for calculating a new [Rect] from [rect] such that [rect] is fully constrained within [bounds].

Any point in the output rect is guaranteed to also be a point contained in [bounds].

It is a runtime error for [rect].width to be greater than [bounds].width, and it is also an error for [rect].height to be greater than [bounds].height.

This algorithm translates [rect] the shortest distance such that it is entirely within [bounds].

If [rect] is already within [bounds], no shift will be applied to [rect] and [rect] will be returned as-is.

It is perfectly valid for the output rect to have a point along the edge of the [bounds]. If the desired output rect requires that no edges are parallel to edges of [bounds], see [Rect.deflate] by 1 on [bounds] to achieve this effect.

# MagnifierDecoration

```dart
class MagnifierDecoration {}
```

The decorations to put around the loupe in a [RawMagnifier].

See also:

- [Decoration], a more general solution for [DecoratedBox].

### MagnifierDecoration()

```dart
MagnifierDecoration({double opacity = 1.0, List<BoxShadow>? shadows, ShapeBorder shape = const RoundedRectangleBorder()})
```

Constructs a [MagnifierDecoration].

By default, [MagnifierDecoration] is a rectangular magnifier with no shadows, and fully opaque.

### opacity

```dart
double opacity
```

The opacity of the magnifier and decorations around the magnifier.

When this is 1.0, the magnified image shows in the [shape] of the magnifier. When this is less than 1.0, the magnified image is transparent and shows through the unmagnified background.

Generally this is only useful for animating the magnifier in and out, as a transparent magnifier looks quite confusing.

### shadows

```dart
List<BoxShadow>? shadows
```

A list of shadows cast by the [shape].

If the shadows are offset, consider setting [RawMagnifier.clipBehavior] to [Clip.hardEdge] (or similar) to ensure the shadow does not occlude the magnifier (the shadow is drawn above the magnifier).

If the shadows are _not_ offset, consider using [BlurStyle.outer] in the shadows instead, to avoid having to introduce a clip.

In the event that [shape] consists of a stack of borders, the shadow is drawn using the bounds of the last one.

See also:

- [kElevationToShadow], which defines some shadows for Material design. Those shadows use [BlurStyle.normal] and may need to be converted to [BlurStyle.outer] for use with [MagnifierDecoration].

### shape

```dart
ShapeBorder shape
```

The shape of the magnifier and the outline (border) around it.

Shapes can be stacked (using the `+` operator). In that case, the magnifier and shadow are drawn according to the outside edge of the last shape, with the borders painted on top.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# RawMagnifier

```dart
class RawMagnifier extends StatelessWidget {}
```

A common base class for magnifiers.

{@tool dartpad} This sample demonstrates what a magnifier is, and how it can be used.

** See code in examples/api/lib/widgets/magnifier/magnifier.0.dart ** {@end-tool}

{@template flutter.widgets.magnifier.intro} This magnifying glass is useful for scenarios on mobile devices where the user's finger may be covering part of the screen where a granular action is being performed, such as navigating a small cursor with a drag gesture, on an image or text. {@endtemplate}

A magnifier can be conveniently managed by [MagnifierController], which handles showing and hiding the magnifier, with an optional entry / exit animation.

See:

- [MagnifierController], a controller to handle magnifiers in an overlay.

### RawMagnifier()

```dart
RawMagnifier({dynamic key, Widget? child, MagnifierDecoration decoration = const MagnifierDecoration(), Clip clipBehavior = Clip.none, Offset focalPointOffset = Offset.zero, double magnificationScale = 1, required Size size})
```

Constructs a [RawMagnifier].

By default, this magnifier uses the default [MagnifierDecoration] (which draws nothing), the focal point is directly under the magnifier, and there is no magnification; this means that a default magnifier will be entirely invisible to the naked eye, painting exactly what is under it, exactly where it was painted originally.

### child

```dart
Widget? child
```

An optional widget to position inside the len of the [RawMagnifier].

This is positioned over the [RawMagnifier] - it may be useful for tinting the [RawMagnifier], or drawing a crosshair-like UI.

### decoration

```dart
MagnifierDecoration decoration
```

This magnifier's decoration.

This sets the shape of the loupe, plus any borders and shadows that it casts. The default has no border and no shadow; combined with the default [magnificationScale] of 1.0, this results in the magnifier having no visible effect.

If the [decoration] has a [MagnifierDecoration.shadows] that uses offset shadows or uses a [BlurStyle] that would obscure the magnified image, consider setting [clipBehavior] to [Clip.hardEdge] (or similar) to ensure the magnified image is visible.

### clipBehavior

```dart
Clip clipBehavior
```

Whether and how to clip the parts of [decoration] that render inside the loupe.

Defaults to [Clip.none].

See the discussion at [decoration].

### focalPointOffset

```dart
Offset focalPointOffset
```

The offset of the magnifier from [RawMagnifier]'s center.

{@template flutter.widgets.magnifier.offset} For example, if [RawMagnifier] is globally positioned at Offset(100, 100), and [focalPointOffset] is Offset(-20, -20), then [RawMagnifier] will see the content at global offset (80, 80).

If left as [Offset.zero], the [RawMagnifier] will show the content that is directly below it. {@endtemplate}

### magnificationScale

```dart
double magnificationScale
```

How "zoomed in" the magnification subject is in the lens.

The default is 1.0, which is no magnification.

### size

```dart
Size size
```

The size of the magnifier.

This does not include the border from the [decoration]; it only includes the size of the magnifier.

### build()

```dart
Widget build(BuildContext context)
```
