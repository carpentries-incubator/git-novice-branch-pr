---
title: Setting Up Git
teaching: 5
exercises: 0
questions:
- "How do I get set up to use Git?"
objectives:
- "Configure `git` the first time it is used on a computer."
- "Understand the meaning of the `--global` configuration flag."
keypoints:
-   "Use `git config` to configure a user name, email address, editor, and other preferences once per machine."
---

When we use Git on a new computer for the first time,
we need to configure a few things. Below are a few examples
of configurations we will set as we get started with Git:

*   our name and email address,
*   to colorize our output,
*   what our preferred text editor is,
*   and that we want to use these settings globally (i.e. for every project)

On a command line, Git commands are written as `git verb`,
where `verb` is what we actually want to do. So here is how
Dracula sets up his new laptop:

~~~
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
$ git config --global color.ui "auto"
~~~
{: .bash}

Please use your own name and email address instead of Dracula's. This user name and email will be associated with your subsequent Git activity,
which means that any changes pushed to
[GitHub](https://github.com/),
[BitBucket](https://bitbucket.org/),
[GitLab](https://gitlab.com/) or
another Git host server
in a later lesson will include this information.

> ## Line Endings
>
> As with other keys, when you hit the 'return' key on your keyboard, 
> your computer encodes this input. 
> For reasons that are long to explain, different operating systems
> use different character(s) to represent the end of a line. 
> (You may also hear these referred to as newlines or line breaks.)
> Because git uses these characters to compare files, 
> it may cause unexpected issues when editing a file on different machines. 
> 
> You can change the way git recognizes and encodes line endings
> using the `core.autocrlf` command to `git config`.
> The following settings are recommended:
>
> On OS X and Linux:
>
> ~~~
> $ git config --global core.autocrlf input
> ~~~
> {: .bash}
>
> And on Windows:
>
> ~~~
> $ git config --global core.autocrlf true
> ~~~
> {: .bash}
> 
> You can read more about this issue 
> [on this GitHub page](https://help.github.com/articles/dealing-with-line-endings/).
{: .callout}

For these lessons, we will be interacting with [GitHub](https://github.com/) and so the email address used should be the same as the one used when setting up your GitHub account. If you are concerned about privacy, please review [GitHub's instructions for keeping your email address private][git-privacy]. 
If you elect to use a private email address with GitHub, then use that same email address for the `user.email` value, e.g. `username@users.noreply.github.com` replacing `username` with your GitHub one. You can change the email address later on by using the `git config` command again.

Dracula also has to set his favorite text editor, following this table:

| Editor             | Configuration command                            |
|:-------------------|:-------------------------------------------------|
| Atom | `$ git config --global core.editor "atom --wait"`|
| nano               | `$ git config --global core.editor "nano -w"`    |
| BBEdit (Mac, with command line tools) | `$ git config --global core.editor "edit -w"`    |
| Sublime Text (Mac) | `$ git config --global core.editor "subl -n -w"` |
| Sublime Text (Win, 32-bit install) | `$ git config --global core.editor "'c:/program files (x86)/sublime text 3/sublime_text.exe' -w"` |
| Sublime Text (Win, 64-bit install) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublime_text.exe' -w"` |
| Notepad++ (Win, 32-bit install)    | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Notepad++ (Win, 64-bit install)    | `$ git config --global core.editor "'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Kate (Linux)       | `$ git config --global core.editor "kate"`       |
| Gedit (Linux)      | `$ git config --global core.editor "gedit --wait --new-window"`   |
| Scratch (Linux)       | `$ git config --global core.editor "scratch-text-editor"`  |
| emacs              | `$ git config --global core.editor "emacs"`   |
| vim                | `$ git config --global core.editor "vim"`   |

It is possible to reconfigure the text editor for Git whenever you want to change it.

> ## Exiting Vim
>
> Note that `vim` is the default editor for many programs. If you haven't used `vim` before and wish to exit a session, type `Esc` then `:q!` and `Enter`.
{: .callout}

Git (2.28+) allows configuration of the name of the branch created when you
initialize any new repository.  Dracula decides to use that feature to set it to `main` so 
it matches the cloud service he will eventually use. 

~~~
$ git config --global init.defaultBranch main
~~~
{: .language-bash}

> ## Default Git branch naming
>
> Source file changes are associated with a "branch." 
> For new learners in this lesson, it's enough to know that branches exist, and this lesson uses one branch.  
> By default, Git will create a branch called `master` 
> when you create a new repository with `git init` (as explained in the next Episode). This term evokes 
> the racist practice of human slavery and the 
> [software development community](https://github.com/github/renaming)  has moved to adopt 
> more inclusive language. 
> 
> In 2020, most Git code hosting services transitioned to using `main` as the default 
> branch. As an example, any new repository that is opened in GitHub and GitLab default 
> to `main`.  However, Git has not yet made the same change.  As a result, local repositories 
> must be manually configured have the same main branch name as most cloud services.  
> 
> For versions of Git prior to 2.28, the change can be made on an individual repository level.  The 
> command for this is in the next episode.  Note that if this value is unset in your local Git 
> configuration, the `init.defaultBranch` value defaults to `master`.
>
{: .callout}


The five commands we just ran above only need to be run once: the flag `--global` tells Git
to use the settings for every project, in your user account, on this computer.

You can check your settings at any time:

~~~
$ git config --list
~~~
{: .bash}

You can change your configuration as many times as you want: just use the
same commands to choose another editor or update your email address.

## SSH Background and Setup
Before Dracula can connect to a remote repository, he needs to set up a way for his computer to authenticate with GitHub so it knows it’s him trying to connect to his remote repository. 

We are going to set up the method that is commonly used by many different services to authenticate access on the command line.  This method is called Secure Shell Protocol (SSH).  SSH is a cryptographic network protocol that allows secure communication between computers using an otherwise insecure network.  

SSH uses what is called a key pair. This is two keys that work together to validate access. One key is publicly known and called the public key, and the other key called the private key is kept private. Very descriptive names.

You can think of the public key as a padlock, and only you have the key (the private key) to open it. You use the public key where you want a secure method of communication, such as your GitHub account.  You give this padlock, or public key, to GitHub and say “lock the communications to my account with this so that only computers that have my private key can unlock communications and send git commands as my GitHub account.”  

What we will do now is the minimum required to set up the SSH keys and add the public key to a GitHub account.

The first thing we are going to do is check if this has already been done on the computer you’re on.  Because generally speaking, this setup only needs to happen once and then you can forget about it. 

> ## Keeping your keys secure
> You shouldn't really forget about your SSH keys, since they keep your account secure. It’s good 
>  practice to audit your secure shell keys every so often. Especially if you are using multiple 
>  computers to access your account.
{: .callout}

We will run the list command to check what key pairs already exist on your computer.

~~~
ls -al ~/.ssh
~~~
{: .language-bash}

Your output is going to look a little different depending on whether or not SSH has ever been set up on the computer you are using. 

Dracula has not set up SSH on his computer, so his output is 

~~~
ls: cannot access '/c/Users/Vlad Dracula/.ssh': No such file or directory
~~~
{: .output}

If SSH has been set up on the computer you're using, the public and private key pairs will be listed. The file names are either `id_ed25519`/`id_ed25519.pub` or `id_rsa`/`id_rsa.pub` depending on how the key pairs were set up.  
Since they don’t exist on Dracula’s computer, he uses this command to create them. 

### Create an SSH key pair
To create an SSH key pair Vlad uses this command, where the `-t` option specifies which type of algorithm to use and `-C` attaches a comment to the key (here, Vlad's email):  

~~~
$ ssh-keygen -t ed25519 -C "vlad@tran.sylvan.ia"
~~~
{: .language-bash}

> ## Ed25519 algorithm on legacy system
> If you are using a legacy system that doesn’t support the Ed25519 algorithm, use: $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
{: .callout}

~~~
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/Vlad Dracula/.ssh/id_ed25519):
~~~
{: .output}

We want to use the default file, so just press <kbd>Enter</kbd>.

~~~
Created directory '/c/Users/Vlad Dracula/.ssh'.
Enter passphrase (empty for no passphrase):
~~~
{: .output}

Now, it is prompting Dracula for a passphrase.  Since he is using his lab’s laptop that other people sometimes have access to, he wants to create a passphrase.  Be sure to use something memorable or save your passphrase somewhere, as there is no "reset my password" option. 

Note: The unix shell won't show anything when you type in your password, not even placeholders!

~~~
Enter same passphrase again:
~~~
{: .output}

After entering the same passphrase a second time, we receive the confirmation

~~~
Your identification has been saved in /c/Users/Vlad Dracula/.ssh/id_ed25519
Your public key has been saved in /c/Users/Vlad Dracula/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:SMSPIStNyA00KPxuYu94KpZgRAYjgt9g4BA4kFy3g1o vlad@tran.sylvan.ia
The key's randomart image is:
+--[ED25519 256]--+
|^B== o.          |
|%*=.*.+          |
|+=.E =.+         |
| .=.+.o..        |
|....  . S        |
|.+ o             |
|+ =              |
|.o.o             |
|oo+.             |
+----[SHA256]-----+
~~~
{: .output}

The "identification" is actually the private key. You should never share it.  The public key is appropriately named.  The "key fingerprint" 
is a shorter version of a public key.

Now that we have generated the SSH keys, we will find the SSH files when we check.

~~~
ls -al ~/.ssh
~~~
{: .language-bash}

~~~
drwxr-xr-x 1 Vlad Dracula 197121   0 Jul 16 14:48 ./
drwxr-xr-x 1 Vlad Dracula 197121   0 Jul 16 14:48 ../
-rw-r--r-- 1 Vlad Dracula 197121 419 Jul 16 14:48 id_ed25519
-rw-r--r-- 1 Vlad Dracula 197121 106 Jul 16 14:48 id_ed25519.pub
~~~
{: .output}

### Copy the public key to GitHub
Now we have a SSH key pair and we can run this command to check if GitHub can read our authentication.  

~~~
ssh -T git@github.com
~~~
{: .language-bash}


~~~
The authenticity of host 'github.com (192.30.255.112)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
git@github.com: Permission denied (publickey).
~~~
{: .output}

Right, we forgot that we need to give GitHub our public key!  

First, we need to copy the public key.  Be sure to include the `.pub` at the end, otherwise you’re looking at the private key. 

~~~
cat ~/.ssh/id_ed25519.pub
~~~
{: .language-bash}

~~~
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDmRA3d51X0uu9wXek559gfn6UFNF69yZjChyBIU2qKI vlad@tran.sylvan.ia
~~~
{: .output}

Now, going to GitHub.com, click on your profile icon in the top right corner to get the drop-down menu.  Click "Settings," then on the 
settings page, click "SSH and GPG keys," on the left side "Account settings" menu.  Click the "New SSH key" button on the right side. Now, 
you can add the title (Dracula uses the title "Vlad's Lab Laptop" so he can remember where the original key pair
files are located), paste your SSH key into the field, and click the "Add SSH key" to complete the setup.

Now that we’ve set that up, let’s check our authentication again from the command line. 
~~~
$ ssh -T git@github.com
~~~
{: .language-bash}

~~~
Hi Vlad! You've successfully authenticated, but GitHub does not provide shell access.
~~~
{: .output}

Good! This output confirms that the SSH key works as intended. We are now ready to push our work to the remote repository.

Now that authentication is setup, we can return to the remote.  This command will push the changes from
our local repository to the repository on GitHub:

~~~
$ git push origin main
~~~
{: .bash}

~~~
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 821 bytes, done.
Total 9 (delta 2), reused 0 (delta 0)
To https://github.com/vlad/planets
 * [new branch]      main -> main
Branch main set up to track remote branch main from origin.
~~~
{: .output}

> ## Proxy
>
> If the network you are connected to uses a proxy, there is a chance that your
> last command failed with "Could not resolve hostname" as the error message. To
> solve this issue, you need to tell Git about the proxy:
>
> ~~~
> $ git config --global http.proxy http://user:password@proxy.url
> $ git config --global https.proxy http://user:password@proxy.url
> ~~~
> {: .bash}
>
> When you connect to another network that doesn't use a proxy, you will need to
> tell Git to disable the proxy using:
>
> ~~~
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~
> {: .bash}
{: .callout}

> ## Password Managers
>
> If your operating system has a password manager configured, `git push` will
> try to use it when it needs your username and password.  For example, this
> is the default behavior for Git Bash on Windows. If you want to type your
> username and password at the terminal instead of using a password manager,
> type:
>
> ~~~
> $ unset SSH_ASKPASS
> ~~~
> {: .bash}
>
> in the terminal, before you run `git push`.  Despite the name, [git uses
> `SSH_ASKPASS` for all credential
> entry](https://git-scm.com/docs/gitcredentials#_requesting_credentials), so
> you may want to unset `SSH_ASKPASS` whether you are using git via SSH or
> https.
>
> You may also want to add `unset SSH_ASKPASS` at the end of your `~/.bashrc`
> to make git default to using the terminal for usernames and passwords.
{: .callout}

[git-privacy]: https://help.github.com/articles/keeping-your-email-address-private/
