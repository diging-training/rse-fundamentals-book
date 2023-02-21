# Local Git Exercises

1. Create a new folder and initialize a Git repository. Then add a file called `bio.txt` that contains a one paragraph about yourself. Stage the file and commit it. Use `git log` to show your commit history. Take a screenshot of the log.

1. Add a second file called `project.txt` and add one paragraph description of one of your projects (if you don't have a project at the moment, you can use an old one or a short summary of a homework). Make a change to the `bio.txt` file. Add and commit your changes. Use `git log` to show the commit history and take screenshot of the log.

1. Get the commit id of your last commit. Then type `git checkout <commit id> bio.txt` (e.g. `git checkout 0954ee152 bio.txt `). Now run `git status`. What does `git status` print? What did the checkout command do here? (Hint: check the `bio.txt` file)

1. Think about your last project/homework/paper. How could you have used Git? How would it have benefitted your project/homework/paper? 

```{note}
<code>git checkout</code> has other uses as well. You will not see the same behavior if you don't provide a file name. If you run `git checkout 0954ee152`, you'll probably see a message like this:


    Note: switching to '0954ee152'.

    You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by switching back to a branch.

    If you want to create a new branch to retain commits you create, you may do so (now or later) by using -c with the switch command. Example:

    git switch -c <new-branch-name>

    Or undo this operation with:

     git switch -

    Turn off this advice by setting config variable advice.detachedHead to false

    HEAD is now at 0954ee1 Added another line.

While this may sound scary, don't worry, you didn't break anything. Just type `git checkout main` to get back to your project.
```

