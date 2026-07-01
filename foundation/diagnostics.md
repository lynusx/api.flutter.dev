@docImport 'dart:developer';

@docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/widgets.dart';

# DiagnosticLevel

```dart
enum DiagnosticLevel {}
```

The various priority levels used to filter which diagnostics are shown and omitted.

Trees of Flutter diagnostics can be very large so filtering the diagnostics shown matters. Typically filtering to only show diagnostics with at least level [debug] is appropriate.

In release mode, this level may not have any effect, as diagnostics in release mode are compacted or truncated to reduce binary size.

Diagnostics that should not be shown.

If a user chooses to display [hidden] diagnostics, they should not expect the diagnostics to be formatted consistently with other diagnostics and they should expect them to sometimes be misleading. For example, [FlagProperty] and [ObjectFlagProperty] have uglier formatting when the property `value` does not match a value with a custom flag description. An example of a misleading diagnostic is a diagnostic for a property that has no effect because some other property of the object is set in a way that causes the hidden property to have no effect.

A diagnostic that is likely to be low value but where the diagnostic display is just as high quality as a diagnostic with a higher level.

Use this level for diagnostic properties that match their default value and other cases where showing a diagnostic would not add much value such as an [IterableProperty] where the value is empty.

Diagnostics that should only be shown when performing fine grained debugging of an object.

Unlike a [fine] diagnostic, these diagnostics provide important information about the object that is likely to be needed to debug. Used by properties that are important but where the property value is too verbose (e.g. 300+ characters long) to show with a higher diagnostic level.

Interesting diagnostics that should be typically shown.

Very important diagnostics that indicate problematic property values.

For example, use if you would write the property description message in ALL CAPS.

Diagnostics that provide a hint about best practices.

For example, a diagnostic describing best practices for fixing an error.

Diagnostics that summarize other diagnostics present.

For example, use this level for a short one or two line summary describing other diagnostics present.

Diagnostics that indicate errors or unexpected conditions.

For example, use for property values where computing the value throws an exception.

Special level indicating that no diagnostics should be shown.

Do not specify this level for diagnostics. This level is only used to filter which diagnostics are shown.

# DiagnosticsTreeStyle

```dart
enum DiagnosticsTreeStyle {}
```

Styles for displaying a node in a [DiagnosticsNode] tree.

In release mode, these styles may be ignored, as diagnostics are compacted or truncated to save on binary size.

See also:

- [DiagnosticsNode.toStringDeep], which dumps text art trees for these styles.

A style that does not display the tree, for release mode.

Sparse style for displaying trees.

See also:

- [RenderObject], which uses this style.

Connects a node to its parent with a dashed line.

See also:

- [RenderSliverMultiBoxAdaptor], which uses this style to distinguish offstage children from onstage children.

Slightly more compact version of the [sparse] style.

See also:

- [Element], which uses this style.

Style that enables transitioning from nodes of one style to children of another.

See also:

- [RenderParagraph], which uses this style to display a [TextSpan] child in a way that is compatible with the [DiagnosticsTreeStyle.sparse] style of the [RenderObject] tree.

Style for displaying content describing an error.

See also:

- [FlutterError], which uses this style for the root node in a tree describing an error.

Render the tree just using whitespace without connecting parents to children using lines.

See also:

- [SliverGeometry], which uses this style.

Render the tree without indenting children at all.

See also:

- [DiagnosticsStackTrace], which uses this style.

Render the tree on a single line without showing children.

Render the tree using a style appropriate for properties that are part of an error message.

The name is placed on one line with the value and properties placed on the following line.

See also:

- [singleLine], which displays the same information but keeps the property and value on the same line.

Render only the immediate properties of a node instead of the full tree.

See also:

- [DebugOverflowIndicatorMixin], which uses this style to display just the immediate children of a node.

Render only the children of a node truncating before the tree becomes too large.

# TextTreeConfiguration

```dart
class TextTreeConfiguration {}
```

Configuration specifying how a particular [DiagnosticsTreeStyle] should be rendered as text art.

In release mode, these configurations may be ignored, as diagnostics are compacted or truncated to save on binary size.

See also:

- [sparseTextConfiguration], which is a typical style.
- [transitionTextConfiguration], which is an example of a complex tree style.
- [DiagnosticsNode.toStringDeep], for code using [TextTreeConfiguration] to render text art for arbitrary trees of [DiagnosticsNode] objects.

### TextTreeConfiguration()

```dart
TextTreeConfiguration({required String prefixLineOne, required String prefixOtherLines, required String prefixLastChildLineOne, required String prefixOtherLinesRootNode, required String linkCharacter, required String propertyPrefixIfChildren, required String propertyPrefixNoChildren, String lineBreak = '\n', bool lineBreakProperties = true, String afterName = ':', String afterDescriptionIfBody = '', String afterDescription = '', String beforeProperties = '', String afterProperties = '', String mandatoryAfterProperties = '', String propertySeparator = '', String bodyIndent = '', String footer = '', bool showChildren = true, bool addBlankLineIfNoChildren = true, bool isNameOnOwnLine = false, bool isBlankLineBetweenPropertiesAndChildren = true, String beforeName = '', String suffixLineOne = '', String mandatoryFooter = ''})
```

Create a configuration object describing how to render a tree as text.

### prefixLineOne

```dart
String prefixLineOne
```

Prefix to add to the first line to display a child with this style.

### suffixLineOne

```dart
String suffixLineOne
```

Suffix to add to end of the first line to make its length match the footer.

### prefixOtherLines

```dart
String prefixOtherLines
```

Prefix to add to other lines to display a child with this style.

[prefixOtherLines] should typically be one character shorter than [prefixLineOne] is.

### prefixLastChildLineOne

```dart
String prefixLastChildLineOne
```

Prefix to add to the first line to display the last child of a node with this style.

### prefixOtherLinesRootNode

```dart
String prefixOtherLinesRootNode
```

Additional prefix to add to other lines of a node if this is the root node of the tree.

### propertyPrefixIfChildren

```dart
String propertyPrefixIfChildren
```

Prefix to add before each property if the node as children.

Plays a similar role to [linkCharacter] except that some configurations intentionally use a different line style than the [linkCharacter].

### propertyPrefixNoChildren

```dart
String propertyPrefixNoChildren
```

Prefix to add before each property if the node does not have children.

This string is typically a whitespace string the same length as [propertyPrefixIfChildren] but can have a different length.

### linkCharacter

```dart
String linkCharacter
```

Character to use to draw line linking parent to child.

The first child does not require a line but all subsequent children do with the line drawn immediately before the left edge of the previous sibling.

### childLinkSpace

```dart
String childLinkSpace
```

Whitespace to draw instead of the childLink character if this node is the last child of its parent so no link line is required.

### lineBreak

```dart
String lineBreak
```

Character(s) to use to separate lines.

Typically leave set at the default value of '\n' unless this style needs to treat lines differently as is the case for [singleLineTextConfiguration].

### lineBreakProperties

```dart
bool lineBreakProperties
```

Whether to place line breaks between properties or to leave all properties on one line.

### beforeName

```dart
String beforeName
```

Text added immediately before the name of the node.

See [errorTextConfiguration] for an example of using this to achieve a custom line art style.

### afterName

```dart
String afterName
```

Text added immediately after the name of the node.

See [transitionTextConfiguration] for an example of using a value other than ':' to achieve a custom line art style.

### afterDescriptionIfBody

```dart
String afterDescriptionIfBody
```

Text to add immediately after the description line of a node with properties and/or children if the node has a body.

### afterDescription

```dart
String afterDescription
```

Text to add immediately after the description line of a node with properties and/or children.

### beforeProperties

```dart
String beforeProperties
```

Optional string to add before the properties of a node.

