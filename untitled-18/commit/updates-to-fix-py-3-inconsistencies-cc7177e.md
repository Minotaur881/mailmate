# Updates to fix py 3 inconsistencies@cc7177e

[Permalink](updates-to-fix-py-3-inconsistencies-cc7177e.md)

[Browse files](https://github.com/rhydlewis/omnifocus-to-kanban/tree/cc7177e55a20514451d1abe6426102b63c9acf18)

 Updates to fix py 3 inconsistencies

* Loading branch information

|  | @@ -6,4 +6,6 @@ log/omnifocus-to-kanban.log |  |
| :--- | :--- | :--- |
|  |  |  \*.pyc |
|  |  |  sync.sh |
|  |  |  log/ |
|  |  |  venv/  |
|  |  |  venv/ |
|  |  |  .python-version |
|  |  |  pyvenv.cfg  |

|  |  | @@ -1,15 +1,15 @@ |
| :--- | :--- | :--- |
|  |  |  import logging |
|  |  |  import yaml |
|  |  |  import os |
|  |  |  from .bin import KanbanFlowBoard |
|  |  |  from kanban\_flow\_board import KanbanFlowBoard |
|  |  |  |
|  |  |  |
|  |  |  class KanbanFlow: |
|  |  |  kb = None |
|  |  |  log = logging.getLogger\(\_\_name\_\_\) |
|  |  |  |
|  |  |  def \_\_init\_\_\(self\): |
|  |  |  self.config = load\_config\("config/kanbanflow-config.yaml"\) |
|  |  |  self.config = load\_config\("./config/kanbanflow-config.yaml"\) |
|  |  |  |
|  |  |  token = self.config\['token'\] |
|  |  |  default\_drop\_lane = self.config\['default\_drop\_lane'\] |
|  |  |  |

|  | @@ -17,7 +17,8 @@ class KanbanFlowBoard: |  |
| :--- | :--- | :--- |
|  |  |  api\_requests = 0 |
|  |  |  |
|  |  |  def \_\_init\_\_\(self, token, default\_drop\_column, types, completed\_columns\): |
|  |  |  self.auth = {'Authorization': "Basic " + base64.b64encode\("apiToken:{0}".format\(token\)\)} |
|  |  |  auth = base64.b64encode\("apiToken:{0}".format\(token\).encode\(\)\).decode\("utf-8"\) |
|  |  |  self.auth = {'Authorization': "Basic {0}".format\(auth\)} |
|  |  |  self.board\_details = self.request\("https://kanbanflow.com/api/v1/board"\).json\(\) |
|  |  |  self.default\_drop\_column = default\_drop\_column |
|  |  |  self.types = types |
|  | @@ -51,7 +52,7 @@ def get\_comment\_containing\_id\(self, \_id\): |  |
|  |  |  comments = self.request\(TASKS\_URI + "{0}/comments".format\(\_id\)\) |
|  |  |  comment\_json = comments.json\(\) |
|  |  |  if comment\_json: |
|  |  |  comment = \(item for item in comment\_json if COMMENT\_PREFIX in item\["text"\]\).next\(\) |
|  |  |  comment = next\(\(item for item in comment\_json if COMMENT\_PREFIX in item\["text"\]\)\) |
|  |  |  if comment: |
|  |  |  return comment |
|  |  |  return None |
|  | @@ -165,7 +166,7 @@ def update\_task\(self, identifier, name, note, subtasks=None\): |  |
|  |  |  |
|  |  |  def get\_column\_name\(self, \_id\): |
|  |  |  columns = self.board\_details\["columns"\] |
|  |  |  column = \(item for item in columns if item\["uniqueId"\] == \_id\).next\(\) |
|  |  |  column = next\(item for item in columns if item\["uniqueId"\] == \_id\) |
|  |  |  return column |
|  |  |  |
|  |  |  def clear\_board\(self\): |
|  |  |  |

|  |  | @@ -1,4 +1,4 @@ |
| :--- | :--- | :--- |
|  |  |  \#!/usr/bin/env python2 |
|  |  |  \#!/usr/bin/env python |
|  |  |  |
|  |  |  """Omnifocus to Kanban |
|  |  |  |
|  | @@ -14,8 +14,8 @@ import logging |  |
|  |  |  import logging.config |
|  |  |  from timeit import default\_timer as timer |
|  |  |  from docopt import docopt |
|  |  |  import omnifocus |
|  |  |  import kanbanFlow |
|  |  |  from kanban\_board import KanbanFlow |
|  |  |  from omnifocus import Omnifocus |
|  |  |  |
|  |  |  |
|  |  |  def main\(\): |
|  | @@ -52,7 +52,7 @@ def main\(\): |  |
|  |  |  |
|  |  |  |
|  |  |  if \_\_name\_\_ == '\_\_main\_\_': |
|  |  |  logging.config.fileConfig\('config/log.conf'\) |
|  |  |  logging.config.fileConfig\('./config/log.conf'\) |
|  |  |  logging.debug\("sys.path: %s", sys.path\) |
|  |  |  logging.debug\("sys.executable: %s", sys.executable\) |
|  |  |  logging.debug\("os.getcwd\(\): %s", os.getcwd\(\)\) |
|  |  |  |

