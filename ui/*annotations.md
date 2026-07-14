# keepToString

```dart
pragma keepToString
```

注解，用于保留 [Object.toString] 的重写实现，而不是出于体积优化的目的将其移除。

对于特定的 URI（目前是 `dart:ui` 和 `package:flutter`），Dart 编译器会在 profile/release 模式下移除类中的 [Object.toString] 重写，以减小代码体积。

各个类可以通过以下注解来选择退出此行为：

- `@pragma('flutter:keep-to-string')`
- `@pragma('flutter:keep-to-string-in-subtypes')`

参见 https://github.com/dart-lang/sdk/blob/main/runtime/docs/pragmas.md

例如，在下面的类中，即使 `--delete-tostring-package-uri` 选项本应生效并将其替换为 `return super.toString();`，`toString` 方法仍会保持为 `return _buffer.toString();`。（按照惯例，`dart:ui` 通常以 `ui` 作为前缀导入。）

```dart
class MyStringBuffer {
  final StringBuffer _buffer = StringBuffer();

  // ...

  @ui.keepToString
  @override
  String toString() {
    return _buffer.toString();
  }
}
```