Only displayed if the node has properties. See [singleLineTextConfiguration] for an example of using this field to enclose the property list with parenthesis.

### afterProperties

```dart
String afterProperties
```

Optional string to add after the properties of a node.

See documentation for [beforeProperties].

### mandatoryAfterProperties

```dart
String mandatoryAfterProperties
```

Mandatory string to add after the properties of a node regardless of whether the node has any properties.

### propertySeparator

```dart
String propertySeparator
```

Property separator to add between properties.

See [singleLineTextConfiguration] for an example of using this field to render properties as a comma separated list.

### bodyIndent

```dart
String bodyIndent
```

Prefix to add to all lines of the body of the tree node.

The body is all content in the node other than the name and description.

### showChildren

```dart
bool showChildren
```

Whether the children of a node should be shown.

See [singleLineTextConfiguration] for an example of using this field to hide all children of a node.

### addBlankLineIfNoChildren

```dart
bool addBlankLineIfNoChildren
```

Whether to add a blank line at the end of the output for a node if it has no children.

See [denseTextConfiguration] for an example of setting this to false.

### isNameOnOwnLine

```dart
bool isNameOnOwnLine
```

Whether the name should be displayed on the same line as the description.

### footer

```dart
String footer
```

Footer to add as its own line at the end of a non-root node.

See [transitionTextConfiguration] for an example of using footer to draw a box around the node. [footer] is indented the same amount as [prefixOtherLines].

### mandatoryFooter

```dart
String mandatoryFooter
```

Footer to add even for root nodes.

### isBlankLineBetweenPropertiesAndChildren

```dart
bool isBlankLineBetweenPropertiesAndChildren
```

Add a blank line between properties and children if both are present.

# sparseTextConfiguration

```dart
TextTreeConfiguration sparseTextConfiguration
```

Default text tree configuration.

Example:

<root_name>: <root_description> │ <property1> │ <property2> │ ... │ <propertyN> ├─<child_name>: <child_description> │ │ <property1> │ │ <property2> │ │ ... │ │ <propertyN> │ │ │ └─<child_name>: <child_description> │ <property1> │ <property2> │ ... │ <propertyN> │ └─<child_name>: <child_description>' <property1> <property2> ... <propertyN>

See also:

- [DiagnosticsTreeStyle.sparse], uses this style for ASCII art display.

# dashedTextConfiguration

```dart
TextTreeConfiguration dashedTextConfiguration
```

Identical to [sparseTextConfiguration] except that the lines connecting parent to children are dashed.

Example:

<root_name>: <root_description> │ <property1> │ <property2> │ ... │ <propertyN> ├─<normal_child_name>: <child_description> ╎ │ <property1> ╎ │ <property2> ╎ │ ... ╎ │ <propertyN> ╎ │ ╎ └─<child_name>: <child_description> ╎ <property1> ╎ <property2> ╎ ... ╎ <propertyN> ╎ ╎╌<dashed_child_name>: <child_description> ╎ │ <property1> ╎ │ <property2> ╎ │ ... ╎ │ <propertyN> ╎ │ ╎ └─<child_name>: <child_description> ╎ <property1> ╎ <property2> ╎ ... ╎ <propertyN> ╎ └╌<dashed_child_name>: <child_description>' <property1> <property2> ... <propertyN>

See also:

- [DiagnosticsTreeStyle.offstage], uses this style for ASCII art display.

# denseTextConfiguration

```dart
TextTreeConfiguration denseTextConfiguration
```

Dense text tree configuration that minimizes horizontal whitespace.

Example:

<root_name>: <root_description>(<property1>; <property2> <propertyN>) ├<child_name>: <child_description>(<property1>, <property2>, <propertyN>) └<child_name>: <child_description>(<property1>, <property2>, <propertyN>)

See also:

- [DiagnosticsTreeStyle.dense], uses this style for ASCII art display.

# transitionTextConfiguration

```dart
TextTreeConfiguration transitionTextConfiguration
```

Configuration that draws a box around a leaf node.

Used by leaf nodes such as [TextSpan] to draw a clear border around the contents of a node.

Example:

<parent_node> ╞═╦══ <name> ═══ │ ║ <description>: │ ║ <body> │ ║ ... │ ╚═══════════ ╘═╦══ <name> ═══ ║ <description>: ║ <body> ║ ... ╚═══════════

See also:

- [DiagnosticsTreeStyle.transition], uses this style for ASCII art display.

# errorTextConfiguration

```dart
TextTreeConfiguration errorTextConfiguration
```

Configuration that draws a box around a node ignoring the connection to the parents.

If nested in a tree, this node is best displayed in the property box rather than as a traditional child.

Used to draw a decorative box around detailed descriptions of an exception.

Example:

══╡ <name>: <description> ╞═════════════════════════════════════ <body> ... ├─<normal_child_name>: <child_description> ╎ │ <property1> ╎ │ <property2> ╎ │ ... ╎ │ <propertyN> ╎ │ ╎ └─<child_name>: <child_description> ╎ <property1> ╎ <property2> ╎ ... ╎ <propertyN> ╎ ╎╌<dashed_child_name>: <child_description> ╎ │ <property1> ╎ │ <property2> ╎ │ ... ╎ │ <propertyN> ╎ │ ╎ └─<child_name>: <child_description> ╎ <property1> ╎ <property2> ╎ ... ╎ <propertyN> ╎ └╌<dashed_child_name>: <child_description>' ════════════════════════════════════════════════════════════════

See also:

- [DiagnosticsTreeStyle.error], uses this style for ASCII art display.

# whitespaceTextConfiguration

```dart
TextTreeConfiguration whitespaceTextConfiguration
```

Whitespace only configuration where children are consistently indented two spaces.

Use this style for displaying properties with structured values or for displaying children within a [transitionTextConfiguration] as using a style that draws line art would be visually distracting for those cases.

Example:

<parent_node> <name>: <description>: <properties> <children> <name>: <description>: <properties> <children>

See also:

- [DiagnosticsTreeStyle.whitespace], uses this style for ASCII art display.

# flatTextConfiguration

```dart
TextTreeConfiguration flatTextConfiguration
```

Whitespace only configuration where children are not indented.

Use this style when indentation is not needed to disambiguate parents from children as in the case of a [DiagnosticsStackTrace].

Example:

<parent_node> <name>: <description>: <properties> <children> <name>: <description>: <properties> <children>

See also:

- [DiagnosticsTreeStyle.flat], uses this style for ASCII art display.

# singleLineTextConfiguration

```dart
TextTreeConfiguration singleLineTextConfiguration
```

Render a node as a single line omitting children.

Example: `<name>: <description>(<property1>, <property2>, ..., <propertyN>)`

See also:

- [DiagnosticsTreeStyle.singleLine], uses this style for ASCII art display.

# errorPropertyTextConfiguration

```dart
TextTreeConfiguration errorPropertyTextConfiguration
```

Render the name on a line followed by the body and properties on the next line omitting the children.

Example:

<name>: <description>(<property1>, <property2>, ..., <propertyN>)

See also:

- [DiagnosticsTreeStyle.errorProperty], uses this style for ASCII art display.

# shallowTextConfiguration

```dart
TextTreeConfiguration shallowTextConfiguration
```

Render a node on multiple lines omitting children.

Example: `<name>: <description> <property1> <property2> <propertyN>`

See also:

- [DiagnosticsTreeStyle.shallow]

# kNoDefaultValue

```dart
Object kNoDefaultValue
```

Marker object indicating that a [DiagnosticsNode] has no default value.

# TextTreeRenderer

```dart
class TextTreeRenderer {}
```

Renderer that creates ASCII art representations of trees of [DiagnosticsNode] objects.

See also:

