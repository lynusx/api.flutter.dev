@docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# TickerCallback

```dart
typedef TickerCallback = void Function(Duration elapsed)
```

传递给 [Ticker] 类构造函数的回调签名。

参数是自该滴答器上次启动时的帧时间戳到当前帧时间戳所经过的时间。

# TickerProvider

```dart
abstract class TickerProvider {}
```

由能够提供 [Ticker] 对象的类所实现的接口。

要获得 [TickerProvider]，可以考虑混入 [TickerProviderStateMixin]（始终有效）或 [SingleTickerProviderStateMixin]（在适用的情况下效率更高），使 [State] 子类实现 [TickerProvider]。随后可将该 [State] 传递给更底层的组件或其他相关对象。这可确保生成的 [Ticker] 仅在该 [State] 的子树按照 [TickerMode] 的定义处于启用状态时才会滴答。

在组件测试中，[WidgetTester] 对象同样也是一个 [TickerProvider]。

任何希望在每次帧触发时收到通知的对象都可以使用滴答器，但最常见的用法是通过 [AnimationController] 间接使用。[AnimationController] 需要一个 [TickerProvider] 来获取其 [Ticker]。

### TickerProvider()

```dart
TickerProvider()
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可在 const 表达式中使用。

### createTicker()

```dart
Ticker createTicker(TickerCallback onTick)
```

使用给定的回调创建一个滴答器。

所提供的滴答器种类取决于滴答器提供者的种类。

# Ticker

```dart
class Ticker {}
```

在启用状态下，每个动画帧调用一次其回调。

要获取滴答器，可考虑使用 [TickerProvider]。

滴答器在创建时最初处于禁用状态。调用 [start] 以启用滴答器。

可以通过将 [muted] 设为 true 来使 [Ticker] 静默。静默期间，时间仍会流逝，[start] 和 [stop] 仍可被调用，但不会调用任何回调。

按照惯例，[start] 和 [stop] 方法由滴答器的使用者（例如 [AnimationController]）调用，而 [muted] 属性则由创建该滴答器的 [TickerProvider] 控制（例如某个使用 [TickerProviderStateMixin] 的 [State]，会在其子树按 [TickerMode] 的定义被禁用时使滴答器静默）。

另请参阅：

- [TickerProvider]，用于获取滴答器。
- [SchedulerBinding.scheduleFrameCallback]，用于驱动滴答器。

### Ticker()

```dart
Ticker(TickerCallback _onTick, {String? debugLabel})
```

创建一个滴答器，在运行期间每帧调用一次所提供的回调。

可以提供一个可选的标签用于调试目的。该标签将出现在 debug 构建的 [toString] 输出中。

### forceFrames

```dart
bool forceFrames
```

如果为 true，此滴答器将使用 [SchedulerBinding.scheduleForcedFrame] 而非 [SchedulerBinding.scheduleFrame] 来请求帧。

这允许进行细粒度的控制，即使在帧通常被禁用的情况下（例如应用处于后台时）也能推进帧。应谨慎使用此功能，因为它可能增加电量消耗。

### muted

```dart
bool get muted
```

此滴答器是否已被静默。

静默期间，滴答器的时钟仍可运行，但不会调用回调。

### muted

```dart
set muted(bool value)
```

设为 true 时，会使滴答器静默，使其不再滴答。如果已经调度了一次滴答，会将其取消调度。但这不会取消调度下一帧。

设为 false 时，会取消滴答器的静默状态，可能会调度一帧以处理下一次滴答。

按照惯例，[muted] 属性由创建 [Ticker] 的对象（通常是 [TickerProvider]）控制，而非监听滴答器滴答事件的对象。

### isTicking

```dart
bool get isTicking
```

此 [Ticker] 是否已调度在下一帧调用其回调。

处于 [muted] 状态的滴答器可以是活动的（参见 [isActive]），但并不在滴答。在这种情况下，滴答器不会调用其回调，[isTicking] 为 false，但时间仍会继续推进。

如果 [SchedulerBinding.lifecycleState] 表明应用程序当前不可见（例如设备屏幕已关闭），此属性将返回 false。

### isActive

```dart
bool get isActive
```

此 [Ticker] 的时间是否正在流逝。调用 [start] 时变为 true，调用 [stop] 时变为 false。

滴答器可以处于活动状态，但实际上并未在滴答（即未调用回调）。要判断滴答器是否实际在滴答，请使用 [isTicking]。

### start()

```dart
TickerFuture start()
```

启动此 [Ticker] 的时钟。如果该滴答器未被 [muted]，此操作还会开始在每个动画帧调用一次滴答器的回调。

返回的 future 会在滴答器 [stop] 滴答后完成。如果滴答器被释放，该 future 将不会完成。可以从返回的 [TickerFuture] 对象中获取一个派生 future，它会在这种情况下通过 [TickerFuture.orCancel] 以错误的形式完成。

调用此方法会将 [isActive] 设为 true。

在滴答器处于活动状态时无法调用此方法。要重新启动滴答器，需先调用 [stop]。

按照惯例，此方法由接收滴答的对象使用（而非创建该滴答器的 [TickerProvider]）。

### describeForError()

```dart
DiagnosticsNode describeForError(String name)
```

添加针对 [Ticker] 的调试表示形式，经过优化以便包含在错误消息中。

### stop()

```dart
void stop({bool canceled = false})
```

停止调用此 [Ticker] 的回调。

如果调用时 `canceled` 参数为 false（默认值），会使 [start] 返回的 future 完成。如果调用时 `canceled` 参数为 true，该 future 不会完成，且从 [TickerFuture.orCancel] 获取的 future（如果有）将以 [TickerCanceled] 错误完成。

调用此方法会将 [isActive] 设为 false。

如果在滴答器处于非活动状态时调用此方法，则不会执行任何操作。

按照惯例，此方法由接收滴答的对象使用（而非创建该滴答器的 [TickerProvider]）。

### scheduled

```dart
bool get scheduled
```

此 [Ticker] 是否已经调度了一个帧回调。

### shouldScheduleTick

```dart
bool get shouldScheduleTick
```

是否应当调度一次滴答。

如果此值为 true，则调用 [scheduleTick] 应当能够成功。

不应调度滴答的原因包括：

- 已经为即将到来的一帧调度了一次滴答。
- 滴答器未处于活动状态（尚未调用 [start]）。
- 滴答器未在滴答，例如因为它处于 [muted] 状态（参见 [isTicking]）。

### scheduleTick()

```dart
void scheduleTick({bool rescheduling = false})
```

为下一帧调度一次滴答。

仅当 [shouldScheduleTick] 为 true 时才应调用此方法。

### unscheduleTick()

```dart
void unscheduleTick()
```

取消由 [scheduleTick] 请求的帧回调（如果有）。

在没有滴答被 [scheduled] 的情况下调用此方法是无害的。

如果在未调度滴答的情况下 [shouldScheduleTick] 将返回 true，则不应调用此方法。

### absorbTicker()

```dart
void absorbTicker(Ticker originalTicker)
```

使此 [Ticker] 接管另一个滴答器的状态，并释放另一个滴答器。

如果一个拥有 [Ticker] 的对象被赋予了新的 [TickerProvider]，但需要保持连续性，此方法会很有用。特别地，如果原始滴答器处于活动状态，此方法会保持原始 [Ticker] 的 [start] 函数所返回的 [TickerFuture] 的一致性（identity）。

调用此方法时，此滴答器必须不处于活动状态。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后，该对象将不再可用。

在 [isActive] 为 true 时调用此方法是合法的，此时会发生以下情况：

- 由 [scheduleTick] 请求的帧回调（如果有）会被取消。
- [start] 返回的 future 不会完成。
- 从 [TickerFuture.orCancel] 获取的 future（如果有）将以 [TickerCanceled] 错误完成。

### debugLabel

```dart
String? debugLabel
```

可以提供一个可选的标签用于调试目的。

该标签将出现在 debug 构建的 [toString] 输出中。

### toString()

```dart
String toString({bool debugIncludeStack = false})
```

# TickerFuture

```dart
class TickerFuture implements Future<void> {}
```

表示一次正在进行的 [Ticker] 序列的对象。

[Ticker.start] 方法返回一个 [TickerFuture]。如果使用 [Ticker.stop] 停止 [Ticker] 时 `canceled` 参数为 false（默认值），则该 [TickerFuture] 会成功完成。

如果 [Ticker] 在未停止的情况下被释放，或者以 `canceled` 设为 true 的方式停止，则此 Future 将永远不会完成。因此，通常不应等待（await）[TickerFuture]，因为如果 [Ticker] 在动画完成之前被取消或静默，等待它们可能会导致无限期挂起。

返回 [TickerFuture] 的方法通常会标记为 `@awaitNotRequired`（或类似的注解），以表明忽略该 Future 是预期的使用方式。需要在完成时做出响应的调用方应使用 [whenComplete]，以便安全地同时处理成功和取消的情况。

此类的工作方式与普通 [Future] 类似，但额外提供了一个属性 [orCancel]，它返回一个派生的 [Future]：如果返回该 [TickerFuture] 的 [Ticker] 是以 `canceled` 设为 true 的方式停止的，或者是在未停止的情况下被释放的，该 Future 将以错误完成。

要在此 future 完成或滴答器被取消时运行回调，请使用 [whenCompleteOrCancel]。

### TickerFuture.complete()

```dart
TickerFuture.complete()
```

创建一个表示已完成的 [Ticker] 序列的 [TickerFuture] 实例。

这对于实现通常依赖 [Ticker]、但有时因动画时长为零而可以跳过滴答器的对象很有用，这类对象仍需要以 [TickerFuture] 的形式表示已完成的动画。

### whenCompleteOrCancel()

```dart
void whenCompleteOrCancel(VoidCallback callback)
```

在此 future 完成时或滴答器被取消时调用 `callback`。

调用此方法会为 [orCancel] future 注册一个异常处理程序，因此即使访问了 [orCancel] 属性，取消滴答器也不会在当前 zone 中导致未捕获的异常。

### orCancel

```dart
Future<void> get orCancel
```

一个 future：当此 future 完成时随之完成，当滴答器被取消时抛出异常。

如果从未访问此属性，则取消滴答器不会抛出任何异常。但一旦访问了此属性，如果对应的滴答器被取消，此获取器返回的 [Future] 将以错误完成，如果该错误未被捕获，则会在当前 zone 中产生一个未捕获的异常。

### asStream()

```dart
Stream<void> asStream()
```

### catchError()

```dart
Future<void> catchError(Function onError, {bool Function(Object)? test})
```

### then()

```dart
Future<R> then<R>(FutureOr<R> Function(void value) onValue, {Function? onError})
```

### timeout()

```dart
Future<void> timeout(Duration timeLimit, {FutureOr<void> Function()? onTimeout})
```

### whenComplete()

```dart
Future<void> whenComplete(dynamic Function() action)
```

### toString()

```dart
String toString()
```

# TickerCanceled

```dart
class TickerCanceled implements Exception {}
```

当滴答器被取消时，[Ticker] 对象在 [TickerFuture.orCancel] future 上抛出的异常。

### TickerCanceled()

```dart
TickerCanceled([Ticker? ticker])
```

创建一个"滴答器已取消"异常。

### ticker

```dart
Ticker? ticker
```

对被取消的 [Ticker] 对象的引用。

如果为 [TickerFuture.orCancel] 创建的 [Future] 是在滴答器被取消之后才创建的，此值可能为 null。

### toString()

```dart
String toString()
```
