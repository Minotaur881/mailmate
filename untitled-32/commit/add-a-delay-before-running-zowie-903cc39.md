# Add a delay before running Zowie@903cc39

[Permalink](add-a-delay-before-running-zowie-903cc39.md)

[Browse files](https://github.com/mhucka/devonthink-hacks/tree/903cc390a6a04f7d323ee282adafda6137180995)

 Add a delay before running Zowie

* Loading branch information

|  | @@ -8,6 +8,11 @@ |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  on performSmartRule\(selectedRecords\) |
|  |  |  repeat with \_record in selectedRecords |
|  |  |  \# In my environment, Zotero takes some time to upload a newly- |
|  |  |  \# added PDF to the cloud. The following delay is needed to |
|  |  |  \# give time for the upload to take place, so that when Zowie |
|  |  |  \# runs, it can get the proper data from the Zotero API. |
|  |  |  delay 30 |
|  |  |  set p to the path of the \_record |
|  |  |  set result to do shell script "/usr/local/bin/zowie -q '" & p & "'" |
|  |  |  if result is not equal to "" then |
|  |  |  |

