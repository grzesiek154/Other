# Git Three stages 

![image-20210106152549141](/home/grzesiek/.config/Typora/typora-user-images/image-20210106152549141.png)

## A quick note on syntax

- `[]`: Optional content
- `<>`: Should be replaced by the actual value when running the command

# Check Out Remote Branches

We’re probably all familiar with `git pull` to bring our local branches up to speed with their remote counterparts. However, if this is our first time working with the remote branch —  i.e., it isn’t being tracked by any branch in our local repository — we  first need to set that up.

**Note:** It’s a good idea to run `git fetch `to make sure we’re working with the most up to date version of `remote`.

- **Command:** `git checkout [-b <new-local-branch-name>] -t <remote>/<branch>`
- **Example:** `git checkout -t origin/my-awesome-feature`
- **Explanation:** This will pull `origin/my-awesome-feature` into a new local branch of the same name and set it up to track `origin/my-awesome-feature`. `-b` will do the same thing, except that the local branch’s name will be set to the one specified.

**Resources**

- [“How do I check out a remote Git branch?” | Stack Overflow](https://stackoverflow.com/a/1783426/4348037)

# Delete Remote Branches

Deleting a local branch is as simple as writing `git branch -d <branch>`. But a different command is needed to delete remote branches.

- **Command:**`git push <remote> -d <branch>` or `git push <remote> :<branch>`
- **Example:** `git push origin :my-awesome-feature`

Resources

- [“How do I delete a Git branch locally and remotely?” | Stack Overflow](https://stackoverflow.com/a/2003515/4348037)

# Change Remote URL

This is for whenever you need to change the URL `<remote>` actually points to. For example, if you change your repository’s name, Git will ask you to do this. Here’s how.

- **Command:** `git remote set-url <remote> <newurl>`
- **Example:** `git remote set-url origin github.com/myusername/my-repo`

Resources

- [git-remote | Git](https://git-scm.com/docs/git-remote)

# Stash Individual Files

`git stash` is used frequently to momentarily set aside all uncommitted changes and reset the branch to the most recent commit. But what if you only want to stash specific files?

- **Command:** `git stash push -- <filepath(s)>`
- **Example:** `git stash push -- src/index.js README.md`

Resources

- [“Stash only one file out of multiple files that have changed with Git?” | Stack Overflow](https://stackoverflow.com/questions/3040833/stash-only-one-file-out-of-multiple-files-that-have-changed-with-git#comment78345399_3040833)

# Show Content of Most Recent Stash

This one’s useful if you’d like to view the changes a stash would apply before applying them.

- **Command:** `git stash show -p [stash@{<n>}]`
- **Explanation: 
  **`-p` says that we want to see the actual content of the stash. Omitting it will show only the file names.
  `stash@{<n>}` allows us to specify a certain stash, denoted by `n` (0 being the most recent one).
- **Example:** `git stash show -p stash@{1}`
- **Effect:** shows the content of the second latest stash

Resources

- [“See what’s in a stash without applying it” | Stash Overflow](https://stackoverflow.com/a/10726185/4348037)
- [git-stash | Git](https://git-scm.com/docs/git-stash#Documentation/git-stash.txt-ltstashgt)

# Apply a Stash Without Deleting It From the Stash List

Speaking of applying stashes, `git stash pop` is usually the go-to command for this and, which will apply the first stash on the stash list (viewed with `git stash list`). The side effect, though, is that the stash is removed from the list in  the process. But if you’d like to keep it, Git has you covered.

- **Command:** `git stash apply`
- **Effect:** Applies the first stash on the list without removing it
- **Tip:** Just as with `git stash show`, you can specify which stash to apply by appending `stash@{<n>}`

Resources

- [git-stash | Git](https://git-scm.com/docs/git-stash#Documentation/git-stash.txt-apply--index-q--quietltstashgt)

# Check Out File From Another Branch

`git checkout <branch>` is no stranger to most Git users. It does exactly what it says, in that it, well, checks out a specific branch. But if needed, the very same  command can also be used to check out a single file.

- **Command:** `git checkout <branch> -- <path(s)>`
- **Example:** `git checkout my-awesome-feature src/lasers.js`
- **Effect:** Checks out `src/lasers.js` from `my-awesome-feature`
- **Tip:** You may also be familiar with `git checkout <commit>`. This variant can be used in the same way to check out a file from a specific commit rather than a specific branch.

Resources

- [“Git tip: How to ‘merge’ specific files from another branch](https://jasonrudolph.com/blog/2009/02/25/git-tip-how-to-merge-specific-files-from-another-branch/)”

# Work With Multiple Branches Simultaneously

If you find yourself often having to checkout a specific branch, for  example to use as a reference while working on another branch, `git worktree` offers a better alternative.

- **Command:** `git worktree add <path> <branch>` 
  And when you no longer need it, run: 
  `git worktree remove [-f] <path>`
- **Example: 
  **1.`git worktree add my-other-awesome-feature ../my-other-awesome-feature`
  \2. `git worktree remove ../my-other-awesome-feature`
- **Explanation:** Creates a [linked working tree](https://git-scm.com/docs/git-worktree#_description) (i.e., another directory on the file system associated with the repo) called `my-other-awesome-feature`, one level above your current working directory, with the specified branch checked out. 
  You could then, for example, open this directory in another code editor  instance or open individual files from it in the current instance.
  Once you’re done with the linked working tree, removing it with 
  `-f` will force-remove working trees with uncommitted changes.

Resources

- [“git working on two branches simultaneously” | Stack Overflow](https://stackoverflow.com/a/30186843/4348037)
- [git-worktree | Git](https://git-scm.com/docs/git-worktree)

# Show Commit Content

Somewhat similar to `git stash show`, it’s often useful to see the changes introduced by a specific commit.

- **Command:** `git show <commit>`
  Alternatively, to see the changes between two specific commits run
   `git diff <commit-a> <commit-b>`
- **Example:** `git diff HEAD~ HEAD`
- **Effect:** Shows the difference between `HEAD` and its immediate ancestor, which is equivalent to `git show`

Resources

- [“How to see the changes in a Git commit?” | Stack Overflow](https://stackoverflow.com/questions/17563726/how-to-see-the-changes-in-a-git-commit/)
- [“Commits are snapshots, not diffs” | The GitHub Blog](https://github.blog/2020-12-17-commits-are-snapshots-not-diffs)
- [git-log | Git](https://git-scm.com/docs/git-log)
- [“Git Basics — Viewing the Commit History” | Git](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

# Compare Files Between Branches/Commits

The power of `git diff` isn’t just exclusive to whole commits, as we just saw, but can be used to target individual files.

- **Command:** `git diff <commit-a> <commit-b> -- <path(s)>`
- **Example:** `git diff 0659bdc e6c7c0d -- src/flair.py`
- **Effect:** Shows how the file at one commit differs from the other. 
  Branch names can also be used here instead of commits to compare the file across branches.
- **Tip:** To compare different files, use 
  `git diff <commit-a>:<path-a> <commit-b>:<path-b>`

Resources

- [“How to compare files from two different branches?” | Stack Overflow](https://stackoverflow.com/questions/4099742/how-to-compare-files-from-two-different-branches)

# Reset a Single File to Most Recent Commit

`git reset --hard` is a godsend when you need to go back to the last stable state, for  example after some unwanted or unintended changes, but it affects the  whole working tree. The command to achieve the same effect but localized to a file should come as no stranger, though.

- **Command:** `git checkout [<commit>] -- <path(s)>`
- **Example:** `git checkout -- README.md`
- **Effect:** This will reset `README.md` to the version in the most recent commit (or a specific commit if one is specified)

Resources

- [“Hard reset of a single file” | Stack Overflow](https://stackoverflow.com/questions/7147270/hard-reset-of-a-single-file)

# Change Last Commit Message

Ever committed changes only to later want to edit the commit message?

- **Command:** `git commit --amend [-m '<message>']`
  If the old commit had already been pushed, you’ll need to additionally run
  `git push --force-with-lease <remote> <branch>`.``**Note:** As a general rule, and especially if you’re working with others, it’s  important to be careful when making any changes to already pushed  commits.
- **Effect:** Adds any staged changes to the last commit. If a message is included with the `-m` option, the last commit’s message is replaced. Otherwise, this opens the editor at the last commit message.
- **Tip:** As you can probably already tell, `git commit --amend` can be used to change more than just the commit’s message. For example, making changes and committing them with the `--amend` option will cause these changes to be added to the last commit rather than creating a new one.

Resources

- [git-commit | Git](https://stackoverflow.com/a/15772171/4348037)
- [“Changing git commit message after push (given that no one pulled from remote)” | Stack Overflow](https://stackoverflow.com/a/8981216/4348037)

# Change a Specific Commit Message

What about changing a specific commit message?

- **Command:** `git rebase -i <commit>`
- **Example (see demo below):** `git rebase -i HEAD~3`
- **Effect:** Opens an editor listing commits, starting from the one specified up to the  current one. In the example above, this list will be made up of the last three commits.
  Replacing `pick` with `reword` for those commits where you wish to change the message and saving will allow you to do just that. 
  **Note:** The actual changes are made in the next step. Changing the messages at this point will have no effect!

![Changing a specific commit message with Git Rebase](https://miro.medium.com/freeze/max/60/1*iZvhBr9v2EeQ_IYuAww7uw.gif?q=20)

![Changing a specific commit message with Git Rebase](https://miro.medium.com/max/1924/1*iZvhBr9v2EeQ_IYuAww7uw.gif)

Changing a specific commit message with Git Rebase

Resources

- [“Change old commit message on Git” | Stack Overflow](https://stackoverflow.com/questions/1884474/change-old-commit-message-on-git)

# Delete Last Commit but Keep the Changes

You’ve committed changes that you’d like to keep, but for whatever reason, you don’t want the commit itself. Fret not!

- **Command:** `git reset HEAD^`**Note:** The warning about making changes to already pushed commits holds here too!
- **Effect:** Moves `HEAD` to point to the previous commit without making any file changes, effectively removing the current commit
- **Tip:** An alternative to this approach is to wait till you’re ready for your next commit and instead of doing so with the usual `git commit`, using our old friend `git comment --amend`. This will have the same intended effect.

Resources

- [“Can I delete a git commit but keep the changes?” | Stack Overflow](https://stackoverflow.com/a/15772171/4348037)

# Unstage a File

What’s the opposite of `git add`? I’ll give you a hint. It’s not `git remove`.

- **Command:** `git reset HEAD <path>`
- **Effect:** Removes the given file from the index. This is useful for when you’re preparing your next commit and decide a file you’d previously staged with `git add` should no longer be part of it. This *doesn’t* affect the file itself. So you don’t have to worry about breaking anything.

Resources:

- [Unstage | GitLab](https://docs.gitlab.com/ee/university/training/topics/unstage.html)
- [“Git Tools — Reset Demystified” | Git](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified)

# Remove Ignored Files From Remote

If you’ve pushed files and later decided to `.gitignore` them, the files will nevertheless persist in your remote repository. To remedy this, `git rm` is the tool for the job.

- **Command:** `git rm [-r] [-n] --cached <path(s)>`.
  Then, simply `add`, `commit`, and `push`.
- **Explanation:** 
  `--cached` ensures the files remain in the working tree. 
  `-n` performs a dry run, essentially a sanity check that allows you to first see which files will be affected before actually executing the command. If you’re happy with the results, simply run the command again without  it. 
  `-r` is used in case folders are being removed to allow for recursive removal.
- **Example: 
  **(1) `git rm -r -n --cached .` (check files affected)
  (2) `git rm -r --cached .`
  (3) `git add .`
  (4) `git commit -m "Remove ignored files"`
  (5) `git push`
- **Effect:** This is an aggressive but useful form of the command. The result is that  your repo will be purged of any files contained in your `.gitignore` without you having to explicitly list every single one.

Resources

- [“How to make Git ‘forget’ about a file that was tracked but is now in .gitignore?” | Stack Overflow](https://stackoverflow.com/questions/1274057/how-to-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore)
- [“Untrack files already added to git repository based on .gitignore” | CodeBlocQ](https://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore)
- [“‘git rm --cached x’ vs ‘git reset head -- x’?” | Stack Overflow](https://stackoverflow.com/questions/5798930/git-rm-cached-x-vs-git-reset-head-x)

# Create GitHub Releases

Finally, here’s a gem I recently started using. This one’s not strictly a Git  command per se but one offered by the GitHub CLI. So you’ll first have  to [download](https://cli.github.com/) it if you haven’t already.

- **Command:** `gh release create <version>`
- **Example (see demo below):** `gh release create v0.3`
- **Effect:** This will open up an interactive command-line menu guiding you through  the process of creating your release. The result will be a GitHub  release created from the provided version [tag](https://git-scm.com/book/en/v2/Git-Basics-Tagging) (a new tag will be created if no such tag exists in your repo).

![Creating a GitHub release from the command line using the GitHub CLI](https://miro.medium.com/freeze/max/60/1*S0hB89j6uvEWjK0opVlwtg.gif?q=20)

![Creating a GitHub release from the command line using the GitHub CLI](https://miro.medium.com/max/1919/1*S0hB89j6uvEWjK0opVlwtg.gif)

Creating a GitHub release from the command line using the GitHub CLI

- **Tip:** At the `Release notes` prompt*,* choose `Write using commit log as template` to have a nice starting point for meaningful release notes. It’s a good idea to run `git fetch --all --tags` beforehand to ensure that only commits since the last tag are included in the template. 
  If an editor other than your default is opened, use `gh config set editor <editor>` to set it to one of your choosing — e.g., `gh config set editor nano`.

Here’s an example of release notes from a recent [release](https://github.com/osharaki/travel_regions/releases/tag/v0.3):

![Here’s an example of release notes from a recent release.](https://miro.medium.com/max/60/1*WUbSMMj8SIy-nfTyY8dfQA.png?q=20)

![Here’s an example of release notes from a recent release.](https://miro.medium.com/max/924/1*WUbSMMj8SIy-nfTyY8dfQA.png)

Resources

- [gh release create | GitHub CLI](https://cli.github.com/manual/gh_release_create)
- [gh config set | GitHub CLI](https://cli.github.com/manual/gh_config_set)



# Resolving merge conflicts

**Step 1**: Run following commands in your terminal

```
git config merge.tool vimdiff
git config merge.conflictstyle diff3
git config mergetool.prompt false
```

This will set vimdiff as the default merge tool.

**Step 2**: Run following command in terminal

```
git mergetool
```

**Step 3**: You will see a vimdiff display in following format

```
  ╔═══════╦══════╦════════╗
  ║       ║      ║        ║
  ║ LOCAL ║ BASE ║ REMOTE ║
  ║       ║      ║        ║
  ╠═══════╩══════╩════════╣
  ║                       ║
  ║        MERGED         ║
  ║                       ║
  ╚═══════════════════════╝
```

These 4 views are

> LOCAL – this is file from the current branch

> BASE – common ancestor, how file looked before both changes

> REMOTE – file you are merging into your branch

> MERGED – merge result, this is what gets saved in the repo

You can navigate among these views using ctrl+w. You can directly reach MERGED view using ctrl+w followed by j.

More info about vimdiff navigation [here](https://stackoverflow.com/questions/4556184/vim-move-window-left-right) and [here](https://stackoverflow.com/questions/27151456/how-do-i-jump-to-the-next-prev-diff-in-git-difftool)

**Step 4**. You could edit the MERGED view the following way

If you want to get changes from REMOTE

```
:diffg RE  
```

If you want to get changes from BASE

```
:diffg BA  
```

If you want to get changes from LOCAL

```
:diffg LO 
```

**Step 5**. Save, Exit, Commit and Clean up

`:wqa` save and exit from vi

```
git commit -m "message"
```

`git clean` Remove extra files (e.g. *.orig) created by diff tool.



Resources:

https://stackoverflow.com/questions/161813/how-to-resolve-merge-conflicts-in-git-repository