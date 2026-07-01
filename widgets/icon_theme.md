@docImport 'package:flutter/material.dart';

@docImport 'icon.dart'; @docImport 'image_icon.dart';

# IconTheme

```dart
class IconTheme extends InheritedTheme {}
```

Controls the default properties of icons in a widget subtree.

The icon theme is honored by [Icon] and [ImageIcon] widgets.

### IconTheme()

```dart
IconTheme({dynamic key, required IconThemeData data, required Widget child})
```

Creates an icon theme that controls properties of descendant widgets.

### merge()

```dart
Widget merge({Key? key, required IconThemeData data, required Widget child})
```

Creates an icon theme that controls the properties of descendant widgets, and merges in the current icon theme, if any.

### data

```dart
IconThemeData data
```

The set of properties to use for icons in this subtree.

### of()

```dart
IconThemeData of(BuildContext context)
```

The data from the closest instance of this class that encloses the given context, if any.

If there is no ambient icon theme, defaults to [IconThemeData.fallback]. The returned [IconThemeData] is concrete (all values are non-null; see [IconThemeData.isConcrete]). Any properties on the ambient icon theme that are null get defaulted to the values specified on [IconThemeData.fallback].

The [Theme] widget from the `material` library introduces an [IconTheme] widget set to the [ThemeData.iconTheme], so in a Material Design application, this will typically default to the icon theme from the ambient [Theme].

Typical usage is as follows:

```dart
IconThemeData theme = IconTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(IconTheme oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
