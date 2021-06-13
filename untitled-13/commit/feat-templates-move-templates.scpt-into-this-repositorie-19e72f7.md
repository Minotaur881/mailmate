# feat\(templates\): Move Templates.scpt into this repositorie@19e72f7

[Permalink](feat-templates-move-templates.scpt-into-this-repositorie-19e72f7.md)

[Browse files](https://github.com/FradSer/automation-omnifocus-3/tree/19e72f7deeb586b60e9aafd637939dabc052bcae)

 feat\(templates\): Move Templates.scpt into this repositorie

* Loading branch information

|  |  | @@ -0,0 +1 @@ |
| :--- | :--- | :--- |
|  |  |  \*.applescript diff=scpt |

|  |  | @@ -0,0 +1,8 @@ |
| :--- | :--- | :--- |
|  |  |  \# Mac OS X |
|  |  |  \*.DS\_Store |
|  |  |  |
|  |  |  \# Backup files |
|  |  |  \*~.nib |
|  |  |  \\#\*\# |
|  |  |  .\#\* |
|  |  |  |

|  |  | @@ -0,0 +1,21 @@ |
| :--- | :--- | :--- |
|  |  |  MIT License |
|  |  |  |
|  |  |  Copyright \(c\) 2013–2017 Chris Sauvé |
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

 Large diffs are not rendered by default.

|  |  | @@ -0,0 +1,37 @@ |
| :--- | :--- | :--- |
|  |  |  \# 0.5.0 |
|  |  |  - Removed the ability to convert from Curt Clifton's script syntax. At this point, both are equally well known and there are no benefits to be had from offering an easy transition between the two. |
|  |  |  \# 0.5.0 |
|  |  |  - Default folder names can now have any level of depth. That is, you can do something like "&gt;&gt;&gt; Work &gt; Clients &gt; John &gt; Smith" and it should select the Smith folder inside the John folder inside the Clients folder inside the Work folder. |
|  |  |  - Killed Growl support. More trouble than it was worth, unfortunately. Notifications use Notification Center instead of Growl now. |
|  |  |  - Removed the pointless dialog confirming that you want to just duplicate a project with no variables. If it's in a template folder, it's a template project, so it will automatically do the duplication. |
|  |  |  - Template folder must, by default, contain the word "Template" |
|  |  |  - Removed the ability to copy a project multiple times with "@copy" |
|  |  |  - You can now compare two variables for the comparison operators |
|  |  |  - You can use \`delete: ask\`, just as with \`complete: ask\`, to have the script ask you if the task should be deleted. |
|  |  |  - Contexts can now have as many variables as you want \(i.e., "$var1 meeting with var2"\). |
|  |  |  - Date parsing now uses Omni's built in parser |
|  |  |  - No need to encase string comparisons in conditions in quotes \(i.e., write @if $condition == Hello then complete instead of @if $condition == "Hello" then complete\) |
|  |  |  |
|  |  |  \#\# 0.5.1 |
|  |  |  - Fixed a bug where times added with a colon would not add correctly. |
|  |  |  |
|  |  |  \#\# 0.5.2 |
|  |  |  - Fixed a bug with using contexts without any variables |
|  |  |  |
|  |  |  \#\# 0.5.3 |
|  |  |  - Fixed bugs related to colons ruining datetime strings used for variable replacement and templates in dropped folders being included in the available template list. |
|  |  |  |
|  |  |  \#\# 0.5.4 |
|  |  |  - Fixed an issue where date variables using hyphens wouldn't be correctly interpretted in setting due/ start dates. |
|  |  |  |
|  |  |  \#\# 0.5.5 |
|  |  |  - The script not works nicely when you start and due default times are simply set at 12AM as mine are. Can't believe how long this bug was lying around in there! |
|  |  |  |
|  |  |  \#\# 0.5.6 |
|  |  |  - Fixed an issue with calculating the due date when adding/ subtracting dates. |
|  |  |  |
|  |  |  \#\# 0.5.7 \(September 25, 2014\) |
|  |  |  - Added recursive folder check to collect all template projects in a template folder regardless of nesting depth. |
|  |  |  |
|  |  |  \# Coming |
|  |  |  - You can use "-W" or "-w" after any relative date \(either hard-coded or entered via an "ask" statement\) to count only weekdays. You can use "-S" or "-s" to skip special dates set with the \`property\` "specialSkipDays" |

|  |  | @@ -0,0 +1,9 @@ |
| :--- | :--- | :--- |
|  |  |  rm -f ../Templates.scpt |
|  |  |  osacompile -o Templates.scpt Templates.applescript |
|  |  |  sips -s format icns Icon.png --out Icon.icns |
|  |  |  echo "read 'icns' \(-16455\) \"Icon.icns\";" &gt;&gt; Icon.rsrc |
|  |  |  Rez -a Icon.rsrc -o Templates.scpt |
|  |  |  SetFile -a C Templates.scpt |
|  |  |  rm Icon.rsrc |
|  |  |  rm Icon.icns |
|  |  |  mv Templates.scpt ../ |

