# FlutterTimeline

```dart
abstract final class FlutterTimeline {}
```

Measures how long blocks of code take to run.

This class can be used as a drop-in replacement for [Timeline] as it provides methods compatible with [Timeline] signature-wise, and it has minimal overhead.

Provides [debugReset] and [debugCollect] methods that make it convenient to use in frame-oriented environment where collected metrics can be attributed to a frame, then aggregated into frame statistics, e.g. frame averages.

Forwards measurements to [Timeline] so they appear in Flutter DevTools.

### debugCollectionEnabled

```dart
bool get debugCollectionEnabled
```

Whether block timings are collected and can be retrieved using the [debugCollect] method.

This is always false in release mode.

### debugCollectionEnabled

```dart
set debugCollectionEnabled(bool value)
```

Enables metric collection.

Metric collection can only be enabled in non-release modes. It is most useful in profile mode where application performance is representative of a deployed application.

When disabled, resets collected data by calling [debugReset].

Throws a [StateError] if invoked in release mode.

### startSync()

```dart
void startSync(String name, {Map<String, Object?>? arguments, Flow? flow})
```

Start a synchronous operation labeled `name`.

Optionally takes a map of `arguments`. This slice may also optionally be associated with a [Flow] event. This operation must be finished by calling [finishSync] before returning to the event queue.

This is a drop-in replacement for [Timeline.startSync].

### finishSync()

```dart
void finishSync()
```

Finish the last synchronous operation that was started.

This is a drop-in replacement for [Timeline.finishSync].

### instantSync()

```dart
void instantSync(String name, {Map<String, Object?>? arguments})
```

Emit an instant event.

This is a drop-in replacement for [Timeline.instantSync].

### timeSync()

```dart
T timeSync<T>(String name, TimelineSyncFunction<T> function, {Map<String, Object?>? arguments, Flow? flow})
```

A utility method to time a synchronous `function`.

Internally calls `function` bracketed by calls to [startSync] and [finishSync].

This is a drop-in replacement for [Timeline.timeSync].

### now

```dart
int get now
```

The current time stamp from the clock used by the timeline in microseconds.

When run on the Dart VM, uses the same monotonic clock as the embedding API's `Dart_TimelineGetMicros`.

When run on the web, uses `window.performance.now`.

This is a drop-in replacement for [Timeline.now].

### debugCollect()

```dart
AggregatedTimings debugCollect()
```

Returns timings collected since [debugCollectionEnabled] was set to true, since the previous [debugCollect], or since the previous [debugReset], whichever was last.

Resets the collected timings.

This is only meant to be used in non-release modes, typically in profile mode that provides timings close to release mode timings.

### debugReset()

```dart
void debugReset()
```

Forgets all previously collected timing data.

Use this method to scope metrics to a frame, a pointer event, or any other event. To do that, call [debugReset] at the start of the event, then call [debugCollect] at the end of the event.

This is only meant to be used in non-release modes.

# TimedBlock

```dart
final class TimedBlock {}
```

Provides [start], [end], and [duration] of a named block of code, timed by [FlutterTimeline].

### TimedBlock()

```dart
TimedBlock({required String name, required double start, required double end})
```

Creates a timed block of code from a [name], [start], and [end].

The [name] should be sufficiently unique and descriptive for someone to easily tell which part of code was measured.

### name

```dart
String name
```

A readable label for a block of code that was measured.

This field should be sufficiently unique and descriptive for someone to easily tell which part of code was measured.

### start

```dart
double start
```

The timestamp in microseconds that marks the beginning of the measured block of code.

### end

```dart
double end
```

The timestamp in microseconds that marks the end of the measured block of code.

### duration

```dart
double get duration
```

How long the measured block of code took to execute in microseconds.

### toString()

```dart
String toString()
```

# AggregatedTimings

```dart
final class AggregatedTimings {}
```

Provides aggregated results for timings collected by [FlutterTimeline].

### AggregatedTimings()

```dart
AggregatedTimings(List<TimedBlock> timedBlocks)
```

Creates aggregated timings for the provided timed blocks.

### timedBlocks

```dart
List<TimedBlock> timedBlocks
```

All timed blocks collected between the last reset and [FlutterTimeline.debugCollect].

### aggregatedBlocks

```dart
List<AggregatedTimedBlock> aggregatedBlocks
```

Aggregated timed blocks collected between the last reset and [FlutterTimeline.debugCollect].

Does not guarantee that all code blocks will be reported. Only those that executed since the last reset are listed here. Use [getAggregated] for graceful handling of missing code blocks.

### getAggregated()

```dart
AggregatedTimedBlock getAggregated(String name)
```

Returns aggregated numbers for a named block of code.

If the block in question never executed since the last reset, returns an aggregation with zero duration and count.

# AggregatedTimedBlock

```dart
final class AggregatedTimedBlock {}
```

Aggregates multiple [TimedBlock] objects that share a [name].

It is common for the same block of code to be executed multiple times within a frame. It is useful to combine multiple executions and report the total amount of time attributed to that block of code.

### AggregatedTimedBlock()

```dart
AggregatedTimedBlock({required String name, required double duration, required int count})
```

Creates a timed block of code from a [name] and [duration].

The [name] should be sufficiently unique and descriptive for someone to easily tell which part of code was measured.

### name

```dart
String name
```

A readable label for a block of code that was measured.

This field should be sufficiently unique and descriptive for someone to easily tell which part of code was measured.

### duration

```dart
double duration
```

The sum of [TimedBlock.duration] values of aggregated blocks.

### count

```dart
int count
```

The number of [TimedBlock] objects aggregated.

### toString()

```dart
String toString()
```
