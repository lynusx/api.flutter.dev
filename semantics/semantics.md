@docImport 'dart:ui';

@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# SemanticsNodeVisitor

```dart
typedef SemanticsNodeVisitor = bool Function(SemanticsNode node)
```

Signature for a function that is called for each [SemanticsNode].

Return false to stop visiting nodes.

Used by [SemanticsNode.visitChildren].

# MoveCursorHandler

```dart
typedef MoveCursorHandler = void Function(bool extendSelection)
```

Signature for [SemanticsAction]s that move the cursor.

If `extendSelection` is set to true the cursor movement should extend the current selection or (if nothing is currently selected) start a selection.

# SetSelectionHandler

```dart
typedef SetSelectionHandler = void Function(TextSelection selection)
```

Signature for the [SemanticsAction.setSelection] handlers to change the text selection (or re-position the cursor) to `selection`.

# SetTextHandler

```dart
typedef SetTextHandler = void Function(String text)
```

Signature for the [SemanticsAction.setText] handlers to replace the current text with the input `text`.

# ScrollToOffsetHandler

```dart
typedef ScrollToOffsetHandler = void Function(Offset targetOffset)
```

Signature for the [SemanticsAction.scrollToOffset] handlers to scroll the scrollable container to the given `targetOffset`.

# SemanticsActionHandler

```dart
typedef SemanticsActionHandler = void Function(Object? args)
```

Signature for a handler of a [SemanticsAction].

Returned by [SemanticsConfiguration.getActionHandler].

# SemanticsUpdateCallback

```dart
typedef SemanticsUpdateCallback = void Function(SemanticsUpdate update)
```

Signature for a function that receives a semantics update and returns no result.

Used by [SemanticsOwner.onSemanticsUpdate].

# ChildSemanticsConfigurationsDelegate

```dart
typedef ChildSemanticsConfigurationsDelegate = ChildSemanticsConfigurationsResult Function(List<SemanticsConfiguration>)
```

Signature for the [SemanticsConfiguration.childConfigurationsDelegate].

The input list contains all [SemanticsConfiguration]s that rendering children want to merge upward. One can tag a render child with a [SemanticsTag] and look up its [SemanticsConfiguration]s through [SemanticsConfiguration.tagsChildrenWith].

The return value is the arrangement of these configs, including which configs continue to merge upward and which configs form sibling merge group.

Use [ChildSemanticsConfigurationsResultBuilder] to generate the return value.

# AccessibilityFocusBlockType

```dart
enum AccessibilityFocusBlockType {}
```

Controls how accessibility focus is blocked.

This is typically used to prevent screen readers from focusing on parts of the UI.

Setting this property also blocks the reporting of keyboard focusability for the semantics node, but it does not affect the actual keyboard focus handled by [FocusNode].

Accessibility focus is **not blocked**.

Blocks accessibility focus for the entire subtree.

Blocks accessibility focus for the **current node only**. Its descendants may still be focusable.

The AccessibilityFocusBlockType when two nodes get merged.

# SemanticsTag

```dart
class SemanticsTag {}
```

A tag for a [SemanticsNode].

Tags can be interpreted by the parent of a [SemanticsNode] and depending on the presence of a tag the parent can for example decide how to add the tagged node as a child. Tags are not sent to the engine.

As an example, the [RenderSemanticsGestureHandler] uses tags to determine if a child node should be excluded from the scrollable area for semantic purposes.

The provided [name] is only used for debugging. Two tags created with the same [name] and the `new` operator are not considered identical. However, two tags created with the same [name] and the `const` operator are always identical.

### SemanticsTag()

```dart
SemanticsTag(String name)
```

Creates a [SemanticsTag].

The provided [name] is only used for debugging. Two tags created with the same [name] and the `new` operator are not considered identical. However, two tags created with the same [name] and the `const` operator are always identical.

### name

```dart
String name
```

A human-readable name for this tag used for debugging.

This string is not used to determine if two tags are identical.

### toString()

```dart
String toString()
```

# ChildSemanticsConfigurationsResult

```dart
class ChildSemanticsConfigurationsResult {}
```

The result that contains the arrangement for the child [SemanticsConfiguration]s.

When the [PipelineOwner] builds the semantics tree, it uses the returned [ChildSemanticsConfigurationsResult] from [SemanticsConfiguration.childConfigurationsDelegate] to decide how semantics nodes should form.

Use [ChildSemanticsConfigurationsResultBuilder] to build the result.

### mergeUp

```dart
List<SemanticsConfiguration> mergeUp
```

Returns the [SemanticsConfiguration]s that are supposed to be merged into the parent semantics node.

[SemanticsConfiguration]s that are either semantics boundaries or are conflicting with other [SemanticsConfiguration]s will form explicit semantics nodes. All others will be merged into the parent.

### siblingMergeGroups

```dart
List<List<SemanticsConfiguration>> siblingMergeGroups
```

The groups of child semantics configurations that want to merge together and form a sibling [SemanticsNode].

All the [SemanticsConfiguration]s in a given group that are either semantics boundaries or are conflicting with other [SemanticsConfiguration]s of the same group will be excluded from the sibling merge group and form independent semantics nodes as usual.

The result [SemanticsNode]s from the merges are attached as the sibling nodes of the immediate parent semantics node. For example, a `RenderObjectA` has a rendering child, `RenderObjectB`. If both of them form their own semantics nodes, `SemanticsNodeA` and `SemanticsNodeB`, any semantics node created from sibling merge groups of `RenderObjectB` will be attach to `SemanticsNodeA` as a sibling of `SemanticsNodeB`.

# ChildSemanticsConfigurationsResultBuilder

```dart
class ChildSemanticsConfigurationsResultBuilder {}
```

The builder to build a [ChildSemanticsConfigurationsResult] based on its annotations.

To use this builder, one can use [markAsMergeUp] and [markAsSiblingMergeGroup] to annotate the arrangement of [SemanticsConfiguration]s. Once all the configs are annotated, use [build] to generate the [ChildSemanticsConfigurationsResult].

### ChildSemanticsConfigurationsResultBuilder()

```dart
ChildSemanticsConfigurationsResultBuilder()
```

Creates a [ChildSemanticsConfigurationsResultBuilder].

### markAsMergeUp()

```dart
void markAsMergeUp(SemanticsConfiguration config)
```

Marks the [SemanticsConfiguration] to be merged into the parent semantics node.

The [SemanticsConfiguration] will be added to the [ChildSemanticsConfigurationsResult.mergeUp] that this builder builds.

### markAsSiblingMergeGroup()

```dart
void markAsSiblingMergeGroup(List<SemanticsConfiguration> configs)
```

Marks a group of [SemanticsConfiguration]s to merge together and form a sibling [SemanticsNode].

The group of [SemanticsConfiguration]s will be added to the [ChildSemanticsConfigurationsResult.siblingMergeGroups] that this builder builds.

### build()

```dart
ChildSemanticsConfigurationsResult build()
```

Builds a [ChildSemanticsConfigurationsResult] contains the arrangement.

# CustomSemanticsAction

```dart
class CustomSemanticsAction {}
```

An identifier of a custom semantics action.

Custom semantics actions can be provided to make complex user interactions more accessible. For instance, if an application has a drag-and-drop list that requires the user to press and hold an item to move it, users interacting with the application using a hardware switch may have difficulty. This can be made accessible by creating custom actions and pairing them with handlers that move a list item up or down in the list.

In Android, these actions are presented in the local context menu. In iOS, these are presented in the radial context menu.

Localization and text direction do not automatically apply to the provided label or hint.

Instances of this class should either be instantiated with const or new instances cached in static fields.

See also:

- [SemanticsProperties], where the handler for a custom action is provided.

### CustomSemanticsAction()

```dart
CustomSemanticsAction({required String? label})
```

Creates a new [CustomSemanticsAction].

The [label] must not be empty.

### CustomSemanticsAction.overridingAction()

```dart
CustomSemanticsAction.overridingAction({required String? hint, required SemanticsAction? action})
```

Creates a new [CustomSemanticsAction] that overrides a standard semantics action.

The [hint] must not be empty.

### label

```dart
String? label
```

The user readable name of this custom semantics action.

### hint

```dart
String? hint
```

The hint description of this custom semantics action.

### action

```dart
SemanticsAction? action
```

The standard semantics action this action replaces.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### toString()

```dart
String toString()
```

### getIdentifier()

```dart
int getIdentifier(CustomSemanticsAction action)
```

Get the identifier for a given `action`.

### getAction()

```dart
CustomSemanticsAction? getAction(int id)
```

Get the `action` for a given identifier.

### resetForTests()

```dart
void resetForTests()
```

Resets internal state between tests. Does nothing if asserts are disabled.

# AttributedString

```dart
class AttributedString {}
```

A string that carries a list of [StringAttribute]s.

### AttributedString()

```dart
AttributedString(String string, {List<StringAttribute> attributes = const <StringAttribute>[]})
```

Creates a attributed string.

The [TextRange] in the [attributes] must be inside the length of the [string].

The [attributes] must not be changed after the attributed string is created.

### string

```dart
String string
```

The plain string stored in the attributed string.

### attributes

```dart
List<StringAttribute> attributes
```

The attributes this string carries.

The list must not be modified after this string is created.

### operator +()

```dart
AttributedString operator +(AttributedString other)
```

Returns a new [AttributedString] by concatenate the operands

The string attribute list of the returned [AttributedString] will contains the string attributes from both operands with updated text ranges.

### operator ==()

```dart
bool operator ==(Object other)
```

Two [AttributedString]s are equal if their string and attributes are.

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# AttributedStringProperty

```dart
class AttributedStringProperty extends DiagnosticsProperty<AttributedString> {}
```

A [DiagnosticsProperty] for [AttributedString]s, which shows a string when there are no attributes, and more details otherwise.

### AttributedStringProperty()

```dart
AttributedStringProperty(String name, dynamic value, {dynamic showName, bool showWhenEmpty = false, dynamic defaultValue, dynamic level, dynamic description})
```

Create a diagnostics property for an [AttributedString] object.

Such properties are used with [SemanticsData] objects.

### showWhenEmpty

```dart
bool showWhenEmpty
```

Whether to show the property when the [value] is an [AttributedString] whose [AttributedString.string] is the empty string.

This overrides [defaultValue].

### isInteresting

```dart
bool get isInteresting
```

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

# SemanticsLabelBuilder

```dart
final class SemanticsLabelBuilder {}
```

Builder for creating semantically correct concatenated labels with proper text direction handling and spacing.

This builder helps address the complexity of concatenating multiple text parts while handling language-specific nuances like RTL vs LTR text direction and proper spacing.

Example usage:

```dart
SemanticsLabelBuilder builder = SemanticsLabelBuilder()
  ..addPart('Hello')
  ..addPart('world');
String label = builder.build(); // "Hello world"
```

For multilingual text with proper RTL support:

```dart
SemanticsLabelBuilder builder = SemanticsLabelBuilder(textDirection: TextDirection.ltr)
  ..addPart('Welcome', textDirection: TextDirection.ltr)
  ..addPart('مرحبا', textDirection: TextDirection.rtl); // Arabic
String label = builder.build(); // "Welcome \u202Bمرحبا\u202C" (with Unicode embedding)
```

### SemanticsLabelBuilder()

```dart
SemanticsLabelBuilder({String separator = ' ', TextDirection? textDirection})
```

Creates a new [SemanticsLabelBuilder].

The [separator] is used between text parts (defaults to space). The [textDirection] specifies the overall text direction for the concatenated label.

### separator

```dart
String separator
```

The separator used between text parts.

### textDirection

```dart
TextDirection? textDirection
```

The overall text direction for the concatenated label.

### addPart()

```dart
void addPart(String label, {TextDirection? textDirection})
```

Adds a text part.

If [textDirection] is specified, it will be used for this specific part. Empty parts are ignored.

### isEmpty

```dart
bool get isEmpty
```

Returns true if no parts have been added to this builder.

### length

```dart
int get length
```

Returns the number of parts added to this builder.

### build()

```dart
String build()
```

Builds and returns the concatenated label from the added parts.

This method concatenates all parts with proper text direction handling and spacing.

### clear()

```dart
void clear()
```

Clears all parts from this builder, allowing it to be reused.

# SemanticsData

```dart
class SemanticsData with Diagnosticable {}
```

Summary information about a [SemanticsNode] object.

A semantics node might [SemanticsNode.mergeAllDescendantsIntoThisNode], which means the individual fields on the semantics node don't fully describe the semantics at that node. This data structure contains the full semantics for the node.

Typically obtained from [SemanticsNode.getSemanticsData].

### SemanticsData()

```dart
SemanticsData({required SemanticsFlags flagsCollection, required int actions, required String identifier, required Object? traversalParentIdentifier, required Object? traversalChildIdentifier, required AttributedString attributedLabel, required AttributedString attributedValue, required AttributedString attributedIncreasedValue, required AttributedString attributedDecreasedValue, required AttributedString attributedHint, required String tooltip, required TextDirection? textDirection, required Rect rect, required TextSelection? textSelection, required int? scrollIndex, required int? scrollChildCount, required double? scrollPosition, required double? scrollExtentMax, required double? scrollExtentMin, required int? platformViewId, required int? maxValueLength, required int? currentValueLength, required int headingLevel, required Uri? linkUrl, required SemanticsRole role, required Set<String>? controlsNodes, required SemanticsValidationResult validationResult, required ui.SemanticsHitTestBehavior hitTestBehavior, required SemanticsInputType inputType, required Locale? locale, required String? minValue, required String? maxValue, Set<SemanticsTag>? tags, Matrix4? transform, List<int>? customSemanticsActionIds})
```

Creates a semantics data object.

If [label] is not empty, then [textDirection] must also not be null.

### flags

```dart
int get flags
```

A bit field of [SemanticsFlag]s that apply to this node.

### flagsCollection

```dart
SemanticsFlags flagsCollection
```

Semantics flags.

### actions

```dart
int actions
```

A bit field of [SemanticsAction]s that apply to this node.

### identifier

```dart
String identifier
```

{@macro flutter.semantics.SemanticsProperties.identifier}

### traversalParentIdentifier

```dart
Object? traversalParentIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalParentIdentifier}

### traversalChildIdentifier

```dart
Object? traversalChildIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalChildIdentifier}

