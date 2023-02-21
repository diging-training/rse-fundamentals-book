# Saving Changes

Let's create some files and save some versions! In your `git-exercise` folder, create a new file. You can do that however you like. You can use your File Explorer/Finder or use `touch` or a command line editor. It doesn't matter as long as there is a new file in your folder. Let's call the file `chapter.txt`. Once you have created a new file, use `git status` to see the status of your git project. You should see something like this:

```bash
# output for: git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	chapter.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Git tells us that there is a new file that has not been added to Git yet. Git, helpful as it is, tells us how to add the file. If we add a file to Git, we tell Git that the file should be included in the next snapshot. So, that's what we will do. And then let's check the status agian.

```bash
git add chapter.txt
git status
```

You should see something like this now:

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   chapter.txt
```

Now you see that Git will include our file `chapter.txt` into the next commit, which is the next version we will save. To *commit* something means to save it in a new version and *a commit* is a version or snapshot of our project.

Let's tell Git to create a new commit. Type the following.

```bash
git commit -m "Added the first chapter."
```

This command tells Git to create a new version. Every commit has a commit message. A commit message describes what has been changed in a commit. In our case, we've added the first chapter. Writing commit messages is an art rather than a science. It should be short but descriptive. The first 50 characters are usually shown when looking at a list of commits, and they ideally should answer the question what will happen if the changes in the commit are applied. 

Now that we have a first commit, we can look at the commit history (the version history) of our project. Type `git log`. You should see something like this:

```bash
commit 5d88a1359c2fef002ed14a6aa20e531626c0ef45 (HEAD -> main)
Author: Julia Damerow <jdamerow@asu.edu>
Date:   Sun Feb 19 16:44:22 2023 -0500

    Added the first chapter.
```

Git log shows you who created a new version (a new commit), when, the message describing the commit, and a unique commit id. This id (which is typically shortened to the first 7 characters) is used when referring to a commit (e.g. if you need to revert changes).

Let's create another commit. Make a change to `chapter.txt`. `git status` will now tell you that you modified the file.

```bash
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   chapter.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Like before, use `git add` to add the changes you made to the next version and then use  `git commit` to create a new version. `git log` will now show you both commits.

```
commit 0954ee152c76a3475cd1196a800bdd465d92bb18 (HEAD -> main)
Author: Julia Damerow <jdamerow@asu.edu>
Date:   Sun Feb 19 16:53:38 2023 -0500

    Added another line.

commit 5d88a1359c2fef002ed14a6aa20e531626c0ef45
Author: Julia Damerow <jdamerow@asu.edu>
Date:   Sun Feb 19 16:44:22 2023 -0500

    Added the first chapter.
```

## Reverting Changes

Let's assume we realize, the last change we made was not right and we want to revert it. You can simply tell Git that you want to revert the change. To do that find the commit id of the change you want to undo and copy the first 7 characters (you can also copy the whole id if you want).

```bash
git revert 0954ee1
```

Once you hit enter, Git will open your default editor and ask you to edit the commit message. By default it will simply say "Revert <the message of the commit to be reverted>". Change the message if you want.Then save and close the editor. Now type `git log` again. You should see three commits now. The last one reverting the previous one.

```
commit ffd7f606ba0416d77c99c0153d679d9aaa057203 (HEAD -> main)
Author: Julia Damerow <jdamerow@asu.edu>
Date:   Sun Feb 19 16:58:35 2023 -0500

    Revert "Added another line."
    
    This reverts commit 0954ee152c76a3475cd1196a800bdd465d92bb18.

commit 0954ee152c76a3475cd1196a800bdd465d92bb18
Author: Julia Damerow <jdamerow@asu.edu>
Date:   Sun Feb 19 16:53:38 2023 -0500

    Added another line.

commit 5d88a1359c2fef002ed14a6aa20e531626c0ef45
Author: Julia Damerow <jdamerow@asu.edu>
Date:   Sun Feb 19 16:44:22 2023 -0500

    Added the first chapter.
```

If you open `chapter.txt` you should see the first version of the file before you changed it.


