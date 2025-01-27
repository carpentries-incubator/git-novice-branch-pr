---
title: Pull Requests
teaching: 60
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Define the terms fork, clone, origin, remote, upstream
- Understand how to make a pull request and what they are useful for

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What are pull requests for?
- How can I make a pull request?

::::::::::::::::::::::::::::::::::::::::::::::::::

Pull requests are a great way to collaborate with others using github.
Instead of making changes directly to a repository you can suggest changes to a repo.
This can be useful if you don't have permission to modify a repository directly or
you want someone else to review your changes.

For this lesson we will be working on the `countries` repository together.
Open the github link for the `countries` repo provided by the instructor
in your browser window.

![](fig/github_screenshot_upstream_repo.png)

:::::::::::::::::::::::::::::::::::::::::  callout

## Repo owner differences

You may have noticed that the `countries` repo in this lesson's pictures
is owned by the 'McMahonLab' organization and this doesn't match
the address you were given.
This is to be expected because this will differ depending on
what organization your instructor used to setup the `countries` repo.

You will also see your username where the 'sstevens2' is in the pictures.

::::::::::::::::::::::::::::::::::::::::::::::::::

Once at the `countries` repo, click the **Fork** button which can be found
in the upper right hand conner of the window.
Forking the repository makes us each our own copy of the repo in our github
account which we can edit.

![](fig/github_screenshot_upstream_forking.png)

Next we need to get this repo on our local computer and
setup connections from our computer to both our forked version
and the authoritative version we forked it from.

First we will **clone** the repo from our forked version.
The clone command does two things:

1. Copies the repo to your local computer
2. Sets up a remote called 'origin' between your computer and the github repo

Copy the web address for your forked version of repo
(from the web address line or click 'Clone and download' and copy that).

![](fig/github_screenshot_cloneOrigin.png)

In terminal or Gitbash, navigate to a folder you'd like to hold this repo,
we will place it on our `Desktop`.
Once there you can use the `clone` command with the link you copied as the first argument.

```bash
$ cd ~/Desktop
$ git clone https://github.com/USERNAME/countries.git
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Why does the command above say 'USERNAME'?

So that we can't copy the command above and accidentally clone someone else's
version of countries to our computer, the command above uses the placeholder
'USERNAME' where you should put your own username if your copied from above
instead of copying the link from your browser and pasting it into the command.

::::::::::::::::::::::::::::::::::::::::::::::::::

```output
Cloning into 'countries'...
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), done.
```

Next we will set up a connection or **remote** to the authoritative repository
(the original version given to you by your instructor).
In your browser, you can go back this repo by clicking on the link that says 'forked from'
in the upper left hand corner, under your username and repo name.

Copy the web address for this repo
(from the web address line or click the 'clone and download' and copy that).

![](fig/github_screenshot_upstream_repo.png)

Then back in your terminal, navigate into the cloned repo and add the remote
connection to this repository.
For this command we must give the remote a different nickname,
where our original remote is 'origin'
this new remote will be called 'upstream'.
You could give it a different nickname but 'upstream' is a common nickname for
the authoritative repository.

```bash
$ cd countries
$ git remote add upstream https://github.com/INSTRUCTOR-GIVEN/countries.git
```

:::::::::::::::::::::::::::::::::::::::::  callout

## If you tried copying the command above...

You will have to replace 'INSTRUCTOR-GIVEN' with the site your instructor
indicated at the beginning of this lesson. This will vary depending
on how your instructor set up for this lesson.

::::::::::::::::::::::::::::::::::::::::::::::::::

At anytime you can see the remote connections your repo has using the following command:

```bash
$ git remote -v
```

```output
origin	https://github.com/USERNAME/countries.git (fetch)
origin	https://github.com/USERNAME/countries.git (push)
upstream	https://github.com/INSTRUCTOR-GIVEN/countries.git (fetch)
upstream	https://github.com/INSTRUCTOR-GIVEN/countries.git (push)
```

Now that we have this setup done we will be able to suggest
changes to this repo using a pull request.
Each person will add a new file with info about a new country in it.

The instructor will now add a single file to the repository containing
information about the the United States.

Next, we will update our local version of the repo to include the new file.
We use a command called `pull` to bring these changes to our local repository.
We must specify the remote and branch we want to pull from, in this case the
`upstream` remote's `main` branch.

```bash
$ git pull upstream main
```

Now your local version of the repo is updated but our forked version of the
repo is not yet up to date.
You can reload your fork in github and see it does not contain the new
`united_states.txt` file.
Now we need to update our forked version.
To do so we can `push` the changes in our local version to the main branch of our fork,
called 'origin'.

```bash
$ git push origin main
```

Now let's each add a new country to the repository.
First let's make a new branch to work on.  This will keep our 'main' version
in sync with the authoritative version of the repository.
We can name our branch descriptively after the country we will be adding.
Mine will be `addFrance` since I'll be working with France.
Please pick a different country and shout it out (or add it to the etherpad)
so no one else chooses the same one.
We will create the branch and switch into in one step
as we learned earlier in the branching lesson.

```bash
$ git checkout -b addFrance
```

```output
Switched to a new branch 'addFrance'
```

Finally before we proceed to adding the new file, we will double
check that we are on the right branch.

```bash
$ git branch
```

```output
* addFrance
  main