### label

```dart
String get label
```

A textual description for the current label of the node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedLabel].

### attributedLabel

```dart
AttributedString attributedLabel
```

A textual description for the current label of the node in [AttributedString] format.

The reading direction is given by [textDirection].

See also [label], which exposes just the raw text.

### value

```dart
String get value
```

A textual description for the current value of the node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedValue].

### attributedValue

```dart
AttributedString attributedValue
```

A textual description for the current value of the node in [AttributedString] format.

The reading direction is given by [textDirection].

See also [value], which exposes just the raw text.

### increasedValue

```dart
String get increasedValue
```

The value that [value] will become after performing a [SemanticsAction.increase] action.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedIncreasedValue].

### attributedIncreasedValue

```dart
AttributedString attributedIncreasedValue
```

The value that [value] will become after performing a [SemanticsAction.increase] action in [AttributedString] format.

The reading direction is given by [textDirection].

See also [increasedValue], which exposes just the raw text.

### decreasedValue

```dart
String get decreasedValue
```

The value that [value] will become after performing a [SemanticsAction.decrease] action.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedDecreasedValue].

### attributedDecreasedValue

```dart
AttributedString attributedDecreasedValue
```

The value that [value] will become after performing a [SemanticsAction.decrease] action in [AttributedString] format.

The reading direction is given by [textDirection].

See also [decreasedValue], which exposes just the raw text.

### hint

```dart
String get hint
```

A brief description of the result of performing an action on this node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedHint].

### attributedHint

```dart
AttributedString attributedHint
```

A brief description of the result of performing an action on this node in [AttributedString] format.

The reading direction is given by [textDirection].

See also [hint], which exposes just the raw text.

### tooltip

```dart
String tooltip
```

A textual description of the widget's tooltip.

The reading direction is given by [textDirection].

### headingLevel

```dart
int headingLevel
```

Indicates that this subtree represents a heading.

A value of 0 indicates that it is not a heading. The value should be a number between 1 and 6, indicating the hierarchical level as a heading.

### textDirection

```dart
TextDirection? textDirection
```

The reading direction for the text in [label], [value], [increasedValue], [decreasedValue], and [hint].

### textSelection

```dart
TextSelection? textSelection
```

The currently selected text (or the position of the cursor) within [value] if this node represents a text field.

### scrollChildCount

```dart
int? scrollChildCount
```

The total number of scrollable children that contribute to semantics.

If the number of children are unknown or unbounded, this value will be null.

### scrollIndex

```dart
int? scrollIndex
```

The index of the first visible semantic child of a scroll node.

### scrollPosition

```dart
double? scrollPosition
```

Indicates the current scrolling position in logical pixels if the node is scrollable.

The properties [scrollExtentMin] and [scrollExtentMax] indicate the valid in-range values for this property. The value for [scrollPosition] may (temporarily) be outside that range, e.g. during an overscroll.

See also:

- [ScrollPosition.pixels], from where this value is usually taken.

### scrollExtentMax

```dart
double? scrollExtentMax
```

Indicates the maximum in-range value for [scrollPosition] if the node is scrollable.

This value may be infinity if the scroll is unbound.

See also:

- [ScrollPosition.maxScrollExtent], from where this value is usually taken.

### scrollExtentMin

```dart
double? scrollExtentMin
```

Indicates the minimum in-range value for [scrollPosition] if the node is scrollable.

This value may be infinity if the scroll is unbound.

See also:

- [ScrollPosition.minScrollExtent], from where this value is usually taken.

### platformViewId

```dart
int? platformViewId
```

The id of the platform view, whose semantics nodes will be added as children to this node.

If this value is non-null, the SemanticsNode must not have any children as those would be replaced by the semantics nodes of the referenced platform view.

See also:

- [AndroidView], which is the platform view for Android.
- [UiKitView], which is the platform view for iOS.

### maxValueLength

```dart
int? maxValueLength
```

The maximum number of characters that can be entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [SemanticsFlag.isTextField] is set. Defaults to null, which means no limit is imposed on the text field.

### currentValueLength

```dart
int? currentValueLength
```

The current number of characters that have been entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [SemanticsFlag.isTextField] is set. This must be set when [maxValueLength] is set.

### linkUrl

```dart
Uri? linkUrl
```

The URL that this node links to.

See also:

- [SemanticsFlag.isLink], which indicates that this node is a link.

### rect

```dart
Rect rect
```

The bounding box for this node in its coordinate system.

### tags

```dart
Set<SemanticsTag>? tags
```

The set of [SemanticsTag]s associated with this node.

### transform

```dart
Matrix4? transform
```

The transform from this node's coordinate system to its parent's coordinate system.

By default, the transform is null, which represents the identity transformation (i.e., that this node has the same coordinate system as its parent).

### customSemanticsActionIds

```dart
List<int>? customSemanticsActionIds
```

The identifiers for the custom semantics actions and standard action overrides for this node.

The list must be sorted in increasing order.

See also:

- [CustomSemanticsAction], for an explanation of custom actions.

### role

```dart
SemanticsRole role
```

{@macro flutter.semantics.SemanticsNode.role}

### controlsNodes

```dart
Set<String>? controlsNodes
```

{@macro flutter.semantics.SemanticsNode.controlsNodes}

{@macro flutter.semantics.SemanticsProperties.controlsNodes}

### validationResult

```dart
SemanticsValidationResult validationResult
```

