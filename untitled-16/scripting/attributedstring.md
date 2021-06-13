# AttributedString

A container holding both characters and associated attributes.

## Examples <a id="examples"></a>

Enumerate attribute ranges:

```text
var effectiveRange = {};
var textLength = attributedString.length;
var index = 0;
while (index < textLength) {
  console.log(attributedString.getAttributesAtIndex(index, effectiveRange));
  index += effectiveRange.length;
}
```

## Creating <a id="creating"></a>

 `::constructor(text)`

Create a new AttributedString with the given text.

| Argument | Description |
| :--- | :--- |
| `text` | Text content for the AttributedString. |

 `::clone()`

Return a clone of this AttributedString. The attributes are shallow copied.

## Characters <a id="characters"></a>

 `::string`

Read-only string `::deleteRange(location, length)`

Delete characters and attributes in range.

| Argument | Description |
| :--- | :--- |
| `location` | Range start character index. |
| `length` | Range length. |

 `::insertText(location, text)`

Insert text into the string.

| Argument | Description |
| :--- | :--- |
| `location` | Location to insert at. |
| `text` | text to insert. |

 `::appendText(text)`

Append text to the end of the string.

| Argument | Description |
| :--- | :--- |
| `text` | text to insert. |

 `::replaceRange(location, length, text)`

Replace existing text range with new text.

| Argument | Description |
| :--- | :--- |
| `location` | Replace range start character index. |
| `length` | Replace range length. |
| `text` | text to insert. |

## Attributes <a id="attributes"></a>

 `::getAttributesAtIndex(index, effectiveRange?, longestEffectiveRange?)`

| Argument | Description |
| :--- | :--- |
| `index` | The character index. |
| `effectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to effective range of the attributes. |
| `longestEffectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to longest effective range of the attributes. |

| Return Values |
| :--- |
| Returns an [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) with keys for each attribute at the given character index, and by reference the range over which the attributes apply. |

 `::getAttributeAtIndex(attribute, index, effectiveRange?, longestEffectiveRange?)`

| Argument | Description |
| :--- | :--- |
| `attribute` | Attribute [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) name. |
| `index` | The character index. |
| `effectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to effective range of the attribute. |
| `longestEffectiveRange?` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) whose `location` and `length` properties are set to longest effective range of the attribute. |

| Return Values |
| :--- |
| Returns the value for an attribute with a given name of the character at a given character index, and by reference the range over which the attribute applies. |

 `::addAttributeInRange(attribute, value, index, length)`

Adds an attribute to the characters in the given range.

| Argument | Description |
| :--- | :--- |
| `attribute` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name. |
| `value` | The attribute value. |
| `index` | Start character index. |
| `length` | Range length. |

 `::addAttributesInRange(attributes, index, length)`

Adds attributes to the characters in the given range.

| Argument | Description |
| :--- | :--- |
| `attributes` |  [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) with keys and values for each attribute |
| `index` | Start index. |
| `length` | Range length. |

 `::removeAttributeInRange(attribute, index, length)`

Removes the attribute from the given range.

| Argument | Description |
| :--- | :--- |
| `attribute` | The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) attribute name |
| `index` | Start character index. |
| `length` | Range length. |

 `::attributedSubstringFromRange(location?, length?)`

| Argument | Description |
| :--- | :--- |
| `location?` | Range start character index. Defaults to 0. |
| `length?` | Range length. Defaults to end of string. |

| Return Values |
| :--- |
| Returns an [`AttributedString`](attributedstring.md) object consisting of the characters and attributes within a given range in the receiver. |

## Debug <a id="debug"></a>

 `::toString()`

| Return Values |
| :--- |
| Returns debug string for this item. |

