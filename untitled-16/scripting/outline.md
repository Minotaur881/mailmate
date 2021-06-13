# Outline

A mutable outline of [`Item`](item.md) s.

Use outlines to create new items, find existing items, watch for changes in items, and add/remove items.

When you add/remove items using the outline’s methods the items children are left in place. For example if you remove an item, it’s chilren stay in the outline and are reasigned to a new parent item.

## Examples <a id="examples"></a>

Group multiple changes:

```text
outline.groupUndoAndChanges(function() {
  root = outline.root;
  root.appendChildren(outline.createItem());
  root.appendChildren(outline.createItem());
  root.firstChild.bodyString = 'first';
  root.lastChild.bodyString = 'last';
});
```

Watch for outline changes:

```text
disposable = outline.onDidChange(function(mutation) {
  switch(mutation.type) {
    case Mutation.ATTRIBUTE_CHANGED:
      console.log(mutation.attributeName);
      break;
    case Mutation.BODY_CHANGED:
      console.log(mutation.target.bodyString);
      break;
    case Mutation.CHILDREN_CHANGED:
      console.log(mutation.addedItems);
      console.log(mutation.removedItems);
      break;
  }
});
...
disposable.dispose()
```

## Construction <a id="construction"></a>

 `.createTaskPaperOutline(content)`

The outline is configured to handle TaskPaper content at runtime. For example when you set attributes through the [`Item`](item.md) API they are encoded in the item body text as @tags. And when you modify the body text @tags are parsed out and stored as attributes.

| Argument | Description |
| :--- | :--- |
| `content` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \(optional\) outline content in TaskPaper format. |

| Return Values |
| :--- |
| Returns a TaskPaper [`Outline`](outline.md) . |

 `::constructor(type?, serialization?)`

Create a new outline.

| Argument | Description |
| :--- | :--- |
| `type?` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) outline type. Default to [`ItemSerializer.TEXTType`](itemserializer.md#static-TEXTType) . |
| `serialization?` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) Serialized outline content of `type` to load. |

## Finding Outlines <a id="finding-outlines"></a>

 `::id`

Read-only unique \(not persistent\) [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) outline ID. `.getOutlines()`

Retrieves all open [`Outline`](outline.md) s.

