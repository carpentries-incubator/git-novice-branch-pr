---
title: Setup
permalink: /setup/
---

## The Bash Shell

Bash is a commonly-used shell that gives you the power to do
tasks more quickly.

::: tab

### Windows

Windows users will install a bash shell called Git Bash when installing git following the instructions below:

1. Download the Git for Windows [installer](https://gitforwindows.org/).
2. Run the installer and follow the steps below:
  1. Click on "Next" to accept the license agreement, again to accept the default installation path, again to select the default components, and a fourth time to name a start menu folder. (If you have git installed already, see the note below.)
  2. From the dropdown menu select "Use the nano editor by default" and click on "Next".
  3. Select "Override the default branch name for new repositories" and leave it set to main. Click on "Next".
  4. Ensure that "Git from the command line and also from 3rd-party software" is selected and click on "Next". (If you don't do this Git Bash will not work properly, requiring you to remove the Git Bash installation, re-run the installer and to select the "Git from the command line and also from 3rd-party software" option.)
  5. Select "Use bundled OpenSSH" and click on "Next".
  6. Select "Use the native Windows Secure Channel library" and click on "Next".
  7. Ensure that "Checkout Windows-style, commit Unix-style line endings" is selected and click on "Next".
  8. Ensure that "Use Windows' default console window" is selected and click on "Next".
  9. Ensure that "Default (fast-forward or merge) is selected and click "Next"
  10. Ensure that "Get Crediential Manager" is selected and click on "Next".
  11. Ensure that "Enable file system caching" is checked and click on "Next".
  12. Do not enable either of the "experimental options". Click "Install".
  13. Click on "Finish" or "Next".
3. If your "HOME" environment variable is not set (or you don't know what this is):
  1. Open command prompt (Open Start Menu then type `cmd` and press Enter)
  2. Type the following line into the command prompt window exactly as shown:
    `setx HOME "%USERPROFILE%"`
  3. Press Enter, you should see SUCCESS: Specified value was saved.
  4. Quit command prompt by typing exit then pressing Enter
This will provide you with both Git and Bash in the Git Bash program.

If you already have git installed, running the installer will upgrade to the newest verison, currently 2.35.1.2. When you launch the installer, ensure "Only show new options" is **unchecked**.


### Mac

The default shell in some versions of macOS is Bash, and Bash is available in all versions, so no need to install anything. You access Bash from the Terminal (found in `/Applications/Utilities`). You may want to keep Terminal in your dock for this workshop.

To see if your default shell is Bash type `echo $SHELL` in Terminal and press the Return key. If the message printed does not end with '/bash' then your default is something else and you can run Bash by typing `bash`

If you want to change your default shell, see this [Apple Support article](https://support.apple.com/en-au/HT208050) and follow the instructions on "How to change your default shell".


### Linux

The default shell is usually Bash and there is usually no need to install anything.

To see if your default shell is Bash type `echo $SHELL` in a terminal and press the Enter key. If the message printed does not end with '/bash' then your default is something else and you can run Bash by typing `bash`.


:::


## Git

Git is a version control system that lets you track who made changes to what when and has options for easily updating a shared or public version of your code on [github.com](https://github.com/). You will need a [supported web browser](https://help.github.com/articles/supported-browsers/).

You will need an account at [github.com](https://github.com/) for parts of the Git lesson. Basic GitHub accounts are free. We encourage you to create a GitHub account if you don't have one already. Please consider what personal information you'd like to reveal. For example, you may want to review these instructions for [keeping your email address private provided by GitHub](https://help.github.com/articles/keeping-your-email-address-private/).

::: tab

### Windows

Git should be installed on your computer as part of your Bash install (see the Shell installation instructions above).

### Mac

Please open the Terminal app, type `git --version` and press Enter/Return. If it's not installed already, follow the instructions to `Install` the "command line developer tools". **Do not click "Get Xcode"**, because that will take too long and is not necessary for our Git lesson. After installing these tools, there won't be anything in your /Applications folder, as they and Git are command line programs. **For older versions of OS X (10.5-10.8)** use the most recent available installer labelled "snow-leopard" [available here](http://sourceforge.net/projects/git-osx-installer/files/). (Note: this project is no longer maintained.) Because this installer is not signed by the developer, you may have to right click (control click) on the .pkg file, click Open, and click Open in the pop-up dialog.



### Linux

If Git is not already available on your machine you can try to install it via your distro's package manager. For Debian/Ubuntu run `sudo apt-get install git` and for Fedora run `sudo dnf install git`.


:::



