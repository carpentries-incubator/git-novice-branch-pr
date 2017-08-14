---
title: Branches
teaching: 20
exercises: 0
questions:
- "What are branches?"
- "How can I work in parallel using branches?"
objectives:
- "Explain why branches can be useful."
- "Use branches for working in parallel"
- "Merge branches back into the master"
keypoints:
- "Branches can be useful for developing while keeping the main line static."
---

So far we've always been working in a straight timeline.
However, there are times when we might want to keep
our main work safe from experimental changes we are working on.
To do this we can use branches to work in parallel from our main branch.

We didn't see it before the the first branch made is called `master`.
We can see the existing branches by typing 

~~~
$ git branch
~~~
{: .bash}

~~~
* master
~~~
{: .output}


The '*' indicates which branch we are currently on.

In this lesson, Dracula is trying to run an analysis
and doesn't know if it will be faster in bash or python.
To keep his master branch safe he will do separate branch
for both bash and python analysis.
Then he will merge the branch with the faster script
into his master branch.

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
* master
  pythondev
~~~
{: .output}

We can see that we created the `pythondev` branch but we
are still in the master branch.
To switch to our new branch we can use the `checkout` command
we learned earlier and check our work with `git branch`.

~~~
$ git checkout pythondev
$ git branch
~~~
{: .bash}

~~~
  master
* pythondev
~~~
{: .output}


Here you can use `git log` and `ls` to see that the history and 
files are the same as our `master` branch.  
Note: They will only match the `master` branch up until 
the new branch was made from it.
New changed in the `master` branch would not be added to `pythondev`
or vice versa, unless explicitly merged.

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


Now let's switch back to the `master` branch and confirm that
it is unchanged.

~~~
$ git checkout master
$ git branch
~~~
{: .bash}

~~~
* master
  pythondev
~~~
{: .output}

Now that we've confirmed we are on the `master` branch again.
Let's confirm that `analysis.py` and our last commit aren't in `master`.

~~~
$ ls
$ git log --oneline
~~~
{: .bash}


Now we can repeat the process with the `bashdev` branch.
This time lets create and switch two the `bashdev` branch
in one command.
We can do so by adding the `-b` flag to checkout.

~~~
$ git branch -b bashdev
$ git branch
~~~
{: .bash}

~~~
* bashdev
  master
  pythonndev
~~~
{: .output}


We can use `ls` and `git log` to see that this branch is 
the same as our current `master` branch.

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

Lets check our work again before we switch back to the master branch.
~~~
$ ls
$ git log --oneline
~~~
{: .bash}

So it turns out the python `analysis.py` is much faster than `analysis.sh`.

Let's merge this version into our `master` branch to move
forward with.
Merging brings the changes from a different branch into 
the current branch.

In order to move this branch into `master` we must first switch
to the `master` branch.

~~~
$ git checkout master
$ git branch
~~~
{: .bash}

~~~
  bashdev
* master
  pythonndev
~~~
{: .output}

Now we can `merge` the `pythondev` branch into our current branch (`master`).

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


Now that we've merged the `pythondev` branch.
We can delete our old branches so we don't get confused about them later.
We can do so by adding the `-d` flag to the `git branch` command.

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

Now we can delete the `pythondev` branch as well

~~~
git branch -d pythondev
~~~
{: .bash}

~~~
Deleted branch pythondev (was x792csa1).
~~~
{: .output}


