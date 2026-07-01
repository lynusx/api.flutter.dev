@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'scroll_view.dart';

# RouteInformation

```dart
class RouteInformation {}
```

A piece of routing information.

The route information consists of a location string of the application and a state object that configures the application in that location.

This information flows two ways, from the [RouteInformationProvider] to the [Router] or from the [Router] to [RouteInformationProvider].

In the former case, the [RouteInformationProvider] notifies the [Router] widget when a new [RouteInformation] is available. The [Router] widget takes these information and navigates accordingly.

The latter case happens in web application where the [Router] reports route changes back to the web engine.

The current [RouteInformation] of an application is also used for state restoration purposes. Before an application is killed, the [Router] converts its current configurations into a [RouteInformation] object utilizing the [RouteInformationProvider]. The [RouteInformation] object is then serialized out and persisted. During state restoration, the object is deserialized and passed back to the [RouteInformationProvider], which turns it into a configuration for the [Router] again to restore its state from.

### RouteInformation()

```dart
RouteInformation({String? location, Uri? uri, Object? state})
```

Creates a route information object.

Either `location` or `uri` must not be null.

### location

```dart
String get location
```

The location of the application.

The string is usually in the format of multiple string identifiers with slashes in between. ex: `/`, `/path`, `/path/to/the/app`.

### uri

```dart
Uri get uri
```

The uri location of the application.

The host and scheme will not be empty if this object is created from a deep link request. They represents the website that redirect the deep link.

In web platform, the host and scheme are always empty.

### state

```dart
Object? state
```

The state of the application in the [uri].

The app can have different states even in the same location. For example, the text inside a [TextField] or the scroll position in a [ScrollView]. These widget states can be stored in the [state].

On the web, this information is stored in the browser history when the [Router] reports this route information back to the web engine through the [PlatformRouteInformationProvider]. The information is then passed back, along with the [uri], when the user clicks the back or forward buttons.

This information is also serialized and persisted alongside the [uri] for state restoration purposes. During state restoration, the information is made available again to the [Router] so it can restore its configuration to the previous state.

The state must be serializable.

# RouterConfig

```dart
class RouterConfig<T> {}
```

A convenient bundle to configure a [Router] widget.

To configure a [Router] widget, one needs to provide several delegates, [RouteInformationProvider], [RouteInformationParser], [RouterDelegate], and [BackButtonDispatcher]. This abstract class provides way to bundle these delegates into a single object to configure a [Router].

The [backButtonDispatcher], [routeInformationProvider], and [routeInformationProvider] are optional.

The [routeInformationProvider] and [routeInformationParser] must both be provided or both not provided.

### RouterConfig()

```dart
RouterConfig({RouteInformationProvider? routeInformationProvider, RouteInformationParser<T>? routeInformationParser, required RouterDelegate<T> routerDelegate, BackButtonDispatcher? backButtonDispatcher})
```

Creates a [RouterConfig].

The [backButtonDispatcher], [routeInformationProvider], and [routeInformationParser] are optional.

The [routeInformationProvider] and [routeInformationParser] must both be provided or both not provided.

### routeInformationProvider

```dart
RouteInformationProvider? routeInformationProvider
```

The [RouteInformationProvider] that is used to configure the [Router].

### routeInformationParser

```dart
RouteInformationParser<T>? routeInformationParser
```

The [RouteInformationParser] that is used to configure the [Router].

### routerDelegate

```dart
RouterDelegate<T> routerDelegate
```

The [RouterDelegate] that is used to configure the [Router].

### backButtonDispatcher

```dart
BackButtonDispatcher? backButtonDispatcher
```

The [BackButtonDispatcher] that is used to configure the [Router].

# Router

```dart
class Router<T> extends StatefulWidget {}
```

The dispatcher for opening and closing pages of an application.

This widget listens for routing information from the operating system (e.g. an initial route provided on app startup, a new route obtained when an intent is received, or a notification that the user hit the system back button), parses route information into data of type `T`, and then converts that data into [Page] objects that it passes to a [Navigator].

Each part of this process can be overridden and configured as desired.

The [routeInformationProvider] can be overridden to change how the name of the route is obtained. The [RouteInformationProvider.value] is used as the initial route when the [Router] is first created. Subsequent notifications from the [RouteInformationProvider] to its listeners are treated as notifications that the route information has changed.

