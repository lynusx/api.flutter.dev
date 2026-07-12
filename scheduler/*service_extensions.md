@docImport 'binding.dart';

# SchedulerServiceExtensions

```dart
enum SchedulerServiceExtensions {}
```

调度器库的服务扩展常量。

这些常量将在框架注册服务扩展时使用，也会被调用这些服务扩展的工具和服务所使用。

应通过在枚举值上调用 `.name` 属性来获取这些扩展名称各自对应的字符串值。

此服务扩展的名称，调用时会更改 [timeDilation] 的值，该值决定了为便于开发调试而减慢动画速度的系数。

另请参阅：

- [timeDilation]，即此服务扩展所暴露的字段。
- [SchedulerBinding.initServiceExtensions]，此服务扩展在此处注册。
