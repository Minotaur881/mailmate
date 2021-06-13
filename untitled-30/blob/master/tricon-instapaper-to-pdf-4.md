# tricon/instapaper-to-pdf

[Permalink](https://github.com/tricon/instapaper-to-pdf/blob/57e4484ddc00e782033c25fbdbe321d3d9ccc8c9/import_to_devonthink.rb)

Cannot retrieve contributors at this time

|  | \# Copyright \(c\) 2011 David Aaron Fendley |
| :--- | :--- |
|  | \# |
|  | \# Import-to-DEVONthink is freely distributable under the terms of MIT license. |
|  | \# See LICENSE file or http://www.opensource.org/licenses/mit-license.php |
|  | \#------------------------------------------------------------------------------ |
|  |  |
|  | \# Import to DEVONthnk |
|  | def import\_to\_devonthink\(filename, database, folder\) |
|  |  puts "Importing to DEVONthink..." |
|  |  %x\[ osascript &lt;&lt;-HDOC |
|  |  tell application id "com.devon-technologies.thinkpro2" to launch |
|  |  tell application id "com.devon-technologies.thinkpro2" |
|  |  set lstFound to databases where name = "\#{database}" |
|  |  if length of lstFound &gt; 0 then |
|  |  set oDb to item 1 of lstFound |
|  |  set theFolder to create location "\#{folder}" in oDb |
|  |  set oWin to open window for record theFolder |
|  |  set theRecord to import \#{filename} to theFolder |
|  |  close oWin |
|  |  end if |
|  |  end tell |
|  |  \] |
|  | end |