The [backButtonDispatcher] can be overridden to change how back button notifications are received. This must be a [BackButtonDispatcher], which is an object where callbacks can be registered, and which can be chained so that back button presses are delegated to subsidiary routers. The callbacks are invoked to indicate that the user is trying to close the current route (by pressing the system back button); the [Router] ensures that when this callback is invoked, the message is passed to the [routerDelegate] and its result is provided back to the [backButtonDispatcher]. Some platforms don't have back buttons (e.g. iOS and desktop platforms); on those platforms this notification is never sent. Typically, the [backButtonDispatcher] for the root router is an instance of [RootBackButtonDispatcher], which uses a [WidgetsBindingObserver] to listen to the `popRoute` notifications from [SystemChannels.navigation]. Nested [Router]s typically use a [ChildBackButtonDispatcher], which must be provided the [BackButtonDispatcher] of its ancestor [Router] (available via [Router.of]).

The [routeInformationParser] can be overridden to change how names obtained from the [routeInformationProvider] are interpreted. It must implement the [RouteInformationParser] interface, specialized with the same type as the [Router] itself. This type, `T`, represents the data type that the [routeInformationParser] will generate.

The [routerDelegate] can be overridden to change how the output of the [routeInformationParser] is interpreted. It must implement the [RouterDelegate] interface, also specialized with `T`; it takes as input the data (of type `T`) from the [routeInformationParser], and is responsible for providing a navigating widget to insert into the widget tree. The [RouterDelegate] interface is also [Listenable]; notifications are taken to mean that the [Router] needs to rebuild.

## Concerns regarding asynchrony

Some of the APIs (notably those involving [RouteInformationParser] and [RouterDelegate]) are asynchronous.

When developing objects implementing these APIs, if the work can be done entirely synchronously, then consider using [SynchronousFuture] for the future returned from the relevant methods. This will allow the [Router] to proceed in a completely synchronous way, which removes a number of complications.

Using asynchronous computation is entirely reasonable, however, and the API is designed to support it. For example, maybe a set of images need to be loaded before a route can be shown; waiting for those images to be loaded before [RouterDelegate.setNewRoutePath] returns is a reasonable approach to handle this case.

If an asynchronous operation is ongoing when a new one is to be started, the precise behavior will depend on the exact circumstances, as follows:

If the active operation is a [routeInformationParser] parsing a new route information: that operation's result, if it ever completes, will be discarded.

If the active operation is a [routerDelegate] handling a pop request: the previous pop is immediately completed with "false", claiming that the previous pop was not handled (this may cause the application to close).

If the active operation is a [routerDelegate] handling an initial route or a pushed route, the result depends on the new operation. If the new operation is a pop request, then the original operation's result, if it ever completes, will be discarded. If the new operation is a push request, however, the [routeInformationParser] will be requested to start the parsing, and only if that finishes before the original [routerDelegate] request completes will that original request's result be discarded.

If the identity of the [Router] widget's delegates change while an asynchronous operation is in progress, to keep matters simple, all active asynchronous operations will have their results discarded. It is generally considered unusual for these delegates to change during the lifetime of the [Router].

If the [Router] itself is disposed while an asynchronous operation is in progress, all active asynchronous operations will have their results discarded also.

No explicit signals are provided to the [routeInformationParser] or [routerDelegate] to indicate when any of the above happens, so it is strongly recommended that [RouteInformationParser] and [RouterDelegate] implementations not perform extensive computation.

## Application architectural design

An application can have zero, one, or many [Router] widgets, depending on its needs.

An application might have no [Router] widgets if it has only one "screen", or if the facilities provided by [Navigator] are sufficient. This is common for desktop applications, where subsidiary "screens" are represented using different windows rather than changing the active interface.

A particularly elaborate application might have multiple [Router] widgets, in a tree configuration, with the first handling the entire route parsing and making the result available for routers in the subtree. The routers in the subtree do not participate in route information parsing but merely take the result from the first router to build their sub routes.

Most applications only need a single [Router].

## URL updates for web applications

In the web platform, keeping the URL in the browser's location bar up to date with the application state ensures that the browser constructs its history entry correctly, allowing its back and forward buttons to function as the user expects.

If an app state change leads to the [Router] rebuilding, the [Router] will retrieve the new route information from the [routerDelegate]'s [RouterDelegate.currentConfiguration] method and the [routeInformationParser]'s [RouteInformationParser.restoreRouteInformation] method.

If the location in the new route information is different from the current location, this is considered to be a navigation event, the [PlatformRouteInformationProvider.routerReportsNewRouteInformation] method calls [SystemNavigator.routeInformationUpdated] with `replace = false` to notify the engine, and through that the browser, to create a history entry with the new url. Otherwise, [PlatformRouteInformationProvider.routerReportsNewRouteInformation] calls [SystemNavigator.routeInformationUpdated] with `replace = true` to update the current history entry with the latest [RouteInformation].

