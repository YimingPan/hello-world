# Highlights of Git

## Key Ideas of Git

| File State | Project Section      |
| :--------- | -------------------- |
| committed  | repository           |
| modified   | working directory    |
| staged     | staging area (index) |

## Get Started

How to [Set Up Git](https://help.github.com/articles/set-up-git/).

If you clone with HTTPS, you are recommended to [cache your GitHub password in Git](https://help.github.com/articles/caching-your-github-password-in-git/).
If you clone with SSH, you must [generate SSH keys](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) to authenticate yourself. One ssh key, one device.

## Git Basics

### fetch and pull

`git fetch <remote>`
If it is the first time you fetch data from a remote, then a FETCH_HEAD will appear when you execute `git branch -a`.

Then we may merge one remote branch into our current working branch:
`git merge <remote>/<branch>`
or create a new local branch:
`git checkout -b <branch> <remote>/<branch>`

Using `git fetch` or `git pull` command to get the latest version on remote is always a good habit. And `git fetch` is more recommended.

### Git Aliases

Aliases are nicknames of git commands. For example, after we execute the following command:

	git config --global alias.unstage 'reset HEAD --'

We can use `git unstage fileA` instead of `git reset HEAD -- fileA`.

### Git Log

Show commit history and optional information.

[option] I usually use:

`--oneline`
`--decorate` : show where the branch pointers are pointing.
`--graph`
`-p` : this option changes the behavior of `git log`. Instead of listing a commit history, it will show you change logs of every commit.

#### Compare Two Branch

[Reference](http://blog.csdn.net/u011240877/article/details/52586664)

`git log <branch1> ^<branch2>`
`git log <branch1>..<branch2>`
`git log <branch1>...<branch2>`

## Git Branching

### Merge Strategy

#### Fast Forward

When the commit pointed to by the branch "to-be-merged" is directly ahead of the commit currently on, Git simply moves the pointer forward. That's why it refers to this merge strategy as "fast forward".

By default, no new commit is created.

#### Recursive

The recursive strategy is used when the development history has diverged from some older point. In this case, Git uses three snapshots to complete the merge, and a new commit will be created.

#### Manual Merge

Sometimes even the recursive strategy cannot perform a merge process, then a merge conflict occurs. By running `git status` we can know all unmerged files. In the file, we will see something like this:

	<<<<<<< HEAD:filename
	conflicted content in HEAD
	=======
	conflicted content in "merged in" branch
	>>>>>>> branchName:filename

