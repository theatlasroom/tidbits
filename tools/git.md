# Git
* View the latest changes patch by patch `git checkout -p`
* Amend a commit with `git commit --amend`
* rename current branch `git branch -m new_name`
* rename another branch `git branch -m old_name new_name`
* Changes in last commit
  - `git show` - shows a diff for the latest commit
  - `git log --name-status HEAD^..HEAD` - commit message + name of the file(s) changed
* git push
  - `--force-with-lease` - update the branch assuming it is in the state we expect it to be, ie no one has changed it
