# Creating Scripts

Create scripts to automate TaskPaper and integrate with other apps.

## Getting Started <a id="getting-started"></a>

```text
function TaskPaperContextScript(editor, options) {
  return editor.selection.selectedItems.map(
    function (item) {
      return item.bodyString
    }
  )
}

Application("TaskPaper").documents[0].evaluate({
  script: TaskPaperContextScript.toString()
})
```

1. Open the "AppleScript Editor" application.
2. Paste the above script into a new editor window.
3. Make sure that the scripting language is set to "JavaScript".
4. Run the script and the text of each selected item displays in the AppleScript Editor Results area. You've run a script!

See the [Scripting API](https://www.taskpaper.com/guide/reference/scripting) for API level documentation.

## TaskPaper's JavaScript Context <a id="taskpapers-javascript-context"></a>

TaskPaper specific scripting happens in TaskPaper's JavaScript context.

Use the `evaluate` command to pass JavaScript code into TaskPaper's JavaScript Context. The script that you pass in is then evaluated and run within TaskPaper in a JavaScript context.

In the Script Editor context:

1. Your script is running within Script Editor.
2. Your script can interact with other scriptable applications.
3. Your script can access TaskPaper's standard scripting suite objects such as the documents list.
4. Your script makes calls to TaskPaper's `evaluate` command.
5. Your script may use JavaScript or AppleScript syntax.

In the TaskPaper JavaScript context:

1. Your script must use JavaScript syntax.
2. TaskPaper uses Javascript's `eval` function to create a function from your script.
3. Your script is then run from within TaskPaper's JavaScript context.
4. Your script can interact with TaskPaper's model objects such as the OutlineEditor.
5. Your can use TaskPaper's Window &gt; JavaScript Debugger to debug your script.

## Debugging TaskPaper's JavaScript Context <a id="debugging-taskpapers-javascript-context"></a>

To debug your script \(TaskPaper 3.2 and above\):

1. Open Safari
2. Open TaskPaper
3. Ensure Safari’s “Develop” menu is showing.
4. Choose Safari &gt; Develop &gt; Computer &gt; TaskPaper &gt; BirchOutlineJavascriptContext

You should now see a debug window for TaskPaper’s JavaScript context. Add a `debugger` statement to your script and your script will pause at that point in the debugger window. For example:

```text
function TaskPaperContextScript(editor, options) {
    debugger;
}

Application("TaskPaper").documents[0].evaluate({
  script: TaskPaperContextScript.toString()
})
```

**Note** Debugging won't work in the Mac App Store version of TaskPaper. It works with the version of TaskPaper that you download from [TaskPaper.com](https://www.taskpaper.com/). If you have purchased the Mac App Store version run it once on your computer. Then you can run the direct download version without having to buy a second license.

## Cross-Platform Scripts <a id="cross-platform-scripts"></a>

[Birch-outline](https://github.com/jessegrosjean/birch-outline) enables cross-platform scripting for TaskPaper.

Use birch-outline to parse, process, and save TaskPaper files wherever you have JavaScript. It's not just a parser. Birch-outline also includes TaskPaper's runtime model–Giving you the same scripting behavior that you have when scripting TaskPaper.app.

