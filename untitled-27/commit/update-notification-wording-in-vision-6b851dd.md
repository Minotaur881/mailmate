# Update notification wording in vision@6b851dd

[Permalink](update-notification-wording-in-vision-6b851dd.md)

[Browse files](https://github.com/brandonpittman/OmniFocus/tree/6b851dd883808b31b52f5a107874aeabd672604a)

 Update notification wording in vision

* Loading branch information

|  |  | @@ -1,26 +1,2 @@ |
| :--- | :--- | :--- |
|  |  |  use AppleScript version "2.4" -- Yosemite \(10.10\) or later |
|  |  |  use scripting additions |
|  |  |  use O : script "omnifocus" |
|  |  |  |
|  |  |  on main\(argv\) |
|  |  |  set sel to selectedItems\(\) of O |
|  |  |  |
|  |  |  repeat with \_sel in sel |
|  |  |  tell application "OmniFocus" |
|  |  |  if name of containing project of \_sel is "Vision" then |
|  |  |  set note of \_sel to name of \_sel & " \(Archiving " & date string of \(current date\) & "\)" & "\n" & note of \_sel |
|  |  |  set name of \_sel to argv |
|  |  |  else |
|  |  |  display notification "No vision tasks selected." |
|  |  |  end if |
|  |  |  end tell |
|  |  |  end repeat |
|  |  |  end main |
|  |  |  |
|  |  |  on run \(argv\) |
|  |  |  main\(argv\) |
|  |  |  end run |
|  |  |  |
|  |  |  on handle\_string\(argv\) |
|  |  |  main\(argv\) |
|  |  |  end handle\_string  |
|  |  |  use AppleScript version "2.4" -- Yosemite \(10.10\) or lateruse scripting additionsuse O : script "omnifocus"on main\(argv\) set sel to selectedItems\(\) of O repeat with \_sel in sel tell application "OmniFocus" if name of containing project of \_sel is "Vision" then set note of \_sel to name of \_sel & " \(Archiving " & date string of \(current date\) & "\)" & " |
|  |  |  " & note of \_sel set name of \_sel to argv else display notification "No vision tasks selected." end if end tell end repeatend mainon run display notification "No vision tasks selected."end runon handle\_string\(argv\) main\(argv\)end handle\_string  |
|  |  |  |

