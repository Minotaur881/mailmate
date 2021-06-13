# Allow more than ten codes@3fba944

[Permalink](allow-more-than-ten-codes-3fba944.md)

[Browse files](https://github.com/joebuhlig/OFScripts/tree/3fba9445eff1d15f11ad0c5c132d0c9c9e6b72c2)

 Allow more than ten codes

* Loading branch information

 Showing with **2 additions** and **3 deletions**.

1.  +2 −3 [Project Codes/ProjectCodes.applescript](allow-more-than-ten-codes-3fba944.md#diff-120970c9172fd0b2386bdacd182b7233195be7dddde4a3dc8ae3534fed7cf971)

|  |  | @@ -1,4 +1,4 @@ |
| :--- | :--- | :--- |
|  |  |  set notesDirectory to "/Users/USERNAME/notes/" |
|  |  |  set notesDirectory to "/Users/joebuhlig/notes.joebuhlig/notes/" |
|  |  |  set projectsFileName to "project-codes.md" |
|  |  |  tell application "Finder" |
|  |  |  if exists \(notesDirectory & projectsFileName\) as POSIX file then |
|  | @@ -16,14 +16,13 @@ if projectsList is not equal to "" then |  |
|  |  |  set dateCode to first text item of projectsList |
|  |  |  set AppleScript's text item delimiters to "-" |
|  |  |  set existingYear to text 3 thru 6 of \(first text item of dateCode\) |
|  |  |  set existingCode to last text item of dateCode |
|  |  |  set AppleScript's text item delimiters to oldDelimiters |
|  |  |  log existingYear |
|  |  |  else |
|  |  |  set existingYear to "1900" |
|  |  |  end if |
|  |  |  set currentYear to year of \(current date\) as string |
|  |  |  if existingYear = currentYear then |
|  |  |  set existingCode to last text item of dateCode |
|  |  |  set newNumber to "0000" & \(\(existingCode as number\) + 1\) as string |
|  |  |  set numberString to text \(\(length of newNumber\) - 3\) thru \(length of newNumber\) of newNumber |
|  |  |  else |
|  |  |  |

