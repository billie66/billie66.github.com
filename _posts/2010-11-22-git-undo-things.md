---
layout: post
---

Last night, I messed up my blog repository which including a useless file. I
really wanted to delete the last commit, So I googled to find a git command to
settle this problem. Though google I not only removed the bad commit, but also
I learned several basic git commands to undo changes that you'd made.

There is a saying that an old pencil is better than a good brain. This was the
second time I met the problem again and I did not want to spend time on it, so
I took a note of it in case of forgetting the method.

Now, I will use an example to explain how to use these basic tools for undoing
something.

## create a repo

     $ mkdir test
     $ cd test/
     $ git init
     Initialized empty Git repository in /home/billie/test/.git/
     $ touch cat
     $ git add cat
     $ git commit -m "initial"

## discard changes in working directory

If you want to discard all changes about a file, you can use [_git checkout_]
[1], for example: 

    $ cat cat
    $ echo "a lovely cat" > cat
    $ cat cat
    a lovely cat
    $ git status
    # On branch master
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #   modified:   cat
    #
    no changes added to commit (use "git add" and/or "git commit -a")
    $ git checkout -- cat
    $ cat cat 
    $ 
[1]: http://www.kernel.org/pub/software/scm/git/docs/git-checkout.html 

If you want to keep the same content with the last commit, undo everything that 
you have made recently in working tree. You can use [_git reset_] [2].

    $ cat dog 
    a nice dog
    $ echo "its colour is black" >> cat
    $ git add .
    $ git status 
    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #   modified:   cat
    #   new file:   dog
    #
    $ git reset HEAD 
    Unstaged changes after reset:
    M   cat
    $ git status 
    # On branch master
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #   modified:   cat
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #   dog
    no changes added to commit (use "git add" and/or "git commit -a")
    $ git add .
    $ git reset --hard HEAD 
    HEAD is now at d59f8eb initial
    $ ls
    cat
    $ cat cat 
    $ 
[2]: http://www.kernel.org/pub/software/scm/git/docs/git-reset.html

## delete the last commit 

If you commited some stuff, but you realize that you did something wrong and
want to delete the last commit. How to settle this? Use _git reset_ again.

    $ touch dog 
    $ echo "a lovely cat" > cat
    $ cat cat 
    a lovely cat
    $ git add .
    $ git commit -m " add a new file"
    [master d5c7bc3]  add a new file
    1 files changed, 1 insertions(+), 0 deletions(-)
    create mode 100644 dog
    $ tig
    $ git reset --hard HEAD~1
    HEAD is now at d59f8eb initial
    $ tig
    $ ls
    cat
    $ cat cat 
    $  

_HEAD~1_ is a shorthand for the commit before head. If you want to keep all
the changes but delete the commit, you can use _--soft_ optin instead of
_--hard_.

Note: If you already pushed a repo and someone pulled it, then you cann't delete the
bad commit. So you can use _git revert_ to fix up your mistakes. _git revert_
will create a new commit that revert an exsiting commit.

The following example will show you how to use _git revert_ to revert the most
recent commit.

    $ echo "a lovely cat" > cat
    $ git revert HEAD
    fatal: Cannot revert a root commit
    $ git add .
    $ git commit -m " add a line in cat"
    [master 8dd70d4]  add a line in cat
    1 files changed, 1 insertions(+), 0 deletions(-)
    $ git revert HEAD
    Finished one revert.
    [master 933b4a1] restore
    1 files changed, 0 insertions(+), 1 deletions(-)
    $ ls
    cat
    $ tig   // there are three commits.
    $ cat cat 
    $ 

A good link about this topic [git community book] [3]
[3]: http://book.git-scm.com/4_undoing_in_git_-_reset,_checkout_and_revert.html