- [DiagnosticsNode.toStringDeep], which uses a [TextTreeRenderer] to return a string representation of this node and its descendants.

### TextTreeRenderer()

```dart
TextTreeRenderer({DiagnosticLevel minLevel = DiagnosticLevel.debug, int wrapWidth = 100, int wrapWidthProperties = 65, int maxDescendentsTruncatableNode = -1})
```

Creates a [TextTreeRenderer] object with the given arguments specifying how the tree is rendered.

Lines are wrapped to at the maximum of [wrapWidth] and the current indent plus [wrapWidthProperties] characters. This ensures that wrapping does not become too excessive when displaying very deep trees and that wrapping only occurs at the overall [wrapWidth] when the tree is not very indented. If [maxDescendentsTruncatableNode] is specified, [DiagnosticsNode] objects with `allowTruncate` set to `true` are truncated after including [maxDescendentsTruncatableNode] descendants of the node to be truncated.

### render()

```dart
String render(DiagnosticsNode node, {String prefixLineOne = '', String? prefixOtherLines, TextTreeConfiguration? parentConfiguration})
```

Renders a [node] to a String.

# DiagnosticsNode

```dart
abstract class DiagnosticsNode {}
```

Defines diagnostics data for a [value].

For debug and profile modes, [DiagnosticsNode] provides a high quality multiline string dump via [toStringDeep]. The core members are the [name], [toDescription], [getProperties], [value], and [getChildren]. All other members exist typically to provide hints for how [toStringDeep] and debugging tools should format output.

In release mode, far less information is retained and some information may not print at all.

### DiagnosticsNode()

```dart
DiagnosticsNode({required String? name, DiagnosticsTreeStyle? style, bool showName = true, bool showSeparator = true, String? linePrefix})
```

Initializes the object.

The [style], [showName], and [showSeparator] arguments must not be null.

### DiagnosticsNode.message()

```dart
DiagnosticsNode.message(String message, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.singleLine, DiagnosticLevel level = DiagnosticLevel.info, bool allowWrap = true})
```

Diagnostics containing just a string `message` and not a concrete name or value.

See also:

- [MessageProperty], which is better suited to messages that are to be formatted like a property with a separate name and message.

### name

```dart
String? name
```

Label describing the [DiagnosticsNode], typically shown before a separator (see [showSeparator]).

The name will be omitted if the [showName] property is false.

### toDescription()

```dart
String toDescription({TextTreeConfiguration? parentConfiguration})
```

Returns a description with a short summary of the node itself not including children or properties.

`parentConfiguration` specifies how the parent is rendered as text art. For example, if the parent does not line break between properties, the description of a property should also be a single line if possible.

### showSeparator

```dart
bool showSeparator
```

Whether to show a separator between [name] and description.

If false, name and description should be shown with no separation. `:` is typically used as a separator when displaying as text.

### isFiltered()

```dart
bool isFiltered(DiagnosticLevel minLevel)
```

Whether the diagnostic should be filtered due to its [level] being lower than `minLevel`.

If `minLevel` is [DiagnosticLevel.hidden] no diagnostics will be filtered. If `minLevel` is [DiagnosticLevel.off] all diagnostics will be filtered.

### level

```dart
DiagnosticLevel get level
```

Priority level of the diagnostic used to control which diagnostics should be shown and filtered.

Typically this only makes sense to set to a different value than [DiagnosticLevel.info] for diagnostics representing properties. Some subclasses have a [level] argument to their constructor which influences the value returned here but other factors also influence it. For example, whether an exception is thrown computing a property value [DiagnosticLevel.error] is returned.

### showName

```dart
bool showName
```

Whether the name of the property should be shown when showing the default view of the tree.

This could be set to false (hiding the name) if the value's description will make the name self-evident.

### linePrefix

```dart
String? linePrefix
```

Prefix to include at the start of each line.

### emptyBodyDescription

```dart
String? get emptyBodyDescription
```

Description to show if the node has no displayed properties or children.

### value

```dart
Object? get value
```

The actual object this is diagnostics data for.

### style

```dart
DiagnosticsTreeStyle? style
```

Hint for how the node should be displayed.

### allowWrap

```dart
bool get allowWrap
```

Whether to wrap text on onto multiple lines or not.

### allowNameWrap

```dart
bool get allowNameWrap
```

Whether to wrap the name onto multiple lines or not.

### allowTruncate

```dart
bool get allowTruncate
```

Whether to allow truncation when displaying the node and its children.

### getProperties()

```dart
List<DiagnosticsNode> getProperties()
```

Properties of this [DiagnosticsNode].

Properties and children are kept distinct even though they are both [List<DiagnosticsNode>] because they should be grouped differently.

### getChildren()

```dart
List<DiagnosticsNode> getChildren()
```

Children of this [DiagnosticsNode].

See also:

- [getProperties], which returns the properties of the [DiagnosticsNode] object.

### toTimelineArguments()

```dart
Map<String, String>? toTimelineArguments()
```

Converts the properties ([getProperties]) of this node to a form useful for [Timeline] event arguments (as in [Timeline.startSync]).

Children ([getChildren]) are omitted.

This method is only valid in debug builds. In profile builds, this method throws an exception. In release builds it returns null.

See also:

- [toJsonMap], which converts this node to a structured form intended for data exchange (e.g. with an IDE).

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

Serialize the node to a JSON map according to the configuration provided in the [DiagnosticsSerializationDelegate].

Subclasses should override if they have additional properties that are useful for the GUI tools that consume this JSON.

See also:

- [WidgetInspectorService], which forms the bridge between JSON returned by this method and interactive tree views in the Flutter IntelliJ plugin.

### toJsonMapIterative()

```dart
Map<String, Object?> toJsonMapIterative(DiagnosticsSerializationDelegate delegate)
```

Iteratively serialize the node to a JSON map according to the configuration provided in the [DiagnosticsSerializationDelegate].

This is only used when [WidgetInspectorServiceExtensions.getRootWidgetTree] is called with fullDetails=false. To get the full widget details, including any details provided by subclasses, [toJsonMap] should be used instead.

See https://github.com/flutter/devtools/issues/8553 for details about this iterative approach.

### toJsonList()

```dart
List<Map<String, Object?>> toJsonList(List<DiagnosticsNode>? nodes, DiagnosticsNode? parent, DiagnosticsSerializationDelegate delegate)
```

Serializes a [List] of [DiagnosticsNode]s to a JSON list according to the configuration provided by the [DiagnosticsSerializationDelegate].

The provided `nodes` may be properties or children of the `parent` [DiagnosticsNode].

### toString()

```dart
String toString({TextTreeConfiguration? parentConfiguration, DiagnosticLevel minLevel = DiagnosticLevel.info})
```

Returns a string representation of this diagnostic that is compatible with the style of the parent if the node is not the root.

`parentConfiguration` specifies how the parent is rendered as text art. For example, if the parent places all properties on one line, the [toString] for each property should avoid line breaks if possible.

`minLevel` specifies the minimum [DiagnosticLevel] for properties included in the output.

In release mode, far less information is retained and some information may not print at all.

### textTreeConfiguration

```dart
TextTreeConfiguration? get textTreeConfiguration
```

Returns a configuration specifying how this object should be rendered as text art.

### toStringDeep()

```dart
String toStringDeep({String prefixLineOne = '', String? prefixOtherLines, TextTreeConfiguration? parentConfiguration, DiagnosticLevel minLevel = DiagnosticLevel.debug, int wrapWidth = 65})
```

Returns a string representation of this node and its descendants.

`prefixLineOne` will be added to the front of the first line of the output. `prefixOtherLines` will be added to the front of each other line. If `prefixOtherLines` is null, the `prefixLineOne` is used for every line. By default, there is no prefix.

