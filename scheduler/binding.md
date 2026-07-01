@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/services.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'ticker.dart';

# timeDilation

```dart
double get timeDilation
```

Slows down animations by this factor to help in development.

# timeDilation

```dart
set timeDilation(double value)
```

If the [SchedulerBinding] has been initialized, setting the time dilation automatically calls [SchedulerBinding.resetEpoch] to ensure that time stamps seen by consumers of the scheduler binding are always increasing.

It is safe to set this before initializing the binding.

# FrameCallback

```dart
typedef FrameCallback = void Function(Duration timeStamp)
```

Signature for frame-related callbacks from the scheduler.

The `timeStamp` is the number of milliseconds since the beginning of the scheduler's epoch. Use timeStamp to determine how far to advance animation timelines so that all the animations in the system are synchronized to a common time base.

# TaskCallback

```dart
typedef TaskCallback<T> = FutureOr<T> Function()
```

Signature for [SchedulerBinding.scheduleTask] callbacks.

The type argument `T` is the task's return value. Consider `void` if the task does not return a value.

# SchedulingStrategy

```dart
typedef SchedulingStrategy = bool Function({required int priority, required SchedulerBinding scheduler})
```

Signature for the [SchedulerBinding.schedulingStrategy] callback. Called whenever the system needs to decide whether a task at a given priority needs to be run.

Return true if a task with the given priority should be executed at this time, false otherwise.

See also:

- [defaultSchedulingStrategy], the default [SchedulingStrategy] for [SchedulerBinding.schedulingStrategy].

# SchedulerPhase

```dart
enum SchedulerPhase {}
```

The various phases that a [SchedulerBinding] goes through during [SchedulerBinding.handleBeginFrame].

This is exposed by [SchedulerBinding.schedulerPhase].

The values of this enum are ordered in the same order as the phases occur, so their relative index values can be compared to each other.

See also:

- [WidgetsBinding.drawFrame], which pumps the build and rendering pipeline to generate a frame.

No frame is being processed. Tasks (scheduled by [SchedulerBinding.scheduleTask]), microtasks (scheduled by [scheduleMicrotask]), [Timer] callbacks, event handlers (e.g. from user input), and other callbacks (e.g. from [Future]s, [Stream]s, and the like) may be executing.

The transient callbacks (scheduled by [SchedulerBinding.scheduleFrameCallback]) are currently executing.

Typically, these callbacks handle updating objects to new animation states.

See [SchedulerBinding.handleBeginFrame].

Microtasks scheduled during the processing of transient callbacks are current executing.

This may include, for instance, callbacks from futures resolved during the [transientCallbacks] phase.

The persistent callbacks (scheduled by [SchedulerBinding.addPersistentFrameCallback]) are currently executing.

Typically, this is the build/layout/paint pipeline. See [WidgetsBinding.drawFrame] and [SchedulerBinding.handleDrawFrame].

The post-frame callbacks (scheduled by [SchedulerBinding.addPostFrameCallback]) are currently executing.

Typically, these callbacks handle cleanup and scheduling of work for the next frame.

See [SchedulerBinding.handleDrawFrame].

# PerformanceModeRequestHandle

```dart
class PerformanceModeRequestHandle {}
```

An opaque handle that keeps a request for [DartPerformanceMode] active until disposed.

To create a [PerformanceModeRequestHandle], use [SchedulerBinding.requestPerformanceMode]. The component that makes the request is responsible for disposing the handle.

### dispose()

```dart
void dispose()
```

Call this method to signal to [SchedulerBinding] that a request for a [DartPerformanceMode] is no longer needed.

This method must only be called once per object.

# SchedulerBinding

```dart
mixin SchedulerBinding on BindingBase {}
```

Scheduler for running the following:

- _Transient callbacks_, triggered by the system's [dart:ui.PlatformDispatcher.onBeginFrame] callback, for synchronizing the application's behavior to the system's display. For example, [Ticker]s and [AnimationController]s trigger from these.

- _Persistent callbacks_, triggered by the system's [dart:ui.PlatformDispatcher.onDrawFrame] callback, for updating the system's display after transient callbacks have executed. For example, the rendering layer uses this to drive its rendering pipeline.

