# List of Git Commands

## States

* Modified;
* Staged/Index;
* Committed;

## Help

##### General

```bash
git help
```

##### Specific command

```bash
git help add
git help commit
git help <any_git_command>
```

## Configuration

### General

Git configurations are stored in the **.gitconfig** file located in the user's home directory (e.g., Windows: C:\Users\Documents and Settings\SNK or *nix /home/snk).

Configurations made with the commands below will be included in this file.

##### Set user name

```bash
git config --global user.name "Douglas Kitagawa"
```

##### Set email

```bash
git config --global user.email dk.software@engineer.com
```

##### Set editor

```bash
git -c 'diff.tool=nvimdiff' difftool
git config --global core.editor neovim
```

##### Set merge tool

```bash
git config --global merge.tool vimdiff
```

##### Set files to be ignored

```bash
git config --global core.excludesfile ~/.gitignore
```

##### List configurations

```bash
git config --list
```

### Ignoring Files

File/directory names or extensions listed in the **.gitignore** file will not be added to a repository. There are two types of .gitignore files:

- Global: Usually stored in the user's home directory. The file containing the list of files/directories to be ignored for **all repositories** should be declared as above. The file does not need to be named **.gitignore**.

- Repository-specific: Stored in the repository directory and contains the list of files/directories to be ignored only for that repository.

## Local Repository

### Create a new repository

```bash
git init
```

### Check file/directory status

```bash
git status
```

### Add file/directory (staged area)

##### Add a specific file

```bash
git add my_file.txt
```

##### Add a specific directory

```bash
git add my_directory
```

##### Add all files/directories

```bash
git add . 
```

##### Add a file listed in .gitignore (global or repository-specific)

```bash
git add -f file_in_gitignore.txt
```

### Commit file/directory

##### Commit a single file

```bash
git  commit my_file.txt
```

##### Commit multiple files

```bash
git  commit my_file.txt my_other_file.txt
```

##### Commit with a message

```bash
git  commit my_file.txt -m "my commit message"
```

### Remove file/directory

##### Remove a file

```bash
git  rm my_file.txt
```

##### Remove a directory

```bash
git  rm -r directory
```

### View history

##### Show history

```bash
git  log
```

##### Show history with diff of last two changes

```bash
git  log -p -2
```

##### Show history summary (full hash, author, date, message, number of changes (+/-))

```bash
git  log --stat
```

##### Show information in one line (full hash and message)

```bash
git  log --pretty=oneline
```

##### Show history with specific format (short hash, author, date, message)

```bash
git  log --pretty=format:"%h - %an, %ar : %s"
	
* %h: Short hash;
* %an: Author name;
* %ar: Date;
* %s: Message.

Check other formatting options in the [Git Book](http://git-scm.com/book/en/Git-Basics-Viewing-the-Commit-History)
```

##### Show history for a specific file

```bash
git  log -- <file_path>
```

##### Show history of a file containing a specific word

```bash
git  log --summary -S<word> [<file_path>]
```

##### Show file modification history

```bash
git  log --diff-filter=M -- <file_path>
```

* `<D>` can be replaced with: Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R), etc.

##### Show history by a specific author

```bash
git  log --author=user
```

##### Show revision and author of the last modification of a line range

```bash
git  blame -L 12,22 my_file.txt
```

### Undoing operations

##### Undo local changes (working directory)
Use this command while the file is not added to the **staged area**.

```bash
git  checkout -- my_file.txt
```

##### Undo local changes (staging area)
Use this command when the file is already in the **staged area**.

```bash
git  reset HEAD my_file.txt
```

If the following result is shown, the reset command did *not* alter the working directory:

```bash
Unstaged changes after reset:
M	my_file.txt
```

To modify the working directory:
```bash
git  checkout my_file.txt
```

## Remote Repository

### Show remote repositories

```bash
git  remote
```

```bash
git  remote -v
```

### Link local repository to a remote repository

```bash
git  remote add origin git@github.com:sdkitagawa/CoreSE.git
```

### Show remote repository information

```bash
git  remote show origin
```

### Rename a remote repository

```bash
git  remote rename origin CoreSE
```

### Remove a remote repository

```bash
git  remote rm CoreSE
```

### Push files/directories to remote repository

The first **push** must include the remote repository name and branch:

```bash
git  push -u origin master
```

Subsequent **pushes** do not require this information:

```bash
git  push
```

### Update local repository from remote

##### Update files in current branch

```bash
git  pull
```

##### Fetch changes without applying to current branch