`minLevel` specifies the minimum [DiagnosticLevel] for properties included in the output.

`wrapWidth` specifies the column number where word wrapping will be applied.

The [toStringDeep] method takes other arguments, but those are intended for internal use when recursing to the descendants, and so can be ignored.

In release mode, far less information is retained and some information may not print at all.

See also:

- [toString], for a brief description of the [value] but not its children.

# MessageProperty

```dart
class MessageProperty extends DiagnosticsProperty<void> {}
```

Debugging message displayed like a property.

{@tool snippet}

The following two properties are better expressed using this [MessageProperty] class, rather than [StringProperty], as the intent is to show a message with property style display rather than to describe the value of an actual property of the object:

```dart
MessageProperty table = MessageProperty('table size', '$columns\u00D7$rows');
MessageProperty usefulness = MessageProperty('usefulness ratio', 'no metrics collected yet (never painted)');
```

{@end-tool} {@tool snippet}

On the other hand, [StringProperty] is better suited when the property has a concrete value that is a string:

```dart
StringProperty name = StringProperty('name', _name);
```

{@end-tool}

See also:

- [DiagnosticsNode.message], which serves the same role for messages without a clear property name.
- [StringProperty], which is a better fit for properties with string values.

### MessageProperty()

```dart
MessageProperty(String name, String message, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.singleLine, DiagnosticLevel level = DiagnosticLevel.info})
```

Create a diagnostics property that displays a message.

Messages have no concrete [value] (so [value] will return null). The message is stored as the description.

# StringProperty

```dart
class StringProperty extends DiagnosticsProperty<String> {}
```

Property which encloses its string [value] in quotes.

See also:

- [MessageProperty], which is a better fit for showing a message instead of describing a property with a string value.

### StringProperty()

```dart
StringProperty(String name, String? value, {String? description, String? tooltip, bool showName, Object? defaultValue, bool quoted = true, String? ifEmpty, DiagnosticsTreeStyle style, DiagnosticLevel level})
```

Create a diagnostics property for strings.

### quoted

```dart
bool quoted
```

Whether the value is enclosed in double quotes.

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

# DoubleProperty

```dart
class DoubleProperty extends _NumProperty<double> {}
```

Property describing a [double] [value] with an optional [unit] of measurement.

Numeric formatting is optimized for debug message readability.

### DoubleProperty()

```dart
DoubleProperty(String name, double? value, {String? ifNull, String? unit, String? tooltip, Object? defaultValue, bool showName, DiagnosticsTreeStyle style, DiagnosticLevel level})
```

If specified, [unit] describes the unit for the [value] (e.g. px).

### DoubleProperty.lazy()

```dart
DoubleProperty.lazy(String name, double? Function() computeValue, {String? ifNull, bool showName, String? unit, String? tooltip, Object? defaultValue, DiagnosticLevel level})
```

Property with a [value] that is computed only when needed.

Use if computing the property [value] may throw an exception or is expensive.

### numberToString()

```dart
String numberToString()
```

# IntProperty

```dart
class IntProperty extends _NumProperty<int> {}
```

An int valued property with an optional unit the value is measured in.

Examples of units include 'px' and 'ms'.

### IntProperty()

```dart
IntProperty(String name, int? value, {String? ifNull, bool showName, String? unit, Object? defaultValue, DiagnosticsTreeStyle style, DiagnosticLevel level})
```

Create a diagnostics property for integers.

### numberToString()

```dart
String numberToString()
```

# PercentProperty

```dart
class PercentProperty extends DoubleProperty {}
```

Property which clamps a [double] to between 0 and 1 and formats it as a percentage.

### PercentProperty()

```dart
PercentProperty(String name, double? fraction, {String? ifNull, bool showName, String? tooltip, String? unit, DiagnosticLevel level})
```

Create a diagnostics property for doubles that represent percentages or fractions.

Setting [showName] to false is often reasonable for [PercentProperty] objects, as the fact that the property is shown as a percentage tends to be sufficient to disambiguate its meaning.

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

### numberToString()

```dart
String numberToString()
```

# FlagProperty

```dart
class FlagProperty extends DiagnosticsProperty<bool> {}
```

Property where the description is either [ifTrue] or [ifFalse] depending on whether [value] is true or false.

Using [FlagProperty] instead of [DiagnosticsProperty<bool>] can make diagnostics display more polished. For example, given a property named `visible` that is typically true, the following code will return 'hidden' when `visible` is false and nothing when visible is true, in contrast to `visible: true` or `visible: false`.

{@tool snippet}

```dart
FlagProperty(
  'visible',
  value: true,
  ifFalse: 'hidden',
)
```

{@end-tool} {@tool snippet}

[FlagProperty] should also be used instead of [DiagnosticsProperty<bool>] if showing the bool value would not clearly indicate the meaning of the property value.

```dart
FlagProperty(
  'inherit',
  value: inherit,
  ifTrue: '<all styles inherited>',
  ifFalse: '<no style specified>',
)
```

{@end-tool}

See also:

- [ObjectFlagProperty], which provides similar behavior describing whether a [value] is null.

### FlagProperty()

```dart
FlagProperty(String name, {required bool? value, String? ifTrue, String? ifFalse, bool showName = false, Object? defaultValue, DiagnosticLevel level = DiagnosticLevel.info})
```

Constructs a FlagProperty with the given descriptions with the specified descriptions.

[showName] defaults to false as typically [ifTrue] and [ifFalse] should be descriptions that make the property name redundant.

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

### ifTrue

```dart
String? ifTrue
```

Description to use if the property [value] is true.

If not specified and [value] equals true the property's priority [level] will be [DiagnosticLevel.hidden].

### ifFalse

```dart
String? ifFalse
```

Description to use if the property value is false.

If not specified and [value] equals false, the property's priority [level] will be [DiagnosticLevel.hidden].

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

### showName

```dart
bool get showName
```

### level

```dart
DiagnosticLevel get level
```

# IterableProperty

```dart
class IterableProperty<T> extends DiagnosticsProperty<Iterable<T>> {}
```

Property with an `Iterable<T>` [value] that can be displayed with different [DiagnosticsTreeStyle] for custom rendering.

If [style] is [DiagnosticsTreeStyle.singleLine], the iterable is described as a comma separated list, otherwise the iterable is described as a line break separated list.

### IterableProperty()

```dart
IterableProperty(String name, Iterable<T>? value, {Object? defaultValue, String? ifNull, String? ifEmpty = '[]', DiagnosticsTreeStyle style, bool showName, bool showSeparator, DiagnosticLevel level})
```

Create a diagnostics property for iterables (e.g. lists).

The [ifEmpty] argument is used to indicate how an iterable [value] with 0 elements is displayed. If [ifEmpty] equals null that indicates that an empty iterable [value] is not interesting to display similar to how [defaultValue] is used to indicate that a specific concrete value is not interesting to display.

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

### level

```dart
DiagnosticLevel get level
```

Priority level of the diagnostic used to control which diagnostics should be shown and filtered.

If [ifEmpty] is null and the [value] is an empty [Iterable] then level [DiagnosticLevel.fine] is returned in a similar way to how an [ObjectFlagProperty] handles when [ifNull] is null and the [value] is null.

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

# EnumProperty

```dart
class EnumProperty<T extends Enum?> extends DiagnosticsProperty<T> {}
```

[DiagnosticsProperty] that has an [Enum] as value.

The enum value is displayed with the enum name stripped. For example: [HitTestBehavior.deferToChild] is shown as `deferToChild`.

This class can be used with enums and returns the enum's name getter. It can also be used with nullable properties; the null value is represented as `null`.

See also:

- [DiagnosticsProperty] which documents named parameters common to all [DiagnosticsProperty].