- _Post-frame callbacks_, which are run after persistent callbacks, just before returning from the [dart:ui.PlatformDispatcher.onDrawFrame] callback.

- Non-rendering tasks, to be run between frames. These are given a priority and are executed in priority order according to a [schedulingStrategy].

### initInstances()

```dart
void initInstances()
```

### instance

```dart
SchedulerBinding get instance
```

The current [SchedulerBinding], if one has been created.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### addTimingsCallback()

```dart
void addTimingsCallback(TimingsCallback callback)
```

Add a [TimingsCallback] that receives [FrameTiming] sent from the engine.

This API enables applications to monitor their graphics performance. Data from the engine is batched into lists of [FrameTiming] objects which are reported approximately once a second in release mode and approximately once every 100ms in debug and profile builds. The list is sorted in ascending chronological order (earliest frame first). The timing of the first frame is sent immediately without batching.

The data returned can be used to catch missed frames (by seeing if [FrameTiming.buildDuration] or [FrameTiming.rasterDuration] exceed the frame budget, e.g. 16ms at 60Hz), and to catch high latency (by seeing if [FrameTiming.totalSpan] exceeds the frame budget). It is possible for no frames to be missed but for the latency to be more than one frame in the case where the Flutter engine is pipelining the graphics updates, e.g. because the sum of the [FrameTiming.buildDuration] and the [FrameTiming.rasterDuration] together exceed the frame budget. In those cases, animations will be smooth but touch input will feel more sluggish.

Using [addTimingsCallback] is preferred over using [dart:ui.PlatformDispatcher.onReportTimings] directly because the [dart:ui.PlatformDispatcher.onReportTimings] API only allows one callback, which prevents multiple libraries from registering listeners simultaneously, while this API allows multiple callbacks to be registered independently.

This API is implemented in terms of [dart:ui.PlatformDispatcher.onReportTimings]. In release builds, when no libraries have registered with this API, the [dart:ui.PlatformDispatcher.onReportTimings] callback is not set, which disables the performance tracking and reduces the runtime overhead to approximately zero. The performance overhead of the performance tracking when one or more callbacks are registered (i.e. when it is enabled) is very approximately 0.01% CPU usage per second (measured on an iPhone 6s).

In debug and profile builds, the [SchedulerBinding] itself registers a timings callback to update the [Timeline].

If the same callback is added twice, it will be executed twice.

See also:

- [removeTimingsCallback], which can be used to remove a callback added using this method.

### removeTimingsCallback()

```dart
void removeTimingsCallback(TimingsCallback callback)
```

Removes a callback that was earlier added by [addTimingsCallback].

### initServiceExtensions()

```dart
void initServiceExtensions()
```

### lifecycleState

```dart
AppLifecycleState? get lifecycleState
```

Whether the application is visible, and if so, whether it is currently interactive.

This is set by [handleAppLifecycleStateChanged] when the [SystemChannels.lifecycle] notification is dispatched.

The preferred ways to watch for changes to this value are using [WidgetsBindingObserver.didChangeAppLifecycleState], or through an [AppLifecycleListener] object.

### resetInternalState()

```dart
void resetInternalState()
```

Allows the test framework to reset the lifecycle state and framesEnabled back to their initial values.

### handleAppLifecycleStateChanged()

```dart
void handleAppLifecycleStateChanged(AppLifecycleState state)
```

Called when the application lifecycle state changes.

Notifies all the observers using [WidgetsBindingObserver.didChangeAppLifecycleState].

This method exposes notifications from [SystemChannels.lifecycle].

### schedulingStrategy

```dart
SchedulingStrategy schedulingStrategy
```

The strategy to use when deciding whether to run a task or not.

Defaults to [defaultSchedulingStrategy].

### scheduleTask()

```dart
Future<T> scheduleTask<T>(TaskCallback<T> task, Priority priority, {String? debugLabel, Flow? flow})
```

Schedules the given `task` with the given `priority`.

If `task` returns a future, the future returned by [scheduleTask] will complete after the former future has been scheduled to completion. Otherwise, the returned future for [scheduleTask] will complete with the same value returned by `task` after it has been scheduled.

