# Item

A paragraph of text in an [`Outline`](outline.md) .

Items cannot be created directly. Use [`Outline::createItem`](outline.md#instance-createItem) to create items.

Items may contain other child items to form a hierarchy. When you move an item its children move with it. See the “Structure” and “Mutate Structure” sections for associated APIs. To move an item while leaving it’s children in place see the methods in [`Outline`](outline.md) s “Insert & Remove Items”.

Items may have associated attributes. You can add your own attributes by using the APIs described in the “Item Attributes” section. For example you might add a due date using the `data-due-date` attribute.

Items have an associated paragraph of body text. You can access it as plain text or as an immutable [`AttributedString`](attributedstring.md) . You can also add and remove attributes from ranges of body text. See “Item Body Text” for associated APIs. While you can add these attributes at runtime, TaskPaper won’t save them to disk since it saved in plain text without associated text run attributes.

## Examples <a id="examples"></a>

Create Items:

```text
var item = outline.createItem('Hello World!');
outline.root.appendChildren(item);
```

Add attributes to body text:

```text
var item = outline.createItem('Hello World!');
item.addBodyAttributeInRange('B', {}, 6, 5);
item.addBodyAttributeInRange('I', {}, 0, 11);
```

Reading attributes from body text:

```text
var effectiveRange = {};
var textLength = item.bodyString.length;
var index = 0;
while (index < textLength) {
  console.log(item.getBodyAttributesAtIndex(index, effectiveRange));
  index += effectiveRange.length;
}
```

## Properties <a id="properties"></a>

 `::id`

Read-only unique [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) identifier. `::outline`

Read-only [`Outline`](outline.md) that this item belongs to.

## Clone <a id="clone"></a>

 `::clone(deep?)`

Clones this item.

| Argument | Description |
| :--- | :--- |
| `deep?` | defaults to true. |

| Return Values |
| :--- |
| Returns a duplicate [`Item`](item.md) with a new [`::id`](item.md#instance-id) . |

## Structure <a id="structure"></a>

 `::isInOutline`

Read-only true if item is contained by root of owning [`Outline`](outline.md) . `::isOutlineRoot`

Read-only true if is [`::outline`](item.md#instance-outline) root [`Item`](item.md) . `::depth`

Read-only depth of [`Item`](item.md) in outline structure. Calculated by summing the [`Item::indent`](item.md#instance-indent) of this item and it’s ancestors. `::parent`

Read-only parent [`Item`](item.md) . `::firstChild`

Read-only first child [`Item`](item.md) . `::lastChild`

Read-only last child [`Item`](item.md) . `::previousSibling`

Read-only previous sibling [`Item`](item.md) . `::nextSibling`

Read-only next sibling [`Item`](item.md) . `::previousBranch`

Read-only previous branch [`Item`](item.md) . `::nextBranch`

Read-only next branch [`Item`](item.md) . `::ancestors`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of ancestor [`Item`](item.md) s. `::descendants`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of descendant [`Item`](item.md) s. `::lastDescendant`

Read-only last descendant [`Item`](item.md) . `::branchItems`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of this [`Item`](item.md) and its descendants. `::lastBranchItem`

Last [`Item`](item.md) in branch rooted at this item. `::previousItem`

Read-only previous [`Item`](item.md) in the outline. `::nextItem`

Read-only next [`Item`](item.md) in the outline. `::hasChildren`

Read-only has children [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) . `::children`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of child [`Item`](item.md) s. `.getCommonAncestors(items)`

Given an array of items determines and returns the common ancestors of those items.

| Argument | Description |
| :--- | :--- |
| `items` |  [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s. |

| Return Values |
| :--- |
| Returns a [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of common ancestor [`Item`](item.md) s. |

 `::contains(item)`

Determines if this item contains the given item.

| Argument | Description |
| :--- | :--- |
| `item` | The [`Item`](item.md) to check for containment. |

| Return Values |
| :--- |
| Returns [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) . |

## Mutate Structure <a id="mutate-structure"></a>

 `::indent`

Visual indent of [`Item`](item.md) relative to parent. Normally this will be 1 for children with a parent as they are indented one level beyond there parent. But items can be visually over-indented in which case this value would be greater then 1. `::insertChildrenBefore(children, referenceSibling?)`

Insert the new children before the referenced sibling in this item’s list of children. If referenceSibling isn’t defined the new children are inserted at the end. This method resets the indent of children to match referenceSibling’s indent or to 1.

| Argument | Description |
| :--- | :--- |
| `children` |  [`Item`](item.md) or [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s to insert. |
| `referenceSibling?` | The referenced sibling [`Item`](item.md) to insert before. |

 `::appendChildren(children)`

Append the new children to this item’s list of children.

| Argument | Description |
| :--- | :--- |
| `children` |  [`Item`](item.md) or [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s to append. |

 `::removeChildren(children)`

Remove the children from this item’s list of children. When an item is removed its the parent’s [`::depth`](item.md#instance-depth) is added to the removed item’s [`::indent`](item.md#instance-indent) , preserving the removed items depth if needed later.

| Argument | Description |
| :--- | :--- |
| `children` |  [`Item`](item.md) or [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of child [`Item`](item.md) s to remove. |

 `::removeFromParent()`

Remove this item from it’s parent item if it has a parent.

## Item Attributes <a id="item-attributes"></a>

 `::attributes`

Read-only key/value object of the attributes associated with this [`Item`](item.md) . `::attributeNames`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of this [`Item`](item.md) ‘s attribute names. `::hasAttribute(name)`

Return [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) `true` if this item has the given attribute.

| Argument | Description |
| :--- | :--- |
| `name` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name. |

 `::getAttribute(name, clazz?, array?)`

Return the value of the given attribute. If the attribute does not exist will return `null`. Attribute values are always stored as [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) s. Use the `class` and `array` parameters to parse the string values to other types before returning.

| Argument | Description |
| :--- | :--- |
| `name` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name. |
| `clazz?` | Class \( [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) or [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) \) to parse string values to objects of given class. |
| `array?` |  [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) true if should split comma separated string value to create an array. |

| Return Values |
| :--- |
| Returns attribute value. |

 `::setAttribute(name, value)`

Adds a new attribute or changes the value of an existing attribute. `id` is reserved and an exception is thrown if you try to set it. Setting an attribute to `null` or `undefined` removes the attribute. Generally all item attribute names should start with `data-` to avoid conflict with built in attribute names.

Attribute values are always stored as [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) s so they will stay consistent through any serialization process. For example if you set an attribute to the Number `1.0` when you [`::getAttribute`](item.md#instance-getAttribute) the value is the [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) `"1.0"`. See [`::getAttribute`](item.md#instance-getAttribute) for options to automatically convert the stored [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) back to a [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) or [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) .

| Argument | Description |
| :--- | :--- |
| `name` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name. |
| `value` | The new attribute value. |

 `::removeAttribute(name)`

Removes an item attribute.

| Argument | Description |
| :--- | :--- |
| `name` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name. |

## Item Body Text <a id="item-body-text"></a>

 `::bodyString`

Body text as plain text [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) . `::bodyContentString`

Body “content” text as plain text [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) . Excludes trailing tags and leading syntax. For example used when displaying items to user’s in menus. `::bodyAttributedString`

Body text as immutable [`AttributedString`](attributedstring.md) . Do not modify this AttributedString, instead use the other methods in this “Body Text” section. They will both modify the string and create the appropriate [`Mutation`](mutation.md) events needed to keep the outline valid. `::bodyHighlightedAttributedString`

Syntax highlighted body text as immutable [`AttributedString`](attributedstring.md) . Unlike `bodyAttributedString` this string contains attributes created by syntax highlighting such as tag name and value ranges.

Do not modify this AttributedString, instead use the other methods in this “Body Text” section. They will both modify the string and create the appropriate [`Mutation`](mutation.md) events needed to keep the outline valid. `::getBodyAttributesAtIndex(characterIndex, effectiveRange?, longestEffectiveRange?)`

| Argument | Description |
| :--- | :--- |
| `characterIndex` | The character index. |
| `effectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to effective range of the attributes. |
| `longestEffectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to longest effective range of the attributes. |

| Return Values |
| :--- |
| Returns an [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) with keys for each attribute at the given character characterIndex, and by reference the range over which the attributes apply. |

 `::getBodyAttributeAtIndex(attribute, characterIndex, effectiveRange?, longestEffectiveRange?)`

| Argument | Description |
| :--- | :--- |
| `attribute` | Attribute [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) name. |
| `characterIndex` | The character index. |
| `effectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to effective range of the attribute. |
| `longestEffectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to longest effective range of the attribute. |

| Return Values |
| :--- |
| Returns the value for an attribute with a given name of the character at a given characterIndex, and by reference the range over which the attribute applies. |

 `::addBodyAttributeInRange(attribute, value, location, length)`

Adds an attribute to the characters in the given range.

| Argument | Description |
| :--- | :--- |
| `attribute` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name. |
| `value` | The attribute value. |
| `location` | Start character index. |
| `length` | Range length. |

 `::addBodyAttributesInRange(attributes, location, length)`

Adds attributes to the characters in the given range.

| Argument | Description |
| :--- | :--- |
| `attributes` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) with keys and values for each attribute |
| `location` | Start index. |
| `length` | Range length. |

 `::removeBodyAttributeInRange(attribute, location, length)`

Removes the attribute from the given range.

| Argument | Description |
| :--- | :--- |
| `attribute` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name |
| `location` | Start character index. |
| `length` | Range length. |

 `::replaceBodyRange(location, length, insertedText)`

Replace body text in the given range.

| Argument | Description |
| :--- | :--- |
| `location` | Start character index. |
| `length` | Range length. |
| `insertedText` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) or [`AttributedString`](attributedstring.md) |

 `::appendBody(text)`

Append body text.

| Argument | Description |
| :--- | :--- |
| `text` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) or [`AttributedString`](attributedstring.md) |

## Debug <a id="debug"></a>

 `::branchToString()`

| Return Values |
| :--- |
| Returns debug string for this item and it’s descendants. |

 `::toString()`

| Return Values |
| :--- |
| Returns debug string for this item. |