### EnumProperty()

```dart
EnumProperty(String name, T? value, {Object? defaultValue, DiagnosticLevel level})
```

Create a diagnostics property that displays an enum.

The [level] argument must also not be null.

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

# ObjectFlagProperty

```dart
class ObjectFlagProperty<T> extends DiagnosticsProperty<T> {}
```

A property where the important diagnostic information is primarily whether the [value] is present (non-null) or absent (null), rather than the actual value of the property itself.

The [ifPresent] and [ifNull] strings describe the property [value] when it is non-null and null respectively. If one of [ifPresent] or [ifNull] is omitted, that is taken to mean that [level] should be [DiagnosticLevel.hidden] when [value] is non-null or null respectively.

This kind of diagnostics property is typically used for opaque values, like closures, where presenting the actual object is of dubious value but where reporting the presence or absence of the value is much more useful.

See also:

- [FlagsSummary], which provides similar functionality but accepts multiple flags under the same name, and is preferred if there are multiple such values that can fit into a same category (such as "listeners").
- [FlagProperty], which provides similar functionality describing whether a [value] is true or false.

### ObjectFlagProperty()

```dart
ObjectFlagProperty(String name, T? value, {String? ifPresent, String? ifNull, bool showName = false, DiagnosticLevel level})
```

Create a diagnostics property for values that can be present (non-null) or absent (null), but for which the exact value's [Object.toString] representation is not very transparent (e.g. a callback).

At least one of [ifPresent] or [ifNull] must be non-null.

### ObjectFlagProperty.has()

```dart
ObjectFlagProperty.has(String name, T? value, {DiagnosticLevel level})
```

Shorthand constructor to describe whether the property has a value.

Only use if prefixing the property name with the word 'has' is a good flag name.

### ifPresent

```dart
String? ifPresent
```

Description to use if the property [value] is not null.

If the property [value] is not null and [ifPresent] is null, the [level] for the property is [DiagnosticLevel.hidden] and the description from superclass is used.

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

### showName

```dart
bool get showName
```

### level

```dart
DiagnosticLevel get level
```

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

# FlagsSummary

```dart
class FlagsSummary<T> extends DiagnosticsProperty<Map<String, T?>> {}
```

A summary of multiple properties, indicating whether each of them is present (non-null) or absent (null).

Each entry of [value] is described by its key. The eventual description will be a list of keys of non-null entries.

The [ifEmpty] describes the entire collection of [value] when it contains no non-null entries. If [ifEmpty] is omitted, [level] will be [DiagnosticLevel.hidden] when [value] contains no non-null entries.

This kind of diagnostics property is typically used for opaque values, like closures, where presenting the actual object is of dubious value but where reporting the presence or absence of the value is much more useful.

See also:

- [ObjectFlagProperty], which provides similar functionality but accepts only one flag, and is preferred if there is only one entry.
- [IterableProperty], which provides similar functionality describing the values a collection of objects.

### FlagsSummary()

```dart
FlagsSummary(String name, Map<String, T?> value, {String? ifEmpty, bool showName, bool showSeparator, DiagnosticLevel level})
```

Create a summary for multiple properties, indicating whether each of them is present (non-null) or absent (null).

The [value], [showName], [showSeparator] and [level] arguments must not be null.

### value

```dart
Map<String, T?> get value
```

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

### level

```dart
DiagnosticLevel get level
```

Priority level of the diagnostic used to control which diagnostics should be shown and filtered.

If [ifEmpty] is null and the [value] contains no non-null entries, then level [DiagnosticLevel.hidden] is returned.

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

# ComputePropertyValueCallback

```dart
typedef ComputePropertyValueCallback<T> = T? Function()
```

Signature for computing the value of a property.

May throw exception if accessing the property would throw an exception and callers must handle that case gracefully. For example, accessing a property may trigger an assert that layout constraints were violated.

# DiagnosticsProperty

```dart
class DiagnosticsProperty<T> extends DiagnosticsNode {}
```

Property with a [value] of type [T].

If the default `value.toString()` does not provide an adequate description of the value, specify `description` defining a custom description.

The [showSeparator] property indicates whether a separator should be placed between the property [name] and its [value].

### DiagnosticsProperty()

```dart
DiagnosticsProperty(String? name, T? value, {String? description, String? ifNull, String? ifEmpty, bool showName, bool showSeparator, Object? defaultValue = kNoDefaultValue, String? tooltip, bool missingIfNull = false, String? linePrefix, bool expandableValue = false, bool allowWrap = true, bool allowNameWrap = true, DiagnosticsTreeStyle style = DiagnosticsTreeStyle.singleLine, DiagnosticLevel level = DiagnosticLevel.info})
```

Create a diagnostics property.

The [level] argument is just a suggestion and can be overridden if something else about the property causes it to have a lower or higher level. For example, if the property value is null and [missingIfNull] is true, [level] is raised to [DiagnosticLevel.warning].

### DiagnosticsProperty.lazy()

```dart
DiagnosticsProperty.lazy(String? name, ComputePropertyValueCallback<T> computeValue, {String? description, String? ifNull, String? ifEmpty, bool showName, bool showSeparator, Object? defaultValue = kNoDefaultValue, String? tooltip, bool missingIfNull = false, bool expandableValue = false, bool allowWrap = true, bool allowNameWrap = true, DiagnosticsTreeStyle style = DiagnosticsTreeStyle.singleLine, DiagnosticLevel level = DiagnosticLevel.info})
```

Property with a [value] that is computed only when needed.

Use if computing the property [value] may throw an exception or is expensive.

The [level] argument is just a suggestion and can be overridden if something else about the property causes it to have a lower or higher level. For example, if calling `computeValue` throws an exception, [level] will always return [DiagnosticLevel.error].

### expandableValue

```dart
bool expandableValue
```

Whether to expose properties and children of the value as properties and children.

### allowWrap

```dart
bool allowWrap
```

### allowNameWrap

```dart
bool allowNameWrap
```

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

Returns a string representation of the property value.

Subclasses should override this method instead of [toDescription] to customize how property values are converted to strings.

Overriding this method ensures that behavior controlling how property values are decorated to generate a nice [toDescription] are consistent across all implementations. Debugging tools may also choose to use [valueToString] directly instead of [toDescription].

`parentConfiguration` specifies how the parent is rendered as text art. For example, if the parent places all properties on one line, the value of the property should be displayed without line breaks if possible.

### toDescription()

```dart
String toDescription({TextTreeConfiguration? parentConfiguration})
```

### ifNull

```dart
String? ifNull
```

Description if the property [value] is null.

### ifEmpty

```dart
String? ifEmpty
```

Description if the property description would otherwise be empty.

### tooltip

```dart
String? tooltip
```

Optional tooltip typically describing the property.

Example tooltip: 'physical pixels per logical pixel'

If present, the tooltip is added in parenthesis after the raw value when generating the string description.

### missingIfNull

```dart
bool missingIfNull
```

Whether a [value] of null causes the property to have [level] [DiagnosticLevel.warning] warning that the property is missing a [value].

### propertyType

```dart
Type get propertyType
```

The type of the property [value].

This is determined from the type argument `T` used to instantiate the [DiagnosticsProperty] class. This means that the type is available even if [value] is null, but it also means that the [propertyType] is only as accurate as the type provided when invoking the constructor.

Generally, this is only useful for diagnostic tools that should display null values in a manner consistent with the property type. For example, a tool might display a null [Color] value as an empty rectangle instead of the word "null".

### value

```dart
T? get value
```

Returns the value of the property either from cache or by invoking a [ComputePropertyValueCallback].

If an exception is thrown invoking the [ComputePropertyValueCallback], [value] returns null and the exception thrown can be found via the [exception] property.

See also:

