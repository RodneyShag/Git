<p align="center">
    <a href="http://files.zeroturnaround.com/pdf/zt_git_cheat_sheet.pdf">
    <img src="images/git_logo.png">
    <br>Cheatsheet
    </a>
</p>

- [Common Commands](#common-commands)
- [More commands](#more-commands)
- [Create repository](#create-repository)
- [Clone repository](#clone-repository)
- [Submit changes](#submit-changes)
- [Rebase](#rebase)
- [Revert changes](#revert-changes)
- [Stashing](#stashing)
- [Merge branch](#merge-branch)
- [Create a new branch and upstream it](#create-a-new-branch-and-upstream-it)
- [Troubleshoot](#troubleshoot)

## Common Commands

All commands should be run without the <> brackets

- `git log` shows commit ids. The latest commit is at the top.
    - `git log -p` - lists the changed files
- `git checkout -b develop` checks out a new branch called "develop"
    - `git checkout init_devices` switches branch to _init_devices_
    - `git checkout <commit_number>` goes to a specific commit
    - `git checkout -b 1234 origin/mainline` checks out a new branch called "1234", that "tracks" origin/mainline, meaning "local branch has its upstream set to a remote branch" ([Reference](https://stackoverflow.com/questions/10002239/difference-between-git-checkout-track-origin-branch-and-git-checkout-b-branch)). Here's more info: [Tracking branches](https://stackoverflow.com/questions/4693588/what-is-a-tracking-branch)
- `git status` lists new or modified files not yet committed
- `git diff <commit_number>` compares current code to any commit
- `git add *` adds all files to "Staging". Ready for commit
    - `git add <file>` adds a specific file to "Staging". Ready for commit.
- `git commit -m "Put Message Here"` commits locally
    - `git commit --amend`" updates commit by amending your new changes to it. Must run after "add" command.
    - `git commit --amend -m "an updated commit message"` updates the commit, and its commit message.
- `git branch` says which branch we're on
- `git push` pushes code to the branch we're on
    - `git push origin <my_branch>` pushes to specific branch. I think origin is a keyword.
 [Reference](https://www.digitalocean.com/community/tutorials/how-to-use-git-branches)
- `git pull` pulls all changed files

## More commands

- `git rm <file>` removes file from server (Must then do a commit, then push)
- `git ls-files | xargs wc -l` counts # of lines of code in a github repo. [Link to Repo](https://gist.github.com/mandiwise/dc53cb9da00856d7cdbb)
- `git config --global --edit` Edit git commit signature
- `git branch -d the_local_branch` Removes local branch. [Link](https://makandracards.com/makandra/621-git-delete-a-branch-local-or-remote)
- `git rebase -i HEAD~3` combines the last 3 commits into 1 commit. Called [Squashing Commits](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html).
- `git reset filename.txt` undoes adding a file.


## Create repository

1. In command line, type `git init <project name>` to create a folder that's a Git repo.
1. Add the repository to Github Desktop and push it through Github Desktop.

## Clone Repository

- `git clone https://github.com/noahprince22/GridWorldMDP.git` - clones repository and puts into same folder that command is run from. Repository will be in GridWorldMDP folder
- `git clone https://github.com/noahprince22/GridWorldMDP.git putIntoThisFolder` - same as above but puts GridWorldMDP repository into _putIntoThisFolder_.

## Submit changes

1. `git status` to list new or modified files not yet committed
1. `git add <file>`
1. `git commit -m "<commit message>"`
1. `git push` to push the code to the repository. If it fails since code needs to be pulled first, do:
    1. `git pull` - this will do a `git fetch` and a `git merge`. (assuming no merge conflicts, go onto next steps)
    1. `git push`


## Revert changes

1. `git revert <commit_number>`
1. then `:wq` to save in VIM
1. then rebase


## Rebase

#### Rebasing with Merge Conflicts

1. Commit my code on mainline
1. `git pull --rebase`
1. If merge conflicts, read the super-helpful tips in terminal. Basically just
    1. Do a `git diff` to resolve the merge conflicts I have
    1. I think next do a `git rebase --continue`

#### Head is not on main branch - Put changes on top of head

Somewhat useful [tutorial for git pull](https://www.atlassian.com/git/tutorials/syncing#git-remote)

1. Do a `git log` to get the commit number corresponding to the changes you made. Save it for step 5.
1. Get the branch we need. Try: `git pull origin <branch_name>` or  `git checkout <branch>`
1. Do `git branch` to make sure we're on correct branch
1. Do `git reset --hard <commit_number>` using the actual 7-digit (or full) commit number, to put changes on top of branch we just switched to. Use commit number from step 1.
1. If not on latest commit, do a `git pull --rebase`. Note: this command doesn't create a merge commit, so it makes other people's code diverge from what they had.


## Stashing

- `git stash` - moves your changes to a stash (a location where changes can be saved)
- `git stash save "Custom Message"` - stashes changes, with custom message.
- `git stash apply` - applies saved changes to your branch. Code also stays in stash.
- `git stash pop` - applies saved changes to your branch. Code is removed stash.
- `git stash show stash@{1} -p` - shows diff for stash@{1} (the 1st entry in the stash). Remove the `-p` to get abbreviated diff.
- `git stash list` - shows all stashes.
- [More stash commands](https://www.atlassian.com/git/tutorials/saving-changes/git-stash), and [even More stash commands](https://medium.freecodecamp.org/useful-tricks-you-might-not-know-about-git-stash-e8a9490f0a1a)

__Stash topmost commit__

1. `git reset HEAD^` - basically like an uncommit
1. `git stash` (this may not stash new files. Maybe try "tracking" the new files to see if this works)


## Merge Branch

To merge 1 branch into another, "giving branch", and do a `git pull`. Then go to receiving branch, and run 1 of the following merge commands:
- `git merge <branch_name>` - Run this from receiving branch. More info [here](https://www.atlassian.com/git/tutorials/using-branches/git-merge)
- `git merge <commit_number_from_another_branch>` - Merges another branch (up to the commit number) into this branch.


## Troubleshoot

__"Checkout" or "Pull" not working__

Common mistake is to modify files on local machine, and then try to do a "checkout" or "pull". Problem is the checkout/pull will overwrite what we have. If we do want to OVERWRITE our files, we can erase our changes by typing `git reset --hard HEAD`. Then we can checkout/pull without problems, which gets us the remote files.
