# voostindie/vincents-productivity-suite-for-alfred

## Beware!

This project isn't called "_Vincent's_ Productivity Suite for Alfred" for nothing. It might not be of any use to anyone but myself. But there's also no reason not to make it public; it could be useful to at least one other person beside me. So why not share?

But please remember that I've had exactly one person in mind while creating this suite: me. _Your mileage may vary!_

**Update November 2020**: Hot on the heels of version 3.0, version 4.0 is out! A new major release, because the contracts with you, the user, are broken. Specifically:

* The configuration file is now expected to be in `~/.vps/config.yaml`. To migrate:
  * Create `~/.vps`
  * Move `~/.vpsrc` to `~/.vps/config.yaml`
  * Delete all files with prefix `.vps` from your home folder. \(These are typically caches.\)
* The Alfred workflow is now generated whenever you change focus. This ensures that hotkeys and keywords are only enabled when the required entity type is supported in the area. Plus, it sets the action icons to the correct applications. To migrate:
  * Delete the current VPS workflow from Alfred.
  * Change the focus at least once through the command line
  * It might be necessary to restart Alfred after this. That's just needed this one time though.
* Due to the way VPS is now set up, with a stable code directory - all changes are stored under `~/.vps` it's now theoretically possible to release an actual Gem from this code.

**Update October 2020**: Version 3.0 of VPS is out. A little over one year since version 2.0 from August 2019! The biggest change on the outside is that commands are now grouped by the type of entity instead of by the plugin that provides them. That seems like a small change, but actually it makes the naming of the commands much more reasonable. Internally a lot has changed as well. There's now a much better decoupling of plugin classes from each other. There's more reuse between plugins, and plugins require less code. But, the configuration file hasn't actually changed.

**A note on the code**: I'm not particularly proud of the code in this project. True Rubyists probably will avert their eyes in disgust. Unit tests are also seriously lacking. But hey, I've been running this tool for several years now day in day out, and it gets the job done!

## So, what's this all about?