One can force the [Router] to report new route information as navigation event to the [routeInformationProvider] (and thus the browser) even if the [RouteInformation.uri] has not changed by calling the [Router.navigate] method with a callback that performs the state change. This causes [Router] to call the [RouteInformationProvider.routerReportsNewRouteInformation] with [RouteInformationReportingType.navigate], and thus causes [PlatformRouteInformationProvider] to push a new history entry regardlessly. This allows one to support the browser's back and forward buttons without changing the URL. For example, the scroll position of a scroll view may be saved in the [RouteInformation.state]. Using [Router.navigate] to update the scroll position causes the browser to create a new history entry with the [RouteInformation.state] that stores this new scroll position. When the user clicks the back button, the app will go back to the previous scroll position without changing the URL in the location bar.

One can also force the [Router] to ignore a navigation event by making those changes during a callback passed to [Router.neglect]. The [Router] calls the [RouteInformationProvider.routerReportsNewRouteInformation] with [RouteInformationReportingType.neglect], and thus causes [PlatformRouteInformationProvider] to replace the current history entry regardlessly even if it detects location change.

To opt out of URL updates entirely, pass null for [routeInformationProvider] and [routeInformationParser]. This is not recommended in general, but may be appropriate in the following cases:

- The application does not target the web platform.

- There are multiple router widgets in the application. Only one [Router] widget should update the URL (typically the top-most one created by the [WidgetsApp.router], [MaterialApp.router], or [CupertinoApp.router]).

- The application does not need to implement in-app navigation using the browser's back and forward buttons.

In other cases, it is strongly recommended to implement the [RouterDelegate.currentConfiguration] and [RouteInformationParser.restoreRouteInformation] APIs to provide an optimal user experience when running on the web platform.

## State Restoration

The [Router] will restore the current configuration of the [routerDelegate] during state restoration if it is configured with a [restorationScopeId] and state restoration is enabled for the subtree. For that, the value of [RouterDelegate.currentConfiguration] is serialized and persisted before the app is killed by the operating system. After the app is restarted, the value is deserialized and passed back to the [RouterDelegate] via a call to [RouterDelegate.setRestoredRoutePath] (which by default just calls [RouterDelegate.setNewRoutePath]). It is the responsibility of the [RouterDelegate] to use the configuration information provided to restore its internal state.

To serialize [RouterDelegate.currentConfiguration] and to deserialize it again, the [Router] calls [RouteInformationParser.restoreRouteInformation] and [RouteInformationParser.parseRouteInformation], respectively. Therefore, if a [restorationScopeId] is provided, a [routeInformationParser] must be configured as well.

### Router()

```dart
Router({dynamic key, RouteInformationProvider? routeInformationProvider, RouteInformationParser<T>? routeInformationParser, required RouterDelegate<T> routerDelegate, BackButtonDispatcher? backButtonDispatcher, String? restorationScopeId})
```

Creates a router.

The [routeInformationProvider] and [routeInformationParser] can be null if this router does not depend on route information. A common example is a sub router that builds its content completely based on the app state.

The [routeInformationProvider] and [routeInformationParser] must both be provided or not provided.

### Router.withConfig()

```dart
Router.withConfig({Key? key, required RouterConfig<T> config, String? restorationScopeId})
```

Creates a router with a [RouterConfig].

The [RouterConfig.routeInformationProvider] and [RouterConfig.routeInformationParser] can be null if this router does not depend on route information. A common example is a sub router that builds its content completely based on the app state.

If the [RouterConfig.routeInformationProvider] is not null, then [RouterConfig.routeInformationParser] must also not be null.

### routeInformationProvider

```dart
RouteInformationProvider? routeInformationProvider
```

The route information provider for the router.

The value at the time of first build will be used as the initial route. The [Router] listens to this provider and rebuilds with new names when it notifies.

This can be null if this router does not rely on the route information to build its content. In such case, the [routeInformationParser] must also be null.

### routeInformationParser

```dart
RouteInformationParser<T>? routeInformationParser
```

The route information parser for the router.

When the [Router] gets a new route information from the [routeInformationProvider], the [Router] uses this delegate to parse the route information and produce a configuration. The configuration will be used by [routerDelegate] and eventually rebuilds the [Router] widget.

Since this delegate is the primary consumer of the [routeInformationProvider], it must not be null if [routeInformationProvider] is not null.

### routerDelegate

```dart
RouterDelegate<T> routerDelegate
```

The router delegate for the router.

This delegate consumes the configuration from [routeInformationParser] and builds a navigating widget for the [Router].