The `debugLabel` and `flow` are used to report the task to the [Timeline], for use when profiling.

## Processing model

Tasks will be executed between frames, in priority order, excluding tasks that are skipped by the current [schedulingStrategy]. Tasks should be short (as in, up to a millisecond), so as to not cause the regular frame callbacks to get delayed.

If an animation is running, including, for instance, a [ProgressIndicator] indicating that there are pending tasks, then tasks with a priority below [Priority.animation] won't run (at least, not with the [defaultSchedulingStrategy]; this can be configured using [schedulingStrategy]).

### unlocked()

```dart
void unlocked()
```

### handleEventLoopCallback()

```dart
bool handleEventLoopCallback()
```

Execute the highest-priority task, if it is of a high enough priority.

Returns false if the scheduler is [locked], or if there are no tasks remaining.

Returns true otherwise, including when no task is executed due to priority being too low.

### transientCallbackCount

```dart
int get transientCallbackCount
```

The current number of transient frame callbacks scheduled.

This is reset to zero just before all the currently scheduled transient callbacks are called, at the start of a frame.

This number is primarily exposed so that tests can verify that there are no unexpected transient callbacks still registered after a test's resources have been gracefully disposed.

### scheduleFrameCallback()

```dart
int scheduleFrameCallback(FrameCallback callback, {bool rescheduling = false, bool scheduleNewFrame = true})
```

Schedules the given transient frame callback.

Adds the given callback to the list of frame callbacks, and ensures that a frame is scheduled if the `scheduleNewFrame` argument is true.

The `scheduleNewFrame` argument dictates whether [scheduleFrame] should be called to ensure a new frame. Defaults to true.

If this is called during the frame's animation phase (when transient frame callbacks are still being invoked), `callback` will be called in the next frame, not in the current frame.

If this is a one-off registration, ignore the `rescheduling` argument.

If this is a callback that will be re-registered each time it fires, then when you re-register the callback, set the `rescheduling` argument to true. This has no effect in release builds, but in debug builds, it ensures that the stack trace that is stored for this callback is the original stack trace for when the callback was _first_ registered, rather than the stack trace for when the callback is re-registered. This makes it easier to track down the original reason that a particular callback was called. If `rescheduling` is true, the call must be in the context of a frame callback.

Callbacks registered with this method can be canceled using [cancelFrameCallbackWithId].

See also:

- [WidgetsBinding.drawFrame], which explains the phases of each frame for those apps that use Flutter widgets (and where transient frame callbacks fit into those phases).

### cancelFrameCallbackWithId()

```dart
void cancelFrameCallbackWithId(int id)
```

Cancels the transient frame callback with the given [id].

Removes the given callback from the list of frame callbacks. If a frame has been requested, this does not also cancel that request.

Transient frame callbacks are those registered using [scheduleFrameCallback].

### debugAssertNoTransientCallbacks()

```dart
bool debugAssertNoTransientCallbacks(String reason)
```

Asserts that there are no registered transient callbacks; if there are, prints their locations and throws an exception.

A transient frame callback is one that was registered with [scheduleFrameCallback].

This is expected to be called at the end of tests (the flutter_test framework does it automatically in normal cases).

Call this method when you expect there to be no transient callbacks registered, in an assert statement with a message that you want printed when a transient callback is registered:

```dart
assert(SchedulerBinding.instance.debugAssertNoTransientCallbacks(
  'A leak of transient callbacks was detected while doing foo.'
));
```

Does nothing if asserts are disabled. Always returns true.

### debugAssertNoPendingPerformanceModeRequests()

```dart
bool debugAssertNoPendingPerformanceModeRequests(String reason)
```

Asserts that there are no pending performance mode requests in debug mode.

Throws a [FlutterError] if there are pending performance mode requests, as this indicates a potential memory leak.

### debugAssertNoTimeDilation()

```dart
bool debugAssertNoTimeDilation(String reason)
```

Asserts that there is no artificial time dilation in debug mode.

Throws a [FlutterError] if there are such dilation, as this will make subsequent tests see dilation and thus flaky.

### debugPrintTransientCallbackRegistrationStack()

