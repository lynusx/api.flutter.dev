# CupertinoIconThemeData

```dart
class CupertinoIconThemeData extends IconThemeData with Diagnosticable {}
```

An [IconThemeData] subclass that automatically resolves its [color] when retrieved using [IconTheme.of].

### CupertinoIconThemeData()

```dart
CupertinoIconThemeData({dynamic size, dynamic fill, dynamic weight, dynamic grade, dynamic opticalSize, dynamic color, dynamic opacity, dynamic shadows, dynamic applyTextScaling})
```

Creates a [CupertinoIconThemeData].

### resolve()

```dart
IconThemeData resolve(BuildContext context)
```

Called by [IconTheme.of] to resolve [color] against the given [BuildContext].

### copyWith()

```dart
CupertinoIconThemeData copyWith({double? size, double? fill, double? weight, double? grade, double? opticalSize, Color? color, double? opacity, List<Shadow>? shadows, bool? applyTextScaling})
```

Creates a copy of this icon theme but with the given fields replaced with the new values.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
