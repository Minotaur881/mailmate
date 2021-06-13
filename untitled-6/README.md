# michaelliebling/fuzof

## fuzof

Tools to create and curate omnifocus projects by fuzzy-searching omnifocus folder tree

In order to use `ofpro` from the terminal, put the following commands into your `.bashrc`.

 \_fzf\_complete\_ofpro\(\) { \_fzf\_complete --with-nth=3.. --delimiter=':' --no-multi --reverse &lt; ~/Desktop/omnifocusprojects.txt } \_fzf\_complete\_ofpro\_post\(\) { ofpro\_pretty } ofpro\_pretty\(\) { local fullpath=$1 if \[ $\# -ne 1 \]; then read fullpath; fi typeofsection="$\(echo "$fullpath" \| sed -e "s/^\[^:\]\*\:\ //" \|\ sed -e "s/:.\*$//"\)" idofsection="$\(echo "$fullpath" \| sed -e "s/\ \[:\].\*$//"\)" nameofproject='Untitled\_Project' if \[\[ $typeofsection =~ "P" \]\]; then nameofproject="$\(echo "$fullpath" \| sed -e "s/^.\*:\ //"\)" fi theoutput="$idofsection '${nameofproject}\_new'" echo "$theoutput" } \[ -n "$BASH" \] && complete -F \_fzf\_complete\_ofpro -o default -o bashdefault ofpro "&gt;

```text
ofpro() {
	#echo  "$1"| pbcopy
	osascript /Users/liebling/Documents/research/programming/omnifocus-scripting/fuzof/NewOmnifocusProjectInContainer.scpt "$1" "$2"
}

# Custom fuzzy completion for "omnifproj" command
#   e.g. ofpro **
_fzf_complete_ofpro() {
  _fzf_complete  --with-nth=3..  --delimiter=':' --no-multi --reverse  < ~/Desktop/omnifocusprojects.txt 
}

_fzf_complete_ofpro_post() {
	ofpro_pretty
}

ofpro_pretty() {
	local fullpath=$1
	if [ $# -ne 1 ]; then
		read fullpath;
	fi
	typeofsection="$(echo "$fullpath" | sed -e "s/^[^:]*\:\ //" |\
                sed -e "s/:.*$//")"
	idofsection="$(echo "$fullpath" | sed -e "s/\ [:].*$//")"
	nameofproject='Untitled_Project'	
	if [[ $typeofsection =~ "P" ]]; then
		nameofproject="$(echo "$fullpath" | sed -e "s/^.*:\ //")"
	fi
	theoutput="$idofsection '${nameofproject}_new'"
	echo "$theoutput"
}

[ -n "$BASH" ] && complete -F _fzf_complete_ofpro -o default -o bashdefault ofpro 


```

## TODO

* /liebling/Library/Application Support/OmniFocus/omnifocusprojects.txt
* save ofpro and ofpro\_pretty \(whose name should be "extract project" to their own functions
* write a fuzzy action creator
* write a grocery copier

