### 1. How to show file commit log?

    git log -p filename # -p, --patch

### 2. How to show last commit details? 

    git log --stat -p -1

    git log --stat -p -1 HEAD # default HEAD

### 3. How to show last commit in origin branch?

    git log -1 origin/develop

### 4. How to show specific commit, filelist and diff detail?    

    git log --stat -p <sha1>

### 5. How to show branch contains specific commit?

    git branch -a -v --no-abbrev --contains <sha1>

`git log origin/develop..HEAD # HEAD - origin/develop, specifies all the commits reachable from the current commit (i.e. HEAD), but not from origin/develop.`

`git log --simplify-merges --full-history filename`

`git show --pretty="" --name-only 368a27180016908edd44fae8b2cef01184207331`

`git checkout --ours -- path/to/conflicted-file.txt`

`git checkout --theirs -- path/to/conflicted-file.txt`

> [gitrevisions](https://www.git-scm.com/docs/gitrevisions)

> [pull vs fetch](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch)

> [resolving a git conflict with binary files](https://stackoverflow.com/questions/278081/resolving-a-git-conflict-with-binary-files)

> [git log](https://www.git-scm.com/docs/git-log)
