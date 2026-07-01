# AnimatedIcon

```dart
class AnimatedIcon extends StatelessWidget {}
```

Shows an animated icon at a given animation [progress].

The available icons are specified in [AnimatedIcons].

{@youtube 560 315 https://www.youtube.com/watch?v=pJcbh8pbvJs}

{@tool dartpad} This example shows how to create an animated icon. The icon is animated forward and reverse in a loop.

** See code in examples/api/lib/material/animated_icon/animated_icon.0.dart ** {@end-tool}

See also:

- [Icons], for the list of available static Material Icons.

### AnimatedIcon()

```dart
AnimatedIcon({dynamic key, required AnimatedIconData icon, required Animation<double> progress, Color? color, double? size, String? semanticLabel, TextDirection? textDirection})
```

Creates an AnimatedIcon.

The [size] and [color] default to the value given by the current [IconTheme].

### progress

```dart
Animation<double> progress
```

The animation progress for the animated icon.

The value is clamped to be between 0 and 1.

This determines the actual frame that is displayed.

### color

```dart
Color? color
```

The color to use when drawing the icon.

Defaults to the current [IconTheme] color, if any.

The given color will be adjusted by the opacity of the current [IconTheme], if any.

In material apps, if there is a [Theme] without any [IconTheme]s specified, icon colors default to white if the theme is dark and black if the theme is light.

If no [IconTheme] and no [Theme] is specified, icons will default to black.

See [Theme] to set the current theme and [ThemeData.brightness] for setting the current theme's brightness.

### size

```dart
double? size
```

The size of the icon in logical pixels.

Icons occupy a square with width and height equal to size.

Defaults to the current [IconTheme] size.

### icon

```dart
AnimatedIconData icon
```

The icon to display. Available icons are listed in [AnimatedIcons].

### semanticLabel

```dart
String? semanticLabel
```

Semantic label for the icon.

Announced by assistive technologies (e.g TalkBack/VoiceOver). This label does not show in the UI.

See also:

- [SemanticsProperties.label], which is set to [semanticLabel] in the underlying [Semantics] widget.

### textDirection

```dart
TextDirection? textDirection
```

The text direction to use for rendering the icon.

If this is null, the ambient [Directionality] is used instead.

If the text direction is [TextDirection.rtl], the icon will be mirrored horizontally (e.g back arrow will point right).

### build()

```dart
Widget build(BuildContext context)
```
