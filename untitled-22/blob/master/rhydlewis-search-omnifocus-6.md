# rhydlewis/search-omnifocus

[Permalink](https://github.com/rhydlewis/search-omnifocus/blob/86335a0ae86bb69672036d28c640c7f8b0a3d63d/omnifocus.py)

Cannot retrieve contributors at this time

|  | import subprocess |
| :--- | :--- |
|  |  |
|  | INBOX = 'Inbox' |
|  | PROJECTS = 'Projects' |
|  | CONTEXTS = 'Contexts' |
|  | TAGS = 'Tags' |
|  | FORECAST = 'Forecast' |
|  | FLAGGED = 'Flagged' |
|  | REVIEW = 'Review' |
|  |  |
|  | DEFAULT\_OF\_VERSION = '3' |
|  |  |
|  | DEFAULT\_OF2\_PERSPECTIVES = \[INBOX, PROJECTS, CONTEXTS, FORECAST, FLAGGED, REVIEW\] |
|  | DEFAULT\_OF3\_PERSPECTIVES = \[INBOX, PROJECTS, TAGS, FORECAST, FLAGGED, REVIEW\] |
|  |  |
|  | PERSPECTIVE\_SEARCH\_SCRIPT = ''' |
|  |  tell application "OmniFocus" |
|  |  try |
|  |  return every perspective's name |
|  |  end try |
|  |  end tell |
|  |  ''' |
|  | LOCATION\_SCRIPT = 'tell application "Finder" to get \(POSIX path of \(path to application "OmniFocus"\)\)' |
|  |  |
|  |  |
|  | def list\_perspectives\(\): |
|  |  results = run\_script\(PERSPECTIVE\_SEARCH\_SCRIPT\) |
|  |  results = \[result.rstrip\("\n"\).decode\('utf-8', 'ignore'\) for result in results if result != "missing value"\] |
|  |  |
|  |  return DEFAULT\_OF3\_PERSPECTIVES + results |
|  |  |
|  |  |
|  | def search\_perspectives\(query\): |
|  |  return \[perspective for perspective in list\_perspectives\(\) if query.lower\(\) in perspective.lower\(\)\] |
|  |  |
|  |  |
|  | \# see suggestion from deanishe at: |
|  | \# http://www.alfredforum.com/topic/5934-search-omnifocus-free-text-search-your-omnifocus-data |
|  | def find\_install\_location\(\): |
|  |  results = run\_script\(LOCATION\_SCRIPT\) |
|  |  return results\[0\].rstrip\("\n"\) |
|  |  |
|  |  |
|  | def run\_script\(query\): |
|  |  \# thanks Dr Drang: http://www.leancrew.com/all-this/2013/03/combining-python-and-applescript/ |
|  |  osa = subprocess.Popen\(\['osascript', '-'\], stdin=subprocess.PIPE, stdout=subprocess.PIPE\) |
|  |  return osa.communicate\(query\)\[0\].split\(', '\) |
|  |  |