```

Next we will copy `united_states.txt` and change the name to the name of our chosen country.
Then we can use nano to edit the contents to reflect the info of your chosen country.  
Hint: You may need to do some internet searching to fill in the information.

```bash
$ cp united_states.txt france.txt
$ nano france.txt
$ cat france.txt
```

```output
Population: 66,991,000
Capital: Paris
```

Next let's add and commit the changes to the repo.

```bash
$ git add france.txt
$ git commit -m "Added file on france"
```

```output
[addFrance 79a312a] Added file on france
 1 file changed, 2 insertions(+), 2 deletions(-)
```

In some cases we may not have permission to push changes directly to the
upstream/authoritative repo or we might like our changes to be reviewed regardless
of permissions, so we'll create a `pull request`.
A `pull request` is a **request** for a member of the upstream repository to **pull**
our changes into the upstream repository from a `fork`, allowing them to request further
changes/improvements and make comments on the changes before doing so.
In order to create a `pull request`, we must push our new branch containing the
changes we'd like to submit to the remote linked to our fork, `origin`, on GitHub.

```bash
$ git push origin addFrance
```

```output
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 783 bytes | 0 bytes/s, done.
Total 4 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To https://github.com/USERNAME/countries.git
   2037539..79a312a  addFrance -> addFrance
```

Next go to your forked github version of the repo and reload the page.
You won't see the new file added in the list of files but you will see
that you recently pushed a new branch to the repository.

![](fig/github_screenshot_origin_master_addFrance.png)

If you wish to view your new branch you can click on the 'Branch' drop down menu
and select that branch.

![](fig/github_screenshot_switch_github_branch.png)

Then you should be able to view the files and commits in that branch.

![](fig/github_screenshot_origin_master_addFrance.png)

Github already suspects that we are going to want to make a pull request so we can click
the 'Compare \& pull request' button to start a new pull request.

![](fig/github_screenshot_makingPR1.png)

The base fork should be the upstream/authoritative version's main branch and then
the head fork should be the new branch of our fork.
You can add more information into the comment section if there is anything you'd like
to add for the person who reviews your suggestion.
Then you can click the 'create pull request button' to submit the pull request.

![](fig/github_screenshot_makingPR2.png)

Now someone with privileges to the upstream repo can review it, give comments and
suggestions, and merge it into the upstream version.
In our pull request they can see any messages we left or click and look at the commits that were made and see the files changed.

Our collaborator reviewing the pull request noticed that
we forgot to add the largest city so let's add it and update our pull request.

```bash
$ nano france.txt
$ cat france.txt
```

```output
Population: 66,991,000
Capital: Paris
Largest City: Paris
```

Next we will add and commit these changes.
Then we can push them to our fork of the repo.

```bash
$ git add france.txt
$ git commit -m "Added largest city to france file"
$ git push origin addFrance
```

```output
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 387 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/USERNAME/countries.git
   31aa2e3..609acfe  addFrance -> addFrance
