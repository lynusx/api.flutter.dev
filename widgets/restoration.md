@docImport 'container.dart'; @docImport 'restoration_properties.dart';

# RestorationScope

```dart
class RestorationScope extends StatefulWidget {}
```

Creates a new scope for restoration IDs used by descendant widgets to claim [RestorationBucket]s.

{@template flutter.widgets.RestorationScope} A restoration scope inserts a [RestorationBucket] into the widget tree, which descendant widgets can access via [RestorationScope.of]. It is uncommon for descendants to directly store data in this bucket. Instead, descendant widgets should consider storing their own restoration data in a child bucket claimed with [RestorationBucket.claimChild] from the bucket provided by this scope. {@endtemplate}

The bucket inserted into the widget tree by this scope has been claimed from the surrounding [RestorationScope] using the provided [restorationId]. If the [RestorationScope] is moved to a different part of the widget tree under a different [RestorationScope], the bucket owned by this scope with all its children and the data contained in them is moved to the new scope as well.

This widget will not make a [RestorationBucket] available to descendants if [restorationId] is null or when there is no surrounding restoration scope to claim a bucket from. In this case, descendant widgets invoking [RestorationScope.of] will receive null as a return value indicating that no bucket is available for storing restoration data. This will turn off state restoration for the widget subtree.

See also:

- [RootRestorationScope], which inserts the root bucket provided by the [RestorationManager] into the widget tree and makes it accessible for descendants via [RestorationScope.of].
- [UnmanagedRestorationScope], which inserts a provided [RestorationBucket] into the widget tree and makes it accessible for descendants via [RestorationScope.of].
- [RestorationMixin], which may be used in [State] objects to manage the restoration data of a [StatefulWidget] instead of manually interacting with [RestorationScope]s and [RestorationBucket]s.
- [RestorationManager], which describes the basic concepts of state restoration in Flutter.

### RestorationScope()

```dart
RestorationScope({dynamic key, required String? restorationId, required Widget child})
```

Creates a [RestorationScope].

Providing null as the [restorationId] turns off state restoration for the [child] and its descendants.

### maybeOf()

```dart
RestorationBucket? maybeOf(BuildContext context)
```

Returns the [RestorationBucket] inserted into the widget tree by the closest ancestor [RestorationScope] of `context`.

{@template flutter.widgets.restoration.RestorationScope.bucket_warning} To avoid accidentally overwriting data already stored in the bucket by its owner, data should not be stored directly in the bucket returned by this method. Instead, consider claiming a child bucket from the returned bucket (via [RestorationBucket.claimChild]) and store the restoration data in that child. {@endtemplate}

This method returns null if state restoration is turned off for this subtree.

Calling this method will create a dependency on the closest [RestorationScope] in the [context], if there is one.

See also:

- [RestorationScope.maybeOf], which is similar to this method, but asserts if no [RestorationScope] ancestor is found.

### of()

```dart
RestorationBucket of(BuildContext context)
```

Returns the [RestorationBucket] inserted into the widget tree by the closest ancestor [RestorationScope] of `context`.

{@macro flutter.widgets.restoration.RestorationScope.bucket_warning}

This method will assert in debug mode and throw an exception in release mode if state restoration is turned off for this subtree.

Calling this method will create a dependency on the closest [RestorationScope] in the [context].

See also:

- [RestorationScope.maybeOf], which is similar to this method, but returns null if no [RestorationScope] ancestor is found.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### restorationId

```dart
String? restorationId
```

The restoration ID used by this widget to obtain a child bucket from the surrounding [RestorationScope].

The child bucket obtained from the surrounding scope is made available to descendant widgets via [RestorationScope.of].

If this is null, [RestorationScope.of] invoked by descendants will return null which effectively turns off state restoration for this subtree.

### createState()

```dart
State<RestorationScope> createState()
```

# UnmanagedRestorationScope

```dart
class UnmanagedRestorationScope extends InheritedWidget {}
```

