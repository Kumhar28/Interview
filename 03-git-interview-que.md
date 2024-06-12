# Git Intoduction

- Git is distributed version control system.

# GIT-cheat-sheet

Certainly! Here's a Git cheat sheet with the 20 most important commands presented in a markdown table format:

| Command                                  | Description                                                   |
|------------------------------------------|---------------------------------------------------------------|
| `git init`                               | Initialize a new Git repository.                              |
| `git clone <repository-url>`             | Clone a remote repository to your local machine.             |
| `git add <file>`                         | Add changes from the working directory to the staging area.  |
| `git commit -m "Commit message"`         | Commit staged changes with a descriptive message.           |
| `git status`                             | View the status of your working directory and staged files. |
| `git log`                                | Display the commit history.                                  |
| `git branch`                             | List all branches in the repository.                         |
| `git checkout <branch>`                  | Switch to a different branch.                                |
| `git merge <branch>`                     | Merge changes from one branch into the current branch.      |
| `git pull origin <branch>`               | Fetch and merge changes from a remote repository.           |
| `git push origin <branch>`               | Push local commits to a remote repository.                   |
| `git remote -v`                          | List remote repositories and their URLs.                    |
| `git remote add <name> <repository-url>` | Add a new remote repository.                                 |
| `git diff`                               | Show changes between working directory and last commit.     |
| `git reset <file>`                       | Unstage changes from the staging area.                      |
| `git stash`                              | Temporarily save changes that are not ready to commit.      |
| `git restore <file>`                     | Discard changes in working directory for a specific file.   |
| `git branch -d <branch>`                 | Delete a branch locally.                                    |
| `git pull --rebase origin <branch>`      | Fetch and reapply commits from a remote repository.         |
| `git tag <tag-name>`                     | Create a lightweight tag for a specific commit.             |
| `git config --global <key> <value>`      | Set a global Git configuration option.                      |
|--------------------------------------|------------------------------------------------------------------------|
| `git switch <branch>`                | Switch to an existing branch.                                          |
| `git switch -c <new-branch>`         | Create and switch to a new branch.                                     |
| `git switch -`                       | Switch to the previously checked out branch.                          |
| `git switch -d <branch>`             | Delete a local branch (if fully merged).                               |
| `git switch -c <new-branch> <start-point>` | Create a new branch starting from a specific commit or branch.     |
| `git switch --guess`                 | Attempt to guess the desired local branch based on the current state. |
| `git switch --track <remote-branch>` | Create a new branch that tracks a remote branch.                      |
| `git switch --detach <commit>`       | Detach HEAD at a specific commit, creating a 'detached HEAD' state.   |
|-----------------------------------------------|-------------------------------------------------------------|
| `git fetch <remote>`                          | Download objects and refs from another repository.         |
| `git remote show <remote>`                    | Display detailed information about a remote repository.    |
| `git checkout -b <new-branch>`                | Create and switch to a new branch.                         |
| `git branch -a`                              | List all remote and local branches.                       |
| `git merge --abort`                          | Abort a conflicted merge operation.                       |
| `git rebase <branch>`                        | Reapply commits from another branch on top of current.    |
| `git cherry-pick <commit>`                   | Apply a specific commit to the current branch.            |
| `git log --oneline`                          | Display a simplified commit history.                     |
| `git diff <commit> <commit>`                 | Show changes between two specific commits.                |
| `git remote rename <old-name> <new-name>`    | Rename a remote repository.                               |
| `git rm <file>`                              | Remove a file from the working directory and stage.       |
| `git tag -a <tag-name> -m "Tag message"`     | Create an annotated tag with a message.                  |
| `git blame <file>`                           | Show who changed each line of a file and when.            |
| `git commit --amend`                        | Modify the last commit message or include new changes.   |
| `git log --graph --oneline --all`            | Display a compact commit history with branch graph.      |
| `git clean -n`                               | Show which untracked files will be removed.               |
| `git remote remove <remote>`                 | Remove a remote repository.                              |
| `git reflog`                                | View a log of reference (HEAD) changes.                 |
| `git revert <commit>`                       | Create a new commit that undoes a specific commit.       |
| `git reset --hard <commit>`                  | Reset the repository and working directory to a commit.  |
|----------------------------------------------|------------------------------------------------------------|
| `git submodule add <repository-url>`         | Add a submodule to your repository.                       |
| `git submodule update --init`                | Initialize and update submodules.                         |
| `git log --author=<author>`                  | Display commit history by a specific author.              |
| `git log --since=<date>`                     | Show commits since a specific date.                      |
| `git log --grep=<pattern>`                   | Search commit messages for a specific pattern.           |
| `git diff --cached`                         | Show changes in the staging area.                        |
| `git stash list`                            | List all stashed changes.                                |
| `git stash pop`                             | Apply the most recent stash and remove it from the list. |
| `git stash apply <stash>`                   | Apply a specific stash.                                 |
| `git stash drop <stash>`                    | Remove a specific stash.                                |
| `git cherry <start-commit> <end-commit>`     | Show commits in one branch that aren't in another.      |
| `git clean -f`                              | Remove untracked files from the working directory.      |
| `git log --stat`                            | Display the file changes in each commit.                |
| `git rebase -i <commit>`                    | Interactively rebase commits and squash or edit them.   |
| `git blame -L <start>,<end> <file>`          | Annotate specific lines in a file with commit info.     |
| `git log --since=<time>`                    | Show commits since a specific time (e.g., "2 weeks ago"). |
| `git revert --no-commit <commit>`           | Revert changes from a specific commit without committing. |
| `git stash branch <new-branch>`             | Create a new branch from a stash.                      |
| `git bisect start`                          | Start a binary search for a faulty commit.              |
| `git bisect good <commit>`                  | Mark a commit as good in a binary search.              |
| `git bisect bad <commit>`                   | Mark a commit as bad in a binary search.               |
  