It is also the primary respondent for the [backButtonDispatcher]. The [Router] relies on [RouterDelegate.popRoute] to handle the back button.

If the [RouterDelegate.currentConfiguration] returns a non-null object, this [Router] will opt for URL updates.

### backButtonDispatcher

```dart
BackButtonDispatcher? backButtonDispatcher
```

The back button dispatcher for the router.

The two common alternatives are the [RootBackButtonDispatcher] for root router, or the [ChildBackButtonDispatcher] for other routers.

### restorationScopeId

```dart
String? restorationScopeId
```

Restoration ID to save and restore the state of the [Router].

If non-null, the [Router] will persist the [RouterDelegate]'s current configuration (i.e. [RouterDelegate.currentConfiguration]). During state restoration, the [Router] informs the [RouterDelegate] of the previous configuration by calling [RouterDelegate.setRestoredRoutePath] (which by default just calls [RouterDelegate.setNewRoutePath]). It is the responsibility of the [RouterDelegate] to restore its internal state based on the provided configuration.

The router uses the [RouteInformationParser] to serialize and deserialize [RouterDelegate.currentConfiguration]. Therefore, a [routeInformationParser] must be provided when [restorationScopeId] is non-null.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### of()

```dart
Router<T> of<T extends Object?>(BuildContext context)
```

Retrieves the immediate [Router] ancestor from the given context.

This method provides access to the delegates in the [Router]. For example, this can be used to access the [backButtonDispatcher] of the parent router when creating a [ChildBackButtonDispatcher] for a nested [Router].

If no [Router] ancestor exists for the given context, this will assert in debug mode, and throw an exception in release mode.

See also:

- [maybeOf], which is a similar function, but it will return null instead of throwing an exception if no [Router] ancestor exists.

### maybeOf()

```dart
Router<T>? maybeOf<T extends Object?>(BuildContext context)
```

Retrieves the immediate [Router] ancestor from the given context.

This method provides access to the delegates in the [Router]. For example, this can be used to access the [backButtonDispatcher] of the parent router when creating a [ChildBackButtonDispatcher] for a nested [Router].

If no `Router` ancestor exists for the given context, this will return null.

See also:

- [of], a similar method that returns a non-nullable value, and will throw if no [Router] ancestor exists.

### navigate()

```dart
void navigate(BuildContext context, VoidCallback callback)
```

Forces the [Router] to run the [callback] and create a new history entry in the browser.

The web application relies on the [Router] to report new route information in order to create browser history entry. The [Router] will only report them if it detects the [RouteInformation.uri] changes. Use this method if you want the [Router] to report the route information even if the location does not change. This can be useful when you want to support the browser backward and forward button without changing the URL.

For example, you can store certain state such as the scroll position into the [RouteInformation.state]. If you use this method to update the scroll position multiple times with the same URL, the browser will create a stack of new history entries with the same URL but different [RouteInformation.state]s that store the new scroll positions. If the user click the backward button in the browser, the browser will restore the scroll positions saved in history entries without changing the URL.

See also:

- [Router]: see the "URL updates for web applications" section for more information about route information reporting.
- [neglect]: which forces the [Router] to not create a new history entry even if location does change.

### neglect()

```dart
void neglect(BuildContext context, VoidCallback callback)
```

Forces the [Router] to run the [callback] without creating a new history entry in the browser.

The web application relies on the [Router] to report new route information in order to create browser history entry. The [Router] will report them automatically if it detects the [RouteInformation.uri] changes.

Creating a new route history entry makes users feel they have visited a new page, and the browser back button brings them back to previous history entry. Use this method if you don't want the [Router] to create a new route information even if it detects changes as a result of running the [callback].

Using this method will still update the URL and state in current history entry.

See also:

- [Router]: see the "URL updates for web applications" section for more information about route information reporting.
- [navigate]: which forces the [Router] to create a new history entry even if location does not change.

### createState()

```dart
State<Router<T>> createState()
```

# RouteInformationReportingType

```dart
enum RouteInformationReportingType {}
```

The [Router]'s intention when it reports a new [RouteInformation] to the [RouteInformationProvider].

See also:

- [RouteInformationProvider.routerReportsNewRouteInformation]: which is called by the router when it has a new route information to report.

Router does not have a specific intention.

The router generates a new route information every time it detects route information may have change due to a rebuild. This is the default type if neither [Router.neglect] nor [Router.navigate] was used during the rebuild.

The accompanying [RouteInformation] were generated during a [Router.neglect] call.

The accompanying [RouteInformation] were generated during a [Router.navigate] call.

# BackButtonDispatcher