Inserts a provided [RestorationBucket] into the widget tree and makes it available to descendants via [RestorationScope.of].

{@macro flutter.widgets.RestorationScope}

If [bucket] is null, no restoration bucket is made available to descendant widgets ([RestorationScope.of] invoked from a descendant will return null). This effectively turns off state restoration for the subtree because no bucket for storing restoration data is made available.

See also:

- [RestorationScope], which inserts a bucket obtained from a surrounding restoration scope into the widget tree and makes it accessible for descendants via [RestorationScope.of].
- [RootRestorationScope], which inserts the root bucket provided by the [RestorationManager] into the widget tree and makes it accessible for descendants via [RestorationScope.of].
- [RestorationMixin], which may be used in [State] objects to manage the restoration data of a [StatefulWidget] instead of manually interacting with [RestorationScope]s and [RestorationBucket]s.
- [RestorationManager], which describes the basic concepts of state restoration in Flutter.

### UnmanagedRestorationScope()

```dart
UnmanagedRestorationScope({dynamic key, RestorationBucket? bucket, required Widget child})
```

Creates an [UnmanagedRestorationScope].

When [bucket] is null state restoration is turned off for the [child] and its descendants.

### bucket

```dart
RestorationBucket? bucket
```

The [RestorationBucket] that this widget will insert into the widget tree.

Descendant widgets may obtain this bucket via [RestorationScope.of].

### updateShouldNotify()

```dart
bool updateShouldNotify(UnmanagedRestorationScope oldWidget)
```

# RootRestorationScope

```dart
class RootRestorationScope extends StatefulWidget {}
```

Inserts a child bucket of [RestorationManager.rootBucket] into the widget tree and makes it available to descendants via [RestorationScope.of].

This widget is usually used near the root of the widget tree to enable the state restoration functionality for the application. For all other use cases, consider using a regular [RestorationScope] instead.

The root restoration bucket can only be retrieved asynchronously from the [RestorationManager]. To ensure that the provided [child] has its restoration data available the first time it builds, the [RootRestorationScope] will build an empty [Container] instead of the actual [child] until the root bucket is available. To hide the empty container from the eyes of users, the [RootRestorationScope] also delays rendering the first frame while the container is shown. On platforms that show a splash screen on app launch the splash screen is kept up (hiding the empty container) until the bucket is available and the [child] is ready to be build.

The exact behavior of this widget depends on its ancestors: When the [RootRestorationScope] does not find an ancestor restoration bucket via [RestorationScope.of] it will claim a child bucket from the root restoration bucket ([RestorationManager.rootBucket]) using the provided [restorationId] and inserts that bucket into the widget tree where descendants may access it via [RestorationScope.of]. If the [RootRestorationScope] finds a non-null ancestor restoration bucket via [RestorationScope.of] it will behave like a regular [RestorationScope] instead: It will claim a child bucket from that ancestor and insert that child into the widget tree.

Unlike the [RestorationScope] widget, the [RootRestorationScope] will guarantee that descendants have a bucket available for storing restoration data as long as [restorationId] is not null and [RestorationManager] is able to provide a root bucket. In other words, it will force-enable state restoration for the subtree if [restorationId] is not null.

If [restorationId] is null, no bucket is made available to descendants, which effectively turns off state restoration for this subtree.

See also:

- [RestorationScope], which inserts a bucket obtained from a surrounding restoration scope into the widget tree and makes it accessible for descendants via [RestorationScope.of].
- [UnmanagedRestorationScope], which inserts a provided [RestorationBucket] into the widget tree and makes it accessible for descendants via [RestorationScope.of].
- [RestorationMixin], which may be used in [State] objects to manage the restoration data of a [StatefulWidget] instead of manually interacting with [RestorationScope]s and [RestorationBucket]s.
- [RestorationManager], which describes the basic concepts of state restoration in Flutter.

### RootRestorationScope()

```dart
RootRestorationScope({dynamic key, required String? restorationId, required Widget child})
```

Creates a [RootRestorationScope].

