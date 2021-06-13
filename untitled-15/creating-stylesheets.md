# Creating StyleSheets

Use stylesheets to set the fonts, colors, and other settings that TaskPaper uses to display and print your lists. To create your own custom StyleSheet:

1. Choose Window &gt; StyleSheet &gt; Open StyleSheet Folder
2. Inside that folder find \(or create\) a `.less` file and open it in a text editor.
3. Edit that file to create your own stylesheet.

TaskPaper stylesheets are live. Use this to your advantage. Make small changes and save often. TaskPaper's window will update right away.

## Example StyleSheets <a id="example-stylesheets"></a>

For each example:

1. Replace the content of your stylesheet with the example text.
2. Save your changes.
3. TaskPaper's windows should update with the new style.

```text
// This example increases the font size and tint color.
@user-font-size: 20;
@tint-color: green;
```

```text
// This example increases project font size and colors them red.
item[data-type=project] {
  font-size: 20;
  color: rgb(255, 0, 0);
}
```

```text
// This example colors items tagged with @today red
item[data-today] {
  color: rgb(255, 0, 0);
}
```

```text
// This example colors the tag text @today ... red!
run[tag=data-today] {
  color: rgb(255, 0, 0);
}
```

```text
// This example enables typewritter scrolling in the editor
editor {
  top-padding-percent: 25%;
  bottom-padding-percent: 50%;
  typewriter-scroll-percent: 50%;
}
```

```text
// This example enables text wrap in the editor
editor {
  editor-wrap-to-column: 100;
  item-wrap-to-column: 66;
}
```

