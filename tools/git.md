# Git
* View the latest changes patch by patch **git checkout -p**
* Amend a commit with **git commit --amend**
* rename current branch **git branch -m new_name**
* rename another branch **git branch -m old_name new_name**
* Changes in last commit
  - **git show** - shows a diff for the latest commit
  - `git log --name-status HEAD^..HEAD` - commit message + name of the file(s) changed
* git push
  - **--force-with-lease** - update the branch assuming it is in the state we expect it to be, ie no one has changed it
* git diff - Shows the changes between the working directory and the index. This shows what has been changed, but is not staged for a commit.
  - **--cached** Shows the changes between the index and the HEAD(which is the last commit on this branch). This shows what has been added to the index and staged for a commit.
  - **HEAD** Shows all the changes between the working directory and HEAD (which includes changes in the index). This shows all the changes since the last commit, whether or not they have been staged for commit or not.
