@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter_test/flutter_test.dart';

@docImport 'actions.dart'; @docImport 'focus_manager.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'scrollable_helpers.dart'; @docImport 'shortcuts.dart';

# PrimaryScrollController

```dart
class PrimaryScrollController extends InheritedWidget {}
```

Associates a [ScrollController] with a subtree.

{@youtube 560 315 https://www.youtube.com/watch?v=33_0ABjFJUU}

When a [ScrollView] has [ScrollView.primary] set to true, the [ScrollView] uses [of] to inherit the [PrimaryScrollController] associated with its subtree.

A ScrollView that doesn't have a controller or the primary flag set will inherit the PrimaryScrollController, if [shouldInherit] allows it. By default [shouldInherit] is true for mobile platforms when the ScrollView has a scroll direction of [Axis.vertical]. This automatic inheritance can be configured with [automaticallyInheritForPlatforms] and [scrollDirection].

Inheriting this ScrollController can provide default behavior for scroll views in a subtree. For example, the [Scaffold] uses this mechanism to implement the scroll-to-top gesture on iOS.

Another default behavior handled by the PrimaryScrollController is default [ScrollAction]s. If a ScrollAction is not handled by an otherwise focused part of the application, the ScrollAction will be evaluated using the scroll view associated with a PrimaryScrollController, for example, when executing [Shortcuts] key events like page up and down.

See also:

- [ScrollAction], an [Action] that scrolls the [Scrollable] that encloses the current [primaryFocus] or is attached to the PrimaryScrollController.
- [Shortcuts], a widget that establishes a [ShortcutManager] to be used by its descendants when invoking an [Action] via a keyboard key combination that maps to an [Intent].

### PrimaryScrollController()

```dart
PrimaryScrollController({dynamic key, required ScrollController? controller, Set<TargetPlatform> automaticallyInheritForPlatforms = _kMobilePlatforms, Axis? scrollDirection = Axis.vertical, required Widget child})
```

Creates a widget that associates a [ScrollController] with a subtree.

### PrimaryScrollController.none()

```dart
PrimaryScrollController.none({dynamic key, required Widget child})
```

Creates a subtree without an associated [ScrollController].

### controller

```dart
ScrollController? controller
```

The [ScrollController] associated with the subtree.

See also:

- [ScrollView.controller], which discusses the purpose of specifying a scroll controller.

### scrollDirection

```dart
Axis? scrollDirection
```

The [Axis] this controller is configured for [ScrollView]s to automatically inherit.

Used in conjunction with [automaticallyInheritForPlatforms]. If the current [TargetPlatform] is not included in [automaticallyInheritForPlatforms], this is ignored.

When null, no [ScrollView] in any Axis will automatically inherit this controller. This is dissimilar to [PrimaryScrollController.none]. When a PrimaryScrollController is inherited, ScrollView will insert PrimaryScrollController.none into the tree to prevent further descendant ScrollViews from inheriting the current PrimaryScrollController.

For the direction in which active scrolling may be occurring, see [ScrollDirection].

Defaults to [Axis.vertical].

### automaticallyInheritForPlatforms

```dart
Set<TargetPlatform> automaticallyInheritForPlatforms
```

The [TargetPlatform]s this controller is configured for [ScrollView]s to automatically inherit.

Used in conjunction with [scrollDirection]. If the [Axis] provided to [shouldInherit] is not [scrollDirection], this is ignored.

When empty, no ScrollView in any Axis will automatically inherit this controller. Defaults to [TargetPlatformVariant.mobile].

### shouldInherit()

```dart
bool shouldInherit(BuildContext context, Axis scrollDirection)
```

Returns true if this PrimaryScrollController is configured to be automatically inherited for the current [TargetPlatform] and the given [Axis].

This method is typically not called directly. [ScrollView] will call this method if it has not been provided a [ScrollController] and [ScrollView.primary] is unset.

If a ScrollController has already been provided to [ScrollView.controller], or [ScrollView.primary] is set, this is method is not called by ScrollView as it will have determined whether or not to inherit the PrimaryScrollController.

### maybeOf()

```dart
ScrollController? maybeOf(BuildContext context)
```

Returns the [ScrollController] most closely associated with the given context.

Returns null if there is no [ScrollController] associated with the given context.

Calling this method will create a dependency on the closest [PrimaryScrollController] in the [context], if there is one.

See also:

- [PrimaryScrollController.maybeOf], which is similar to this method, but asserts if no [PrimaryScrollController] ancestor is found.

### of()

```dart
ScrollController of(BuildContext context)
```

Returns the [ScrollController] most closely associated with the given context.

If no ancestor is found, this method will assert in debug mode, and throw an exception in release mode.

Calling this method will create a dependency on the closest [PrimaryScrollController] in the [context].

See also:

- [PrimaryScrollController.maybeOf], which is similar to this method, but returns null if no [PrimaryScrollController] ancestor is found.

### updateShouldNotify()

```dart
bool updateShouldNotify(PrimaryScrollController oldWidget)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
