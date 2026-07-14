# DartPluginRegistrant

```dart
abstract final class DartPluginRegistrant {}
```

用于 Dart 插件注册器的辅助函数。

### ensureInitialized()

```dart
void ensureInitialized()
```

确保已为此 isolate 调用过 Dart 插件注册器。可以在同一个 isolate 上安全地多次执行此操作，但不应在根 isolate 上调用。
