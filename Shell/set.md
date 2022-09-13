`set -e` Exit immediately if a pipeline (see Pipelines), which may consist of a single simple command (see Simple Commands), a list (see Lists), or a compound command (see Compound Commands) returns a non-zero status.

`set +e` Using ‘+’ rather than ‘-’ causes these options to be turned off.

default:

	#!/usr/bin/env bash
	a = 1
	echo "Hello World"
	
	# output:
	# t.sh: line 4: a: command not found
	# Hello World
		
using `set -e`
	
	#!/usr/bin/env bash
	set -e
	a = 1
	echo "Hello World"
	
	# output:
	# t.sh: line 3: a: command not found

correct:

	#!/usr/bin/env bash
	set -e
	a=1
	echo "Hello World"
	
	# output:
	# Hello World
	
`set -u` Treat unset variables and parameters other than the special parameters ‘@’ or ‘*’ as an error when performing parameter expansion.

default:

	#!/usr/bin/env bash
	echo "$a World"
	
	# output:  
	#  World

using `set -u`:
	
	#!/usr/bin/env bash
	set -u
	echo "$a World"
	
	# output:
	# t.sh: line 3: a: unbound variable
	
correct:
	
	#!/usr/bin/env bash
	set -u
	a="Hello"
	echo "$a World"	
	
	# output:
	# Hello World
	
`set -x` Print a trace of simple commands, `for` commands, `case` commands, `select` commands, and arithmetic for commands and their arguments or associated word lists after they are expanded and before they are executed. 
		
	 #!/usr/bin/env bash
	 set -xe
	 a=0
	 sum=$((1+a))
	 domain="baidu.com"
	 ping "$domain" -c $sum
	 
	 # output:
	 
	 # + a=0
	 # + sum=1
	 # + domain=baidu.com
	 # + ping baidu.com -c 1
	 # PING baidu.com (110.242.68.66): 56 data bytes
	 # 64 bytes from 110.242.68.66: icmp_seq=0 ttl=54 time=24.235 ms
	
	 # --- baidu.com ping statistics ---
	 # 1 packets transmitted, 1 packets received, 0.0% packet loss
	 # round-trip min/avg/max/stddev = 24.235/24.235/24.235/0.000 ms

> [The-Set-Builtin](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html)