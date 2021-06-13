# write report file as utf8, fix typo, update scpt file@8599d82

[Permalink](write-report-file-as-utf8-fix-typo-update-scpt-file-8599d82.md)

[Browse files](https://github.com/joebuhlig/OFScripts/tree/8599d822dff330bb50ee20dc00c336c0848d70a6)

 write report file as utf8, fix typo, update scpt file

* Loading branch information

|  | @@ -3,7 +3,7 @@ on hazelProcessFile\(theFile\) |  |
| :--- | :--- | :--- |
|  |  |  set outputToFile to true -- Do you want to output to a text file? |
|  |  |  set filePath to "/Users/USERNAME/TaskReports/" -- Where to save the resulting text file \(Be sure to add the trailing "/"\) |
|  |  |  |
|  |  |  -- Evernote ouput options |
|  |  |  -- Evernote output options |
|  |  |  set outputToEvernote to false -- Do you want to output to Evernote? |
|  |  |  set evernoteNotebook to "Stream of consciousness" -- Where to file the resulting Evernote note \(Be sure the Notebook already exists\) |
|  |  |  |
|  | @@ -71,7 +71,7 @@ on hazelProcessFile\(theFile\) |  |
|  |  |  -- Create the new report file |
|  |  |  set newFile to open for access filePath & fileName & ".txt" with write permission |
|  |  |  -- Add the report text to the new file |
|  |  |  write reportText to newFile |
|  |  |  write reportText to newFile as Çclass utf8È |
|  |  |  -- Close the report file |
|  |  |  close access newFile |
|  |  |  end if |
|  |  |  |