```dart
void debugPrintTransientCallbackRegistrationStack()
```

Prints the stack for where the current transient callback was registered.

A transient frame callback is one that was registered with [scheduleFrameCallback].

When called in debug more and in the context of a transient callback, this function prints the stack trace from where the current transient callback was registered (i.e. where it first called [scheduleFrameCallback]).

When called in debug mode in other contexts, it prints a message saying that this function was not called in the context a transient callback.

In release mode, this function does nothing.

To call this function, use the following code:

```dart
SchedulerBinding.debugPrintTransientCallbackRegistrationStack();
```

### addPersistentFrameCallback()

```dart
void addPersistentFrameCallback(FrameCallback callback)
```

Adds a persistent frame callback.

Persistent callbacks are called after transient (non-persistent) frame callbacks.

Does _not_ request a new frame. Conceptually, persistent frame callbacks are observers of "begin frame" events. Since they are executed after the transient frame callbacks they can drive the rendering pipeline.

Persistent frame callbacks cannot be unregistered. Once registered, they are called for every frame for the lifetime of the application.

See also:

- [WidgetsBinding.drawFrame], which explains the phases of each frame for those apps that use Flutter widgets (and where persistent frame callbacks fit into those phases).

### addPostFrameCallback()

```dart
void addPostFrameCallback(FrameCallback callback, {String debugLabel = 'callback'})
```

Schedule a callback for the end of this frame.

The provided callback is run immediately after a frame, just after the persistent frame callbacks (which is when the main rendering pipeline has been flushed).

This method does _not_ request a new frame. If a frame is already in progress and the execution of post-frame callbacks has not yet begun, then the registered callback is executed at the end of the current frame. Otherwise, the registered callback is executed after the next frame (whenever that may be, if ever).

The callbacks are executed in the order in which they have been added.

Post-frame callbacks cannot be unregistered. They are called exactly once.