| Return Values |
| :--- |
| Returns an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Outline`](outline.md) s. |

 `.getOutlineForID(id)`

| Argument | Description |
| :--- | :--- |
| `id` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) outline id. |

| Return Values |
| :--- |
| Returns existing [`Outline`](outline.md) with the given outline id. |

## Events <a id="events"></a>

 `::onDidBeginChanges(callback)`

Invoke the given callback when the outline begins a series of changes.

| Argument | Description |
| :--- | :--- |
| `callback` |  [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) to be called when the outline begins updating. |

| Return Values |
| :--- |
| Returns a [`Disposable`](https://atom.io/docs/api/latest/Disposable) on which `.dispose()` can be called to unsubscribe. |

 `::onWillChange(callback)`

Invoke the given callback _before_ the outline changes.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>callback</code>
      </td>
      <td style="text-align:left">
        <p> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function"><code>Function</code></a> to
          be called when the outline will change.</p>
        <ul>
          <li> <code>mutation</code> &#x2014; <a href="mutation.md"><code>Mutation</code></a> describing
            the change.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

| Return Values |
| :--- |
| Returns a [`Disposable`](https://atom.io/docs/api/latest/Disposable) on which `.dispose()` can be called to unsubscribe. |

 `::onDidChange(callback)`

Invoke the given callback when the outline changes.

See [`Outline`](outline.md) Examples for an example of subscribing to this event.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>callback</code>
      </td>
      <td style="text-align:left">
        <p> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function"><code>Function</code></a> to
          be called when the outline changes.</p>
        <ul>
          <li> <code>mutation</code> &#x2014; <a href="mutation.md"><code>Mutation</code></a> describing
            the changes.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

| Return Values |
| :--- |
| Returns a [`Disposable`](https://atom.io/docs/api/latest/Disposable) on which `.dispose()` can be called to unsubscribe. |

 `::onDidEndChanges(callback)`

Invoke the given callback when the outline ends a series of changes.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>callback</code>
      </td>
      <td style="text-align:left">
        <p> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function"><code>Function</code></a> to
          be called when the outline ends updating.</p>
        <ul>
          <li> <code>changes</code> &#x2014; <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array"><code>Array</code></a> of
            <a
            href="mutation.md"><code>Mutation</code>
              </a>s.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

| Return Values |
| :--- |
| Returns a [`Disposable`](https://atom.io/docs/api/latest/Disposable) on which `.dispose()` can be called to unsubscribe. |

 `::onDidUpdateChangeCount(callback)`

Invoke the given callback when the outline’s change count is updated.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>callback</code>
      </td>
      <td style="text-align:left">
        <p> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function"><code>Function</code></a> to
          be called when change count is updated.</p>
        <ul>
          <li> <code>changeType</code> &#x2014; The type of change made to the document.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

| Return Values |
| :--- |
| Returns a [`Disposable`](https://atom.io/docs/api/latest/Disposable) on which `.dispose()` can be called to unsubscribe. |

 `::onDidDestroy(callback)`

Invoke the given callback when the outline is destroyed.

| Argument | Description |
| :--- | :--- |
| `callback` |  [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) to be called when the outline is destroyed. |

| Return Values |
| :--- |
| Returns a [`Disposable`](https://atom.io/docs/api/latest/Disposable) on which `.dispose()` can be called to unsubscribe. |

## Reading Items <a id="reading-items"></a>

 `::root`

Read-only root [`Item`](item.md) in the outline. `::items`

Read-only [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) [`Item`](item.md) s in the outline \(except the root\). `::getItemForID(id)`

| Argument | Description |
| :--- | :--- |
| `id` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) id. |

| Return Values |
| :--- |
| Returns [`Item`](item.md) for given id. |

 `::evaluateItemPath(itemPath, contextItem?)`

Evaluate the [item path search](../searches.md) starting from this outline’s [`Outline.root`](outline.md#static-root) item or from the passed in `contextItem` if present.

| Argument | Description |
| :--- | :--- |
| `itemPath` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) itempath expression. |
| `contextItem?` | defaults to [`Outline.root`](outline.md#static-root) . |

| Return Values |
| :--- |
| Returns an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of matching [`Item`](item.md) s. |

## Creating Items <a id="creating-items"></a>

 `::createItem(text?)`

Create a new item. The new item is owned by this outline, but is not yet inserted into it so it won’t be visible until you insert it.

| Argument | Description |
| :--- | :--- |
| `text?` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) or [`AttributedString`](attributedstring.md) . |

 `::cloneItem(item, deep?)`

The cloned item is owned by this outline, but is not yet inserted into it so it won’t be visible until you insert it.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to clone. |
| `deep?` | defaults to true. |

| Return Values |
| :--- |
| Returns Clone of the given [`Item`](item.md) . |

 `::importItem(item, deep?)`

Creates a clone of the given [`Item`](item.md) from an external outline that can be inserted into the current outline.

| Argument | Description |
| :--- | :--- |
| `item` |  [`Item`](item.md) to import. |
| `deep?` | defaults to true. |

| Return Values |
| :--- |
| Returns [`Item`](item.md) clone. |

## Insert & Remove Items <a id="insert--remove-items"></a>

 `::insertItemsBefore(items, referenceItem)`

Insert the items before the given `referenceItem`. If the reference item isn’t defined insert at the end of this outline.

Unlike [`Item::insertChildrenBefore`](item.md#instance-insertChildrenBefore) this method uses [`Item::indent`](item.md#instance-indent) to determine where in the outline structure to insert the items. Depending on the indent value these items may become referenceItem’s parent, previous sibling, or unrelated.

| Argument | Description |
| :--- | :--- |
| `items` |  [`Item`](item.md) or [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s to insert. |
| `referenceItem` | Reference [`Item`](item.md) to insert before. |

 `::removeItems(items)`

Remove the items but leave their child items in the outline and give them new parents.

| Argument | Description |
| :--- | :--- |
| `items` |  [`Item`](item.md) or [`Item`](item.md) [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) to remove. |

## Changes <a id="changes"></a>

 `::isChanging`

Read-only [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) true if outline is changing. `::isChanged()`

Determine if the outline is changed.

| Return Values |
| :--- |
| Returns a [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) . |

 `::updateChangeCount()`

Updates the receiver’s change count according to the given change type. `::groupChanges(callback)`

Group changes to the outline for better performance.

| Argument | Description |
| :--- | :--- |
| `callback` | Callback that contains code to change [`Item`](item.md) s in this [`Outline`](outline.md) . |

## Undo <a id="undo"></a>

 `::groupUndo(callback)`

Group multiple changes into a single undo group.

| Argument | Description |
| :--- | :--- |
| `callback` | Callback that contains code to change [`Item`](item.md) s in this [`Outline`](outline.md) . |

 `::groupUndoAndChanges(callback)`

Group multiple changes into a single undo and change group. This is a shortcut for:

```text
outline.groupUndo(function() {
  outline.groupChanges(function() {
    console.log('all grouped up!');
  });
});
```

| Argument | Description |
| :--- | :--- |
| `callback` | Callback that contains code to change [`Item`](item.md) s in this [`Outline`](outline.md) . |

 `::undo()`

Undo the last undo group. `::redo()`

Redo the last undo group.

## Serialization <a id="serialization"></a>

 `::serialize(options?)`

Return a serialized [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) version of this Outline’s content.

| Argument | Description |
| :--- | :--- |
| `options?` | Serialization options as defined in . `type` key defaults to . |

 `::reloadSerialization(serialization, options?)`

Reload the content of this outline using the given string serilaization.

| Argument | Description |
| :--- | :--- |
| `serialization` |  [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) outline serialization. |
| `options?` | Deserialization options as defined in . `type` key defaults to . |

## Debug <a id="debug"></a>

 `::toString()`

| Return Values |
| :--- |
| Returns debug string for this item. |

