1. How to revert some files to specific commit version?

        git show -m --name-only -1 // show HEAD commit files, it is convenient to get [files] that need to process

        git restore -s [specific commit version] [files]


2. How to restore all files in the current directory?

        git restore .