{@macro flutter.semantics.SemanticsProperties.validationResult}

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior hitTestBehavior
```

{@macro flutter.semantics.SemanticsProperties.hitTestBehavior}

### inputType

```dart
SemanticsInputType inputType
```

{@macro flutter.semantics.SemanticsNode.inputType}

### locale

```dart
Locale? locale
```

The locale for this semantics node.

Assistive technologies uses this property to correctly interpret the content of this semantics node.

### maxValue

```dart
String? maxValue
```

{@macro flutter.semantics.SemanticsProperties.maxValue}

### minValue

```dart
String? minValue
```

{@macro flutter.semantics.SemanticsProperties.minValue}

### hasFlag()

```dart
bool hasFlag(SemanticsFlag flag)
```

Whether [flags] contains the given flag.

### hasAction()

```dart
bool hasAction(SemanticsAction action)
```

Whether [actions] contains the given action.

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# SemanticsHintOverrides

```dart
class SemanticsHintOverrides extends DiagnosticableTree {}
```

Provides hint values which override the default hints on supported platforms.

On iOS, these values are always ignored.

### SemanticsHintOverrides()

```dart
SemanticsHintOverrides({String? onTapHint, String? onLongPressHint})
```

Creates a semantics hint overrides.

### onTapHint

```dart
String? onTapHint
```

The hint text for a tap action.

If null, the standard hint is used instead.

The hint should describe what happens when a tap occurs, not the manner in which a tap is accomplished.

Bad: 'Double tap to show movies'. Good: 'show movies'.

### onLongPressHint

```dart
String? onLongPressHint
```

The hint text for a long press action.

If null, the standard hint is used instead.

The hint should describe what happens when a long press occurs, not the manner in which the long press is accomplished.

Bad: 'Double tap and hold to show tooltip'. Good: 'show tooltip'.

### isNotEmpty

```dart
bool get isNotEmpty
```

Whether there are any non-null hint values.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SemanticsProperties

```dart
class SemanticsProperties extends DiagnosticableTree {}
```

Contains properties used by assistive technologies to make the application more accessible.

The properties of this class are used to generate a [SemanticsNode]s in the semantics tree.

### SemanticsProperties()

```dart
SemanticsProperties({bool? enabled, bool? checked, bool? mixed, bool? expanded, bool? selected, bool? toggled, bool? button, bool? link, Uri? linkUrl, bool? header, int? headingLevel, bool? textField, bool? slider, bool? keyboardKey, bool? readOnly, bool? focusable, bool? focused, AccessibilityFocusBlockType? accessibilityFocusBlockType, bool? inMutuallyExclusiveGroup, bool? hidden, bool? obscured, bool? multiline, bool? scopesRoute, bool? namesRoute, bool? image, bool? liveRegion, bool? isRequired, int? maxValueLength, int? currentValueLength, String? identifier, Object? traversalParentIdentifier, Object? traversalChildIdentifier, String? label, AttributedString? attributedLabel, String? value, AttributedString? attributedValue, String? increasedValue, AttributedString? attributedIncreasedValue, String? decreasedValue, AttributedString? attributedDecreasedValue, String? hint, String? tooltip, AttributedString? attributedHint, SemanticsHintOverrides? hintOverrides, TextDirection? textDirection, SemanticsSortKey? sortKey, SemanticsTag? tagForChildren, SemanticsRole? role, Set<String>? controlsNodes, SemanticsInputType? inputType, SemanticsValidationResult validationResult = SemanticsValidationResult.none, ui.SemanticsHitTestBehavior? hitTestBehavior, VoidCallback? onTap, VoidCallback? onLongPress, VoidCallback? onScrollLeft, VoidCallback? onScrollRight, VoidCallback? onScrollUp, VoidCallback? onScrollDown, VoidCallback? onIncrease, VoidCallback? onDecrease, VoidCallback? onCopy, VoidCallback? onCut, VoidCallback? onPaste, MoveCursorHandler? onMoveCursorForwardByCharacter, MoveCursorHandler? onMoveCursorBackwardByCharacter, MoveCursorHandler? onMoveCursorForwardByWord, MoveCursorHandler? onMoveCursorBackwardByWord, SetSelectionHandler? onSetSelection, SetTextHandler? onSetText, VoidCallback? onDidGainAccessibilityFocus, VoidCallback? onDidLoseAccessibilityFocus, VoidCallback? onFocus, VoidCallback? onDismiss, VoidCallback? onExpand, VoidCallback? onCollapse, Map<CustomSemanticsAction, VoidCallback>? customSemanticsActions, String? minValue, String? maxValue})
```

Creates a semantic annotation.

### enabled

```dart
bool? enabled
```

If non-null, indicates that this subtree represents something that can be in an enabled or disabled state.

For example, a button that a user can currently interact with would set this field to true. A button that currently does not respond to user interactions would set this field to false.

### checked

```dart
bool? checked
```

If non-null, indicates that this subtree represents a checkbox or similar widget with a "checked" state, and what its current state is.

When the [Checkbox.value] of a tristate Checkbox is null, indicating a mixed-state, this value shall be false, in which case, [mixed] will be true.

This is mutually exclusive with [toggled] and [mixed].

### mixed

```dart
bool? mixed
```

If non-null, indicates that this subtree represents a checkbox or similar widget with a "half-checked" state or similar, and whether it is currently in this half-checked state.

This must be null when [Checkbox.tristate] is false, or when the widget is not a checkbox. When a tristate checkbox is fully unchecked/checked, this value shall be false.

This is mutually exclusive with [checked] and [toggled].

### expanded

```dart
bool? expanded
```

If non-null, indicates that this subtree represents something that can be in an "expanded" or "collapsed" state.

For example, if a [SubmenuButton] is opened, this property should be set to true; otherwise, this property should be false.

### toggled

```dart
bool? toggled
```

If non-null, indicates that this subtree represents a toggle switch or similar widget with an "on" state, and what its current state is.

This is mutually exclusive with [checked] and [mixed].

### selected

```dart
bool? selected
```

If non-null indicates that this subtree represents something that can be in a selected or unselected state, and what its current state is.

The active tab in a tab bar for example is considered "selected", whereas all other tabs are unselected.

### button

```dart
bool? button
```

If non-null, indicates that this subtree represents a button.

TalkBack/VoiceOver provides users with the hint "button" when a button is focused.

### link

```dart
bool? link
```

If non-null, indicates that this subtree represents a link.

iOS's VoiceOver provides users with a unique hint when a link is focused. Android's Talkback will announce a link hint the same way it does a button.

### header

```dart
bool? header
```

If non-null, indicates that this subtree represents a header.

A header is typically the top element of a page or section, such as a page title or app bar title.

### textField

```dart
bool? textField
```

If non-null, indicates that this subtree represents a text field.

TalkBack/VoiceOver provide special affordances to enter text into a text field.

### slider

```dart
bool? slider
```

If non-null, indicates that this subtree represents a slider.

Talkback/\VoiceOver provides users with the hint "slider" when a slider is focused.

### keyboardKey

```dart
bool? keyboardKey
```

If non-null, indicates that this subtree represents a keyboard key.

### readOnly

```dart
bool? readOnly
```

If non-null, indicates that this subtree is read only.

Only applicable when [textField] is true.

TalkBack/VoiceOver will treat it as non-editable text field.

### focusable

```dart
bool? focusable
```

If non-null, whether the node is able to hold input focus.

If [focusable] is set to false, then [focused] must not be true.

Input focus indicates that the node will receive keyboard events. It is not to be confused with accessibility focus. Accessibility focus is the green/black rectangular highlight that TalkBack/VoiceOver draws around the element it is reading, and is separate from input focus.

### focused

```dart
bool? focused
```

If non-null, whether the node currently holds input focus.

If null, the node is not focusable.

At most one node in the tree should hold input focus at any point in time, and it should not be set to true if [focusable] is false.

Input focus indicates that the node will receive keyboard events. It is not to be confused with accessibility focus. Accessibility focus is the green/black rectangular highlight that TalkBack/VoiceOver draws around the element it is reading, and is separate from input focus.

### accessibilityFocusBlockType

```dart
AccessibilityFocusBlockType? accessibilityFocusBlockType
```

If non-null, indicates if this subtree or current node is blocked in a11y focus.

This is for accessibility focus, which is the focus used by screen readers like TalkBack and VoiceOver. It is different from input focus, which is usually held by the element that currently responds to keyboard inputs.

### inMutuallyExclusiveGroup

```dart
bool? inMutuallyExclusiveGroup
```

If non-null, whether a semantic node is in a mutually exclusive group.

For example, a radio button is in a mutually exclusive group because only one radio button in that group can be marked as [checked].

### hidden

```dart
bool? hidden
```

If non-null, whether the node is considered hidden.

Hidden elements are currently not visible on screen. They may be covered by other elements or positioned outside of the visible area of a viewport.

Hidden elements cannot gain accessibility focus though regular touch. The only way they can be focused is by moving the focus to them via linear navigation.

Platforms are free to completely ignore hidden elements and new platforms are encouraged to do so.

Instead of marking an element as hidden it should usually be excluded from the semantics tree altogether. Hidden elements are only included in the semantics tree to work around platform limitations and they are mainly used to implement accessibility scrolling on iOS.

### obscured

```dart
bool? obscured
```

If non-null, whether [value] should be obscured.

This option is usually set in combination with [textField] to indicate that the text field contains a password (or other sensitive information). Doing so instructs screen readers to not read out the [value].

### multiline

```dart
bool? multiline
```

Whether the [value] is coming from a field that supports multiline text editing.

This option is only meaningful when [textField] is true to indicate whether it's a single-line or multiline text field.

This option is null when [textField] is false.

### scopesRoute

```dart
bool? scopesRoute
```

If non-null, whether the node corresponds to the root of a subtree for which a route name should be announced.

Generally, this is set in combination with [SemanticsConfiguration.explicitChildNodes], since nodes with this flag are not considered focusable by Android or iOS.

See also:

- [SemanticsFlag.scopesRoute] for a description of how the announced value is selected.

### namesRoute

```dart
bool? namesRoute
```

If non-null, whether the node contains the semantic label for a route.

See also:

- [SemanticsFlag.namesRoute] for a description of how the name is used.

### image

```dart
bool? image
```

If non-null, whether the node represents an image.

See also:

- [SemanticsFlag.isImage], for the flag this setting controls.

### liveRegion

```dart
bool? liveRegion
```

If non-null, whether the node should be considered a live region.

A live region indicates that updates to semantics node are important. Platforms may use this information to make polite announcements to the user to inform them of updates to this node.

An example of a live region is a [SnackBar] widget. On Android and iOS, live region causes a polite announcement to be generated automatically, even if the widget does not have accessibility focus. This announcement may not be spoken if the OS accessibility services are already announcing something else, such as reading the label of a focused widget or providing a system announcement.

See also:

- [SemanticsFlag.isLiveRegion], the semantics flag this setting controls.
- [SemanticsConfiguration.liveRegion], for a full description of a live region.

### isRequired

```dart
bool? isRequired
```

If non-null, whether the node should be considered required.

If true, user input is required on the semantics node before a form can be submitted. If false, the node is optional before a form can be submitted. If null, the node does not have a required semantics.

For example, a login form requires its email text field to be non-empty.

On web, this will set a `aria-required` attribute on the DOM element that corresponds to the semantics node.

See also:

- [SemanticsFlag.isRequired], for the flag this setting controls.

### maxValueLength

```dart
int? maxValueLength
```

The maximum number of characters that can be entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [textField] is true. Defaults to null, which means no limit is imposed on the text field.

### currentValueLength

```dart
int? currentValueLength
```

The current number of characters that have been entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [textField] is true. Must be set when [maxValueLength] is set.

### identifier

```dart
String? identifier
```

{@template flutter.semantics.SemanticsProperties.identifier} Provides an identifier for the semantics node in native accessibility hierarchy.

This value is not exposed to the users of the app.

It's usually used for UI testing with tools that work by querying the native accessibility, like UIAutomator, XCUITest, or Appium. It can be matched with [CommonFinders.bySemanticsIdentifier].

When set, this property implicitly forces the creation of a new [SemanticsNode] (equivalent to setting `container` to true in [Semantics]). This ensures the identifier is always attached to its own node and is not merged into an ancestor.

On Android, this is used for `AccessibilityNodeInfo.setViewIdResourceName`. It'll be appear in accessibility hierarchy as `resource-id`.

On iOS, this will set `UIAccessibilityElement.accessibilityIdentifier`.

On web, this will set a `flt-semantics-identifier` attribute on the DOM element that corresponds to the semantics node. {@endtemplate}

### traversalParentIdentifier

```dart
Object? traversalParentIdentifier
```

{@template flutter.semantics.SemanticsProperties.traversalParentIdentifier} Provides an identifier for establishing parent-child relationships in the semantics traversal tree.

This property is used to create a logical parent-child relationship between semantics nodes that may not be directly connected in the widget tree. It's primarily used with [OverlayPortal] to ensure proper accessibility traversal order when overlay content needs to be semantically connected to its parent widget.

When a semantics node has a [traversalParentIdentifier], it indicates that this node can act as a parent for other nodes that reference this identifier in their [traversalChildIdentifier]. This allows assistive technologies to navigate the UI in the correct logical order.

The `traversalParentIdentifier` must be unique in the semantics. No two semantics node can have the same `traversalParentIdentifier`. This unique identifier serves as the only reference for its traversal children. To graft other nodes as the traversal children of this node, assign this same value to their `traversalChildIdentifier`. {@endtemplate}

### traversalChildIdentifier

```dart
Object? traversalChildIdentifier
```

{@template flutter.semantics.SemanticsProperties.traversalChildIdentifier} Provides an identifier for establishing parent-child relationships in the semantics traversal tree.

This property is used to create a logical parent-child relationship between semantics nodes that may not be directly connected in the widget tree. It's primarily used with [OverlayPortal] to ensure proper accessibility traversal order when overlay content needs to be semantically connected to its parent widget.

When a semantics node has a [traversalChildIdentifier], it indicates that this node should be treated as a child of another node that has this same identifier as its [traversalParentIdentifier]. This allows assistive technologies to navigate the UI in the correct logical order.

The `traversalChildIdentifier` value may be duplicated across multiple semantics nodes. To establish one or more nodes as the traversal children of a parent node, assign this identifier the same value as the parent's `traversalParentIdentifier`. {@endtemplate}

### label

```dart
String? label
```

Provides a textual description of the widget.

If a label is provided, there must either by an ambient [Directionality] or an explicit [textDirection] should be provided.

Callers must not provide both [label] and [attributedLabel]. One or both must be null.

See also:

- [SemanticsConfiguration.label] for a description of how this is exposed in TalkBack and VoiceOver.
- [attributedLabel] for an [AttributedString] version of this property.

### attributedLabel

```dart
AttributedString? attributedLabel
```

Provides an [AttributedString] version of textual description of the widget.

If a [attributedLabel] is provided, there must either by an ambient [Directionality] or an explicit [textDirection] should be provided.

Callers must not provide both [label] and [attributedLabel]. One or both must be null.

See also:

- [SemanticsConfiguration.attributedLabel] for a description of how this is exposed in TalkBack and VoiceOver.
- [label] for a plain string version of this property.

### value

```dart
String? value
```

Provides a textual description of the value of the widget.

If a value is provided, there must either by an ambient [Directionality] or an explicit [textDirection] should be provided.

Callers must not provide both [value] and [attributedValue], One or both must be null.

See also:

- [SemanticsConfiguration.value] for a description of how this is exposed in TalkBack and VoiceOver.
- [attributedLabel] for an [AttributedString] version of this property.

### attributedValue

```dart
AttributedString? attributedValue
```

Provides an [AttributedString] version of textual description of the value of the widget.

If a [attributedValue] is provided, there must either by an ambient [Directionality] or an explicit [textDirection] should be provided.

Callers must not provide both [value] and [attributedValue], One or both must be null.

See also:

- [SemanticsConfiguration.attributedValue] for a description of how this is exposed in TalkBack and VoiceOver.
- [value] for a plain string version of this property.

### increasedValue

```dart
String? increasedValue
```

The value that [value] or [attributedValue] will become after a [SemanticsAction.increase] action has been performed on this widget.

If a value is provided, [onIncrease] must also be set and there must either be an ambient [Directionality] or an explicit [textDirection] must be provided.

Callers must not provide both [increasedValue] and [attributedIncreasedValue], One or both must be null.

See also:

- [SemanticsConfiguration.increasedValue] for a description of how this is exposed in TalkBack and VoiceOver.
- [attributedIncreasedValue] for an [AttributedString] version of this property.

### attributedIncreasedValue

```dart
AttributedString? attributedIncreasedValue
```

The [AttributedString] that [value] or [attributedValue] will become after a [SemanticsAction.increase] action has been performed on this widget.

If a [attributedIncreasedValue] is provided, [onIncrease] must also be set and there must either be an ambient [Directionality] or an explicit [textDirection] must be provided.

Callers must not provide both [increasedValue] and [attributedIncreasedValue], One or both must be null.

See also:

- [SemanticsConfiguration.attributedIncreasedValue] for a description of how this is exposed in TalkBack and VoiceOver.
- [increasedValue] for a plain string version of this property.

### decreasedValue

```dart
String? decreasedValue
```

The value that [value] or [attributedValue] will become after a [SemanticsAction.decrease] action has been performed on this widget.

If a value is provided, [onDecrease] must also be set and there must either be an ambient [Directionality] or an explicit [textDirection] must be provided.

Callers must not provide both [decreasedValue] and [attributedDecreasedValue], One or both must be null.

See also:

- [SemanticsConfiguration.decreasedValue] for a description of how this is exposed in TalkBack and VoiceOver.
- [attributedDecreasedValue] for an [AttributedString] version of this property.

### attributedDecreasedValue

```dart
AttributedString? attributedDecreasedValue
```

The [AttributedString] that [value] or [attributedValue] will become after a [SemanticsAction.decrease] action has been performed on this widget.

If a [attributedDecreasedValue] is provided, [onDecrease] must also be set and there must either be an ambient [Directionality] or an explicit [textDirection] must be provided.

Callers must not provide both [decreasedValue] and [attributedDecreasedValue], One or both must be null/// provided.

See also:

- [SemanticsConfiguration.attributedDecreasedValue] for a description of how this is exposed in TalkBack and VoiceOver.
- [decreasedValue] for a plain string version of this property.

### hint

```dart
String? hint
```

Provides a brief textual description of the result of an action performed on the widget.

If a hint is provided, there must either be an ambient [Directionality] or an explicit [textDirection] should be provided.

Callers must not provide both [hint] and [attributedHint], One or both must be null.

See also:

- [SemanticsConfiguration.hint] for a description of how this is exposed in TalkBack and VoiceOver.
- [attributedHint] for an [AttributedString] version of this property.

### attributedHint

```dart
AttributedString? attributedHint
```

Provides an [AttributedString] version of brief textual description of the result of an action performed on the widget.

If a [attributedHint] is provided, there must either by an ambient [Directionality] or an explicit [textDirection] should be provided.

Callers must not provide both [hint] and [attributedHint], One or both must be null.

See also:

- [SemanticsConfiguration.attributedHint] for a description of how this is exposed in TalkBack and VoiceOver.
- [hint] for a plain string version of this property.

### tooltip

```dart
String? tooltip
```

Provides a textual description of the widget's tooltip.

In Android, this property sets the `AccessibilityNodeInfo.setTooltipText`. In iOS, this property is appended to the end of the `UIAccessibilityElement.accessibilityLabel`.

If a [tooltip] is provided, there must either by an ambient [Directionality] or an explicit [textDirection] should be provided.

### headingLevel

```dart
int? headingLevel
```

The heading level in the document structure.

A heading divides content into sections. For example, an address book application might define headings A, B, C, etc. to divide the list of alphabetically sorted contacts into sections.

Screen readers use this value to determine which part of the page structure this heading represents. A level 1 heading usually indicates the main heading of a page, a level 2 heading the first subsection, a level 3 is a subsection of that, and so on.

On web, this sets the `aria-level` attribute (e.g., `aria-level="1"`). On Android, this sets the `isHeading` property for accessibility.

### hintOverrides

```dart
SemanticsHintOverrides? hintOverrides
```

Overrides the default accessibility hints provided by the platform.

This [hintOverrides] property does not affect how the platform processes hints; it only sets the custom text that will be read by assistive technology.

On Android, these overrides replace the default hints for semantics nodes with tap or long-press actions. For example, if [SemanticsHintOverrides.onTapHint] is provided, instead of saying `Double tap to activate`, the screen reader will say `Double tap to <onTapHint>`.

On iOS, this property is ignored, and default platform behavior applies.

Example usage:

```dart
const Semantics.fromProperties(
 properties: SemanticsProperties(
   hintOverrides: SemanticsHintOverrides(
     onTapHint: 'open settings',
   ),
 ),
 child: Text('button'),
)
```

### textDirection

```dart
TextDirection? textDirection
```

The reading direction of the [label], [value], [increasedValue], [decreasedValue], and [hint].

Defaults to the ambient [Directionality].

### sortKey

```dart
SemanticsSortKey? sortKey
```

Determines the position of this node among its siblings in the traversal sort order.

This is used to describe the order in which the semantic node should be traversed by the accessibility services on the platform (e.g. VoiceOver on iOS and TalkBack on Android).

### tagForChildren

```dart
SemanticsTag? tagForChildren
```

A tag to be applied to the child [SemanticsNode]s of this widget.

The tag is added to all child [SemanticsNode]s that pass through the [RenderObject] corresponding to this widget while looking to be attached to a parent SemanticsNode.

Tags are used to communicate to a parent SemanticsNode that a child SemanticsNode was passed through a particular RenderObject. The parent can use this information to determine the shape of the semantics tree.

See also:

- [SemanticsConfiguration.addTagForChildren], to which the tags provided here will be passed.

### linkUrl

```dart
Uri? linkUrl
```

The URL that this node links to.

On the web, this is used to set the `href` attribute of the DOM element.

See also:

- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href

### onTap

```dart
VoidCallback? onTap
```

The handler for [SemanticsAction.tap].

This is the semantic equivalent of a user briefly tapping the screen with the finger without moving it. For example, a button should implement this action.

VoiceOver users on iOS and TalkBack users on Android _may_ trigger this action by double-tapping the screen while an element is focused.

Note: different OSes or assistive technologies may decide to interpret user inputs differently. Some may simulate real screen taps, while others may call semantics tap. One way to handle taps properly is to provide the same handler to both gesture tap and semantics tap.

### onLongPress

```dart
VoidCallback? onLongPress
```

The handler for [SemanticsAction.longPress].

This is the semantic equivalent of a user pressing and holding the screen with the finger for a few seconds without moving it.

VoiceOver users on iOS and TalkBack users on Android _may_ trigger this action by double-tapping the screen without lifting the finger after the second tap.

Note: different OSes or assistive technologies may decide to interpret user inputs differently. Some may simulate real long presses, while others may call semantics long press. One way to handle long press properly is to provide the same handler to both gesture long press and semantics long press.

### onScrollLeft

```dart
VoidCallback? onScrollLeft
```

The handler for [SemanticsAction.scrollLeft].

This is the semantic equivalent of a user moving their finger across the screen from right to left. It should be recognized by controls that are horizontally scrollable.

VoiceOver users on iOS can trigger this action by swiping left with three fingers. TalkBack users on Android can trigger this action by swiping right and then left in one motion path. On Android, [onScrollUp] and [onScrollLeft] share the same gesture. Therefore, only on of them should be provided.

### onScrollRight

```dart
VoidCallback? onScrollRight
```

The handler for [SemanticsAction.scrollRight].

This is the semantic equivalent of a user moving their finger across the screen from left to right. It should be recognized by controls that are horizontally scrollable.

VoiceOver users on iOS can trigger this action by swiping right with three fingers. TalkBack users on Android can trigger this action by swiping left and then right in one motion path. On Android, [onScrollDown] and [onScrollRight] share the same gesture. Therefore, only on of them should be provided.

### onScrollUp

```dart
VoidCallback? onScrollUp
```

The handler for [SemanticsAction.scrollUp].

This is the semantic equivalent of a user moving their finger across the screen from bottom to top. It should be recognized by controls that are vertically scrollable.

VoiceOver users on iOS can trigger this action by swiping up with three fingers. TalkBack users on Android can trigger this action by swiping right and then left in one motion path. On Android, [onScrollUp] and [onScrollLeft] share the same gesture. Therefore, only on of them should be provided.

### onScrollDown

```dart
VoidCallback? onScrollDown
```

The handler for [SemanticsAction.scrollDown].

This is the semantic equivalent of a user moving their finger across the screen from top to bottom. It should be recognized by controls that are vertically scrollable.

VoiceOver users on iOS can trigger this action by swiping down with three fingers. TalkBack users on Android can trigger this action by swiping left and then right in one motion path. On Android, [onScrollDown] and [onScrollRight] share the same gesture. Therefore, only on of them should be provided.

### onIncrease

```dart
VoidCallback? onIncrease
```

The handler for [SemanticsAction.increase].

This is a request to increase the value represented by the widget. For example, this action might be recognized by a slider control.

If a [value] is set, [increasedValue] must also be provided and [onIncrease] must ensure that [value] will be set to [increasedValue].

VoiceOver users on iOS can trigger this action by swiping up with one finger. TalkBack users on Android can trigger this action by pressing the volume up button.

### onDecrease

```dart
VoidCallback? onDecrease
```

The handler for [SemanticsAction.decrease].

This is a request to decrease the value represented by the widget. For example, this action might be recognized by a slider control.

If a [value] is set, [decreasedValue] must also be provided and [onDecrease] must ensure that [value] will be set to [decreasedValue].

VoiceOver users on iOS can trigger this action by swiping down with one finger. TalkBack users on Android can trigger this action by pressing the volume down button.

### onCopy

```dart
VoidCallback? onCopy
```

The handler for [SemanticsAction.copy].

This is a request to copy the current selection to the clipboard.

TalkBack users on Android can trigger this action from the local context menu of a text field, for example.

### onCut

```dart
VoidCallback? onCut
```

The handler for [SemanticsAction.cut].

This is a request to cut the current selection and place it in the clipboard.

TalkBack users on Android can trigger this action from the local context menu of a text field, for example.

### onPaste

```dart
VoidCallback? onPaste
```

The handler for [SemanticsAction.paste].

This is a request to paste the current content of the clipboard.

TalkBack users on Android can trigger this action from the local context menu of a text field, for example.

### onMoveCursorForwardByCharacter

```dart
MoveCursorHandler? onMoveCursorForwardByCharacter
```

The handler for [SemanticsAction.moveCursorForwardByCharacter].

This handler is invoked when the user wants to move the cursor in a text field forward by one character.

TalkBack users can trigger this by pressing the volume up key while the input focus is in a text field.

### onMoveCursorBackwardByCharacter

```dart
MoveCursorHandler? onMoveCursorBackwardByCharacter
```

The handler for [SemanticsAction.moveCursorBackwardByCharacter].

This handler is invoked when the user wants to move the cursor in a text field backward by one character.

TalkBack users can trigger this by pressing the volume down key while the input focus is in a text field.

### onMoveCursorForwardByWord

```dart
MoveCursorHandler? onMoveCursorForwardByWord
```

The handler for [SemanticsAction.moveCursorForwardByWord].

This handler is invoked when the user wants to move the cursor in a text field backward by one word.

TalkBack users can trigger this by pressing the volume down key while the input focus is in a text field.

### onMoveCursorBackwardByWord

```dart
MoveCursorHandler? onMoveCursorBackwardByWord
```

The handler for [SemanticsAction.moveCursorBackwardByWord].

This handler is invoked when the user wants to move the cursor in a text field backward by one word.

TalkBack users can trigger this by pressing the volume down key while the input focus is in a text field.

### onSetSelection

```dart
SetSelectionHandler? onSetSelection
```

The handler for [SemanticsAction.setSelection].

This handler is invoked when the user either wants to change the currently selected text in a text field or change the position of the cursor.

TalkBack users can trigger this handler by selecting "Move cursor to beginning/end" or "Select all" from the local context menu.

### onSetText

```dart
SetTextHandler? onSetText
```

The handler for [SemanticsAction.setText].

This handler is invoked when the user wants to replace the current text in the text field with a new text.

Voice access users can trigger this handler by speaking `type <text>` to their Android devices.

### onDidGainAccessibilityFocus

```dart
VoidCallback? onDidGainAccessibilityFocus
```

The handler for [SemanticsAction.didGainAccessibilityFocus].

This handler is invoked when the node annotated with this handler gains the accessibility focus. The accessibility focus is the green (on Android with TalkBack) or black (on iOS with VoiceOver) rectangle shown on screen to indicate what element an accessibility user is currently interacting with.

The accessibility focus is different from the input focus. The input focus is usually held by the element that currently responds to keyboard inputs. Accessibility focus and input focus can be held by two different nodes!

See also:

- [onDidLoseAccessibilityFocus], which is invoked when the accessibility focus is removed from the node.
- [onFocus], which is invoked when the assistive technology requests that the input focus is gained by a widget.
- [FocusNode], [FocusScope], [FocusManager], which manage the input focus.

### onDidLoseAccessibilityFocus

```dart
VoidCallback? onDidLoseAccessibilityFocus
```

The handler for [SemanticsAction.didLoseAccessibilityFocus].

This handler is invoked when the node annotated with this handler loses the accessibility focus. The accessibility focus is the green (on Android with TalkBack) or black (on iOS with VoiceOver) rectangle shown on screen to indicate what element an accessibility user is currently interacting with.

The accessibility focus is different from the input focus. The input focus is usually held by the element that currently responds to keyboard inputs. Accessibility focus and input focus can be held by two different nodes!

See also:

- [onDidGainAccessibilityFocus], which is invoked when the node gains accessibility focus.
- [FocusNode], [FocusScope], [FocusManager], which manage the input focus.

### onFocus

```dart
VoidCallback? onFocus
```

{@template flutter.semantics.SemanticsProperties.onFocus} The handler for [SemanticsAction.focus].

This handler is invoked when the assistive technology requests that the focusable widget corresponding to this semantics node gain input focus. The [FocusNode] that manages the focus of the widget must gain focus. The widget must begin responding to relevant key events. For example:

- Buttons must respond to tap/click events produced via keyboard shortcuts.
- Text fields must become focused and editable, showing an on-screen keyboard, if necessary.
- Checkboxes, switches, and radio buttons must become toggleable using keyboard shortcuts.

Focus behavior is specific to the platform and to the assistive technology used. See the documentation of [SemanticsAction.focus] for more detail.

See also:

- [onDidGainAccessibilityFocus], which is invoked when the node gains accessibility focus. {@endtemplate}

### onDismiss

```dart
VoidCallback? onDismiss
```

The handler for [SemanticsAction.dismiss].

This is a request to dismiss the currently focused node.

TalkBack users on Android can trigger this action in the local context menu, and VoiceOver users on iOS can trigger this action with a standard gesture or menu option.

### onExpand

```dart
VoidCallback? onExpand
```

The handler for [SemanticsAction.expand].

This is a request to expand the currently focused node. For example, this action might be recognized by a dropdown.

This handler should only be set when the node is in a collapsed state (i.e., [expanded] is false).

### onCollapse

```dart
VoidCallback? onCollapse
```

The handler for [SemanticsAction.collapse].

This is a request to collapse the currently focused node. For example, this action might be recognized by a dropdown.

This handler should only be set when the node is in an expanded state (i.e., [expanded] is true).

### customSemanticsActions

```dart
Map<CustomSemanticsAction, VoidCallback>? customSemanticsActions
```

A map from each supported [CustomSemanticsAction] to a provided handler.

The handler associated with each custom action is called whenever a semantics action of type [SemanticsAction.customAction] is received. The provided argument will be an identifier used to retrieve an instance of a custom action which can then retrieve the correct handler from this map.

See also:

- [CustomSemanticsAction], for an explanation of custom actions.

### role

```dart
SemanticsRole? role
```

{@template flutter.semantics.SemanticsProperties.role} A enum to describe what role the subtree represents.

Setting the role for a widget subtree helps assistive technologies, such as screen readers, to understand and interact with the UI correctly.

Defaults to [SemanticsRole.none] if not set, which means the subtree does not represent any complex ui or controls.

For a list of available roles, see [SemanticsRole]. {@endtemplate}

### controlsNodes

```dart
Set<String>? controlsNodes
```

The [SemanticsNode.identifier]s of widgets controlled by this subtree.

{@template flutter.semantics.SemanticsProperties.controlsNodes} If a widget is controlling the visibility or content of another widget, for example, [Tab]s control child visibilities of [TabBarView] or [ExpansionTile] controls visibility of its expanded content, one must assign a [SemanticsNode.identifier] to the content and also provide a set of identifiers including the content's identifier to this property. {@endtemplate}

### validationResult

```dart
SemanticsValidationResult validationResult
```

{@template flutter.semantics.SemanticsProperties.validationResult} Describes the validation result for a form field represented by this widget.

Providing a validation result helps assistive technologies, such as screen readers, to communicate to the user whether they provided correct information in a form.

Defaults to [SemanticsValidationResult.none] if not set, which means no validation information is available for the respective semantics node.

For a list of available validation results, see [SemanticsValidationResult]. {@endtemplate}

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior? hitTestBehavior
```

