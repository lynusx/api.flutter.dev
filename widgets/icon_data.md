@docImport 'dart:ui'; @docImport 'package:flutter/material.dart';

@docImport 'basic.dart'; @docImport 'icon.dart';

# IconData

```dart
final class IconData {}
```

A description of an icon fulfilled by a font glyph.

See [Icons] for a number of predefined icons available for material design applications.

In release builds, the Flutter tool will tree shake out of bundled fonts the code points (or instances of [IconData]) which are not referenced from Dart app code. See the [staticIconProvider] annotation for more details.

### IconData()

```dart
IconData(int codePoint, {String? fontFamily, String? fontPackage, bool matchTextDirection = false, List<String>? fontFamilyFallback})
```

Creates icon data.

Rarely used directly. Instead, consider using one of the predefined icons like the [Icons] collection.

The [fontFamily] argument is normally required when using custom icons.

e.g. When using a [codePoint] from a `CustomIcons` font

```yaml
fonts:
  - family: CustomIcons
    fonts:
      - asset: assets/fonts/CustomIcons.ttf
```

`IconData` usages should specify `fontFamily: 'CustomIcons'`.

The [fontPackage] argument must be non-null when using a font family that is included in a package. This is used when selecting the font.

Instantiating non-const instances of this class in your app will mean the app cannot be built in release mode with icon tree-shaking (it need to be explicitly opted out at build time). See [staticIconProvider] for more context.

### codePoint

```dart
int codePoint
```

The Unicode code point at which this icon is stored in the icon font.

### fontFamily

```dart
String? fontFamily
```

The font family from which the glyph for the [codePoint] will be selected.

### fontPackage

```dart
String? fontPackage
```

The name of the package from which the font family is included.

The name is used by the [Icon] widget when configuring the [TextStyle] so that the given [fontFamily] is obtained from the appropriate asset.

See also:

- [TextStyle], which describes how to use fonts from other packages.

### matchTextDirection

```dart
bool matchTextDirection
```

Whether this icon should be automatically mirrored in right-to-left environments.

The [Icon] widget respects this value by mirroring the icon when the [Directionality] is [TextDirection.rtl].

### fontFamilyFallback

```dart
List<String>? fontFamilyFallback
```

The ordered list of font families to fall back on when a glyph cannot be found in a higher priority font family.

For more details, refer to the documentation of [TextStyle]

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

# IconDataProperty

```dart
class IconDataProperty extends DiagnosticsProperty<IconData> {}
```

[DiagnosticsProperty] that has an [IconData] as value.

### IconDataProperty()

```dart
IconDataProperty(String name, dynamic value, {dynamic ifNull, dynamic showName, dynamic style, dynamic level})
```

Create a diagnostics property for [IconData].

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

# staticIconProvider

```dart
Object staticIconProvider
```

Annotation for classes that only provide static const [IconData] instances.

This is a hint to the font tree shaker to ignore the constant instances of [IconData] appearing in the declaration of this class when tree-shaking unused code points from the bundled font.

Classes with this annotation must have only "static const" members. The presence of any non-const [IconData] instances will preclude apps importing the declaration into their application from being able to use icon tree-shaking during release builds, resulting in larger font assets.

```dart
@staticIconProvider
abstract final class MyCustomIcons {
  static const String fontFamily = 'MyCustomIcons';
  static const IconData happyFace = IconData(1, fontFamily: fontFamily);
  static const IconData sadFace = IconData(2, fontFamily: fontFamily);
}
```
