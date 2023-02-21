# First Steps with Git

## Setup

Before we start using Git, we will need to set it up. Open a terminal and type the following:

```bash
git config --global user.name "Your Name"
```

Like other commands, this one starts first with the program we want to call `git`. Git provides a list of commands that we can specify as a parameter. Here we specify `config`, which tells Git that we want to configure it. `config` in turn takes three more parameters here. First, we tell it that the setting we are specifying should be used for all our Git projects from here on out (`--global`). Then we tell the `config` command what setting we want to specify, namely `user.name`, which will hold our name. And lastly, we provide our name `"Your Name"`.

Once you've set your name, let's configure your email address. Make sure to use the same email address you used when you signed up with GitHub. GitHub will use your email address to identify you.

```bash
git config --global user.email "you@email.org"
```

Like most other command line programs, you can print the command help by typing:

```bash
git --help
```

## Setting up a new Project in Git

Let's start a new project. Go to a folder in your file system using the command line (e.g. your Desktop or home directory). Then create a new folder and change to that directory.

```bash
cd ~/Desktop
mkdir git-exercise
cd git-exercise
```

Remember, `cd` stands for "change directory" and moves you into another directory. `mkdir` creates a new directory.

This new folder `git-exercise` will keep all the files of our project. To tell Git that we want this directory to be version controlled by Git, we run the following command.

```bash
git init
```

Try running `ls` now. It should return nothing. If you run `ls -a`, however, to also see all hidden files, you will see that there is now a folder called `.git`. This folder contains all of Git's data regarding our project. All versions of our files will be stored in this folder. This means that if you delete the `.git` folder, all your version history will be lost (so don't do it unless you are absolutely sure that's what you want).

```bash
ls -a
# outputs:
# .	..	.git
```

Now, let's set up a branch to work on. *Branches* in Git are strands of possibly independent development. You can use branches to experiment with new features or if you collaborate with others and don't want to get into the way of each other. By default the main branch is called `master` branch. But it has become customary to call it `main` instead. We create our main branch by typing:

```bash
git checkout -b main
```

Git should tell you that your command succeeded with the message `Switched to a new branch 'main'`.

Now type `git status`. You should see the followin output (or a version of it).

```
# output for: git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

`git status` is your friend. Use it often! It will always tell you the status of your changes. Specifically, it tells you what branch you are working on, what has been changed, and what has been marked as to be included in your next version. `git status` will never change something. It'll just tell you what's currently going on.

Congratulations, using `git init`, you have created your first local Git repository.