{@template flutter.semantics.SemanticsProperties.hitTestBehavior} Describes how the semantic node should behave during hit testing.

See [ui.SemanticsHitTestBehavior] for more details. {@endtemplate}

### inputType

```dart
SemanticsInputType? inputType
```

{@template flutter.semantics.SemanticsProperties.inputType} The input type for of a editable widget.

This property is only used when the subtree represents a text field.

Assistive technologies use this property to provide better information to users. For example, screen reader reads out the input type of text field when focused. {@endtemplate}

### maxValue

```dart
String? maxValue
```

{@template flutter.semantics.SemanticsProperties.maxValue} The maximum value of the node.

Used in conjunction with [value] to define the current value and range of a node. A typical usage is for progress indicators, where [value] represents the current progress and [maxValue] defines the maximum possible value.

{@endtemplate}

### minValue

```dart
String? minValue
```

{@template flutter.semantics.SemanticsProperties.minValue} The minimum value of the node.

Used in conjunction with [value] to define the current value and range of a node. A typical usage is for progress indicators, where [value] represents the current progress and [minValue] defines the minimum possible value.

{@endtemplate}

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toStringShort()

```dart
String toStringShort()
```

# debugResetSemanticsIdCounter()

```dart
void debugResetSemanticsIdCounter()
```

In tests use this function to reset the counter used to generate [SemanticsNode.id].

# SemanticsNode

```dart
class SemanticsNode with DiagnosticableTreeMixin {}
```

A node that represents some semantic data.

The semantics tree is maintained during the semantics phase of the pipeline (i.e., during [PipelineOwner.flushSemantics]), which happens after compositing. The semantics tree is then uploaded into the engine for use by assistive technology.

### SemanticsNode()

```dart
SemanticsNode({Key? key, VoidCallback? showOnScreen})
```

Creates a semantic node.

Each semantic node has a unique identifier that is assigned when the node is created.

### SemanticsNode.root()

```dart
SemanticsNode.root({Key? key, VoidCallback? showOnScreen, required SemanticsOwner owner})
```

Creates a semantic node to represent the root of the semantics tree.

The root node is assigned an identifier of zero.

### key

```dart
Key? key
```

Uniquely identifies this node in the list of sibling nodes.

Keys are used during the construction of the semantics tree. They are not transferred to the engine.

### id

```dart
int get id
```

The unique identifier for this node.

The root node has an id of zero. Other nodes are given a unique id when they are attached to a [SemanticsOwner]. If they are detached, their ids are invalid and should not be used.

In rare circumstances, id may change if this node is detached and re-attached to the [SemanticsOwner]. This should only happen when the application has generated too many semantics nodes.

### transform

```dart
Matrix4? get transform
```

The transform from this node's coordinate system to its parent's coordinate system.

By default, the transform is null, which represents the identity transformation (i.e., that this node has the same coordinate system as its parent).

### transform

```dart
set transform(Matrix4? value)
```

### rect

```dart
Rect get rect
```

The bounding box for this node in its coordinate system.

### rect

```dart
set rect(Rect value)
```

### parentSemanticsClipRect

```dart
Rect? parentSemanticsClipRect
```

The semantic clip from an ancestor that was applied to this node.

Expressed in the coordinate system of the node. May be null if no clip has been applied.

Descendant [SemanticsNode]s that are positioned outside of this rect will be excluded from the semantics tree. Descendant [SemanticsNode]s that are overlapping with this rect, but are outside of [parentPaintClipRect] will be included in the tree, but they will be marked as hidden because they are assumed to be not visible on screen.

If this rect is null, all descendant [SemanticsNode]s outside of [parentPaintClipRect] will be excluded from the tree.

If this rect is non-null it has to completely enclose [parentPaintClipRect]. If [parentPaintClipRect] is null this property is also null.

### parentPaintClipRect

```dart
Rect? parentPaintClipRect
```