## Repository
- In Git, Repository is like a data structure used by VCS to store metadata for a set of files and directories. 
- It contains the collection of the file as well as the history of changes made to those files. 
- Repositories in Git is considered as your project folder. 
- A repository has all the project-related data. Distinct projects have distinct repositories.
- .git directory is a git repository
- `.git` is a hidden directory in repo directory including git files. 
- It is created after "git init".
<br><br>

## Git Three stage architecture

virtual space where the changes "go" when we `git add`. It allows the preparation for any `commit`
- `Working directory`  Area of live files, also known as untracked area of git
- `Staging area` Staging area is when git starts tracking and saving changes taht occur in files
- `git dirrecttory (repository)` .git dir. Also called as local repo<br><br> 

Git = Control Version System.<br><br>
Files have 3 states:
- commited (aka stores in database)
- modified (aka changed, not commited)
- staged (A modified version of the file, marked for the next commit)<br><br>

> **Note**:Each commit has its own unique ID, it is a hash of its containers and its metadata. It must have a perfix of at least 4 chars (unique in repo).

## Index
- The Git index is a staging area between the working directory and repository. 
- It is used as the index to build up a set of changes that you want to commit together.<br><br>

## master/main
- Master is a naming convention for Git branch. 
- It's a default branch of Git. 
- After cloning a project from a remote server, the resulting local repository contains only a single local branch. 
- This branch is called a "master" branch. It means that "master" is a repository's "default" branch.<br><br>

1. Setting username: -> The username is used by the Git for each commit.

- `git config --global user.name "Sandeep"`  

2. Setting email id:-> The Git uses this email id for each commit.

- `git config --global user.email  "user@devopsbysandeep.com"`  

3. Setting editor

- `git config --global core.editor vim`  
    
- `git config -list`  :-> This command will list all your settings.


### Git configuration levels
- The git config command can accept arguments to specify the configuration level. 
- The following configuration levels are available in the Git config.

`--local`
- It is the default level in Git. Git config will write to a local level if no configuration option is given. 
- Local configuration values are stored in `.git/config` directory as a file.

`--global`
- The global level configuration is user-specific configuration. User-specific means, it is applied to an individual operating system user. 
- Global configuration values are stored in a user's home directory. `~ /.gitconfig` on UNIX systems and `C:\Users\\.gitconfig` on windows as a file format.

`--system`
- The system-level configuration is applied across an entire system. 
- The entire system means all users on an operating system and all repositories. 
- The system-level configuration file stores in a gitconfig file off the system directory. `$(prefix)/etc/gitconfig` on UNIX systems and `C:\ProgramData\Git\config` on Windows.

> **Note**: The order of priority of the Git config is local, global, and system, respectively. It means when looking for a configuration value, Git will start at the local level and bubble up to the system level.

# Git Workflow from scrach

- Define author name and email to be used for all commits in current repo. Devs
commonly use --global flag to set config options for current user.

