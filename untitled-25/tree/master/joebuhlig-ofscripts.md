# joebuhlig/OFScripts

[OFScripts]()/**Alfred Project Code Management**/

### Files <a id="files"></a>

 [Permalink](https://github.com/joebuhlig/OFScripts/tree/751a02199ddf16ecc3dfd9d11209440ac5a76bda/Alfred%20Project%20Code%20Management)

 Failed to load latest commit information.

Type

Name

Latest commit message

Commit time

## Alfred Project Code Management

There are two workflows here. One is for creating the projects and one is finding the projects.

When you create a new project, it will create a project in OmniFocus, create a markdown file in the directory of your choice, and create a directory for the project. In the notes field for the OmniFocus project, you will find a link to the markdown file and the project directory. In the markdown file, there will be a link to the OmniFocus project. In the project directory there will be a symlinked file to the markdown file and an internet location file \(shortcut\) to the OmniFocus project.

Once you've downloaded and installed the workflows into Alfred, open the workflow, and do a find/replace on the AppleScript for `joebuhlig` and replace with the your username.

To run the workflow, type `p n` and then the name of the project you want to create. To search for a project, type `p f` and a search term.

To convert this to using nvAlt over nvUltra, do a find/replace on the AppleScript for `x-nvultra` and change it to `nvalt`.