The paint clip from an ancestor that was applied to this node.

Expressed in the coordinate system of the node. May be null if no clip has been applied.

Descendant [SemanticsNode]s that are positioned outside of this rect will either be excluded from the semantics tree (if they have no overlap with [parentSemanticsClipRect]) or they will be included and marked as hidden (if they are overlapping with [parentSemanticsClipRect]).

This rect is completely enclosed by [parentSemanticsClipRect].

If this rect is null [parentSemanticsClipRect] also has to be null.

### indexInParent

```dart
int? indexInParent
```

The index of this node within the parent's list of semantic children.

This includes all semantic nodes, not just those currently in the child list. For example, if a scrollable has five children but the first two are not visible (and thus not included in the list of children), then the index of the last node will still be 4.

### isInvisible

```dart
bool get isInvisible
```

Whether the node is invisible.

A node whose [rect] is outside of the bounds of the screen and hence not reachable for users is considered invisible if its semantic information is not merged into a (partially) visible parent as indicated by [isMergedIntoParent].

An invisible node can be safely dropped from the semantic tree without losing semantic information that is relevant for describing the content currently shown on screen.

### isMergedIntoParent

```dart
bool get isMergedIntoParent
```

Whether this node merges its semantic information into an ancestor node.

This value indicates whether this node has any ancestors with [mergeAllDescendantsIntoThisNode] set to true.

### isMergedIntoParent

```dart
set isMergedIntoParent(bool value)
```

### areUserActionsBlocked

```dart
bool get areUserActionsBlocked
```

Whether the user can interact with this node in assistive technologies.

This node can still receive accessibility focus even if this is true. Setting this to true prevents the user from activating pointer related [SemanticsAction]s, such as [SemanticsAction.tap] or [SemanticsAction.longPress].

### areUserActionsBlocked

```dart
set areUserActionsBlocked(bool value)
```

### isPartOfNodeMerging

```dart
bool get isPartOfNodeMerging
```

Whether this node is taking part in a merge of semantic information.

This returns true if the node is either merged into an ancestor node or if decedent nodes are merged into this node.

See also:

- [isMergedIntoParent]
- [mergeAllDescendantsIntoThisNode]

### mergeAllDescendantsIntoThisNode

```dart
bool get mergeAllDescendantsIntoThisNode
```

Whether this node and all of its descendants should be treated as one logical entity.

### hasChildren

```dart
bool get hasChildren
```

Whether this node has a non-zero number of children.

### childrenCount

```dart
int get childrenCount
```

The number of children this node has in hit-test(paint) order.

### childrenCountInTraversalOrder

```dart
int get childrenCountInTraversalOrder
```

The number of children this node has in traversal order.

### visitChildren()

```dart
void visitChildren(SemanticsNodeVisitor visitor)
```

Visits the immediate children of this node.

This function calls visitor for each immediate child until visitor returns false.

### owner

```dart
SemanticsOwner? get owner
```

The owner for this node (null if unattached).

The entire semantics tree that this node belongs to will have the same owner.

### attached

```dart
bool get attached
```

Whether the semantics tree this node belongs to is attached to a [SemanticsOwner].

This becomes true during the call to [attach].

This becomes false during the call to [detach].

### parent

```dart
SemanticsNode? get parent
```

The parent of this node in the semantics tree.

The [parent] of the root node in the semantics tree is null.

### traversalParent

```dart
SemanticsNode? get traversalParent
```

The real parent of this node in traversal order.

This is useful for an [OverlayPortal] or a similar scenario where the node's hit-test parent (i.e., [parent]) and its traversal parent (i.e., [traversalParent]) are different. If this node indicates an overlay portal child, [traversalParent] is its overlay portal parent node in traversal order. Otherwise, it is the same as [parent]. The [traversalParent] is used when the transform of this node needs to be updated in traversal order.

### traversalParent

```dart
set traversalParent(SemanticsNode? value)
```

### depth

```dart
int get depth
```

The depth of this node in the semantics tree.

The depth of nodes in a tree monotonically increases as you traverse down the tree. There's no guarantee regarding depth between siblings.

The depth is used to ensure that nodes are processed in depth order.

### attach()

```dart
void attach(SemanticsOwner owner)
```

Mark this node as attached to the given owner.

### detach()

```dart
void detach()
```

Mark this node as detached from its owner.

### debugIsDirty

```dart
bool? get debugIsDirty
```

When asserts are enabled, returns whether node is marked as dirty.

Otherwise, returns null.

This getter is intended for use in framework unit tests. Applications must not depend on its value.

### tags

```dart
Set<SemanticsTag>? tags
```

The [SemanticsTag]s this node is tagged with.

Tags are used during the construction of the semantics tree. They are not transferred to the engine.

### isTagged()

```dart
bool isTagged(SemanticsTag tag)
```

Whether this node is tagged with `tag`.

### flagsCollection

```dart
SemanticsFlags get flagsCollection
```

Semantics flags.

### hasFlag()

```dart
bool hasFlag(SemanticsFlag flag)
```

Whether this node currently has a given [SemanticsFlag].

### identifier

```dart
String get identifier
```

{@macro flutter.semantics.SemanticsProperties.identifier}

### traversalParentIdentifier

```dart
Object? get traversalParentIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalParentIdentifier}

### traversalChildIdentifier

```dart
Object? get traversalChildIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalChildIdentifier}

### label

```dart
String get label
```

A textual description of this node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedLabel].

### attributedLabel

```dart
AttributedString get attributedLabel
```

A textual description of this node in [AttributedString] format.

The reading direction is given by [textDirection].

See also [label], which exposes just the raw text.

### value

```dart
String get value
```

A textual description for the current value of the node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedValue].

### attributedValue

```dart
AttributedString get attributedValue
```

A textual description for the current value of the node in [AttributedString] format.

The reading direction is given by [textDirection].

See also [value], which exposes just the raw text.

### increasedValue

```dart
String get increasedValue
```

The value that [value] will have after a [SemanticsAction.increase] action has been performed.

This property is only valid if the [SemanticsAction.increase] action is available on this node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedIncreasedValue].

### attributedIncreasedValue

```dart
AttributedString get attributedIncreasedValue
```

The value in [AttributedString] format that [value] or [attributedValue] will have after a [SemanticsAction.increase] action has been performed.

This property is only valid if the [SemanticsAction.increase] action is available on this node.

The reading direction is given by [textDirection].

See also [increasedValue], which exposes just the raw text.

### decreasedValue

```dart
String get decreasedValue
```

The value that [value] will have after a [SemanticsAction.decrease] action has been performed.

This property is only valid if the [SemanticsAction.decrease] action is available on this node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedDecreasedValue].

### attributedDecreasedValue

```dart
AttributedString get attributedDecreasedValue
```

The value in [AttributedString] format that [value] or [attributedValue] will have after a [SemanticsAction.decrease] action has been performed.

This property is only valid if the [SemanticsAction.decrease] action is available on this node.

The reading direction is given by [textDirection].

See also [decreasedValue], which exposes just the raw text.

### hint

```dart
String get hint
```

A brief description of the result of performing an action on this node.

The reading direction is given by [textDirection].

This exposes the raw text of the [attributedHint].

### attributedHint

```dart
AttributedString get attributedHint
```

A brief description of the result of performing an action on this node in [AttributedString] format.

The reading direction is given by [textDirection].

See also [hint], which exposes just the raw text.

### tooltip

```dart
String get tooltip
```

A textual description of the widget's tooltip.

The reading direction is given by [textDirection].

### hintOverrides

```dart
SemanticsHintOverrides? get hintOverrides
```

Provides hint values which override the default hints on supported platforms.

### textDirection

```dart
TextDirection? get textDirection
```

The reading direction for [label], [value], [hint], [increasedValue], and [decreasedValue].

### sortKey

```dart
SemanticsSortKey? get sortKey
```

Determines the position of this node among its siblings in the traversal sort order.

This is used to describe the order in which the semantic node should be traversed by the accessibility services on the platform (e.g. VoiceOver on iOS and TalkBack on Android).

### textSelection

```dart
TextSelection? get textSelection
```

The currently selected text (or the position of the cursor) within [value] if this node represents a text field.

### isMultiline

```dart
bool? get isMultiline
```

If this node represents a text field, this indicates whether or not it's a multiline text field.

### scrollChildCount

```dart
int? get scrollChildCount
```

The total number of scrollable children that contribute to semantics.

If the number of children are unknown or unbounded, this value will be null.

### scrollIndex

```dart
int? get scrollIndex
```

The index of the first visible semantic child of a scroll node.

### scrollPosition

```dart
double? get scrollPosition
```

Indicates the current scrolling position in logical pixels if the node is scrollable.

The properties [scrollExtentMin] and [scrollExtentMax] indicate the valid in-range values for this property. The value for [scrollPosition] may (temporarily) be outside that range, e.g. during an overscroll.

See also:

- [ScrollPosition.pixels], from where this value is usually taken.

### scrollExtentMax

```dart
double? get scrollExtentMax
```

Indicates the maximum in-range value for [scrollPosition] if the node is scrollable.

This value may be infinity if the scroll is unbound.

See also:

- [ScrollPosition.maxScrollExtent], from where this value is usually taken.

### scrollExtentMin

```dart
double? get scrollExtentMin
```

Indicates the minimum in-range value for [scrollPosition] if the node is scrollable.

This value may be infinity if the scroll is unbound.

See also:

- [ScrollPosition.minScrollExtent] from where this value is usually taken.

### platformViewId

```dart
int? get platformViewId
```

The id of the platform view, whose semantics nodes will be added as children to this node.

If this value is non-null, the SemanticsNode must not have any children as those would be replaced by the semantics nodes of the referenced platform view.

See also:

- [AndroidView], which is the platform view for Android.
- [UiKitView], which is the platform view for iOS.

### maxValueLength

```dart
int? get maxValueLength
```

The maximum number of characters that can be entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [SemanticsFlag.isTextField] is set. Defaults to null, which means no limit is imposed on the text field.

### currentValueLength

```dart
int? get currentValueLength
```

The current number of characters that have been entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [SemanticsFlag.isTextField] is set. Must be set when [maxValueLength] is set.

### headingLevel

```dart
int get headingLevel
```

The level of the widget as a heading within the structural hierarchy of the screen. A value of 1 indicates the highest level of structural hierarchy. A value of 2 indicates the next level, and so on.

### linkUrl

```dart
Uri? get linkUrl
```

The URL that this node links to.

### role

```dart
SemanticsRole get role
```

{@template flutter.semantics.SemanticsNode.role} The role this node represents

A semantics node's role helps assistive technologies, such as screen readers, understand and interact with the UI correctly.

For a list of possible roles, see [SemanticsRole]. {@endtemplate}

### controlsNodes

```dart
Set<String>? get controlsNodes
```

{@template flutter.semantics.SemanticsNode.controlsNodes} The [SemanticsNode.identifier]s of widgets controlled by this node. {@endtemplate}

{@macro flutter.semantics.SemanticsProperties.controlsNodes}

### minValue

```dart
String? get minValue
```

{@macro flutter.semantics.SemanticsProperties.minValue}

### maxValue

```dart
String? get maxValue
```

{@macro flutter.semantics.SemanticsProperties.maxValue}

### validationResult

```dart
SemanticsValidationResult get validationResult
```

{@macro flutter.semantics.SemanticsProperties.validationResult}

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior get hitTestBehavior
```

{@macro flutter.semantics.SemanticsProperties.hitTestBehavior}

### inputType

```dart
SemanticsInputType get inputType
```

{@template flutter.semantics.SemanticsNode.inputType} The input type for of a editable node.

This property is only used when this node represents a text field.

Assistive technologies use this property to provide better information to users. For example, screen reader reads out the input type of text field when focused. {@endtemplate}

### updateWith()

```dart
void updateWith({required SemanticsConfiguration? config, List<SemanticsNode>? childrenInInversePaintOrder})
```

Reconfigures the properties of this object to describe the configuration provided in the `config` argument and the children listed in the `childrenInInversePaintOrder` argument.

The arguments may be null; this represents an empty configuration (all values at their defaults, no children).

No reference is kept to the [SemanticsConfiguration] object, but the child list is used as-is and should therefore not be changed after this call.

### getSemanticsData()

```dart
SemanticsData getSemanticsData()
```

Returns a summary of the semantics for this node.

If this node has [mergeAllDescendantsIntoThisNode], then the returned data includes the information from this node's descendants. Otherwise, the returned data matches the data on this node.

### sendEvent()

```dart
void sendEvent(SemanticsEvent event)
```

Sends a [SemanticsEvent] associated with this [SemanticsNode].

Semantics events should be sent to inform interested parties (like the accessibility system of the operating system) about changes to the UI.

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toStringDeep()

```dart
String toStringDeep({String prefixLineOne = '', String? prefixOtherLines, DiagnosticLevel minLevel = DiagnosticLevel.debug, DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder, int wrapWidth = 65})
```

Returns a string representation of this node and its descendants.

The order in which the children of the [SemanticsNode] will be printed is controlled by the [childOrder] parameter.

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style = DiagnosticsTreeStyle.sparse, DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder})
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren({DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder})
```

### debugListChildrenInOrder()

```dart
List<SemanticsNode> debugListChildrenInOrder(DebugSemanticsDumpOrder childOrder)
```

Returns the list of direct children of this node in the specified order.

# SemanticsOwner

```dart
class SemanticsOwner extends ChangeNotifier {}
```

Owns [SemanticsNode] objects and notifies listeners of changes to the render tree semantics.

To listen for semantic updates, call [SemanticsBinding.ensureSemantics] or [PipelineOwner.ensureSemantics] to obtain a [SemanticsHandle]. This will create a [SemanticsOwner] if necessary.

### SemanticsOwner()

```dart
SemanticsOwner({required SemanticsUpdateCallback onSemanticsUpdate})
```

Creates a [SemanticsOwner] that manages zero or more [SemanticsNode] objects.

### onSemanticsUpdate

```dart
SemanticsUpdateCallback onSemanticsUpdate
```

The [onSemanticsUpdate] callback is expected to dispatch [SemanticsUpdate]s to the [FlutterView] that is associated with this [PipelineOwner] and/or [SemanticsOwner].