```dart
abstract class BackButtonDispatcher extends _CallbackHookProvider<Future<bool>> {}
```

Report to a [Router] when the user taps the back button on platforms that support back buttons (such as Android).

When [Router] widgets are nested, consider using a [ChildBackButtonDispatcher], passing it the parent [BackButtonDispatcher], so that the back button requests get dispatched to the appropriate [Router]. To make this work properly, it's important that whenever a [Router] thinks it should get the back button messages (e.g. after the user taps inside it), it calls [takePriority] on its [BackButtonDispatcher] (or [ChildBackButtonDispatcher]) instance.

The class takes a single callback, which must return a [Future<bool>]. The callback's semantics match [WidgetsBindingObserver.didPopRoute]'s, namely, the callback should return a future that completes to true if it can handle the pop request, and a future that completes to false otherwise.

### hasCallbacks

```dart
bool get hasCallbacks
```

### invokeCallback()

```dart
Future<bool> invokeCallback(Future<bool> defaultValue)
```

Handles a pop route request.

This method prioritizes the children list in reverse order and calls [ChildBackButtonDispatcher.notifiedByParent] on them. If any of them handles the request (by returning a future with true), it exits this method by returning this future. Otherwise, it keeps moving on to the next child until a child handles the request. If none of the children handles the request, this back button dispatcher will then try to handle the request by itself. This back button dispatcher handles the request by notifying the router which in turn calls the [RouterDelegate.popRoute] and returns its result.

To decide whether this back button dispatcher will handle the pop route request, you can override the [RouterDelegate.popRoute] of the router delegate you pass into the router with this back button dispatcher to return a future of true or false.

### createChildBackButtonDispatcher()

```dart
ChildBackButtonDispatcher createChildBackButtonDispatcher()
```

Creates a [ChildBackButtonDispatcher] that is a direct descendant of this back button dispatcher.

To participate in handling the pop route request, call the [takePriority] on the [ChildBackButtonDispatcher] created from this method.

When the pop route request is handled by this back button dispatcher, it propagate the request to its direct descendants that have called the [takePriority] method. If there are multiple candidates, the latest one that called the [takePriority] wins the right to handle the request. If the latest one does not handle the request (by returning a future of false in [ChildBackButtonDispatcher.notifiedByParent]), the second latest one will then have the right to handle the request. This dispatcher continues finding the next candidate until there are no more candidates and finally handles the request itself.

### takePriority()

```dart
void takePriority()
```

Make this [BackButtonDispatcher] take priority among its peers.

This has no effect when a [BackButtonDispatcher] has no parents and no children. If a [BackButtonDispatcher] does have parents or children, however, it causes this object to be the one to dispatch the notification when the parent would normally notify its callback.

The [BackButtonDispatcher] must have a listener registered before it can be told to take priority.

### deferTo()

```dart
void deferTo(ChildBackButtonDispatcher child)
```

Mark the given child as taking priority over this object and the other children.

This causes [invokeCallback] to defer to the given child instead of calling this object's callback.

Children are stored in a list, so that if the current child is removed using [forget], a previous child will return to take its place. When [takePriority] is called, the list is cleared.

Calling this again without first calling [forget] moves the child back to the head of the list.

The [BackButtonDispatcher] must have a listener registered before it can be told to defer to a child.

### forget()

```dart
void forget(ChildBackButtonDispatcher child)
```

Causes the given child to be removed from the list of children to which this object might defer, as if [deferTo] had never been called for that child.

This should only be called once per child, even if [deferTo] was called multiple times for that child.

If no children are left in the list, this object will stop deferring to its children. (This is not the same as calling [takePriority], since, if this object itself is a [ChildBackButtonDispatcher], [takePriority] would additionally attempt to claim priority from its parent, whereas removing the last child does not.)

# RootBackButtonDispatcher

```dart
class RootBackButtonDispatcher extends BackButtonDispatcher with WidgetsBindingObserver {}
```

The default implementation of back button dispatcher for the root router.

This dispatcher listens to platform pop route notifications. When the platform wants to pop the current route, this dispatcher calls the [BackButtonDispatcher.invokeCallback] method to handle the request.

### RootBackButtonDispatcher()

```dart
RootBackButtonDispatcher()
```

Create a root back button dispatcher.

### addCallback()

```dart
void addCallback(ValueGetter<Future<bool>> callback)
```

### removeCallback()

```dart
void removeCallback(ValueGetter<Future<bool>> callback)
```

### didPopRoute()

```dart
Future<bool> didPopRoute()
```

# ChildBackButtonDispatcher

```dart
class ChildBackButtonDispatcher extends BackButtonDispatcher {}
```

