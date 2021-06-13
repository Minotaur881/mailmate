# Add Duration Titles@1d238ae

[Permalink](add-duration-titles-1d238ae.md)

|  |  | @@ -0,0 +1,24 @@ |
| :--- | :--- | :--- |
|  |  |  var of = Application\('OmniFocus'\); |
|  |  |  |
|  |  |  var doc = of.defaultDocument; |
|  |  |  |
|  |  |  var today = new Date\(\); |
|  |  |  var dueDate = new Date\(today.setDate\(today.getDate\(\)+7\)\); |
|  |  |  var taskList = \[\]; |
|  |  |  var flattenedTasks = doc.flattenedTasks.whose\({effectivelyCompleted: false, effectivelyDropped: false}\); |
|  |  |  |
|  |  |  flattenedTasks\(\).forEach\(function\(task\){ |
|  |  |  var splitString = task.name\(\).split\(" \|\| "\); |
|  |  |  var unit = ""; |
|  |  |  if \(task.estimatedMinutes\(\) !== null\) { |
|  |  |  if \(task.estimatedMinutes\(\) &gt; 1\){ |
|  |  |  unit = " \|\| " + task.estimatedMinutes\(\) + " mins"; |
|  |  |  } else { |
|  |  |  unit = " \|\| 1 min"; |
|  |  |  } |
|  |  |  } |
|  |  |  var newTitle = splitString\[0\] + unit; |
|  |  |  task.name = newTitle; |
|  |  |  }\); |
|  |  |  |
|  |  |  of.synchronize\(\);  |

|  |  | @@ -0,0 +1,7 @@ |
| :--- | :--- | :--- |
|  |  |  \# Duration Titles |
|  |  |  |
|  |  |  This script takes the Estimated Duration and appends it to the title of the task. The main reason for this is that the duration isn't easily accessed on iOS. So by putting it at the end of the task name, it now becomes visible everywhere you see the task. |
|  |  |  |
|  |  |  \# Development |
|  |  |  |
|  |  |  I'm certainly open to the submission of Pull Requests to make this better. If you find issues and fix them, please let me know and I'll be happy to update and give you credit. |

