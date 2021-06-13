# Added support for Trello, config for logging now from a file@490a8d4

|  |  | @@ -1,43 +1,136 @@ |
| :--- | :--- | :--- |
|  |  |  from leankit import LeankitKanban |
|  |  |  from trello import TrelloClient, Label |
|  |  |  import logging |
|  |  |  import yaml |
|  |  |  import os |
|  |  |  import re |
|  |  |  |
|  |  |  |
|  |  |  class LeanKit: |
|  |  |  kb = None |
|  |  |  log = logging.getLogger\(\_\_name\_\_\) |
|  |  |  |
|  |  |  def \_\_init\_\_\(self\): |
|  |  |  self.config = self.load\_config\(\) |
|  |  |  self.config = load\_config\("leankit-config.yaml"\) |
|  |  |  board\_id = self.config\['board\_id'\] |
|  |  |  self.kb = LeankitKanban\(self.config\['account'\], self.config\['email'\], self.config\['password'\]\) |
|  |  |  self.log.debug\("Connecting to Leankit board {0}".format\(board\_id\)\) |
|  |  |  self.board = self.kb.getBoard\(board\_id=board\_id\) |
|  |  |  |
|  |  |  def find\_completed\_card\_ids\(self\): |
|  |  |  lanes = self.config\['completed\_lanes'\] |
|  |  |  self.log.info\("Looking for cards in completed lanes: {0}".format\(lanes\)\) |
|  |  |  self.log.info\("Looking for completed cards in lanes: {0}".format\(lanes\)\) |
|  |  |  cards = \[\] |
|  |  |  |
|  |  |  \[cards.extend\(\[card.external\_card\_id for card in self.board.getLane\(lane\).cards |
|  |  |  if len\(card.external\_card\_id\) &gt; 1\]\) for lane in lanes\] |
|  |  |  self.log.debug\("Found {0} external ids".format\(len\(cards\)\)\) |
|  |  |  self.log.info\("Found {0} completed cards on the board".format\(len\(cards\)\)\) |
|  |  |  self.log.debug\("External ids: {0}".format\(cards\)\) |
|  |  |  return cards |
|  |  |  |
|  |  |  def card\_exists\(self, identifier\): |
|  |  |  return identifier in self.board.external\_ids |
|  |  |  \# return identifier in \[card.external\_card\_id for card in self.board.cards\_with\_external\_ids\(\)\] |
|  |  |  |
|  |  |  def add\_cards\(self, cards\): |
|  |  |  self.board.add\_cards\(cards\) |
|  |  |  return True |
|  |  |  |
|  |  |  def load\_config\(self\): |
|  |  |  path = "{0}/leankit-config.yaml".format\(os.getcwd\(\)\) |
|  |  |  self.log.debug\("Loading config file {0}".format\(path\)\) |
|  |  |  f = open\(path\) |
|  |  |  config = yaml.safe\_load\(f\) |
|  |  |  f.close\(\) |
|  |  |  return config |
|  |  |  |
|  |  |  class Trello: |
|  |  |  COMMENT\_PREFIX = "external\_id=" |
|  |  |  log = logging.getLogger\(\_\_name\_\_\) |
|  |  |  |
|  |  |  def \_\_init\_\_\(self\): |
|  |  |  self.config = load\_config\("trello-config.yaml"\) |
|  |  |  |
|  |  |  app\_key = self.config\['app\_key'\] |
|  |  |  token = self.config\['token'\] |
|  |  |  board\_id = self.config\['board\_id'\] |
|  |  |  |
|  |  |  self.board = TrelloClient\(api\_key=app\_key, token=token\).get\_board\(board\_id\) |
|  |  |  self.classify\_board\(\) |
|  |  |  self.log.debug\("Connecting to Trello board {0}".format\(board\_id\)\) |
|  |  |  |
|  |  |  def classify\_board\(self\): |
|  |  |  cards = self.board.all\_cards\(\) |
|  |  |  self.log.debug\("Classifying Trello board, contains {0} cards".format\(len\(cards\)\)\) |
|  |  |  self.cards\_with\_external\_ids = \[\] |
|  |  |  self.labels = {} |
|  |  |  |
|  |  |  for label in self.board.get\_labels\(\): |
|  |  |  self.labels\[label.name\] = label |
|  |  |  |
|  |  |  for card in cards: |
|  |  |  if card.closed: |
|  |  |  self.log.info\("Ignoring closed card {0} \({1}\)".format\(card.name, card.id\)\) |
|  |  |  else: |
|  |  |  self.log.debug\("Looking for external id in {0}".format\(card.name\)\) |
|  |  |  self.cards\_with\_external\_ids.append\(Trello.get\_external\_id\(card\)\) |
|  |  |  \# comments = \[comment for comment in card.comments if card.comments.include\('omnifocus'\)\] |
|  |  |  |
|  |  |  @staticmethod |
|  |  |  def get\_external\_id\(card\): |
|  |  |  external\_id = None |
|  |  |  card.fetch\(\) |
|  |  |  comments = card.comments |
|  |  |  if comments: |
|  |  |  for comment in comments: |
|  |  |  text = comment\['data'\]\['text'\] |
|  |  |  if Trello.COMMENT\_PREFIX in text: |
|  |  |  external\_id = re.sub\(Trello.COMMENT\_PREFIX, '', text\) |
|  |  |  return external\_id |
|  |  |  |
|  |  |  def clear\_board\(self\): |
|  |  |  for card in self.board.all\_cards\(\): |
|  |  |  self.log.info\("Deleting {0} {1}".format\(card.name, card.id\)\) |
|  |  |  card.delete\(\) |
|  |  |  |
|  |  |  def card\_exists\(self, identifier\): |
|  |  |  return identifier in self.cards\_with\_external\_ids |
|  |  |  |
|  |  |  def add\_cards\(self, cards\): |
|  |  |  default\_list = self.board.get\_list\(self.config\['default\_list'\]\) |
|  |  |  self.log.info\("Adding {0} cards to lane {1} \({2}\)".format\(len\(cards\), default\_list.name, default\_list.id\)\) |
|  |  |  for card in cards: |
|  |  |  name = card\['name'\] |
|  |  |  identifier = card\['identifier'\] |
|  |  |  card\_type = card\['type'\] |
|  |  |  |
|  |  |  card = default\_list.add\_card\(name\) |
|  |  |  card.comment\("{0}{1}".format\(Trello.COMMENT\_PREFIX, identifier\)\) |
|  |  |  |
|  |  |  try: |
|  |  |  card.add\_label\(self.labels\[card\_type\]\) |
|  |  |  self.log.info\("Creating card with details: name={0} id={1} type={2}".format\(name, identifier, |
|  |  |  card\_type\)\) |
|  |  |  except KeyError: |
|  |  |  self.log.info\("Can't find card type {0} configured in Trello".format\(card\_type\)\) |
|  |  |  self.log.info\("Creating card with details: name={0} id={1} type=default".format\(name, identifier\)\) |
|  |  |  |
|  |  |  def find\_completed\_card\_ids\(self\): |
|  |  |  completed\_lists = self.config\['completed\_lists'\] |
|  |  |  self.log.info\("Looking for cards in completed lanes: {0}".format\(completed\_lists\)\) |
|  |  |  cards = \[\] |
|  |  |  |
|  |  |  for list\_id in completed\_lists: |
|  |  |  completed\_list = self.board.get\_list\(list\_id\) |
|  |  |  cards.extend\(\[Trello.get\_external\_id\(card\) for card in completed\_list.list\_cards\(\)\]\) |
|  |  |  |
|  |  |  \# \[cards.extend\(\[card.external\_card\_id for card in self.trello.lane.get\(lane\).cards |
|  |  |  \# if len\(card.external\_card\_id\) &gt; 1\]\) for lane in lanes\] |
|  |  |  self.log.info\("Found {0} completed cards on the board".format\(len\(cards\)\)\) |
|  |  |  self.log.debug\("External ids: {0}".format\(cards\)\) |
|  |  |  return cards |
|  |  |  |
|  |  |  |
|  |  |  def load\_config\(path\): |
|  |  |  path = "{0}/{1}".format\(os.getcwd\(\), path\) |
|  |  |  logging.debug\("Loading config file {0}".format\(path\)\) |
|  |  |  f = open\(path\) |
|  |  |  config = yaml.safe\_load\(f\) |
|  |  |  f.close\(\) |
|  |  |  return config |
|  |  |  |
|  |  |  if \_\_name\_\_ == '\_\_main\_\_': |
|  |  |  board = Trello\(\) |
|  |  |  board.clear\_board\(\) |

