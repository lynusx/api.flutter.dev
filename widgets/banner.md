@docImport 'package:flutter/material.dart';

@docImport 'app.dart';

# BannerLocation

```dart
enum BannerLocation {}
```

Where to show a [Banner].

The start and end locations are relative to the ambient [Directionality] (which can be overridden by [Banner.layoutDirection]).

Show the banner in the top-right corner when the ambient [Directionality] (or [Banner.layoutDirection]) is [TextDirection.rtl] and in the top-left corner when the ambient [Directionality] is [TextDirection.ltr].

Show the banner in the top-left corner when the ambient [Directionality] (or [Banner.layoutDirection]) is [TextDirection.rtl] and in the top-right corner when the ambient [Directionality] is [TextDirection.ltr].

Show the banner in the bottom-right corner when the ambient [Directionality] (or [Banner.layoutDirection]) is [TextDirection.rtl] and in the bottom-left corner when the ambient [Directionality] is [TextDirection.ltr].

Show the banner in the bottom-left corner when the ambient [Directionality] (or [Banner.layoutDirection]) is [TextDirection.rtl] and in the bottom-right corner when the ambient [Directionality] is [TextDirection.ltr].

# BannerPainter

```dart
class BannerPainter extends CustomPainter {}
```

Paints a [Banner].

### BannerPainter()

```dart
BannerPainter({required String message, required TextDirection textDirection, required BannerLocation location, required TextDirection layoutDirection, Color color = _kColor, TextStyle textStyle = _kTextStyle, BoxShadow shadow = _kShadow})
```

Creates a banner painter.

### message

```dart
String message
```

The message to show in the banner.

### textDirection

```dart
TextDirection textDirection
```

The directionality of the text.

This value is used to disambiguate how to render bidirectional text. For example, if the message is an English phrase followed by a Hebrew phrase, in a [TextDirection.ltr] context the English phrase will be on the left and the Hebrew phrase to its right, while in a [TextDirection.rtl] context, the English phrase will be on the right and the Hebrew phrase on its left.

See also:

- [layoutDirection], which controls the interpretation of values in [location].

### location

```dart
BannerLocation location
```

Where to show the banner (e.g., the upper right corner).

### layoutDirection

```dart
TextDirection layoutDirection
```

The directionality of the layout.

This value is used to interpret the [location] of the banner.

See also:

- [textDirection], which controls the reading direction of the [message].

### color

```dart
Color color
```

The color to paint behind the [message].

Defaults to a dark red.

### textStyle

```dart
TextStyle textStyle
```

The text style to use for the [message].

Defaults to bold, white text.

### shadow

```dart
BoxShadow shadow
```

The shadow properties for the banner.

Use a [BoxShadow] object to define the shadow's color, blur radius, and spread radius. These properties can be used to create different shadow effects.

### dispose()

```dart
void dispose()
```

Release resources held by this painter.

After calling this method, this object is no longer usable.

### paint()

```dart
void paint(Canvas canvas, Size size)
```

### shouldRepaint()

```dart
bool shouldRepaint(BannerPainter oldDelegate)
```

### hitTest()

```dart
bool hitTest(Offset position)
```

# Banner

```dart
class Banner extends StatefulWidget {}
```

Displays a diagonal message above the corner of another widget.

Useful for showing the execution mode of an app (e.g., that asserts are enabled.)

See also:

- [CheckedModeBanner], which the [WidgetsApp] widget includes by default in debug mode, to show a banner that says "DEBUG".

### Banner()

```dart
Banner({dynamic key, Widget? child, required String message, TextDirection? textDirection, required BannerLocation location, TextDirection? layoutDirection, Color color = _kColor, TextStyle textStyle = _kTextStyle, BoxShadow shadow = _kShadow})
```

Creates a banner.

### child

```dart
Widget? child
```

The widget to show behind the banner.

{@macro flutter.widgets.ProxyWidget.child}

### message

```dart
String message
```

The message to show in the banner.

### textDirection

```dart
TextDirection? textDirection
```

The directionality of the text.

This is used to disambiguate how to render bidirectional text. For example, if the message is an English phrase followed by a Hebrew phrase, in a [TextDirection.ltr] context the English phrase will be on the left and the Hebrew phrase to its right, while in a [TextDirection.rtl] context, the English phrase will be on the right and the Hebrew phrase on its left.

Defaults to the ambient [Directionality], if any.

See also:

- [layoutDirection], which controls the interpretation of the [location].

### location

```dart
BannerLocation location
```

Where to show the banner (e.g., the upper right corner).

### layoutDirection

```dart
TextDirection? layoutDirection
```

The directionality of the layout.

This is used to resolve the [location] values.

Defaults to the ambient [Directionality], if any.

See also:

- [textDirection], which controls the reading direction of the [message].

### color

```dart
Color color
```

The color of the banner.

### textStyle

```dart
TextStyle textStyle
```

The style of the text shown on the banner.

### shadow

```dart
BoxShadow shadow
```

The shadow properties for the banner.

Use a [BoxShadow] object to define the shadow's color, blur radius, and spread radius. These properties can be used to create different shadow effects.

### createState()

```dart
State<Banner> createState()
```

# CheckedModeBanner

```dart
class CheckedModeBanner extends StatelessWidget {}
```

Displays a [Banner] saying "DEBUG" when running in debug mode. [MaterialApp] builds one of these by default.

Does nothing in release mode.

### CheckedModeBanner()

```dart
CheckedModeBanner({dynamic key, required Widget child})
```

Creates a const debug mode banner.

### child

```dart
Widget child
```

The widget to show behind the banner.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