```sh
git config --global user.name "Name"
git config --global user.email  "user@abc.com"
git config --list # displays our aliases
```
- Create empty Git repo in specified directory. Run with no
arguments to initialize the current directory as a git repository.

```sh
mkdir /project
git init
```

- Stage all changes in <directory> for the next commit.
Replace <directory> with a <file> to change a specific file.

```sh
touch file1.txt # Add some content
git add file1.txt
git add * 
```
## git commit
- Commit the staged snapshot, but instead of launching
a text editor, use <message> as the commit message.

```sh
git commit -m "<message>"
```
- List which files are staged, unstaged, and untracked.

```sh
git status
```
## git ls-files

```sh
git ls-files                     # show information about files in the index and the working tree
```

## git log
- Display the entire commit history using the default format.
- git log by default uses less command so you can use these: f=next page, b=prev page, search=/<query>, n=next match, p=prev match, q=quit

- For customization see additional options.
```sh
git log                      # shows the log of commits
git log --oneline            # shows the log of commits, each commit in a single line

git log --author="Sandeep"
# OR
git log --author="sandeep.sontakkey@gmail.com"
git log --author="Ram"  # No output beacause no commit done on this
git log --no-pager    # shows the log of commits without less command
git log --oneline --graph --decorate    # shows the log of commits, each commit in a single line with graph 
git log --since=<time>                    # shows the log of commits since given time
git log -- <file_name>
git log -p <file_name>       # change over time for a specific file
git log <Branch1> ^<Branch2> # lists commit(s) in branch1 that are not in branch2
git log -n <x>               # lists the last x commits
git log -n <x> --oneline     # lists the last x commits, each commit in single line
git grep --heading --line-number '<string/regex>' # Find lines matching the pattern in tracked files
git log --grep='<string/regex>'                   # Search Commit log

```

> **Note**: There are muliple persons working in a single project
 To identify the commit of a perticular person

## git reflog

- Show a log of changes to the local repository’s HEAD .
- Add --relative-date flag to show date info or --all to show all refs.

```sh
git reflog #--> all the changes
git reflog <branch> #--> changes on our branch
git reflog --date=relative #--> displays changes relative to time
```
<br><br>

