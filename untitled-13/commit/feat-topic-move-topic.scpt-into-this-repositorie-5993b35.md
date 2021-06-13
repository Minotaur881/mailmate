# feat\(topic\): Move Topic.scpt into this repositorie@5993b35

[Permalink](feat-topic-move-topic.scpt-into-this-repositorie-5993b35.md)

[Browse files](https://github.com/FradSer/automation-omnifocus-3/tree/5993b3516b0bb97a2d6ad54c4cad459ad9a50d20)

 feat\(topic\): Move Topic.scpt into this repositorie

* Loading branch information

|  |  | @@ -0,0 +1,21 @@ |
| :--- | :--- | :--- |
|  |  |  The MIT License \(MIT\) |
|  |  |  |
|  |  |  Copyright \(c\) 2016 Frad Lee |
|  |  |  |
|  |  |  Permission is hereby granted, free of charge, to any person obtaining a copy |
|  |  |  of this software and associated documentation files \(the "Software"\), to deal |
|  |  |  in the Software without restriction, including without limitation the rights |
|  |  |  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell |
|  |  |  copies of the Software, and to permit persons to whom the Software is |
|  |  |  furnished to do so, subject to the following conditions: |
|  |  |  |
|  |  |  The above copyright notice and this permission notice shall be included in all |
|  |  |  copies or substantial portions of the Software. |
|  |  |  |
|  |  |  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR |
|  |  |  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, |
|  |  |  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE |
|  |  |  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER |
|  |  |  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, |
|  |  |  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE |
|  |  |  SOFTWARE. |

|  |  | @@ -0,0 +1,2 @@ |
| :--- | :--- | :--- |
|  |  |  \# Topic.scpt |
|  |  |  Another useful script for OmniFocus 2. |

|  |  | @@ -0,0 +1,17 @@ |
| :--- | :--- | :--- |
|  |  |  \# Change Log |
|  |  |  All notable changes to this project will be documented in this file. |
|  |  |  |
|  |  |  \#\# \[0.1.0\] - 2016-08-02 |
|  |  |  \#\#\# Added |
|  |  |  - Quick add "$project: \[projectTitle\]" to note of project |
|  |  |  |
|  |  |  \#\# \[0.0.2\] - 2016-06-15 |
|  |  |  \#\#\# Added |
|  |  |  - Control of notification |
|  |  |  |
|  |  |  \#\# 0.0.1 - 2016-06-12 |
|  |  |  \#\#\# Added |
|  |  |  - Replace \`$topic\` in name of task by setting in note of task's project |
|  |  |  |
|  |  |  \[0.0.2\]: https://github.com/FradSer/topic-for-omnifocus-2/compare/v0.0.1...v0.0.2 |
|  |  |  \[0.1.0\]: https://github.com/FradSer/topic-for-omnifocus-2/compare/v0.0.2...v0.1.0 |

|  |  | @@ -0,0 +1,14 @@ |
| :--- | :--- | :--- |
|  |  |  \#!/bin/sh |
|  |  |  |
|  |  |  rm ../Topic.scpt |
|  |  |  osacompile -o ../Topic.scpt Topic.applescript |
|  |  |  \# Take an image and make the image its own icon: |
|  |  |  sips -i icon.icns |
|  |  |  \# Extract the icon to its own resource file: |
|  |  |  DeRez -only icns icon.icns &gt; tmpicns.rsrc |
|  |  |  \# append this resource to the file you want to icon-ize. |
|  |  |  Rez -append tmpicns.rsrc -o ../Topic.scpt |
|  |  |  \# Use the resource to set the icon. |
|  |  |  SetFile -a C ../Topic.scpt |
|  |  |  \# clean up. |
|  |  |  rm tmpicns.rsrc |

|  |  | @@ -0,0 +1,44 @@ |
| :--- | :--- | :--- |
|  |  |  \(\* |
|  |  |  Topic.applescript |
|  |  |  By Frad Lee of \[Hello from FradSer\]\(http://fradser.me\). |
|  |  |  See README for details. |
|  |  |  \*\) |
|  |  |  |
|  |  |  -- PROPS |
|  |  |  property isNotify : false |
|  |  |  |
|  |  |  property scriptSuiteName : "Frad's Scripts" |
|  |  |  |
|  |  |  -- MAIN |
|  |  |  set newTopic to missing value |
|  |  |  tell application "OmniFocus" |
|  |  |  tell front document |
|  |  |  tell content of document window 1 |
|  |  |  set anProject to value of \(first descendant tree where class of its value is project\) |
|  |  |  set projectNote to note of anProject |
|  |  |  set projectTitle to name of anProject |
|  |  |  if projectNote does not contain "$topic" then |
|  |  |  set topicName to do shell script "echo '" & projectTitle & "'\|sed 's/\\\[//' \| sed 's/\\\]//'" |
|  |  |  set note of anProject to projectNote & return & "------------------------" & return & "$topic: " & topicName |
|  |  |  else |
|  |  |  set allTask to value of \(every descendant tree where class of its value is task\) |
|  |  |  repeat with anTask in allTask |
|  |  |  if name of anTask contains "$topic" then |
|  |  |  set newTopic to do shell script "echo '" & projectNote & "' \| sed -n '/$topic: /p' \| sed 's/$topic: //g'" |
|  |  |  set taskTitle to name of anTask |
|  |  |  set name of anTask to do shell script "echo '" & taskTitle & "' \| sed 's/$topic/\#" & newTopic & " /g'" |
|  |  |  if \(newTopic is not missing value\) and \(isNotify\) then |
|  |  |  my notify\("Changed topic.", newTopic\) |
|  |  |  end if |
|  |  |  end if |
|  |  |  end repeat |
|  |  |  end if |
|  |  |  end tell |
|  |  |  end tell |
|  |  |  end tell |
|  |  |  |
|  |  |  -- NOTIFY |
|  |  |  |
|  |  |  on notify\(theTitle, theDescription\) |
|  |  |  display notification theDescription with title scriptSuiteName subtitle theTitle |
|  |  |  end notify  |

