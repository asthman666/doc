### Using parameters in batch files: %0 and %9

%0 is the program name as it was called.

%1 is the first command line parameter

%2 is the second command line parameter

and so on till %9.

Example:

Put the following command in a batch file called mybatch.bat:

    @echo off
    @echo hello %1 %2
    pause

Invoking the batch file like this: mybatch john billy would output:

    hello john billy


### %~1 means "remove the enclosing quotes (if they exist) from the first parameter.

Put the following command in a batch file called **mybatch.bat**:

    @echo off
    @echo hello %~1
    @echo hello %1    

Invoking the batch file like below:

    mybatch "Hello World"

    # output
    Hello World
    "Hello World"


### if check    

    if %1 == "Y" (
        @echo "Get Input Y"
    )

> [using-parameters-in-batch-files-at-windows-command-line](https://stackoverflow.com/questions/14286457/using-parameters-in-batch-files-at-windows-command-line)

> [how-to-pass-arguments-to-a-batch-file](https://stackoverflow.com/questions/46771007/how-to-pass-arguments-to-a-batch-file)    