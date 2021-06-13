# Edited README file@ffaa1f4

[Permalink](edited-readme-file-ffaa1f4.md)

 Showing with **49 additions** and **0 deletions**.

1.  +49 −0 [README.md](edited-readme-file-ffaa1f4.md#diff-b335630551682c19a781afebcf4d07bf978fb1f8ac04c6bf87428ed5106870f5)

|  |  | @@ -1,2 +1,51 @@ |
| :--- | :--- | :--- |
|  |  |  \# fuzof |
|  |  |  Tools to create and curate omnifocus projects by fuzzy-searching omnifocus folder tree |
|  |  |  |
|  |  |  In order to use \`ofpro\` from the terminal, put the following commands into your \`.bashrc\`. |
|  |  |  |
|  |  |  \`\`\`bash |
|  |  |  ofpro\(\) { |
|  |  |  \#echo "$1"\| pbcopy |
|  |  |  osascript /Users/liebling/Documents/research/programming/omnifocus-scripting/fuzof/NewOmnifocusProjectInContainer.scpt "$1" "$2" |
|  |  |  } |
|  |  |  |
|  |  |  \# Custom fuzzy completion for "omnifproj" command |
|  |  |  \# e.g. ofpro \*\* |
|  |  |  \_fzf\_complete\_ofpro\(\) { |
|  |  |  \_fzf\_complete --with-nth=3.. --delimiter=':' --no-multi --reverse &lt; ~/Desktop/omnifocusprojects.txt |
|  |  |  } |
|  |  |  |
|  |  |  \_fzf\_complete\_ofpro\_post\(\) { |
|  |  |  ofpro\_pretty |
|  |  |  } |
|  |  |  |
|  |  |  ofpro\_pretty\(\) { |
|  |  |  local fullpath=$1 |
|  |  |  if \[ $\# -ne 1 \]; then |
|  |  |  read fullpath; |
|  |  |  fi |
|  |  |  typeofsection="$\(echo "$fullpath" \| sed -e "s/^\[^:\]\*\:\ //" \|\ |
|  |  |  sed -e "s/:.\*$//"\)" |
|  |  |  idofsection="$\(echo "$fullpath" \| sed -e "s/\ \[:\].\*$//"\)" |
|  |  |  nameofproject='Untitled\_Project' |
|  |  |  if \[\[ $typeofsection =~ "P" \]\]; then |
|  |  |  nameofproject="$\(echo "$fullpath" \| sed -e "s/^.\*:\ //"\)" |
|  |  |  fi |
|  |  |  theoutput="$idofsection '${nameofproject}\_new'" |
|  |  |  echo "$theoutput" |
|  |  |  } |
|  |  |  |
|  |  |  \[ -n "$BASH" \] && complete -F \_fzf\_complete\_ofpro -o default -o bashdefault ofpro |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  \`\`\` |
|  |  |  |
|  |  |  |
|  |  |  \# TODO |
|  |  |  |
|  |  |  \* /liebling/Library/Application Support/OmniFocus/omnifocusprojects.txt |
|  |  |  \* save ofpro and ofpro\_pretty \(whose name should be "extract project" to their own functions |
|  |  |  |
|  |  |  \* write a fuzzy action creator |
|  |  |  \* write a grocery copier |

