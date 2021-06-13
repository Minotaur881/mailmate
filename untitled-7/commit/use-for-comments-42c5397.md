# Use '\#' for comments@42c5397

[Permalink](use-for-comments-42c5397.md)

[Browse files](../tree/mhucka-omnifocus-hacks.md)

 Use '\#' for comments

* Loading branch information

 Showing with **21 additions** and **20 deletions**.

1.  +21 −20 [of-toggle-tag.scpt](use-for-comments-42c5397.md#diff-86a4881297cb38c1810d005d4b8ece3f156cd5c816c7d7adc709fc3c05d0a66f)

|  |  | @@ -1,31 +1,31 @@ |
| :--- | :--- | :--- |
|  |  |  -- ============================================================================ |
|  |  |  -- @file of-toggle-tag |
|  |  |  -- @brief Add or remove one or more tags from tasks |
|  |  |  -- @author Michael Hucka |
|  |  |  -- @license Please see the file LICENSE in the parent directory |
|  |  |  -- @repo https://github.com/mhucka/omnifocus-hacks |
|  |  |  -- ============================================================================ |
|  |  |  \# ============================================================================= |
|  |  |  \# @file of-toggle-tag |
|  |  |  \# @brief Add or remove one or more tags from OmniFocus tasks |
|  |  |  \# @author Michael Hucka |
|  |  |  \# @license Please see the file LICENSE in the parent directory |
|  |  |  \# @repo https://github.com/mhucka/omnifocus-hacks |
|  |  |  \# ============================================================================= |
|  |  |  |
|  |  |  -- Global variables and constants. |
|  |  |  -- ............................................................................ |
|  |  |  \# Global variables and constants. |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  global tagsList |
|  |  |  set tagsList to {"today", "soon"} |
|  |  |  |
|  |  |  -- Utility functions. |
|  |  |  -- ............................................................................ |
|  |  |  \# Utility functions. |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  on askUserForTags\(\) |
|  |  |  tell application "System Events" |
|  |  |  activate |
|  |  |  set selectedTags to {choose from list tagsList with title "Toggle Tags 🏷" with prompt "Tags to toggle:" with multiple selections allowed} |
|  |  |  end tell |
|  |  |  -- We get back a list of lists. I don't know why. Return the inner one. |
|  |  |  \# We get back a list of lists. I don't know why. Return the inner one. |
|  |  |  return item 1 of selectedTags |
|  |  |  end askUserForTags |
|  |  |  |
|  |  |  -- The following is based on code posted by user "RosemaryOrchard" here: |
|  |  |  -- https://talk.automators.fm/t/running-into-problems-adding-a-tag-in-omnifocus-3-with-an-applescript/2227/2 |
|  |  |  \# The following is based on code posted by user "RosemaryOrchard" here: |
|  |  |  \# https://talk.automators.fm/t/running-into-problems-adding-a-tag-in-omnifocus-3-with-an-applescript/2227/2 |
|  |  |  |
|  |  |  on tagObjectFromOF\(theTagName\) |
|  |  |  tell application "OmniFocus" |
|  | @@ -36,12 +36,12 @@ on tagObjectFromOF\(theTagName\) |  |
|  |  |  end tagObjectFromOF |
|  |  |  |
|  |  |  |
|  |  |  -- The following is based in part on code posted by user "hammer" in Oct. 2018 |
|  |  |  -- https://discourse.omnigroup.com/t/omnifocus-3-script-to-remove-today-tag-and-mark-complete/42541/2 |
|  |  |  \# The following is based in part on code posted by user "hammer" in Oct. 2018 |
|  |  |  \# https://discourse.omnigroup.com/t/omnifocus-3-script-to-remove-today-tag-and-mark-complete/42541/2 |
|  |  |  |
|  |  |  on toggleTag\(theTask, theTagName\) |
|  |  |  tell application "OmniFocus" |
|  |  |  -- First look for the tag in the task's tags & remove it if it's there. |
|  |  |  \# First look for the tag in the task's tags & remove it if it's there. |
|  |  |  set currTags to name of tags of theTask |
|  |  |  repeat with x from 1 to count of currTags |
|  |  |  set currTagName to item x of currTags |
|  | @@ -52,15 +52,15 @@ on toggleTag\(theTask, theTagName\) |  |
|  |  |  end if |
|  |  |  end repeat |
|  |  |  |
|  |  |  -- If we get here, we didn't find the tag. Add it. |
|  |  |  \# If we get here, we didn't find the tag. Add it. |
|  |  |  set theTag to my tagObjectFromOF\(theTagName\) |
|  |  |  add theTag to tags of theTask |
|  |  |  end tell |
|  |  |  end toggleTag |
|  |  |  |
|  |  |  |
|  |  |  -- Main body. |
|  |  |  -- ............................................................................ |
|  |  |  \# Main body. |
|  |  |  \# ............................................................................. |
|  |  |  |
|  |  |  set listOfTagsToToggle to my askUserForTags\(\) |
|  |  |  |
|  | @@ -82,3 +82,4 @@ tell application "OmniFocus" |  |
|  |  |  end repeat |
|  |  |  end tell |
|  |  |  end tell |
|  |  |  |

