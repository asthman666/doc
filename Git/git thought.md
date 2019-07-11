# git thought

## The Three Trees

* **HEAD**

HEAD is the pointer to the current branch reference, which is in turn a pointer to the last commit made on that branch. That means HEAD will be the parent of the next commit that is created. It’s generally simplest to think of HEAD as the snapshot of your last commit on that branch.

* **Index**

The index is your proposed next commit. We’ve also been referring to this concept as Git’s “Staging Area” as this is what Git looks at when you run git commit.

* **Working Directory**

Finally, you have your working directory (also commonly referred to as the “working tree”). The other two trees store their content in an efficient but inconvenient manner, inside the .git folder. The working directory unpacks them into actual files, which makes it much easier for you to edit them. Think of the working directory as a sandbox, where you can try changes out before committing them to your staging area (index) and then to history.

[Git Reset](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified)

[origin in git push](https://stackoverflow.com/questions/5270760/whats-the-meaning-of-origin-in-git-push-origin-master)