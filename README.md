# List of Git Commands

## States

* Modified;
* Staged/Index
* Committed;

## Help

##### General
	git help
	
##### Specific command
	git help add
	git help commit
	git help <any_git_command>
	

## Configuration

### General

Git configurations are stored in the **.gitconfig** file located in the user's home directory (e.g., Windows: C:\Users\Documents and Settings\Leonardo or *nix /home/leonardo).

Configurations made with the commands below will be included in this file.

##### Set user name
	git config --global user.name "Leonardo Comelli"

##### Set email
	git config --global user.email leonardo@software-ltda.com.br
	
##### Set editor
	git config --global core.editor vim
	
##### Set merge tool
	git config --global merge.tool vimdiff

##### Set files to be ignored
	git config --global core.excludesfile ~/.gitignore

##### List configurations
	git config --list

### Ignoring Files

File/directory names or extensions listed in the **.gitignore** file will not be added to a repository. There are two types of .gitignore files:

* Global: Usually stored in the user's home directory. The file containing the list of files/directories to be ignored for **all repositories** should be declared as above. The file does not need to be named **.gitignore**.

* Repository-specific: Stored in the repository directory and contains the list of files/directories to be ignored only for that repository.

## Local Repository

### Create a new repository

	git init

### Check file/directory status

	git status

### Add file/directory (staged area)

##### Add a specific file

	git add my_file.txt

##### Add a specific directory

	git add my_directory

##### Add all files/directories
	
	git add .	
	
##### Add a file listed in .gitignore (global or repository-specific)
	
	git add -f file_in_gitignore.txt
	
### Commit file/directory

##### Commit a single file
	
	git commit my_file.txt

##### Commit multiple files

	git commit my_file.txt my_other_file.txt
	
##### Commit with a message

	git commit my_file.txt -m "my commit message"

### Remove file/directory

##### Remove a file

	git rm my_file.txt

##### Remove a directory

	git rm -r directory

### View history

##### Show history
	
	git log
	
##### Show history with diff of last two changes

	git log -p -2
	
##### Show history summary (full hash, author, date, message, number of changes (+/-))

	git log --stat
	
##### Show information in one line (full hash and message)

	git log --pretty=oneline
	
##### Show history with specific format (short hash, author, date, message)

	git log --pretty=format:"%h - %an, %ar : %s"
	
* %h: Short hash;
* %an: Author name;
* %ar: Date;
* %s: Message.

Check other formatting options in the [Git Book](http://git-scm.com/book/en/Git-Basics-Viewing-the-Commit-History)

##### Show history for a specific file

	git log -- <file_path>

##### Show history of a file containing a specific word

	git log --summary -S<word> [<file_path>]

##### Show file modification history

	git log --diff-filter=M -- <file_path>

* <D> can be replaced with: Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R), etc.

##### Show history by a specific author

	git log --author=user

##### Show revision and author of the last modification of a line range

	git blame -L 12,22 my_file.txt 

### Undoing operations

##### Undo local changes (working directory)
Use this command while the file is not added to the **staged area**. 

	git checkout -- my_file.txt

##### Undo local changes (staging area)
Use this command when the file is already in the **staged area**.

	git reset HEAD my_file.txt

If the following result is shown, the reset command did *not* alter the working directory:

	Unstaged changes after reset:
	M	my_file.txt

To modify the working directory:

	git checkout my_file.txt

## Remote Repository

### Show remote repositories

	git remote
	
	git remote -v

### Link local repository to a remote repository

	git remote add origin git@github.com:leocomelli/curso-git.git
	
### Show remote repository information

	git remote show origin
	
### Rename a remote repository 

	git remote rename origin curso-git
	
### Remove a remote repository
	
	git remote rm curso-git

### Push files/directories to remote repository

The first **push** must include the remote repository name and branch:

	git push -u origin master
	
Subsequent **pushes** do not require this information:

	git push
	

### Update local repository from remote

##### Update files in current branch

	git pull
	
##### Fetch changes without applying to current branch

	git fetch
	
