Software Carpentry Workshop: Lesson6: Introduction to Git and Github
===

SWC workshop, February 22
Instructor: Peace
Time: 1.5 hours

This lesson is a modified version of [Software Carpentry Git Lesson](http://swcarpentry.github.io/git-novice/) and part of the UTA [Software Carpentry workshop] (https://annawilliford.github.io/2018-02-24-UTA/)

Additional resources:
[tutorials](https://www.atlassian.com/git/tutorials)
[pull requests](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)

## 1. What is Git/GitHub and why you would want to use it

Does this look familiar?

![](https://github.com/AnnaWilliford/2017-11-11-UTA/raw/gh-pages/workshop/images/Final.png)

**Git**
Git is a version control software. It is used to track changes in documents on your local machine. All file versions and revision history are saved to a folder known as **repository**.

Version control systems start with a base version of the document and then save just the changes you made at each step of the way. You can think of it as a tape: if you rewind the tape and start at the base document, then you can play back each change and end up with your latest version.

![](http://swcarpentry.github.io/git-novice/fig/play-changes.svg)

Once you think of changes as separate from the document itself, you can then think about “playing back” different sets of changes onto the base document and getting different versions of the document. For example, two users can make independent sets of changes based on the same document.

![](http://swcarpentry.github.io/git-novice/fig/versions.svg)

Unless there are conflicts, you can combine two sets of changes onto the same base document.

![](http://swcarpentry.github.io/git-novice/fig/merge.svg)

**Github** is a cloud service that hosts repositories, it is a central hub to hold all our local repositories. Github has additional functionality that enables efficient collaboration.


![](https://github.com/AnnaWilliford/2017-11-11-UTA/raw/gh-pages/workshop/images/github_bigPicture.png)

As you can see, there are many ways users can interact with remote repositories. The main advantage here is to have access to repositories other than your own, a framework that promotes collaboration. Before exploring Github, let's understand how to make reposotories and track files on your local machines.

## 2. Setting up Git

Git should be already installed on your machines. If you are on Windows, Git came with your gitbash installation. If you are on Mac, Git has been preinstalled on your system.


When we use Git on a new computer for the first time, we need to configure a few things. Below are a few examples of configurations we will set as we get started with Git:

- our name and email address,
- to colorize our output,
- what our preferred text editor is,
- and that we want to use these settings globally (i.e. for every project)

On a command line, Git commands are written as `git verb`, where `verb` is what we actually want to do. 
```shell
$ git config --global user.name "Your username"
$ git config --global user.email "Your email" 
$ git config --global color.ui "auto"

#add a text editor of your choice 
#Mac: Text Wrangler
$ git config --global core.editor "edit -w"

#Windows: notepad
$ git config --global core.editor "notepad"

#Windows: notepad++
$ git config --global core.editor "C:/Program Files (x86)/Notepad++/notepad++.exe"

#Linux
$ git config --global core.editor "gedit --wait --new-window"
```
The four commands we just ran above only need to be run once: the flag --global tells Git to use the settings for every project, in your user account, on this computer.

You can check your settings at any time:
```shell
$ git config --list
```
`git config` command has other options. You can get help with this and other git commands by typing
```shell
$ "YourCommand" -h
$ git config -h
$ git config --help
```
So far we have only used `git config` command, but there are many more. You can get an idea about the functionality of Git by taking a look at the available commands.
```shell
$ git
```
We will explore some of them next.

## 3. Track your documents with Git

We are now ready to use Git.
To start with, let's make a new folder `git_test` on your Desktop, outside `SWC_fall2017` directory.

Suppose you started working on your thesis. You create a folder `Thesis` inside `git_test` . 
```shell
#go to git_test
cd git_test

#make folder
$ mkdir Thesis

#go into Thesis folder
$ cd Thesis

#check Thesis contents
$ ls -a 
./  ../ 
```
At this point we have the expected output. Let's make a new file in this folder, say a file for thesis notes.
```shell
$ echo "Chapeter 1 notes" > notes.txt

$ ls -a
./  ../  notes.txt

$ cat notes.txt
```
We can ask now if our new file, `notes.txt` is being tracked. We can do this with `git status` command
```shell
$ git status
fatal: Not a git repository (or any of the parent directories): .git
```
This message means that `Thesis` folder is not under the control of Git, none of the documents within this folder are being tracked.

To place a folder under Git control, we need to initialize out `Thesis` folder.

```shell
#check that you are in Thesis
$ pwd

#initialize Thesis directory with Git
$ git init
Initialized empty Git repository in ...

#check content
$ ls -a
./  ../  .git/  notes.txt
```
The folder that contains .git directory is called ***repository***

Let's try `git status` command now.
```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```
You can see that initializing a directory makes it visible to Git. Now Git tells us what files are in the directory and what is their status. In our case, Git says that there is notes.txt file and it is not tracked. Git also tells us that we need to use `git add` command to start tracking this file.
```
$ git add notes.txt

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   notes.txt
```
The current version of `notes.txt` is now ready (or staged) to be recorded by Git. To record the current version of notes.txt, `git commit` command is used
```
#commit changes
$ git commit -m "first note"

[master (root-commit) 851e745] first note
 1 file changed, 1 insertion(+)
 create mode 100644 notes.txt
```
When we run `git commit`, Git takes everything we have told it to save by using `git add` and stores a copy permanently inside the special `.git` directory. This permanent copy is called a **commit** (or revision) and its short identifier is 851e745 (Your commit may have another identifier.)

We use the -m flag (for “message”) to record a short, descriptive, and specific comment that will help us remember later on what we did and why. If we just run `git commit` without the -m option, Git will launch nano (or whatever other editor we configured as core.editor) so that we can write a longer message.

Good commit messages start with a brief (<50 characters) summary of changes made in the commit. If you want to go into more detail, add a blank line between the summary line and your additional notes.

Now run `git status` again. 
```
#check satus
$ git status
On branch master
nothing to commit, working tree clean
```
Everything is up to date!

You can check the history of your commits:
```
$ git log

commit 851e745b2d4c72541cce750ba1d19d6b3d59ee6a
Author: AnnaWilliford <awillifo@uta>
Date:   Thu Nov 2 13:29:28 2017 -0500

    first note 
    
#or for a faster view
$ git log --oneline
```
In summary, here are the steps that must be completed to track changes in your documents with Git.

- [x] Initialize your folder with `git init` command. This is done only **one** time for every new parent directory
- [x] Prepare new/modified files for saving(committing) with `git add` command
- [x] Create a permanent copy of your new/modified file with `git commit -m "message" `


![](http://swcarpentry.github.io/git-novice/fig/git-staging-area.svg)



 **Challenge 3.1:**
```
 Open notes.txt in text editor and add a line of text to it. 
 Save your changes and track your changes with Git.
```
>**Solution**
>
> Open note.txt, add text, save and close.
> You can see your new note.txt with 
> $ cat notes.txt
> 
> Chapter 1 notes
> Chapter 2 notes

> $ git status
> On branch master
> Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
>
>    modified:   notes.txt
>
>no changes added to commit (use "git add" and/or "git commit -a")
>
> $ git add notes.txt
> $ git commit -m "added chapter2 notes"

Now, run `git log`.  The output of `git log` tells you the history of your changes. Your commit messages are very important, in case you want to restore an old version of the document, they will help you to pick out the version you want.

Your versions (or commits) have unique identifiers. In addition, the most recent version can be identified by `HEAD`. You can see differences betwee any 2 versions by using `git diff` command:
```shell
#you can specify only first few characters of the commit identifier.
$ git diff 851e745b2 HEAD notes.txt
```
 
Now, let's see how to turn an existing directory into git repository. You might want to track files for some of your existing projects. Maybe for `SWC_fall2017` directory? How will you place this directory under Git control?

```
#Go to SWC_fall2017
$ cd ~/Desktop/SWC_fall2017

#initialize
$ git init

#check status
$ git status

#prepare files for tracking
$ git add .

#commit changes 
$ git commit -m "added SWC_fall2017 directory"

#check commit history
$ git log
```
Now every file in this directory is being tracked.

Notice that we added multiple folders and files in the same commit. If you want to know what files were included in this commit:
```
# print the list of files that are part of a given commit
$ git show --name-only 1e228d70f
```
As you continue working on this project, you will be adding new directories and files to it.
Let's try it.

**Challenge 3.2**
```
Make a new directory `git_github` in `SWC_fall2017`. 
Make a file called git_steps.txt inside `git_github`. 
Record `git` commands you must use to start tracking your changes.
Save this file and commit `git_github` directory to Git.

NOTE:`git init` should only be run one time in the root directory of your project. 
```
 
## 4. Accessing older versions

The clear advantage of tracking your documents with Git is that you can always go back to the previous version. Let's see how this works.

The output of `git log` provides all the information you need to retrieve the older version of the document.

In our case, we do not have multiple versions of the same document, so let's modify our git_steps.txt and add a note to it:

```
$ echo "Use git init only one time for every project" >>git_steps.txt

$ cat git_steps.txt

$ git add .
$ git commit -m "added note to git_steps.txt"

#view latest version
$ cat git_steps.txt
```

Now, this is our second version of git_steps.txt. Our first version was stored when we first created the file, and our second version when we added a new line to it.

Suppose that some time later, you want the original version of git_steps.txt. How would you do that?

To restore any of the original versions of the document, you use `git checkout` command:
```
#general syntax
$ git checkout <commitID> <file>
```

If we want the original git_steps.txt:
```
#see what commitID is associated with the original version
git log --oneline

#the commit that includes original file has message "added git_github directory" (or whatever you used when you committed the change)
$ git checkout ad91ea0aab git_steps.txt
```

Now let's make sure that we have original version of git_steps.txt
```
#view restored version
$ cat git_steps.txt

#restored version has not been committed, see HEAD commit
$ git log

#see what to do next
$ git status

#If you decide to go ahead with restoring file, commit the change since checkout command places file in the staging area (no need for 'git add')

$ git commit -m "changed to the original git_steps.txt version"

$ git status

#see HEAD now
$ git log

#if you run `git checkout, but would like to cancel restoring the old version:
#unstage restored file
$ git reset HEAD git_steps.txt 

#return to latest version before you attempted to restore the file
$ git checkout -- git_steps.txt

#see current file
$ cat git_steps.txt
```

## 5. Tracking Microsoft Word documents

This part of the lesson has been modified from this [source](http://blog.martinfenner.org/2014/08/25/using-microsoft-word-with-git/)

Initially, git was designed to track changes to software source code. The functionality of Git is now greatly expanded and you can track various file formats, including documents written in Microsoft Word. But first, you need to convert word documents to plain text and let Git know that Pandoc is the tool you use to do it.
- Install [pandoc](https://github.com/jgm/pandoc/releases/tag/2.0.1.1) for you system.

- Create a new file, `.gitattributes` in your git project folder
```
#add this line to .gitattributes
*.docx diff=pandoc
```
- Open `.gitconfig` file in your home directory
```
#add these lines to .gitconfig 

[diff "pandoc"]
  textconv=pandoc --to=markdown
  prompt = false
[alias]
  wdiff = diff --word-diff=color --unified=1
  ```
 The last command sets alias for `diff` command to `wdiff`. You can now use `git wdiff` to see changes between versions by word and not by line.

## 6. GitHub: share your repository with the world

So far, our work was restricted to the local machine. But if you want to share your repositories with your colleagues, it would be nice to have a central place where everyone could make their repositories available for comments/suggestions/collaborations. Github is a service that allows us to do that. 

If you have not created Github account, please go to github.com and do it now. 

Now we want to create repository that will be a remote copy of our local `SWC_fall2017` repository. 
```
#from your github account:
Click on 'new repository'
Repository name: 'SWC_fall2017'
Type: public
Click on 'create repository'
```
You have just created remote empty `SWC_fall2017` repository. This repository has a specific identifier URL associated with it. We now let our local machine know that we have a remote location for our local repository.
```
#on your local machine
$ git remote add origin URL
```
The name origin is a local nickname for your remote repository. We could use something else if we wanted to, but origin is by far the most common choice.

Once the nickname origin is set up, this command will push the changes from our local repository to the repository on GitHub:
```
$ git push -u origin master
```
This is it! You just made your local 'SWC_fall2017' repository available on Github to everyone. You are now in position to share your work and collaborate with others. How cool is this?

---


![](https://github.com/AnnaWilliford/2017-11-11-UTA/raw/gh-pages/workshop/images/Git_push.png)

---

**Challenge 6.1**
```
Suppose you want to add another file to your repository. 
Download command history file for R_into lesson from yesterday and 
add it to your local directory and then push it to Github.

https://www.dropbox.com/s/hifr9hn3y2v7sy6/R_commands.R?dl=0

```


## 7. Working with and/or contributing to someone else's projects


![](https://github.com/AnnaWilliford/2017-11-11-UTA/raw/gh-pages/workshop/images/Github_fork.png)

---

![](https://github.com/AnnaWilliford/2017-11-11-UTA/raw/gh-pages/workshop/images/Github_pullRequest.png)

---

This part of the lesson is modified from this [Source](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)

You can contribute to whatever project you like. Suppose you would like to add a new feature to someone else's project. You can always propose your changes - in Github language this is known as  `pull request`.

Steps for making pull requests (or PRs):

- go to the project you want to contribute to
  (https://github.com/AnnaWilliford/SWC_fall2017_lessons)

- copy the project to your Github account by clicking `fork` button on the top right corner of the page

You should now have a new repository called `SWC_fall2017_lessons` in **YOUR** account. This is great, you can copy other projects/repositories to your Github account!

You can also copy remote repository to the local machine, say to the Desktop. From your local terminal, type:
```
$ git clone https://github.com/YourUsername/SWC_fall2017_lessons.git ~/Desktop/SWC_fall2017_lessons.git
```
You now have all lessons from this workshop both on your Github account and on your local machine!

See, you have access to any public repository on Github in a similar way.

Now, what is even better, you can contribute to the project you forked/cloned(copied) by suggesting changes to the documents in the repository. If, for example, you find a better way to explain some topic we were covering in this workshop, you can make changes to the lessons locally on your machine and then send a `pull request` to the owner of repository. The owner will review your changes and decide to accept(merge) proposed changes or reject them.

Want to try?
Go to `SWC_fall2017_lessons` repo on your local machine and open a new topic branch for the project:
```
$ git checkout -b YourName
```
You can now modify and add anything you want in this project. When ready with your final contributions, you will be able to send your pull request.

For example, add your create new file, say "R_intro_NewChallenge"
```
#create new file
$ git add .
$ git commit -m "add new file"

#Push your topic branch up to your fork:
$ git push origin YourName
```
Go to the forked repo on your GitHub account and click on the green `compare & pull request` button

A bit more terminology here: 
`base fork` is the repository you'd like to merge changes into. Use the `base branch` drop-down menu to select the branch of the upstream repository you'd like to merge changes into.

Use the `head fork` drop-down menu to select your fork, then use the compare branch drop-down menu to select the branch you made your changes in.

Type a title and description for your pull request.

Click `Create pull request`

The owner of repository will get notification about pull request and will review your proposed changes.

## 8. Direct Collaboration on Github

![](https://github.com/AnnaWilliford/2017-11-11-UTA/raw/gh-pages/workshop/images/Github_collaborate.png)


Now you try to collaborate with each other and one of you with me.

To add collaborators to our project:
On your github account under repository you want to collaborate, go to:
seetings-> add collaborator
Wait for Collaborator to accept invitation. The invitation comes as notification - you can read it by clicking a bell icon in the top right corner of the Github page.

Next, the Collaborator needs to download a copy of the Owner’s repository to her machine. This is called “cloning a repo”. To clone the Owner’s repo into her Desktop folder, the Collaborator enters:
```
$ git clone https://github.com/username/repositoryName.git ~/Desktop/repositoryName
```
The Collaborator can now make a change in her clone of the Owner’s repository, exactly the same way as we’ve been doing before:

```
#in ~/Desktop/repositoryName
#add new file to the project
$ echo "comments" > Comments.txt
$ git status
$ git add .
$ git commit -m "added Comments.txt file"
```
Then push the change to the **Owner’s** repository on GitHub:
```
$ git push -u origin master
```
Note that we didn’t have to create a remote called origin: Git uses this name by default when we clone a repository. You can check the URL associated with `origin`
```
$ git config --get remote.origin.url
```
Take a look at the Owner’s repository on GitHub website now (maybe you need to refresh your browser.) You should be able to see the new commit made by the Collaborator.

To download the Collaborator’s changes from GitHub, the Owner now enters:
```
$ git pull origin master
```
In practice, it is good to be sure that you have an updated version of the repository you are collaborating on, so you should `git pull` before making our changes. The basic collaborative workflow would be:

- update your local repo with git pull origin master,
- make your changes and stage them with git add,
- commit your changes with git commit -m, and
- upload the changes to GitHub with git push origin master

It is better to make many commits with smaller changes rather than of one commit with massive changes: small commits are easier to read and review.
