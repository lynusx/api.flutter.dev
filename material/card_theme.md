@docImport 'card.dart'; @docImport 'material.dart';

# CardTheme

```dart
class CardTheme extends InheritedWidget with Diagnosticable {}
```

Defines default property values for descendant [Card] widgets.

Descendant widgets obtain the current [CardThemeData] object using [CardTheme.of]. Instances of [CardThemeData] can be customized with [CardThemeData.copyWith].

Typically a [CardThemeData] is specified as part of the overall [Theme] with [ThemeData.cardTheme].

All [CardThemeData] properties are `null` by default. When null, the [Card] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### CardTheme()

```dart
CardTheme({dynamic key, Clip? clipBehavior, Color? color, Color? surfaceTintColor, Color? shadowColor, double? elevation, EdgeInsetsGeometry? margin, ShapeBorder? shape, CardThemeData? data, Widget? child})
```

Creates a theme that can be used for [ThemeData.cardTheme].

The [elevation] must be null or non-negative.

### clipBehavior

```dart
Clip? get clipBehavior
```

Overrides the default value for [Card.clipBehavior].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.clipBehavior] property in [data] instead.

### color

```dart
Color? get color
```

Overrides the default value for [Card.color].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.color] property in [data] instead.

### surfaceTintColor

```dart
Color? get surfaceTintColor
```

Overrides the default value for [Card.surfaceTintColor].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.surfaceTintColor] property in [data] instead.

### shadowColor

```dart
Color? get shadowColor
```

Overrides the default value for [Card.shadowColor].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.shadowColor] property in [data] instead.

### elevation

```dart
double? get elevation
```

Overrides the default value for [Card.elevation].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.elevation] property in [data] instead.

### margin

```dart
EdgeInsetsGeometry? get margin
```

Overrides the default value for [Card.margin].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.margin] property in [data] instead.

### shape

```dart
ShapeBorder? get shape
```

Overrides the default value for [Card.shape].

This property is obsolete and will be deprecated in a future release: please use the [CardThemeData.shape] property in [data] instead.

### data

```dart
CardThemeData get data
```

The properties used for all descendant [Card] widgets.

### copyWith()

```dart
CardTheme copyWith({Clip? clipBehavior, Color? color, Color? shadowColor, Color? surfaceTintColor, double? elevation, EdgeInsetsGeometry? margin, ShapeBorder? shape})
```

Creates a copy of this object with the given fields replaced with the new values.

This method is obsolete and will be deprecated in a future release: please use the [CardThemeData.copyWith] instead.

### of()

```dart
CardThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [CardTheme] ancestor.

If there is no ancestor, it returns [ThemeData.cardTheme].

Typical usage is as follows:

```dart
CardThemeData theme = CardTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(CardTheme oldWidget)
```

### lerp()

```dart
CardTheme lerp(CardTheme? a, CardTheme? b, double t)
```

Linearly interpolate between two Card themes.

{@macro dart.ui.shadow.lerp}

This method is obsolete and will be deprecated in a future release: please use the [CardThemeData.lerp] instead.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# CardThemeData

```dart
class CardThemeData with Diagnosticable {}
```

Defines default property values for descendant [Card] widgets.

Descendant widgets obtain the current [CardThemeData] object using `CardTheme.of(context)`. Instances of [CardThemeData] can be customized with [CardThemeData.copyWith].

Typically a [CardThemeData] is specified as part of the overall [Theme] with [ThemeData.cardTheme].

All [CardThemeData] properties are `null` by default. When null, the [Card] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults. See the individual [Card] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### CardThemeData()

```dart
CardThemeData({Clip? clipBehavior, Color? color, Color? shadowColor, Color? surfaceTintColor, double? elevation, EdgeInsetsGeometry? margin, ShapeBorder? shape})
```

Creates a theme that can be used for [ThemeData.cardTheme].

The [elevation] must be null or non-negative.

### clipBehavior

```dart
Clip? clipBehavior
```

Overrides the default value for [Card.clipBehavior].

### color

```dart
Color? color
```

Overrides the default value for [Card.color].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value for [Card.shadowColor].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value for [Card.surfaceTintColor].

### elevation

```dart
double? elevation
```

Overrides the default value for [Card.elevation].

### margin

```dart
EdgeInsetsGeometry? margin
```

Overrides the default value for [Card.margin].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value for [Card.shape].

### copyWith()

```dart
CardThemeData copyWith({Clip? clipBehavior, Color? color, Color? shadowColor, Color? surfaceTintColor, double? elevation, EdgeInsetsGeometry? margin, ShapeBorder? shape})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
CardThemeData lerp(CardThemeData? a, CardThemeData? b, double t)
```

Linearly interpolate between two Card themes.

{@macro dart.ui.shadow.lerp}

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