A [SemanticsOwner] calls [onSemanticsUpdate] during [sendSemanticsUpdate] after the [SemanticsUpdate] has been build, but before the [SemanticsOwner]'s listeners have been notified.

### rootSemanticsNode

```dart
SemanticsNode? get rootSemanticsNode
```

The root node of the semantics tree, if any.

If the semantics tree is empty, returns null.

### getSemanticsNode()

```dart
SemanticsNode? getSemanticsNode(int id)
```

Returns the [SemanticsNode] with the given [id], if any.

### dispose()

```dart
void dispose()
```

### sendSemanticsUpdate()

```dart
void sendSemanticsUpdate()
```

Update the semantics using [onSemanticsUpdate].

### performAction()

```dart
void performAction(int id, SemanticsAction action, [Object? args])
```

Asks the [SemanticsNode] with the given id to perform the given action.

If the [SemanticsNode] has not indicated that it can perform the action, this function does nothing.

If the given `action` requires arguments they need to be passed in via the `args` parameter.

### performActionAt()

```dart
void performActionAt(Offset position, SemanticsAction action, [Object? args])
```

Asks the [SemanticsNode] at the given position to perform the given action.

If the [SemanticsNode] has not indicated that it can perform the action, this function does nothing.

If the given `action` requires arguments they need to be passed in via the `args` parameter.

### toString()

```dart
String toString()
```

# SemanticsConfiguration

```dart
class SemanticsConfiguration {}
```

Describes the semantic information associated with the owning [RenderObject].

The information provided in the configuration is used to generate the semantics tree.

### isSemanticBoundary

```dart
bool get isSemanticBoundary
```

Whether the [RenderObject] owner of this configuration wants to own its own [SemanticsNode].

When set to true semantic information associated with the [RenderObject] owner of this configuration or any of its descendants will not leak into parents. The [SemanticsNode] generated out of this configuration will act as a boundary.

Whether descendants of the owning [RenderObject] can add their semantic information to the [SemanticsNode] introduced by this configuration is controlled by [explicitChildNodes].

This has to be true if [isMergingSemanticsOfDescendants] is also true.

### isSemanticBoundary

```dart
set isSemanticBoundary(bool value)
```

### localeForSubtree

```dart
Locale? get localeForSubtree
```

The locale for widgets in the subtree.

### localeForSubtree

```dart
set localeForSubtree(Locale? value)
```

### locale

```dart
Locale? locale
```

The locale of the resulting semantics node if this configuration formed one.

This is used internally to track the inherited locale from parent rendering object and should not be used directly.

To set a locale for a rendering object, use [localeForSubtree] instead.

### isBlockingUserActions

```dart
bool isBlockingUserActions
```

Whether to block pointer related user actions for the rendering subtree.

Setting this to true will prevent users from interacting with the rendering object produces this semantics configuration and its subtree through pointer-related [SemanticsAction]s in assistive technologies.

The [SemanticsNode] created from this semantics configuration is still focusable by assistive technologies. Only pointer-related [SemanticsAction]s, such as [SemanticsAction.tap] or its friends, are blocked.

If this semantics configuration is merged into a parent semantics node, only the [SemanticsAction]s from this rendering object and the rendering objects in the subtree are blocked.

### explicitChildNodes

```dart
bool explicitChildNodes
```

Whether the configuration forces all children of the owning [RenderObject] that want to contribute semantic information to the semantics tree to do so in the form of explicit [SemanticsNode]s.

When set to false children of the owning [RenderObject] are allowed to annotate [SemanticsNode]s of their parent with the semantic information they want to contribute to the semantic tree. When set to true the only way for children of the owning [RenderObject] to contribute semantic information to the semantic tree is to introduce new explicit [SemanticsNode]s to the tree.

This setting is often used in combination with [isSemanticBoundary] to create semantic boundaries that are either writable or not for children.

### isBlockingSemanticsOfPreviouslyPaintedNodes

```dart
bool isBlockingSemanticsOfPreviouslyPaintedNodes
```

Whether the owning [RenderObject] makes other [RenderObject]s previously painted within the same semantic boundary unreachable for accessibility purposes.

If set to true, the semantic information for all siblings and cousins of this node, that are earlier in a depth-first pre-order traversal, are dropped from the semantics tree up until a semantic boundary (as defined by [isSemanticBoundary]) is reached.

If [isSemanticBoundary] and [isBlockingSemanticsOfPreviouslyPaintedNodes] is set on the same node, all previously painted siblings and cousins up until the next ancestor that is a semantic boundary are dropped.

Paint order as established by [RenderObject.visitChildrenForSemantics] is used to determine if a node is previous to this one.

### hasBeenAnnotated

```dart
bool get hasBeenAnnotated
```

Whether this configuration is empty.

An empty configuration doesn't contain any semantic information that it wants to contribute to the semantics tree.

### onTap

```dart
VoidCallback? get onTap
```

The handler for [SemanticsAction.tap].

This is the semantic equivalent of a user briefly tapping the screen with the finger without moving it. For example, a button should implement this action.

VoiceOver users on iOS and TalkBack users on Android can trigger this action by double-tapping the screen while an element is focused.

On Android prior to Android Oreo a double-tap on the screen while an element with an [onTap] handler is focused will not call the registered handler. Instead, Android will simulate a pointer down and up event at the center of the focused element. Those pointer events will get dispatched just like a regular tap with TalkBack disabled would: The events will get processed by any [GestureDetector] listening for gestures in the center of the focused element. Therefore, to ensure that [onTap] handlers work properly on Android versions prior to Oreo, a [GestureDetector] with an onTap handler should always be wrapping an element that defines a semantic [onTap] handler. By default a [GestureDetector] will register its own semantic [onTap] handler that follows this principle.

### onTap

```dart
set onTap(VoidCallback? value)
```

### onLongPress

```dart
VoidCallback? get onLongPress
```

The handler for [SemanticsAction.longPress].

This is the semantic equivalent of a user pressing and holding the screen with the finger for a few seconds without moving it.

VoiceOver users on iOS and TalkBack users on Android can trigger this action by double-tapping the screen without lifting the finger after the second tap.

### onLongPress

```dart
set onLongPress(VoidCallback? value)
```

### onScrollLeft

```dart
VoidCallback? get onScrollLeft
```

The handler for [SemanticsAction.scrollLeft].

This is the semantic equivalent of a user moving their finger across the screen from right to left. It should be recognized by controls that are horizontally scrollable.

VoiceOver users on iOS can trigger this action by swiping left with three fingers. TalkBack users on Android can trigger this action by swiping right and then left in one motion path. On Android, [onScrollUp] and [onScrollLeft] share the same gesture. Therefore, only on of them should be provided.

### onScrollLeft

```dart
set onScrollLeft(VoidCallback? value)
```

### onDismiss

```dart
VoidCallback? get onDismiss
```

The handler for [SemanticsAction.dismiss].

This is a request to dismiss the currently focused node.

TalkBack users on Android can trigger this action in the local context menu, and VoiceOver users on iOS can trigger this action with a standard gesture or menu option.

### onDismiss

```dart
set onDismiss(VoidCallback? value)
```

### onScrollRight

```dart
VoidCallback? get onScrollRight
```

The handler for [SemanticsAction.scrollRight].

This is the semantic equivalent of a user moving their finger across the screen from left to right. It should be recognized by controls that are horizontally scrollable.

VoiceOver users on iOS can trigger this action by swiping right with three fingers. TalkBack users on Android can trigger this action by swiping left and then right in one motion path. On Android, [onScrollDown] and [onScrollRight] share the same gesture. Therefore, only on of them should be provided.

### onScrollRight

```dart
set onScrollRight(VoidCallback? value)
```

### onScrollUp

```dart
VoidCallback? get onScrollUp
```

The handler for [SemanticsAction.scrollUp].

This is the semantic equivalent of a user moving their finger across the screen from bottom to top. It should be recognized by controls that are vertically scrollable.

VoiceOver users on iOS can trigger this action by swiping up with three fingers. TalkBack users on Android can trigger this action by swiping right and then left in one motion path. On Android, [onScrollUp] and [onScrollLeft] share the same gesture. Therefore, only on of them should be provided.

### onScrollUp

```dart
set onScrollUp(VoidCallback? value)
```

### onScrollDown

```dart
VoidCallback? get onScrollDown
```

The handler for [SemanticsAction.scrollDown].

This is the semantic equivalent of a user moving their finger across the screen from top to bottom. It should be recognized by controls that are vertically scrollable.

VoiceOver users on iOS can trigger this action by swiping down with three fingers. TalkBack users on Android can trigger this action by swiping left and then right in one motion path. On Android, [onScrollDown] and [onScrollRight] share the same gesture. Therefore, only on of them should be provided.

### onScrollDown

```dart
set onScrollDown(VoidCallback? value)
```

### onScrollToOffset

```dart
ScrollToOffsetHandler? get onScrollToOffset
```

The handler for [SemanticsAction.scrollToOffset].

This handler is only called on iOS by UIKit, when the iOS focus engine switches its focus to an item too close to a scrollable edge of a scrollable container, to make sure the focused item is always fully visible.

The callback, if not `null`, should typically set the scroll offset of the associated scrollable container to the given `targetOffset` without animation as it is already animated by the caller: the iOS focus engine invokes [onScrollToOffset] every frame during the scroll animation with animated scroll offset values.

### onScrollToOffset

```dart
set onScrollToOffset(ScrollToOffsetHandler? value)
```

### onIncrease

```dart
VoidCallback? get onIncrease
```

The handler for [SemanticsAction.increase].

This is a request to increase the value represented by the widget. For example, this action might be recognized by a slider control.

If [value] is set, [increasedValue] must also be provided and [onIncrease] must ensure that [value] will be set to [increasedValue].

VoiceOver users on iOS can trigger this action by swiping up with one finger. TalkBack users on Android can trigger this action by pressing the volume up button.

### onIncrease

```dart
set onIncrease(VoidCallback? value)
```

### onDecrease

```dart
VoidCallback? get onDecrease
```

The handler for [SemanticsAction.decrease].

This is a request to decrease the value represented by the widget. For example, this action might be recognized by a slider control.

If [value] is set, [decreasedValue] must also be provided and [onDecrease] must ensure that [value] will be set to [decreasedValue].

VoiceOver users on iOS can trigger this action by swiping down with one finger. TalkBack users on Android can trigger this action by pressing the volume down button.

### onDecrease

```dart
set onDecrease(VoidCallback? value)
```

### onCopy

```dart
VoidCallback? get onCopy
```

The handler for [SemanticsAction.copy].

This is a request to copy the current selection to the clipboard.

TalkBack users on Android can trigger this action from the local context menu of a text field, for example.

### onCopy

```dart
set onCopy(VoidCallback? value)
```

### onCut

```dart
VoidCallback? get onCut
```

The handler for [SemanticsAction.cut].

This is a request to cut the current selection and place it in the clipboard.

TalkBack users on Android can trigger this action from the local context menu of a text field, for example.

### onCut

```dart
set onCut(VoidCallback? value)
```

### onPaste

```dart
VoidCallback? get onPaste
```

The handler for [SemanticsAction.paste].

This is a request to paste the current content of the clipboard.

TalkBack users on Android can trigger this action from the local context menu of a text field, for example.

### onPaste

```dart
set onPaste(VoidCallback? value)
```

### onShowOnScreen

```dart
VoidCallback? get onShowOnScreen
```

The handler for [SemanticsAction.showOnScreen].

A request to fully show the semantics node on screen. For example, this action might be send to a node in a scrollable list that is partially off screen to bring it on screen.

For elements in a scrollable list the framework provides a default implementation for this action and it is not advised to provide a custom one via this setter.

### onShowOnScreen

```dart
set onShowOnScreen(VoidCallback? value)
```

### onMoveCursorForwardByCharacter

```dart
MoveCursorHandler? get onMoveCursorForwardByCharacter
```

The handler for [SemanticsAction.moveCursorForwardByCharacter].

This handler is invoked when the user wants to move the cursor in a text field forward by one character.

TalkBack users can trigger this by pressing the volume up key while the input focus is in a text field.

### onMoveCursorForwardByCharacter

```dart
set onMoveCursorForwardByCharacter(MoveCursorHandler? value)
```

### onMoveCursorBackwardByCharacter

```dart
MoveCursorHandler? get onMoveCursorBackwardByCharacter
```

The handler for [SemanticsAction.moveCursorBackwardByCharacter].

This handler is invoked when the user wants to move the cursor in a text field backward by one character.

TalkBack users can trigger this by pressing the volume down key while the input focus is in a text field.

### onMoveCursorBackwardByCharacter

```dart
set onMoveCursorBackwardByCharacter(MoveCursorHandler? value)
```

### onMoveCursorForwardByWord

```dart
MoveCursorHandler? get onMoveCursorForwardByWord
```

The handler for [SemanticsAction.moveCursorForwardByWord].

This handler is invoked when the user wants to move the cursor in a text field backward by one word.

TalkBack users can trigger this by pressing the volume down key while the input focus is in a text field.

### onMoveCursorForwardByWord

```dart
set onMoveCursorForwardByWord(MoveCursorHandler? value)
```

### onMoveCursorBackwardByWord

```dart
MoveCursorHandler? get onMoveCursorBackwardByWord
```

The handler for [SemanticsAction.moveCursorBackwardByWord].

This handler is invoked when the user wants to move the cursor in a text field backward by one word.

TalkBack users can trigger this by pressing the volume down key while the input focus is in a text field.

### onMoveCursorBackwardByWord

```dart
set onMoveCursorBackwardByWord(MoveCursorHandler? value)
```

### onSetSelection

```dart
SetSelectionHandler? get onSetSelection
```

The handler for [SemanticsAction.setSelection].

This handler is invoked when the user either wants to change the currently selected text in a text field or change the position of the cursor.

TalkBack users can trigger this handler by selecting "Move cursor to beginning/end" or "Select all" from the local context menu.

### onSetSelection

```dart
set onSetSelection(SetSelectionHandler? value)
```

### onSetText

```dart
SetTextHandler? get onSetText
```

The handler for [SemanticsAction.setText].

This handler is invoked when the user wants to replace the current text in the text field with a new text.

Voice access users can trigger this handler by speaking `type <text>` to their Android devices.

### onSetText

