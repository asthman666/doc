# [git log](https://www.git-scm.com/docs/git-log)

`git log -p filename # -p, --patch`

`git log -1 HEAD # default HEAD`

`git log -1 origin/develop`

`git log origin/develop..HEAD # HEAD - origin/develop, specifies all the commits reachable from the current commit (i.e. HEAD), but not from origin/develop.`

`git log --simplify-merges --full-history filename`

`git log -p <sha1>`

> [gitrevisions](https://www.git-scm.com/docs/gitrevisions)

> [pull vs fetch](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch)