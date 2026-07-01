# PointerRoute

```dart
typedef PointerRoute = void Function(PointerEvent event)
```

A callback that receives a [PointerEvent]

# PointerRouter

```dart
class PointerRouter {}
```

A routing table for [PointerEvent] events.

### addRoute()

```dart
void addRoute(int pointer, PointerRoute route, [Matrix4? transform])
```

Adds a route to the routing table.

Whenever this object routes a [PointerEvent] corresponding to pointer, call route.

Routes added reentrantly within [PointerRouter.route] will take effect when routing the next event.

### removeRoute()

```dart
void removeRoute(int pointer, PointerRoute route)
```

Removes a route from the routing table.

No longer call route when routing a [PointerEvent] corresponding to pointer. Requires that this route was previously added to the router.

Routes removed reentrantly within [PointerRouter.route] will take effect immediately.

### addGlobalRoute()

```dart
void addGlobalRoute(PointerRoute route, [Matrix4? transform])
```

Adds a route to the global entry in the routing table.

Whenever this object routes a [PointerEvent], call route.

Routes added reentrantly within [PointerRouter.route] will take effect when routing the next event.

### removeGlobalRoute()

```dart
void removeGlobalRoute(PointerRoute route)
```

Removes a route from the global entry in the routing table.

No longer call route when routing a [PointerEvent]. Requires that this route was previously added via [addGlobalRoute].

Routes removed reentrantly within [PointerRouter.route] will take effect immediately.

### debugGlobalRouteCount

```dart
int get debugGlobalRouteCount
```

The number of global routes that have been registered.

This is valid in debug builds only. In release builds, this will throw an [UnsupportedError].

### route()

```dart
void route(PointerEvent event)
```

Calls the routes registered for this pointer event.

Routes are called in the order in which they were added to the PointerRouter object.
