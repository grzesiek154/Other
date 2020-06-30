Remember that each file in your working directory can be in one of two states: tracked or
untracked. Tracked files are files that were in the last snapshot; they can be unmodified, modified,
or staged. Untracked files are everything else — any files in your working directory that were not
in your last snapshot and are not in your staging area. When you first clone a repository, all of
your files will be tracked and unmodified because you just checked them out and haven’t edited
anything.  

As you edit files, Git sees them as modified, because you’ve changed them since your last
commit. You stage these modified files and then commit all your staged changes, and the cycle
repeats. This lifecycle is illustrated in Figure 2-1.  

![The Git Lifecycle | Learn to Code in Boston with Launch Academy](https://git-scm.com/figures/18333fig0201-tn.png)