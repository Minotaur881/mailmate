# mhucka/omnifocus-hacks

[Permalink](https://github.com/mhucka/omnifocus-hacks/blob/42c539711953e6990994550ff7bdfe2364ce3f02/.gitattributes)

Cannot retrieve contributors at this time

|  | \# -\*- mode: sh; -\*- |
| :--- | :--- |
|  |  |
|  | \# Set the default behavior, in case people don't have core.autocrlf set. |
|  | \# ............................................................................. |
|  |  |
|  | \* text=auto |
|  |  |
|  | \# Specify what's text and should be normalized. |
|  | \# ............................................................................. |
|  |  |
|  | \*.py text |
|  | \*.in text |
|  | \*.rst text |
|  | \*.cfg text |
|  | \*.ini text |
|  | \*.yml text |
|  | \*.json text |
|  | \*.bat text |
|  | \*.sh text |
|  | LICENSE text |
|  | CONTRIBUTING text |
|  |  |
|  | \# Denote all files that are truly binary and should not be modified. |
|  | \# ............................................................................. |
|  |  |
|  | \*.png binary |
|  | \*.jpg binary |
|  | \*.xls binary |
|  | \*.doc binary |
|  |  |
|  | \# This next one is because in other projects, we've had problems with git |
|  | \# getting confused about line endings when people using Windows and Mac edit |
|  | \# the same files. |
|  | \# ............................................................................. |
|  |  |
|  | \*.csv binary diff=csv |
|  |  |
|  | \# Special handling for AppleScript |
|  | \# ............................................................................. |
|  | \# This makes it possible to diff and open AppleScript files in text editors. |
|  | \# It requires git-ascr-filter from https://stackoverflow.com/a/14425009/743730 |
|  | \# and also requires the user to execute the following commands: |
|  | \# |
|  | \# git config filter.ascr.clean "git-ascr-filter --clean %f" |
|  | \# git config filter.ascr.smudge "git-ascr-filter --smudge %f" |
|  |  |
|  | \*.scpt filter=ascr |

