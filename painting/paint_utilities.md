# paintZigZag()

```dart
void paintZigZag(Canvas canvas, Paint paint, Offset start, Offset end, int zigs, double width)
```

Draw a line between two points, which cuts diagonally back and forth across the line that connects the two points.

The line will cross the line `zigs - 1` times.

If `zigs` is 1, then this will draw two sides of a triangle from `start` to `end`, with the third point being `width` away from the line, as measured perpendicular to that line.

If `width` is positive, the first `zig` will be to the left of the `start` point when facing the `end` point. To reverse the zigging polarity, provide a negative `width`.

The line is drawn using the provided `paint` on the provided `canvas`.