- [valueToString], which converts the property value to a string.

### exception

```dart
Object? get exception
```

Exception thrown if accessing the property [value] threw an exception.

Returns null if computing the property value did not throw an exception.

### defaultValue

```dart
Object? defaultValue
```

The default value of this property, when it has not been set to a specific value.

For most [DiagnosticsProperty] classes, if the [value] of the property equals [defaultValue], then the priority [level] of the property is downgraded to [DiagnosticLevel.fine] on the basis that the property value is uninteresting. This is implemented by [isInteresting].

The [defaultValue] is [kNoDefaultValue] by default. Otherwise it must be of type `T?`.

### isInteresting

```dart
bool get isInteresting
```

Whether to consider the property's value interesting. When a property is uninteresting, its [level] is downgraded to [DiagnosticLevel.fine] regardless of the value provided as the constructor's `level` argument.

### level

```dart
DiagnosticLevel get level
```

Priority level of the diagnostic used to control which diagnostics should be shown and filtered.

The property level defaults to the value specified by the [level] constructor argument. The level is raised to [DiagnosticLevel.error] if an [exception] was thrown getting the property [value]. The level is raised to [DiagnosticLevel.warning] if the property [value] is null and the property is not allowed to be null due to [missingIfNull]. The priority level is lowered to [DiagnosticLevel.fine] if the property [value] equals [defaultValue].

### getProperties()

```dart
List<DiagnosticsNode> getProperties()
```

### getChildren()

```dart
List<DiagnosticsNode> getChildren()
```

# DiagnosticableNode

```dart
class DiagnosticableNode<T extends Diagnosticable> extends DiagnosticsNode {}
```

[DiagnosticsNode] that lazily calls the associated [Diagnosticable] [value] to implement [getChildren] and [getProperties].

### DiagnosticableNode()

```dart
DiagnosticableNode({String? name, required T value, required DiagnosticsTreeStyle? style})
```

Create a diagnostics describing a [Diagnosticable] value.

### value

```dart
T value
```

### builder

```dart
DiagnosticPropertiesBuilder? get builder
```

Retrieve the [DiagnosticPropertiesBuilder] of current node.

It will cache the result to prevent duplicate operation.

### style

```dart
DiagnosticsTreeStyle get style
```

### emptyBodyDescription

```dart
String? get emptyBodyDescription
```

### getProperties()

```dart
List<DiagnosticsNode> getProperties()
```

### getChildren()

```dart
List<DiagnosticsNode> getChildren()
```

### toDescription()

```dart
String toDescription({TextTreeConfiguration? parentConfiguration})
```

# DiagnosticableTreeNode

```dart
class DiagnosticableTreeNode extends DiagnosticableNode<DiagnosticableTree> {}
```

[DiagnosticsNode] for an instance of [DiagnosticableTree].

### DiagnosticableTreeNode()

```dart
DiagnosticableTreeNode({String? name, required DiagnosticableTree value, required DiagnosticsTreeStyle? style})
```

Creates a [DiagnosticableTreeNode].

### getChildren()

```dart
List<DiagnosticsNode> getChildren()
```

# shortHash()

```dart
String shortHash(Object? object)
```

Returns a 5 character long hexadecimal string generated from [Object.hashCode]'s 20 least-significant bits.

# describeIdentity()

```dart
String describeIdentity(Object? object)
```

Returns a summary of the runtime type and hash code of `object`.

See also:

- [Object.hashCode], a value used when placing an object in a [Map] or other similar data structure, and which is also used in debug output to distinguish instances of the same class (hash collisions are possible, but rare enough that its use in debug output is useful).
- [Object.runtimeType], the [Type] of an object.

# describeEnum()

```dart
String describeEnum(Object enumEntry)
```

Returns a short description of an enum value.

Strips off the enum class name from the `enumEntry.toString()`.

For real enums, this is redundant with calling the `name` getter on the enum value (see [EnumName.name]), a feature that was added to Dart 2.15.

This function can also be used with classes whose `toString` return a value in the same form as an enum (the class name, a dot, then the value name). For example, it's used with [SemanticsAction], which is written to appear to be an enum but is actually a bespoke class so that the index values can be set as powers of two instead of as sequential integers.

{@tool snippet}

```dart
enum Day {
  monday, tuesday, wednesday, thursday, friday, saturday, sunday
}

void validateDescribeEnum() {
  assert(Day.monday.toString() == 'Day.monday');
  // ignore: deprecated_member_use
  assert(describeEnum(Day.monday) == 'monday');
  assert(Day.monday.name == 'monday'); // preferred for real enums
}
```

{@end-tool}

# DiagnosticPropertiesBuilder

```dart
class DiagnosticPropertiesBuilder {}
```

Builder to accumulate properties and configuration used to assemble a [DiagnosticsNode] from a [Diagnosticable] object.

### DiagnosticPropertiesBuilder()

```dart
DiagnosticPropertiesBuilder()
```

Creates a [DiagnosticPropertiesBuilder] with [properties] initialize to an empty array.

### DiagnosticPropertiesBuilder.fromProperties()

```dart
DiagnosticPropertiesBuilder.fromProperties(List<DiagnosticsNode> properties)
```

Creates a [DiagnosticPropertiesBuilder] with a given [properties].

### add()

```dart
void add(DiagnosticsNode property)
```

Add a property to the list of properties.

### properties

```dart
List<DiagnosticsNode> properties
```

List of properties accumulated so far.

### defaultDiagnosticsTreeStyle

```dart
DiagnosticsTreeStyle defaultDiagnosticsTreeStyle
```

Default style to use for the [DiagnosticsNode] if no style is specified.

### emptyBodyDescription

```dart
String? emptyBodyDescription
```

Description to show if the node has no displayed properties or children.

# Diagnosticable

```dart
mixin Diagnosticable {}
```

A mixin class for providing string and [DiagnosticsNode] debug representations describing the properties of an object.

The string debug representation is generated from the intermediate [DiagnosticsNode] representation. The [DiagnosticsNode] representation is also used by debugging tools displaying interactive trees of objects and properties.

See also:

- [debugFillProperties], which lists best practices for specifying the properties of a [DiagnosticsNode]. The most common use case is to override [debugFillProperties] defining custom properties for a subclass of [DiagnosticableTreeMixin] using the existing [DiagnosticsProperty] subclasses.
- [DiagnosticableTree], which extends this class to also describe the children of a tree structured object.
- [DiagnosticableTree.debugDescribeChildren], which lists best practices for describing the children of a [DiagnosticsNode]. Typically the base class already describes the children of a node properly or a node has no children.
- [DiagnosticsProperty], which should be used to create leaf diagnostic nodes without properties or children. There are many [DiagnosticsProperty] subclasses to handle common use cases.

### toStringShort()

```dart
String toStringShort()
```

A brief description of this object, usually just the [runtimeType] and the [hashCode].

See also:

- [toString], for a detailed description of the object.

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style})
```

Returns a debug representation of the object that is used by debugging tools and by [DiagnosticsNode.toStringDeep].

Leave [name] as null if there is not a meaningful description of the relationship between the this node and its parent.

Typically the [style] argument is only specified to indicate an atypical relationship between the parent and the node. For example, pass [DiagnosticsTreeStyle.offstage] to indicate that a node is offstage.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

Add additional properties associated with the node.

{@youtube 560 315 https://www.youtube.com/watch?v=DnC7eT-vh1k}

Use the most specific [DiagnosticsProperty] existing subclass to describe each property instead of the [DiagnosticsProperty] base class. There are only a small number of [DiagnosticsProperty] subclasses each covering a common use case. Consider what values a property is relevant for users debugging as users debugging large trees are overloaded with information. Common named parameters in [DiagnosticsNode] subclasses help filter when and how properties are displayed.

`defaultValue`, `showName`, `showSeparator`, and `level` keep string representations of diagnostics terse and hide properties when they are not very useful.

- Use `defaultValue` any time the default value of a property is uninteresting. For example, specify a default value of null any time a property being null does not indicate an error.
- Avoid specifying the `level` parameter unless the result you want cannot be achieved by using the `defaultValue` parameter or using the [ObjectFlagProperty] class to conditionally display the property as a flag.
- Specify `showName` and `showSeparator` in rare cases where the string output would look clumsy if they were not set.
  ```dart
  DiagnosticsProperty<Object>('child(3, 4)', null, ifNull: 'is null', showSeparator: false).toString()
  ```

Shows using `showSeparator` to get output `child(3, 4) is null` which is more polished than `child(3, 4): is null`.
`dart
    DiagnosticsProperty<IconData>('icon', icon, ifNull: '<empty>', showName: false).toString()
    `
Shows using `showName` to omit the property name as in this context the property name does not add useful information.

`ifNull`, `ifEmpty`, `unit`, and `tooltip` make property descriptions clearer. The examples in the code sample below illustrate good uses of all of these parameters.

## DiagnosticsProperty subclasses for primitive types

- [StringProperty], which supports automatically enclosing a [String] value in quotes.
- [DoubleProperty], which supports specifying a unit of measurement for a [double] value.
- [PercentProperty], which clamps a [double] to between 0 and 1 and formats it as a percentage.
- [IntProperty], which supports specifying a unit of measurement for an [int] value.
- [FlagProperty], which formats a [bool] value as one or more flags. Depending on the use case it is better to format a bool as `DiagnosticsProperty<bool>` instead of using [FlagProperty] as the output is more verbose but unambiguous.

## Other important [DiagnosticsProperty] variants

- [EnumProperty], which provides terse descriptions of enum values working around limitations of the `toString` implementation for Dart enum types.
- [IterableProperty], which handles iterable values with display customizable depending on the [DiagnosticsTreeStyle] used.
- [ObjectFlagProperty], which provides terse descriptions of whether a property value is present or not. For example, whether an `onClick` callback is specified or an animation is in progress.
- [ColorProperty], which must be used if the property value is a [Color] or one of its subclasses.
- [IconDataProperty], which must be used if the property value is of type [IconData].

If none of these subclasses apply, use the [DiagnosticsProperty] constructor or in rare cases create your own [DiagnosticsProperty] subclass as in the case for [TransformProperty] which handles [Matrix4] that represent transforms. Generally any property value with a good `toString` method implementation works fine using [DiagnosticsProperty] directly.

{@tool snippet}

This example shows best practices for implementing [debugFillProperties] illustrating use of all common [DiagnosticsProperty] subclasses and all common [DiagnosticsProperty] parameters.

```dart
class ExampleObject extends ExampleSuperclass {

  // ...various members and properties...

  @override
  void debugFillProperties(DiagnosticPropertiesBuilder properties) {
    // Always add properties from the base class first.
    super.debugFillProperties(properties);

    // Omit the property name 'message' when displaying this String property
    // as it would just add visual noise.
    properties.add(StringProperty('message', message, showName: false));

    properties.add(DoubleProperty('stepWidth', stepWidth));

    // A scale of 1.0 does nothing so should be hidden.
    properties.add(DoubleProperty('scale', scale, defaultValue: 1.0));

    // If the hitTestExtent matches the paintExtent, it is just set to its
    // default value so is not relevant.
    properties.add(DoubleProperty('hitTestExtent', hitTestExtent, defaultValue: paintExtent));

    // maxWidth of double.infinity indicates the width is unconstrained and
    // so maxWidth has no impact.
    properties.add(DoubleProperty('maxWidth', maxWidth, defaultValue: double.infinity));

    // Progress is a value between 0 and 1 or null. Showing it as a
    // percentage makes the meaning clear enough that the name can be
    // hidden.
    properties.add(PercentProperty(
      'progress',
      progress,
      showName: false,
      ifNull: '<indeterminate>',
    ));

    // Most text fields have maxLines set to 1.
    properties.add(IntProperty('maxLines', maxLines, defaultValue: 1));

    // Specify the unit as otherwise it would be unclear that time is in
    // milliseconds.
    properties.add(IntProperty('duration', duration.inMilliseconds, unit: 'ms'));

    // Tooltip is used instead of unit for this case as a unit should be a
    // terse description appropriate to display directly after a number
    // without a space.
    properties.add(DoubleProperty(
      'device pixel ratio',
      devicePixelRatio,
      tooltip: 'physical pixels per logical pixel',
    ));

    // Displaying the depth value would be distracting. Instead only display
    // if the depth value is missing.
    properties.add(ObjectFlagProperty<int>('depth', depth, ifNull: 'no depth'));

    // bool flag that is only shown when the value is true.
    properties.add(FlagProperty('using primary controller', value: primary));

    properties.add(FlagProperty(
      'isCurrent',
      value: isCurrent,
      ifTrue: 'active',
      ifFalse: 'inactive',
    ));

    properties.add(DiagnosticsProperty<bool>('keepAlive', keepAlive));

    // FlagProperty could have also been used in this case.
    // This option results in the text "obscureText: true" instead
    // of "obscureText" which is a bit more verbose but a bit clearer.
    properties.add(DiagnosticsProperty<bool>('obscureText', obscureText, defaultValue: false));

    properties.add(EnumProperty<TextAlign>('textAlign', textAlign, defaultValue: null));
    properties.add(EnumProperty<ImageRepeat>('repeat', repeat, defaultValue: ImageRepeat.noRepeat));

    // Warn users when the widget is missing but do not show the value.
    properties.add(ObjectFlagProperty<Widget>('widget', widget, ifNull: 'no widget'));

    properties.add(IterableProperty<BoxShadow>(
      'boxShadow',
      boxShadow,
      defaultValue: null,
      style: style,
    ));

    // Getting the value of size throws an exception unless hasSize is true.
    properties.add(DiagnosticsProperty<Size>.lazy(
      'size',
      () => size,
      description: '${ hasSize ? size : "MISSING" }',
    ));

    // If the `toString` method for the property value does not provide a
    // good terse description, write a DiagnosticsProperty subclass as in
    // the case of TransformProperty which displays a nice debugging view
    // of a Matrix4 that represents a transform.
    properties.add(TransformProperty('transform', transform));

    // If the value class has a good `toString` method, use
    // DiagnosticsProperty<YourValueType>. Specifying the value type ensures
    // that debugging tools always know the type of the field and so can
    // provide the right UI affordances. For example, in this case even
    // if color is null, a debugging tool still knows the value is a Color
    // and can display relevant color related UI.
    properties.add(DiagnosticsProperty<Color>('color', color));

    // Use a custom description to generate a more terse summary than the
    // `toString` method on the map class.
    properties.add(DiagnosticsProperty<Map<Listenable, VoidCallback>>(
      'handles',
      handles,
      description: handles != null
        ? '${handles!.length} active client${ handles!.length == 1 ? "" : "s" }'
        : null,
      ifNull: 'no notifications ever received',
      showName: false,
    ));
  }
}
```

{@end-tool}

Used by [toDiagnosticsNode] and [toString].

Do not add values that have lifetime shorter than the object.

# DiagnosticableTree

```dart
abstract class DiagnosticableTree with Diagnosticable {}
```

A base class for providing string and [DiagnosticsNode] debug representations describing the properties and children of an object.

The string debug representation is generated from the intermediate [DiagnosticsNode] representation. The [DiagnosticsNode] representation is also used by debugging tools displaying interactive trees of objects and properties.

See also:

- [DiagnosticableTreeMixin], a mixin that implements this class.
- [Diagnosticable], which should be used instead of this class to provide diagnostics for objects without children.

### DiagnosticableTree()

```dart
DiagnosticableTree()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### toStringShallow()

