	#!/bin/bash          
	STR=""
	echo ${STR-a}   # output: empty string
	echo ${STR:-a}  # output: a
	
	echo ${SSS-a}   # output: a
	echo ${SSS:-a}  # output: a