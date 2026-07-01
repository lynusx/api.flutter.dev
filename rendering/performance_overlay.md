@docImport 'package:flutter/material.dart';

# PerformanceOverlayOption

```dart
enum PerformanceOverlayOption {}
```

The options that control whether the performance overlay displays certain aspects of the compositor.

Display the frame time and FPS of the last frame rendered. This field is updated every frame.

This is the time spent by the rasterizer as it tries to convert the layer tree obtained from the widgets into OpenGL commands and tries to flush them onto the screen. When the total time taken by this step exceeds the frame slice, a frame is lost.

Display the rasterizer frame times as they change over a set period of time in the form of a graph. The y axis of the graph denotes the total time spent by the rasterizer as a fraction of the total frame slice. When the bar turns red, a frame is lost.

Display the frame time and FPS at which the interface can construct a layer tree for the rasterizer (whose behavior is described above) to consume.

This involves all layout, animations, etc. When the total time taken by this step exceeds the frame slice, a frame is lost.

Display the engine frame times as they change over a set period of time in the form of a graph. The y axis of the graph denotes the total time spent by the engine as a fraction of the total frame slice. When the bar turns red, a frame is lost.

# RenderPerformanceOverlay

```dart
class RenderPerformanceOverlay extends RenderBox {}
```

Displays performance statistics.

The overlay shows two time series. The first shows how much time was required on this thread to produce each frame. The second shows how much time was required on the raster thread (formerly known as the GPU thread) to produce each frame. Ideally, both these values would be less than the total frame budget for the hardware on which the app is running. For example, if the hardware has a screen that updates at 60 Hz, each thread should ideally spend less than 16ms producing each frame. This ideal condition is indicated by a green vertical line for each thread. Otherwise, the performance overlay shows a red vertical line.

The simplest way to show the performance overlay is to set [MaterialApp.showPerformanceOverlay] or [WidgetsApp.showPerformanceOverlay] to true.

### RenderPerformanceOverlay()

```dart
RenderPerformanceOverlay({int optionsMask = 0})
```

Creates a performance overlay render object.

### optionsMask

```dart
int get optionsMask
```

The mask is created by shifting 1 by the index of the specific [PerformanceOverlayOption] to enable.

### optionsMask

```dart
set optionsMask(int value)
```

### sizedByParent

```dart
bool get sizedByParent
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```
