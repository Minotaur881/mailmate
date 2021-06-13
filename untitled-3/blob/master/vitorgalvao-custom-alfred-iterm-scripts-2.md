# vitorgalvao/custom-alfred-iterm-scripts

[Permalink](https://github.com/vitorgalvao/custom-alfred-iterm-scripts/blob/95bc444c2c1a2f166bb3f5b0d7f59707e241a361/custom_iterm_script.applescript)

Cannot retrieve contributors at this time

|  | -- For the latest version: |
| :--- | :--- |
|  | -- https://github.com/vitorgalvao/custom-alfred-iterm-scripts |
|  |  |
|  | -- Set this property to true to always open in a new window |
|  | property open\_in\_new\_window : false |
|  |  |
|  | -- Handlers |
|  | on new\_window\(\) |
|  |  tell application "iTerm" to create window with default profile |
|  | end new\_window |
|  |  |
|  | on new\_tab\(\) |
|  |  tell application "iTerm" to tell the first window to create tab with default profile |
|  | end new\_tab |
|  |  |
|  | on call\_forward\(\) |
|  |  tell application "iTerm" to activate |
|  | end call\_forward |
|  |  |
|  | on is\_running\(\) |
|  |  application "iTerm" is running |
|  | end is\_running |
|  |  |
|  | on has\_windows\(\) |
|  |  if not is\_running\(\) then return false |
|  |  if windows of application "iTerm" is {} then return false |
|  |  true |
|  | end has\_windows |
|  |  |
|  | on send\_text\(custom\_text\) |
|  |  tell application "iTerm" to tell the first window to tell current session to write text custom\_text |
|  | end send\_text |
|  |  |
|  | -- Main |
|  | on alfred\_script\(query\) |
|  |  if has\_windows\(\) then |
|  |  if open\_in\_new\_window then |
|  |  new\_window\(\) |
|  |  else |
|  |  new\_tab\(\) |
|  |  end if |
|  |  else |
|  |  -- If iTerm is not running and we tell it to create a new window, we get two |
|  |  -- One from opening the application, and the other from the command |
|  |  if is\_running\(\) then |
|  |  new\_window\(\) |
|  |  else |
|  |  call\_forward\(\) |
|  |  end if |
|  |  end if |
|  |  |
|  |  -- Make sure a window exists before we continue, or the write may fail |
|  |  repeat until has\_windows\(\) |
|  |  delay 0.01 |
|  |  end repeat |
|  |  |
|  |  send\_text\(query\) |
|  |  call\_forward\(\) |
|  | end alfred\_script |

