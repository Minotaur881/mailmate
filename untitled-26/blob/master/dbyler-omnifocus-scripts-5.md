# dbyler/omnifocus-scripts

[Permalink](https://github.com/dbyler/omnifocus-scripts/blob/6bc2fa08de5ab670242e8298f2392d348f03ef31/Focus%20in%20New%20Tab.applescript)

Cannot retrieve contributors at this time

|  | \(\* |
| :--- | :--- |
|  |  \# DESCRIPTION \# |
|  |  |
|  |  Opens the selected task's project in a new window so you can jump from a tag |
|  |  perspective view into the project without losing place. |
|  |  |
|  |  \(Also works with multiple items selected\) |
|  |  |
|  |  |
|  |  \# REQUIREMENTS \# |
|  |  |
|  |  1. You must be running macOS Sierra or later \(for tab support\) |
|  |  2. You need a Projects perspective called "Projects". This should be enabled in any default OmniFocus installation |
|  |  |
|  |  |
|  |  \# INSTALLATION \# |
|  |  |
|  |  This script requires a little jiu jitsu to work around macOS limitations. |
|  |  |
|  |  To run the script from LaunchBar or Alfred: |
|  |  |
|  |  - LaunchBar or Alfred will be the authorized app in System Preferences → Security & Privacy → Privacy → Accessibility. \(There's a good chance you've already done this.\) |
|  |  |
|  |  To run the script from the OmniFocus toolbar: |
|  |  |
|  |  - Save this script as an application \("FocusTabApp" in the zip file, or you can do this from Script Editor\) |
|  |  - Move FocusTabApp and FocusTab \(the helper script\) to the OmniFocus scripts folder \(OmniFocus → Help → Open Scripts Folder\) |
|  |  - Add FocusTabApp to your allowed applications in System Preferences → Security & Privacy → Privacy → Accessibility |
|  |  - Add FocusTab to the OmniFocus toolbar |
|  |  - ONLY IF NEEDED: Update the helper script \("FocusTab" in the zip file\) to point to to the location of FocusTabApp |
|  |  |
|  |  Why is this necessary? |
|  |  |
|  |  1. To use UI scripting, an application needs to be granted explicit access in the System Preferences → Security & Privacy → Privacy → Accessibility. \(For more information see https://developer.apple.com/library/content/documentation/LanguagesUtilities/Conceptual/MacAutomationScriptingGuide/AutomatetheUserInterface.html\) |
|  |  2. AppleScripts cannot be granted acccess in this way. |
|  |  3. OmniFocus does not allow application-type scripts in the toolbar. |
|  |  |
|  |  What's the "helper script"? |
|  |  |
|  |  do shell script "open -a ~/Library/Application\\ Scripts/com.omnigroup.OmniFocus2/FocusTabApp.app" |
|  |  |
|  |  |
|  |  \# LICENSE \# |
|  |  |
|  |  Copyright © 2017-2020 Dan Byler \(contact: dbyler@gmail.com\) |
|  |  Licensed under MIT License \(http://www.opensource.org/licenses/mit-license.php\) |
|  |  \(TL;DR: no warranty, do whatever you want with it.\) |
|  |  |
|  |  |
|  |  \# CHANGE HISTORY \# |
|  |  |
|  |  2020-02-14 |
|  |  - Minor cleanup |
|  |  |
|  |  2017-04-23 |
|  |  - Adding the "helper script" workaround to run from OmniFocus toolbar |
|  |  |
|  |  2017-04-17 |
|  |  - Initial release |
|  |  |
|  | \*\) |
|  |  |
|  |  |
|  | on main\(\) |
|  |  tell application "OmniFocus" |
|  |  set myFocus to {} |
|  |  -- get selection |
|  |  tell content of front document window of front document |
|  |  set validSelectedItemsList to value of \(selected trees where class of its value is not item and class of its value is not folder\) |
|  |  set totalItems to count of validSelectedItemsList |
|  |  if totalItems is 0 then |
|  |  display notification "No valid task\(s\) selected" with title "Error" |
|  |  return |
|  |  end if |
|  |  repeat with validSelectedItem in validSelectedItemsList |
|  |  validSelectedItem |
|  |  if \(containing project of validSelectedItem\) is not missing value then |
|  |  set end of myFocus to \(containing project of validSelectedItem\) |
|  |  else if \(assigned container of validSelectedItem\) is not missing value then |
|  |  set end of myFocus to \(assigned container of validSelectedItem\) |
|  |  end if |
|  |  end repeat |
|  |  end tell |
|  |  |
|  |  -- no valid projects to focus on |
|  |  if length of myFocus is 0 then |
|  |  display notification "No projects to focus" |
|  |  return |
|  |  end if |
|  |  |
|  |  -- make new tab |
|  |  tell application "System Events" |
|  |  tell process "OmniFocus" |
|  |  set frontmost to true |
|  |  click menu item "New Tab" of menu "File" of menu bar 1 |
|  |  click menu item "Projects" of menu "Perspectives" of menu bar 1 |
|  |  end tell |
|  |  end tell |
|  |  |
|  |  -- set focus |
|  |  tell front document window of front document |
|  |  set focus to myFocus |
|  |  end tell |
|  |  end tell |
|  | end main |
|  |  |
|  | main\(\) |