```dart
set onSetText(SetTextHandler? value)
```

### onDidGainAccessibilityFocus

```dart
VoidCallback? get onDidGainAccessibilityFocus
```

The handler for [SemanticsAction.didGainAccessibilityFocus].

This handler is invoked when the node annotated with this handler gains the accessibility focus. The accessibility focus is the green (on Android with TalkBack) or black (on iOS with VoiceOver) rectangle shown on screen to indicate what element an accessibility user is currently interacting with.

The accessibility focus is different from the input focus. The input focus is usually held by the element that currently responds to keyboard inputs. Accessibility focus and input focus can be held by two different nodes!

See also:

- [onDidLoseAccessibilityFocus], which is invoked when the accessibility focus is removed from the node.
- [FocusNode], [FocusScope], [FocusManager], which manage the input focus.

### onDidGainAccessibilityFocus

```dart
set onDidGainAccessibilityFocus(VoidCallback? value)
```

### onDidLoseAccessibilityFocus

```dart
VoidCallback? get onDidLoseAccessibilityFocus
```

The handler for [SemanticsAction.didLoseAccessibilityFocus].

This handler is invoked when the node annotated with this handler loses the accessibility focus. The accessibility focus is the green (on Android with TalkBack) or black (on iOS with VoiceOver) rectangle shown on screen to indicate what element an accessibility user is currently interacting with.

The accessibility focus is different from the input focus. The input focus is usually held by the element that currently responds to keyboard inputs. Accessibility focus and input focus can be held by two different nodes!

See also:

- [onDidGainAccessibilityFocus], which is invoked when the node gains accessibility focus.
- [FocusNode], [FocusScope], [FocusManager], which manage the input focus.

### onDidLoseAccessibilityFocus

```dart
set onDidLoseAccessibilityFocus(VoidCallback? value)
```

### onFocus

```dart
VoidCallback? get onFocus
```

{@macro flutter.semantics.SemanticsProperties.onFocus}

### onFocus

```dart
set onFocus(VoidCallback? value)
```

### onExpand

```dart
VoidCallback? get onExpand
```

The handler for [SemanticsAction.expand].

This is a request to expand the currently focused node.

### onExpand

```dart
set onExpand(VoidCallback? value)
```

### onCollapse

```dart
VoidCallback? get onCollapse
```

The handler for [SemanticsAction.collapse].

This is a request to collapse the currently focused node.

### onCollapse

```dart
set onCollapse(VoidCallback? value)
```

### childConfigurationsDelegate

```dart
ChildSemanticsConfigurationsDelegate? get childConfigurationsDelegate
```

A delegate that decides how to handle [SemanticsConfiguration]s produced in the widget subtree.

The [SemanticsConfiguration]s are produced by rendering objects in the subtree and want to merge up to their parent. This delegate can decide which of these should be merged together to form sibling SemanticsNodes and which of them should be merged upwards into the parent SemanticsNode.

The input list of [SemanticsConfiguration]s can be empty if the rendering object of this semantics configuration is a leaf node or child rendering objects do not contribute to the semantics.

### childConfigurationsDelegate

```dart
set childConfigurationsDelegate(ChildSemanticsConfigurationsDelegate? value)
```

### getActionHandler()

```dart
SemanticsActionHandler? getActionHandler(SemanticsAction action)
```

Returns the action handler registered for [action] or null if none was registered.

### sortKey

```dart
SemanticsSortKey? get sortKey
```

Determines the position of this node among its siblings in the traversal sort order.

This is used to describe the order in which the semantic node should be traversed by the accessibility services on the platform (e.g. VoiceOver on iOS and TalkBack on Android).

Whether this sort key has an effect on the [SemanticsNode] sort order is subject to how this configuration is used. For example, the [absorb] method may decide to not use this key when it combines multiple [SemanticsConfiguration] objects.

### sortKey

```dart
set sortKey(SemanticsSortKey? value)
```

### indexInParent

```dart
int? get indexInParent
```

The index of this node within the parent's list of semantic children.

This includes all semantic nodes, not just those currently in the child list. For example, if a scrollable has five children but the first two are not visible (and thus not included in the list of children), then the index of the last node will still be 4.

### indexInParent

```dart
set indexInParent(int? value)
```

### scrollChildCount

```dart
int? get scrollChildCount
```

The total number of scrollable children that contribute to semantics.

If the number of children are unknown or unbounded, this value will be null.

### scrollChildCount

```dart
set scrollChildCount(int? value)
```

### scrollIndex

```dart
int? get scrollIndex
```

The index of the first visible scrollable child that contributes to semantics.

### scrollIndex

```dart
set scrollIndex(int? value)
```

### platformViewId

```dart
int? get platformViewId
```

The id of the platform view, whose semantics nodes will be added as children to this node.

### platformViewId

```dart
set platformViewId(int? value)
```

### maxValueLength

```dart
int? get maxValueLength
```

The maximum number of characters that can be entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [isTextField] is true. Defaults to null, which means no limit is imposed on the text field.

### maxValueLength

```dart
set maxValueLength(int? value)
```

### currentValueLength

```dart
int? get currentValueLength
```

The current number of characters that have been entered into an editable text field.

For the purpose of this function a character is defined as one Unicode scalar value.

This should only be set when [isTextField] is true. Must be set when [maxValueLength] is set.

### currentValueLength

```dart
set currentValueLength(int? value)
```

### isMergingSemanticsOfDescendants

```dart
bool get isMergingSemanticsOfDescendants
```

Whether the semantic information provided by the owning [RenderObject] and all of its descendants should be treated as one logical entity.

If set to true, the descendants of the owning [RenderObject]'s [SemanticsNode] will merge their semantic information into the [SemanticsNode] representing the owning [RenderObject].

Setting this to true requires that [isSemanticBoundary] is also true.

### isMergingSemanticsOfDescendants

```dart
set isMergingSemanticsOfDescendants(bool value)
```

### customSemanticsActions

```dart
Map<CustomSemanticsAction, VoidCallback> get customSemanticsActions
```

The handlers for each supported [CustomSemanticsAction].

Whenever a custom accessibility action is added to a node, the action [SemanticsAction.customAction] is automatically added. A handler is created which uses the passed argument to lookup the custom action handler from this map and invoke it, if present.

### customSemanticsActions

```dart
set customSemanticsActions(Map<CustomSemanticsAction, VoidCallback> value)
```

### identifier

```dart
String get identifier
```

{@macro flutter.semantics.SemanticsProperties.identifier}

### identifier

```dart
set identifier(String identifier)
```

### traversalParentIdentifier

```dart
Object? get traversalParentIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalParentIdentifier}

### traversalParentIdentifier

```dart
set traversalParentIdentifier(Object? value)
```

### traversalChildIdentifier

```dart
Object? get traversalChildIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalChildIdentifier}

### traversalChildIdentifier

```dart
set traversalChildIdentifier(Object? value)
```

### role

```dart
SemanticsRole get role
```

{@macro flutter.semantics.SemanticsProperties.role}

### role

```dart
set role(SemanticsRole value)
```

### label

```dart
String get label
```

A textual description of the owning [RenderObject].

Setting this attribute will override the [attributedLabel].

The reading direction is given by [textDirection].

See also:

- [attributedLabel], which is the [AttributedString] of this property.

### label

```dart
set label(String label)
```

### attributedLabel

```dart
AttributedString get attributedLabel
```

A textual description of the owning [RenderObject] in [AttributedString] format.

On iOS this is used for the `accessibilityAttributedLabel` property defined in the `UIAccessibility` Protocol. On Android it is concatenated together with [attributedValue] and [attributedHint] in the following order: [attributedValue], [attributedLabel], [attributedHint]. The concatenated value is then used as the `Text` description.

The reading direction is given by [textDirection].

See also:

- [label], which is the raw text of this property.

### attributedLabel

```dart
set attributedLabel(AttributedString attributedLabel)
```

### value

```dart
String get value
```

A textual description for the current value of the owning [RenderObject].

Setting this attribute will override the [attributedValue].

The reading direction is given by [textDirection].

See also:

- [attributedValue], which is the [AttributedString] of this property.
- [increasedValue] and [attributedIncreasedValue], which describe what [value] will be after performing [SemanticsAction.increase].
- [decreasedValue] and [attributedDecreasedValue], which describe what [value] will be after performing [SemanticsAction.decrease].

### value

```dart
set value(String value)
```

### attributedValue

```dart
AttributedString get attributedValue
```

A textual description for the current value of the owning [RenderObject] in [AttributedString] format.

On iOS this is used for the `accessibilityAttributedValue` property defined in the `UIAccessibility` Protocol. On Android it is concatenated together with [attributedLabel] and [attributedHint] in the following order: [attributedValue], [attributedLabel], [attributedHint]. The concatenated value is then used as the `Text` description.

The reading direction is given by [textDirection].

See also:

- [value], which is the raw text of this property.
- [attributedIncreasedValue], which describes what [value] will be after performing [SemanticsAction.increase].
- [attributedDecreasedValue], which describes what [value] will be after performing [SemanticsAction.decrease].

### attributedValue

```dart
set attributedValue(AttributedString attributedValue)
```

### increasedValue

```dart
String get increasedValue
```

The value that [value] will have after performing a [SemanticsAction.increase] action.

Setting this attribute will override the [attributedIncreasedValue].

One of the [attributedIncreasedValue] or [increasedValue] must be set if a handler for [SemanticsAction.increase] is provided and one of the [value] or [attributedValue] is set.

The reading direction is given by [textDirection].

See also:

- [attributedIncreasedValue], which is the [AttributedString] of this property.

### increasedValue

```dart
set increasedValue(String increasedValue)
```

### attributedIncreasedValue

```dart
AttributedString get attributedIncreasedValue
```

The value that [value] will have after performing a [SemanticsAction.increase] action in [AttributedString] format.

One of the [attributedIncreasedValue] or [increasedValue] must be set if a handler for [SemanticsAction.increase] is provided and one of the [value] or [attributedValue] is set.

The reading direction is given by [textDirection].

See also:

- [increasedValue], which is the raw text of this property.

### attributedIncreasedValue

```dart
set attributedIncreasedValue(AttributedString attributedIncreasedValue)
```

### decreasedValue

```dart
String get decreasedValue
```

The value that [value] will have after performing a [SemanticsAction.decrease] action.

Setting this attribute will override the [attributedDecreasedValue].

One of the [attributedDecreasedValue] or [decreasedValue] must be set if a handler for [SemanticsAction.decrease] is provided and one of the [value] or [attributedValue] is set.

The reading direction is given by [textDirection].

- [attributedDecreasedValue], which is the [AttributedString] of this property.

### decreasedValue

```dart
set decreasedValue(String decreasedValue)
```

### attributedDecreasedValue

```dart
AttributedString get attributedDecreasedValue
```

The value that [value] will have after performing a [SemanticsAction.decrease] action in [AttributedString] format.

One of the [attributedDecreasedValue] or [decreasedValue] must be set if a handler for [SemanticsAction.decrease] is provided and one of the [value] or [attributedValue] is set.

The reading direction is given by [textDirection].

See also:

- [decreasedValue], which is the raw text of this property.

### attributedDecreasedValue

```dart
set attributedDecreasedValue(AttributedString attributedDecreasedValue)
```

### hint

```dart
String get hint
```

A brief description of the result of performing an action on this node.

Setting this attribute will override the [attributedHint].

The reading direction is given by [textDirection].

See also:

- [attributedHint], which is the [AttributedString] of this property.

### hint

```dart
set hint(String hint)
```

### attributedHint

```dart
AttributedString get attributedHint
```

A brief description of the result of performing an action on this node in [AttributedString] format.

On iOS this is used for the `accessibilityAttributedHint` property defined in the `UIAccessibility` Protocol. On Android it is concatenated together with [attributedLabel] and [attributedValue] in the following order: [attributedValue], [attributedLabel], [attributedHint]. The concatenated value is then used as the `Text` description.

The reading direction is given by [textDirection].

See also:

- [hint], which is the raw text of this property.

### attributedHint

```dart
set attributedHint(AttributedString attributedHint)
```

### tooltip

```dart
String get tooltip
```

A textual description of the widget's tooltip.

The reading direction is given by [textDirection].

### tooltip

```dart
set tooltip(String tooltip)
```

### hintOverrides

```dart
SemanticsHintOverrides? get hintOverrides
```

Provides hint values which override the default hints on supported platforms.

### hintOverrides

```dart
set hintOverrides(SemanticsHintOverrides? value)
```

### scopesRoute

```dart
bool get scopesRoute
```

Whether the semantics node is the root of a subtree for which values should be announced.

See also:

- [SemanticsFlag.scopesRoute], for a full description of route scoping.

### scopesRoute

```dart
set scopesRoute(bool value)
```

### namesRoute

```dart
bool get namesRoute
```

Whether the semantics node contains the label of a route.

See also:

- [SemanticsFlag.namesRoute], for a full description of route naming.

### namesRoute

```dart
set namesRoute(bool value)
```

### isImage

```dart
bool get isImage
```

Whether the semantics node represents an image.

### isImage

```dart
set isImage(bool value)
```

### liveRegion

```dart
bool get liveRegion
```

Whether the semantics node is a live region.

A live region indicates that updates to semantics node are important. Platforms may use this information to make polite announcements to the user to inform them of updates to this node.

An example of a live region is a [SnackBar] widget. On Android and iOS, live region causes a polite announcement to be generated automatically, even if the widget does not have accessibility focus. This announcement may not be spoken if the OS accessibility services are already announcing something else, such as reading the label of a focused widget or providing a system announcement.

See also:

- [SemanticsFlag.isLiveRegion], the semantics flag that this setting controls.

### liveRegion

