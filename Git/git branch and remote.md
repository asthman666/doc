# git branch and remote

## branch

* get help

        git branch -h

* show local branch

        git branch

* show remote branch, act on remote-tracking branches

        git branch -r

* list both remote-tracking and local branchs

        git branch -a

* Delete a branch. The branch must be fully merged in its upstream branch, or in HEAD if no upstream was set with --track or --set-upstream-to.

        git branch -d branch_name

* force delete

        git branch -D branch_name

* Display the full sha1s in the output listing rather than abbreviating them.

        git branch --no-abbrev -vv

* show contains commit id branch

        git branch -a --contains 368a27180016908edd44fae8b2cef01184207331

        git branch -a -vv --no-abbrev --contains 368a27180016908edd44fae8b2cef01184207331

* set up When creating a new branch, set up branch.[name].remote and branch.[name].merge configuration entries to mark the start-point branch as "upstream" from the new branch. This behavior is the default when the start point is a remote-tracking branch.

        git checkout -t -b branch_name

* Gives some information about the remote_name. origin is the default remote_name

        git remote show origin

* show remote name

        git remote

[delete git branch locally and remotely](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely)

[find out branch is tracking](https://stackoverflow.com/questions/171550/find-out-which-remote-branch-a-local-branch-is-tracking/9753364)

[origin mean](https://stackoverflow.com/questions/5270760/whats-the-meaning-of-origin-in-git-push-origin-master)

[git-remote](https://git-scm.com/docs/git-remote)

[git-branch](https://git-scm.com/docs/git-branch)