@docImport 'value_listenable_builder.dart';

# StreamBuilderBase

```dart
abstract class StreamBuilderBase<T, S> extends StatefulWidget {}
```

基于与指定 [Stream](https://www.yuque.com/thyname/dart.async/stream) 的交互来构建自身的组件的基类。

[StreamBuilderBase](https://www.yuque.com/thyname/flutter.widgets/streambuilderbase) 是有状态的，并维护到目前为止交互的摘要（summary）。摘要的类型以及每次交互时如何更新摘要由子类定义。

摘要的示例包括：

- 整数流的运行平均值；
- 基于地理位置数据流得出的当前方向和速度；
- 显示流中数据点的图表。

通常，摘要是对流接收到的数据项和错误，以及表示流终止或更改的伪事件进行折叠（fold）计算的结果。初始摘要由子类通过重写 [initial] 来指定。收到流数据和错误时对摘要的更新分别通过重写 [afterData] 和 [afterError] 来指定。如有需要，可以通过重写 [afterDone] 在流终止时更新摘要。最后，可以通过重写 [afterDisconnected] 和 [afterConnected] 在流更改时更新摘要。

`T` 是流事件的类型。

`S` 是交互摘要的类型。

另请参阅：

- [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder)，它专门用于仅需要最近一次交互即可构建组件的情况。

### StreamBuilderBase()

```dart
StreamBuilderBase({dynamic key, required Stream<T>? stream})
```

创建一个连接到指定 [stream] 的 [StreamBuilderBase](https://www.yuque.com/thyname/flutter.widgets/streambuilderbase)。

### stream

```dart
Stream<T>? stream
```

此构建器当前连接到的异步计算，可能为 null。更改时，若前一个流不为 null，则使用 [afterDisconnected] 更新当前摘要；若新流不为 null，则随后使用 [afterConnected] 更新。

### initial()

```dart
S initial()
```

返回流交互的初始摘要，通常表示尚未发生任何交互。

子类必须重写此方法，为折叠计算提供初始值。

### afterConnected()

```dart
S afterConnected(S current)
```

返回反映当前已连接到流的更新版本的 [current] 摘要。

默认实现按原样返回 [current]。

### afterData()

```dart
S afterData(S current, T data)
```

返回在数据事件之后更新的 [current] 摘要。

子类必须重写此方法，以指定在折叠计算中如何将当前摘要与新数据项组合。

### afterError()

```dart
S afterError(S current, Object error, StackTrace stackTrace)
```

返回在发生带堆栈跟踪的错误之后更新的 [current] 摘要。

默认实现按原样返回 [current]。

### afterDone()

```dart
S afterDone(S current)
```

返回在流终止之后更新的 [current] 摘要。

默认实现按原样返回 [current]。

### afterDisconnected()

```dart
S afterDisconnected(S current)
```

返回反映当前不再连接到流的更新版本的 [current] 摘要。

默认实现按原样返回 [current]。

### build()

```dart
Widget build(BuildContext context, S currentSummary)
```

基于 [currentSummary] 返回一个 Widget。

### createState()

```dart
State<StreamBuilderBase<T, S>> createState()
```

# ConnectionState

```dart
enum ConnectionState {}
```

与异步计算的连接状态。

通常的状态流转如下：

1.  [none]，可能带有一些初始数据。
2.  [waiting]，表示异步操作已经开始，数据通常为 null。
3.  [active]，数据非空，且可能随时间变化。
4.  [done]，数据非空。

另请参阅：

- [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot)，它用从异步计算接收到的信息来扩充连接状态。

当前未连接到任何异步计算。

例如，[FutureBuilder.future] 为 null 的 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder)。

已连接到异步计算，正在等待交互。

已连接到活跃的异步计算。

例如，已返回至少一个值但尚未完成的 [Stream](https://www.yuque.com/thyname/dart.async/stream)。

已连接到已终止的异步计算。

# AsyncSnapshot

```dart
class AsyncSnapshot<T> {}
```

与异步计算的最近一次交互的不可变表示。

另请参阅：

- [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder)，它基于与 [Stream](https://www.yuque.com/thyname/dart.async/stream) 交互产生的快照来构建自身。
- [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder)，它基于与 [Future](https://www.yuque.com/thyname/dart.async/future) 交互产生的快照来构建自身。

### AsyncSnapshot.nothing()

```dart
AsyncSnapshot.nothing()
```

创建一个处于 [ConnectionState.none] 状态、数据和错误均为 null 的 [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot)。

### AsyncSnapshot.waiting()

```dart
AsyncSnapshot.waiting()
```

创建一个处于 [ConnectionState.waiting] 状态、数据和错误均为 null 的 [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot)。

### AsyncSnapshot.withData()

```dart
AsyncSnapshot.withData(ConnectionState state, T data)
```

创建一个处于指定 [state] 状态、且具有指定 [data] 的 [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot)。

### AsyncSnapshot.withError()

```dart
AsyncSnapshot.withError(ConnectionState state, Object error, [StackTrace stackTrace = StackTrace.empty])
```

创建一个处于指定 [state] 状态、且具有指定 [error] 和 [stackTrace] 的 [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot)。

若未显式指定 [stackTrace]，则会改用 [StackTrace.empty]。

### connectionState

```dart
ConnectionState connectionState
```

与异步计算的当前连接状态。

### data

```dart
T? data
```

异步计算接收到的最新数据。

若此值非 null，则 [hasData] 为 true。

若 [error] 不为 null，则此值为 null。参见 [hasError]。

若异步计算从未返回过值，此值可能被设置为相关组件指定的初始数据值。参见 [FutureBuilder.initialData] 和 [StreamBuilder.initialData]。

### requireData

```dart
T get requireData
```

返回接收到的最新数据；若没有数据则失败。

若 [hasError]，则抛出 [error]。若 [hasData] 和 [hasError] 均为 false，则抛出 [StateError](https://www.yuque.com/thyname/dart.core/stateerror)。

### error

```dart
Object? error
```

异步计算接收到的最新错误对象。

若此值非 null，则 [hasError] 为 true。

若 [data] 不为 null，则此值为 null。

### stackTrace

```dart
StackTrace? stackTrace
```

异步计算接收到的最新堆栈跟踪对象。

当且仅当 [error] 不为 null 时，此值才不为 null。因此，当 [hasError] 为 true 时，[stackTrace] 也不为 null。

但是，即使不为 null，[stackTrace] 也可能为空。当存在错误但未提供堆栈跟踪时，堆栈跟踪即为空。

### inState()

```dart
AsyncSnapshot<T> inState(ConnectionState state)
```

返回一个与当前快照类似、但处于指定 [state] 状态的快照。

[data]、[error] 和 [stackTrace] 字段保持不变，即使新状态为 [ConnectionState.none]。

### hasData

```dart
bool get hasData
```

返回此快照是否包含非 null 的 [data] 值。

即使异步计算已成功完成，此值也可能为 false，前提是该计算未返回非 null 的值。例如，[Future<void>] 即便成功完成，也会以 null 值结束。

### hasError

```dart
bool get hasError
```

返回此快照是否包含非 null 的 [error] 值。

若异步计算的最后一次结果为失败，则此值始终为 true。

# AsyncWidgetBuilder

```dart
typedef AsyncWidgetBuilder<T> = Widget Function(BuildContext context, AsyncSnapshot<T> snapshot)
```

基于异步交互构建组件的策略的函数签名。

另请参阅：

- [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder)，它委托给一个 [AsyncWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/asyncwidgetbuilder)，基于与 [Stream](https://www.yuque.com/thyname/dart.async/stream) 交互产生的快照来构建自身。
- [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder)，它委托给一个 [AsyncWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/asyncwidgetbuilder)，基于与 [Future](https://www.yuque.com/thyname/dart.async/future) 交互产生的快照来构建自身。

# StreamBuilder

```dart
class StreamBuilder<T> extends StreamBuilderBase<T, AsyncSnapshot<T>> {}
```

基于与 [Stream](https://www.yuque.com/thyname/dart.async/stream) 交互的最新快照来构建自身的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=MkKEWHfy99Y}

## 管理流

[stream] 必须提前获取，例如在 [State.initState]、[State.didUpdateWidget] 或 [State.didChangeDependencies] 期间获取。在构造 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder) 时，不得在 [State.build] 或 [StatelessWidget.build] 方法调用期间创建它。若 [stream] 与 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder) 同时创建，则每次 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder) 的父组件重建时，异步任务都会重新启动。

一般性的准则是：假定每个 `build` 方法都可能在每一帧被调用，并将未调用的情况视为一种优化。

## 时序

组件重建由每次交互通过 [State.setState] 调度，但在其他方面与流的时序解耦。[builder] 由 Flutter 管线自行决定调用时机，因此它接收到的是代表与流交互的快照的一个与时序相关的子序列。

例如，当与一个产生整数 0 到 9 的流交互时，[builder] 可能会以下列快照的任意有序子序列被调用，只要该子序列包含最后一个快照（即 ConnectionState.done 的快照）：

- `AsyncSnapshot<int>.withData(ConnectionState.waiting, null)`
- `AsyncSnapshot<int>.withData(ConnectionState.active, 0)`
- `AsyncSnapshot<int>.withData(ConnectionState.active, 1)`
- ...
- `AsyncSnapshot<int>.withData(ConnectionState.active, 9)`
- `AsyncSnapshot<int>.withData(ConnectionState.done, 9)`

[builder] 实际的调用顺序取决于流产生事件的相对时序与 Flutter 管线构建速率之间的关系。

在事件产生期间将 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder) 的配置更改为另一个流，会引入如下形式的快照对：

- `AsyncSnapshot<int>.withData(ConnectionState.none, 5)`
- `AsyncSnapshot<int>.withData(ConnectionState.waiting, 5)`

后者仅在新流非 null 时产生，前者仅在旧流非 null 时产生。

流可能产生错误，从而生成如下形式的快照：

- `AsyncSnapshot<int>.withError(ConnectionState.active, 'some error', someStackTrace)`

仅当状态为 `ConnectionState.active` 时，所产生快照的数据和错误字段才会发生变化。

可以通过指定 [initialData] 来控制初始快照数据。应使用它来确保第一帧具有预期的值，因为在流监听器有机会被处理之前，构建器总会先被调用。

{@tool dartpad} 此示例展示了一个监听拍卖出价流的 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder)。每当 StreamBuilder 从 Stream 接收到一次出价时，它会在图标下方显示出价的价格。若 Stream 发出错误，则会在错误图标下方显示错误信息。当 Stream 结束出价发送时，会显示最终价格。

** 请参阅 examples/api/lib/widgets/async/stream_builder.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [ValueListenableBuilder](https://www.yuque.com/thyname/flutter.widgets/valuelistenablebuilder)，它包装的是 [ValueListenable](https://www.yuque.com/thyname/flutter.foundation/valuelistenable) 而非 [Stream](https://www.yuque.com/thyname/dart.async/stream)。
- [StreamBuilderBase](https://www.yuque.com/thyname/flutter.widgets/streambuilderbase)，它支持基于跨越与流的所有交互的计算来构建组件。

### StreamBuilder()

```dart
StreamBuilder({dynamic key, T? initialData, required Stream<T>? stream, required AsyncWidgetBuilder<T> builder})
```

创建一个新的 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder)，它基于与指定 [stream] 交互的最新快照来构建自身，其构建策略由 [builder] 给出。

[initialData] 用于创建初始快照。

### builder

```dart
AsyncWidgetBuilder<T> builder
```

此构建器当前使用的构建策略。

此构建器只能返回一个组件，且不应产生任何副作用，因为它可能会被多次调用。

### initialData

```dart
T? initialData
```

用于创建初始快照的数据。

提供此值（大概是在创建 [Stream](https://www.yuque.com/thyname/dart.async/stream) 时以某种同步方式获得的）可确保第一帧显示有用的数据。否则，无论流上是否有可用的值，第一帧都将以 null 值进行构建：由于流是异步的，在初始构建之前无法从流中获取任何事件。

# FutureBuilder

```dart
class FutureBuilder<T> extends StatefulWidget {}
```

基于与 [Future](https://www.yuque.com/thyname/dart.async/future) 交互的最新快照来构建自身的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=zEdw_1B7JHY}

## 管理 future

[future] 必须提前获取，例如在 [State.initState]、[State.didUpdateWidget] 或 [State.didChangeDependencies] 期间获取。在构造 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder) 时，不得在 [State.build] 或 [StatelessWidget.build] 方法调用期间创建它。若 [future] 与 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder) 同时创建，则每次 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder) 的父组件重建时，异步任务都会重新启动。

一般性的准则是：假定每个 `build` 方法都可能在每一帧被调用，并将未调用的情况视为一种优化。

## 时序

组件重建由 future 的完成通过 [State.setState] 调度，但在其他方面与 future 的时序解耦。[builder] 回调由 Flutter 管线自行决定调用时机，因此它接收到的是代表与 future 交互的快照的一个与时序相关的子序列。

这样做的一个副作用是：向 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder) 提供一个新的但已经完成的 future，会导致产生处于 [ConnectionState.waiting] 状态的一帧。这是因为无法以同步方式判断 [Future](https://www.yuque.com/thyname/dart.async/future) 是否已经完成。

## 构建器契约

对于成功完成并带有数据的 future，假设 [initialData] 为 null，[builder] 会以下列两个快照中的两者，或仅以后者被调用：

- `AsyncSnapshot<String>.withData(ConnectionState.waiting, null)`
- `AsyncSnapshot<String>.withData(ConnectionState.done, 'some data')`

若同一 future 改为以错误结束，则 [builder] 会以下列两者，或仅以后者被调用：

- `AsyncSnapshot<String>.withData(ConnectionState.waiting, null)`
- `AsyncSnapshot<String>.withError(ConnectionState.done, 'some error', someStackTrace)`

可以通过指定 [initialData] 来控制初始快照数据。可以利用这一机制来确保：若 [builder] 在 future 完成之前被调用，快照携带的是你所选择的数据，而非默认的 null 值。

快照的数据和错误字段仅在连接状态字段从 `waiting` 转变为 `done` 时才会改变，并且在将 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder) 的配置更改为另一个 future 时会被保留。若旧 future 已经如上所述成功完成并带有数据，则将配置更改为新 future 会产生如下形式的快照对：

- `AsyncSnapshot<String>.withData(ConnectionState.none, 'data of first future')`
- `AsyncSnapshot<String>.withData(ConnectionState.waiting, 'data of second future')`

通常，后者仅在新 future 非 null 时产生，前者仅在旧 future 非 null 时产生。

[FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder) 的行为与配置了 `future?.asStream()` 的 [StreamBuilder](https://www.yuque.com/thyname/flutter.widgets/streambuilder) 完全相同，只是后者可能会出现 `ConnectionState.active` 状态的快照，这取决于该流的具体实现。

{@tool dartpad} 此示例展示了一个在加载数据时显示加载指示器的 [FutureBuilder](https://www.yuque.com/thyname/flutter.widgets/futurebuilder)。若 [Future](https://www.yuque.com/thyname/dart.async/future) 以结果完成，则显示成功图标和文本；若 [Future](https://www.yuque.com/thyname/dart.async/future) 以错误完成，则显示错误图标和文本。假定 `_calculation` 字段是通过按下界面其他位置的按钮来设置的。

** 请参阅 examples/api/lib/widgets/async/future_builder.0.dart 中的代码 ** {@end-tool}

### FutureBuilder()

```dart
FutureBuilder({dynamic key, required Future<T>? future, T? initialData, required AsyncWidgetBuilder<T> builder})
```

创建一个基于与 [Future](https://www.yuque.com/thyname/dart.async/future) 交互的最新快照来构建自身的组件。

### future

```dart
Future<T>? future
```

此构建器当前连接到的异步计算，可能为 null。

若尚无 future 完成（包括 [future] 为 null 的情况），则提供给 [builder] 的数据将被设置为 [initialData]。

### builder

```dart
AsyncWidgetBuilder<T> builder
```

此构建器当前使用的构建策略。

构建器会得到一个 [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot) 对象，其 [AsyncSnapshot.connectionState] 属性将是以下值之一：

- [ConnectionState.none]：[future] 为 null。[AsyncSnapshot.data] 将被设置为 [initialData]，除非之前已有 future 完成过，在这种情况下之前的结果会被保留。

- [ConnectionState.waiting]：[future] 不为 null，但尚未完成。[AsyncSnapshot.data] 将被设置为 [initialData]，除非之前已有 future 完成过，在这种情况下之前的结果会被保留。

- [ConnectionState.done]：[future] 不为 null，且已完成。若该 future 成功完成，[AsyncSnapshot.data] 将被设置为该 future 所完成的值。若它以错误结束，则 [AsyncSnapshot.hasError] 将为 true，且 [AsyncSnapshot.error] 将被设置为该错误对象。

此构建器只能返回一个组件，且不应产生任何副作用，因为它可能会被多次调用。

### initialData

```dart
T? initialData
```

用于创建快照的数据，在非 null 的 [future] 完成之前，快照都会使用此数据。

若该 future 以错误结束，则无论 [initialData] 为何，提供给 [builder] 的 [AsyncSnapshot](https://www.yuque.com/thyname/flutter.widgets/asyncsnapshot) 中的数据都将变为 null。（错误本身可通过 [AsyncSnapshot.error] 获取，且 [AsyncSnapshot.hasError] 将为 true。）

### debugRethrowError

```dart
bool debugRethrowError
```

异步计算接收到的最新错误是应重新抛出还是被吞掉。此属性用于调试目的。

设置为 true 时，仅在调试模式下才会重新抛出最新的错误。

默认为 `false`，即吞掉错误。
