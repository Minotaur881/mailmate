# More elegant implementation of 2.1.0@96acf02

|  | @@ -121,42 +121,22 @@ export default class DEVONlinkPlugin extends Plugin { |  |
| :--- | :--- | :--- |
|  |  |  let vaultAdapter = this.app.vault.adapter; |
|  |  |  let maximumRelatedItemsSetting = this.settings.maximumRelatedItemsSetting; |
|  |  |  let relatedItemsPrefix = this.settings.relatedItemsPrefixSetting; |
|  |  |  let wikilinksAppleScript = \`tell application id "DNtp" |
|  |  |  if not running then |
|  |  |  run |
|  |  |  end if |
|  |  |  try |
|  |  |  set theDatabases to databases |
|  |  |  repeat with thisDatabase in theDatabases |
|  |  |  try |
|  |  |  set theNoteRecord to \(first item in \(lookup records with file "${noteFilename}" in thisDatabase\)\) |
|  |  |  set seeAlso to compare record theNoteRecord to theNoteRecord's database |
|  |  |  set listOfRecords to "" |
|  |  |  set maximumItems to ${maximumRelatedItemsSetting} |
|  |  |  set itemCount to 0 |
|  |  |  repeat with eachRecord in seeAlso |
|  |  |  if itemCount is not 0 then |
|  |  |  if itemCount is greater than maximumItems then |
|  |  |  return listOfRecords |
|  |  |  else |
|  |  |  if eachRecord's type is markdown then |
|  |  |  set listOfRecords to listOfRecords & "${relatedItemsPrefix}" & "\[\[" & name of eachRecord & "\]\]" & return |
|  |  |  else |
|  |  |  set listOfRecords to listOfRecords & "${relatedItemsPrefix}" & "\[\[" & filename of eachRecord & "\]\]" & return |
|  |  |  end if |
|  |  |  end if |
|  |  |  end if |
|  |  |  set itemCount to itemCount + 1 |
|  |  |  end repeat |
|  |  |  return listOfRecords |
|  |  |  on error |
|  |  |  return "failure" |
|  |  |  end try |
|  |  |  end repeat |
|  |  |  end try |
|  |  |  end tell\` |
|  |  |  |
|  |  |  let devonthinkLinksAppleScript = \`tell application id "DNtp" |
|  |  |  |
|  |  |  if \(vaultAdapter instanceof FileSystemAdapter\) { |
|  |  |  // let vaultPath = vaultAdapter.getBasePath\(\); // No longer needed, but leaving it in in case I ever decide to return to try to figure out how to get the path right. It would be a more robust solution than relying on filenames. |
|  |  |  // let homeFolderPath = await runAppleScriptAsync\('get POSIX path of the \(path to home folder\)'\); // see above |
|  |  |  // attempting to get path to work: await runAppleScriptAsync\('tell application id "DNtp" to open window for record \(first item in \(lookup records with path "~' + vaultPath + '/' + notePath + '"\) in database \(get database with uuid "'+ this.settings.databaseUUID + '"\)\) with force'\); // see above |
|  |  |  let currentLinkType = this.settings.linkTypeSetting; |
|  |  |  |
|  |  |  var linkLine; |
|  |  |  |
|  |  |  if \(currentLinkType == "wikilinks"\) { |
|  |  |  linkLine = \`"${relatedItemsPrefix}" & "\[\[" & name of eachRecord & "\]\]" & return\` |
|  |  |  } else if \(currentLinkType == "devonthinkURL"\) { |
|  |  |  linkLine = \`"${relatedItemsPrefix}" & "\[" & name of eachRecord & "\]\(" & reference URL of eachRecord & "\)" & return\` |
|  |  |  } |
|  |  |  let appleScript = \`tell application id "DNtp" |
|  |  |  if not running then |
|  |  |  run |
|  |  |  end if |
|  | @@ -175,9 +155,9 @@ export default class DEVONlinkPlugin extends Plugin { |  |
|  |  |  return listOfRecords |
|  |  |  else |
|  |  |  if eachRecord's type is markdown then |
|  |  |  set listOfRecords to listOfRecords & "${relatedItemsPrefix}" & "\[" & name of eachRecord & "\]\(" & reference URL of eachRecord & "\)" & return |
|  |  |  set listOfRecords to listOfRecords & ${linkLine} |
|  |  |  else |
|  |  |  set listOfRecords to listOfRecords & "${relatedItemsPrefix}" & "\[" & name of eachRecord & "\]\(" & reference URL of eachRecord & "\)" & return |
|  |  |  set listOfRecords to listOfRecords & ${linkLine} |
|  |  |  end if |
|  |  |  end if |
|  |  |  end if |
|  | @@ -190,18 +170,7 @@ export default class DEVONlinkPlugin extends Plugin { |  |
|  |  |  end repeat |
|  |  |  end try |
|  |  |  end tell\` |
|  |  |  |
|  |  |  if \(vaultAdapter instanceof FileSystemAdapter\) { |
|  |  |  // let vaultPath = vaultAdapter.getBasePath\(\); // No longer needed, but leaving it in in case I ever decide to return to try to figure out how to get the path right. It would be a more robust solution than relying on filenames. |
|  |  |  // let homeFolderPath = await runAppleScriptAsync\('get POSIX path of the \(path to home folder\)'\); // see above |
|  |  |  // attempting to get path to work: await runAppleScriptAsync\('tell application id "DNtp" to open window for record \(first item in \(lookup records with path "~' + vaultPath + '/' + notePath + '"\) in database \(get database with uuid "'+ this.settings.databaseUUID + '"\)\) with force'\); // see above |
|  |  |  let currentLinkType = this.settings.linkTypeSetting; |
|  |  |  let DEVONlinkResults = ""; |
|  |  |  if \(currentLinkType == "wikilinks"\) { |
|  |  |  DEVONlinkResults = await runAppleScriptAsync\(wikilinksAppleScript\); |
|  |  |  } else if \(currentLinkType == "devonthinkURL"\) { |
|  |  |  DEVONlinkResults = await runAppleScriptAsync\(devonthinkLinksAppleScript\); |
|  |  |  } |
|  |  |  let DEVONlinkResults = await runAppleScriptAsync\(appleScript\); |
|  |  |  if \(DEVONlinkResults == "failure"\) { |
|  |  |  new Notice\("Sorry, DEVONlink couldn't find a matching record in your DEVONthink databases. Make sure your notes are indexed, the index is up to date, and the DEVONthink database with the indexed notes is open."\); |
|  |  |  console.log\("Debugging DEVONlink. Failed filename: '" + noteFilename +"'."\); |
|  |  |  |

