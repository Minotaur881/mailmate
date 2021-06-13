# OutlineEditor

Maps an [`Outline`](outline.md) into an editable text buffer.

The outline editor maintains the hoisted item, folded items, filter path, and selected items. It uses this state to determine which items are displayed and selected in the text buffer.

## Finding Outline Editors <a id="finding-outline-editors"></a>

 `.getOutlineEditors()`

Retrieves all open [`OutlineEditor`](outlineeditor.md) s.

| Return Values |
| :--- |
| Returns an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`OutlineEditor`](outlineeditor.md) s. |

 `.getOutlineEditorsForOutline(outline)`

Return [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of all [`OutlineEditor`](outlineeditor.md) s associated with the given [`Outline`](outline.md) .

| Argument | Description |
| :--- | :--- |
| `outline` | Edited [`Outline`](outline.md) . |

## Outline <a id="outline"></a>

 `::outline`

 [`Outline`](outline.md) that is edited.

## State <a id="state"></a>

 `::hoistedItem`

Root of all items displayed in the text buffer. `::focusedItem`

Focused item in the text buffer. Similar to [`::hoistedItem`](outlineeditor.md#instance-hoistedItem) , but the hoisted item is never displayed in the text buffer, while [`::focusedItem`](outlineeditor.md#instance-focusedItem) is displayed \(and temporarily expanded\) to show any children. `::itemPathFilter`

Item path formatted [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) . When set only matching items display in the text buffer.

## Folding Items <a id="folding-items"></a>

 `::fold()`

Toggle folding status of current selection. `::isExpanded(item)`

Return true of the given item is expanded.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to check. |

 `::isFiltered(item)`

Return true of the given item has some of its children visible and others hidden.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to check. |

 `::isCollapsed(item)`

Return true of the given item is collapsed.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to check. |

 `::setExpanded(items)`

Expand the given item\(s\).

| Argument | Description |
| :--- | :--- |
| `items` |  [`Item`](item.md) or [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of items to expand. |

 `::setCollapsed(items)`

Collapse the given item\(s\).

| Argument | Description |
| :--- | :--- |
| `items` |  [`Item`](item.md) or [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of items to collapse. |

## Displayed Items <a id="displayed-items"></a>

 `::displayedItems`

 [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of visible [`Item`](item.md) s in editor \(readonly\). `::firstDisplayedItem`

First displayed [`Item`](item.md) in editor \(readonly\). `::lastDisplayedItem`

Last displayed [`Item`](item.md) in editor \(readonly\). `::isDisplayed(item)`

Determine if an [`Item`](item.md) is displayed in the editor’s text buffer. A displayed item isn’t neccessarily visible because it might be scrolled off screen. Displayed means that its body text is present and editable in the buffer.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to test. |

| Return Values |
| :--- |
| Returns [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) indicating if item is displayed. |

 `::forceDisplayed(item, showAncestors?)`

Force the given [`Item`](item.md) to display in the editor’s text buffer, expanding ancestors, removing filters, and unhoisting items as needed.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to make displayed. |
| `showAncestors?` |  [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) defaults to false. |

 `::forceHidden(item, hideDescendants?)`

Remove the given [`Item`](item.md) \(s\) from display in the editor’s text buffer, leaving all other items in place.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) \(s\) to hide. |
| `hideDescendants?` |  [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) defaults to false. |

 `::getNextDisplayedItem(item)`

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) |

| Return Values |
| :--- |
| Returns next displayed [`Item`](item.md) relative to given item. |

 `::getPreviousDisplayedItem(item)`

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) |

| Return Values |
| :--- |
| Returns previous displayed [`Item`](item.md) relative to given item. |

## Text Buffer <a id="text-buffer"></a>

 `::textLength`

Read-only text buffer [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) length. `::getItemOffsetForLocation(location)`

Translate from a text buffer location to an [`Item`](item.md) offset.

| Argument | Description |
| :--- | :--- |
| `location` | Text buffer character [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) location. |

| Return Values |
| :--- |
| Returns [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) with `item` and `offset` properties. |

 `::getLocationForItemOffset(item, offset)`

Translate from item offset to the nearest valid text buffer location.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to lookup. |
| `offset` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) offset into the items text. |

| Return Values |
| :--- |
| Returns text buffer character offset [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) . |

 `::getTextInRange(location, length)`

Get text in the given range.

| Argument | Description |
| :--- | :--- |
| `location` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character location. |
| `length` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character range length. |

 `::replaceRangeWithString(location, length, string)`

Replace the given range with a string.

| Argument | Description |
| :--- | :--- |
| `location` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character location. |
| `length` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character range length. |
| `string` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) to insert. |

 `::replaceRangeWithItems(location, length, items)`

Replace the given range with a items.

| Argument | Description |
| :--- | :--- |
| `location` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character location. |
| `length` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character range length. |
| `items` |  [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s to insert. |

## Selection <a id="selection"></a>

 `::selection`

Read-only [`Selection`](selection.md) snapshot. `::moveSelectionToRange(focusLocation, anchorLocation?)`

Set selection by character locations in text buffer.

| Argument | Description |
| :--- | :--- |
| `focusLocation` | Selection focus character [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) location. |
| `anchorLocation?` | Selection anchor character [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) location. |

 `::moveSelectionToItems(headItem, headOffset?, anchorItem?, anchorOffset?)`

Set selection by [`Item`](item.md) .

| Argument | Description |
| :--- | :--- |
| `headItem` | Selection head [`Item`](item.md) |
| `headOffset?` | Selection head offset index. Or `undefined` when selecting at item level. |
| `anchorItem?` | Selection anchor [`Item`](item.md) |
| `anchorOffset?` | Selection anchor offset index. Or `undefined` when selecting at item level. |

 `::scrollBy(xDelta, yDelta)`

Adjust [`::scrollPoint`](outlineeditor.md#instance-scrollPoint) by the given delta.

| Argument | Description |
| :--- | :--- |
| `xDelta` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) scroll point x delta. |
| `yDelta` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) scroll point y delta. |

 `::scrollRangeToVisible(location, length)`

Scroll the given range to visible in the text buffer.

| Argument | Description |
| :--- | :--- |
| `location` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character location. |
| `length` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character range length. |

 `::getRectForRange(location, length)`

Get rectangle for the given character range.

| Argument | Description |
| :--- | :--- |
| `location` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character location. |
| `length` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character range length. |

| Return Values |
| :--- |
| Returns [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) with `x`, `y`, `width`, and `height` keys. |

 `::getCharacterIndexForPoint(x, y)`

Get character index for the given point.

| Argument | Description |
| :--- | :--- |
| `x` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) x position. |
| `y` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) y position. |

| Return Values |
| :--- |
| Returns [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character index. |

## Item Serialization <a id="item-serialization"></a>

 `::serializeRange(location, length, options)`

Get item serialization from the given range.

| Argument | Description |
| :--- | :--- |
| `location` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character location. |
| `length` |  [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) character range length. |
| `options` | Serialization options as defined in [`ItemSerializer`](itemserializer.md) . |

