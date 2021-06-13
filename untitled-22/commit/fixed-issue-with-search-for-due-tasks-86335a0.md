# Fixed issue with search for due tasks@86335a0

[Permalink](fixed-issue-with-search-for-due-tasks-86335a0.md)

[Browse files](../tree/rhydlewis-search-omnifocus.md)

 Fixed issue with search for due tasks

* Loading branch information

 Showing with **11 additions** and **13 deletions**.

1.  +1 −1 [info.plist](fixed-issue-with-search-for-due-tasks-86335a0.md#diff-ef6dac0c1c122a5c9efd56197356cab3608e10a0ff362195e31e0bda9d4a1e7e)
2.  +8 −9 [queries.py](fixed-issue-with-search-for-due-tasks-86335a0.md#diff-b492800a769560271f3b03388547d12fdc391d13dc87faf34466b65dd7fdbdbc)
3.  +1 −2 [search.py](fixed-issue-with-search-for-due-tasks-86335a0.md#diff-e8703cd6cf05cc52236932145af843693c57e83d336220550d18ae4c5e4771b6)
4.  +1 −1 [version](fixed-issue-with-search-for-due-tasks-86335a0.md#diff-5ca4f3850ccc331aaf8a257d6086e526a3b42a63e18cb11d020847985b31d188)

|  | @@ -2233,7 +2233,7 @@ Well, I want it because I can't quickly search for, say, a task within OmniFocus |  |
| :--- | :--- | :--- |
|  |  |  &lt;key&gt;variablesdontexportkey&gt; |
|  |  |  &lt;array/&gt; |
|  |  |  &lt;key&gt;versionkey&gt; |
|  |  |  &lt;string&gt;2.1.1string&gt; |
|  |  |  &lt;string&gt;2.1.2string&gt; |
|  |  |  &lt;key&gt;webaddresskey&gt; |
|  |  |  &lt;string&gt;rhydlewis.netstring&gt; |
|  |  |  dict&gt; |
|  |  |  |

|  | @@ -21,6 +21,7 @@ |  |
| :--- | :--- | :--- |
|  |  |  ALLOWS\_NEXT\_ACTION = str\("allows\_next\_action"\) |
|  |  |  CONTAINING\_PROJECT\_INFO = str\("parent"\) |
|  |  |  MODIFIED\_DATE = str\("modified"\) |
|  |  |  PROJECT\_IS\_REMAINING = str\("project\_remaining"\) |
|  |  |  |
|  |  |  |
|  |  |  NAME\_SORT = "name ASC" |
|  | @@ -40,13 +41,14 @@ |  |
|  |  |  "pi.status AS {0}".format\(STATUS\), |
|  |  |  "t.effectiveFlagged", |
|  |  |  "t.dateModified AS {0}".format\(MODIFIED\_DATE\), |
|  |  |  "t.containingProjectInfo AS {0}".format\(CONTAINING\_PROJECT\_INFO\) |
|  |  |  \]\) + ", t.dateDue AS {0}".format\(DUE\_DATE\) |
|  |  |  "t.containingProjectInfo AS {0}".format\(CONTAINING\_PROJECT\_INFO\), |
|  |  |  "t.dateDue AS {0}".format\(DUE\_DATE\) |
|  |  |  \]\) + ", t.effectiveContainingProjectInfoRemaining AS {0}".format\(PROJECT\_IS\_REMAINING\) |
|  |  |  TASK\_FROM = \("\(\(task tt left join projectinfo pi on tt.containingprojectinfo=pi.pk\) t left join " |
|  |  |  "task p on t.task=p.persistentIdentifier\) "\) |
|  |  |  TASK\_WHERE = "\(t.containingProjectInfo &lt;&gt; t.persistentIdentifier OR t.containingProjectInfo is NULL\) " |
|  |  |  TASK\_NAME\_WHERE = "t.dateCompleted IS NULL AND lower\(t.name\) LIKE lower\('%{0}%'\) AND " |
|  |  |  NOT\_COMPLETED\_CLAUSE = "t.dateCompleted IS NULL" |
|  |  |  NOT\_COMPLETED\_CLAUSE = "t.dateCompleted IS NULL AND t.effectiveContainingProjectInfoRemaining = 1" |
|  |  |  ACTIVE\_CLAUSE = "t.blocked = 0 AND " |
|  |  |  TAG\_SELECT = ", ".join\(\[ |
|  |  |  "persistentIdentifier AS {0}".format\(ID\), |
|  | @@ -137,12 +139,9 @@ def show\_recent\_tasks\(active\_only\): |  |
|  |  |  return "SELECT {0} FROM {1} ORDER BY {2} LIMIT {3}".format\(TASK\_SELECT, TASK\_FROM, "t.dateModified DESC", 10\) |
|  |  |  |
|  |  |  |
|  |  |  def show\_due\_tasks\(version\): |
|  |  |  constraint = OF2\_DUE\_SOON\_CONSTRAINT |
|  |  |  if version == DEFAULT\_OF\_VERSION: |
|  |  |  constraint = OF3\_DUE\_SOON\_CONSTRAINT |
|  |  |  |
|  |  |  return \_generate\_query\(TASK\_SELECT, TASK\_FROM, NOT\_COMPLETED\_CLAUSE + constraint, "t.dateDue ASC"\) + " LIMIT 10" |
|  |  |  def show\_due\_tasks\(\): |
|  |  |  return \_generate\_query\(TASK\_SELECT, TASK\_FROM, NOT\_COMPLETED\_CLAUSE + OF3\_DUE\_SOON\_CONSTRAINT, |
|  |  |  "t.dateDue ASC"\) + " LIMIT 10" |
|  |  |  |
|  |  |  |
|  |  |  def \_generate\_query\(select, from\_, where, order\_by\): |
|  |  |  |

|  | @@ -19,7 +19,6 @@ |  |
| :--- | :--- | :--- |
|  |  |  "com.omnigroup.OmniFocusModel/OmniFocusDatabase.db" |
|  |  |  OF3\_MAS\_DB\_LOCATION = OF3\_DB\_LOCATION.replace\('.OmniFocus3', '.OmniFocus3.MacAppStore'\) |
|  |  |  |
|  |  |  |
|  |  |  OF\_ICON\_ROOT = '/Applications/OmniFocus.app/Contents/Resources' |
|  |  |  |
|  |  |  \# Update workflow from GitHub repo |
|  | @@ -137,7 +136,7 @@ def populate\_query\(args\): |  |
|  |  |  sql = queries.show\_recent\_tasks\(active\_only\) |
|  |  |  elif args.due: |
|  |  |  log.debug\('Listing overdue or due items'\) |
|  |  |  sql = queries.show\_due\_tasks\(workflow.settings\[VERSION\_KEY\]\) |
|  |  |  sql = queries.show\_due\_tasks\(\) |
|  |  |  else: |
|  |  |  log.debug\('Searching tasks'\) |
|  |  |  sql = queries.search\_tasks\(active\_only, flagged\_only, query, everything\) |
|  |  |  |