```

If we reload the pull request, we'll see that the new commit was added to the
pull request and the changes have been automatically updated.
New commits pushed to the same branch are included in the previous pull request.
If you want to suggest changes separately you need to make separate branches but
if you want the changes to be considered together you should put them in the same branch.

![](fig/github_screenshot_after_new_commit.png)

When working with others we might encounter the conflicts, which we
learned about earlier in branches.  Let's practice resolving conflicts when working
collaboratively.

We will continue to work in the `addFrance` branch from before and check we are
in that branch before we start.

```bash
$ git branch
```

```output
* addFrance
  main
```

Next we will each add our country to the existing `README.md` file in the repository in the line directly following the `Countries:` line.

```bash
$ nano README.md
$ cat README.md
```

```output
# countries
Sandbox for learning PR's in Software Carpentry workshop

Countries:
France
```

Next we need to add, commit, and push these requests to our existing pull request.

```bash
$ git add README.md
$ git commit -m "Added France to list of countries in README"
```

```output
[addFrance 66d7ebf] Added France to list of countries in README
 1 file changed, 1 insertions(+), 1 deletions(-)
```

```bash
$ git push origin addFrance
```

```output
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 376 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/USERNAME/countries.git
   609acfe..66d7ebf  addFrance -> addFrance
```

Now if we reload the page we had a pull request we notice that our `addFrance`
branch is conflicting with upstream's `main` branch.
This is because someone else edited the same line of the `README.md` file by
adding 'United States' where we added 'France'.

![](fig/github_screenshot_conflicting_PR.png)

In this case, it is possible to resolve this conflict in github by
clicking the 'Resolve Conflicts' button.
However, we will reuse the skills we learned earlier to resolve this conflict locally,
as we did in our branching conflict.

First we need to pull down the changes from upstream's `main` branch into our
`addFrance` branch.

```bash
$ git pull upstream main
```

```output
From https://github.com/McMahonLab/countries
 * branch            main     -> FETCH_HEAD
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

From the conflict error message we can see the conflict is in `README.md` or by running `git status` and seeing the 'both modified' status.

```bash
$ git status
```

```output
On branch addFrance
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Now we will resolve the conflict by editing the `README.md` file to contain both
'United States' and 'France' and none of the additional lines git added to
indicate conflict

```bash
$ nano README.md
$ cat README.md
```

```output
# countries
Sandbox for ComBEE github workshop on PR's

Countries:
France
United States
```

Then we add and commit our resolved conflict.

```bash
$ git add README.md
$ git commit -m "Resolved conflict in readme w two countries"
```

```output
[addFrance 912317b] Resolved conflict in readme w two countries
```

Finally we can update the pull request by pushing these changes to our github
fork of the repository.

```bash
$ git push origin addFrance
```

```output
git push origin addFrance
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 732 bytes | 0 bytes/s, done.
Total 6 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To https://github.com/USERNAME/countries.git
   66d7ebf..912317b  addFrance -> addFrance
```

Now if we reload our browser we will see that the new commit is in the pull
request and it has no conflicts with the base branch.

![](fig/github_screenshot_resolved_PR_conflict.png)

Now the owner/administrator/manager of the authoritative repo can review our pull requests and decide to incorporate them.

:::::::::::::::::::::::::::::::::::::::  challenge

## Add new country file and make additional PR

- Starting in the main branch make a new branch
- Copy other country file into a new country
- Edit the file to include info on the new country
- Add and commit this new file
- Push the new changes to github

:::::::::::::::  solution

## Solution

```bash
$ git checkout main
$ git checkout -b addItaly
$ cp united_states.txt italy.txt
$ nano italy.txt #Add the right info into the file
$ git add italy.txt
$ git commit -m "Added file on Italy"
$ git push origin addItaly
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Pull requests suggest changes to repos where you don't have privileges

::::::::::::::::::::::::::::::::::::::::::::::::::


