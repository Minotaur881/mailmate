# ksalzke/estimate-total-time-omnifocus-plugin

[Permalink](https://github.com/ksalzke/estimate-total-time-omnifocus-plugin/blob/0e142ae0924bcddabf4b5020fb64e879e615fda2/estimateTotalTime.omnifocusjs)

Cannot retrieve contributors at this time

|  | /\* global PlugIn Task Alert \*/ |
| :--- | :--- |
|  | /\*{ |
|  | "type": "action", |
|  | "targets": \["omnifocus"\], |
|  | "author": "Kaitlin Salzke", |
|  | "identifier": "com.KaitlinSalzke.estimateTotalTime", |
|  | "version": "1.0", |
|  | "description": "Estimates the total time of the selected items", |
|  | "label": "Estimate Total Time", |
|  | "shortLabel": "Estimate Total Time" |
|  | }\*/ |
|  |  |
|  | \(\(\) =&gt; { |
|  |  const action = new PlugIn.Action\(function \(selection, sender\) { |
|  |  let totalTime = 0 |
|  |  const noEstimate = \[\] |
|  |  |
|  |  function accumulate \(task\) { |
|  |  if \(task.estimatedMinutes === null\) { |
|  |  noEstimate.push\(task.name\) |
|  |  } |
|  |  totalTime += task.estimatedMinutes |
|  |  } |
|  |  |
|  |  selection.projects.forEach\(function \(project\) { |
|  |  project.task.apply\(\(task\) =&gt; { |
|  |  if \( |
|  |  !task.hasChildren && |
|  |  task.taskStatus !== Task.Status.Dropped && |
|  |  task.taskStatus !== Task.Status.Completed |
|  |  \) { |
|  |  accumulate\(task\) |
|  |  } |
|  |  }\) |
|  |  }\) |
|  |  |
|  |  selection.tasks.forEach\(accumulate\) |
|  |  |
|  |  selection.tags.forEach\(function \(tag\) { |
|  |  // 'remainingTasks' not used as there is currently an OF bug - this returns available tasks only |
|  |  tag.tasks.forEach\(\(task\) =&gt; { |
|  |  if \( |
|  |  task.taskStatus !== Task.Status.Dropped && |
|  |  task.taskStatus !== Task.Status.Completed |
|  |  \) { |
|  |  accumulate\(task\) |
|  |  } |
|  |  }\) |
|  |  }\) |
|  |  |
|  |  showEstimatedTimes\(totalTime, noEstimate\) |
|  |  }\) |
|  |  |
|  |  action.validate = function \(selection, sender\) { |
|  |  return selection.tasks.length &gt; 0 \|\| selection.projects.length &gt; 0 \|\| selection.tags.length &gt; 0 |
|  |  } |
|  |  |
|  |  return action |
|  | }\)\(\) |
|  |  |
|  | function showEstimatedTimes \(totalTime, tasksWithNoEstimate\) { |
|  |  const hours = Math.floor\(totalTime / 60\) |
|  |  const minutes = totalTime % 60 |
|  |  |
|  |  // build string to show estimate of total time |
|  |  const hoursUnit = \(hours === 1\) ? 'hour' : 'hours' |
|  |  const minutesUnit = \(minutes === 1\) ? 'minute' : 'minutes' |
|  |  let timeString |
|  |  if \(hours === 0\) { |
|  |  timeString = minutes + ' ' + minutesUnit |
|  |  } else if \(minutes === 0\) { |
|  |  timeString = hours + ' ' + hoursUnit |
|  |  } else { |
|  |  timeString = |
|  |  hours + ' ' + hoursUnit + ' and ' + minutes + ' ' + minutesUnit |
|  |  } |
|  |  |
|  |  let warning |
|  |  switch \(tasksWithNoEstimate.length\) { |
|  |  case 0: |
|  |  warning = '' |
|  |  break |
|  |  case 1: |
|  |  warning = |
|  |  'Note that the following task has no estimate: \u201C' + |
|  |  tasksWithNoEstimate\[0\] + |
|  |  '\u201D.' |
|  |  break |
|  |  case 2: |
|  |  warning = |
|  |  'Note that the following 2 tasks have no estimate: \u201C' + |
|  |  tasksWithNoEstimate\[0\] + |
|  |  '\u201D and \u201C' + |
|  |  tasksWithNoEstimate\[1\] + |
|  |  '\u201D.' |
|  |  break |
|  |  default: |
|  |  warning = |
|  |  'Note that the following ' + |
|  |  tasksWithNoEstimate.length + |
|  |  ' tasks have no estimate: ' |
|  |  tasksWithNoEstimate.forEach\(function \(item, index, array\) { |
|  |  if \(index !== 0\) { |
|  |  warning += ', ' |
|  |  } |
|  |  if \(index === array.length - 1\) { |
|  |  warning += 'and ' |
|  |  } |
|  |  warning += |
|  |  '\u201C' + |
|  |  item + |
|  |  '\u201D' |
|  |  if \(index === array.length - 1\) { |
|  |  warning += '.' |
|  |  } |
|  |  }\) |
|  |  } |
|  |  |
|  |  // show result |
|  |  const alert = new Alert\('Estimated total time: ' + timeString + '.', warning\) |
|  |  alert.show\(\) |
|  | } |

