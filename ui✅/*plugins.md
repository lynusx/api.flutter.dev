# CallbackHandle

```dart
class CallbackHandle {}
```

原始回调句柄的封装类。

这是 [PluginUtilities.getCallbackHandle] 的返回类型。

### CallbackHandle.fromRawHandle()

```dart
CallbackHandle.fromRawHandle(int _handle)
```

使用原始回调句柄创建实例。

只应使用通过调用 [CallbackHandle.toRawHandle] 生成的值，否则该对象将是一个无效句柄。

### toRawHandle()

```dart
int toRawHandle()
```

获取原始回调句柄，以便通过 [MethodChannel](https://www.yuque.com/thyname/flutter.services/methodchannel) 或 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)（传递给另一个 [Isolate](https://www.yuque.com/thyname/dart.isolate/isolate)）传递。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# PluginUtilities

```dart
abstract final class PluginUtilities {}
```

面向 Flutter 插件开发者的功能集合。

另请参阅：

- [IsolateNameServer](https://www.yuque.com/thyname/dart.ui/isolatenameserver)，提供处理 [Isolate](https://www.yuque.com/thyname/dart.isolate/isolate) 的实用工具。

### getCallbackHandle()

```dart
CallbackHandle? getCallbackHandle(Function callback)
```

获取具名顶层或静态回调函数的句柄，该句柄可轻松在 isolate 之间传递。

`callback` 参数不能为 null。

返回一个 [CallbackHandle](https://www.yuque.com/thyname/dart.ui/callbackhandle)，可提供给 [PluginUtilities.getCallbackFromHandle] 以获取原始回调的 tear-off（函数引用）。如果 `callback` 不是顶层或静态函数，则返回 null。

### getCallbackFromHandle()

```dart
Function? getCallbackFromHandle(CallbackHandle handle)
```

获取由句柄表示的具名顶层或静态回调的 tear-off（函数引用）。

`handle` 参数不能为 null。

如果 `handle` 不是由 [PluginUtilities.getCallbackHandle] 返回的有效句柄，则返回 null。否则，返回与 `handle` 关联的回调的 tear-off。
