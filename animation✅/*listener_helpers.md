# AnimationLazyListenerMixin

```dart
mixin AnimationLazyListenerMixin {}
```

一个 mixin，用于帮助仅在此对象已注册监听器时才监听另一个对象。

此 mixin 提供了 [didRegisterListener] 和 [didUnregisterListener] 的实现，因此可以与需要这些方法的其他 mixin（如 [AnimationLocalListenersMixin](https://www.yuque.com/thyname/flutter.animation/animationlocallistenersmixin) 和 [AnimationLocalStatusListenersMixin](https://www.yuque.com/thyname/flutter.animation/animationlocalstatuslistenersmixin)）一起使用。

### didRegisterListener()

```dart
void didRegisterListener()
```

每当注册一个监听器导致监听器列表从空变为非空时，调用 [didStartListening]。

另请参阅：

- [didUnregisterListener]，它可能导致监听器列表再次变为空，进而再次调用 [didStartListening]。

### didUnregisterListener()

```dart
void didUnregisterListener()
```

当唯一剩余的监听器被注销、使列表变空时，调用 [didStopListening]。

另请参阅：

- [didRegisterListener]，它会导致监听器列表变为非空。

### didStartListening()

```dart
void didStartListening()
```

当监听器数量从零变为一时调用。

### didStopListening()

```dart
void didStopListening()
```

当监听器数量从一变为零时调用。

### isListening

```dart
bool get isListening
```

是否存在任何监听器。

# AnimationEagerListenerMixin

```dart
mixin AnimationEagerListenerMixin {}
```

一个 mixin，用 dispose 约定取代了 [didRegisterListener]/[didUnregisterListener] 约定。

此 mixin 提供了 [didRegisterListener] 和 [didUnregisterListener] 的实现，因此可以与需要这些方法的其他 mixin（如 [AnimationLocalListenersMixin](https://www.yuque.com/thyname/flutter.animation/animationlocallistenersmixin) 和 [AnimationLocalStatusListenersMixin](https://www.yuque.com/thyname/flutter.animation/animationlocalstatuslistenersmixin)）一起使用。

### didRegisterListener()

```dart
void didRegisterListener()
```

此实现会忽略监听器注册。

### didUnregisterListener()

```dart
void didUnregisterListener()
```

此实现会忽略监听器注册。

### dispose()

```dart
void dispose()
```

释放此对象使用的资源。调用此方法后，此对象将不再可用。

# AnimationLocalListenersMixin

```dart
mixin AnimationLocalListenersMixin {}
```

一个 mixin，实现了 [addListener]/[removeListener] 协议，并在调用 [notifyListeners] 时通知所有已注册的监听器。

此 mixin 要求混入的类提供 [didRegisterListener] 和 [didUnregisterListener] 方法。这些方法的实现可以通过混入此库中的其他 mixin（如 [AnimationLazyListenerMixin](https://www.yuque.com/thyname/flutter.animation/animationlazylistenermixin)）来获得。

### didRegisterListener()

```dart
void didRegisterListener()
```

在通过 [addListener] 添加监听器之前立即调用。

在调用此方法时，已注册的监听器尚未被 [notifyListeners] 通知。

### didUnregisterListener()

```dart
void didUnregisterListener()
```

在通过 [removeListener] 移除监听器之后立即调用。

在调用此方法时，已移除的监听器将不再被 [notifyListeners] 通知。

### addListener()

```dart
void addListener(VoidCallback listener)
```

每当动画的值发生变化时调用该监听器。

可以使用 [removeListener] 移除监听器。

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

停止在动画值发生变化时调用该监听器。

可以使用 [addListener] 添加监听器。

### clearListeners()

```dart
void clearListeners()
```

移除所有通过 [addListener] 添加的监听器。

如果使用此 mixin 的类同时使用了 [AnimationEagerListenerMixin](https://www.yuque.com/thyname/flutter.animation/animationeagerlistenermixin)，通常会在该类的 `dispose` 方法中调用此方法。

调用此方法不会触发 [didUnregisterListener]。

### notifyListeners()

```dart
void notifyListeners()
```

调用所有监听器。

如果在此函数执行期间添加或移除了监听器，这些修改不会影响本次迭代中被调用的监听器。

# AnimationLocalStatusListenersMixin

```dart
mixin AnimationLocalStatusListenersMixin {}
```

一个 mixin，实现了 addStatusListener/removeStatusListener 协议，并在调用 notifyStatusListeners 时通知所有已注册的监听器。

此 mixin 要求混入的类提供 [didRegisterListener] 和 [didUnregisterListener] 方法。这些方法的实现可以通过混入此库中的其他 mixin（如 [AnimationLazyListenerMixin](https://www.yuque.com/thyname/flutter.animation/animationlazylistenermixin)）来获得。

### didRegisterListener()

```dart
void didRegisterListener()
```

在通过 [addStatusListener] 添加状态监听器之前立即调用。

在调用此方法时，已注册的监听器尚未被 [notifyStatusListeners] 通知。

### didUnregisterListener()

```dart
void didUnregisterListener()
```

在通过 [removeStatusListener] 移除状态监听器之后立即调用。

在调用此方法时，已移除的监听器将不再被 [notifyStatusListeners] 通知。

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

每当动画的状态发生变化时调用该监听器。

可以使用 [removeStatusListener] 移除监听器。

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

停止在动画状态发生变化时调用该监听器。

可以使用 [addStatusListener] 添加监听器。

### clearStatusListeners()

```dart
void clearStatusListeners()
```

移除所有通过 [addStatusListener] 添加的监听器。

如果使用此 mixin 的类同时使用了 [AnimationEagerListenerMixin](https://www.yuque.com/thyname/flutter.animation/animationeagerlistenermixin)，通常会在该类的 `dispose` 方法中调用此方法。

调用此方法不会触发 [didUnregisterListener]。

### notifyStatusListeners()

```dart
void notifyStatusListeners(AnimationStatus status)
```

调用所有状态监听器。

如果在此函数执行期间添加或移除了监听器，这些修改不会影响本次迭代中被调用的监听器。
