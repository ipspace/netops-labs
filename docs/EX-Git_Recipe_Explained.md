# Git Recipe Explained

Git is a complex tool, so most novices [try to cheat their way through](https://xkcd.com/1597/) with arcane recipes.

As it's always better to [understand what you're doing](http://blog.ipspace.net/2008/09/knowledge-or-recipes.html) instead of a [google-and-paste approach](http://blog.ipspace.net/2011/08/road-to-complex-designs-is-paved-with.html), let's analyze a pretty common one. Use it to [describe your network automation lab](EX-Build_Lab.md).

```
git init
```

Git tracks changes you make in a distributed, eventually consistent database implemented with many small files in the `.git` directory. **git init** initializes that database within the .git subdirectory of the current directory. Use it in an empty directory you plan to use for your project.

```
git remote add origin https://github.com/username/repository
```

Git can synchronize the local database with multiple remote databases (repositories). Remote repositories are added with the **git remote add** command that [takes at least two arguments](https://git-scm.com/docs/git-remote):

-   The nickname of the remote repository;
-   The URI to access the remote repository.

!!! Warning
    The remote repository must exist before you run the **git remote add** command. For example, you must create a GitHub repository first, then do **git remote add** in an empty folder where you executed **git init**.

!!! Tip
    * The URI **git** uses to access a remote repository can use non-HTTP(S) methods, such as SSH.
    * All recipes call the remote repository **origin** (the default value), but you can give it any descriptive name, for example **git remote add github _url_**.

```
git branch -M main
```

In the old days, the initial Git branch was called the **master** branch. The Politically Correct movement forced numerous Git-based platforms to change the name of the initial branch to **main**. While I don't care how that branch is called, the **git** CLI tool does not necessarily share that sentiment, leaving you with an inconsistent branch naming scheme.

If you need to rename the local branch, use the **git branch -M _new_name_** command. For example, the above command accommodates a remote Git platform that insists on naming its most initial branch **main**.

```
echo "# netops-labs" >> README.md  # or windows equivalent
```

They wanted to say *make the changes you want to make*, but that would be too obvious.

```
git add some_file.text    # or 'git add .' for all
```

**git add** adds a snapshot of the specified files to the [*staging area*](http://softwareengineering.stackexchange.com/questions/119782/what-does-stage-mean-in-git) (prepares them for commit). If needed, remove the files from the staging area (**git status** will tell you how) or replace them with newer versions with another **git add** command without modifying **git** repositories.

!!! Tip
    To see which files have been modified (or haven't been added to the git database yet), use the **git status** command.

```
git commit -m 'a comment'
```

**git commit** saves (commits) the changes from the staging area to the local repository. You can specify the commit message in the –m parameter or use a text editor to write a longer message.

```
git push -u origin main
```

**git push** synchronizes the changes made in the local repository with a remote repository. Git keeps a mapping between local branches and remote branches so that you can use **git push** with no extra parameters to push changes to the remote repository. However, when you push changes for the first time, you have to specify the remote repository (**origin**) and remote branch (**main**), and tell Git that you want to create a new local-to-remote mapping with the `-u` or `--set-upstream` parameter.
