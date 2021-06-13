# brandonpittman/OmniFocus

## Notices

* It's possible that some of these scripts may not work correctly with OmniFocus 3 \(as they were all written before OF3 was released\). Feel free to let me know if you find anything not working. Pull requests are welcomed.
* Probably any script in this repo will require the library. Assume you need it.

## Why is there a new OmniFocus library?

I had previously written an OmniFocus library using JavaScript for Automation, but it's got issues that vanilla AppleScript does not. Also, I realized that I didn't really need the fancy regex abilities from JavaScript that I thought I needed, so I went back to standard AppleScript. It works just as well, and the source code is a lot more readable. I hope you find this new library useful.

* [**Download the library**](https://github.com/brandonpittman/OmniFocus/blob/master/OmniFocus%20Library/omnifocus.scpt?raw=true)
* [**Browse the repo Github**]()

## Basic Usage

Put _omnifocus.scpt_ in `~/Library/Script Libraries`, or else AppleScript won't know where to find it!

```text
use application "OmniFocus"
use O : script "omnifocus"

tell O
   set sel to selectedItems()
   deferDaily(sel)  # this will set all the selected tasks to start again after completion daily
   setDefer(sel, current date)

   set theTask to findTask("Log food") # find the first task whose name is "Log food"
   set theProject to findProject("Groceries")
   set theContext to findContext("Home")
   set theFolder to findFolder("Routine")

   # Parse using transport text (see below for details)
   parse("Do something! @home ::misc #5pm #tomorrow //This is a note")
end
```

## Transport Text

For those who don't know about transport text, it's a format that OmniFocus uses to parse task information like so:

`Do something! @home ::misc #5pm #tomorrow //This is a note`

The `!` makes `Do something` a flagged task. `@home` sets the context to "home". `::` is used for matching a project. Both `@` and `::` will fuzzy match existing contexts and projects. The first `#` is used for a defer date, while the second `#` is for a due date. Both support natural language parsing like the inspector in OmniFocus. Word of caution though, if only one `#` is present, OmniFocus assumes it's a due date. Lastly, `//` starts the note for a task. While more involved ways of creating OmniFocus tasks exist in the library, you'll find using `of.parse` as your primary means of creating tasks.

## Functions

```text
- selectedItems()
- parse(transportText)
- findContext(contextName)
- findProject(projectName)
- findFolder(folderName)
- findTask(taskName)
- allTasks()
- allProjects()
- allContexts()
- setDue(input, dueDate)
- setDefer(input, deferDate)
- setProject(input, projectName)
- setContext(input, contextName)
- namePrepend(input, prependString)
- nameAppend(input, appendString)
- inboxTasks()
- setComplete(input, booleanFlag)
- setSequential(input, booleanFlag)
- openPerspective(perspectiveName)
- inboxCount()
- errandsCount()
- landAndSeaCount()
- routineCount()
- computerName()
- setRepeat(input, repetitionRule)
- deferDaily(input)
- deferWeekly(input)
- deferMonthly(input)
- repeatDaily(input)
- repeatWeekly(input)
- repeatMonthly(input)
- clearRepeat(input)
- clearDefer(input)
- clearContainer(input) *Only works on inbox tasks.*
- clearContext(input)
- setOnHold(input)
- setActive(input)
- showAbout()
- toggleColon(input)
- setColon(input)
- clearColon(input)
- setPrefix(input, prefix)
- clearPrefix(input, prefix)
- clearPrefixAll(input)
- setConsider(input)
- clearConsider(input)
- toggleConsider(input)
- kindOf(input) *This will be a task, project, context or folder.*
- isProject(input)
- isContext(input)
- isTask(input)
- isFolder(input)
```

[![Buy Me A Coffee](https://camo.githubusercontent.com/0d50b40f26fab03e9eedcb918467d2372def6d6f43f29b7681087a5021d07cf4/68747470733a2f2f63646e2e6275796d6561636f666665652e636f6d2f627574746f6e732f64656661756c742d626c75652e706e67)](https://www.buymeacoffee.com/blp)

