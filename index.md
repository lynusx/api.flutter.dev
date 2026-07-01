# Flutter API reference documentation

> Flutter SDK Version：3.44.4

Flutter is Google's SDK for crafting beautiful, fast user experiences for mobile, web, and desktop from a single codebase. Flutter works with existing code, is used by developers and organizations around the world, and is free and open source.

This API reference covers all libraries that are exported by the Flutter SDK.

## More Documentation

This site hosts Flutter's API documentation. Other documentation can be found at the following locations:

- [Install Flutter](https://docs.flutter.dev/get-started)
- [Flutter documentation](https://docs.flutter.dev/)
- [Stable channel API reference documentation](https://api.flutter.dev/)
- [Main channel API reference documentation](https://main-api.flutter.dev/)
- [Contributing to Flutter](https://github.com/flutter/flutter/blob/main/CONTRIBUTING.md)

## Offline Documentation

In addition to the online sites above, Flutter's documentation can be downloaded as an HTML documentation ZIP file for use when offline or when you have a poor internet connection.

Note

The offline documentation files are quite large, approximately 300MB zipped, 1GB unzipped.

Offline HTML documentation ZIP bundles:

- [Stable channel](https://api.flutter.dev/offline/flutter.docs.zip)
- [Main channel](https://main-api.flutter.dev/offline/flutter.docs.zip)

Or, you can add Flutter to the open-source [Zeal](https://zealdocs.org/) app using the following XML configurations. Follow the instructions in the application for adding a feed.

- Stable channel Zeal XML configuration URL: [api.flutter.dev/offline/flutter.xml](https://api.flutter.dev/offline/flutter.xml)
- Main channel Zeal XML configuration URL: [main-api.flutter.dev/offline/flutter.xml](https://main-api.flutter.dev/offline/flutter.xml)

## Importing a Library

### Framework Libraries

Libraries in the "Libraries" section below (or in the left navigation) are part of the core Flutter framework and are imported using `'package:flutter/<library>.dart'`, like so:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
```

### Dart Libraries

Libraries in the "Dart" section exist in the `dart:` namespace and are imported using `'dart:<library>'`, like so:

```dart
import 'dart:async';
import 'dart:ui';
```

Except for `'dart:core'`, you must import a Dart library before you can use it.

### Supporting Libraries

Libraries in other sections are supporting libraries that ship with Flutter. They are organized by package and are imported using `'package:<package>/<library>.dart'`, like so:

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:file/local.dart';
```

## Packages on pub.dev

Flutter has a rich ecosystem of packages that have been contributed by the Flutter team and the broader open source community to a central repository. Among the thousands of packages, you'll find support for Firebase, Google Fonts, hardware services like Bluetooth and camera, new widgets and animations, and integration with other popular web services. You can browse those packages at [pub.dev](https://pub.dev/).

## Libraries

- [animation](https://api.flutter.dev/flutter/animation/)

  The Flutter animation system.

- [cupertino](https://api.flutter.dev/flutter/cupertino/)

  Flutter widgets implementing the current iOS design language.

- [foundation](https://api.flutter.dev/flutter/foundation/)

  Core Flutter framework primitives.

- [gestures](https://api.flutter.dev/flutter/gestures/)

  The Flutter gesture recognizers.

- [material](https://api.flutter.dev/flutter/material/)

  Flutter widgets implementing Material Design.

- [painting](https://api.flutter.dev/flutter/painting/)

  The Flutter painting library.

- [physics](https://api.flutter.dev/flutter/physics/)

  Simple one-dimensional physics simulations, such as springs, friction, and gravity, for use in user interface animations.

- [rendering](https://api.flutter.dev/flutter/rendering/)

  The Flutter rendering tree.

- [scheduler](https://api.flutter.dev/flutter/scheduler/)

  The Flutter Scheduler library.

- [semantics](https://api.flutter.dev/flutter/semantics/)

  The Flutter semantics package.

- [services](https://api.flutter.dev/flutter/services/)

  Platform services exposed to Flutter apps.

- [widget_previews](https://api.flutter.dev/flutter/widget_previews/)

  The Flutter widget preview annotations and data classes.

- [widgets](https://api.flutter.dev/flutter/widgets/)

  The Flutter widgets framework.

## Dart

- [dart:ui](https://api.flutter.dev/flutter/dart-ui/)

  Built-in types and core primitives for a Flutter application.