A variant of [BackButtonDispatcher] which listens to notifications from a parent back button dispatcher, and can take priority from its parent for the handling of such notifications.

Useful when [Router]s are being nested within each other.

Use [Router.of] to obtain a reference to the nearest ancestor [Router], from which the [Router.backButtonDispatcher] can be found, and then used as the [parent] of the [ChildBackButtonDispatcher].

### ChildBackButtonDispatcher()

```dart
ChildBackButtonDispatcher(BackButtonDispatcher parent)
```

Creates a back button dispatcher that acts as the child of another.

### parent

```dart
BackButtonDispatcher parent
```

The back button dispatcher that this object will attempt to take priority over when [takePriority] is called.

The parent must have a listener registered before this child object can have its [takePriority] or [deferTo] methods used.

### notifiedByParent()

```dart
Future<bool> notifiedByParent(Future<bool> defaultValue)
```

The parent of this child back button dispatcher decide to let this child to handle the invoke the callback request in [BackButtonDispatcher.invokeCallback].

Return a boolean future with true if this child will handle the request; otherwise, return a boolean future with false.

### takePriority()

```dart
void takePriority()
```

### deferTo()

```dart
void deferTo(ChildBackButtonDispatcher child)
```

### removeCallback()

```dart
void removeCallback(ValueGetter<Future<bool>> callback)
```

# BackButtonListener

```dart
class BackButtonListener extends StatefulWidget {}
```

A convenience widget that registers a callback for when the back button is pressed.

In order to use this widget, there must be an ancestor [Router] widget in the tree that has a [RootBackButtonDispatcher]. e.g. The [Router] widget created by the [MaterialApp.router] has a built-in [RootBackButtonDispatcher] by default.

It only applies to platforms that accept back button clicks, such as Android.

It can be useful for scenarios, in which you create a different state in your screen but don't want to use a new page for that.

### BackButtonListener()

```dart
BackButtonListener({dynamic key, required Widget child, required ValueGetter<Future<bool>> onBackButtonPressed})
```

Creates a BackButtonListener widget .

### child

```dart
Widget child
```

The widget below this widget in the tree.

### onBackButtonPressed

```dart
ValueGetter<Future<bool>> onBackButtonPressed
```

The callback function that will be called when the back button is pressed.

It must return a boolean future with true if this child will handle the request; otherwise, return a boolean future with false.

### createState()

```dart
State<BackButtonListener> createState()
```

# RouteInformationParser

```dart
abstract class RouteInformationParser<T> {}
```

A delegate that is used by the [Router] widget to parse a route information into a configuration of type T.

This delegate is used when the [Router] widget is first built with initial route information from [Router.routeInformationProvider] and any subsequent new route notifications from it. The [Router] widget calls the [parseRouteInformation] with the route information from [Router.routeInformationProvider].

One of the [parseRouteInformation] or [parseRouteInformationWithDependencies] must be implemented, otherwise a runtime error will be thrown.

### RouteInformationParser()

