# CarouselViewThemeData

```dart
class CarouselViewThemeData with Diagnosticable {}
```

Defines default property values for descendant [CarouselView] widgets.

Descendant widgets obtain the current [CarouselViewThemeData] object using [CarouselViewTheme.of]. Instances of [CarouselViewThemeData] can be customized with [CarouselViewThemeData.copyWith].

Typically a [CarouselViewThemeData] is specified as part of the overall [Theme] with [ThemeData.carouselViewTheme].

All [CarouselViewThemeData] properties are `null` by default. When null, the [CarouselView] will provide its own defaults.

See also:

- [CarouselViewTheme], an [InheritedWidget] that propagates the theme to its descendants.
- [ThemeData], which describes the overall theme information for the application.

### CarouselViewThemeData()

```dart
CarouselViewThemeData({double? elevation, Color? backgroundColor, WidgetStateProperty<Color?>? overlayColor, OutlinedBorder? shape, EdgeInsets? padding, Clip? itemClipBehavior})
```

Creates a theme that can be used for [ThemeData.carouselViewTheme].

### padding

```dart
EdgeInsets? padding
```

The amount of space to surround each carousel item with.

Overrides the default value for [CarouselView.padding].

### backgroundColor

```dart
Color? backgroundColor
```

The background color for each carousel item.

Overrides the default value for [CarouselView.backgroundColor].

### elevation

```dart
double? elevation
```

The z-coordinate of each carousel item.

This controls the size of the shadow below the carousel.

Overrides the default value for [CarouselView.elevation].

### shape

```dart
OutlinedBorder? shape
```

The shape of the carousel item's [Material].

Overrides the default value for [CarouselView.shape].

### itemClipBehavior

```dart
Clip? itemClipBehavior
```

The clip behavior for each carousel item.

The item content will be clipped (or not) according to this option. Refer to the [Clip] enum for more details on the different clip options.

Overrides the default value for [CarouselView.itemClipBehavior].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

The highlight color to indicate the carousel items are in pressed, hovered or focused states.

Overrides the default value for [CarouselView.overlayColor].

### copyWith()

```dart
CarouselViewThemeData copyWith({Color? backgroundColor, double? elevation, OutlinedBorder? shape, WidgetStateProperty<Color?>? overlayColor, EdgeInsets? padding, Clip? itemClipBehavior})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
CarouselViewThemeData lerp(CarouselViewThemeData? a, CarouselViewThemeData? b, double t)
```

Linearly interpolate between two carousel themes.

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

# CarouselViewTheme

```dart
class CarouselViewTheme extends InheritedTheme {}
```

Applies a carousel theme to descendant [CarouselView] widgets.

Descendant widgets obtain the current theme's [CarouselViewThemeData] using [CarouselViewTheme.of]. When a widget uses [CarouselViewTheme.of], it is automatically rebuilt if the theme later changes.

A carousel theme can be specified as part of the overall Material theme using [ThemeData.carouselViewTheme].

See also:

- [CarouselViewThemeData], which describes the actual configuration of a carousel theme.
- [Theme], which controls the overall theme inheritance.

### CarouselViewTheme()

```dart
CarouselViewTheme({dynamic key, required CarouselViewThemeData data, required dynamic child})
```

Creates a carousel theme that configures all descendant [CarouselView] widgets.

### data

```dart
CarouselViewThemeData data
```

The properties for descendant carousel widgets.

### of()

```dart
CarouselViewThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [CarouselViewTheme] ancestor.

If there is no ancestor, it returns [ThemeData.carouselViewTheme].

Typical usage is as follows:

```dart
CarouselViewThemeData theme = CarouselViewTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

Wraps the given [child] with a [CarouselViewTheme] containing the [data].

### updateShouldNotify()

```dart
bool updateShouldNotify(CarouselViewTheme oldWidget)
```

Returns true if the [data] fields of the two themes are different.
