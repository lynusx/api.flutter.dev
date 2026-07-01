@docImport 'card.dart'; @docImport 'divider_theme.dart';

# MergeableMaterialItem

```dart
abstract class MergeableMaterialItem {}
```

The base type for [MaterialSlice] and [MaterialGap].

All [MergeableMaterialItem] objects need a [LocalKey].

### MergeableMaterialItem()

```dart
MergeableMaterialItem(LocalKey key)
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### key

```dart
LocalKey key
```

The key for this item of the list.

The key is used to match parts of the mergeable material from frame to frame so that state is maintained appropriately even as slices are added or removed.

# MaterialSlice

```dart
class MaterialSlice extends MergeableMaterialItem {}
```

A class that can be used as a child to [MergeableMaterial]. It is a slice of [Material] that animates merging with other slices.

All [MaterialSlice] objects need a [LocalKey].

### MaterialSlice()

```dart
MaterialSlice({required LocalKey key, required Widget child, Color? color})
```

Creates a slice of [Material] that's mergeable within a [MergeableMaterial].

### child

```dart
Widget child
```

The contents of this slice.

{@macro flutter.widgets.ProxyWidget.child}

### color

```dart
Color? color
```

Defines the color for the slice.

By default, the value of [color] is [ThemeData.cardColor].

### toString()

```dart
String toString()
```

# MaterialGap

```dart
class MaterialGap extends MergeableMaterialItem {}
```

A class that represents a gap within [MergeableMaterial].

All [MaterialGap] objects need a [LocalKey].

### MaterialGap()

```dart
MaterialGap({required LocalKey key, double size = 16.0})
```

Creates a Material gap with a given size.

### size

```dart
double size
```

The main axis extent of this gap. For example, if the [MergeableMaterial] is vertical, then this is the height of the gap.

### toString()

```dart
String toString()
```

# MergeableMaterial

```dart
class MergeableMaterial extends StatefulWidget {}
```

Displays a list of [MergeableMaterialItem] children. The list contains [MaterialSlice] items whose boundaries are either "merged" with adjacent items or separated by a [MaterialGap]. The [children] are distributed along the given [mainAxis] in the same way as the children of a [ListBody]. When the list of children changes, gaps are automatically animated open or closed as needed.

To enable this widget to correlate its list of children with the previous one, each child must specify a key.

When a new gap is added to the list of children the adjacent items are animated apart. Similarly when a gap is removed the adjacent items are brought back together.

When a new slice is added or removed, the app is responsible for animating the transition of the slices, while the gaps will be animated automatically.

See also:

- [Card], a piece of material that does not support splitting and merging but otherwise looks the same.

### MergeableMaterial()

```dart
MergeableMaterial({dynamic key, Axis mainAxis = Axis.vertical, double elevation = 2, bool hasDividers = false, List<MergeableMaterialItem> children = const <MergeableMaterialItem>[], Color? dividerColor})
```

Creates a mergeable Material list of items.

### children

```dart
List<MergeableMaterialItem> children
```

The children of the [MergeableMaterial].

### mainAxis

```dart
Axis mainAxis
```

The main layout axis.

### elevation

```dart
double elevation
```

The z-coordinate at which to place all the [Material] slices.

Defaults to 2, the appropriate elevation for cards.

### hasDividers

```dart
bool hasDividers
```

Whether connected pieces of [MaterialSlice] have dividers between them.

### dividerColor

```dart
Color? dividerColor
```

Defines color used for dividers if [hasDividers] is true.

If [dividerColor] is null, then [DividerThemeData.color] is used. If that is null, then [ThemeData.dividerColor] is used.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### createState()

```dart
State<MergeableMaterial> createState()
```
