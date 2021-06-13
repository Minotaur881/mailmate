# Update script comments@cef698e

[Permalink](update-script-comments-cef698e.md)

[Browse files](../tree/metbril-omnifocus-scripts.md)

 Update script comments

* Loading branch information

 Showing with **13 additions** and **3 deletions**.

1.  +13 −3 [Birthdays.applescript](update-script-comments-cef698e.md#diff-edcd4dd28e472b53d44d943cc8104c307f89f03af5fb13d33fc630ce20354321)

|  |  | @@ -1,7 +1,7 @@ |
| :--- | :--- | :--- |
|  |  |  \(\* |
|  |  |  ========== |
|  |  |  Name : Birthdays |
|  |  |  Description : Add a task to OmniFocus Inbox for each contact with a nearby birthday |
|  |  |  Name : Add Birthdays to OmniFocus |
|  |  |  Description : Add a task to OmniFocus Inbox for contacts with close birthdays |
|  |  |  Author : Robert van Bregt \(https://robertvanbregt.nl/\) |
|  |  |  |
|  |  |  Known bugs and features: |
|  | @@ -21,6 +21,10 @@ property AHEAD : 7 |  |
|  |  |  set cdt to \(current date\) |
|  |  |  set cyr to year of \(current date\) |
|  |  |  |
|  |  |  set s to date string of \(current date\) |
|  |  |  -- display notification s |
|  |  |  |
|  |  |  |
|  |  |  tell application "Contacts" |
|  |  |  |
|  |  |  -- get all people with a birth date |
|  | @@ -41,6 +45,8 @@ tell application "Contacts" |  |
|  |  |  |
|  |  |  if \(bdy is greater than cdt\) and \(bdy is less than \(cdt + AHEAD \* days\)\) then |
|  |  |  |
|  |  |  log "Matching birth day: " & short date string of bdy |
|  |  |  |
|  |  |  if \(byr = 1604\) then -- unknown year |
|  |  |  set age to "zoveelste" |
|  |  |  else |
|  | @@ -77,13 +83,17 @@ tell application "Contacts" |  |
|  |  |  set task\_defer to bdy - 12 \* hours |
|  |  |  set task\_due to bdy + 8 \* hours |
|  |  |  |
|  |  |  |
|  |  |  set task\_note to "--- |
|  |  |  Van harte gefeliciteerd met je " & age & " verjaardag. Geniet van je dag. |
|  |  |  --- |
|  |  |  " & task\_phone & " |
|  |  |  " & task\_email & " |
|  |  |  ---" |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  tell application "OmniFocus" |
|  |  |  tell default document |
|  |  |  make new inbox task with properties Â |
|  | @@ -92,7 +102,6 @@ Van harte gefeliciteerd met je " & age & " verjaardag. Geniet van je dag. |  |
|  |  |  |
|  |  |  end tell |
|  |  |  end tell |
|  |  |  |
|  |  |  end if |
|  |  |  |
|  |  |  end repeat |
|  | @@ -112,3 +121,4 @@ on removeGarbageFromLabel\(theLabel\) |  |
|  |  |  set theLabel to my findAndReplaceInText\(theLabel, "&gt;!$\_", ""\) |
|  |  |  return theLabel |
|  |  |  end removeGarbageFromLabel |
|  |  |  |

