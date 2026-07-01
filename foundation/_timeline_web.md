# performanceTimestamp

```dart
double get performanceTimestamp
```

Returns the current timestamp in microseconds from a monotonically increasing clock.

This is the web implementation, which uses `window.performance.now` as the source of the timestamp.

See:

- https://developer.mozilla.org/en-US/docs/Web/API/Performance/now
