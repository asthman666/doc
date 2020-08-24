# git thought

## The Three Trees

* **HEAD**

HEAD is the pointer to the current branch reference, which is in turn a pointer to the last commit made on that branch. That means HEAD will be the parent of the next commit that is created. It’s generally simplest to think of HEAD as the snapshot of your last commit on that branch.

* **Index**

The index is your proposed next commit. We’ve also been referring to this concept as Git’s “Staging Area” as this is what Git looks at when you run git commit.

* **Working Directory**

Finally, you have your working directory (also commonly referred to as the “working tree”). The other two trees store their content in an efficient but inconvenient manner, inside the .git folder. The working directory unpacks them into actual files, which makes it much easier for you to edit them. Think of the working directory as a sandbox, where you can try changes out before committing them to your staging area (index) and then to history.

`git reset [model] [commit]`

* --soft 
    
    Does not touch the index file or the working tree at all (but resets the head to [commit], just like all modes do). This leaves all your changed files "Changes to be committed", as git status would put it.

* --mixed

    Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the **default action**.

* --hard

    Resets the index and working tree. Any changes to tracked files in the working tree since [commit] are discarded.

### Recap

The reset command overwrites these three trees in a specific order, stopping when you tell it to:

* Move the branch HEAD points to (stop here if --soft).

* Make the index look like HEAD (stop here unless --hard).

* Make the working directory look like the index.

[Git Reset](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified)

[origin in git push](https://stackoverflow.com/questions/5270760/whats-the-meaning-of-origin-in-git-push-origin-master)