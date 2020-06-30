You can also specify -v, which shows you the URL that Git has stored for the shortname to be
expanded to:

```
$ git remote -v
```



| origin  origin | git://github.com/schacon/ticgit.git (fetch) git://github.com/schacon/ticgit.git (push) |
| -------------- | ------------------------------------------------------------ |
|                |                                                              |

37
Chapter 2 Git Basics Scott Chacon Pro Git
If you have more than one remote, the command lists them all. For example, my Grit repository
looks something like this.

```
$ cd grit
$ git remote -v
bakkdoor git://github.com/bakkdoor/grit.git
cho45 git://github.com/cho45/grit.git
defunkt git://github.com/defunkt/grit.git
koke git://github.com/koke/grit.git
origin git@github.com:mojombo/grit.git
```

I’ve mentioned and given some demonstrations of adding remote repositories in previous sections, but here is how to do it explicitly. To add a new remote Git repository as a shortname you
can reference easily, run git remote add [shortname] [url]:

Now you can use the string pb on the command line in lieu of the whole URL. For example, if
you want to fetch all the information that Paul has but that you don’t yet have in your repository,
you can run git fetch pb:

```
$ git remote
origin
$ git remote add pb git://github.com/paulboone/ticgit.git
$ git remote -v
origin git://github.com/schacon/ticgit.git
pb git://github.com/paulboone/ticgit.git
```

Now you can use the string pb on the command line in lieu of the whole URL. For example, if
you want to fetch all the information that Paul has but that you don’t yet have in your repository,
you can run git fetch pb:

Paul’s master branch is accessible locally as pb/master — you can merge it into one of your
branches, or you can check out a local branch at that point if you want to inspect it.  

```
$ git fetch pb
remote: Counting objects: 58, done.
remote: Compressing objects: 100% (41/41), done.
remote: Total 44 (delta 24), reused 1 (delta 0)
Unpacking objects: 100% (44/44), done.
From git://github.com/paulboone/ticgit
\* [new branch] master -> pb/master
\* [new branch] ticgit -> pb/ticgit
```

Paul’s master branch is accessible locally as pb/master — you can merge it into one of your
branches, or you can check out a local branch at that point if you want to inspect it.  



# Fetching and Pulling from Your Remotes

As you just saw, to get data from your remote projects, you can run:

```
$ git fetch [remote-name]
```

The command goes out to that remote project and pulls down all the data from that remote
project that you don’t have yet. After you do this, you should have references to all the branches
from that remote, which you can merge in or inspect at any time. (We’ll go over what branches are
and how to use them in much more detail in Chapter 3.)
If you clone a repository, the command automatically adds that remote repository under the
name origin. So, git fetch origin fetches any new work that has been pushed to that server
since you cloned (or last fetched from) it. It’s important to note that the fetch command pulls the
data to your local repository — it doesn’t automatically merge it with any of your work or modify
what you’re currently working on. You have to merge it manually into your work when you’re
ready.
If you have a branch set up to track a remote branch (see the next section and Chapter 3 for
more information), you can use the git pull command to automatically fetch and then merge a
remote branch into your current branch. This may be an easier or more comfortable workflow for
you; and by default, the git clone command automatically sets up your local master branch to
track the remote master branch on the server you cloned from (assuming the remote has a master
branch). Running git pull generally fetches data from the server you originally cloned from and
automatically tries to merge it into the code you’re currently working on  