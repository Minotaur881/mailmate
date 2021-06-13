# Releases

Better implementation for the new feature from 2.1.0, a setting to configure whether the Insert Related Items command uses `[[wikilinks]]` or `x-devonthink-item` links.

  Assets 4

Added a link type settings—users can now specify whether they want wikilinks or `x-devonthink-item` links from the Related Items command.

  Assets 4

DEVONlink v2 introduces a new command: "Insert Related Items." This command uses DEVONthink's knowledge of your notes to find notes and files related to the current note, then inserts them into the current note as a list of wikilinks.

[![A demo of the Insert Related Items command](https://user-images.githubusercontent.com/3618647/112695652-18385080-8e4a-11eb-98ab-54ea7d125480.mov)](https://user-images.githubusercontent.com/3618647/112695652-18385080-8e4a-11eb-98ab-54ea7d125480.mov)

  Assets 4

Mar 26, 2021

```text
v2.0.0, now with an "insert related files" command
```

* Mar 26, 2021
*  [a54bdee](https://github.com/ryanjamurphy/DEVONlink-obsidian/commit/a54bdeedf6d9b1b3d2d67d3543bd0e89aa4d53b4)
*  [zip](https://github.com/ryanjamurphy/DEVONlink-obsidian/archive/refs/tags/2.0.0.zip)
*  [tar.gz](https://github.com/ryanjamurphy/DEVONlink-obsidian/archive/refs/tags/2.0.0.tar.gz)

Fixed a bug with the ribbon icon setting. Previously, the button would disappear, never to be seen again. Now that doesn't happen.

  Assets 4

DEVONlink would sometimes fail if the database with the associated files wasn't active. I think this version provides a more robust approach.

  Assets 4

The AppleScript wasn't properly iterating through the available databases. This has been fixed, making the plugin succeed even when the necessary database isn't currently active. \(It still needs to be open in DEVONthink, though.\)

  Assets 4

Adds a couple of settings for controlling the look/behaviour of the ribbon icon.

  Assets 4

Initial release.

  Assets 4

