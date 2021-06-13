# Using the Sidebar

Use the sidebar to focus projects, activate searches, or filter by tag.

The sidebar has three sections: projects, searches, and tags. You can hide any section by clicking the "Hide" button that shows to the right of the section title when you move your mouse over it.

### Projects <a id="projects"></a>

1. To focus a project select it in the sidebar.
2. Drag and drop to reorder projects in the sidebar.
3. You can also drag and drop items from the editor onto projects in the sidebar.
4. Double-click on project in sidebar to "hoist". Hide the item, but show its descendants.

## Searches <a id="searches"></a>

The searches section shows saved searches.

1. To create a saved search right-click on the "Searches" sidebar heading and choose New Search.
2. To edit a saved search right-click on the search in the sidebar and choose Edit Search.
3. In the search edit sheet there's a checkbox that determines where the search gets saved. Embedded in the current document, or saved into a common "searches" configuration file.

TaskPaper stored saved searches using `@search` tags. Here's an example that you can paste into your own document:

```text
Todo @search(@today and not @done)
```

There are some quirks when editing `@search` tags. In particular if your search has a `(` or `)` you **must** escape them by preceding them with a `\` character.

Use the View &gt; New Sidebar Search to show a search editing sheet that avoid this issue.

The tags section shows tags from the current document and the "tags" configuration file. Try it, enter a `@newtag` into your document and note that it shows up in the sidebar.

## Configuration Files <a id="configuration-files"></a>

To view and edit the above described configuration files:

1. Choose the menu item: Window &gt; StyleSheet &gt; Open StyleSheet Folder
2. Locate the "Configurations" folder, which is a sibling to the "StyleSheets" folder
3. Edit the contained "searches" or "tags" configuration file. As soon as you save your edits TaskPaper's sidebar should reflect the changes.

