# seishonagon/pm\_hook\_workflows

[Permalink](https://github.com/seishonagon/pm_hook_workflows/blob/b864e69e8e46556e254800d0500932966a557f70/README.md)

Cannot retrieve contributors at this time

## pm\_hook\_workflows

3 Alfred workflows for poor man's project management in Hook

### Introduction

These workflows leverage the power of .hook files to point them to individual "projects" \(which can really be any directories on your hard drive\) on your machine.

_pc_ will create a "project" on your hard drive \(there are some options for where to create it, and you can even create it as an Alfred Folder Action\), populate it with a set of template files, and create a .hook file to index this project.

_pr_ will list all current .hook files \(and hence, projects\). Usual Alfred shortcuts are available: arrow navigation, autocompletion/filtering ... until you choose a file- you can then either: open the project in the finder or open the .hook file

_pa_ will archive the "project" by moving files to a specific archive folder and deleting the .hook file

### Installation

* download the workflows and install them in Alfred
* make sure you have the \(Hook CLI\)\[[https://brettterpstra.com/projects/hook-cli/](https://brettterpstra.com/projects/hook-cli/)\] designed by Brett Terpstra - although it's not mandatory and because of AppleScript limits, it's still kind of slow, but it will get better!
* dig in the workflows to ensure the hard coded directories correspond to what you want

If there is interest, I'll try and make the directory setup more user friendly. For now it's very much presented "as is"