## Git Ignore
- In Git, the term ignore used to specify intentionally untracked files that Git should ignore. 
- It doesn't affect the Files that already tracked by Git.
- is a file including names of stuff that you don"t want to be staged or tracked.
- You usually keep your local files like database, media, etc here.
- You can find good resources online about ignoring specific files in your project files.
- .gitignore is also get ignored 
- .gitignore = file in the main folder which contains a list of files that are ignored by git (so they're not affected by `git add`s and `git status`es). 
- It can contain patterns (`*.pyc, /folder/, /folder,`) and paths to files.<br><br>
<br>

## Git rm
- In Git, the term rm stands for remove. 
- It is used to remove individual filwebes or a collection of files. 
- The key function of git rm is to remove tracked files from the Git index. 
- Additionally, it can be used to remove files from both the working directory and staging index.<br><br>

```sh
git rm <filename> # deletes a file, updates git and then commit!<br>
git rm --cached <filename> # delete a previously tracked file
```
<br>


## git diff to check difference
```sh
git diff
git diff # displays what will be added if I `git add`, so what changed in the folder and hasn't been updated yet
git diff <filename>  # displays the alterations of a file (the modified and the commited versions of it)
git diff --staged # displays what has already been added and thus what changed will be recorded
git diff HEAD # displays changes since last commit
git diff <Commit ID><any previous ID> # you can comapir the using commit ID
```
<br><br>

## git archive
- create an archive of files from a named tree

```sh
git archive <branch_name> --format=zip --outpute=./<archive_name>.zip 
```

# Undo Changes
## HEAD

- HEAD is the representation of the last commit in the current checkout branch. 
- We can think of the head like a current branch. 
- When you switch branches with git checkout, the HEAD revision changes, and points the new branch.<br><br>
<br><br>

## Checkout
- The git checkout command is used to delete last change in tracked file in a repository.<br><br>
```sh
git checkout -- <file name>
```

## Git Restore
- restore file after file modified
git rerstore --staged <file-name>

## Git Revert

- In Git, the term revert is used to revert some commit. 
- To revert a commit, `git revert` command is used. 
- It is an undo type command. However, it is not a traditional undo alternative.
- Create new commit that undoes all of the changes made in <commit>, then apply it to the current branch.
- Inverted add/deletes etc. It cancels the commit that has already happened.
- revert will remove the content of latest commit and create new comment ID with message

```sh
git revert <commit hash id> # revert is commited and content but no msg
git revert -n <commit hash id> # first evert and seperately commit the change
git commit -am "commit git revert" # modify any file
git log --online # latest comment we will see
git revert HEAD 

```
<br><br>

## Git Reset

- In Git, the term reset stands for undoing changes. 
- The git reset command is used to reset the changes. 
- The git reset command has three core forms of invocation. 
These forms are as follows.
o	Soft
o	Mixed
o	Hard<br><br>
- It will reset your HEAD. It will rollback back to previous commit and delete the latest commit 
- This unstages a file without overwriting any changes.
- we are basically doing "rollback"

```sh
git log --online
git reset <commit hash id>
git reset --mixed <git ID>       # This will reset comment history file will be in working area
git reset --soft <git ID>       # This will reset only comment history file will be in staging area
git reset --hard <commit hash id>  # This will reset and changes and content will reverted in the files.

```
## Git clean
- Shows which files would be removed from working directory.
- Use the -f flag in place of the -n flag to execute the clean.

```sh
git clean -n # Test-Delete untracked files
git clean -f # Delete untracked files (not staging)
git clean -f -d/git clean -fd     # To remove directories permanently
git clean -f -X/git clean -fX    # To remove ignored files permanently
git clean -f -x/git clean -fx     # To remove ignored and non-ignored files permanently
git clean -d --dry-run            # shows what would be deleted
```

# Rewriting Git History 

## amend
- Replace the last commit with the staged changes and last commit
- combined. Use with nothing staged to edit the last commit’s message.
- Update most recent commit (also update the commit message)

```sh
git commit --amend -m "ammend comment" # quickly modify a commit before pushing
git commit --amend           # combine staged changes with the previous commit, or edit the previous commit message without changing its snapshot
git commit --amend --no-edit # amends a commit without changing its commit message
git commit --amend --author='Author Name <email@address.com>'    # Amend the author of a commit
```
## Rebase
- In Git, the term rebase is referred to as the process of moving or combining a sequence of commits to a new base commit. 
- Rebasing is very beneficial and visualized the process in the environment of a feature branching workflow.
- From a content perception, rebasing is a technique of changing the base of your branch from one commit to another.
- Rebase the current branch onto <base>. 
- <base> can be a commit ID, branch name, a tag, or a relative reference to `HEAD`

```sh
git rebase <base>
git rebase -i <commit_id>         # Rebase commits from a commit ID
git rebase --abort                # Abort a running rebase
git rebase --continue             # Continue rebasing after fixing all conflicts
```
<br><br>

## git cherry-pick
- git push to origin
- realising done commit on wrong branch
- want to commit a spefic commit then we use cherrypick.
- If you want to merge a specific commit then we use cherry-pick.
- If you want a specific feature from another branch in current branch then we can use cherry-pick with using commit ID.
```sh
git switch master
git cherry-pick  <commit-ID> # this ID is from another branch eg taken from Devlope branch
```

# Remote Repositories
## GITHUB
- GitHUB is a website and cloud-based service that helps developer to store their code, as well as track and control changes to their code.
- GitHUB is remote repository 
<br><br>

## Remote
- In Git, the term remote is concerned with the remote repository. 
- It is a shared repository that all team members use to exchange their changes. 
- A remote repository is stored on a code hosting service like an internal server, GitHub, Subversion and more.
- In case of a local repository, a remote typically does not provide a file tree of the project's current state, as an alternative it only consists of the `.git` versioning data.
<br><br>

```sh
git remote add <name> <url>
git remote add origin https://github.com/repo_name.git

git remote                         # shows the remotes
git remote -v                      # shows the remote for pull and push
git remote add my-remote <address> # creates a remote (get the address from your git-server)
git remote rm my-remote            # Remove a remote
```
## Origin
- In Git, "origin" is a reference to the remote repository from a project was initially cloned. 
<br><br>

## Clone and the repo
- The git clone is a Git command-line utility. It is used to make a copy of the target repository or clone it. 
- If I want a local copy of my repository from GitHub, this tool allows creating a local copy of that repository on your local directory from the repository URL.<br><br>
```sh
git clone <repo link>
git clone <address> # creates a git repo from given address (get the address from your git-server)
git clone <address> -b <branch_name> <path/to/directory>  # clones a git repo from the address into the given directory and checkout's the given branch
git clone -b main <repo link>  # create new content on githuub assume commmited this file on github
git clone <address> -b <branch_name> --single-branch  # Clones a single branch
```

## Pull
- The term Pull is used to receive data from GitHub. 
- It fetches and merges changes on the remote server to your working directory. 
- The git pull command is used to make a Git pull.<br><br>
- Fetch the specified remote’s copy of current branch and immediately merge it into the local copy.

```sh
git pull <remote>
```

## Fetch
- It is used to fetch branches and tags from one or more other repositories, along with the objects necessary to complete their histories. 
- It updates the remote-tracking branches.<br><br>
```sh
git fetch <remote> <branch>
```

## Upstream And Downstream
- The term upstream and downstream is a reference of the repository. 
- `upstream` is where you cloned the repository from (the origin) 
- and `downstream` is any project that integrates your work with other works. 
- However, these terms are not restricted to Git repositories.<br><br>

## Push
- The push term refers to upload local repository content to a remote repository. 
- Pushing is an act of transfer commits from your local repository to a remote repository. 
- Pushing is capable of overwriting changes; caution should be taken when pushing.<br><br>

```sh
git push <remote> <branch>
```

## Tag
- Tags make a point as a specific point in Git history. 
- It is used to mark a commit stage as important. 
- We can tag a commit for future reference. 
- Primarily, it is used to mark a projects initial point like v1.1. 
There are two types of tags.
1.	Light-weighted tag
2.	Annotated tag

```sh
git tag                           # shows all the tags
git tag -a v1.0 -m "msg"          # creates an annotated tag
git show v1.0                     # shows the description of version-1.0 tag
git tag --delete v1.0             # deletes the tag in local directory
git push --delete my-remote v1.0  # deletes the tag in my-remote (be carefore to not delete a branch)
git push my-remote my-branch v1.0 # push v1.0 tag to my-remote in my-branch
git fetch --tags                  # pulls the tags from remote
```
<br><br>

## GITHUB Private repository
```sh
git add .
git commmit -am "modify the file"  # this command run only when there is already tracked files

git push

ask password 
```
> **Note:** In private code reporitory we have to provide credententials on both operations push and pull.
            Every time you are require to push the code to github

## Authentication in git and github

1) Open your githubaccout and go to settings
2) got ssh and GPG keys
3) Create ssh keys

