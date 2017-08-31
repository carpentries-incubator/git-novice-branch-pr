---
title: Conflicts
teaching: 15
exercises: 0
questions:
- "What do I do when my changes conflict?"
objectives:
- "Explain what conflicts are and when they can occur."
- "Understand how to resolve conflicts resulting from a merge."
keypoints:
- "Conflicts occur when files are changed in the same place in two commits that are being merged."
- "The version control system does not allow one to overwrite changes blindly during a merge, but highlights conflicts so that they can be resolved."
---

If we are working on a piece of software on both our laptop and a
server in the lab, we could make different changes to each copy.
Version control helps us manage these [conflicts]({{ page.root}}/reference/#conflicts)
by giving us tools to [resolve]({{ page.root}}/reference/#resolve) overlapping changes.

To see how we can resolve conflicts, we must first create one.  The
file `mars.txt` currently looks like this in our `planets` repository:

~~~
$ cat mars.txt
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~
{: .output}

Let's create a new branch for discussing Mars' temperature and
checkout that branch.

~~~
$ git branch marsTemp
~~~
{: .bash}

But before we make changes related to Mars' temperature in the `marsTemp`
branch, let's add a line to Mars.txt here in the `master` branch.

~~~
$ nano mars.txt
$ cat mars.txt
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
I'll be able to get 40 extra minutes of beauty rest
~~~
{: .output}

and commit that change to the `master` branch

~~~
$ git add mars.txt
$ git commit -m "Add a line about the daylight on Mars."
~~~
{: .bash}

~~~
[master 5ae9631] Add a line about the daylight on Mars.
 1 file changed, 1 insertion(+)
~~~
{: .output}

We can then examine the commit history of the `master` branch.

~~~
$ git log --oneline
~~~
{: .bash}

~~~
5ae9631 Add a line about the daylight on Mars.
005937f Discuss concerns about Mars' climate for Mummy
34961b1 Add concerns about effects of Mars' moons on Wolfman
f22b25e Start notes on Mars as a base
~~~
{: .output}

Now that we've made our changes in the `master` branch, let's get to work on our comments about
the temperature in the `marsTemp` branch.

~~~
$ git checkout marsTemp
$ git branch
~~~
{: .bash}

~~~
* marsTemp
  master
~~~
{: .output}

Let's make a note in `mars.txt` about the temperature. Note that when we open
this file the line we added about the daylight on Mars will not be present as
that change is not part of this branch.

~~~
$ nano mars.txt
$ cat mars.txt
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
Yeti will appreciate the cold
~~~
{: .output}

Now let's commit this change to the `marsTemp` branch

~~~
$ git add mars.txt
$ git commit -m "Add a line about the temperature on Mars"
~~~
{: .bash}

~~~
[master 07ebc69] Add a line about the temperature on Mars
 1 file changed, 1 insertion(+)
~~~
{: .output}

Again, we can look at the history of this branch.

~~~
$ git log --oneline
~~~
{: .bash}

~~~
07ebc69 Add a line about the temperature on Mars
005937f Discuss concerns about Mars' climate for Mummy
34961b1 Add concerns about effects of Mars' moons on Wolfman
f22b25e Start notes on Mars as a base
~~~
{: .output}

> Notice that the commit related to Mars' daylight is not present as it is part of
> the `master` branch, not the `marsTemp` branch.
{: .callout}

Now that we've added changes about the temperature
we can merge them into the `master` branch. First, let's checkout the
`master` branch.

~~~
$ git checkout master
$ git branch
~~~
{: .bash}

~~~
  marsTemp
* master
~~~
{: .output}

And then merge the changes from `marsTemp` into our current branch, `master`.

~~~
$ git merge marsTemp
~~~
{: .bash}

~~~
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

  both modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")

~~~
{: .output}

![The Conflicting Changes](../fig/conflict.svg)

Git detects that the changes made in one copy overlap with those made
in the other and stops us from trampling on our previous work. It also
marks that conflict in the affected file:

~~~
$ cat mars.txt
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
<<<<<<< HEAD
I'll be able to get 40 extra minutes of beauty rest
=======
Yeti will appreciate the cold
>>>>>>> 07ebc69c450e8475aee9b14b4383acc99f42af1d
~~~
{: .output}

Our change—the one at the `HEAD` of the `master` branch—is preceded by `<<<<<<<`.
Git has then inserted `=======` as a separator between the conflicting changes
and marked the end of our commit from the `marsTemp` branch with `>>>>>>>`.
(The string of letters and digits after that marker
identifies the commit we made in the `marsTemp` branch.)

It is now up to us to edit this file to remove these markers
and reconcile the changes.
We can do anything we want: keep the change made in the `master` branch, keep
the change made in the `marsTemp` branch, write something new to replace both,
or get rid of the change entirely.

Let's replace both of the comments about Mar's daylight and the temperature
along with the conflict identifiers so that the file looks like this:

~~~
$ nano mars.txt
$ cat mars.txt
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
We removed the conflict on this line
~~~
{: .output}

To finish merging,
we add `mars.txt` to the changes being made by the merge
and then commit:

~~~
$ git add mars.txt
$ git status
~~~
{: .bash}

~~~
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   mars.txt

~~~
{: .output}

~~~
$ git commit -m "Merge changes from marsTemp"
~~~
{: .bash}

~~~
[master 2abf2b1] Merge changes from marsTemp
~~~
{: .output}

Git keeps track of what we've merged with what,
so we don't have to fix things by hand again.

Let's make another change to the `marsTemp` branch:

~~~
$ git checkout marsTemp
$ echo "The polar caps will probably be Yeti's home" >> mars.txt
$ git add mars.txt
$ git commit -m "A note about Yeti's home"
~~~
{: .bash}

~~~
[master 34avo82] A note about Yeti's home
 1 file changed, 1 insertion(+)
~~~
{: .output}

And merge that change into master

~~~
$ git checkout master
$ git merge marsTemp
~~~

~~~
Updating 12687f6..x792csa1
Fast-forward
 mars.txt | 1 +
 1 file changed, 1 insertions(+), 0 deletions(-)
~~~
{: .output}

There is no conflict and our changes are added automatically

~~~
$ cat mars.txt
~~~
{: .bash}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
We removed the conflict on this line
The polar caps will probably be Yeti's home
~~~
{: .output}

We don't need to merge again because Git knows someone has already done that.

Git's ability to resolve conflicts is very useful, but conflict resolution
costs time and effort, and can introduce errors if conflicts are not resolved
correctly. If you find yourself resolving a lot of conflicts in a project,
consider one of these approaches to reducing them:

- Try breaking large files apart into smaller files so that it is less
  likely that you will be working in the same file at the same time
  in different branches
- Create branches focused on separable tasks so that your work won't overlap in files

> ## Create a conflict between branches and resolve it
>
> - Create a new branch off of the master branch
> - Make a change to a file in the master branch
> - Change to the new branch
> - Make a change to the same line in the same file
> - Change back to the master branch
> - Merge the new branch into the master branch
> - Address the resulting conflict in the text editor of your choice
> - Add the file containing the conflict and commit conflict resolution to the repository
>
> > ## Solution
> >
> > ~~~
> > # to make sure we're starting in the master branch
> > $ git checkout master 
> > # create a new branch, but don't change into it
> > $ git branch new_branch 
> > # make a change to the file
> > $ nano mars.txt 
> > # add changes in mars.txt to the staging area
> > $ git add mars.txt 
> > $ git commit -m "Small change to mars.txt"
> > # switch to the new branch
> > $ git checkout new_branch 
> > # make a change to mars.txt on the same line
> > $ nano mars.txt 
> > # add changes in mars.txt to the staging area
> > $ git add mars.txt 
> > $ git commit -m "Another change to mars.txt"
> > # change back to the master branch
> > $ git checkout master 
> > # attempt to merge the branches
> > $ git merge new_branch 
> > # address conflicts by removing `<<<`, `===`, and `>>>` lines leaving the desired changes intact
> > $ nano mars.txt
> > $ git add mars.txt
> > $ git commit -m "Resolving conflict in mars.txt."
> > ~~~
> > {: .bash}
> {: .solution}
{: .challenge}