@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# PageTransitionsBuilder

```dart
abstract class PageTransitionsBuilder {}
```

Defines a page transition animation for a [PageRoute].

PageTransitionsBuilder can be used directly with widget layer primitives in any design system. Custom [PageRoute] subclasses can accept a PageTransitionsBuilder and delegate to its [buildTransitions] method when overriding [ModalRoute.buildTransitions]. This enables reusable transition animations that work with [Navigator] and other navigation primitives.

## Example usage

{@tool dartpad} This example shows how to create a custom [PageTransitionsBuilder] that slides the new page in from the right while fading it in, and how to use it with a custom [PageRoute].

** See code in examples/api/lib/widgets/page_transitions_builder/page_transitions_builder.0.dart ** {@end-tool}

As an example of usage, in the Material library this class is used by [PageTransitionsTheme] to define a [MaterialPageRoute] page transition animation. Apps can configure the map of builders for [ThemeData.pageTransitionsTheme] to customize the default [MaterialPageRoute] page transition animation for different platforms.

See also:

- [PageTransitionsTheme], which uses this class to configure page transitions.
- [MaterialPageRoute], which uses this class to build its transition.
- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android O.
- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android P.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android Q.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- [FadeForwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android U.

### PageTransitionsBuilder()

```dart
PageTransitionsBuilder()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### delegatedTransition

```dart
DelegatedTransitionBuilder? get delegatedTransition
```

Provides a secondary transition to the previous route.

{@macro flutter.widgets.delegatedTransition}

### transitionDuration

```dart
Duration get transitionDuration
```

{@macro flutter.widgets.TransitionRoute.transitionDuration}

Defaults to 300 milliseconds.

### reverseTransitionDuration

```dart
Duration get reverseTransitionDuration
```

{@macro flutter.widgets.TransitionRoute.reverseTransitionDuration}

Defaults to 300 milliseconds.

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T> route, BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

Wraps the child with one or more transition widgets which define how [route] arrives on and leaves the screen.

Subclasses override this method to create a transition animation.

The [MaterialPageRoute.buildTransitions] method is an example of a method that uses this to build a transition. It looks up the current [PageTransitionsTheme] with `Theme.of(context).pageTransitionsTheme` and delegates to this method with a [PageTransitionsBuilder] based on the theme's [ThemeData.platform].

# FadeUpwardsPageTransitionsBuilder

```dart
class FadeUpwardsPageTransitionsBuilder extends PageTransitionsBuilder {}
```

A page transition builder that animates incoming pages by fading and sliding them upwards.

This transition combines two animations:

- A fade-in effect using an ease-in curve
- An upward slide starting from 25% below the top of the screen

The resulting animation creates a smooth entrance effect where the new page appears to rise up while simultaneously becoming visible.

See also:

- [OpenUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android P.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android Q.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- [PredictiveBackPageTransitionsBuilder], which defines a page transition that allows peeking behind the current route on Android U and above.

### FadeUpwardsPageTransitionsBuilder()

```dart
FadeUpwardsPageTransitionsBuilder()
```

Constructs a page transition animation that slides the page up.

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T>? route, BuildContext? context, Animation<double> animation, Animation<double>? secondaryAnimation, Widget child)
```

# OpenUpwardsPageTransitionsBuilder

```dart
class OpenUpwardsPageTransitionsBuilder extends PageTransitionsBuilder {}
```

A page transition builder that animates incoming pages by revealing them from bottom to top with a clipping effect.

This transition combines several animations:

- A clip animation that gradually reveals the new page from bottom to top
- A subtle upward slide of the new page (5% translation)
- A slight upward movement of the old page (2.5% translation)
- A darkening scrim effect on the background

The resulting animation creates a layered effect where the new page appears to open upward from the bottom of the screen while the previous page slides back slightly.

See also:

- [FadeUpwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android O.
- [ZoomPageTransitionsBuilder], which defines the default page transition that's similar to the one provided in Android Q.
- [CupertinoPageTransitionsBuilder], which defines a horizontal page transition that matches native iOS page transitions.
- [PredictiveBackPageTransitionsBuilder], which defines a page transition that allows peeking behind the current route on Android.
- [FadeForwardsPageTransitionsBuilder], which defines a page transition that's similar to the one provided by Android U.

### OpenUpwardsPageTransitionsBuilder()

```dart
OpenUpwardsPageTransitionsBuilder()
```

Constructs a page transition animation that matches the transition used on Android P.

### buildTransitions()

```dart
Widget buildTransitions<T>(PageRoute<T>? route, BuildContext? context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```
