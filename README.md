# Github
- Config files are global to the host
- 4 Stages of a File in Git ![File Stages](Images/4Stages_Of_File.png)
- GIT Cheat Sheet ![Cheat Sheet](Images/Git-Cheat-Sheet.webp)
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

## Git Commands 
### git init
- Initializes a database in the ```.git folder```
- Repository is entirely stored within this ```.git folder```
- Files within ```.git folder```
    ``` 
    cd .git 
    ls
    ```
    - Files Present ![.git folder contents](Images/git_folder_files.png)
***

### HEAD File
- This file points to the current branch or commit ID you are currently on
- Inside this file (```cat HEAD```) you can find string ```refs/heads/currentBranch```, this an internal representation of ```currentBranch```
***

### Move HEAD to previous commit
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

### GIT Config File
- Config file stores info about repo's local configuration 
- ```
	cd .git
	cat config
  ``` 
- ![git config](Images/git_config.png)
***

### git log
- Look at repositories history
- ``` git log ``` ![git log](Images/git_log.png)

***

### git status
- Retrieve Repo's current status, deleted/modified/created files
- ```Untracked Files``` => Git has detected that a file exists, but the repo isn't aware of it, add file to repo to make repo aware of it
***

### git add
- Tells git repo to starts tracking the file in the local index
- ```git add fileName```
- Adds a file to the index. It is ready to be committed to the repository.
- Still, the file won't have any history! Git has simply been made aware of the file, and you must make a commit to initiate Git’s history.
***

### git commit
- Tells Git to take a snapshot of all added content at this point.