Providing null as the [restorationId] turns off state restoration for the [child] and its descendants.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### restorationId

```dart
String? restorationId
```

The restoration ID used to identify the child bucket that this widget will insert into the tree.

If this is null, no bucket is made available to descendants and state restoration for the subtree is essentially turned off.

### createState()

```dart
State<RootRestorationScope> createState()
```

# RestorableProperty

```dart
abstract class RestorableProperty<T> extends ChangeNotifier {}
```

Manages an object of type `T`, whose value a [State] object wants to have restored during state restoration.

The property wraps an object of type `T`. It knows how to store its value in the restoration data and it knows how to re-instantiate that object from the information it previously stored in the restoration data.

The knowledge of how to store the wrapped object in the restoration data is encoded in the [toPrimitives] method and the knowledge of how to re-instantiate the object from that data is encoded in the [fromPrimitives] method. A call to [toPrimitives] must return a representation of the wrapped object that can be serialized with the [StandardMessageCodec]. If any collections (e.g. [List]s, [Map]s, etc.) are returned, they must not be modified after they have been returned from [toPrimitives]. At a later point in time (which may be after the application restarted), the data obtained from [toPrimitives] may be handed back to the property's [fromPrimitives] method to restore it to the previous state described by that data.

A [RestorableProperty] needs to be registered to a [RestorationMixin] using a restoration ID that is unique within the mixin. The [RestorationMixin] provides and manages the [RestorationBucket], in which the data returned by [toPrimitives] is stored.

Whenever the value returned by [toPrimitives] (or the [enabled] getter) changes, the [RestorableProperty] must call [notifyListeners]. This will trigger the [RestorationMixin] to update the data it has stored for the property in its [RestorationBucket] to the latest information returned by [toPrimitives].

When the property is registered with the [RestorationMixin], the mixin checks whether there is any restoration data available for the property. If data is available, the mixin calls [fromPrimitives] on the property, which must return an object that matches the object the property wrapped when the provided restoration data was obtained from [toPrimitives]. If no restoration data is available to restore the property's wrapped object from, the mixin calls [createDefaultValue]. The value returned by either of those methods is then handed to the property's [initWithValue] method.

Usually, subclasses of [RestorableProperty] hold on to the value provided to them in [initWithValue] and make it accessible to the [State] object that owns the property. This [RestorableProperty] base class, however, has no opinion about what to do with the value provided to [initWithValue].

The [RestorationMixin] may call [fromPrimitives]/[createDefaultValue] followed by [initWithValue] multiple times throughout the life of a [RestorableProperty]: Whenever new restoration data is made available to the [RestorationMixin] the property is registered with, the cycle of calling [fromPrimitives] (if the new restoration data contains information to restore the property from) or [createDefaultValue] (if no information for the property is available in the new restoration data) followed by a call to [initWithValue] repeats. Whenever [initWithValue] is called, the property should forget the old value it was wrapping and re-initialize itself with the newly provided value.

In a typical use case, a subclass of [RestorableProperty] is instantiated either to initialize a member variable of a [State] object or within [State.initState]. It is then registered to a [RestorationMixin] in [RestorationMixin.restoreState] and later [dispose]ed in [State.dispose]. For less common use cases (e.g. if the value stored in a [RestorableProperty] is only needed while the [State] object is in a certain state), a [RestorableProperty] may be registered with a [RestorationMixin] any time after [RestorationMixin.restoreState] has been called for the first time. A [RestorableProperty] may also be unregistered from a [RestorationMixin] before the owning [State] object is disposed by calling [RestorationMixin.unregisterFromRestoration]. This is uncommon, though, and will delete the information that the property contributed from the restoration data (meaning the value of the property will no longer be restored during a future state restoration).

See also:

- [RestorableValue], which is a [RestorableProperty] that makes the wrapped value accessible to the owning [State] object via a `value` getter and setter.
- [RestorationMixin], to which a [RestorableProperty] must be registered.
- [RestorationManager], which describes how state restoration works in Flutter.