```bash
git  fetch
```

### Clone an existing remote repository

```bash
git  clone git@github.com:sdkitagawa/CoreSE.git
```

### Tags

##### Create a lightweight tag

```bash
git  tag vs-1.1
```

##### Create an annotated tag

```bash
git  tag -a vs-1.1 -m "My version 1.1"
```

##### Create a signed tag
Requires a private key (GNU Privacy Guard - GPG).

```bash
git  tag -s vs-1.1 -m "My signed tag 1.1"
```

##### Create tag from a commit (hash)

```bash
git  tag -a vs-1.2 9fceb02
```

##### Push a tag to remote repository

```bash
git  push origin vs-1.2
```

##### Push all local tags to remote

```bash
git  push origin --tags
```

### Branches

The **master** branch is the main Git branch.

The **HEAD** is a *special* pointer indicating the current branch. By default, **HEAD** points to the master branch.

##### Create a new branch

```bash
git  branch bug-123
```

##### Switch to an existing branch

```bash
git  checkout bug-123
```

Here, the **HEAD** pointer points to the branch bug-123.

##### Create and switch to a new branch

```bash
git  checkout -b bug-456
```

##### Switch back to master

```bash
git  checkout master
```

##### Merge branches

```bash
git  merge bug-123
```

To merge, you must be on the branch receiving the changes. Merge can be automatic or manual. Automatic merge occurs for text files without overlapping changes; manual merge occurs when changes overlap.

Manual merge message:

```bash
Automerging my_file.txt
CONFLICT (content): Merge conflict in my_file.txt
Automatic merge failed; fix conflicts and then commit the result.
```

##### Delete a branch

```bash
git  branch -d bug-123
```

##### List branches 

###### List branches

```bash
git  branch
```

###### List branches with last commit info

```bash
git  branch -v
```

###### List branches merged with **master**

```bash
git  branch --merged
```

###### List branches not merged with **master**

```bash
git  branch --no-merged
```

##### Create remote branches

###### Push branch with same name

```bash
git  push origin bug-123
```

###### Push branch with different name

```bash
git  push origin bug-123:new-branch
```

##### Checkout remote branch locally

```bash
git  checkout -b bug-123 origin/bug-123
```

##### Delete remote branch

```bash
git  push origin:bug-123
```

### Rebasing

Rebase branch bug-123 onto master:
```bash
git  checkout experiment
```

```bash
git  rebase master
```

More info about [**Rebasing here**](http://git-scm.com/book/en/Git-Branching-Rebasing).

### Stash

To switch branches, you must commit changes first. If you want to switch without committing, create a **stash**, which is a temporary branch holding uncommitted changes.

##### Create a stash

```bash
git  stash
```

##### List stashes

```bash
git  stash list
```

##### Apply last stash

```bash
git  stash apply
```

##### Apply specific stash

```bash
git  stash apply stash@{2}
```

Where **2** is the stash index.

##### Create branch from stash

```bash
git  stash branch my_branch
```

### Rewriting history

##### Amend commit message

```bash
git  commit --amend -m "My new message"
```

##### Change last commits
Change last three commits:

```bash
git  rebase -i HEAD~3

The editor opens with the last three commits:

	pick f7f3f6d changed my name a bit
	pick 310154e updated README formatting and added blame
	pick a5f4a0d added catfile

Change to edit the commits you want to modify:

	edit f7f3f6d changed my name a bit
	pick 310154e updated README formatting and added blame
	pick a5f4a0d added catfile

Close editor.
```

Amend commit message:

```bash
git  commit –amend -m “New message”
```

Continue rebase:

```bash
git  rebase --continue
```

**Note:** You can also reorder or remove commits by editing the lines.

##### Squash multiple commits
Follow the same steps above, marking commits to squash with **squash**.

##### Remove all history of a file

```bash
git  filter-branch --tree-filter 'rm -f passwords.txt' HEAD
```

### Bisect
Bisect (binary search) helps find a commit causing a bug or inconsistency.

##### Start bisect

```bash
git  bisect start
```

##### Mark current commit as bad

```bash
git  bisect bad
```

##### Mark a commit/tag as good

```bash
git  bisect good vs-1.1
```

##### Mark current commit as good
If current commit is fine, mark it as **good**.

```bash
git  bisect good
```

##### Mark commit as bad

If commit has the issue, mark as **bad**.

```bash
git  bisect bad
```

##### Finish bisect

After finding the bad commit, return to *HEAD*:
```bash
git  bisect reset
```
