# Mutation

A record of a single change in an [`Item`](item.md) .

A new mutation is created to record each attribute set, body text change, and child item update. Use [`Outline::onDidChange`](outline.md#instance-onDidChange) to receive this mutation record so you can track what changes as an outline is edited.

## Constants <a id="constants"></a>

 `.ATTRIBUTE_CHANGED`

ATTRIBUTE\_CHANGED Mutation type constant. `.BODY_CHANGED`

BODY\_CHANGED Mutation type constant. `.CHILDREN_CHANGED`

CHILDREN\_CHANGED Mutation type constant.

## Attribute <a id="attribute"></a>

 `::target`

Read-only [`Item`](item.md) target of the mutation. `::type`

Read-only type of change. [`Mutation.ATTRIBUTE_CHANGED`](mutation.md#static-ATTRIBUTE_CHANGED) , [`Mutation.BODY_CHANGED`](mutation.md#static-BODY_CHANGED) , or [`Mutation.CHILDREN_CHANGED`](mutation.md#static-CHILDREN_CHANGED) . `::attributeName`

Read-only name of changed attribute in the target [`Item`](item.md) , or null. `::attributeOldValue`

Read-only previous value of changed attribute in the target [`Item`](item.md) , or null. `::insertedTextLocation`

Read-only value of the body text location where the insert started in the target [`Item`](item.md) , or null. `::insertedTextLength`

Read-only value of length of the inserted body text in the target [`Item`](item.md) , or null. `::replacedText`

Read-only [`AttributedString`](attributedstring.md) of replaced body text in the target [`Item`](item.md) , or null. `::addedItems`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of child [`Item`](item.md) s added to the target. `::removedItems`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of child [`Item`](item.md) s removed from the target. `::previousSibling`

Read-only previous sibling [`Item`](item.md) of the added or removed Items, or null. `::nextSibling`

Read-only next sibling [`Item`](item.md) of the added or removed Items, or null.

