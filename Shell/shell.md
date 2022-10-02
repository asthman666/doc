### What is sh?

`sh` (or the Shell Command Language) is a programming language described by the POSIX standard. It has many implementations (ksh88, Dash, ...). `Bash` can also be considered an implementation of sh.

Because sh is a specification, not an implementation, `/bin/sh` is a symlink (or a hard link) to an actual implementation on most POSIX systems.

Any unix/linux OS will have an `sh` shell. On Ubuntu `sh` often invokes `dash` and on MacOS it's a special POSIX version of `bash`.	

How can you find out what /bin/sh points to on Ubuntu?

	$ file -h /bin/sh
	/bin/sh: symbolic link to dash	

Calls to the POSIX sh `/bin/sh` in macOS are handled by `/bin/bash` in sh compatibility mode. You can verify this by asking sh for its version:

	% sh --version
	GNU bash, version 3.2.57(1)-release (x86_64-apple-darwin21)
	Copyright (C) 2007 Free Software Foundation, Inc.

In MacOS, the symbolic link at /var/select/sh determines which shell stands in as `sh`. By default the link points to `/bin/bash`:

	% readlink /var/select/sh
	/bin/bash 

### What is Bash?

Bash started as an sh-compatible implementation (although it predates the POSIX standard by a few years), but as time passed it has acquired many extensions. 


### Shell Prompt and Shell Types

The prompt, `$`, which is called the command prompt, is issued by the shell. While the prompt is displayed, you can type a command.

Shell reads your input after you press Enter. It determines the command you want executed by looking at the first word of your input. A word is an unbroken set of characters. Spaces and tabs separate words.

    Bourne shell − If you are using a Bourne-type shell, the $ character is the default prompt.
    C shell − If you are using a C-type shell, the % character is the default prompt.

The Bourne Shell has the following subcategories −

    Bourne shell (sh)
    Korn shell (ksh)
    Bourne Again shell (bash)
    POSIX shell (sh)

The different C-type shells follow −

    C shell (csh)
    TENEX/TOPS C shell (tcsh)

Bourne shell was the first shell to appear on Unix systems, thus it is referred to as "the shell".

### Example Script

Assume we create a test.sh script. Note all the scripts would have the .sh extension. Before you add anything else to your script, you need to alert the system that a shell script is being started. This is done using the shebang construct. For example −

`#!/bin/sh`

This tells the system that the commands that follow are to be executed by the Bourne shell. It's called a shebang because the # symbol is called a hash, and the ! symbol is called a bang.

### Shell Comments

You can put your comments in your script as follows −

	#!/bin/bash
	
	# Author : Zara Ali
	# Copyright (c) Tutorialspoint.com
	# Script follows here:
	date

Save the above content and make the script executable −

	$chmod +x test.sh

The shell script is now ready to be executed −

	$./test.sh
	
> [unix-what-is-shell](https://www.tutorialspoint.com/unix/unix-what-is-shell.htm)
> 
> [sh-macos](https://scriptingosx.com/2020/06/about-bash-zsh-sh-and-dash-in-macos-catalina-and-beyond/)
> 
> [difference-between-sh-and-bash](https://stackoverflow.com/questions/5725296/difference-between-sh-and-bash)

