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

### 6. .gitconfig

    [user]
        name = noah song
        email = noah.song@aspiraconnect.com
    [merge]
        tool = vscode
    [mergetool "vscode"]
        cmd = code --wait $MERGED
    # [diff]
    #   submodule=short	
    #[difftool "vscode"]
    #	cmd = code --wait --diff $LOCAL $REMOTE
    [alias]
        parent = "!git show-branch | grep '*' | grep -v \"$(git rev-parse --abbrev-ref HEAD)\" | head -n1 | sed 's/.*\\[\\(.*\\)\\].*/\\1/' | sed 's/[\\^~].*//' #"
        author = "!sh -c 'git log -p --author \"$1\"' -"
        alias = "!git config --get-regexp alias"
        his = "!sh -c 'git log --pretty=format:\"%h - %an, %cd(%ar) : %s\" -n \"$1\"' -" # e.g.: git his 3
        last = log -1 HEAD	
        showfile = "!sh -c 'git show --pretty="" --name-status $1' -"
        pm = "!sh -c 'git log -n \"$1\" --pretty=\"%C(Yellow)%h  %C(reset)%ad %C(Cyan)%an: %C(reset)%s\"' -" # e.g.: git pm 3
    [core]
        editor = code --wait
        hooksPath = ~/.git/hooks
    [gui]
        recentrepo = F:/work/CA/Overall

### 7. Filter commits by log messages

    git log -i --grep="ISSUE-43560"

### 8. Filter commits by file content

    git log -i -S"function login()" -p


`git log origin/develop..HEAD # HEAD - origin/develop, specifies all the commits reachable from the current commit (i.e. HEAD), but not from origin/develop.`

`git log --simplify-merges --full-history filename`

`git show --pretty="" --name-only 368a27180016908edd44fae8b2cef01184207331`

`git checkout --ours -- path/to/conflicted-file.txt`

`git checkout --theirs -- path/to/conflicted-file.txt`

> [gitrevisions](https://www.git-scm.com/docs/gitrevisions)

> [pull vs fetch](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch)

> [resolving a git conflict with binary files](https://stackoverflow.com/questions/278081/resolving-a-git-conflict-with-binary-files)

> [git log](https://www.git-scm.com/docs/git-log)

> [git log tricks](https://hackernoon.com/ten-useful-git-log-tricks-7nt3yxy)