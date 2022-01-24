---
title: Branches
teaching: 20
exercises: 0
questions:
- "What are branches?"
- "How can I work in parallel using branches?"
objectives:
- "Understand why branches are useful for:"
- "*working on separate tasks in the same repository concurrently*"
- "*trying multiple solutions to a problem*"
- "*check-pointing versions of code*"
- "Merge branches back into the main branch"
keypoints:
- "Branches can be useful for developing while keeping the primary work untouched."
---

So far we've always been working in a straight timeline.
However, there are times when we might want to keep
our primary work safe from experimental changes we are working on.
To do this we can use branches to work on separate tasks in parallel
without changing our current branch, `main`.

We didn't see it before but the first branch made is called `main`.
This is the default branch created when initializing a repository and
is often considered to be the "clean" or "working" version of a
repository's code.

We can see what branches exist in a repository by typing

~~~
$ git branch
~~~
{: .bash}

~~~
* main
~~~
{: .output}


The '*' indicates which branch we are currently on.

In this lesson, Dracula is trying to run an analysis
and doesn't know if it will be faster in bash or python.
To keep his main branch safe he will use separate branches
for both bash and python analysis.
Then he will merge the branch with the faster script
into his main branch.

First let's make the python branch.
We use the same `git branch` command but now add the 
name we want to give our new branch

~~~
$ git branch pythondev
~~~
{: .bash}

We can now check our work with the `git branch` command.

~~~
$ git branch
~~~
{: .bash}

~~~
* main
  pythondev
~~~
{: .output}

We can see that we created the `pythondev` branch but we
are still in the main branch.

We can also see this in the output of the `git status` command.

~~~
$ git status
~~~
{: .bash}

~~~
On branch main
nothing to commit, working directory clean
~~~
{: .output}

To switch to our new branch we can use the `checkout` command
we learned earlier and check our work with `git branch`.

~~~
$ git checkout pythondev
$ git branch
~~~
{: .bash}

~~~
  main
* pythondev
~~~
{: .output}

Before we used the `checkout` command to checkout a file from a specific commit
using commit hashes or `HEAD` and the filename (`git checkout HEAD <file>`). The
`checkout` command can also be used to checkout an entire previous version of the
repository, updating all files in the repository to match the state of a desired commit.

Branches allow us to do this using a human-readable name rather than memorizing
a commit hash. This name also typically gives purpose to the set of changes in
that branch. When we use the command `git checkout <branch_name>`, we are using
a nickname to checkout a version of the repository that matches the most recent
commit in that branch (a.k.a. the HEAD of that branch).

Here you can use `git log` and `ls` to see that the history and 
files are the same as our `main` branch. This will be true until
some changes are committed to our new branch.

Now lets make our python script.  
For simplicity sake, we will `touch` the script making an empty file
but imagine we spent hours working on this python script for our analysis.

~~~
$ touch analysis.py
~~~
{: .bash}

Now we can add and commit the script to our branch.

~~~
$ git add analysis.py
$ git commit -m "Wrote and tested python analysis script"
~~~
{: .bash}

~~~
[pythondev x792csa1] Wrote and tested python analysis script
 1 file changed, 1 insertion(+)
 create mode 100644 analysis.py
~~~
{: .output}

Lets check our work!

~~~
$ ls
$ git log --oneline
~~~
{: .bash}

As expected, we see our commit in the log.

Now let's switch back to the `main` branch.

~~~
$ git checkout main
$ git branch
~~~
{: .bash}

~~~
* main
  pythondev
~~~
{: .output}

Let's explore the repository a bit.

Now that we've confirmed we are on the `main` branch again.
Let's confirm that `analysis.py` and our last commit aren't in `main`.

~~~
$ ls
$ git log --oneline
~~~
{: .bash}

We no longer see the file `analysis.py` and our latest commit doesn't
appear in this branch's history. But do not fear! All of our hard work
remains in the `pythondev` branch. We can confirm this by moving back
to that branch.

~~~
$ git checkout pythondev
$ git branch
~~~
{: .bash}

~~~
  main
* pythondev
~~~
{: .output}

~~~
$ ls
$ git log --oneline
~~~
{: .bash}

And we see that our `analysis.py` file and respective commit have been
preserved in the `pythondev` branch.

Now we can repeat the process for our bash script in a branch called
`bashdev`.

First we must checkout the `main` branch again. New branches will
include the entire history up to the current commit, and we'd like
to keep these two tasks separate.

~~~
$ git checkout main
$ git branch
~~~
{: .bash}

~~~
* main
  pythondev
~~~
{: .output}

This time let's create and switch two the `bashdev` branch
in one command.

We can do so by adding the `-b` flag to checkout.

~~~
$ git checkout -b bashdev
$ git branch
~~~
{: .bash}

~~~
* bashdev
  main
  pythonndev
~~~
{: .output}


We can use `ls` and `git log` to see that this branch is 
the same as our current `main` branch.

Now we can make `analysis.sh` and add and commit it.
Again imagine instead of `touch`ing the file we worked 
on it for many hours.

~~~
$ touch analysis.sh
$ git add analysis.sh
$ git commit –m “Wrote and tested bash analysis script”
~~~
{: .bash}

~~~
[bashdev 2n779ds] Wrote and tested bash analysis script
 1 file changed, 1 insertion(+)
 create mode 100644 analysis.sh
~~~
{: .output}

Lets check our work again before we switch back to the main branch.
~~~
$ ls
$ git log --oneline
~~~
{: .bash}

So it turns out the python `analysis.py` is much faster than `analysis.sh`.

Let's merge this version into our `main` branch so we can use it for
our work going forward.

Merging brings the changes from a different branch into 
the current branch.

First we must switch to the branch we're merging changes into, `main`.

~~~
$ git checkout main
$ git branch
~~~
{: .bash}

~~~
  bashdev
* main
  pythonndev
~~~
{: .output}

Now we can `merge` the `pythondev` branch into our current branch
(`main`). In english, this command could be stated as "`git`, please
`merge` the changes in the `pythondev` branch into the current branch
I'm in".

~~~
$ git merge pythondev
~~~
{: .bash}

~~~
Updating 12687f6..x792csa1
Fast-forward
 analysis.py | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 analysis.py
~~~
{: .output}

Now that we've merged the `pythondev` into `main`, these changes
exist in both branches. This could be confusing in the future if we
stumble upon the `pythondev` branch again.

We can delete our old branches so as to avoid this confusion later.
We can do so by adding the `-d` flag to the `git branch` command.

~~~
git branch -d pythondev
~~~
{: .bash}

~~~
Deleted branch pythondev (was x792csa1).
~~~
{: .output}

And because we don't want to keep the changes in the `bashdev` branch,
we can delete the `bashdev` branch as well
~~~
$ git branch -d bashdev
~~~
{: .bash}

~~~
error: The branch 'bashdev' is not fully merged.
If you are sure you want to delete it, run 'git branch -D bashdev'.
~~~
{: .output}

Since we've never merged the changes from the `bashdev` branch,
git warns us about deleting them and tells us to use the `-D` flag instead.

Since we really want to delete this branch we will go ahead and do so.

~~~
git branch -D bashdev
~~~
{: .bash}

~~~
Deleted branch bashdev (was 2n779ds).
~~~
{: .output}
