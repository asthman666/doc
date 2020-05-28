## git hook

### default hook directory 

	app/.git/hooks

### how to custom hook directory

	git config core.hooksPath /etc/hooks # git version >= 2.9.0

> [core.hooksPath](https://github.com/git/git/blob/master/Documentation/RelNotes/2.9.0.txt#L127-L128)

> [customizing git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)

### how to prevent console.log debug string commit

the code in **.git/hooks/pre-commit**

	#!/usr/bin/perl
	use strict;
	
	my $content = `git diff --cached`;
	if ( $content =~ m/\+\s*console\.log/ ) {
	    print "commit diff has 'console.log' debug string, do you want to continue commit? (y/n)\n";
	    open STDIN, '<', '/dev/tty';
	    my $answer = <STDIN>;
	    close STDIN;
	    chomp $answer; 
	    exit(0) if $answer =~ /y|Y/;
	    exit(1);
	}
	exit(0);
	
### show last commit detail when commit

the code in **.git/hooks/**

	#!/usr/bin/perl
	
	my $cmd = "git log --stat -p -1 HEAD";
	exec($cmd);


> [git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)