This is a command-line interface \(CLI\) as well as an [Alfred](https://www.alfredapp.com/) workflow on top of a set of Ruby scripts that make my daily computer work a lot more efficient. So, yes it's macOS only, and specifically it works with:

* Alfred \(duh!\)
* Apple Contacts
* Apple Mail
* Apple Calendar
* Bear
* BitBar / SwiftBar
* Desktop wallpapers
* GeekTool
* iA Writer
* Markdown editors
* Marked 2
* Obsidian
* OmniFocus
* Outlook Calendar
* Teams

A lot of activity at my computer consists of managing projects and tasks in OmniFocus, editing notes in Obsidian, writing e-mails in Mail and tracking people and groups in Contacts. This CLI and the workflow on top of it give me the means to quickly edit notes and write e-mails and refer to projects and people, either through the terminal, keyboard shortcuts, keywords, or snippets.

An important aspect of this tool is that it works with _areas of responsibility_ \(a [Getting Things Done \(GTD\)](https://gettingthingsdone.com/) term\), like work, family, sports, and software projects \(like this one\). At any time, exactly one area has focus. The CLI commands and the keyboard hotkeys, keywords and snippets for Alfred are always the same, but they do different things depending on the area that has the focus.

To give you an idea of what the CLI and Alfred workflow can do, here is the output of `vps help` on my own configuration, for the area with the most extensive configuration \(work\):

```text
Usage: vps [options]   [arguments]
    -a, --[no-]alfred                Generate output in Alfred format
    -f, --focus [AREA]               Force the focus to the specified area temporarily
    -v, --version                    Show the version number and exit

To get information on all available plugins: vps help

Where  and  are one of:

  area
    commands  : List all available commands for entities of the specified type in this area
    current   : Prints the name of the area that has focus
    flush     : Flushes any caches for all plugins in this area
    focus     : Set the focus to the specified area
    list      : List all available areas
  contact
    list      : List all available contacts in this area
    mail      : Write an e-mail
    note      : Edit this contact's note
    notes     : Search notes for this contact
    open      : Open in Contacts
    paste     : Paste contact to the frontmost app
  event
    join      : Join Teams meeting
    list      : List all events for today in this area
    markdown  : Paste event as Markdown to the frontmost app
    note      : Edit this event's note
    notes     : Search notes for this event
    paste     : Paste event to the frontmost app
    paste-attendees: Paste event attendees to the frontmost app
  file
    documents : Browse documents in Alfred
    reference : Browse reference material in Alfred
  group
    list      : List all available groups in this area
    mail      : Write an e-mail
    paste     : Paste group to the frontmost app
  note
    create    : Create a new, empty note, optionally with a title
    list      : List all notes in this area
    open      : Open in Obsidian
    paste     : Paste note to the frontmost app
    root      : Return the root path on disk to the notes
    today     : Create or open today's note
    view      : Open in Marked
  project
    files     : Browse project files
    list      : List all available projects in this area
    markdown  : Paste project as Markdown to the frontmost app
    note      : Edit this project's note
    notes     : Search notes for this project
    open      : Open in OmniFocus
    paste     : Paste project to the frontmost app

  help  : show help on a specific command

Note that the types and commands available depend on the focused area.
```

The accompanying Alfred workflow looks like this \(at least, a tiny portion of it; the complete one has 19 rows...\):

What you see here is that the CLI and workflow act on _entities_, like projects, contacts, files and notes. Under the hood, VPS triggers macOS applications according to the configuration. For notes, for example, you can use either Obsidian, Bear or iA Writer. The CLI commands, hotkeys and keywords are always the same. You remember the hotkey for creating a new note once, and it will continue to work, even if you switch from one application to another!

## Installation

### Command-line

1. Clone this repository: `git clone https://github.com/voostindie/vincents-productivity-suite-for-alfred.git`
2. Go to the project root: `cd vincents-productivity-suite-for-alfred`
3. Install all required libraries: `bundle install`

**Important**: if you use macOS's system Ruby, you will need to use `sudo` for the last command!

After all this, an `exe/vps help` should work. For easier use on the command-line you might want to add the `exe` directory to your `PATH`.

### Alfred

Just change focus once, through the CLI. Every time you change the focus the Alfred workflow is rebuilt, specifically for the area you've selected. This includes registering the workflow in Alfred. \(The very first time you might have to restart Alfred.\)

### About Ruby versions

I'm taking care that this plugin works with the Ruby version that comes with the latest macOS. At the moment that's `2.6.3`. But I actually use the latest version of Ruby myself. To manage multiple Ruby versions I use [rbenv](https://github.com/rbenv/rbenv) as provided by [Homebrew](https://brew.sh/).

The Alfred workflow by default uses the same version of Ruby as the command-line does, but you can override it in the Alfred plugin. See below.

I haven't yet found a way to make the BitBar plugin use the same version. it always uses the system Ruby. But I'm making sure that also works.

## Alfred features

### Keywords and hotkeys

* `focus` / _ctrl_ + _opt_ + _cmd_ + A: sets the focus to an area of responsibility.
* `flush`: flushes all caches for the focused area of responsibility.
* `note` / _ctrl_ + _opt_ + _cmd_ + ,: creates a new note and opens it for editing in after you specify the title.
* `notes` / _ctrl_ + _opt_ + _cmd_ + N: selects a note and shows an action list
* `today` / _ctrl_ + _opt_ + _cmd_ + T: open today's note
* `contact` / _ctrl_ + _opt_ + _cmd_ + C: selects a person from Contacts and shows an action list.
* `project` / _ctrl_ + _opt_ + _cmd_ + P: selects a project from OmniFocus and shows an action list.
* `docs` / _ctrl_ + _opt_ + _cmd_ + D: browses the Documents for the selected area in Alfred's file browser.
* `refs` / _ctrl_ + _opt_ + _cmd_ + R: browses the Reference Material for the selected area in Alfred's file browser.

The list of actions available for a contact or project depends on the configuration of the focused area of responsibility. E.g. if iA Writer is enabled, the action to create a note on a contact, project or event will automatically show up.

### Snippets

Using the shared prefix `;` and no suffix for snippets:

* `;c`: copies a contact's name into the frontmost application.
* `;e`: copies an event's name into the frontmost application.
* `;p`: copies a project's name into the frontmost application.
* `;g`: copies all contacts from a contact group into the frontmost application
* `;n`: copies a note's ID into the frontmost application as a Wiki-link

## How to configure

Create a file `.vps/config.yaml` that looks something like this:

```text
areas:
   work:
        obsidian:
        omnifocus:
        contacts:
        calendar:
        alfred:
```

This sets up a single _area of responsibility_ with the Obsidian, OmniFocus, Contacts, Calendar and Alfred plugins enabled. These plugins all have default configurations, which is why you don't see anything here.

Once the configuration file exists, use `vps area focus` command in the Terminal, or the `focus` keyword \(or ⌃⌥⌘-F\) in Alfred to focus on a specific area.

## How to configure, in detail

The minimal configuration sample above means exactly the same as:

```text
areas:
    work:
        name: 'Work'
        root: '~/Work'
        obsidian:
            vault: 'Work'
            path: 'Notes'
        omnifocus:
            folder: 'Work'
        contacts:
            group: 'Work'
            prefix: 'Work -'
            cache: false
        calendar:
            name: 'Work'
        alfred:
            documents: 'Documents'
            reference material: 'Reference Material'
        bitbar:
            label: 'Work'
actions:
    alfred:
```

Again, this is the exact same configuration as the one mentioned earlier. From this full example, you probably get the gist. Below there's detailed information on every separate plugin.

To define an additional area, just add one at the same level as 'work'. Name it however you like. To disable a certain feature for an area, remove its reference completely. E.g. if you remove the `obsidian` section and don't add one for another notes app, creating notes is not possible in that area. Alternatively you can select a different plugin that supports the same entities, to have the same shortcuts magically use a different application when you switch focus!

### Areas

An area looks as follow:

Where:

* `key`: the technical key. It doesn't really matter what it is, except that the name is derived from it, and that you'll have to use it in CLI when switching focus.
* `name`: the name of the area as shown in Alfred, and as used by the other features as default values. The default value is the `key`, capitalized.
* `root`: the directory under which all files for this area reside on disk. The default is set to `~/`.
* : the name of the plugin you want to enable, followed by its configuration \(if any\). Enable as many plugins as needed!

### Obsidian \(and note applications in general!\)

Since October 2020 I'm using Obsidian for note keeping. It's my current editor of choice. It uses Markdown files on disk. I prefer that over having all my notes - thousands of them, collected over many years - hidden in some database.

The Obsidian plugin supports creating notes from scratch or from existing entities \(contacts, events, projects\) using _templates_. This templating system is explained here, but it **also applies to the other note keeping applications: iA Writer and Bear**. It works across all apps!

Overall instructions on the usage of Obsidian are:

```text
obsidian:
    vault:
    path:
    frontmatter:
    templates:
        default:
            filename: null
            title: '{{input}}'
            text: ''
            tags: []
```

With:

* `vault`: the name \(or ID\) of the Vault in Obsidian. This defaults to the area name.
* `path`: the root of the notes on disk, defaults to the root of the area followed by `Notes`. Tip: check the output of `vps note root` to test!
* `templates`: these are explained below, in a separate section.
* `frontmatter`: whether tags should be written to the note as YAML frontmatter or not, in which case they are added at the bottom of the file, prepended with a `#`. Defaults to `false`.

#### A note on IDs

This plugin works by assuming that the filename of each note, excluding its extension, is unique. That means that you can move notes around in subdirectories \(for example to an archive folder\) without breaking anything.

What's there to break? Two things:

1. Note selections. If you do a `vps note list` you'll get all note IDs.
2. Note links. Pressing `;n` allows you to put a link to a note anywhere. This link is not actually a link, but just plaintext: `[[Like This]]`.

This is, by the way, fully compatible with how Obsidian works.

#### Templates

The note templating support in VPS allows you to set up templates for different types of entities, and for all parts of a note separately. Every individual property you can configure is actually a [Liquid template](https://shopify.github.io/liquid/).

Each note has a filename, a title, a text and a set of tags. The defaults are shown in the configuration of Obsidian above.

You can:

* Change the defaults that apply to each type of note.
* Change settings for a specific type of note.

The available note types are

* `default`: for the settings that apply everywhere
* `plain`: for the basic `note create` command
* `today`: for "Today's note"
* `contact`: for notes based on a contact
* `event`: for notes based on an event
* `project`: for notes based on a project

Here's an example to give you a better idea:

```text
iawriter:
    templates:
        default:
            filename: '{{year}}-{{month}}-{{day}} {{input}}'
            title: '{{input}} {{day}}-{{month}}-{{year}}'
            tags:
                - 'todo'
        today:
            filename: '{{year}}-{{month}}-{{day}}'
            tags:
                - 'log'
                - 'todo'
        event:
            text: |
                ## Attendees
                
                {% for name in names %}- {{name}}
                {% endfor %}
```

This sets up the defaults to prepend the current date to every note filename in YYYY-MM-DD format, append it to the title in DD-MM-YYYY format and also add a "todo" tag. Since these are the defaults, this happens for every note type. But, for events, the text is set to a template that fills in the attendees of the event \(pulled from the calender\).

The default template for the filename - if you don't configure anything - is `null` \(in YAML\). In that case VPS uses the template for the title instead. This saves you the trouble of having to define the same thing twice if you want filename and title to be the same.

The variables available to each template depend on the type of note you're configuring:

**Every note type**

* `day`: the number of the day in the current month, zero-padded
* `month`: the number of the current month
* `year`: the current year
* `week`: the number of the week in the current month, zero padded
* `query`: the arguments passed to the command as a string, separated by a space
* `input`: same as query

You can see here that the arguments are passed both in `query` and in `input`. That's on purpose. `input` is meant to be overridden by different note types so that the default template \(`{{input}}`\) is always sensible. Yet the original arguments are then still available if you need them, in `query`.

**Plain**

* `input`: the input text specified by the user

**Contact**

* `input`: the name of the contact
* `name`: the name of the contact

**Event**

* `input`: the title of the event
* `title`: the title of the event
* `names`: an array of contact names

**Project**

* `input`: the name of the project
* `name`: the name of the project

For projects managed in OmniFocus \(see later\) there's a special add-on: you can override the templates for the title, the text and the tags, _per project_. You do that by adding a "Yaml Back Matter" section at the end of the note of the project, like so:

```text
---
:
    title: YOUR TITLE TEMPLATE
    text: YOUR TEXT HERE
    tags: YOUR TAGS HERE
```

Just to be sure: put this at the **bottom** of the note, not at the top!

You can have configurations for different plugins next to each other; VPS will pick the right one.

**Today**

* `input`: empty; there is no input text

Tip: Obsidian has a nice _Daily notes_ plugin that works nicely with the `vps note today` command. Note that VPS's templates are more powerful than those from Obsidian. Also, you can trigger it from any application using Alfred's global shortcut, not just from within Obsidian. By setting the filename template to `{{year}}-{{month}}-{{day}}` compatibility is guaranteed.

#### Search

The Obsidian plugin also supports searching for projects, events and contacts. Given one of these, VPS can open the search results in Obsidian for it.

This works automatically and requires no additional configuration. However for \(OmniFocus\) project you can tweak the query by configuring it in the YAML Back Matter of the project, like so:

```text
obsidian:
    query: "SEARCH STRING"
```

### iA Writer

Between April 2020 and October 2020 I've used iA Writer for all my note keeping, going back to trusty old Markdown on disk, after using Bear for a little under a year.

The configuration values for iA Writer are:

```text
iawriter:
    location:
    path:
    frontmatter:
```

With:

* `location`: the location in iA Writer for this area, defaults to the name of the area.
* `path`: the root of the notes on disk, defaults to the root of the area followed by `Notes`.
* `frontmatter`: whether tags should be written to the note as YAML frontmatter or not, in which case they are added at the bottom of the file, prepended with a `#`. Defaults to `false`. Note that this is mostly for interoperability with other apps. iA Writer itself does **not** recognize tags configured in the frontmatter!

This is the same as just:

**And of course you can add a `templates` section!** See the Obsidian plugin for information on how that works.

### Bear

I've used Bear for a little under a year, and stopped using it in August 2020. I went back to sticking my notes in Markdown files on disk. I found that to be more flexible in the end. This plugin is still supported however!!

The configuration values for Bear are:

With:

* `token`: the authentication token required by Bear to control it using URL Commands. To get your token, switch to Bear, select the Help menu and, in there, the API Token section.

**And of course you can add a `templates` section!** See the Obsidian plugin for information on how that works.

### OmniFocus

I use OmniFocus to keep track of all projects and tasks in my life. As most OmniFocus users will have done, I've created top-level folders in the project tree, one for each area of responsibility. This is why the configuration looks like this:

Where `folder` is the name of the folder to get projects from. It defaults to the name of the area.

In my work folder, where I have the biggest list of projects, I have created several subfolders. That doesn't matter for this workflow, because it gets all projects from all subfolders.

Projects are sorted in the order they appear in OmniFocus, but thanks to Alfred's smart filtering the more you use a project, the higher it will get on the list.

This plugin supports "YAML Back Matter" configuration: if an OmniFocus project _ends_ with a piece of YAML, its content is available to every command that works with projects. These commands in turn can use this to their benefit. See the Obsidian \(and iA Writer and Bear\) note plugins for example, as well as the Alfred plugin.

The YAML Back Matter applies specifically to OmniFocus, but it should be fairly easy to port to other task management applications.

### Alfred

I store files on disk for an area in two separate directories:

1. Documents: everything I create myself \(or collaborate on with others\)
2. Reference Material: all documents I get from others as reference or support material.

By enabling the Alfred plugin I can browse these directories through a global shortcut.

The configuration looks as follows:

```text
alfred:
    documents:
    reference material:
```

With:

* `documents` \(optional\): the subdirectory under the area's root directory where documents are stored. Defaults to `Documents`.
* `reference material` \(optional\): the subdirectory under the area's root directory where documents are stored. Defaults to `Reference Material`.

But wait, there's more:

#### Project Files

The Alfred plugin also adds a command to projects: you can browse the files belonging to that project.

The way the plugin resolves the directory on disk is by taking the path to the reference material \(see previous section\) and appending the name of the project to it.

In case of OmniFocus you can have a different specified in the note of the project, in the "YAML Back Matter", for example:

```text
---
alfred:
    folder: My Project
```

This will make Alfred browse the "My Project" folder in the reference material, even if the project is named differently.

### Apple Contacts

For me, the default Contacts app from Apple is good enough to manage all my contacts. For that to work across my areas of responsibility, I have set up several groups. \(You can create and edit groups only on macOS, not on iOS, but once you have them, you can see and use them on all your devices!\)

This plugin supports contacts as well as groups of contacts.

The configuration for Contacts looks as follows:

```text
contacts:
    group:
    prefix:
    cache:
```

With:

* `group`: the name of the Contacts group to show contacts from. This defaults to the name of the area.
* `prefix`: the prefix of all names of the groups in this area. This defaults to the value of the `group` setting followed by "`-`"
* `cache`: whether caching of contacts is enabled or not. To prevent surprises this defaults to `false`

Contacts are sorted by name. But thanks to Alfred, the more you use a name, the higher it will get in the result list.

When groups are large, fetching their contacts can take some time. To speed up VPS, you can enable the cache. This stores output on disk, speeding up consecutive runs. The cache is pretty dumb; it doesn't automatically refresh in any way. To flush the cache, run `vps area flush`, which deletes all existing caches for the active area. Since I don't add or delete contacts that much, this is good enough for me.

### Apple Mail

The mail plugin adds a command to Contact and Group entities, by allowing you to send e-mails to them.

The configuration looks as follows:

With:

* `from`: in case you have several accounts configured in Mail, here you can configure which one to use for the area. The format of this field is `Name`. Both the name of the address must match _exactly_ what's configured in Mail. If the account is not found, Mail will fall back to its default.

So, how do you quickly send a mail to a bunch of people? Stick them in a group, select the group in Alfred, select "Write an e-mail", and watch the magic happen ;-\)

### Apple Calendar

This plugin uses SQL to fetch data from the the Apple Calendar cache, and is definitely not perfect. It doesn't always find all events for the day, even though it does a nice of job of combining one-time events and recurring events. And it's fast.

It also fetches the attendees from the events, and makes them available to other commands.

The configuration looks as follows:

```text
calendar:
    name:
    me:
    replacements:
```

With:

* `name`: the name of the calendar to fetch events from.
* `me`: your own name, as it shows up in events. Filling this in ensures that your own name is filtered from the list of attendees for a meeting.
* `replacements`: a list of key-value pairs of people's names, see below.

#### Replacements

Although this plugin does a pretty good job of unmangling people's names from the Calendar, it doesn't always work. On top of that some people are simply published under the wrong name. With the replacements you have the option to fix that. For example:

```text
replacements:
    "Bert Simpson": "Bart Simpson"
```

This can save you a lot of repetitive manual work that's easy to forget.

### Outlook Calendar

**WARNING**: this plugin is limited, in two ways:

1. It's sloooooow. The plugin uses scripting to fetch today's calendar events from Outlook. This takes many seconds, at least in my case.
2. It doesn't find all events for the day. Recurring items that have not been adapted for today are not found.

It's boggling my mind how hard it is to fetch all events that happen on a particular day. I would expect this to be one simple API call away. \(This is just as true for Apple's Calendar, by the way.\)

Anyway, although hampered, this plugin is still useful I think, because it allows me to create notes for events fairly quickly, including a list of all attendees. That saves me a lot of typing.

The configuration looks as follows:

```text
outlookcalendar:
    account: 
    calendar:
    me:
```

Where:

* `account`: the name of the account in Outlook. This defaults to the name of the area.
* `calendar`: the name of the calendar to fetch events from. This defaults to `Calendar`.
* `me`: your e-mail address. This defaults to nothing. Filling this in ensures that your own name is filtered from the list of attendees for a meeting.

### Teams

The Teams plugin allows you to join virtual meetings from the calendar in the Microsoft Teams app. Without a plugin that acts on events enabled in the same area, like the Apple Calendar plugin, this plugin has no use.

The plugin has no configuration of its own, so all you need to do to enable it, is:

This adds a `join` command to events, in case the event note contains a link to a Teams meeting.

### Markdown

The Markdown plugin pulls data from projects and events and pastes it to the frontmost application as Markdown. That Markdown looks as follows:

```text
## 

text
</code></pre></div>
<p>Configuration:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="markdown:
    level:
    link:
"><pre><span class="pl-ent">markdown</span>:
    <span class="pl-ent">level</span>:
    <span class="pl-ent">link</span>:</pre></div>
<p>With:</p>
<ul>
<li><code>level</code> (optional): the level of the Markdown heading for the pasted text. It defaults to 2.</li>
<li><code>link</code> (optional): whether the name of the project and attendees of events should be generated as [[wikilinks]] or not. It defaults to <code>false</code>.</li>
</ul>
<p>In case of using OmniFocus for projects, the title and text for a project can be defined in the YAML Back Matter of the project, defined under the key <code>markdown</code>. If there is no YAML Back Matter, the project name is used as the title of the Markdown, and text is omitted. Note that the configuration in OmniFocus are not just strings of characters, but actual Liquid templates. You can use mostly the same variables as for other notes: day, month, year and week.</p>
<p>In case of an event, the text of the is set to the list of attendees of the event.</p>
<h3><a id="user-content-marked" class="anchor" aria-hidden="true" href="#marked"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Marked</h3>
<p>The Marked plugin adds a single command to notes: <code>view</code>, for showing the note in the Marked 2. The configuration couldn't be simpler:</p>
<p>Configuration:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="marked:
"><pre><span class="pl-ent">marked</span>:</pre></div>
<p>There's no point enabling this plugin when you keep your notes in Bear. It won't show up in that case, because there are no files on disk that Marked can open.</p>
<h3><a id="user-content-bitbar--swiftbar" class="anchor" aria-hidden="true" href="#bitbar--swiftbar"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>BitBar / SwiftBar</h3>
<p>In case you enable the BitBar or SwiftBar action that's triggered when the focus changes (see below), you can override the label that's shown in the menubar. By default it's the name of the area.</p>
<p>The configuration for BitBar looks as follows:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="bitbar:
    label:
"><pre><span class="pl-ent">bitbar</span>:
    <span class="pl-ent">label</span>:</pre></div>
<p>With:</p>
<ul>
<li><code>label</code>: the text to show in the menubar. (Tip: you can use emoji's as short titles, and you can configure the label in several ways, like setting the font, the size, the color... See the <a href="https://github.com/matryer/bitbar#plugin-api">BitBar Plugin API documentation</a>.)</li>
</ul>
<p>Note: also if you use SwiftBar, the configuration to use is <code>bitbar</code>!</p>
<h3><a id="user-content-paste" class="anchor" aria-hidden="true" href="#paste"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Paste</h3>
<p>The "Paste" plugin has no configuration and it's automatically enabled for all area's. What it does is provide a command named <code>paste</code> to various entity types, allowing you to paste it to the frontmost application. That can save you some typing in the long run. It's what makes keyboard shortcuts like <code>;c</code> in Alfred work.</p>
<p>For events it adds another command: <code>paste-attendees</code>, which pastes the names of all attendees from the selected event, straight from you calendar.</p>
<h2><a id="user-content-performing-actions-when-the-focus-changes" class="anchor" aria-hidden="true" href="#performing-actions-when-the-focus-changes"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Performing actions when the focus changes</h2>
<p>Apart from the <code>areas</code> section, the configuration also supports an <code>actions</code> section, where you can list things that must happen whenever the focus changes. Currently these are available:</p>
<ol>
<li>Rebuilding the Alfred workflow</li>
<li>Refreshing the name of the area in BitBar / SwiftBar</li>
<li>Changing the desktop wallpaper</li>
<li>Changing the focus in OmniFocus</li>
<li>Refreshing geeklets from GeekTool</li>
</ol>
<p>The <code>alfred</code> plugin is always enabled, even if it's not in your configuration. You can't disable it.</p>
<p>To enable all actions, add this to your configuration:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="actions:
    alfred:
    bitbar:
    wallpaper:
    omnifocus:
    geektool:
"><pre><span class="pl-ent">actions</span>:
    <span class="pl-ent">alfred</span>:
    <span class="pl-ent">bitbar</span>:
    <span class="pl-ent">wallpaper</span>:
    <span class="pl-ent">omnifocus</span>:
    <span class="pl-ent">geektool</span>:</pre></div>
<p>See below for details on configuration of each action.</p>
<h3><a id="user-content-updating-the-alfred-workflow" class="anchor" aria-hidden="true" href="#updating-the-alfred-workflow"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Updating the Alfred workflow</h3>
<p>As mentioned, the <code>alfred</code> action is enabled by default. The only reason to explicitly configure it is to override some of its settings:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="alfred:
    ruby: /path/to/ruby
    notifications: false
"><pre><span class="pl-ent">alfred</span>:
    <span class="pl-ent">ruby</span>: <span class="pl-s">/path/to/ruby</span>
    <span class="pl-ent">notifications</span>: <span class="pl-c1">false</span></pre></div>
<p>Where</p>
<ul>
<li><code>ruby</code>: the path to the Ruby executable to use from Alfred; see below.</li>
<li><code>notifications</code>: whether the Alfred actions from VPS should trigger macOS notifications; defaults to <code>true</code>.</li>
</ul>
<h4><a id="user-content-configuring-ruby" class="anchor" aria-hidden="true" href="#configuring-ruby"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Configuring Ruby</h4>
<p>When running VPS without a specific configuration, VPS configures the Alfred workflow with the Ruby that was used to call VPS itself. This works
most of the time, but can lead to surprises in some cases, for example when using rbenv and replacing the current Ruby.</p>
<p>When running VPS under rbenv, the Ruby version is set to something like
<code>/Users/vincent/.rbenv/versions/2.7.2/bin/ruby</code>. This works until I replace Ruby 2.7.2 with a newer version. Then all of a sudden the Alfred workflow is broken.</p>
<p>The solution:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="alfred:
    ruby: ~/.rbenv/shims/ruby
"><pre><span class="pl-ent">alfred</span>:
    <span class="pl-ent">ruby</span>: <span class="pl-s">~/.rbenv/shims/ruby</span></pre></div>
<p>This ensures that the Alfred workflow always uses the global default, whatever it is.</p>
<h3><a id="user-content-refreshing-the-name-of-the-area-in-bitbar--swiftbar" class="anchor" aria-hidden="true" href="#refreshing-the-name-of-the-area-in-bitbar--swiftbar"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Refreshing the name of the area in BitBar / SwiftBar</h3>
<p><a href="https://getbitbar.com" rel="nofollow">BitBar</a> is a nice utility that can show all kinds of texts in the menubar. I use it to show the name of the focused area, so that I always know for sure which area I'm working in. (That's getting more and more important, with any new plugin this tool gets.)</p>
<p>To enable this plugin, first:</p>
<ul>
<li>Install BitBar</li>
<li>Symlink (!) to the <code>bitbar/focused-area.1d.rb</code> script from your BitBar plugins folder. <strong>Do not copy the script, otherwise it won't work! Really do make a symlink!</strong></li>
</ul>
<p>With this done, BitBar will already show the name of the focused area. But, you'll also want it to update itself whenever you change the focus. One way is polling, but I think that's silly for this use case (which is why the script ends with "1d", meaning: "refresh only once each day"). Instead, this suite can explicitly tell BitBar to refresh the name. To do that, add BitBar to the <code>actions</code> configuration, like:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="bitbar:
    plugin:
"><pre><span class="pl-ent">bitbar</span>:
    <span class="pl-ent">plugin</span>:</pre></div>
<p>With:</p>
<ul>
<li><code>plugin</code> (optional): the exact name of the plugin. You only need to set this if you changed the name of the symlink.</li>
</ul>
<p>To override what BitBar shows in the menubar for the focused, see the BitBar configuration on area level, described above.</p>
<p><a href="https://swiftbar.app" rel="nofollow">SwiftBar</a> is a newer alternative to BitBar, that aims to be fully compatible. The BitBar plugin bundled with VPS works with SwiftBar as well.</p>
<p>In case you use SwiftBar, follow the instructions above replacing "BitBar" with "SwiftBar". Only the configuration is slightly different:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="swiftbar:
    plugin:
"><pre><span class="pl-ent">swiftbar</span>:
    <span class="pl-ent">plugin</span>:</pre></div>
<p>Here the (optional) <code>plugin</code> refers to the name of the VPS plugin <em>without any extensions</em>!.</p>
<p>What I personally like about SwiftBar is that it can hide the default built-in menu options, all 5 of them, resulting in a much cleaner application interface. The VPS plugin does exactly that when running under SwiftBar.</p>
<h3><a id="user-content-change-the-desktop-wallpaper" class="anchor" aria-hidden="true" href="#change-the-desktop-wallpaper"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Change the desktop wallpaper</h3>
<p>To be able to see which area has the focus, it's possible to have the wallpaper on the current desktop change when changing the focus.</p>
<p>To enable this action, put it in the <code>actions</code> configuration, like:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="wallpaper:
    default:
"><pre><span class="pl-ent">wallpaper</span>:
    <span class="pl-ent">default</span>:</pre></div>
<p>With:</p>
<ul>
<li><code>default</code> (optional): the path to the default picture to select when no specific picture is configured for an area. If you don't specifiy this value, you get the built-in High Sierra wallpaper.</li>
</ul>
<p>This only enables the action. To make it do anything useful, you'll also want to configure a different wallpaper per area. You do that by adding a <code>wallpaper</code> section in each area, like so:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="wallpaper:
    path:
"><pre><span class="pl-ent">wallpaper</span>:
    <span class="pl-ent">path</span>:</pre></div>
<p>With:</p>
<ul>
<li><code>path</code>: the path to the picture to use as desktop wallpaper. If not specified, the default will be used (see above).</li>
</ul>
<p>Unfortunately this plugin works only on the desktop (space) that's currently being shown. If you have multiple desktops, you'll probably end up with different wallpapers. I haven't yet found a way to fix this.</p>
<h2><a id="user-content-change-the-focus-in-omnifocus" class="anchor" aria-hidden="true" href="#change-the-focus-in-omnifocus"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Change the focus in OmniFocus</h2>
<p>To set the focus to the group configured for the active area, simply add an action for OmniFocus:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="omnifocus:
"><pre><span class="pl-ent">omnifocus</span>:</pre></div>
<p>That's it. The section has no default settings as of yet.</p>
<p>What this action does is pick the very first OmniFocus window it can find, and change its focus. For me this is just fine, since I always have exactly one OmniFocus window open anyway.</p>
<h3><a id="user-content-show-the-focused-area-in-geektool" class="anchor" aria-hidden="true" href="#show-the-focused-area-in-geektool"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>Show the focused area in GeekTool</h3>
<p>Lately I've been experimenting a bit with my desktop setup. Currently I use just one desktop and have set the menubar and Dock to hide automatically. That means I don't get to see the active area all the time with BitBar. Solution: <a href="https://www.tynsoe.org/v2/geektool/" rel="nofollow">GeekTool</a>. I've set up a couple of <em>geeklets</em> that show up at the bottom of my screen and that are hardly ever covered by windows: the currently playing track, a clock, and the name of the active area.</p>
<p>The geeklet to show the active area simply calls <code>vps area current</code>, which outputs the name of the focused area. On top of that VPS offers a plugin to tell GeekTool to refresh certain geeklets whenever the focus changes. To enable that plugin, add GeekTool to the <code>actions</code> configuration:</p>
<div class="highlight highlight-source-yaml position-relative" data-snippet-clipboard-copy-content="geektool:
    geeklets:
"><pre><span class="pl-ent">geektool</span>:
    <span class="pl-ent">geeklets</span>:</pre></div>
<p>The geeklets property expects a list of geeklet <em>names</em> to refresh. Setting a name is optional in GeekTool, but for this plugin to work you'll have to configure them. (The alternative is to use IDs. But these are long, random and can't easily be copied.)</p>
<h2><a id="user-content-about-the-icon" class="anchor" aria-hidden="true" href="#about-the-icon"><svg class="octicon octicon-link" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"/></svg></a>About the icon</h2>
<p>The icon used by VPS is made by <a href="http://www.freepik.com" rel="nofollow">Freepik</a> from <a href="https://www.flaticon.com" rel="nofollow">Flaticon</a> and is licensed by a <a href="http://creativecommons.org/licenses/by/3.0" rel="nofollow">Creative Commons BY 3.0</a>.</p>
</article>
        </div>
    </div>

  </readme-toc>


</div>

    <div data-view-component="true" class="flex-shrink-0 col-12 col-md-3">      

      <div class="BorderGrid BorderGrid--spacious" data-pjax>
        <div class="BorderGrid-row hide-sm hide-md">
          <div class="BorderGrid-cell">
            <h2 class="mb-3 h4">About</h2>

    <p class="f4 mt-3">
      A CLI and automatically generated Alfred workflows to make my daily computer work more efficient.
    </p>

  <h3 class="sr-only">Topics</h3>
  <div class="mt-3">
      <div class="f6">
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:javascript" href="/topics/javascript" title="Topic: javascript" data-view-component="true" class="topic-tag topic-tag-link">
  javascript
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:ruby" href="/topics/ruby" title="Topic: ruby" data-view-component="true" class="topic-tag topic-tag-link">
  ruby
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:macos" href="/topics/macos" title="Topic: macos" data-view-component="true" class="topic-tag topic-tag-link">
  macos
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:productivity" href="/topics/productivity" title="Topic: productivity" data-view-component="true" class="topic-tag topic-tag-link">
  productivity
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:alfred" href="/topics/alfred" title="Topic: alfred" data-view-component="true" class="topic-tag topic-tag-link">
  alfred
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:jxa" href="/topics/jxa" title="Topic: jxa" data-view-component="true" class="topic-tag topic-tag-link">
  jxa
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:alfred-workflow" href="/topics/alfred-workflow" title="Topic: alfred-workflow" data-view-component="true" class="topic-tag topic-tag-link">
  alfred-workflow
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:bitbar" href="/topics/bitbar" title="Topic: bitbar" data-view-component="true" class="topic-tag topic-tag-link">
  bitbar
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:omnifocus" href="/topics/omnifocus" title="Topic: omnifocus" data-view-component="true" class="topic-tag topic-tag-link">
  omnifocus
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:obsidian" href="/topics/obsidian" title="Topic: obsidian" data-view-component="true" class="topic-tag topic-tag-link">
  obsidian
</a>
      <a data-ga-click="Topic, repository page" data-octo-click="topic_click" data-octo-dimensions="topic:ia-writer" href="/topics/ia-writer" title="Topic: ia-writer" data-view-component="true" class="topic-tag topic-tag-link">
  ia-writer
</a>
  </div>

  </div>

  <h3 class="sr-only">Resources</h3>
  <div class="mt-3">
    <a class="Link--muted" href="#readme">
      <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-book mr-2">
    <path fill-rule="evenodd" d="M0 1.75A.75.75 0 01.75 1h4.253c1.227 0 2.317.59 3 1.501A3.744 3.744 0 0111.006 1h4.245a.75.75 0 01.75.75v10.5a.75.75 0 01-.75.75h-4.507a2.25 2.25 0 00-1.591.659l-.622.621a.75.75 0 01-1.06 0l-.622-.621A2.25 2.25 0 005.258 13H.75a.75.75 0 01-.75-.75V1.75zm8.755 3a2.25 2.25 0 012.25-2.25H14.5v9h-3.757c-.71 0-1.4.201-1.992.572l.004-7.322zm-1.504 7.324l.004-5.073-.002-2.253A2.25 2.25 0 005.003 2.5H1.5v9h3.757a3.75 3.75 0 011.994.574z"/>
</svg>
      Readme
</a>  </div>

  <h3 class="sr-only">License</h3>
  <div class="mt-3">
    <a href="/voostindie/vincents-productivity-suite-for-alfred/blob/master/LICENSE.txt" class="Link--muted">
      <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-law mr-2">
    <path fill-rule="evenodd" d="M8.75.75a.75.75 0 00-1.5 0V2h-.984c-.305 0-.604.08-.869.23l-1.288.737A.25.25 0 013.984 3H1.75a.75.75 0 000 1.5h.428L.066 9.192a.75.75 0 00.154.838l.53-.53-.53.53v.001l.002.002.002.002.006.006.016.015.045.04a3.514 3.514 0 00.686.45A4.492 4.492 0 003 11c.88 0 1.556-.22 2.023-.454a3.515 3.515 0 00.686-.45l.045-.04.016-.015.006-.006.002-.002.001-.002L5.25 9.5l.53.53a.75.75 0 00.154-.838L3.822 4.5h.162c.305 0 .604-.08.869-.23l1.289-.737a.25.25 0 01.124-.033h.984V13h-2.5a.75.75 0 000 1.5h6.5a.75.75 0 000-1.5h-2.5V3.5h.984a.25.25 0 01.124.033l1.29.736c.264.152.563.231.868.231h.162l-2.112 4.692a.75.75 0 00.154.838l.53-.53-.53.53v.001l.002.002.002.002.006.006.016.015.045.04a3.517 3.517 0 00.686.45A4.492 4.492 0 0013 11c.88 0 1.556-.22 2.023-.454a3.512 3.512 0 00.686-.45l.045-.04.01-.01.006-.005.006-.006.002-.002.001-.002-.529-.531.53.53a.75.75 0 00.154-.838L13.823 4.5h.427a.75.75 0 000-1.5h-2.234a.25.25 0 01-.124-.033l-1.29-.736A1.75 1.75 0 009.735 2H8.75V.75zM1.695 9.227c.285.135.718.273 1.305.273s1.02-.138 1.305-.273L3 6.327l-1.305 2.9zm10 0c.285.135.718.273 1.305.273s1.02-.138 1.305-.273L13 6.327l-1.305 2.9z"/>
</svg>
        MIT License
    </a>
  </div>

          </div>
        </div>
          <div class="BorderGrid-row" hidden>
            <div class="BorderGrid-cell">
              <include-fragment src="/voostindie/vincents-productivity-suite-for-alfred/used_by_list" accept="text/fragment+html">
</include-fragment>
            </div>
          </div>
          <div class="BorderGrid-row">
            <div class="BorderGrid-cell">
              <h2 class="h4 mb-3">
  <a href="/voostindie/vincents-productivity-suite-for-alfred/graphs/contributors" data-view-component="true" class="Link--primary no-underline">
    Contributors <span title="2" data-view-component="true" class="Counter">2</span>
</a></h2>


    
  <ul class="list-style-none ">
      <li class="mb-2 d-flex">
        <a class="mr-2" data-hovercard-type="user" data-hovercard-url="/users/voostindie/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="/voostindie">
          <img class="d-block avatar-user" src="https://avatars.githubusercontent.com/u/883979?s=64&v=4" width="32" height="32" alt="@voostindie">
</a>          <span class="flex-self-center flex-auto min-width-0 css-truncate css-truncate-target width-fit">
            <a class="Link--primary no-underline flex-self-center" href="/voostindie">
              <strong>voostindie</strong>
              <span class="color-text-secondary">Vincent Oostindië</span>
</a>          </span>
      </li>
      <li class="mb-2 d-flex">
        <a class="mr-2" data-hovercard-type="user" data-hovercard-url="/users/snyk-bot/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="/snyk-bot">
          <img class="d-block avatar-user" src="https://avatars.githubusercontent.com/u/19733683?s=64&v=4" width="32" height="32" alt="@snyk-bot">
</a>          <span class="flex-self-center flex-auto min-width-0 css-truncate css-truncate-target width-fit">
            <a class="Link--primary no-underline flex-self-center" href="/snyk-bot">
              <strong>snyk-bot</strong>
              <span class="color-text-secondary">Snyk bot</span>
</a>          </span>
      </li>
  </ul>



            </div>
          </div>
          <div class="BorderGrid-row">
            <div class="BorderGrid-cell">
              <h2 class="h4 mb-3">Languages</h2>
<div class="mb-2">
  <span data-view-component="true" class="Progress">
    <span itemprop="keywords" aria-label="Ruby 92.9" style="background-color: #701516;width: 92.9%;" data-view-component="true" class="Progress-item"></span>
    <span itemprop="keywords" aria-label="JavaScript 7.1" style="background-color: #f1e05a;width: 7.1%;" data-view-component="true" class="Progress-item"></span>
</span></div>
<ul class="list-style-none">
    <li class="d-inline">
      <a class="d-inline-flex flex-items-center flex-nowrap Link--secondary no-underline text-small mr-3" href="/voostindie/vincents-productivity-suite-for-alfred/search?l=ruby" data-ga-click="Repository, language stats search click, location:repo overview">
        <svg class="octicon octicon-dot-fill mr-2" style="color:#701516;" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8z"/></svg>
        <span class="color-text-primary text-bold mr-1">Ruby</span>
        <span>92.9%</span>
      </a>
    </li>
    <li class="d-inline">
      <a class="d-inline-flex flex-items-center flex-nowrap Link--secondary no-underline text-small mr-3" href="/voostindie/vincents-productivity-suite-for-alfred/search?l=javascript" data-ga-click="Repository, language stats search click, location:repo overview">
        <svg class="octicon octicon-dot-fill mr-2" style="color:#f1e05a;" viewbox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8z"/></svg>
        <span class="color-text-primary text-bold mr-1">JavaScript</span>
        <span>7.1%</span>
      </a>
    </li>
</ul>

            </div>
          </div>
      </div>
</div>
</div></div>



  </div>
</div>

    </main>
  </div>

  </div>

          
<div class="footer container-xl width-full p-responsive" role="contentinfo">
  <div class="position-relative d-flex flex-row-reverse flex-lg-row flex-wrap flex-lg-nowrap flex-justify-center flex-lg-justify-between pt-6 pb-2 mt-6 f6 color-text-secondary border-top color-border-secondary ">
    <ul class="list-style-none d-flex flex-wrap col-12 col-lg-5 flex-justify-center flex-lg-justify-between mb-2 mb-lg-0">
      <li class="mr-3 mr-lg-0">© 2021 GitHub, Inc.</li>
        <li class="mr-3 mr-lg-0"><a href="https://docs.github.com/en/github/site-policy/github-terms-of-service" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://docs.github.com/en/github/site-policy/github-privacy-statement" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li class="mr-3 mr-lg-0"><a data-ga-click="Footer, go to security, text:security" href="https://github.com/security">Security</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://www.githubstatus.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
        <li><a data-ga-click="Footer, go to help, text:Docs" href="https://docs.github.com">Docs</a></li>
    </ul>

    <a aria-label="Homepage" title="GitHub" class="footer-octicon d-none d-lg-block mx-lg-4" href="https://github.com">
      <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="24" width="24" class="octicon octicon-mark-github">
    <path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/>
</svg>
</a>
    <ul class="list-style-none d-flex flex-wrap col-12 col-lg-5 flex-justify-center flex-lg-justify-between mb-2 mb-lg-0">
        <li class="mr-3 mr-lg-0"><a href="https://support.github.com" data-ga-click="Footer, go to contact, text:contact">Contact GitHub</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://github.com/pricing" data-ga-click="Footer, go to Pricing, text:Pricing">Pricing</a></li>
      <li class="mr-3 mr-lg-0"><a href="https://docs.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li class="mr-3 mr-lg-0"><a href="https://services.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://github.blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a data-ga-click="Footer, go to about, text:about" href="https://github.com/about">About</a></li>
    </ul>
  </div>
  <div class="d-flex flex-justify-center pb-6">
    <span class="f6 color-text-tertiary"></span>
  </div>

  
</div>



  <div id="ajax-error-message" class="ajax-error-message flash flash-error" hidden>
    <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-alert">
    <path fill-rule="evenodd" d="M8.22 1.754a.25.25 0 00-.44 0L1.698 13.132a.25.25 0 00.22.368h12.164a.25.25 0 00.22-.368L8.22 1.754zm-1.763-.707c.659-1.234 2.427-1.234 3.086 0l6.082 11.378A1.75 1.75 0 0114.082 15H1.918a1.75 1.75 0 01-1.543-2.575L6.457 1.047zM9 11a1 1 0 11-2 0 1 1 0 012 0zm-.25-5.25a.75.75 0 00-1.5 0v2.5a.75.75 0 001.5 0v-2.5z"/>
</svg>
    <button type="button" class="flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
      <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-x">
    <path fill-rule="evenodd" d="M3.72 3.72a.75.75 0 011.06 0L8 6.94l3.22-3.22a.75.75 0 111.06 1.06L9.06 8l3.22 3.22a.75.75 0 11-1.06 1.06L8 9.06l-3.22 3.22a.75.75 0 01-1.06-1.06L6.94 8 3.72 4.78a.75.75 0 010-1.06z"/>
</svg>
    </button>
    You can’t perform that action at this time.
  </div>

  <div class="js-stale-session-flash flash flash-warn flash-banner" hidden>
    <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-alert">
    <path fill-rule="evenodd" d="M8.22 1.754a.25.25 0 00-.44 0L1.698 13.132a.25.25 0 00.22.368h12.164a.25.25 0 00.22-.368L8.22 1.754zm-1.763-.707c.659-1.234 2.427-1.234 3.086 0l6.082 11.378A1.75 1.75 0 0114.082 15H1.918a1.75 1.75 0 01-1.543-2.575L6.457 1.047zM9 11a1 1 0 11-2 0 1 1 0 012 0zm-.25-5.25a.75.75 0 00-1.5 0v2.5a.75.75 0 001.5 0v-2.5z"/>
</svg>
    <span class="js-stale-session-flash-signed-in" hidden>You signed in with another tab or window. <a href>Reload</a> to refresh your session.</span>
    <span class="js-stale-session-flash-signed-out" hidden>You signed out in another tab or window. <a href>Reload</a> to refresh your session.</span>
  </div>
    <template id="site-details-dialog">
  <details class="details-reset details-overlay details-overlay-dark lh-default color-text-primary hx_rsm" open>
    <summary role="button" aria-label="Close dialog"></summary>
    <details-dialog class="Box Box--overlay d-flex flex-column anim-fade-in fast hx_rsm-dialog hx_rsm-modal">
      <button class="Box-btn-octicon m-0 btn-octicon position-absolute right-0 top-0" type="button" aria-label="Close dialog" data-close-dialog>
        <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-x">
    <path fill-rule="evenodd" d="M3.72 3.72a.75.75 0 011.06 0L8 6.94l3.22-3.22a.75.75 0 111.06 1.06L9.06 8l3.22 3.22a.75.75 0 11-1.06 1.06L8 9.06l-3.22 3.22a.75.75 0 01-1.06-1.06L6.94 8 3.72 4.78a.75.75 0 010-1.06z"/>
</svg>
      </button>
      <div class="octocat-spinner my-6 js-details-dialog-spinner"></div>
    </details-dialog>
  </details>
</template>

    <div class="Popover js-hovercard-content position-absolute" style="display: none; outline: none;" tabindex="0">
  <div class="Popover-message Popover-message--bottom-left Popover-message--large Box color-shadow-large" style="width:360px;">
  </div>
</div>

    <template id="snippet-clipboard-copy-button">
  <div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w">
      <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-clippy js-clipboard-clippy-icon m-2">
    <path fill-rule="evenodd" d="M5.75 1a.75.75 0 00-.75.75v3c0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75v-3a.75.75 0 00-.75-.75h-4.5zm.75 3V2.5h3V4h-3zm-2.874-.467a.75.75 0 00-.752-1.298A1.75 1.75 0 002 3.75v9.5c0 .966.784 1.75 1.75 1.75h8.5A1.75 1.75 0 0014 13.25v-9.5a1.75 1.75 0 00-.874-1.515.75.75 0 10-.752 1.298.25.25 0 01.126.217v9.5a.25.25 0 01-.25.25h-8.5a.25.25 0 01-.25-.25v-9.5a.25.25 0 01.126-.217z"/>
</svg>
      <svg aria-hidden="true" viewbox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"/>
</svg>
    </clipboard-copy>
  </div>
</template>



  

  </body>
</html>

```

