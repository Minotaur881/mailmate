# voostindie/vincents-productivity-suite-for-alfred

## Commits on Jan 8, 2021

1.  ["Improve" formatting of names pulled from the Apple Calendar.](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/5d5a0af210946c9ac1bacc1b67b33b7ff4f6ff97)

   ```text
   Improve is between quotes because although the result is better, the code is messier.
   What Apple's Calendar presents as names, at least on a Microsoft Exchange account
   (my work) is quite a mess. Anything goes, it seems.

   The goal is to fix the names as much as possible to save me from doing the work of
   manually fixing them (which I either forget or do incorrectly). It's probably
   never going to be a 100% correct...
   ```

## Commits on Dec 6, 2020

1. 2. 3. 4.  [Allow commands that act on instances to disable themselves.](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/c41e87c2a61c516b08a583a0f49e17455105ddae)

   ```text
   When calling "vps area commands  ", the list of commands now only
   shows commands that are able to act on the specified instance. By default a
   command is always enabled.

   This feature is used by the Teams and Alfred plugins, to disable themselves
   if an event doesn't contain a meeting URL, or if no folder exists for the
   project on disk, respectively.

   In the process I refactored the contexts somewhat, so that they're easier to use
   and require less code to create.
   ```

5. 
## Commits on Nov 27, 2020

1.  [Allow tags in Markdown notes to be written as YAML frontmatter.](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/bdd590a04d910173855c056d38bf5096f254d273)

   ```text
   Reason for doing this: Obsidian just introduced more support for frontmatter.

   An awesome new Obisidan feature is setting up aliases. That allows one to link
   to notes using their full name as well as any other name you use (like
   abbreviations). It works really well!

   Aliases are configured in the YAML frontmatter. As can tags. So, I decided to move
   my tags over from a line of text at the bottom (with every tag prepended with '#'),
   to a `tags` attribute in the frontmatter.
   ```

## Commits on Nov 13, 2020

1. 2. 3.  [Fix the BitBar plugin.](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/a6dd141e2cc6bc970061b62e3c228f4849c7501c)

   ```text
   - Include the Alfred plugin, otherwise loading the
     configuration crashes.
   - Disable warnings, so that BitBar doesn't barf.
   ```

4. 
## Commits on Nov 9, 2020

1. 2. 3. 4.  [Update the README.](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/6732ad6f896be5133e85d5b1a255721ec744002f)

   ```text
   Some plugins weren't documented. Also, the introduction is updated to include the
   actual output of the CLI to show what VPS is capable of.
   ```

5. 6.  [Version 4.0! Breaking changes!](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/e290143a8ffb3ad061e86b53ea248437da201f6e)

   ```text
   See the README for more information on how to migrate.

   The two biggest changes:

   1. The configuration file must now be in `~/.vps/config.yaml`
   2. The Alfred workflow is now generated when changing focus.

   Point 2 is the biggest one: I don't have to maintain the workflow
   by hand anymore and it's not as complex as it was. Generating a
   bit of duplication is not really a problem.

   The nice thing of generating the workflow:

   - No hotkeys/keywords for entities that aren't available.
   - Icons for entities match the plugins.

   AFAIK the generated workflow supports the same things as the version
   I wrote by hand before.
   ```

## Commits on Nov 4, 2020

1.  [Add a simple GeekTool plugin.](https://github.com/voostindie/vincents-productivity-suite-for-alfred/commit/eb738f2b0fd98407de4e5507b2697da174b29628)

   ```text
   I'm experimenting with GeekTool, putting the name of the active
   area on my desktop.

   The GeekTool plugin offers an action that refreshes one or more Geeklets.

   Added to that is the "area current" command, that outputs the name of
   the focused area.
   ```

