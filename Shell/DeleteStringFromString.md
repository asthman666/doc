	filename="shell.string.txt"
	
	echo ${filename#*.}  # string.txt
	echo ${filename##*.} # txt
	
	echo ${filename%.*}  # shell.string
	echo ${filename%%.*} # shell
	
	filenames=("dotnet.string.txt", "java.string.txt")
	echo ${filenames[@]%%.*} # dotnet java
	echo ${filenames[*]%.*}  # dotnet.string java.string

> [Shell-Parameter-Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)

> [Pattern-Matching](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html)

> [remove-a-fixed-prefix-suffix-from-a-string-in-bash](https://stackoverflow.com/questions/16623835/remove-a-fixed-prefix-suffix-from-a-string-in-bash)

> [what-is-the-concept-of-shortest-sub-string-match-in-unix-shell](https://unix.stackexchange.com/questions/461058/what-is-the-concept-of-shortest-sub-string-match-in-unix-shell)
