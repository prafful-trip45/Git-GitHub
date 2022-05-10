# Github
- Config files are global to the host
- 4 Stages of a File in Git ![File Stages](Images/4Stages_Of_File.png)
- GIT Cheat Sheet ![Cheat Sheet](Images/Git-Cheat-Sheet.webp)
- The repo from which current folder was cloned, that remote is given ```origin``` name by default
- Git can supported both Distributed VCS as well as Centralized VCS
***

## Errors faced
- Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
    - Generate Personal Access Token and instead of entering password enter the generated PAT
- Prompt to enter Github username and password every time
    - Configure osxkeychain credential helper
    - ```https://www.atlassian.com/git/tutorials/install-git```
    - Store PAT Under Github Keychain Password
    - Now after you enter username and password for the first time
    - osxkeychain will get store the credentials and you don't need to enter uname and pwd each time you push to main

# Git Commands 
## git init
- Initializes a database in the ```.git folder```
- Repository is entirely stored within this ```.git folder```
- Files within ```.git folder```
    ``` 
    cd .git 
    ls
    ```
    - Files Present ![.git folder contents](Images/git_folder_files.png)
***

## HEAD File
- This file points to the current branch or commit ID you are currently on
- Inside this file (```cat HEAD```) you can find string ```refs/heads/currentBranch```, this an internal representation of ```currentBranch```
***

## Move HEAD to previous commit
- In order to do so, we'll need the commit hash
- ```git log``` command, copy the commit ID/commit HASH ![git log](Images/git_log.png)
- ```git checkout commitHash```, this command will move the current head to particular commit ![git checkout commitHash](Images/git_checkout_commitHash.png)
- Now if you make changes here you won't be able to push it, as there is no branch created

	#### How to push changes from commitID
	- Add files and commit changes
	- You will get an associated commitID/Hash
	- Create branch out of this commit ID
	- ```git branch branchName commitID/Hash```
	- Now you can push these changes
***

## GIT Config File
- Config file stores info about repo's local configuration 
- ```
	cd .git
	cat config
  ``` 
- ![git config](Images/git_config.png)
***

## git log
- Look at repositories history
- ``` git log ``` ![git log](Images/git_log.png), hit space+down to scroll output pages
- ```git log oneline```, view the log is ```one line per commit```
- ```git log --oneline --graph```, get a visual representation of the history
***

## git status
- Retrieve Repo's current status, deleted/modified/created files
- ```Untracked Files``` => Git has detected that a file exists, but the repo isn't aware of it, add file to repo to make repo aware of it
***

## git add
- Tells git repo to starts tracking the file in the local index
- ```git add fileName```
- Adds a file to the index. It is ready to be committed to the repository.
- Still, the file won't have any history! Git has simply been made aware of the file, and you must make a commit to initiate Git’s history.
***

