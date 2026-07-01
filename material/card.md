@docImport 'dialog.dart'; @docImport 'ink_well.dart'; @docImport 'list_tile.dart';

# Card

```dart
class Card extends StatelessWidget {}
```

A Material Design card: a panel with slightly rounded corners and an elevation shadow.

A card is a sheet of [Material] used to represent some related information, for example an album, a geographical location, a meal, contact details, etc.

This is what it looks like when run:

![A card with a slight shadow, consisting of two rows, one with an icon and some text describing a musical, and the other with buttons for buying tickets or listening to the show.](https://flutter.github.io/assets-for-api-docs/assets/material/card.png)

{@tool dartpad} This sample shows creation of a [Card] widget that shows album information and two actions.

** See code in examples/api/lib/material/card/card.0.dart ** {@end-tool}

Sometimes the primary action area of a card is the card itself. Cards can be one large touch target that shows a detail screen when tapped.

{@tool dartpad} This sample shows creation of a [Card] widget that can be tapped. When tapped this [Card]'s [InkWell] displays an "ink splash" that fills the entire card.

** See code in examples/api/lib/material/card/card.1.dart ** {@end-tool}

For Material Design 2 (when [ThemeData.useMaterial3] is false), there is a single card type: the elevated card. In that mode the named constructors ([Card.filled], [Card.outlined]) behave the same as the default [Card].

For Material Design 3 (when [ThemeData.useMaterial3] is true), three visual variants are available: the default [Card] (elevated), [Card.filled], and [Card.outlined]. All variants share the same theme class, [CardThemeData], so theme properties (for example [CardThemeData.shape]) apply to every card variant within the theme's scope.

{@tool dartpad} This sample shows creation of [Card] widgets for elevated, filled and outlined types, as described in: https://m3.material.io/components/cards/overview

** See code in examples/api/lib/material/card/card.2.dart ** {@end-tool}

See also:

- [ListTile], to display icons and text in a card.
- [showDialog], to display a modal card.
- <https://material.io/design/components/cards.html>
- <https://m3.material.io/components/cards>

### Card()

```dart
Card({dynamic key, Color? color, Color? shadowColor, Color? surfaceTintColor, double? elevation, ShapeBorder? shape, bool borderOnForeground = true, EdgeInsetsGeometry? margin, Clip? clipBehavior, Widget? child, bool semanticContainer = true})
```

Creates an elevated variant of Card.

Elevated cards have a drop shadow, providing more separation from the background than filled cards, but less than outlined cards.

The [elevation] must be null or non-negative.

### Card.filled()

```dart
Card.filled({dynamic key, Color? color, Color? shadowColor, Color? surfaceTintColor, double? elevation, ShapeBorder? shape, bool borderOnForeground = true, EdgeInsetsGeometry? margin, Clip? clipBehavior, Widget? child, bool semanticContainer = true})
```

Create a filled variant of Card.

Filled cards provide subtle separation from the background. This has less emphasis than elevated cards (the default) or outlined cards.

If [ThemeData.useMaterial3] is false, this constructor is equivalent to the default constructor of [Card].

### Card.outlined()

```dart
Card.outlined({dynamic key, Color? color, Color? shadowColor, Color? surfaceTintColor, double? elevation, ShapeBorder? shape, bool borderOnForeground = true, EdgeInsetsGeometry? margin, Clip? clipBehavior, Widget? child, bool semanticContainer = true})
```

Create an outlined variant of Card.

Outlined cards have a visual boundary around the container. This can provide greater emphasis than the other types.

The card's outline is defined by the [shape] property. By default, the card uses a [RoundedRectangleBorder] with a 12.0 corner radius, a 1.0 border width, and the color from [ColorScheme.outlineVariant]. If you provide a custom [shape], it is recommended to use an [OutlinedBorder] with a non-null [OutlinedBorder.side] to keep a visible outline.

If [ThemeData.useMaterial3] is false, this constructor is equivalent to the default constructor of [Card].

### color

```dart
Color? color
```

The card's background color.

Defines the card's [Material.color].

If this property is null then the ambient [CardTheme.color] is used. If that is null, and [ThemeData.useMaterial3] is true, then [ColorScheme.surfaceContainerLow] of [ThemeData.colorScheme] is used. Otherwise, [ThemeData.cardColor] is used.

### shadowColor

```dart
Color? shadowColor
```

The color to paint the shadow below the card.

If null then the ambient [CardThemeData.shadowColor] is used. If that's null too, then the overall theme's [ThemeData.shadowColor] (default black) is used.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The color used as an overlay on [color] to indicate elevation.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If this is null, no overlay will be applied. Otherwise this color will be composited on top of [color] with an opacity related to [elevation] and used to paint the background of the card.

The default is [Colors.transparent].

See [Material.surfaceTintColor] for more details on how this overlay is applied.

### elevation

```dart
double? elevation
```

The z-coordinate at which to place this card. This controls the size of the shadow below the card.

Defines the card's [Material.elevation].

If this property is null then the ambient [CardThemeData.elevation] is used. If that's null, the default value is 1.0.

### shape

```dart
ShapeBorder? shape
```

The shape of the card's [Material].

Defines the card's [Material.shape].

If null, the ambient [CardTheme.shape] from [ThemeData.cardTheme] is used. If that is also null, the shape defaults to a [RoundedRectangleBorder]. The default corner radius is 12.0 when [ThemeData.useMaterial3] is true, and 4.0 otherwise. For Material 3 outlined cards, the default [shape] also includes a border side (see [OutlinedBorder.side]).

### borderOnForeground

```dart
bool borderOnForeground
```

Whether to paint the [shape] border in front of the [child].

The default value is true. If false, the border will be painted behind the [child].

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

If this property is null then the ambient [CardThemeData.clipBehavior] is used. If that's null then the behavior will be [Clip.none].

### margin

```dart
EdgeInsetsGeometry? margin
```

The empty space that surrounds the card.

Defines the card's outer [Container.margin].

If this property is null then the ambient [CardThemeData.margin] is used. If that's null, the default margin is 4.0 logical pixels on all sides: `EdgeInsets.all(4.0)`.

### semanticContainer

```dart
bool semanticContainer
```

Whether this widget represents a single semantic container, or if false a collection of individual semantic nodes.

Defaults to true.

Setting this flag to true will attempt to merge all child semantics into this node. Setting this flag to false will force all child semantic nodes to be explicit.

This flag should be false if the card contains multiple different types of content.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```
