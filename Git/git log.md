### 1. How to show file commit log?

    git log -p filename # -p, --patch

    git log -m --sparse --full-history -p filename

    --sparse
        All commits in the simplified history are shown.

    --full-history
        Same as the default mode, but does not prune some history.  

    -m
        This flag makes the merge commits show the full diff like regular commits; for each merge parent, a separate log entry and diff is generated. An exception is that only diff against the first parent is shown when --first-parent option is given; in that case, the output represents the changes the merge brought into the then-current branch.              

### 2. How to show last commit details? 

    git log --stat -p -1

    git log --stat -p -1 HEAD # default HEAD

### 3. How to show last commit in origin branch?

    git log -1 origin/develop

### 4. How to show specific commit, filelist and diff detail?

    git show <sha1>

    git show -m <sha1>

    git show -m --name-only <sha1>

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

`git checkout --ours -- path/to/conflicted-file.txt`

`git checkout --theirs -- path/to/conflicted-file.txt`

> [gitrevisions](https://www.git-scm.com/docs/gitrevisions)

> [pull vs fetch](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch)

> [resolving a git conflict with binary files](https://stackoverflow.com/questions/278081/resolving-a-git-conflict-with-binary-files)

> [git log](https://www.git-scm.com/docs/git-log)

> [git log tricks](https://hackernoon.com/ten-useful-git-log-tricks-7nt3yxy)