### RestorableProperty()

```dart
RestorableProperty()
```

Creates a [RestorableProperty].

### createDefaultValue()

```dart
T createDefaultValue()
```

Called by the [RestorationMixin] if no restoration data is available to restore the value of the property from to obtain the default value for the property.

The method returns the default value that the property should wrap if no restoration data is available. After this is called, [initWithValue] will be called with this method's return value.

The method may be called multiple times throughout the life of the [RestorableProperty]. Whenever new restoration data has been provided to the [RestorationMixin] the property is registered to, either this method or [fromPrimitives] is called before [initWithValue] is invoked.

### fromPrimitives()

```dart
T fromPrimitives(Object? data)
```

Called by the [RestorationMixin] to convert the `data` previously retrieved from [toPrimitives] back into an object of type `T` that this property should wrap.

The object returned by this method is passed to [initWithValue] to restore the value that this property is wrapping to the value described by the provided `data`.

The method may be called multiple times throughout the life of the [RestorableProperty]. Whenever new restoration data has been provided to the [RestorationMixin] the property is registered to, either this method or [createDefaultValue] is called before [initWithValue] is invoked.

### initWithValue()

```dart
void initWithValue(T value)
```

Called by the [RestorationMixin] with the `value` returned by either [createDefaultValue] or [fromPrimitives] to set the value that this property currently wraps.

The [initWithValue] method may be called multiple times throughout the life of the [RestorableProperty] whenever new restoration data has been provided to the [RestorationMixin] the property is registered to. When [initWithValue] is called, the property should forget its previous value and re-initialize itself to the newly provided `value`.

### toPrimitives()

```dart
Object? toPrimitives()
```

Called by the [RestorationMixin] to retrieve the information that this property wants to store in the restoration data.

The returned object must be serializable with the [StandardMessageCodec] and if it includes any collections, those should not be modified after they have been returned by this method.

The information returned by this method may be handed back to the property in a call to [fromPrimitives] at a later point in time (possibly after the application restarted) to restore the value that the property is currently wrapping.

When the value returned by this method changes, the property must call [notifyListeners]. The [RestorationMixin] will invoke this method whenever the property's listeners are notified.

### enabled

```dart
bool get enabled
```

Whether the object currently returned by [toPrimitives] should be included in the restoration state.

When this returns false, no information is included in the restoration data for this property and the property will be initialized to its default value (obtained from [createDefaultValue]) the next time that restoration data is used for state restoration.

Whenever the value returned by this getter changes, [notifyListeners] must be called. When the value changes from true to false, the information last retrieved from [toPrimitives] is removed from the restoration data. When it changes from false to true, [toPrimitives] is invoked to add the latest restoration information provided by this property to the restoration data.

### dispose()

```dart
void dispose()
```

### state

```dart
State get state
```

The [State] object that this property is registered with.

Must only be called when [isRegistered] is true.

### isRegistered

```dart
bool get isRegistered
```

Whether this property is currently registered with a [RestorationMixin].

# RestorationMixin

```dart
mixin RestorationMixin<S extends StatefulWidget> on State<S> {}
```

Manages the restoration data for a [State] object of a [StatefulWidget].

Restoration data can be serialized out and, at a later point in time, be used to restore the stateful members in the [State] object to the same values they had when the data was generated.

This mixin organizes the restoration data of a [State] object in [RestorableProperty]. All the information that the [State] object wants to get restored during state restoration need to be saved in a subclass of [RestorableProperty]. For example, to restore the count value in a counter app, that value should be stored in a member variable of type [RestorableInt] instead of a plain member variable of type [int].

The mixin ensures that the current values of the [RestorableProperty]s are serialized as part of the restoration state. It is up to the [State] to ensure that the data stored in the properties is always up to date. When the widget is restored from previously generated restoration data, the values of the [RestorableProperty]s are automatically restored to the values that had when the restoration data was serialized out.

Within a [State] that uses this mixin, [RestorableProperty]s are usually instantiated to initialize member variables. Users of the mixin must override [restoreState] and register their previously instantiated [RestorableProperty]s in this method by calling [registerForRestoration]. The mixin calls this method for the first time right after [State.initState]. After registration, the values stored in the property have either been restored to their previous value or - if no restoration data for restoring is available - they are initialized with a property-specific default value. At the end of a [State] object's life cycle, all restorable properties must be disposed in [State.dispose].

In addition to being invoked right after [State.initState], [restoreState] is invoked again when new restoration data has been provided to the mixin. When this happens, the [State] object must re-register all properties with [registerForRestoration] again to restore them to their previous values as described by the new restoration data. All initialization logic that depends on the current value of a restorable property should be included in the [restoreState] method to ensure it re-executes when the properties are restored to a different value during the life time of the [State] object.

Internally, the mixin stores the restoration data from all registered properties in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the [State]-provided [restorationId]. The [restorationId] must be unique in the surrounding [RestorationScope]. State restoration is disabled for the [State] object using this mixin if [restorationId] is null or when there is no surrounding [RestorationScope]. In that case, the values of the registered properties will not be restored during state restoration.

The [RestorationBucket] used to store the registered properties is available via the [bucket] getter. Interacting directly with the bucket is uncommon, but the [State] object may make this bucket available for its descendants to claim child buckets from. For that, the [bucket] is injected into the widget tree in [State.build] with the help of an [UnmanagedRestorationScope].

The [bucket] getter returns null if state restoration is turned off. If state restoration is turned on or off during the lifetime of the widget (e.g. because [restorationId] changes from null to non-null) the value returned by the getter will also change from null to non-null or vice versa. The mixin calls [didToggleBucket] on itself to notify the [State] object about this change. Overriding this method is not necessary as long as the [State] object does not directly interact with the [bucket].

Whenever the value returned by [restorationId] changes, [didUpdateRestorationId] must be called (unless the change already triggers a call to [didUpdateWidget]).

{@tool dartpad} This example demonstrates how to make a simple counter app restorable by using the [RestorationMixin] and a [RestorableInt].

** See code in examples/api/lib/widgets/restoration/restoration_mixin.0.dart ** {@end-tool}

See also:

- [RestorableProperty], which is the base class for all restoration properties managed by this mixin.
- [RestorationManager], which describes how state restoration in Flutter works.
- [RestorationScope], which creates a new namespace for restoration IDs in the widget tree.

### restorationId

```dart
String? get restorationId
```

The restoration ID used for the [RestorationBucket] in which the mixin will store the restoration data of all registered properties.

The restoration ID is used to claim a child [RestorationScope] from the surrounding [RestorationScope] (accessed via [RestorationScope.of]) and the ID must be unique in that scope (otherwise an exception is triggered in debug mode).

State restoration for this mixin is turned off when this getter returns null or when there is no surrounding [RestorationScope] available. When state restoration is turned off, the values of the registered properties cannot be restored.

Whenever the value returned by this getter changes, [didUpdateRestorationId] must be called unless the (unless the change already triggered a call to [didUpdateWidget]).

The restoration ID returned by this getter is often provided in the constructor of the [StatefulWidget] that this [State] object is associated with.

### bucket

```dart
RestorationBucket? get bucket
```

The [RestorationBucket] used for the restoration data of the [RestorableProperty]s registered to this mixin.

The bucket has been claimed from the surrounding [RestorationScope] using [restorationId].

The getter returns null if state restoration is turned off. When state restoration is turned on or off during the lifetime of this mixin (and hence the return value of this getter switches between null and non-null) [didToggleBucket] is called.

Interacting directly with this bucket is uncommon. However, the bucket may be injected into the widget tree in the [State]'s `build` method using an [UnmanagedRestorationScope]. That allows descendants to claim child buckets from this bucket for their own restoration needs.

### restoreState()

```dart
void restoreState(RestorationBucket? oldBucket, bool initialRestore)
```