```dart
RouteInformationParser()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### parseRouteInformation()

```dart
Future<T> parseRouteInformation(RouteInformation routeInformation)
```

{@template flutter.widgets.RouteInformationParser.parseRouteInformation} Converts the given route information into parsed data to pass to a [RouterDelegate].

The method should return a future which completes when the parsing is complete. The parsing may be asynchronous if, e.g., the parser needs to communicate with the OEM thread to obtain additional data about the route.

Consider using a [SynchronousFuture] if the result can be computed synchronously, so that the [Router] does not need to wait for the next microtask to pass the data to the [RouterDelegate]. {@endtemplate}

One can implement [parseRouteInformationWithDependencies] instead if the parsing depends on other dependencies from the [BuildContext].

### parseRouteInformationWithDependencies()

```dart
Future<T> parseRouteInformationWithDependencies(RouteInformation routeInformation, BuildContext context)
```

{@macro flutter.widgets.RouteInformationParser.parseRouteInformation}

The input [BuildContext] can be used for looking up [InheritedWidget]s If one uses [BuildContext.dependOnInheritedWidgetOfExactType], a dependency will be created. The [Router] will re-parse the [RouteInformation] from its [RouteInformationProvider] if the dependency notifies its listeners.

One can also use [BuildContext.getElementForInheritedWidgetOfExactType] to look up [InheritedWidget]s without creating dependencies.

### restoreRouteInformation()

```dart
RouteInformation? restoreRouteInformation(T configuration)
```

Restore the route information from the given configuration.

This may return null, in which case the browser history will not be updated and state restoration is disabled. See [Router]'s documentation for details.

The [parseRouteInformation] method must produce an equivalent configuration when passed this method's return value.

# RouterDelegate

```dart
abstract class RouterDelegate<T> extends Listenable {}
```

A delegate that is used by the [Router] widget to build and configure a navigating widget.

This delegate is the core piece of the [Router] widget. It responds to push route and pop route intents from the engine and notifies the [Router] to rebuild. It also acts as a builder for the [Router] widget and builds a navigating widget, typically a [Navigator], when the [Router] widget builds.

When the engine pushes a new route, the route information is parsed by the [RouteInformationParser] to produce a configuration of type T. The router delegate receives the configuration through [setInitialRoutePath] or [setNewRoutePath] to configure itself and builds the latest navigating widget when asked ([build]).

When implementing subclasses, consider defining a [Listenable] app state object to be used for building the navigating widget. The router delegate would update the app state accordingly and notify its own listeners when the app state has changed and when it receive route related engine intents (e.g. [setNewRoutePath], [setInitialRoutePath], or [popRoute]).

All subclass must implement [setNewRoutePath], [popRoute], and [build].

## State Restoration

If the [Router] owning this delegate is configured for state restoration, it will persist and restore the configuration of this [RouterDelegate] using the following mechanism: Before the app is killed by the operating system, the value of [currentConfiguration] is serialized out and persisted. After the app has restarted, the value is deserialized and passed back to the [RouterDelegate] via a call to [setRestoredRoutePath] (which by default just calls [setNewRoutePath]). It is the responsibility of the [RouterDelegate] to use the configuration information provided to restore its internal state.

See also:

- [RouteInformationParser], which is responsible for parsing the route information to a configuration before passing in to router delegate.
- [Router], which is the widget that wires all the delegates together to provide a fully functional routing solution.

### setInitialRoutePath()

```dart
Future<void> setInitialRoutePath(T configuration)
```

Called by the [Router] at startup with the structure that the [RouteInformationParser] obtained from parsing the initial route.

This should configure the [RouterDelegate] so that when [build] is invoked, it will create a widget tree that matches the initial route.

By default, this method forwards the [configuration] to [setNewRoutePath].

Consider using a [SynchronousFuture] if the result can be computed synchronously, so that the [Router] does not need to wait for the next microtask to schedule a build.

See also:

- [setRestoredRoutePath], which is called instead of this method during state restoration.

### setRestoredRoutePath()

```dart
Future<void> setRestoredRoutePath(T configuration)
```

Called by the [Router] during state restoration.

When the [Router] is configured for state restoration, it will persist the value of [currentConfiguration] during state serialization. During state restoration, the [Router] calls this method (instead of [setInitialRoutePath]) to pass the previous configuration back to the delegate. It is the responsibility of the delegate to restore its internal state based on the provided configuration.

By default, this method forwards the `configuration` to [setNewRoutePath].

### setNewRoutePath()

```dart
Future<void> setNewRoutePath(T configuration)
```

Called by the [Router] when the [Router.routeInformationProvider] reports that a new route has been pushed to the application by the operating system.

Consider using a [SynchronousFuture] if the result can be computed synchronously, so that the [Router] does not need to wait for the next microtask to schedule a build.

### popRoute()

```dart
Future<bool> popRoute()
```

Called by the [Router] when the [Router.backButtonDispatcher] reports that the operating system is requesting that the current route be popped.

The method should return a boolean [Future] to indicate whether this delegate handles the request. Returning true indicates that the request has been handled and prevents it from bubbling up. Returning false means this delegate did not handle the request, so the request may continue to a parent [BackButtonDispatcher] in a nested [Router] setup. If the request reaches the root [WidgetsBinding] and remains unhandled, the platform is requested to pop the application by calling [SystemNavigator.pop].

Consider using a [SynchronousFuture] if the result can be computed synchronously, so that the [Router] does not need to wait for the next microtask to schedule a build.

### currentConfiguration

```dart
T? get currentConfiguration
```

Called by the [Router] when it detects a route information may have changed as a result of rebuild.

If this getter returns non-null, the [Router] will start to report new route information back to the engine. In web applications, the new route information is used for populating browser history in order to support the forward and the backward buttons.

When overriding this method, the configuration returned by this getter must be able to construct the current app state and build the widget with the same configuration in the [build] method if it is passed back to the [setNewRoutePath]. Otherwise, the browser backward and forward buttons will not work properly.

By default, this getter returns null, which prevents the [Router] from reporting the route information. To opt in, a subclass can override this getter to return the current configuration.

At most one [Router] can opt in to route information reporting. Typically, only the top-most [Router] created by [WidgetsApp.router] should opt for route information reporting.

## State Restoration

This getter is also used by the [Router] to implement state restoration. During state serialization, the [Router] will persist the current configuration and during state restoration pass it back to the delegate by calling [setRestoredRoutePath].

### build()

```dart
Widget build(BuildContext context)
```

Called by the [Router] to obtain the widget tree that represents the current state.

This is called whenever the [Future]s returned by [setInitialRoutePath], [setNewRoutePath], or [setRestoredRoutePath] complete as well as when this notifies its clients (see the [Listenable] interface, which this interface includes). In addition, it may be called at other times. It is important, therefore, that the methods above do not update the state that the [build] method uses before they complete their respective futures.

Typically this method returns a suitably-configured [Navigator]. If you do plan to create a navigator, consider using the [PopNavigatorRouterDelegateMixin]. If state restoration is enabled for the [Router] using this delegate, consider providing a non-null [Navigator.restorationScopeId] to the [Navigator] returned by this method.

This method must not return null.

The `context` is the [Router]'s build context.

# RouteInformationProvider

```dart
abstract class RouteInformationProvider extends ValueListenable<RouteInformation> {}
```

A route information provider that provides route information for the [Router] widget

This provider is responsible for handing the route information through [value] getter and notifies listeners, typically the [Router] widget, when a new route information is available.

When the router opts for route information reporting (by overriding the [RouterDelegate.currentConfiguration] to return non-null), override the [routerReportsNewRouteInformation] method to process the route information.

See also:

- [PlatformRouteInformationProvider], which wires up the itself with the [WidgetsBindingObserver.didPushRoute] to propagate platform push route intent to the [Router] widget, as well as reports new route information from the [Router] back to the engine by overriding the [routerReportsNewRouteInformation].

### routerReportsNewRouteInformation()

```dart
void routerReportsNewRouteInformation(RouteInformation routeInformation, {RouteInformationReportingType type = RouteInformationReportingType.none})
```

A callback called when the [Router] widget reports new route information

The subclasses can override this method to update theirs values or trigger other side effects. For example, the [PlatformRouteInformationProvider] overrides this method to report the route information back to the engine.

The `routeInformation` is the new route information generated by the Router rebuild, and it can be the same or different from the [value].

The `type` denotes the [Router]'s intention when it reports this `routeInformation`. It is useful when deciding how to update the internal state of [RouteInformationProvider] subclass with the `routeInformation`. For example, [PlatformRouteInformationProvider] uses this property to decide whether to push or replace the browser history entry with the new `routeInformation`.

For more information on how [Router] determines a navigation event, see the "URL updates for web applications" section in the [Router] documentation.

# PlatformRouteInformationProvider

```dart
class PlatformRouteInformationProvider extends RouteInformationProvider with WidgetsBindingObserver, ChangeNotifier {}
```

The route information provider that propagates the platform route information changes.

This provider also reports the new route information from the [Router] widget back to engine using message channel method, the [SystemNavigator.routeInformationUpdated].

Each time [SystemNavigator.routeInformationUpdated] is called, the [SystemNavigator.selectMultiEntryHistory] method is also called. This overrides the initialization behavior of [Navigator.reportsRouteUpdateToEngine].

### PlatformRouteInformationProvider()

```dart
PlatformRouteInformationProvider({required RouteInformation initialRouteInformation})
```

Create a platform route information provider.

Use the [initialRouteInformation] to set the default route information for this provider.

### routerReportsNewRouteInformation()

```dart
void routerReportsNewRouteInformation(RouteInformation routeInformation, {RouteInformationReportingType type = RouteInformationReportingType.none})
```

### value

```dart
RouteInformation get value
```

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### dispose()

```dart
void dispose()
```

### didPushRouteInformation()

```dart
Future<bool> didPushRouteInformation(RouteInformation routeInformation)
```

# PopNavigatorRouterDelegateMixin

```dart
mixin PopNavigatorRouterDelegateMixin<T> on RouterDelegate<T> {}
```

A mixin that wires [RouterDelegate.popRoute] to the [Navigator] it builds.

This mixin calls [Navigator.maybePop] when it receives an Android back button intent through the [RouterDelegate.popRoute]. Using this mixin guarantees that the back button still respects pageless routes in the navigator.

Only use this mixin if you plan to build a navigator in the [RouterDelegate.build].

### navigatorKey

```dart
GlobalKey<NavigatorState>? get navigatorKey
```

The key used for retrieving the current navigator.

When using this mixin, be sure to use this key to create the navigator.

### popRoute()

```dart
Future<bool> popRoute()
```
