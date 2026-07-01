@docImport 'package:flutter/rendering.dart';

# ClipContext

```dart
abstract class ClipContext {}
```

Clip utilities used by [PaintingContext].

### canvas

```dart
Canvas get canvas
```

The canvas on which to paint.

### clipPathAndPaint()

```dart
void clipPathAndPaint(Path path, Clip clipBehavior, Rect bounds, VoidCallback painter)
```

Clip [canvas] with [Path] according to [Clip] and then paint. [canvas] is restored to the pre-clip status afterwards.

`bounds` is the saveLayer bounds used for [Clip.antiAliasWithSaveLayer].

### clipRRectAndPaint()

```dart
void clipRRectAndPaint(RRect rrect, Clip clipBehavior, Rect bounds, VoidCallback painter)
```

Clip [canvas] with [Path] according to `rrect` and then paint. [canvas] is restored to the pre-clip status afterwards.

`bounds` is the saveLayer bounds used for [Clip.antiAliasWithSaveLayer].

### clipRSuperellipseAndPaint()

```dart
void clipRSuperellipseAndPaint(RSuperellipse rse, Clip clipBehavior, Rect bounds, VoidCallback painter)
```

Clip [canvas] with [Path] according to the given rounded superellipse and then paint. [canvas] is restored to the pre-clip status afterwards.

The `bounds` is the saveLayer bounds used for [Clip.antiAliasWithSaveLayer].

### clipRectAndPaint()

```dart
void clipRectAndPaint(Rect rect, Clip clipBehavior, Rect bounds, VoidCallback painter)
```

Clip [canvas] with [Path] according to `rect` and then paint. [canvas] is restored to the pre-clip status afterwards.

`bounds` is the saveLayer bounds used for [Clip.antiAliasWithSaveLayer].
