# ryanjamurphy/DEVONlink-obsidian

 import { addIcon, App, FileSystemAdapter, Notice, Plugin, PluginSettingTab, Setting, MarkdownView } from 'obsidian'; import {runAppleScriptAsync} from 'run-applescript'; addIcon\('DEVONthink-logo-neutral', \`  \`\); addIcon\('DEVONthink-logo-blue', \`  \`\); interface DEVONlinkSettings { ribbonButtonAction: string; DEVONlinkIconColor: string; maximumRelatedItemsSetting: number; relatedItemsPrefixSetting: string; linkTypeSetting: string; } const DEFAULT\_SETTINGS: DEVONlinkSettings = { ribbonButtonAction: 'open', DEVONlinkIconColor: 'DEVONthink-logo-blue', maximumRelatedItemsSetting: 10, relatedItemsPrefixSetting: "- ", linkTypeSetting: "wikilinks" } export default class DEVONlinkPlugin extends Plugin { settings: DEVONlinkSettings; ribbonIcon: HTMLElement; async onload\(\) { console.log\('Loading the DEVONlink plugin.'\); await this.loadSettings\(\); this.ribbonIcon = this.addRibbonIcon\(this.settings.DEVONlinkIconColor, 'DEVONlink', \(\) =&gt; { this.doRibbonAction\(\); }\); this.addCommand\({ id: 'open-indexed-note-in-DEVONthink', name: 'Open indexed note in DEVONthink', checkCallback: this.openInDEVONthink.bind\(this\) }\); this.addCommand\({ id: 'reveal-indexed-note-in-DEVONthink', name: 'Reveal indexed note in DEVONthink', checkCallback: this.revealInDEVONthink.bind\(this\) }\); this.addCommand\({ id: 'insert-related-items-from-DEVONthink-analysis', name: 'Insert related items from DEVONthink concordance', checkCallback: this.insertRelatedFromDEVONthink.bind\(this\) }\) this.addSettingTab\(new DEVONlinkSettingsTab\(this.app, this\)\); } onunload\(\) { console.log\('Unloading the DEVONlink plugin'\); } async resetRibbonIcon\(\) { //Hat-tip to @liam for this elegant way of managing the plugin's ribbon button. The idea is to give the plugin the ribbon icon as an object to hold onto. Then, since the ribbon icons are a \`HTMLElement\`, you can \`.detach\(\)\` them to remove them and re-add them, reassigning the object. this.ribbonIcon.detach\(\); this.ribbonIcon = this.addRibbonIcon\(this.settings.DEVONlinkIconColor, 'DEVONlink', \(\) =&gt; { this.doRibbonAction\(\); }\); } async loadSettings\(\) { this.settings = Object.assign\({}, DEFAULT\_SETTINGS, await this.loadData\(\)\); } async saveSettings\(\) { await this.saveData\(this.settings\); } doRibbonAction\(\) { if \(this.settings.ribbonButtonAction == "open"\) { this.openInDEVONthink\(false\); } else if \(this.settings.ribbonButtonAction == "reveal"\) { this.revealInDEVONthink\(false\); } else if \(this.settings.ribbonButtonAction == "related"\) { this.insertRelatedFromDEVONthink\(false\); } }; getVaultPath\(someVaultAdapter: FileSystemAdapter\) { return someVaultAdapter.getBasePath\(\); } async insertRelatedFromDEVONthink\(checking: boolean\) : Promise&lt;boolean&gt; { const activeView = this.app.workspace.getActiveViewOfType\(MarkdownView\); let activeFile = this.app.workspace.getActiveFile\(\); if \(!checking\) { if \(activeView\) { const editor = activeView.editor; let noteFilename = activeFile.name; let vaultAdapter = this.app.vault.adapter; let maximumRelatedItemsSetting = this.settings.maximumRelatedItemsSetting; let relatedItemsPrefix = this.settings.relatedItemsPrefixSetting; if \(vaultAdapter instanceof FileSystemAdapter\) { // let vaultPath = vaultAdapter.getBasePath\(\); // No longer needed, but leaving it in in case I ever decide to return to try to figure out how to get the path right. It would be a more robust solution than relying on filenames. // let homeFolderPath = await runAppleScriptAsync\('get POSIX path of the \(path to home folder\)'\); // see above // attempting to get path to work: await runAppleScriptAsync\('tell application id "DNtp" to open window for record \(first item in \(lookup records with path "~' + vaultPath + '/' + notePath + '"\) in database \(get database with uuid "'+ this.settings.databaseUUID + '"\)\) with force'\); // see above let currentLinkType = this.settings.linkTypeSetting; var linkLine; if \(currentLinkType == "wikilinks"\) { linkLine = \`"${relatedItemsPrefix}" & "\[\[" & name of eachRecord & "\]\]" & return\` } else if \(currentLinkType == "devonthinkURL"\) { linkLine = \`"${relatedItemsPrefix}" & "\[" & name of eachRecord & "\]\(" & reference URL of eachRecord & "\)" & return\` } let appleScript = \`tell application id "DNtp" if not running then run end if try set theDatabases to databases repeat with thisDatabase in theDatabases try set theNoteRecord to \(first item in \(lookup records with file "${noteFilename}" in thisDatabase\)\) set seeAlso to compare record theNoteRecord to theNoteRecord's database set listOfRecords to "" set maximumItems to ${maximumRelatedItemsSetting} set itemCount to 0 repeat with eachRecord in seeAlso if itemCount is not 0 then if itemCount is greater than maximumItems then return listOfRecords else if eachRecord's type is markdown then set listOfRecords to listOfRecords & ${linkLine} else set listOfRecords to listOfRecords & ${linkLine} end if end if end if set itemCount to itemCount + 1 end repeat return listOfRecords on error return "failure" end try end repeat end try end tell\` let DEVONlinkResults = await runAppleScriptAsync\(appleScript\); if \(DEVONlinkResults == "failure"\) { new Notice\("Sorry, DEVONlink couldn't find a matching record in your DEVONthink databases. Make sure your notes are indexed, the index is up to date, and the DEVONthink database with the indexed notes is open."\); console.log\("Debugging DEVONlink. Failed filename: '" + noteFilename +"'."\); } else { console.log\(DEVONlinkResults\); let cursor = editor.getCursor\(\); // let lineText = editor.getLine\(cursor.line\); editor.replaceSelection\(DEVONlinkResults\); } } return true; } else { new Notice\("No active pane. Try again with a note open in edit mode."\); } } return false; } async openInDEVONthink\(checking: boolean\) : Promise&lt;boolean&gt; { let activeFile = this.app.workspace.getActiveFile\(\); if \(!checking\) { if \(activeFile\) { let noteFilename = activeFile.name; let vaultAdapter = this.app.vault.adapter; if \(vaultAdapter instanceof FileSystemAdapter\) { // let vaultPath = vaultAdapter.getBasePath\(\); // No longer needed, but leaving it in in case I ever decide to return to try to figure out how to get the path right. It would be a more robust solution than relying on filenames. // let homeFolderPath = await runAppleScriptAsync\('get POSIX path of the \(path to home folder\)'\); // see above // attempting to get path to work: await runAppleScriptAsync\('tell application id "DNtp" to open window for record \(first item in \(lookup records with path "~' + vaultPath + '/' + notePath + '"\) in database \(get database with uuid "'+ this.settings.databaseUUID + '"\)\) with force'\); // see above let DEVONlinkResults = await runAppleScriptAsync\( \`tell application id "DNtp" activate try set theDatabases to databases repeat with thisDatabase in theDatabases try set theNoteRecord to \(first item in \(lookup records with file "${noteFilename}" in thisDatabase\)\) set newDEVONthinkWindow to open window for record theNoteRecord with force activate return "success" end try end repeat on error return "failure" end try end tell\`\); if \(DEVONlinkResults != "success"\) { new Notice\("Sorry, DEVONlink couldn't find a matching record in your DEVONthink databases. Make sure your notes are indexed, the index is up to date, and the DEVONthink database with the indexed notes is open."\); console.log\("Debugging DEVONlink. Failed filename: '" + noteFilename +"'."\); } } return true; } else { new Notice\("No active pane. Try again with a note open."\); } } return false; } async revealInDEVONthink\(checking: boolean\) : Promise&lt;boolean&gt; { let activeFile = this.app.workspace.getActiveFile\(\); if \(!checking\) { if \(activeFile\) { let noteFilename = activeFile.name; let vaultAdapter = this.app.vault.adapter; if \(vaultAdapter instanceof FileSystemAdapter\) { // let vaultPath = vaultAdapter.getBasePath\(\); // No longer needed, but leaving it in in case I ever decide to return to try to figure out how to get the path right. It would be a more robust solution than relying on filenames. // let homeFolderPath = await runAppleScriptAsync\('get POSIX path of the \(path to home folder\)'\); // see above // attempting to get path to work: await runAppleScriptAsync\('tell application id "DNtp" to open window for record \(first item in \(lookup records with path "~' + vaultPath + '/' + notePath + '"\) in database \(get database with uuid "'+ this.settings.databaseUUID + '"\)\) with force'\); // see above let DEVONlinkResults = await runAppleScriptAsync\( \`tell application id "DNtp" activate try set theDatabases to databases repeat with thisDatabase in theDatabases try set theNoteRecord to \(first item in \(lookup records with file "${noteFilename}" in thisDatabase\)\) set theParentRecord to the first parent of theNoteRecord set newDEVONthinkWindow to open window for record theParentRecord with force set newDEVONthinkWindow's selection to theNoteRecord as list activate return "success" end try end repeat on error return "failure" end try end tell\`\); if \(DEVONlinkResults != "success"\) { new Notice\("Sorry, DEVONlink couldn't find a matching record in your DEVONthink databases. Make sure your notes are indexed, the index is up to date, and the DEVONthink database with the indexed notes is open."\); console.log\("Debugging DEVONlink. Failed filename: '" + noteFilename +"'."\); } } return true; } else { new Notice\("No active pane. Try again with a note open."\); } } return false; } } class DEVONlinkSettingsTab extends PluginSettingTab { plugin: DEVONlinkPlugin; constructor\(app: App, plugin: DEVONlinkPlugin\) { super\(app, plugin\); this.plugin = plugin; } display\(\): void { let {containerEl} = this; containerEl.empty\(\); containerEl.createEl\('h2', {text: 'DEVONlink Settings'}\); new Setting\(containerEl\) .setName\('Ribbon button action'\) .setDesc\('Should the ribbon button open the note in DEVONthink, or reveal it in the DEVONthink database?'\) .addDropdown\(buttonMenu =&gt; buttonMenu .addOption\("open", "Open the note in the database"\) .addOption\("reveal", "Reveal the note in the database"\) .addOption\("related", "Insert a list of items related to the active note"\) .setValue\(this.plugin.settings.ribbonButtonAction\) .onChange\(async \(value\) =&gt; { this.plugin.settings.ribbonButtonAction = value; await this.plugin.saveSettings\(\); }\)\); new Setting\(containerEl\) .setName\('Ribbon button colour'\) .setDesc\('Should the ribbon button be DEVONthink blue or inherit the theme colour?'\) .addDropdown\(buttonMenu =&gt; buttonMenu .addOption\("DEVONthink-logo-neutral", "Inherit the theme colour"\) .addOption\("DEVONthink-logo-blue", "DEVONthink blue"\) .setValue\(this.plugin.settings.DEVONlinkIconColor\) .onChange\(async \(value\) =&gt; { this.plugin.settings.DEVONlinkIconColor = value; this.plugin.resetRibbonIcon\(\); await this.plugin.saveSettings\(\); }\)\); new Setting\(containerEl\) .setName\('Maximum items returned with the Related Items command'\) .setDesc\('Set the maximum number of related items DEVONlink will try to return when using the Related Items command.'\) .addText\(textbox =&gt; textbox .setValue\(this.plugin.settings.maximumRelatedItemsSetting.toString\(\)\) .onChange\(async \(value\) =&gt; { if \(Number\(value\)\) { this.plugin.settings.maximumRelatedItemsSetting = Number\(value\); await this.plugin.saveSettings\(\); } else { new Notice\("It looks like you haven't entered a number. Please use integers \(e.g.: 1, 2, or 3\) only. Resetting the maximum related items to the default value of 5."\); this.plugin.settings.maximumRelatedItemsSetting = 5; await this.plugin.saveSettings\(\); } }\)\); new Setting\(containerEl\) .setName\('Related items list prefix'\) .setDesc\('The Related Items command returns a list of \`\[\[\`-wrapped file names. This setting allows you to configure what the list items look like. E.g., use \`- \` for a bulleted list or \`!\` for embeds.'\) .addText\(textbox =&gt; textbox .setValue\(this.plugin.settings.relatedItemsPrefixSetting\) .onChange\(async \(value\) =&gt; { this.plugin.settings.relatedItemsPrefixSetting = value; await this.plugin.saveSettings\(\); }\)\); new Setting\(containerEl\) .setName\('Link type for related items'\) .setDesc\('Set the type of link returned by the Related Items command'\) .addDropdown\(buttonMenu =&gt; buttonMenu .addOption\("wikilinks", "\[\[Wikilinks\]\]"\) .addOption\("devonthinkURL", "DEVONthink x-devonthink-item links"\) .setValue\(this.plugin.settings.linkTypeSetting\) .onChange\(async \(value\) =&gt; { this.plugin.settings.linkTypeSetting = value; await this.plugin.saveSettings\(\); }\)\); } }
