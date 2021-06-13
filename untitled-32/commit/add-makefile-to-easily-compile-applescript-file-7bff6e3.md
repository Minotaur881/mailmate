# Add makefile to easily compile applescript file@7bff6e3

[Permalink](add-makefile-to-easily-compile-applescript-file-7bff6e3.md)

[Browse files](https://github.com/mhucka/devonthink-hacks/tree/7bff6e33d821296304f0c9a862cceabecaa0cfbf)

 Add makefile to easily compile applescript file

* Loading branch information

 Showing with **15 additions** and **0 deletions**.

1.  +15 −0 [open-url-in-devonthink/Makefile](add-makefile-to-easily-compile-applescript-file-7bff6e3.md#diff-46999db1b822a685749e3402a2a147e73f0e0b424aee555cbac9b182121a78c9)

|  |  | @@ -0,0 +1,15 @@ |
| :--- | :--- | :--- |
|  |  |  \# ============================================================================= |
|  |  |  \# @file Makefile |
|  |  |  \# @brief Trivial makefile for compiling AppleScript |
|  |  |  \# @author Michael Hucka |
|  |  |  \# @date 2020-11-13 |
|  |  |  \# @license Please see the file named LICENSE in the project directory |
|  |  |  \# @website https://github.com/mhucka/devonthink-hacks |
|  |  |  \# ============================================================================= |
|  |  |  |
|  |  |  sources = $\(shell find . -iname '\*.applescript' \| sed 's/ /\\ /g'\) |
|  |  |  |
|  |  |  compile: $\(sources:.applescript=.scpt\) |
|  |  |  |
|  |  |  %.scpt: %.applescript |
|  |  |  osacompile -o "$@" "$&lt;" |