```dart
set liveRegion(bool value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The reading direction for the text in [label], [value], [hint], [increasedValue], and [decreasedValue].

### textDirection

```dart
set textDirection(TextDirection? textDirection)
```

### isSelected

```dart
bool get isSelected
```

Whether the owning [RenderObject] is selected (true) or not (false).

This is different from having accessibility focus. The element that is accessibility focused may or may not be selected; e.g. a [ListTile] can have accessibility focus but have its [ListTile.selected] property set to false, in which case it will not be flagged as selected.

### isSelected

```dart
set isSelected(bool value)
```

### isExpanded

```dart
bool? get isExpanded
```

If this node has Boolean state that can be controlled by the user, whether that state is expanded or collapsed, corresponding to true and false, respectively.

Do not call the setter for this field if the owning [RenderObject] doesn't have expanded/collapsed state that can be controlled by the user.

The getter returns null if the owning [RenderObject] does not have expanded/collapsed state.

### isExpanded

```dart
set isExpanded(bool? value)
```

### isEnabled

```dart
bool? get isEnabled
```

Whether the owning [RenderObject] is currently enabled.

A disabled object does not respond to user interactions. Only objects that usually respond to user interactions, but which currently do not (like a disabled button) should be marked as disabled.

The setter should not be called for objects (like static text) that never respond to user interactions.

The getter will return null if the owning [RenderObject] doesn't support the concept of being enabled/disabled.

This property does not control whether semantics are enabled. If you wish to disable semantics for a particular widget, you should use an [ExcludeSemantics] widget.

### isEnabled

```dart
set isEnabled(bool? value)
```

### isChecked

```dart
bool? get isChecked
```

If this node has Boolean state that can be controlled by the user, whether that state is checked or unchecked, corresponding to true and false, respectively.

Do not call the setter for this field if the owning [RenderObject] doesn't have checked/unchecked state that can be controlled by the user.

The getter returns null if the owning [RenderObject] does not have checked/unchecked state.

### isChecked

```dart
set isChecked(bool? value)
```

### isCheckStateMixed

```dart
bool? get isCheckStateMixed
```

If this node has tristate that can be controlled by the user, whether that state is in its mixed state.

Do not call the setter for this field if the owning [RenderObject] doesn't have checked/unchecked state that can be controlled by the user.

The getter returns null if the owning [RenderObject] does not have mixed checked state.

### isCheckStateMixed

```dart
set isCheckStateMixed(bool? value)
```

### isToggled

```dart
bool? get isToggled
```

If this node has Boolean state that can be controlled by the user, whether that state is on or off, corresponding to true and false, respectively.

Do not call the setter for this field if the owning [RenderObject] doesn't have on/off state that can be controlled by the user.

The getter returns null if the owning [RenderObject] does not have on/off state.

### isToggled

```dart
set isToggled(bool? value)
```

### isInMutuallyExclusiveGroup

```dart
bool get isInMutuallyExclusiveGroup
```

Whether the owning RenderObject corresponds to UI that allows the user to pick one of several mutually exclusive options.

For example, a [Radio] button is in a mutually exclusive group because only one radio button in that group can be marked as [isChecked].

### isInMutuallyExclusiveGroup

```dart
set isInMutuallyExclusiveGroup(bool value)
```

### isFocusable

```dart
bool get isFocusable
```

Whether the owning [RenderObject] can hold the input focus.

### isFocusable

```dart
set isFocusable(bool value)
```

### isFocused

```dart
bool? get isFocused
```

Whether the owning [RenderObject] currently holds the input focus.

### isFocused

```dart
set isFocused(bool? value)
```

### accessibilityFocusBlockType

```dart
AccessibilityFocusBlockType get accessibilityFocusBlockType
```

Whether the owning [RenderObject] and its subtree is blocked in the a11y focus (different from input focus).

### accessibilityFocusBlockType

```dart
set accessibilityFocusBlockType(AccessibilityFocusBlockType value)
```

### isButton

```dart
bool get isButton
```

Whether the owning [RenderObject] is a button (true) or not (false).

### isButton

```dart
set isButton(bool value)
```

### isLink

```dart
bool get isLink
```

Whether the owning [RenderObject] is a link (true) or not (false).

### isLink

```dart
set isLink(bool value)
```

### linkUrl

```dart
Uri? get linkUrl
```

The URL that the owning [RenderObject] links to.

### linkUrl

```dart
set linkUrl(Uri? value)
```

### isHeader

```dart
bool get isHeader
```

Whether the owning [RenderObject] is a header (true) or not (false).

### isHeader

```dart
set isHeader(bool value)
```

### headingLevel

```dart
int get headingLevel
```

Indicates the heading level in the document structure.

This is only used for web semantics, and is ignored on other platforms.

### headingLevel

```dart
set headingLevel(int value)
```

### isSlider

```dart
bool get isSlider
```

Whether the owning [RenderObject] is a slider (true) or not (false).

### isSlider

```dart
set isSlider(bool value)
```

### isKeyboardKey

```dart
bool get isKeyboardKey
```

Whether the owning [RenderObject] is a keyboard key (true) or not (false).

### isKeyboardKey

```dart
set isKeyboardKey(bool value)
```

### isHidden

```dart
bool get isHidden
```

Whether the owning [RenderObject] is considered hidden.

Hidden elements are currently not visible on screen. They may be covered by other elements or positioned outside of the visible area of a viewport.

Hidden elements cannot gain accessibility focus though regular touch. The only way they can be focused is by moving the focus to them via linear navigation.

Platforms are free to completely ignore hidden elements and new platforms are encouraged to do so.

Instead of marking an element as hidden it should usually be excluded from the semantics tree altogether. Hidden elements are only included in the semantics tree to work around platform limitations and they are mainly used to implement accessibility scrolling on iOS.

### isHidden

```dart
set isHidden(bool value)
```

### isTextField

```dart
bool get isTextField
```

Whether the owning [RenderObject] is a text field.

### isTextField

```dart
set isTextField(bool value)
```

### isReadOnly

```dart
bool get isReadOnly
```

Whether the owning [RenderObject] is read only.

Only applicable when [isTextField] is true.

### isReadOnly

```dart
set isReadOnly(bool value)
```

### isObscured

```dart
bool get isObscured
```

Whether [value] should be obscured.

This option is usually set in combination with [isTextField] to indicate that the text field contains a password (or other sensitive information). Doing so instructs screen readers to not read out [value].

### isObscured

```dart
set isObscured(bool value)
```

### isMultiline

```dart
bool get isMultiline
```

Whether the text field is multiline.

This option is usually set in combination with [isTextField] to indicate that the text field is configured to be multiline.

### isMultiline

```dart
set isMultiline(bool value)
```

### isRequired

```dart
bool? get isRequired
```

Whether the semantics node has a required state.

Do not call the setter for this field if the owning [RenderObject] doesn't have a required state that can be controlled by the user.

The getter returns null if the owning [RenderObject] does not have a required state.

See also:

- [SemanticsFlag.isRequired], for a full description of required nodes.

### isRequired

```dart
set isRequired(bool? value)
```

### hasImplicitScrolling

```dart
bool get hasImplicitScrolling
```

Whether the platform can scroll the semantics node when the user attempts to move focus to an offscreen child.

For example, a [ListView] widget has implicit scrolling so that users can easily move to the next visible set of children. A [TabBar] widget does not have implicit scrolling, so that users can navigate into the tab body when reaching the end of the tab bar.

### hasImplicitScrolling

```dart
set hasImplicitScrolling(bool value)
```

### textSelection

```dart
TextSelection? get textSelection
```

The currently selected text (or the position of the cursor) within [value] if this node represents a text field.

### textSelection

```dart
set textSelection(TextSelection? value)
```

### scrollPosition

```dart
double? get scrollPosition
```

Indicates the current scrolling position in logical pixels if the node is scrollable.

The properties [scrollExtentMin] and [scrollExtentMax] indicate the valid in-range values for this property. The value for [scrollPosition] may (temporarily) be outside that range, e.g. during an overscroll.

See also:

- [ScrollPosition.pixels], from where this value is usually taken.

### scrollPosition

```dart
set scrollPosition(double? value)
```

### scrollExtentMax

```dart
double? get scrollExtentMax
```

Indicates the maximum in-range value for [scrollPosition] if the node is scrollable.

This value may be infinity if the scroll is unbound.

See also:

- [ScrollPosition.maxScrollExtent], from where this value is usually taken.

### scrollExtentMax

```dart
set scrollExtentMax(double? value)
```

### scrollExtentMin

```dart
double? get scrollExtentMin
```

Indicates the minimum in-range value for [scrollPosition] if the node is scrollable.

This value may be infinity if the scroll is unbound.

See also:

- [ScrollPosition.minScrollExtent], from where this value is usually taken.

### scrollExtentMin

```dart
set scrollExtentMin(double? value)
```

### controlsNodes

```dart
Set<String>? get controlsNodes
```

The [SemanticsNode.identifier]s of widgets controlled by this node.

### controlsNodes

```dart
set controlsNodes(Set<String>? value)
```

### validationResult

```dart
SemanticsValidationResult get validationResult
```

{@macro flutter.semantics.SemanticsProperties.validationResult}

### validationResult

```dart
set validationResult(SemanticsValidationResult value)
```

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior get hitTestBehavior
```

{@macro flutter.semantics.SemanticsProperties.hitTestBehavior}

### hitTestBehavior

```dart
set hitTestBehavior(ui.SemanticsHitTestBehavior value)
```

### inputType

```dart
SemanticsInputType get inputType
```

{@macro flutter.semantics.SemanticsProperties.inputType}

### inputType

```dart
set inputType(SemanticsInputType value)
```

### maxValue

```dart
String? get maxValue
```

{@macro flutter.semantics.SemanticsProperties.maxValue}

### maxValue

```dart
set maxValue(String? value)
```

### minValue

```dart
String? get minValue
```

{@macro flutter.semantics.SemanticsProperties.minValue}

### minValue

```dart
set minValue(String? value)
```

### tagsForChildren

```dart
Iterable<SemanticsTag>? get tagsForChildren
```

The set of tags that this configuration wants to add to all child [SemanticsNode]s.

See also:

- [addTagForChildren] to add a tag and for more information about their usage.

### tagsChildrenWith()

```dart
bool tagsChildrenWith(SemanticsTag tag)
```

Whether this configuration will tag the child semantics nodes with a given [SemanticsTag].

### addTagForChildren()

```dart
void addTagForChildren(SemanticsTag tag)
```

Specifies a [SemanticsTag] that this configuration wants to apply to all child [SemanticsNode]s.

The tag is added to all [SemanticsNode] that pass through the [RenderObject] owning this configuration while looking to be attached to a parent [SemanticsNode].

Tags are used to communicate to a parent [SemanticsNode] that a child [SemanticsNode] was passed through a particular [RenderObject]. The parent can use this information to determine the shape of the semantics tree.

See also:

- [RenderViewport.excludeFromScrolling] for an example of how tags are used.

### isCompatibleWith()

```dart
bool isCompatibleWith(SemanticsConfiguration? other)
```

Whether this configuration is compatible with the provided `other` configuration.

Two configurations are said to be compatible if they can be added to the same [SemanticsNode] without losing any semantics information.

### absorb()

```dart
void absorb(SemanticsConfiguration child)
```

Absorb the semantic information from `child` into this configuration.

This adds the semantic information of both configurations and saves the result in this configuration.

The [RenderObject] owning the `child` configuration must be a descendant of the [RenderObject] that owns this configuration.

Only configurations that have [explicitChildNodes] set to false can absorb other configurations and it is recommended to only absorb compatible configurations as determined by [isCompatibleWith].

### copy()

```dart
SemanticsConfiguration copy()
```

Returns an exact copy of this configuration.

# DebugSemanticsDumpOrder

```dart
enum DebugSemanticsDumpOrder {}
```

Used by [debugDumpSemanticsTree] to specify the order in which child nodes are printed.

Print nodes in inverse hit test order.

In inverse hit test order, the last child of a [SemanticsNode] will be asked first if it wants to respond to a user's interaction, followed by the second last, etc. until a taker is found.

Print nodes in semantic traversal order.

This is the order in which a user would navigate the UI using the "next" and "previous" gestures.

# SemanticsSortKey

```dart
abstract class SemanticsSortKey with Diagnosticable implements Comparable<SemanticsSortKey> {}
```

Base class for all sort keys for [SemanticsProperties.sortKey] accessibility traversal order sorting.

Sort keys are sorted by [name], then by the comparison that the subclass implements. If [SemanticsProperties.sortKey] is specified, sort keys within the same semantic group must all be of the same type.

Keys with no [name] are compared to other keys with no [name], and will be traversed before those with a [name].

If no sort key is applied to a semantics node, then it will be ordered using a platform dependent default algorithm.

See also:

- [OrdinalSortKey] for a sort key that sorts using an ordinal.

### SemanticsSortKey()

```dart
SemanticsSortKey({String? name})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### name

```dart
String? name
```

An optional name that will group this sort key with other sort keys of the same [name].

Sort keys must have the same `runtimeType` when compared.

Keys with no [name] are compared to other keys with no [name], and will be traversed before those with a [name].

### compareTo()

```dart
int compareTo(SemanticsSortKey other)
```

### doCompare()

```dart
int doCompare(SemanticsSortKey other)
```

The implementation of [compareTo].

The argument is guaranteed to be of the same type as this object and have the same [name].

The method should return a negative number if this object comes earlier in the sort order than the argument; and a positive number if it comes later in the sort order. Returning zero causes the system to use default sort order.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OrdinalSortKey

```dart
class OrdinalSortKey extends SemanticsSortKey {}
```

A [SemanticsSortKey] that sorts based on the `double` value it is given.

The [OrdinalSortKey] compares itself with other [OrdinalSortKey]s to sort based on the order it is given.

[OrdinalSortKey]s are sorted by the optional [name], then by their [order]. If [SemanticsProperties.sortKey] is a [OrdinalSortKey], then all the other specified sort keys in the same semantics group must also be [OrdinalSortKey]s.

Keys with no [name] are compared to other keys with no [name], and will be traversed before those with a [name].

The ordinal value [order] is typically a whole number, though it can be fractional, e.g. in order to fit between two other consecutive whole numbers. The value must be finite (it cannot be [double.nan], [double.infinity], or [double.negativeInfinity]).

### OrdinalSortKey()

```dart
OrdinalSortKey(double order, {String? name})
```

Creates a const semantics sort key that uses a [double] as its key value.

The [order] must be a finite number.

### order

```dart
double order
```

Determines the placement of this key in a sequence of keys that defines the order in which this node is traversed by the platform's accessibility services.

Lower values will be traversed first. Keys with the same [name] will be grouped together and sorted by name first, and then sorted by [order].

### doCompare()

```dart
int doCompare(OrdinalSortKey other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