## git commit
- Tells Git to take a snapshot of all added content at this point.
- ``` git commit -m "Commit Message"
- Now changes made to this file can be seen by ```git diff``` command
***

## git diff
- Look at local file changes ![git diff](Images/git_diff.png)
***

## Simultaneous Add and commit
- ```git commit -am "Commit Message"```
***

## git clone
- Create Local copies of git repositories to work with
***

## git reset
- Command to return to a prvious known state
- Types of reset in git
	- ```soft``` : only changes HEAD, but doesn’t change staged files in index or working files, just moves HEAD ,no alteration to added/staged files or modified files
	- ```mixed```: moves HEAD and updates the index with the contents of the revision to which HEAD now points
		- Takes items out of their added status but keeps them altered in the current working folder	--> ```default reset flag used```.
	- ```hard``` : --hard not only takes items out of their added status, but they also make the working tree state consistent with what was last committed. You can effectively lose your changes with the --hard flag.
***

## Removed files by mistake, Recover it !!
- ```rm -rf ../Git-Github/*```
- Above command deletes your cloned repo.
- But ```.git``` folder is skipped from deletion
- The ```*``` character does not match any file starting with ```.```
- Restore
	- ```git reset``` to recover the state of Git repo
	- By default, Git will recover whatever has been added to the index/staging area an place it in your working directory
	- ```git reset --hard```  will reset all local and added changes, reverting your checkout to a just-cloned and committed state.
***

## git branch
- ```git branch newBranch```
***

## git checkout
- Switch to a branch ```git checkout branchName```
***

## Detached 
- **Detaching**
	- The HEAD pointer can move to any arbitrary point, achieved by ```git checkout```
	- Specify a reference / commit ID 
	- ``` git checkout e36355ed00ac3af009d7113a9dd281c269a79afd```
	- **Detached HEAD** just means that the HEAD pointer is not pointed to any branch right now
	- Instead it is pointing to a commit ID
***

## Tags
- Tags are the same as branches, except they do not have history. They point to a particular commit, but it doesn't change
- ```git tag i_was_here```
***

## Merging
- Merging is the opposite of branching
- When you merge, you take two separate points in your development tree and fuse them together
- ```git merge firstBranchName secondBranchName```
- Pre Merge repo tree ![Pre-Merge Tree](Images/Pre-Merge.png)
- Post Merge repo tree ![Post-Merge Tree](Images/Post-Merge.png)
### Merge Conflicts
- When merging current branch ```A``` with another branch ```B```, git looks for the first common ancestor
- Git then takes the changes on the branch ```B``` that you are merging into from that ```first common ancestor``` and applies them to the branch you are on in one go.
- These changes create a new commit.
- Sometimes these changes conflict with each other, meaning both branches altered same lines, thus git throws a merge conflict error
- 3 type of arrows
    - ```<<<<<<<``` Marks First common ancestor, and the start of changes on current branch
    - ```=======``` Marks the junction of two branches, the current branch and the branch to be merged with
    - ```>>>>>>>``` Marks the end of changes in other branch
***

## git stash
- With ``stash`` concept, we can store all local changes and re-apply at will wherever needed
- ```do some work
    get interrupted
    git stash
    deal with interruption
    git stash pop```
- Changes are stores on a separate branch named ``ref/stash``
- Git commits the state of the index and then commits all current local changes to above branch
- “commit” message ``WIP on master`` and ``index on master`` is added automatically for the stash.
- And the HEAD pointer is moved back to previous commit before these local changes
- ``git stash list``
- Stash works on FIFO i.e., stack DS, hence latest stash changes are applied first
- ``git stash show --patch stash@{0}`` to see information about particular git stash
- ``git stash apply stash@{1}`` to apply a particular stash changes
- ``git stash drop`` will remove the stash item.
***

## Git Add Interactive
### git add -i command
- Opens up Git Interactive menu
- TBD
***

## Reflog
- Reflog gives you references to a sequential history of what you have done to the repository
- Git's reflog is a history of the changes made to the HEAD 
- Delete current commit by following commands
```  git checkout HEAD^
	 git branch -f currentBranch
	 git checkout currentBranch
	 git log
```
- Now you can see ```git log``` doesn't show your latest commit, and it's history is kind of lost
- This is where ```git reflog``` comes into picture, it tracks all the movements of HEAD pointer, and it contains references/commitID's to the state of the repository ay various points even in those points are no longer reachable within the repository
- ``` git reset --hard latestCommitID
	  git log
  ```
- Above command will help restore previous commit
***

## Cherry-Picking
- ``Port changes from one branch to another``
- Since every commit in Git is a change set with a reference ID, changes can be ported from one branch to another
- Use commit ID of which changes are to be brought into current branch
- ```git cherry-pick commitID```
- Above command might fail if ``diff`` operation can be applied, i.e., merge conflicts arise
**

## Git Rebase and Fast-Forwarding
- Concept of Git rebase is to overcome drawbacks of merging
- With ``Merging``, history can get complicated due to extra commits getting introduced
- And with rebase current branch can be deleted safely without any significant information being lost.
- Merging Scenarios
	- ![Before Merge](Images/Pre-Merge1.png)
	- ![Post Merge](Images/Post-Merge2.png)
- With rebase 
	- ![After Rebase](Images/afterRebase.png)
	- ![After Fast Forward](Images/afterFastForward.png)
- ``What Rebasing Does``
	- ``git rebase master``, this command takes the changes from latest master branch commit and move them to currentBranch, which might result in merge conflicts
	- Afterr resolving merge conflicts do ``git rebase --continue`` to continue rebase operation
	- Now head is pointing to currentBranch, refer to After ``Rebase Image`` above
	- Now all the changes are in one tree line, now merge ``current branch`` into ```master branch``` by ``git merge branchName`` command
	- Because the changes are in a line, there aren’t any new changes that need to be made. The master branch pointer merely needs to be “fast-forwarded” to the same point as feature1!
	- Boom!! You are in the desired state of ``After Fast Forward`` image above
**

## Git Bisect
- ``man git-bisect``
- Bisecting is a very powerful ``tool for finding bugs``.
- You create a ``Git bisect “session”`` and interact with the repository until you get the answer to your problem.
- Scenario
	- Suppose there are 100 commits to a branch ![Initial Bisect branch](Images/100CommitBranch.png)
	- Now I clone repo and notice a bug with current state
	- To investigate the issue 
		- First way is to read code, try to debug, do lodding, etc.
		- Second way is to use ``git bisect``
- Choose two scenarios, ``good`` and ``bad`` ![goodAndBadCommit](Images/good-bad-commits.png)
- Now git bisect works by Binary Search method 
- It provides a version that is ``halfway`` in between ``good`` and ``bad`` ![git bisect 1](Images/git-bisect-1.png)
- And carry on above process until the commit where bug arised is found ![git bisect 2](Images/git-bisect-2.png)
- BAD commit found ![BAD commit found](Images/found-BAD-commit.png)
- ```git bisect start
	 git bisect bad
	 git bisect good
  ```
- Repeat until the broken commit is found

### ~ Operator
- Used to move current head to n number of commits back
- Example - ``git checkout HEAD~99`` will result in HEAD moving from commit 100 to commit 1
### ^ Operator
- Used to move to parent commit
- Example - ``git checkout HEAD^99`` will move HEAD to it's parent Commit
### Practice
```git show HEAD^
	 git show HEAD^^
	 git show HEAD^2
	 git show HEAD~1
	 git show HEAD~2
	 git show HEAD~2^1
```

***

## The -X ours flag
- When merging, you can tell Git to use specific strategies to help it decide how to merge and reduce the chances of having to resolve a conflict.
- With ``-X ours`` flag, when faced with a conflict, Git will favor changes made within the current branch over the one being merged in.
***

## Cloning a Repo
- When a repo is cloned, then the origin branch has no visibility of any remotes, but the cloned one does ![clonedRepo-Config](Images/cloned-config.png) ![originRepo-Config](Images/origin-config.png)
- The files in two repos would have ``identical content``, but their config files would ``differ``
- See contents of ```./git/config``` file for a cloned repo ```cat .git/config```
- It would have entry corresponding to ``origin`` URL
	- URLs can be an ``http://`` or ``https://`` one or even ``ssh://`` or ``git://``
	- ``git://`` is a git specific protocol that is rarely used these days
	- A Git repository cloned with ``git@``, in fact using the ssh:// protocol under the hood.
- ```git remote``` would return name ```origin``` back
- The name ```origin``` is the _default name for a remote_

## Git Fetch and Push and Merge
- Remotes are divided into ``fetch`` and ``pull`` actions
- These relate to two different actions on remotes, ``getting changes from a remote`` and ``pushing changes to a remote``
- ```Fecthing from Remote```
	- The command git fetch gets the latest changes from the remote repository and copies them into the local repository, updating the local copies of any branches that have been changed.
	- These fetched changes are not mixed with local branches but are kept in a separate place in repo.
	- Reference to HEAD pointers to origin are stored under ``.git/refs`` folders files
	- ``git fetch origin branchName`` fetches changes from the specified branch
	- ``git branch --all``, you can see repository is aware of all the branches ![branches After fetch](Images/Branch-List-after-fetch.png)
- ```refs folder```
	- ``ls ./git/refs`` under cloned repo after executing Fetch ![git-refs-contents](Images/git-refs.png)
	- It has heads, which contains references/commitID's to the local branch: ``cat .git/refs/heads/master`` ![HEAD-ref-local](Images/HEAD-refsLocal.png)
	- And similarly for remote branches: ``cat .git/refs/remotes/origin/master`` ![HEAD-ref-remotes](Images/git-refs-remotes.png)
- So now we've fetched the remote branch and have a copy of it locally in cloned repo.
- ``Apply Remote Changes to Local``
	- ``git merge origin/remoteBranchName``
	- ``git log --oneline --graph``
## Git Pull
- ``git pull origin`` combines ``fetch`` and ``merge`` operations simulatneously
***

## Working with Multiple Repo's/Remotes
- How to move changes between multiple remotes !!
- Can add remote reference of branch into another by ``git remote add remoteName ../repoName``
- ``git remote -v`` to see all remotes for current repo ![Added Extra Remotes](Images/add-remote.png)
- Changes from Any remote can be fetched now ``git fetch remoteName branchname`` ![Fetch remote Branch](Images/fetch-any-remote-branch.png)
***

## Pushing Code
