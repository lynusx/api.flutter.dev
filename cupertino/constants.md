@docImport 'package:flutter/material.dart';

@docImport 'checkbox.dart'; @docImport 'radio.dart'; @docImport 'switch.dart'; @docImport 'text_theme.dart';

# kMinInteractiveDimensionCupertino

```dart
double kMinInteractiveDimensionCupertino
```

The minimum dimension of any interactive region according to the iOS Human Interface Guidelines.

This is used to avoid small regions that are hard for the user to interact with. It applies to both dimensions of a region, so a square of size kMinInteractiveDimension x kMinInteractiveDimension is the smallest acceptable region that should respond to gestures.

See also:

- [kMinInteractiveDimension]
- <https://developer.apple.com/ios/human-interface-guidelines/visual-design/adaptivity-and-layout/>

# kCupertinoFocusColorOpacity

```dart
double kCupertinoFocusColorOpacity
```

The relative values needed to transform a color to it's equivalent focus outline color.

These are used to draw a focus ring around [CupertinoSwitch], [CupertinoCheckbox], [CupertinoRadio] and [CupertinoButton].

See also:

- <https://developer.apple.com/design/human-interface-guidelines/focus-and-selection/>

# kCupertinoButtonTintedOpacityLight

```dart
double kCupertinoButtonTintedOpacityLight
```

Opacity values for the background of a [CupertinoButton.tinted].

See also:

- <https://developer.apple.com/design/human-interface-guidelines/buttons#iOS-iPadOS>

# kCupertinoButtonDefaultIconSize

```dart
double kCupertinoButtonDefaultIconSize
```

The default value for [IconThemeData.size] of [CupertinoButton.child].

Set to match the most-frequent size of icons in iOS (matches md/lg).

Used only when the [CupertinoTextThemeData.actionTextStyle] or [CupertinoTextThemeData.actionSmallTextStyle] has a null [TextStyle.fontSize].

# kCupertinoButtonPadding

```dart
Map<CupertinoButtonSize, EdgeInsetsGeometry> kCupertinoButtonPadding
```

The padding values for the different [CupertinoButtonSize]s.

Based on the iOS (17) [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/buttons#iOS-iPadOS).

# kCupertinoButtonSizeBorderRadius

```dart
Map<CupertinoButtonSize, BorderRadius> kCupertinoButtonSizeBorderRadius
```

The border radius values for the different [CupertinoButtonSize]s.

Based on the iOS (17) [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/buttons#iOS-iPadOS).

# kCupertinoButtonMinSize

```dart
Map<CupertinoButtonSize, double> kCupertinoButtonMinSize
```

The minimum size of a [CupertinoButton] based on the [CupertinoButtonSize].

Based on the iOS (17) [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/buttons#iOS-iPadOS).

# kCupertinoButtonTapMoveSlop

```dart
double kCupertinoButtonTapMoveSlop
```

The distance a button needs to be moved after being pressed for its opacity to change.

The opacity changes when the position moved is this distance away from the button. This variable is effective on mobile platforms. For desktop platforms, a distance of 0 is used.

This value was obtained through actual testing on an iOS 18.1 simulator.
