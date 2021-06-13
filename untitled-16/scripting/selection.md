# Selection

Read-only selection snapshot from [`OutlineEditor::selection`](outlineeditor.md#instance-selection) .

This selection can not be changed and will not update when the outline or editor selection changes. Use [`OutlineEditor::moveSelectionToItems`](outlineeditor.md#instance-moveSelectionToItems) or [`OutlineEditor::moveSelectionToRange`](outlineeditor.md#instance-moveSelectionToRange) to change the editor’s selection.

The selection character offsets are always valid, but in some cases the selection endpoint [`Item`](item.md) s maybe be null. For instance if the [`OutlineEditor`](outlineeditor.md) has hoisted an item that has no children then the character selection will be `0,0`, but [`::startItem`](selection.md#instance-startItem) and [`::endItem`](selection.md#instance-endItem) will be `null`.

The [`::endItem`](selection.md#instance-endItem) end point isn’t always the last item in [`::selectedItems`](selection.md#instance-selectedItems) . For example if [`::endItem`](selection.md#instance-endItem) doesn’t equal [`::startItem`](selection.md#instance-startItem) and [`::endOffset`](selection.md#instance-endOffset) is 0 then [`::endItem`](selection.md#instance-endItem) isn’t included in the selected items because it doesn’t overlap the selection, it’s just an endpoint anchor, not a selcted item.

## Selection <a id="selection"></a>

 `::isCollapsed`

Read-only true if selection start equals end. `::isFullySelectingItems`

Read-only true if selection starts at item start boundary and ends at item end boundary.

## Characters <a id="characters"></a>

 `::start`

Read-only selection start character offset. `::end`

Read-only selection end character offset. `::location`

Read-only selection character location offset. `::length`

Read-only selection character length.

## Items <a id="items"></a>

 `::startItem`

Read-only selection start [`Item`](item.md) \(or null\) in outline order. `::startOffset`

Read-only text offset in the [`::startItem`](selection.md#instance-startItem) where selection starts. `::endItem`

Read-only selection endpoint [`Item`](item.md) \(or null\) in outline order. `::endOffset`

Read-only text offset endpoint in [`::endItem`](selection.md#instance-endItem) or undefined. `::selectedItems`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s intersecting the selection. Does not include [`::endItem`](selection.md#instance-endItem) if [`::endItem`](selection.md#instance-endItem) doesn’t equal [`::startItem`](selection.md#instance-startItem) and [`::endOffset`](selection.md#instance-endOffset) is 0. Does include all overlapped outline items, including folded and hidden ones, between the start and end items. `::displayedSelectedItems`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of displayed [`Item`](item.md) s intersecting the selection. Does not include [`::endItem`](selection.md#instance-endItem) if [`::endItem`](selection.md#instance-endItem) doesn’t equal [`::startItem`](selection.md#instance-startItem) and [`::endOffset`](selection.md#instance-endOffset) is 0. Does not include items that the selection overlaps but that are hidden in the editor. `::displayedAncestorSelectedItems`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of displayed [`Item`](item.md) s intersecting the selection. Does not include [`::endItem`](selection.md#instance-endItem) if [`::endItem`](selection.md#instance-endItem) doesn’t equal [`::startItem`](selection.md#instance-startItem) and [`::endOffset`](selection.md#instance-endOffset) is 0. Does include items that overlap the selection by that are not visible. `::selectedItemsCommonAncestors`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of the common ancestors of [`::selectedItems`](selection.md#instance-selectedItems) .

