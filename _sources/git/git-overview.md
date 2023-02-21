# How Git Works

You can find instructions on how to install Git [here](https://carpentries.github.io/workshop-template/#git).

Because we'll want to collaborate on our code, you will also need to [create an account in GitHub](https://github.com/signup). There are other service providers besides GitHub (e.g. [GitLab](https://gitlab.com/)) but for the lessons here, we will use GitHub.

The way Git works is that creating a new version, a new snapshot of your files, is a two step process. After you have edited some files, you first tell Git which changes should be part of the next snapshot. Once that is done, you tell Git to create a new snapshot, a new version. The folder in your file system where you keep your files are called the *working directory* or *working tree*. When you tell Git which changes you want to include in the next version, you *stage* them. The *index* keeps track of what changes you want to include in the next version. To create a new version you *commit* the *staged* changes to the *repository*.

```{image} ./imgs/wd-staging-repo.png
:width: 400px
:align: center
```

