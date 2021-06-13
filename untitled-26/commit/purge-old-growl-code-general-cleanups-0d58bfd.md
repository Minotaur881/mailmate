# Purge old Growl code; general cleanups@0d58bfd

|  | @@ -10,13 +10,16 @@ |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  \# LICENSE \# |
|  |  |  |
|  |  |  Copyright © 2015-2017 Dan Byler \(contact: dbyler@gmail.com\) |
|  |  |  Copyright © 2015-2020 Dan Byler \(contact: dbyler@gmail.com\) |
|  |  |  Licensed under MIT License \(http://www.opensource.org/licenses/mit-license.php\) |
|  |  |  \(TL;DR: no warranty, do whatever you want with it.\) |
|  |  |  |
|  |  |  |
|  |  |  \# CHANGE HISTORY \# |
|  |  |  |
|  |  |  2020-02-14 |
|  |  |  - Purge old Growl code; general cleanups |
|  |  |  |
|  |  |  2017-04-23 |
|  |  |  - Fixes an issue when running with certain top-level category separators selected |
|  |  |  - Minor update to notification code |
|  | @@ -27,18 +30,9 @@ |  |
|  |  |  |
|  |  |  2015-05-09 |
|  |  |  - Original release |
|  |  |  |
|  |  |  \*\) |
|  |  |  |
|  |  |  -- To change settings, modify the following properties |
|  |  |  property showSummaryNotification : true --if true, will display success notifications |
|  |  |  |
|  |  |  -- Don't change these |
|  |  |  property growlAppName : "Dan's Scripts" |
|  |  |  property allNotifications : {"General", "Error"} |
|  |  |  property enabledNotifications : {"General", "Error"} |
|  |  |  property iconApplication : "OmniFocus.app" |
|  |  |  |
|  |  |  property showNotification : true --if true, will display success notifications |
|  |  |  |
|  |  |  on main\(q\) |
|  |  |  if q is missing value then |
|  | @@ -48,97 +42,33 @@ on main\(q\) |  |
|  |  |  tell application "OmniFocus" |
|  |  |  tell content of first document window of front document |
|  |  |  --Get selection |
|  |  |  set validSelectedItemsList to value of \(selected trees where class of its value is not item and class of its value is not folder and class of its value is not context and class of its value is not perspective\) |
|  |  |  set validSelectedItemsList to value of \(selected trees where class of its value is not item and class of its value is not folder and class of its value is not tag and class of its value is not perspective\) |
|  |  |  set totalItems to count of validSelectedItemsList |
|  |  |  if totalItems is 0 then |
|  |  |  set alertName to "Error" |
|  |  |  set alertTitle to "Error" |
|  |  |  set alertText to "No valid task\(s\) selected" |
|  |  |  my notify\(alertName, alertTitle, alertText\) |
|  |  |  display notification "No valid task\(s\) selected" with title "Error" |
|  |  |  return |
|  |  |  end if |
|  |  |  |
|  |  |  if totalItems &gt; 1 then |
|  |  |  display dialog "Multiple items selected. Continue?" buttons {"Cancel", "OK"} default button 2 |
|  |  |  end if |
|  |  |  |
|  |  |  repeat with thisItem in validSelectedItemsList |
|  |  |  tell thisItem |
|  |  |  repeat with myTask in validSelectedItemsList |
|  |  |  tell myTask |
|  |  |  insert q & " |
|  |  |  |
|  |  |  " at before first paragraph of note |
|  |  |  end tell |
|  |  |  end repeat |
|  |  |  |
|  |  |  if showSummaryNotification then |
|  |  |  set alertName to "General" |
|  |  |  set alertTitle to "\"" & q & "\"" |
|  |  |  if length of alertTitle &gt; 20 then |
|  |  |  set alertTitle to \(text 1 thru 20 of alertTitle\) & "É\"" |
|  |  |  end if |
|  |  |  if totalItems &gt; 1 then |
|  |  |  set alertText to "Note appended to " & totalItems & " selected tasks" |
|  |  |  else |
|  |  |  set alertText to "Note appended to: |
|  |  |  " & name of first item in validSelectedItemsList |
|  |  |  if showNotification then |
|  |  |  set alertTitle to "Note added to " & name of myTask |
|  |  |  set alertText to "\"" & q & "\"" |
|  |  |  display notification alertText with title alertTitle |
|  |  |  end if |
|  |  |  my notify\(alertName, alertTitle, alertText\) |
|  |  |  end if |
|  |  |  |
|  |  |  end repeat |
|  |  |  end tell |
|  |  |  end tell |
|  |  |  end main |
|  |  |  |
|  |  |  |
|  |  |  \(\* Begin notification code \*\) |
|  |  |  on notify\(alertName, alertTitle, alertText\) |
|  |  |  --Call this to show a normal notification |
|  |  |  my notifyMain\(alertName, alertTitle, alertText, false\) |
|  |  |  end notify |
|  |  |  |
|  |  |  on notifyWithSticky\(alertName, alertTitle, alertText\) |
|  |  |  --Show a sticky Growl notification |
|  |  |  my notifyMain\(alertName, alertTitle, alertText, true\) |
|  |  |  end notifyWithSticky |
|  |  |  |
|  |  |  on IsGrowlRunning\(\) |
|  |  |  tell application "System Events" to set GrowlRunning to \(count of \(every process where creator type is "GRRR"\)\) &gt; 0 |
|  |  |  return GrowlRunning |
|  |  |  end IsGrowlRunning |
|  |  |  |
|  |  |  on notifyWithGrowl\(growlHelperAppName, alertName, alertTitle, alertText, useSticky\) |
|  |  |  tell my application growlHelperAppName |
|  |  |  Çevent registerÈ given Çclass applÈ:growlAppName, Çclass anotÈ:allNotifications, Çclass dnotÈ:enabledNotifications, Çclass iappÈ:iconApplication |
|  |  |  Çevent notifygrÈ given Çclass nameÈ:alertName, Çclass titlÈ:alertTitle, Çclass applÈ:growlAppName, Çclass descÈ:alertText |
|  |  |  end tell |
|  |  |  end notifyWithGrowl |
|  |  |  |
|  |  |  on NotifyWithoutGrowl\(alertText, alertTitle\) |
|  |  |  display notification alertText with title alertTitle |
|  |  |  end NotifyWithoutGrowl |
|  |  |  |
|  |  |  on notifyMain\(alertName, alertTitle, alertText, useSticky\) |
|  |  |  set GrowlRunning to my IsGrowlRunning\(\) --check if Growl is running... |
|  |  |  if not GrowlRunning then --if Growl isn't running... |
|  |  |  set GrowlPath to "" --check to see if Growl is installed... |
|  |  |  try |
|  |  |  tell application "Finder" to tell \(application file id "GRRR"\) to set strGrowlPath to POSIX path of \(its container as alias\) & name |
|  |  |  end try |
|  |  |  if GrowlPath is not "" then --...try to launch if so... |
|  |  |  do shell script "open " & strGrowlPath & " &gt; /dev/null 2&gt;&1 &" |
|  |  |  delay 0.5 |
|  |  |  set GrowlRunning to my IsGrowlRunning\(\) |
|  |  |  end if |
|  |  |  end if |
|  |  |  if GrowlRunning then |
|  |  |  tell application "Finder" to tell \(application file id "GRRR"\) to set growlHelperAppName to name |
|  |  |  notifyWithGrowl\(growlHelperAppName, alertName, alertTitle, alertText, useSticky\) |
|  |  |  else |
|  |  |  NotifyWithoutGrowl\(alertText, alertTitle\) |
|  |  |  end if |
|  |  |  end notifyMain |
|  |  |  \(\* end notification code \*\) |
|  |  |  |
|  |  |  main\(missing value\) |
|  |  |  |
|  |  |  on alfred\_script\(q\) |
|  |  |  |