```dart
String toStringShallow({String joiner = ', ', DiagnosticLevel minLevel = DiagnosticLevel.debug})
```

Returns a one-line detailed description of the object.

This description is often somewhat long. This includes the same information given by [toStringDeep], but does not recurse to any children.

`joiner` specifies the string which is place between each part obtained from [debugFillProperties]. Passing a string such as `'\n '` will result in a multiline string that indents the properties of the object below its name (as per [toString]).

`minLevel` specifies the minimum [DiagnosticLevel] for properties included in the output.

See also:

- [toString], for a brief description of the object.
- [toStringDeep], for a description of the subtree rooted at this object.

### toStringDeep()

```dart
String toStringDeep({String prefixLineOne = '', String? prefixOtherLines, DiagnosticLevel minLevel = DiagnosticLevel.debug, int wrapWidth = 65})
```

Returns a string representation of this node and its descendants.

`prefixLineOne` will be added to the front of the first line of the output. `prefixOtherLines` will be added to the front of each other line. If `prefixOtherLines` is null, the `prefixLineOne` is used for every line. By default, there is no prefix.

`minLevel` specifies the minimum [DiagnosticLevel] for properties included in the output.

`wrapWidth` specifies the column number where word wrapping will be applied.

The [toStringDeep] method takes other arguments, but those are intended for internal use when recursing to the descendants, and so can be ignored.

See also:

- [toString], for a brief description of the object but not its children.
- [toStringShallow], for a detailed description of the object but not its children.

### toStringShort()

```dart
String toStringShort()
```

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style})
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

Returns a list of [DiagnosticsNode] objects describing this node's children.

Children that are offstage should be added with `style` set to [DiagnosticsTreeStyle.offstage] to indicate that they are offstage.

The list must not contain any null entries. If there are explicit null children to report, consider [DiagnosticsNode.message] or [DiagnosticsProperty<Object>] as possible [DiagnosticsNode] objects to provide.

Used by [toStringDeep], [toDiagnosticsNode] and [toStringShallow].

See also:

- [RenderTable.debugDescribeChildren], which provides high quality custom descriptions for its child nodes.

# DiagnosticableTreeMixin

```dart
mixin DiagnosticableTreeMixin implements DiagnosticableTree {}
```

A mixin that helps dump string and [DiagnosticsNode] representations of trees.

This mixin is identical to class [DiagnosticableTree].

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### toStringShallow()

```dart
String toStringShallow({String joiner = ', ', DiagnosticLevel minLevel = DiagnosticLevel.debug})
```

### toStringDeep()

```dart
String toStringDeep({String prefixLineOne = '', String? prefixOtherLines, DiagnosticLevel minLevel = DiagnosticLevel.debug, int wrapWidth = 65})
```

### toStringShort()

```dart
String toStringShort()
```

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style})
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DiagnosticsBlock

```dart
class DiagnosticsBlock extends DiagnosticsNode {}
```

[DiagnosticsNode] that exists mainly to provide a container for other diagnostics that typically lacks a meaningful value of its own.

This class is typically used for displaying complex nested error messages.

### DiagnosticsBlock()

```dart
DiagnosticsBlock({String? name, DiagnosticsTreeStyle style = DiagnosticsTreeStyle.whitespace, bool showName = true, bool showSeparator, String? linePrefix, Object? value, String? description, DiagnosticLevel level = DiagnosticLevel.info, bool allowTruncate = false, List<DiagnosticsNode> children = const <DiagnosticsNode>[], List<DiagnosticsNode> properties = const <DiagnosticsNode>[]})
```

Creates a diagnostic with properties specified by [properties] and children specified by [children].

### level

```dart
DiagnosticLevel level
```

### value

```dart
Object? value
```

### allowTruncate

```dart
bool allowTruncate
```

### getChildren()

```dart
List<DiagnosticsNode> getChildren()
```

### getProperties()

```dart
List<DiagnosticsNode> getProperties()
```

### toDescription()

```dart
String toDescription({TextTreeConfiguration? parentConfiguration})
```

# DiagnosticsSerializationDelegate

```dart
abstract class DiagnosticsSerializationDelegate {}
```

A delegate that configures how a hierarchy of [DiagnosticsNode]s should be serialized.

Implement this class in a subclass to fully configure how [DiagnosticsNode]s get serialized.

### DiagnosticsSerializationDelegate()

```dart
DiagnosticsSerializationDelegate({int subtreeDepth, bool includeProperties})
```

Creates a simple [DiagnosticsSerializationDelegate] that controls the [subtreeDepth] and whether to [includeProperties].

For additional configuration options, extend [DiagnosticsSerializationDelegate] and provide custom implementations for the methods of this class.

### additionalNodeProperties()

```dart
Map<String, Object?> additionalNodeProperties(DiagnosticsNode node, {bool fullDetails = true})
```

Returns a serializable map of additional information that will be included in the serialization of the given [DiagnosticsNode].

This method is called for every [DiagnosticsNode] that's included in the serialization.

### filterChildren()

```dart
List<DiagnosticsNode> filterChildren(List<DiagnosticsNode> nodes, DiagnosticsNode owner)
```

Filters the list of [DiagnosticsNode]s that will be included as children for the given `owner` node.

The callback may return a subset of the children in the provided list or replace the entire list with new child nodes.

See also:

- [subtreeDepth], which controls how many levels of children will be included in the serialization.

### filterProperties()

```dart
List<DiagnosticsNode> filterProperties(List<DiagnosticsNode> nodes, DiagnosticsNode owner)
```

Filters the list of [DiagnosticsNode]s that will be included as properties for the given `owner` node.

The callback may return a subset of the properties in the provided list or replace the entire list with new property nodes.

By default, `nodes` is returned as-is.

See also:

- [includeProperties], which controls whether properties will be included at all.

### truncateNodesList()

```dart
List<DiagnosticsNode> truncateNodesList(List<DiagnosticsNode> nodes, DiagnosticsNode? owner)
```

Truncates the given list of [DiagnosticsNode] that will be added to the serialization as children or properties of the `owner` node.

The method must return a subset of the provided nodes and may not replace any nodes. While [filterProperties] and [filterChildren] completely hide a node from the serialization, truncating a node will leave a hint in the serialization that there were additional nodes in the result that are not included in the current serialization.

By default, `nodes` is returned as-is.

### delegateForNode()

```dart
DiagnosticsSerializationDelegate delegateForNode(DiagnosticsNode node)
```

Returns the [DiagnosticsSerializationDelegate] to be used for adding the provided [DiagnosticsNode] to the serialization.

By default, this will return a copy of this delegate, which has the [subtreeDepth] reduced by one.

This is called for nodes that will be added to the serialization as property or child of another node. It may return the same delegate if no changes to it are necessary.

### subtreeDepth

```dart
int get subtreeDepth
```

Controls how many levels of children will be included in the serialized hierarchy of [DiagnosticsNode]s.

Defaults to zero.

See also:

- [filterChildren], which provides a way to filter the children that will be included.

### includeProperties

```dart
bool get includeProperties
```

Whether to include the properties of a [DiagnosticsNode] in the serialization.

Defaults to false.

See also:

- [filterProperties], which provides a way to filter the properties that will be included.

### expandPropertyValues

```dart
bool get expandPropertyValues
```

Whether properties that have a [Diagnosticable] as value should be expanded.

### copyWith()

```dart
DiagnosticsSerializationDelegate copyWith({int subtreeDepth, bool includeProperties})
```

Creates a copy of this [DiagnosticsSerializationDelegate] with the provided values.
