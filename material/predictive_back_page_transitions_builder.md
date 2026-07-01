@docImport 'package:flutter/cupertino.dart';

@docImport 'page.dart';

# PredictiveBackPageTransitionsBuilder

```dart
class PredictiveBackPageTransitionsBuilder extends PageTransitionsBuilder {}
```

Used by [PageTransitionsTheme] to define a [MaterialPageRoute] page transition animation that looks like the default page transition used on Android U and above when using predictive back.

Predictive back is only supported on Android U and above, and if this [PageTransitionsBuilder] is used by any other platform, it will fall back to [FadeForwardsPageTransitionsBuilder].

When used on Android U and above, animates along with the back gesture to reveal the destination route. Can be canceled by dragging back towards the edge of the screen.

See also:

- [PredictiveBackFullscreenPageTransitionsBuilder], which is another variant of Android's predictive back page transition.
- [FadeForwardsPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android 16.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android 10.
- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android 9.
- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android 8.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- https://developer.android.com/design/ui/mobile/guides/patterns/predictive-back#shared-element-transition, which is the Android spec for this page transition, called the Shared Element page transition.

### PredictiveBackPageTransitionsBuilder()

```dart
PredictiveBackPageTransitionsBuilder({Color? fallbackColor})
```

Creates an instance of a [PageTransitionsBuilder] that matches Android U's predictive back transition.

### fallbackColor

```dart
Color? fallbackColor
```

The color of the scrim (background) when the predictive back transition is not supported.

If not provided, the background color of a default [FadeForwardsPageTransitionsBuilder] will be used.

### transitionDuration

```dart
Duration get transitionDuration
```

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

# PredictiveBackFullscreenPageTransitionsBuilder

```dart
class PredictiveBackFullscreenPageTransitionsBuilder extends PageTransitionsBuilder {}
```

Used by [PageTransitionsTheme] to define a [MaterialPageRoute] page transition animation that looks like Android's Full Screen page transition.

Predictive back is only supported on Android U and above, and if this [PageTransitionsBuilder] is used by any other platform, it will fall back to [ZoomPageTransitionsBuilder].

When used on Android U and above, animates along with the back gesture to reveal the destination route. Can be canceled by dragging back towards the edge of the screen.

See also:

- [PredictiveBackPageTransitionsBuilder], which is the default Android predictive back page transition.
- [FadeForwardsPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android 16.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android 10.
- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android 9.
- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android 8.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- https://developer.android.com/design/ui/mobile/guides/patterns/predictive-back#full-screen-surfaces, which is the native Android docs for this page transition.

### PredictiveBackFullscreenPageTransitionsBuilder()

```dart
PredictiveBackFullscreenPageTransitionsBuilder({Color? fallbackColor})
```

Creates an instance of a [PageTransitionsBuilder] that matches Android U's full screen predictive back transition.

### fallbackColor

```dart
Color? fallbackColor
```

The color of the scrim (background) when the predictive back transition is not supported.

If not provided, the background color of a default [ZoomPageTransitionsBuilder] will be used.

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```
