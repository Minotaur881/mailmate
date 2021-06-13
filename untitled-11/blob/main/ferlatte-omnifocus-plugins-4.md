# ferlatte/omnifocus-plugins

[Permalink](https://github.com/ferlatte/omnifocus-plugins/blob/29e900a6ba8d5bf528931d3756710e423917ee19/defer-task-to-tomorrow.omnijs)

Cannot retrieve contributors at this time

|  | /\*{ |
| :--- | :--- |
|  |  "author": "Mark Ferlatte", |
|  |  "targets": \["omnifocus"\], |
|  |  "type": "action", |
|  |  "identifier": "net.cryptio.defer-task-to-tomorrow", |
|  |  "version": "0.1", |
|  |  "description": "Defers a task to tomorrow regardless of the current defer date.", |
|  |  "label": "Defer a task to tomorrow", |
|  |  "mediumLabel": "Defer a task to tomorrow", |
|  |  "paletteLabel": "Defer a task to tomorrow", |
|  |  }\*/ |
|  |  |
|  | /\* global Calendar, PlugIn \*/ |
|  |  |
|  | function dateForTomorrow\(\) { |
|  |  let calendar = Calendar.current; |
|  |  let oneDay = new DateComponents\(\); |
|  |  oneDay.day = 1; |
|  |  let now = new Date\(\); |
|  |  let today = calendar.startOfDay\(now\); |
|  |  return calendar.dateByAddingDateComponents\(today, oneDay\); |
|  | } |
|  |  |
|  | \(\(\) =&gt; { |
|  |  var action = new PlugIn.Action\(function\(selection\) { |
|  |  selection.tasks.forEach\(function\(task\) { |
|  |  task.deferDate = dateForTomorrow\(\); |
|  |  }\); |
|  |  }\); |
|  |  |
|  |  |
|  |  action.validate = function\(selection\){ |
|  |  return \(selection.tasks.length &gt; 0\); |
|  |  }; |
|  |  |
|  |  return action; |
|  | }\)\(\); |

