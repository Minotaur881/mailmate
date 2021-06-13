# ItemSerializer

A class for serializing and deserializing [`Item`](item.md) s.

## Format Constants <a id="format-constants"></a>

 `.ItemReferencesType`

Outline and item ID JSON for the pasteboard. `.BMLType`

BML type constant.

* HTML subset for representing outlines in HTML.

 `.OPMLType`

OPML type constant.

* See [https://en.wikipedia.org/wiki/OPML](https://en.wikipedia.org/wiki/OPML)

 `.TaskPaperType`

TaskPaper text type constant.

* Encode item structure with tabs.
* Encode item `data-*` attributes with `tag(value)` pattern.

 `.TEXTType`

Plain text type constant.

* Encode item structure with tabs.

## Serialize & Deserialize Items <a id="serialize--deserialize-items"></a>

 `.serializeItems(items, options?)`

Serialize items into a supported format.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>items</code>
      </td>
      <td style="text-align:left"> <a href="item.md"><code>Item</code></a>  <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array"><code>Array</code></a> to
        serialize.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>options?</code>
      </td>
      <td style="text-align:left">
        <p>Serialization options.</p>
        <ul>
          <li> <code>type</code> &#x2014; <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String"><code>String</code></a> (default:
            ItemSerializer.BMLType)</li>
          <li> <code>startOffset</code> &#x2014; <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number"><code>Number</code></a> (default:
            0) Offset into first into to start at.</li>
          <li> <code>endOffset</code> &#x2014; <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number"><code>Number</code></a> (default:
            lastItem.bodyString.length) Offset from end of last item to end at.</li>
          <li> <code>expandedItems</code> &#x2014; <a href="item.md"><code>Item</code></a> 
            <a
            href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array"><code>Array</code>
              </a>of expanded items</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

 `.deserializeItems(itemsData, outline, options)`

Deserialize items from a supported format.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>itemsData</code>
      </td>
      <td style="text-align:left"> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String"><code>String</code></a> to
        deserialize.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>outline</code>
      </td>
      <td style="text-align:left"> <a href="outline.md"><code>Outline</code></a> to use when creating deserialized
        items.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>options</code>
      </td>
      <td style="text-align:left">
        <p>Deserialization options.</p>
        <ul>
          <li> <code>type</code> &#x2014; <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String"><code>String</code></a> (default:
            ItemSerializer.TEXTType)</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

| Return Values |
| :--- |
| Returns [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) of [`Item`](item.md) s. |