Called to initialize or restore the [RestorableProperty]s used by the [State] object.

This method is always invoked at least once right after [State.initState] to register the [RestorableProperty]s with the mixin even when state restoration is turned off or no restoration data is available for this [State] object.

Typically, [registerForRestoration] is called from this method to register all [RestorableProperty]s used by the [State] object with the mixin. The registration will either restore the property's value to the value described by the restoration data, if available, or, if no restoration data is available - initialize it to a property-specific default value.

The method is called again whenever new restoration data (in the form of a new [bucket]) has been provided to the mixin. When that happens, the [State] object must re-register all previously registered properties, which will restore their values to the value described by the new restoration data.

Since the method may change the value of the registered properties when new restoration state is provided, all initialization logic that depends on a specific value of a [RestorableProperty] should be included in this method. That way, that logic re-executes when the [RestorableProperty]s have their values restored from newly provided restoration data.

The first time the method is invoked, the provided `oldBucket` argument is always null. In subsequent calls triggered by new restoration data in the form of a new bucket, the argument given is the previous value of [bucket].

### didToggleBucket()

```dart
void didToggleBucket(RestorationBucket? oldBucket)
```

Called when [bucket] switches between null and non-null values.

[State] objects that wish to directly interact with the bucket may override this method to store additional values in the bucket when one becomes available or to save values stored in a bucket elsewhere when the bucket goes away. This is uncommon and storing those values in [RestorableProperty]s should be considered instead.

The `oldBucket` is provided to the method when the [bucket] getter changes from non-null to null. The `oldBucket` argument is null when the [bucket] changes from null to non-null.

See also:

- [restoreState], which is called when the [bucket] changes from one non-null value to another non-null value.

### registerForRestoration()

```dart
void registerForRestoration(RestorableProperty<Object?> property, String restorationId)
```

Registers a [RestorableProperty] for state restoration.

The registration associates the provided `property` with the provided `restorationId`. If restoration data is available for the provided `restorationId`, the property's value is restored to the value described by the restoration data. If no restoration data is available, the property will be initialized to a property-specific default value.

Each property within a [State] object must be registered under a unique ID. Only registered properties will have their values restored during state restoration.

Typically, this method is called from within [restoreState] to register all restorable properties of the owning [State] object. However, if a given [RestorableProperty] is only needed when certain conditions are met within the [State], [registerForRestoration] may also be called at any time after [restoreState] has been invoked for the first time.

A property that has been registered outside of [restoreState] must be re-registered within [restoreState] the next time that method is called unless it has been unregistered with [unregisterFromRestoration].

### unregisterFromRestoration()

```dart
void unregisterFromRestoration(RestorableProperty<Object?> property)
```

Unregisters a [RestorableProperty] from state restoration.

The value of the `property` is removed from the restoration data and it will not be restored if that data is used in a future state restoration.

Calling this method is uncommon, but may be necessary if the data of a [RestorableProperty] is only relevant when the [State] object is in a certain state. When the data of a property is no longer necessary to restore the internal state of a [State] object, it may be removed from the restoration data by calling this method.

### didUpdateRestorationId()

```dart
void didUpdateRestorationId()
```

Must be called when the value returned by [restorationId] changes.

This method is automatically called from [didUpdateWidget]. Therefore, manually invoking this method may be omitted when the change in [restorationId] was caused by an updated widget.

### didUpdateWidget()

```dart
void didUpdateWidget(S oldWidget)
```

### restorePending

```dart
bool get restorePending
```

Whether [restoreState] will be called at the beginning of the next build phase.

Returns true when new restoration data has been provided to the mixin, but the registered [RestorableProperty]s have not been restored to their new values (as described by the new restoration data) yet. The properties will get the values restored when [restoreState] is invoked at the beginning of the next build cycle.

While this is true, [bucket] will also still return the old bucket with the old restoration data. It will update to the new bucket with the new data just before [restoreState] is invoked.

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### dispose()

```dart
void dispose()
```
