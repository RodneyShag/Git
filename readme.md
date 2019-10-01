<p align="center">
    <a href="http://files.zeroturnaround.com/pdf/zt_git_cheat_sheet.pdf">
    <img src="images/git_logo.png">
    </a>
    <br>[Git Cheatsheet](http://files.zeroturnaround.com/pdf/zt_git_cheat_sheet.pdf)
</p>



## Commands

All commands should be run without the <> brackets

- `git log` - shows the commit ids, and the latest commit is at the top
- `git log -p` - lists the changed files
- `git checkout -b develop` checks out a new branch called "develop"
- `git add *` - adds all files
- `git add <file>` - adds a specific file (Must then do a commit, then push)
- `git commit -m "Put Message Here"` - commits locally
- `git commit --amend`" - updates commit by amending your new changes to it. Must run after "add" command
- `git commit --amend -m "an updated commit message`" - updates the commit, and its commit message.
- `git push` - pushes to what branch we're on
- `git push origin <my_branch>` - pushes to specific branch (I think origin is a keyword.
 [Reference](https://www.digitalocean.com/community/tutorials/how-to-use-git-branches)
- `git diff <commit_number>` - compares current code to any commit
- `git branch` - says which branch we're on
- `git checkout init_devices` - switches branch to *init_devices*
- `git checkout <commit_number>` - goes to a specific commit
- `git status` - shows differences between local files and remote files
- `git rm <file>` - removes file from server (Must then do a commit, then push)
- `git pull` - pulls all changed files
- `git ls-files | xargs wc -l` - counts # of lines of code in a github repo. [Link to Repo](https://gist.github.com/mandiwise/dc53cb9da00856d7cdbb)
- `git config --global --edit` - Edit git commit signature
- `git branch -d the_local_branch` - Removes local branch. [Link](https://makandracards.com/makandra/621-git-delete-a-branch-local-or-remote)
- `git rebase -i HEAD~3` - combines the last 3 commits into 1 commit. Called [Squashing Commits](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html)
- `git reset filename.txt` - undoes adding a file.

## More functionality

__Creating a Repository__
1. `git init <project name>`
1. Add the repository to Github Desktop and push it

__Submitting changes__
1. `git status` - to see what's modified
1. `git add <files>`,
1. `git commit -m "<commit message>"`
1. `git push` to push the code to the repository

__Submitting changes when more code needs to be pulled__
1. `git status` - to see what's modified
1. `git add <files>`,
1. `git commit -m "<commit message>"`
1. `git push` to push the code to the repository (if it fails, continue to next step)
1. `git pull` - this will do a `git fetch` and a `git merge`. (assuming no merge conflicts, go onto next steps)
1. `git push`

Doing `git pull --rebase` doesn't create a merge commit, so it makes other people's code diverge from what they had.

__Stashing__

- `git stash` - undo saved changes - [More commands](https://www.atlassian.com/git/tutorials/saving-changes/git-stash), and [even More commands](https://medium.freecodecamp.org/useful-tricks-you-might-not-know-about-git-stash-e8a9490f0a1a)
- `git stash save "Custom Message"` - stashes changes, with custom message.
- `git stash apply` - redo saved changes
- `git stash pop` - redo saved changes and remove from stash
- `git stash show stash@{1} -p` - shows diff. Remove the `-p` to get abbreviated diff.
- `git stash list` - shows all stashes

__Stash topmost commit__ (from Sunaya)
- `git reset HEAD^` - "basically like an uncommit"
- `git stash`

__Merge 1 branch into another__
- Go to the "giving branch", and do a `git pull`. Then go to receiving branch, and run 1 of the following merge commands
  - `git merge <branch_name>` - Run this from receiving branch. More info [here](https://www.atlassian.com/git/tutorials/using-branches/git-merge)
  - `git merge <commit_number_from_another_branch>` - Merges another branch (up to the commit number) into this branch.

__Head isn't on main branch. Put changes on top of head before doing CR__

- Somewhat useful [tutorial for git pull](https://www.atlassian.com/git/tutorials/syncing#git-remote)
- Steps
    1. Do a `git log` to get the commit number corresponding to the changes you made. Save it for step 5.
    1. Somehow get the branch we need. I think it's `git pull origin <branch>` (use the actual branch, like _dpx-release_)
    1. `git checkout <branch>`
    1. Do `git branch` to make sure we're on correct branch
    1. Do `git reset --hard <commit number>` (remove brackets, and use the actual 7-digit commit number) to put my changes on top of branch we just switched to. Use commit number from step 1.
    1. If not on latest commit, do a `git pull --rebase`

__Rebasing with Merge Conflicts__
1. Commit my code on mainline
1. `git pull --rebase`
1. If merge conflicts, read the super-helpful tips in terminal. Basically just
    1. Do a `git diff` to resolve the merge conflicts I have
    1. I think next do a `git rebase --continue`

__Cloning Repository__
- `git clone https://github.com/noahprince22/GridWorldMDP.git` - clones repository and puts into same folder that command is run from. Repository will be in GridWorldMDP folder
- `git clone https://github.com/noahprince22/GridWorldMDP.git putIntoThisFolder` - same as above but puts GridWorldMDP repository into _putIntoThisFolder_.

__"Checkout" or "Pull" not working__
- Common mistake is to modify files on local machine, and then try to do a "checkout" or "pull". Problem is the checkout/pull will overwrite what we have. If we do want to OVERWRITE our files, we can erase our changes by typing `git reset --hard HEAD`. Then we can checkout/pull without problems, which gets us the remote files.

__Revert changes__
- Something like
    1. `git revert <commit_number>` (without brackets)
    1. then :wq to save in VIM
    1. then rebase

__Create a new branch and upstream it to code.amazon.com__

1. [Copy the branch](https://stackoverflow.com/a/14998980)
1. `git push -u origin Icon_farm_v2` this will "upstream" the branch to code.amazon.com
1. Here's [another Reference](https://stackoverflow.com/questions/1911109/how-to-clone-a-specific-git-branch)

or my newer approach

- `git checkout -b [name_of_your_new_branch]` to create a local branch. [Link](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)