In debug mode, if [debugTracePostFrameCallbacks] is set to true, then the registered callback will show up in the timeline events chart, which can be viewed in [DevTools](https://docs.flutter.dev/tools/devtools). In that case, the `debugLabel` argument specifies the name of the callback as it will appear in the timeline. In profile and release builds, post-frame are never traced, and the `debugLabel` argument is ignored.

See also:

- [scheduleFrameCallback], which registers a callback for the start of the next frame.
- [WidgetsBinding.drawFrame], which explains the phases of each frame for those apps that use Flutter widgets (and where post frame callbacks fit into those phases).

### endOfFrame

```dart
Future<void> get endOfFrame
```

Returns a Future that completes after the frame completes.

If this is called between frames, a frame is immediately scheduled if necessary. If this is called during a frame, the Future completes after the current frame.

If the device's screen is currently turned off, this may wait a very long time, since frames are not scheduled while the device's screen is turned off.

### hasScheduledFrame

```dart
bool get hasScheduledFrame
```

Whether this scheduler has requested that [handleBeginFrame] be called soon.

### schedulerPhase

```dart
SchedulerPhase get schedulerPhase
```

The phase that the scheduler is currently operating under.

### framesEnabled

```dart
bool get framesEnabled
```

Whether frames are currently being scheduled when [scheduleFrame] is called.

This value depends on the value of the [lifecycleState].

### ensureFrameCallbacksRegistered()

```dart
void ensureFrameCallbacksRegistered()
```

Ensures callbacks for [PlatformDispatcher.onBeginFrame] and [PlatformDispatcher.onDrawFrame] are registered.

### ensureVisualUpdate()

```dart
void ensureVisualUpdate()
```

Schedules a new frame using [scheduleFrame] if this object is not currently producing a frame.

Calling this method ensures that [handleDrawFrame] will eventually be called, unless it's already in progress.

This has no effect if [schedulerPhase] is [SchedulerPhase.transientCallbacks] or [SchedulerPhase.midFrameMicrotasks] (because a frame is already being prepared in that case), or [SchedulerPhase.persistentCallbacks] (because a frame is actively being rendered in that case). It will schedule a frame if the [schedulerPhase] is [SchedulerPhase.idle] (in between frames) or [SchedulerPhase.postFrameCallbacks] (after a frame).

### scheduleFrame()

```dart
void scheduleFrame()
```

If necessary, schedules a new frame by calling [dart:ui.PlatformDispatcher.scheduleFrame].

After this is called, the engine will (eventually) call [handleBeginFrame]. (This call might be delayed, e.g. if the device's screen is turned off it will typically be delayed until the screen is on and the application is visible.) Calling this during a frame forces another frame to be scheduled, even if the current frame has not yet completed.

Scheduled frames are serviced when triggered by a "Vsync" signal provided by the operating system. The "Vsync" signal, or vertical synchronization signal, was historically related to the display refresh, at a time when hardware physically moved a beam of electrons vertically between updates of the display. The operation of contemporary hardware is somewhat more subtle and complicated, but the conceptual "Vsync" refresh signal continue to be used to indicate when applications should update their rendering.

To have a stack trace printed to the console any time this function schedules a frame, set [debugPrintScheduleFrameStacks] to true.

See also:

- [scheduleForcedFrame], which ignores the [lifecycleState] when scheduling a frame.
- [scheduleWarmUpFrame], which ignores the "Vsync" signal entirely and triggers a frame immediately.

### scheduleForcedFrame()

```dart
void scheduleForcedFrame()
```

Schedules a new frame by calling [dart:ui.PlatformDispatcher.scheduleFrame].

After this is called, the engine will call [handleBeginFrame], even if frames would normally not be scheduled by [scheduleFrame] (e.g. even if the device's screen is turned off).

The framework uses this to force a frame to be rendered at the correct size when the phone is rotated, so that a correctly-sized rendering is available when the screen is turned back on.

To have a stack trace printed to the console any time this function schedules a frame, set [debugPrintScheduleFrameStacks] to true.

Prefer using [scheduleFrame] unless it is imperative that a frame be scheduled immediately, since using [scheduleForcedFrame] will cause significantly higher battery usage when the device should be idle.

Consider using [scheduleWarmUpFrame] instead if the goal is to update the rendering as soon as possible (e.g. at application startup).

### scheduleWarmUpFrame()

```dart
void scheduleWarmUpFrame()
```

Schedule a frame to run as soon as possible, rather than waiting for the engine to request a frame in response to a system "Vsync" signal.

This is used during application startup so that the first frame (which is likely to be quite expensive) gets a few extra milliseconds to run.

Locks events dispatching until the scheduled frame has completed.

If a frame has already been scheduled with [scheduleFrame] or [scheduleForcedFrame], this call may delay that frame.

If any scheduled frame has already begun or if another [scheduleWarmUpFrame] was already called, this call will be ignored.

Prefer [scheduleFrame] to update the display in normal operation.

## Design discussion

The Flutter engine prompts the framework to generate frames when it receives a request from the operating system (known for historical reasons as a vsync). However, this may not happen for several milliseconds after the app starts (or after a hot reload). To make use of the time between when the widget tree is first configured and when the engine requests an update, the framework schedules a _warm-up frame_.

A warm-up frame may never actually render (as the engine did not request it and therefore does not have a valid context in which to paint), but it will cause the framework to go through the steps of building, laying out, and painting, which can together take several milliseconds. Thus, when the engine requests a real frame, much of the work will already have been completed, and the framework can generate the frame with minimal additional effort.

Warm-up frames are scheduled by [runApp] on startup, and by [RendererBinding.performReassemble] during a hot reload.

Warm-up frames are also scheduled when the framework is unblocked by a call to [RendererBinding.allowFirstFrame] (corresponding to a call to [RendererBinding.deferFirstFrame] that blocked the rendering).

### resetEpoch()

```dart
void resetEpoch()
```

Prepares the scheduler for a non-monotonic change to how time stamps are calculated.

Callbacks received from the scheduler assume that their time stamps are monotonically increasing. The raw time stamp passed to [handleBeginFrame] is monotonic, but the scheduler might adjust those time stamps to provide [timeDilation]. Without careful handling, these adjusts could cause time to appear to run backwards.

The [resetEpoch] function ensures that the time stamps are monotonic by resetting the base time stamp used for future time stamp adjustments to the current value. For example, if the [timeDilation] decreases, rather than scaling down the [Duration] since the beginning of time, [resetEpoch] will ensure that we only scale down the duration since [resetEpoch] was called.

Setting [timeDilation] calls [resetEpoch] automatically. You don't need to call [resetEpoch] yourself.

Adjusts the given time stamp into the current epoch.

This both offsets the time stamp to account for when the epoch started (both in raw time and in the epoch's own time line) and scales the time stamp to reflect the time dilation in the current epoch.

These mechanisms together combine to ensure that the durations we give during frame callbacks are monotonically increasing.

### currentFrameTimeStamp

```dart
Duration get currentFrameTimeStamp
```

The time stamp for the frame currently being processed.

This is only valid while between the start of [handleBeginFrame] and the end of the corresponding [handleDrawFrame], i.e. while a frame is being produced.

### currentSystemFrameTimeStamp

```dart
Duration get currentSystemFrameTimeStamp
```

The raw time stamp as provided by the engine to [dart:ui.PlatformDispatcher.onBeginFrame] for the frame currently being processed.

Unlike [currentFrameTimeStamp], this time stamp is neither adjusted to offset when the epoch started nor scaled to reflect the [timeDilation] in the current epoch.

On most platforms, this is a more or less arbitrary value, and should generally be ignored. On Fuchsia, this corresponds to the system-provided presentation time, and can be used to ensure that animations running in different processes are synchronized.

### handleBeginFrame()

```dart
void handleBeginFrame(Duration? rawTimeStamp)
```

Called by the engine to prepare the framework to produce a new frame.

This function calls all the transient frame callbacks registered by [scheduleFrameCallback]. It then returns, any scheduled microtasks are run (e.g. handlers for any [Future]s resolved by transient frame callbacks), and [handleDrawFrame] is called to continue the frame.

If the given time stamp is null, the time stamp from the last frame is reused.

To have a banner shown at the start of every frame in debug mode, set [debugPrintBeginFrameBanner] to true. The banner will be printed to the console using [debugPrint] and will contain the frame number (which increments by one for each frame), and the time stamp of the frame. If the given time stamp was null, then the string "warm-up frame" is shown instead of the time stamp. This allows frames eagerly pushed by the framework to be distinguished from those requested by the engine in response to the "Vsync" signal from the operating system.

You can also show a banner at the end of every frame by setting [debugPrintEndFrameBanner] to true. This allows you to distinguish log statements printed during a frame from those printed between frames (e.g. in response to events or timers).

### requestPerformanceMode()

```dart
PerformanceModeRequestHandle? requestPerformanceMode(DartPerformanceMode mode)
```

Request a specific [DartPerformanceMode].

Returns `null` if the request was not successful due to conflicting performance mode requests. Two requests are said to be in conflict if they are not of the same [DartPerformanceMode] type, and an explicit request for a performance mode has been made prior.

Requestor is responsible for calling [PerformanceModeRequestHandle.dispose] when it no longer requires the performance mode.

Remove a request for a specific [DartPerformanceMode].

If all the pending requests have been disposed, the engine will revert to the [DartPerformanceMode.balanced] performance mode.

### debugGetRequestedPerformanceMode()

```dart
DartPerformanceMode? debugGetRequestedPerformanceMode()
```

Returns the current [DartPerformanceMode] requested or `null` if no requests have been made.

This is only supported in debug and profile modes, returns `null` in release mode.

### handleDrawFrame()

```dart
void handleDrawFrame()
```

Called by the engine to produce a new frame.

This method is called immediately after [handleBeginFrame]. It calls all the callbacks registered by [addPersistentFrameCallback], which typically drive the rendering pipeline, and then calls the callbacks registered by [addPostFrameCallback].

See [handleBeginFrame] for a discussion about debugging hooks that may be useful when working with frame callbacks.

# defaultSchedulingStrategy()

```dart
bool defaultSchedulingStrategy({required int priority, required SchedulerBinding scheduler})
```

The default [SchedulingStrategy] for [SchedulerBinding.schedulingStrategy].

If there are any frame callbacks registered, only runs tasks with a [Priority] of [Priority.animation] or higher. Otherwise, runs all tasks.