```sh
ssh-keygen -t ed25519 -C "yogesh@gmail.com"

Your identification has been saved in /c/Users/Yogesh/.ssh/id_ed25519
Your public key has been saved in /c/Users/Yogesh/.ssh/id_ed25519.pub
```
- Now try git push again
`OR`
- Create tockan in github developer setting
```sh

git remote -v # this may be your ssh url
git remote set-url origin https://<username>:<tokan>@githun.com/.............
git push origin master
```

## git branch
- A branch is a version of the repository that diverges from the main working project. 
- It is an essential feature available in most modern version control systems. 
- A Git project can have more than one branch. 
- We can perform many operations on Git branch-like rename, list, delete, etc.<br><br>
- List all of the branches in your repo. Add a <branch> argument to

```sh
# Dafault Branch main or master
# Branching is a version of a code
# main branch will be continue
git branch    # show all branches
git branch -a  #===> list all available branch
git branch <branch name> #===> create new branch
git branch -m <old name><new name>  #====>remame the branch
git branch -d <branch name>   #====> delete branch

```
## git switch / checkout
- Switch to another branch 
```sh
git switch <branch name>
git checkout -b <branch name> # create and switch to new created branch
git checkout <branch name> #====> Switch the branch in git
```

## git merge
- The git merge command facilitates you to take the data created by git branch and integrate them into a single branch.<br><br>
```sh
git merge <branch>
```
#### **TASK**
1. create a new branch with the name <branch> .
```bash
git branch
* master    # ===> you are on this branch
git branch fix
or
git checkout -b fix
```
2. Create and check out a new branch named <branch> .
```bash
git switch fix
or
git checkout fix
```
3. Add some files/ content to branch
```bash
git status
git commit -am "sample mmerge test 01"
git checkout master
```
4. Check difference in both the branches
```bash
git checkout master
git checkout fix
```
5. Push new branch to GITHUB
```bash
git push origin dev
```
6. Merge <branch> into the current branch.
```bash
git log --oneline --graph
git checkout master
git merge fix -m "merging devloped main"
```
7. Push master branch to GITHUB
```bash
git push origin master
```
8. delete the branch "fix"
```bash
git branch -d fix
```

