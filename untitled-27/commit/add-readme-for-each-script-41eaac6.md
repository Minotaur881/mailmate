# Add README for each script@41eaac6

[Permalink](add-readme-for-each-script-41eaac6.md)

[Browse files](https://github.com/brandonpittman/OmniFocus/tree/41eaac6b860ddb41751ba6a004b74b1191f611d8)

 Add README for each script

* Loading branch information

 Showing with **0 additions** and **70 deletions**.

1.  +0 −21 [Colonize/README.md](add-readme-for-each-script-41eaac6.md#diff-f6282592d5ac8be4a2e118f6ca6d29d18733b63afcb7b630234849b5b7e91542)
2.  +0 −19 [Considered/README.md](add-readme-for-each-script-41eaac6.md#diff-8493d76a552793137d1d636505ea568123ad080583b3792bc08e42e24f2a103c)
3.  +0 −30 [Fixxxer/README.md](add-readme-for-each-script-41eaac6.md#diff-df271919a77b28a8dcedf51cc4c58c32612886420a561a376938e57bbc75ee34)

|  |  | @@ -1,24 +1,3 @@ |
| :--- | :--- | :--- |
|  |  |  I just whipped up a neat little script that uses the latest version of my OmniFocus Library. It's called \[Colonize\]\(https://github.com/brandonpittman/OmniFocus\). You can use it to select some tasks in OmniFocus, and then if you run \`Colonize.scpt\`, it'll switch the first word of the task name into a prefix or into a bare word if the first word is already a prefix. This makes handling tasks like \`Review daily logs\` and \`Review: daily logs\` easy. |
|  |  |  |
|  |  |  Here's the code: |
|  |  |  |
|  |  |  \`\`\`applescript |
|  |  |  use AppleScript version "2.4" -- Yosemite \(10.10\) or later |
|  |  |  use scripting additions |
|  |  |  use O : script "omnifocus" |
|  |  |  use OmniFocus : application "OmniFocus" |
|  |  |  |
|  |  |  on run |
|  |  |  tell O to toggleColon\(selectedItems\(\)\) |
|  |  |  end run |
|  |  |  |
|  |  |  on handle\_string\(argv\) |
|  |  |  if argv is "set" then |
|  |  |  O's setColon\(selectedItems\(\) of O\) |
|  |  |  else if argv is "clear" then |
|  |  |  O's clearColon\(selectedItems\(\) of O\) |
|  |  |  end if |
|  |  |  end handle\_string |
|  |  |  \`\`\` |
|  |  |  |
|  |  |  You will, of course, need my library installed first. This script is set up to work with LaunchBar already. If you pass "set" or "clear" to the script \(or on the command line\), instead of toggling, it'll blank set or clear colons. |

|  |  | @@ -1,22 +1,3 @@ |
| :--- | :--- | :--- |
|  |  |  I wrote another cool little tool using my AppleScript library. It's called \[Considered\]\(https://github.com/brandonpittman/OmniFocus\). It also handles things having to do with colons and prefixes, but specifically the \*\*Consider:\*\* prefix. If you're unfamiliar with considered tasks, read all about them \[here\]\(http://www.usingomnifocus.com/2014/01/the-considered-task/\). Instead of trying to set task names to something like "Consider reviewing" with the \*\*ing\*\*, I opted for Kourosh Dini's prefix-style considered tasks where you just add \*\*Consider:\*\* as a prefix. It's simpler and easier to script. Here's the code \(using my OmniFocus library, of course.\) |
|  |  |  |
|  |  |  \`\`\`applescript |
|  |  |  use AppleScript version "2.4" -- Yosemite \(10.10\) or later |
|  |  |  use scripting additions |
|  |  |  use O : script "omnifocus" |
|  |  |  use OmniFocus : application "OmniFocus" |
|  |  |  |
|  |  |  on run |
|  |  |  tell O to toggleConsider\(selectedItems\(\)\) |
|  |  |  end run |
|  |  |  |
|  |  |  on handle\_string\(argv\) |
|  |  |  if argv is "set" then |
|  |  |  tell O to setConsider\(selectedItems\(\)\) |
|  |  |  else if argv is "clear" then |
|  |  |  tell O to clearConsider\(selectedItems\(\)\) |
|  |  |  end if |
|  |  |  end handle\_string |
|  |  |  \`\`\` |
|  |  |  |
|  |  |  It's a pretty nifty script that will toggle consider prefixes on and off. It's set up to accept an argument with LaunchBar \(either "set" or "clear"\) to flip the considered switch one way or the other no matter what the current state. |

|  |  | @@ -1,31 +1 @@ |
| :--- | :--- | :--- |
|  |  |  Another nifty script for OmniFocus. It's called \[Fixxxer\]\(https://github.com/brandonpittman/OmniFocus\). It does two things. If you run it with no arguments, it will remove \*\*colonized\*\* prefixes from task names. If you pass it an argument, it will \*\*add\*\* that argument as a prefix to selected tasks. It's LaunchBar-ready. If you want to turn off the confirmation dialog, set \`nagMePlease\` to \`false\`. |
|  |  |  |
|  |  |  \`\`\`applescript |
|  |  |  use AppleScript version "2.4" -- Yosemite \(10.10\) or later |
|  |  |  use scripting additions |
|  |  |  use O : script "omnifocus" |
|  |  |  use OmniFocus : application "OmniFocus" |
|  |  |  -- If you want to play it safe, set nagMePlease to true |
|  |  |  property nagMePlease : true |
|  |  |  |
|  |  |  on run |
|  |  |  if nagMePlease then |
|  |  |  set question to display dialog "Do you want to remove all prefixes?" |
|  |  |  if button returned of question is "OK" then |
|  |  |  removePrefixes\(\) |
|  |  |  end if |
|  |  |  else |
|  |  |  removePrefixes\(\) |
|  |  |  end if |
|  |  |  end run |
|  |  |  |
|  |  |  on handle\_string\(argv\) |
|  |  |  tell O to setPrefix\(selectedItems\(\), argv\) |
|  |  |  end handle\_string |
|  |  |  |
|  |  |  on removePrefixes\(\) |
|  |  |  tell O to clearPrefixAll\(selectedItems\(\)\) |
|  |  |  display notification ¬ |
|  |  |  "All prefixes removed." with title "Fixxxer" |
|  |  |  end removePrefixes |
|  |  |  \`\`\` |