### Clone an existing remote repository

	git clone git@github.com:leocomelli/curso-git.git
	
### Tags

##### Create a lightweight tag

	git tag vs-1.1

##### Create an annotated tag

	git tag -a vs-1.1 -m "My version 1.1"

##### Create a signed tag
Requires a private key (GNU Privacy Guard - GPG).

	git tag -s vs-1.1 -m "My signed tag 1.1"

##### Create tag from a commit (hash)

	git tag -a vs-1.2 9fceb02
	
##### Push a tag to remote repository

	git push origin vs-1.2
	
##### Push all local tags to remote

	git push origin --tags
	
### Branches

The **master** branch is the main Git branch.

The **HEAD** is a *special* pointer indicating the current branch. By default, **HEAD** points to the master branch.

##### Create a new branch

	git branch bug-123
	
##### Switch to an existing branch

	git checkout bug-123
	
Here, the **HEAD** pointer points to the branch bug-123.

##### Create and switch to a new branch 

	git checkout -b bug-456
	
##### Switch back to master

	git checkout master
	
##### Merge branches

	git merge bug-123
	
To merge, you must be on the branch receiving the changes. Merge can be automatic or manual. Automatic merge occurs for text files without overlapping changes; manual merge occurs when changes overlap.

Manual merge message:

	Automerging my_file.txt
	CONFLICT (content): Merge conflict in my_file.txt
	Automatic merge failed; fix conflicts and then commit the result.

##### Delete a branch

	git branch -d bug-123

##### List branches 

###### List branches

	git branch

###### List branches with last commit info

	git branch -v

###### List branches merged with **master**

	git branch --merged

###### List branches not merged with **master**

	git branch --no-merged

##### Create remote branches

###### Push branch with same name

	git push origin bug-123

###### Push branch with different name

	git push origin bug-123:new-branch

##### Checkout remote branch locally

	git checkout -b bug-123 origin/bug-123

##### Delete remote branch

	git push origin:bug-123

### Rebasing

Rebase branch bug-123 onto master:

	git checkout experiment
	
	git rebase master
	

More info about [Rebasing](http://git-scm.com/book/en/Git-Branching-Rebasing)

### Stash

To switch branches, you must commit changes first. If you want to switch without committing, create a **stash**, which is a temporary branch holding uncommitted changes.

##### Create a stash
	
	git stash
	
##### List stashes

	git stash list

##### Apply last stash

	git stash apply

##### Apply specific stash
	
	git stash apply stash@{2}
	
Where **2** is the stash index.

##### Create branch from stash

	git stash branch my_branch

### Rewriting history

##### Amend commit message

	git commit --amend -m "My new message"

##### Change last commits
Change last three commits:

	git rebase -i HEAD~3

The editor opens with the last three commits:

	pick f7f3f6d changed my name a bit
	pick 310154e updated README formatting and added blame
	pick a5f4a0d added catfile

Change to edit the commits you want to modify:

	edit f7f3f6d changed my name a bit
	pick 310154e updated README formatting and added blame
	pick a5f4a0d added catfile

Close editor.

Amend commit message:

	git commit –amend -m “New message”

Continue rebase:

	git rebase --continue

**Note:** You can also reorder or remove commits by editing the lines.

##### Squash multiple commits
Follow the same steps above, marking commits to squash with **squash**.
	
##### Remove all history of a file

	git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
	
	
### Bisect
Bisect (binary search) helps find a commit causing a bug or inconsistency.

##### Start bisect

	git bisect start
	
##### Mark current commit as bad

	git bisect bad

##### Mark a commit/tag as good

	git bisect good vs-1.1

##### Mark current commit as good
If current commit is fine, mark it as **good**.

	git bisect good

##### Mark commit as bad
If commit has the issue, mark as **bad**.

	git bisect bad
	 
##### Finish bisect
After finding the bad commit, return to *HEAD*:

	git bisect reset
	

# Contributions

Feel free to add more info or corrections. Fork me!
