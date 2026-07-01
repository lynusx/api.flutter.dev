@docImport 'app.dart'; @docImport 'color_scheme.dart'; @docImport 'text_theme.dart';

# kThemeAnimationDuration

```dart
Duration kThemeAnimationDuration
```

The duration over which theme changes animate by default.

# Theme

```dart
class Theme extends StatelessWidget {}
```

Applies a theme to descendant widgets.

A theme describes the colors and typographic choices of an application.

{@youtube 560 315 https://www.youtube.com/watch?v=oTvQDJOBXmM}

Descendant widgets obtain the current theme's [ThemeData] object using [Theme.of]. When a widget uses [Theme.of], it is automatically rebuilt if the theme later changes, so that the changes can be applied.

The [Theme] widget implies an [IconTheme] widget, set to the value of the [ThemeData.iconTheme] of the [data] for the [Theme].

To interact seamlessly with descendant Cupertino widgets, the [Theme] widget provides a [CupertinoTheme] for its descendants with a [CupertinoThemeData] inherited from the nearest ancestor [CupertinoTheme] or if none exists, derived from the Material [data] for the [Theme]. The values in the Material derived [CupertinoThemeData] are overridable through [ThemeData.cupertinoOverrideTheme]. The values from an inherited [CupertinoThemeData] can be overridden by wrapping the desired subtree with a [CupertinoTheme].

See also:

- [ThemeData], which describes the actual configuration of a theme.
- [AnimatedTheme], which animates the [ThemeData] when it changes rather than changing the theme all at once.
- [MaterialApp], which includes an [AnimatedTheme] widget configured via the [MaterialApp.theme] argument.

### Theme()

```dart
Theme({dynamic key, required ThemeData data, required Widget child})
```

Applies the given theme [data] to [child].

### data

```dart
ThemeData data
```

Specifies the color and typography values for descendant widgets.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### of()

```dart
ThemeData of(BuildContext context)
```

The data from the closest [Theme] instance that encloses the given context.

If the given context is enclosed in a [Localizations] widget providing [MaterialLocalizations], the returned data is localized according to the nearest available [MaterialLocalizations].

Defaults to [ThemeData.fallback] if there is no [Theme] in the given build context.

Typical usage is as follows:

```dart
@override
Widget build(BuildContext context) {
  return Text(
    'Example',
    style: Theme.of(context).textTheme.titleLarge,
  );
}
```

When the [Theme] is actually created in the same `build` function (possibly indirectly, e.g. as part of a [MaterialApp]), the `context` argument to the `build` function can't be used to find the [Theme] (since it's "above" the widget being returned). In such cases, the following technique with a [Builder] can be used to provide a new scope with a [BuildContext] that is "under" the [Theme]:

```dart
@override
Widget build(BuildContext context) {
  return MaterialApp(
    theme: ThemeData.light(),
    home: Builder(
      // Create an inner BuildContext so that we can refer to
      // the Theme with Theme.of().
      builder: (BuildContext context) {
        return Center(
          child: Text(
            'Example',
            style: Theme.of(context).textTheme.titleLarge,
          ),
        );
      },
    ),
  );
}
```

See also:

- [ColorScheme.of], a convenience method that returns [ThemeData.colorScheme] from the closest [Theme] ancestor. (equivalent to `Theme.of(context).colorScheme`).
- [TextTheme.of], a convenience method that returns [ThemeData.textTheme] from the closest [Theme] ancestor. (equivalent to `Theme.of(context).textTheme`).
- [IconTheme.of], that returns [ThemeData.iconTheme] from the closest [Theme] or [IconThemeData.fallback] if there is no [IconTheme] ancestor.

### brightnessOf()

```dart
Brightness brightnessOf(BuildContext context)
```

Retrieves the [Brightness] to use for descendant Material widgets, based on the value of [ThemeData.brightness] in the given [context].

If no [InheritedTheme] can be found in the given [context], or its `brightness` is null, it will fall back to [MediaQueryData.platformBrightness].

See also:

- [maybeBrightnessOf], which returns null if no valid [InheritedTheme] or [MediaQuery] exists.
- [ThemeData.brightness], the property that takes precedence over [MediaQueryData.platformBrightness] for descendant Material widgets.

### maybeBrightnessOf()

```dart
Brightness? maybeBrightnessOf(BuildContext context)
```

Retrieves the [Brightness] to use for descendant Material widgets, based on the value of [ThemeData.brightness] in the given [context].

If no [InheritedTheme] or [MediaQuery] can be found in the given [context], it will return null.

See also:

- [ThemeData.brightness], the property that takes precedence over [MediaQueryData.platformBrightness] for descendant Material widgets.
- [brightnessOf], which return a default value if no valid [InheritedTheme] or [MediaQuery] exists, instead of returning null.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ThemeDataTween

```dart
class ThemeDataTween extends Tween<ThemeData> {}
```

An interpolation between two [ThemeData]s.

This class specializes the interpolation of [Tween<ThemeData>] to call the [ThemeData.lerp] method.

See [Tween] for a discussion on how to use interpolation objects.

### ThemeDataTween()

```dart
ThemeDataTween({dynamic begin, dynamic end})
```

Creates a [ThemeData] tween.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### lerp()

```dart
ThemeData lerp(double t)
```

# AnimatedTheme

```dart
class AnimatedTheme extends ImplicitlyAnimatedWidget {}
```

Animated version of [Theme] which automatically transitions the colors, etc, over a given duration whenever the given theme changes.

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.elasticInOut]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_theme.mp4}

See also:

- [Theme], which [AnimatedTheme] uses to actually apply the interpolated theme.
- [ThemeData], which describes the actual configuration of a theme.
- [MaterialApp], which includes an [AnimatedTheme] widget configured via the [MaterialApp.theme] argument.

### AnimatedTheme()

```dart
AnimatedTheme({dynamic key, required ThemeData data, dynamic curve, dynamic duration = kThemeAnimationDuration, dynamic onEnd, required Widget child})
```

Creates an animated theme.

By default, the theme transition uses a linear curve.

### data

```dart
ThemeData data
```

Specifies the color and typography values for descendant widgets.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
AnimatedWidgetBaseState<AnimatedTheme> createState()
```
