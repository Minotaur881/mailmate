# ryanjamurphy/DEVONlink-obsidian

Open or reveal the current note in DEVONthink. Or, insert related files using DEVONthink's AI features.

Pair it with the companion AppleScript to integrate Obsidian and DEVONthink notes. Read more about the plugin and find the AppleScript here: [https://axle.design/devonlink-integrate-obsidian-and-devonthink](https://axle.design/devonlink-integrate-obsidian-and-devonthink)

[![This video shows the user using the plugin and AppleScript to open notes back and forth from Obsidian and DEVONthink.](https://camo.githubusercontent.com/47086d0746c4316b3b798c48e15f554d4134011c6bdc773ac3f46dfaf0a9aa7a/68747470733a2f2f692e696d6775722e636f6d2f5652757272394c2e676966)](https://camo.githubusercontent.com/47086d0746c4316b3b798c48e15f554d4134011c6bdc773ac3f46dfaf0a9aa7a/68747470733a2f2f692e696d6775722e636f6d2f5652757272394c2e676966) [![Version 2 introduces a way to insert related items from DEVONthink&apos;s AI into your notes in Obsidian.](https://user-images.githubusercontent.com/3618647/113517367-c6c04d80-953c-11eb-81ca-5f898c776ff0.gif)](https://user-images.githubusercontent.com/3618647/113517367-c6c04d80-953c-11eb-81ca-5f898c776ff0.gif)

## How to use

1. Make sure your notes are indexed in a DEVONthink database, and that the database is open in DEVONthink.
2. Click the ribbon button to invoke one of DEVONlink's commands, configurable in the plugin's settings. Or, use the commands via the Command Palette \(type cmd+p, then search for "DEVONlink"\). Or, assign hotkeys to those commands in Obsidian's hotkey preferences.

## How it works

The plugin uses the name of your active note to look for the first instance of a file with that name in any of your open databases.

If you have the same file in multiple places \(e.g., via replicants or duplicates\), or if you have multiple files with the same name as your note, you may not get desirable results.

## Installing the plugin

Look it up in Obsidian's Community Plugins gallery and select "Install."

## Manually installing the plugin

* Copy over `main.js` and `manifest.json` to your vault folder in the directory `VaultFolder/.obsidian/plugins/DEVONlink-obsidian/`.

