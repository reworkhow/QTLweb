# Git


Turorial from **tryGit** in code school

> scratched the surface of Git

### definition:

Git allows groups of people to work on the same documents (often code) at the same time, and without stepping on each other's toes. It's a distributed version control system.

##### glossory

`Staging Area`: A place where we can group files together before we "commit" them to Git.

`Commit`: A "commit" is a snapshot of our repository. This way if we ever need to look back at the changes we've made (or if someone else does), we will see a nice timeline of all changes.

`branching`: When developers are working on a feature or bug they'll often create a copy (aka. branch) of their code they can make separate commits to. Then when they're done they can merge this branch back into their main master branch.

Branches are what naturally happens when you want to work on multiple features at the same time. You wouldn't want to end up with a master branch which has Feature A half done and Feature B half done. Rather you'd separate the code base into two "snapshots" (branches) and work on and commit to them separately. As soon as one was ready, you might merge this branch back into the master branch and push it to the remote server.

### basic commands in git

##### commands

| commands | actions |
| :-- | :-- |
| git init | to initialize a Git repository here |
| git status | to see the current state of our project |
| git add | To tell Git to start tracking changes made to octocat.txt, we first need to add it to the staging area by using git add. |
| git commit | To store our staged changes we run the commit command with a message describing what we've changed. |
| git log | Think of Git's log as a journal that remembers all the changes we've committed so far, in the order we committed them. |
| git remote add origin [https://github.com/try-git/try_git.git](https://github.com/try-git/try_git.git) |  |
| git push -u origin master |  |
| git pull origin master |  |
| git diff HEAD | show the diff of our most recent commit |
| git diff --staged | show diff in stage |
| git reset | unstage files (only unstage not remove from disk, see detail in git checkout below) |
| git checkout ... | go back to how thing were before a time point |
| git branch new_branch | create a branch |
| git checkout new_branch | switch to another branch |
| git checkout -b new_branch | combine the previous two together, create and switch to a new brach |
| git rm | remove files from disk and stage the removal( after this still need to be commited) |
| git rm -r | for folders |
| git merge another_branch | merge another branch to this one |
| git branch -d branch_name | delete a branch |
| git branch -D | force delete (reason see below) |

##### outputs in terminal



```
> git init

Initialized empty Git repository in /.git/
(Success!)

$ git status

# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)

(Success!)

$ git status (after create a file in directory)

# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#   octocat.txt
nothing added to commit but untracked files present (use "git add" to track)

(Success!)

$ git add octocat.txt

(Nice job, you've added octocat.txt to the Staging Area)

$ git status

# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#   new file:   octocat.txt
#

(Success!)

$ git commit -m "Add cute octocat story"

[master (root-commit) 20b5ccd] Add cute octocat story
1 file changed, 1 insertion(+)
create mode 100644 octocat.txt

(Success!)

$ git log

commit 3852b4db1634463d0bb4d267edb7b3f9cd02ace1
Author: Try Git <try_git@github.com>
Date:   Sat Oct 10 08:30:00 2020 -0500

    Add all the octocat txt files
```



 commit b652edfd888cd3d5e7fcb857d0dabc5a0fcb5e28 Author: Try Git Date: Sat Oct 10 08:30:00 2020 -0500



```
    Added cute octocat story

(Success!)

$ git remote add origin https://github.com/try-git/try_git.git
$ git push -u origin master

Branch master set up to track remote branch master from origin.
(Success!)

$ git pull origin master

Updating 3852b4d..3e70b0f
Fast-forward
yellow_octocat.txt |    1 +
1 file changed, 1 insertion(+)
create mode 100644 yellow_octocat.txt
(Success!)

$ git diff HEAD

diff --git a/octocat.txt b/octocat.txt
index 7d8d808..e725ef6 100644
--- a/octocat.txt
+++ b/octocat.txt
```



 @@ -1 +1 @@  -A Tale of Two Octocats  +[mA Tale of Two Octocats and an Octodog (Success!)



```
$ git diff --staged

diff --git a/octofamily/octodog.txt b/octofamily/octodog.txt
new file mode 100644
index 0000000..cfbc74a
--- /dev/null
+++ b/octofamily/octodog.txt
```



 @@ -0,0 +1 @@  +[mwoof (Success!)



```
$ git reset octofamily/octodog.txt
（remove this file）

$ git checkout -- octocat.txt
$ git branch clean_up
(create a brach called clean_up)
$ git checkout clean_up

Switched to branch 'clean_up'
(Success!)

$ git rm '*.txt'

rm 'blue_octocat.txt'
rm 'octocat.txt'
rm 'octofamily/baby_octocat.txt'
rm 'octofamily/momma_octocat.txt'
rm 'red_octocat.txt'
(Success!)
(don't forget next step)
(Now that you've removed all the cats you'll need to commit your changes.)

$ git commit -m "Remove all the cats"

[clean_up 63540fe] Remove all the cats
5 files changed, 5 deletions(-)
delete mode 100644 blue_octocat.txt
delete mode 100644 octocat.txt
delete mode 100644 octofamily/baby_octocat.txt
delete mode 100644 octofamily/momma_octocat.txt
delete mode 100644 red_octocat.txt
(Success!)

$ git checkout master
(We're already on the master branch, so we just need to tell Git to merge the clean_up branch into it)
$ git merge clean_up

Updating 3852b4d..ec6888b
Fast-forward
blue_octocat.txt             |    1 -
octocat.txt                  |    1 -
octofamily/baby_octocat.txt  |    1 -
octofamily/momma_octocat.txt |    1 -
red_octocat.txt              |    1 -
5 files changed, 5 deletions(-)
delete mode 100644 blue_octocat.txt
delete mode 100644 octocat.txt
delete mode 100644 octofamily/baby_octocat.txt
delete mode 100644 octofamily/momma_octocat.txt
delete mode 100644 red_octocat.txt
(Success!)  

$git branch -d clean_up
Deleted branch clean_up (was ec6888b).
(Success!)

$git push 
(push everything you've been working on to your remote repository)
To https://github.com/try-git/try_git.git
3e70b0f..70d9899  master -> master
(Success!)
```



##### Tricks

###### `wildcard`:

I put some in an octofamily directory and some others ended up in the root of our octobox. Luckily, we can add all the new files using a wildcard with git add. Don't forget the quotes!



```
git add '*.txt'
```



We need `quotes` so that Git will receive the wildcard before our shell can interfere with it. Without quotes our shell will only execute the wildcard search within the current directory. Git will receive the list of files the shell found instead of the wildcard and it will not be able to add the files inside of the octofamily directory.

###### `remote repositories`

`remote repositories with github`

Great job! We've gone ahead and created a new empty GitHub repository for you to use with Try Git at [https://github.com/try-git/try_git.git](https://github.com/try-git/try_git.git). To push our local repo to the GitHub server we'll need to add a remote repository.

This command takes a remote name and a repository URL, which in your case is [https://github.com/try-git/try_git.git](https://github.com/try-git/try_git.git).

Go ahead and run git remote add with the options below:



```
git remote add origin https://github.com/try-git/try_git.git
```



`haha`git remote: Git doesn't care what you name your remotes, but it's typical to name your main one origin. It's also a good idea for your main repository to be on a remote server like GitHub in case your machine is lost at sea during a transatlantic boat cruise or crushed by three monkey statues during an earthquake.

`pushing remotely`

The push command tells Git where to put our commits when we're ready, and boy we're ready. So let's push our local changes to our origin repo (on GitHub).

The name of our remote is origin and the default local branch name is master. The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do. Go ahead and push it!



```
$ git push -u origin master
```



`pulling remotely`

Let's pretend some time has passed. We've invited other people to our github project who have pulled your changes, made their own commits, and pushed them.

We can check for changes on our GitHub repository and pull down any new changes by running:



```
$ git pull origin master
```



![Smaller icon](media/favicon.ico "Title here")`git checkout --<target>`

git reset did a great job of unstaging octodog.txt, but you'll notice that he's still there. He's just not staged anymore. It would be great if we could go back to how things were before octodog came around and ruined the party.

Files can be changed back to how they were at the last commit by using the command: git checkout -- . Go ahead and get rid of all the changes since the last commit for octocat.txt

`-a option`

If you happen to delete a file without using 'git rm' you'll find that you still have to 'git rm' the deleted files from the working tree. You can save this step by using the '-a' option on 'git commit', which auto removes deleted files with the commit. git commit -am "Delete stuff"

`Merge Conflicts`

Merge Conflicts can occur when changes are made to a file at the same time. A lot of people get really scared when a conflict happens, but fear not! They aren't that scary, you just need to decide which code to keep. Merge conflicts are beyond the scope of this course, but if you're interested in reading more, take a look the section of the [Pro Git book](http://git-scm.com/book) on [how conflicts are presented](http://git-scm.com/docs/git-merge#_how_conflicts_are_presented).

`Force delete`

What if you have been working on a feature branch and you decide you really don't want this feature anymore? You might decide to delete the branch since you're scrapping the idea. You'll notice that git branch -d bad_feature doesn't work. This is because -d won't let you delete something that hasn't been merged. You can either add the --force (-f) option or use -D which combines -d -f together into one command.

##### cool stuff

`The .git directory` On the left you'll notice a .git directory. It's usually hidden but we're showing it to you for convenience. If you click it you'll notice it has all sorts of directories and files inside it. You'll rarely ever need to do anything inside here but it's the guts of Git, where all the magic happens.

`hooks`

`git stash:` Sometimes when you go to pull you may have changes you don't want to commit just yet. One option you have, other than commiting, is to stash the changes. Use the command 'git stash' to stash your changes, and 'git stash apply' to re-apply your changes after your pull.

`HEAD` The HEAD is a pointer that holds your position within all your different commits. By default HEAD points to your most recent commit, so it can be used as a quick way to reference that commit without having to look up the SHA.

![Smaller icon](media/favicon.ico "Title here")`Pull request in Github` If you're hosting your repo on GitHub, you can do something called a pull request. A pull request allows the boss of the project to look through your changes and make comments before deciding to merge in the change. It's a really great feature that is used all the time for remote workers and open-source projects. Check out out the pull request help page for more information.

## question

How to revert to previous Git commit? For a rep I use only for myself, I dn't need to care the influence of moving back.



```
git reset --hard commitNumber
git push -f origin master
```



After this, both my local repository and remote repository in Github are reverted to precious commit with commitNumber.

`recover to last commit` git reset --hard master@{1} Detail with the problem "undo git pull"[Click Here!](http://stackoverflow.com/questions/1223354/undo-git-pull-how-to-bring-repos-to-old-state)

`merge two weird branches` [click1](http://stackoverflow.com/questions/161813/how-do-i-fix-merge-conflicts-in-git) [click2](http://stackoverflow.com/questions/9537392/git-fetch-remote-branch) [click3](http://stackoverflow.com/questions/1407638/git-merge-removing-files-i-want-to-keep)



