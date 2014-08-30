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

### create a repo

{% highlight bash %}
$ git init
Initialized empty Git repository in /home/billie/test/.git/
{% endhighlight %}

### discard changes in working directory

If you want to discard all changes on the file named cat, you can 
use [_git checkout_][1],
for example:

{% highlight bash %}
$ git checkout -- cat
{% endhighlight %}

If you want to keep the same content with the last commit, undo everything that 
you have made recently in working tree. You can use [_git reset_][2].

{% highlight bash %}
$ git reset --hard HEAD 
{% endhighlight %}

### delete the last commit 

If you commited some stuff, but you realize that you did something wrong and
want to delete the last commit. How to settle this? Use _git reset_ again.

{% highlight bash %}
$ git reset --hard HEAD~1
{% endhighlight %}

_HEAD~1_ is a shorthand for the commit before head. If you want to keep all
the changes but delete the commit, you can use `--soft` option instead of
`--hard`.

Note: If you already pushed a repo and someone pulled it, then you cann't delete the
bad commit. So you can use [_git revert_][3] to fix up your mistakes. _git revert_
will create a new commit that revert an exsiting commit.

The following example will show you how to use _git revert_ to revert the most
recent commit.

{% highlight bash %}
$ git revert HEAD^1
{% endhighlight %}

There is a good book about git:

[Pro Git][4]

[1]: http://www.kernel.org/pub/software/scm/git/docs/git-checkout.html
[2]: http://www.kernel.org/pub/software/scm/git/docs/git-reset.html
[3]: http://www.kernel.org/pub/software/scm/git/docs/git-revert.html
[4]: http://book.git-scm.com/
