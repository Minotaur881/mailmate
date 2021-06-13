# ferlatte/omnifocus-plugins

[Permalink](https://github.com/ferlatte/omnifocus-plugins/blob/29e900a6ba8d5bf528931d3756710e423917ee19/clear-flag-from-tasks.omnijs)

Cannot retrieve contributors at this time

|  | /\*{ |
| :--- | :--- |
|  |  "author": "Mark Ferlatte", |
|  |  "targets": \["omnifocus"\], |
|  |  "type": "action", |
|  |  "identifier": "net.cryptio.clear-flag-from-tasks", |
|  |  "version": "0.1", |
|  |  "description": "Clear flag from uncompleted tasks.", |
|  |  "label": "Clear flag from uncompleted tasks", |
|  |  "mediumLabel": "Clear flag from uncompleted tasks", |
|  |  "paletteLabel": "Clear flag from uncompleted tasks", |
|  |  }\*/ |
|  |  |
|  | /\* global PlugIn, flattenedTasks, Task \*/ |
|  |  |
|  | \(\(\) =&gt; { |
|  |  var action = new PlugIn.Action\(function\(\) { |
|  |  let tasks = flattenedTasks.filter\(task =&gt; { |
|  |  return task.taskStatus !== Task.Status.Completed; |
|  |  }\).filter\(task =&gt; { |
|  |  return task.taskStatus !== Task.Status.Dropped; |
|  |  }\); |
|  |  tasks.forEach\(task =&gt; { |
|  |  task.flagged = false; |
|  |  }\); |
|  |  }\); |
|  |  |
|  |  action.validate = function\(\) { |
|  |  return true; |
|  |  }; |
|  |  |
|  |  return action; |
|  | }\)\(\); |

