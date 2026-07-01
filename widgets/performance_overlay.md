@docImport 'package:flutter/material.dart';

@docImport 'app.dart';

# PerformanceOverlay

```dart
class PerformanceOverlay extends LeafRenderObjectWidget {}
```

Displays performance statistics.

The overlay shows two time series. The first shows how much time was required on this thread to produce each frame. The second shows how much time was required on the raster thread (formerly known as the GPU thread) to produce each frame. Ideally, both these values would be less than the total frame budget for the hardware on which the app is running. For example, if the hardware has a screen that updates at 60 Hz, each thread should ideally spend less than 16ms producing each frame. This ideal condition is indicated by a green vertical line for each thread. Otherwise, the performance overlay shows a red vertical line.

The simplest way to show the performance overlay is to set [MaterialApp.showPerformanceOverlay] or [WidgetsApp.showPerformanceOverlay] to true.

### PerformanceOverlay()

```dart
PerformanceOverlay({dynamic key, int optionsMask = 0})
```

Create a performance overlay that only displays specific statistics. The mask is created by shifting 1 by the index of the specific [PerformanceOverlayOption] to enable.

### PerformanceOverlay.allEnabled()

```dart
PerformanceOverlay.allEnabled({dynamic key})
```

Create a performance overlay that displays all available statistics.

### optionsMask

```dart
int optionsMask
```

The mask is created by shifting 1 by the index of the specific [PerformanceOverlayOption] to enable.

### createRenderObject()

```dart
RenderPerformanceOverlay createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderPerformanceOverlay renderObject)
```
