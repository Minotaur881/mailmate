# ChaunceyKiwi/omni-automation-script

[Permalink](https://github.com/ChaunceyKiwi/omni-automation-script/blob/1b8db02c2423e9005934ecb2513b23143edf762d/NoteToObject.omnijs)

Cannot retrieve contributors at this time

|  | /\*{ |
| :--- | :--- |
|  |  "type": "action", |
|  |  "targets": \["omnifocus"\], |
|  |  "author": "Chauncey Liu", |
|  |  "identifier": "com.omni-automation.of.note-to-object", |
|  |  "version": "1.0", |
|  |  "description": "This action will export selected task as JSON object.", |
|  |  "label": "Export as JSON Object", |
|  |  "shortLabel": "Export" |
|  | }\*/ |
|  | \(\(\) =&gt; { |
|  |  var action = new PlugIn.Action\(function \(selection, sender\) { |
|  |  var task = selection.tasks\[0\]; |
|  |  var textToWrite = JSON.stringify\(generateObject\(task\), null, 2\); |
|  |  console.log\(textToWrite\); |
|  |  if \(textToWrite === ""\) { |
|  |  var alertMsg = "There is no content to export"; |
|  |  new Alert\("Missing Data", alertMsg\).show\(\); |
|  |  } else { |
|  |  var textDataObj = Data.fromString\(textToWrite\); |
|  |  var textFileName = task.name + ".json"; |
|  |  var wrapper = FileWrapper.withContents\(textFileName, textDataObj\); |
|  |  var filesaver = new FileSaver\(\); |
|  |  var fileSaverPromise = filesaver.show\(wrapper\); |
|  |  |
|  |  fileSaverPromise.then\(function \(urlObj\) { |
|  |  console.log\(urlObj.string\); |
|  |  if \(Device.current.mac\) { |
|  |  var alertTitle = "File Created"; |
|  |  var alertMsg = "Open the file?"; |
|  |  var alert = new Alert\(alertTitle, alertMsg\); |
|  |  alert.addOption\("Open"\); |
|  |  alert.addOption\("Skip"\); |
|  |  alert.show\(function \(result\) { |
|  |  if \(result == 0\) { |
|  |  urlObj.open\(\); |
|  |  } |
|  |  }\); |
|  |  } |
|  |  }\); |
|  |  |
|  |  fileSaverPromise.catch\(function \(err\) { |
|  |  console.log\(err.message\); |
|  |  }\); |
|  |  } |
|  |  }\); |
|  |  |
|  |  let generateObject = \(item\) =&gt; { |
|  |  let obj = \[\]; |
|  |  |
|  |  // Only export an item if it has tags and is completed |
|  |  if \(item.tags.length &gt; 0 && item.completed\) { |
|  |  obj.push\({ |
|  |  Date: getDateString\(item.effectiveCompletedDate\), |
|  |  Tag: item.tags\[0\].name, |
|  |  Summary: item.name, |
|  |  }\); |
|  |  } |
|  |  for \(const childItem of item.children\) { |
|  |  obj = obj.concat\(generateObject\(childItem\)\); |
|  |  } |
|  |  return obj; |
|  |  }; |
|  |  |
|  |  var getDateString = \(date\) =&gt; { |
|  |  return \( |
|  |  new Intl.DateTimeFormat\("en", { year: "numeric" }\).format\(date\) + |
|  |  new Intl.DateTimeFormat\("en", { month: "2-digit" }\).format\(date\) + |
|  |  new Intl.DateTimeFormat\("en", { day: "2-digit" }\).format\(date\) |
|  |  \); |
|  |  }; |
|  |  |
|  |  action.validate = function \(selection, sender\) { |
|  |  // validation code |
|  |  // selection options: tasks, projects, folders, tags, allObjects |
|  |  return selection.tasks.length === 1; |
|  |  }; |
|  |  |
|  |  return action; |
|  | }\)\(\); |

