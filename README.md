# Github
- Config files are global to the host
## Errors faced
- Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
    - Generate Personal Access Token and instead of entering password enter the generated PAT
- Prompt to enter Github username and password every time
    - Configure osxkeychain credential helper
    - https://www.atlassian.com/git/tutorials/install-git
    - Store PAT Under Github Keychain Password
    - Now after you enter username and password for the first time
    - osxkeychain will get store the credentials and you don't need to enter uname and pwd each time you push to main
## Git Commands
### git init
- Initializes a database in the **.git folder**
- Repository is entirely stored within this **.git folder**
- Files within **.git folder**
    - cd .git
    - ls
    - Files Present --> ![.git folder contents](https://drive.google.com/open?id=1-8fXTRyjcCCJnYu_aNhybNn2kWOidQ0Y&authuser=stormbreaker4545%40gmail.com&usp=drive_fs)

### HEAD File
- This file points to the current branch or commit ID you are currently on
- Inside this file **cat HEAD** you can find string **refs/heads/currentBranch**, this an internal representation of *currentBranch*
- 

### Move HEAD to previous commit
- In order to do so, we'll need the commit hash
- **git log** command, copy the commit ID/commit HASH ![git log](https://drive.google.com/open?id=1-6NyebraZB2P6sfQLniNjZEX-dpQsUGU&authuser=stormbreaker4545%40gmail.com&usp=drive_fs)
- **git checkout commitHash**, this command will move the current head to particular commit ![git checkout commitHash](https://drive.google.com/open?id=1-CQDgoYf9SQx6bue2vz49i_GmS7gVGMk&authuser=stormbreaker4545%40gmail.com&usp=drive_fs)