## Merge conflicts 
- There is conflict in files, auto merge failed (master to dev)
```
Conflicts can't be automatically merged! Git has changed our file, merges what it can, but the rest is left on us:
Open an editor and look for lines like so: <<<<<, =====, >>>>>
These mark our conflict areas, where we keep all we need and discard what we don't.
Afterwards, we git add each file, git commit (therefore merge) and all is OK!
```
- Resolve the conflict by editing file
#### **TASK**
- Do some changes in same files in both the branches and try to merge.

# Git stashing
- Sometimes you want to switch the branches, but you are working on an incomplete part of your current project. 
- You don't want to make a commit of half-done work. Git stashing allows you to do so. 
- The git stash command enables you to switch branch without committing the current branch.<br><br>

```sh
git stash apply 0               # applies stashed state with index 0
git stash                            # stashes the tracked file changes (git status will be clean after it)
git stash clear                            #  clear stash data
git stash -u                         # stash everything including new untracked files (but not .gitignore)
git stash save "msg"                 # stash with a msg
git stash list                       # list all stashes
git stash pop                        # removed code from stash / delete the recent stash and applies it
git stash pop stash@{2}              # delete the {2} stash and applies it
git stash show                       # shows the description of stash
git stash apply                      # keep the stash and applies it to the git
git stash branch my-branch stash@{1} # creates a branch from your stash
git stash drop stash@{1}             # deletes the {1} stash
git stash clear                      # clears all the stash
```

> **Note**:- In apply and pop difference is in pop no need to remove stash area


# Some useful notes
## Better Commit messages:
- Key to Effective Debugging
- For the commit message to help in debugging effectively, ensure that it is short and use an imperative 
- mood (spoken or written as if giving a command or instruction) when constructing them.
- Also use feature tense for commit messages.
- The first word in your commit message should be one of these:
#) Add
#) Create
#) Refactor
#) Fix
#) Release
#) Document
#) Modify
#) Update
#) Remove
#) Delete etc...

## About resetting:
- Use git revert instead of git reset in shared repositories
- git revert creates a new commit that introduces the opposite changes from the specified commit.
- Revert does not change history the original commit stays in the repository


## Difference between ~ and ^ in git:
###   > ^ or ^n
        >no args: == ^1: the first parent commit
        >n: the nth parent commit

####   > ~ or ~n
        >no args: == ~1: the first commit back, following 1st parent
        >n: number of commits back, following only 1st parent
note: ^ and ~ can be combined

#### What are the different GIT branching strategies?
##### Master branch
- This is the main branch and one of the repository in which we have the latest stable code of production.  

General rules:

- Access to direct merge is restricted
- Best practice is to create a CI/CD pipeline to merge code into this branch after deployment is done in Production
- It should always have the latest stable version of production server
- Allow access to only CD tools like Jenkins to make commits to this branch

The master branch should never have unreleased code, i.e., commits made but not yet released.



##### Integration branch
This is the most important and active branch of the repository from which we make releases to the production server.

General rules:

- Access to direct merge is restricted
- Code is merged into this branch when it becomes eligible for production deployment
- Code in this branch should always be in a deployable state to production
- QA tested code should be into this branch using CI/CD tools
Ideally, the Integration branch should also never have unreleased code, some time on the deployment day when the code is merged a few hours before deployment time.

‍
##### Staging branch
This is another stable branch of the repository for QA-environment from which we make releases to the QA server.

General rules:

- Access is restricted
- Changes can be submitted only through Pull Requests. No direct commits are allowed
- Should always have the latest stable/released version of QA release server
- It is absolutely necessary to ensure only dev tested and reviewed code gets merged into this branch
Prior to production deployment, all the feature changes must get merged in staging and validated on QA. Once validation is completed, we'll raise another MR towards the integration branch.


##### Dev-deploy branch
This branch will be used primarily for deploying on-going development work to the Dev environment. Since multiple teams may work on different features, projects and bugs at the same time, all of them need a Dev environment to test the changes before moving to QA. The idea of the Dev-deploy branch is to merge multiple feature branches to a common branch and deploy the same.

This is so that everyone can use a shared development environment at the same time to validate changes.

##### Feature branching
- Feature branching is a simple branching strategy where each new feature is developed on its own branch.
- This approach allows for isolated development and testing of features, making it easier to roll back changes if necessary.
