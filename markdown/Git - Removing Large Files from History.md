# Removing Large Files From Git Repos
It's not uncommon to accidentally (or intentionally) store oversized files in a [[Git]] repository. Once this change is made, it can be make working with the repo painfully slow, and the mistake can be difficult to reverse.

## Alter Commit History Using Rebase
- Find the commit hash of the last good state.
- Start an interactive rebase using  `git rebase -i <last-good-hash>`. This will open a `vi` editor, where you can modify the history between `HEAD` and `<last-good-hash>`.
- Each line represents a different commit. For all commits you wish to remove, replace `pick` with `drop` .

If your last good hash is `3a5403c`, and you want to remove the commit with hash `b0650c4`, you would want your rebase command would show something like this:

```
pick da875a3 cleanup
pick 770ce4a Helper fns
pick f3e2575 event fn
pick 068eda4 use helper fn
pick 31510d0 helper fns
pick 381a61e create package for helper fns
pick 0567e07 Cleanup
pick b5e2304 Hide KeepAlive()
drop b0650c4 Include bigfile.exe
pick 40a2464 Remove unminified js
pick 73ceecd parse xml struct
pick de1bcb2 parse xml
pick 2d3bb0a parse html
pick a301cac render html
pick 32038ca hydrate

# Rebase 3a5403c..32038ca onto 3a5403c (15 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# . create a merge commit using the original merge commit's
# . message (or the oneline, if no original merge commit was
# . specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
```

Save and Quit using `:wq` to apply your changes.

## Remove Dangling Objects
Even if particular files are deleted from your commit history, they may still be in use by your branch's [[Git - Reflog|reference log]]. Use the following commands to remove dangling files:

```
git reflog expire --expire=now --all
git repack -ad # Remove dangling objects from packfiles
git prune # Remove dangling loose objects
```


## Compress and Optimize the Git History
The `git gc` command will run a number of housekeeping tasks, including file compression and removing unreachable objects. It typically runs quite quickly, but we can enable aggressive cleanup using the command `git gc --aggressive --prune`.

