---
layout: page
title: Setup
permalink: /setup/
---

<div id="shell">
  <h3>The Bash Shell</h3>
  <p>
    Bash is a commonly-used shell that gives you the power to do
    tasks more quickly.
  </p>

  <div>
    <ul class="nav nav-tabs" role="tablist">
      <li role="presentation" class="active"><a data-os="windows" href="#shell-windows" aria-controls="Windows" role="tab" data-toggle="tab">Windows</a></li>
      <li role="presentation"><a data-os="macos" href="#shell-macos" aria-controls="MacOS" role="tab" data-toggle="tab">MacOS</a></li>
      <li role="presentation"><a data-os="linux" href="#shell-linux" aria-controls="Linux" role="tab" data-toggle="tab">Linux</a></li>
    </ul>

    <div class="tab-content">
      <article role="tabpanel" class="tab-pane active" id="shell-windows">
        <ol>
          <li>Download the Git for Windows <a href="https://gitforwindows.org/">installer</a>.</li>
          <li>Run the installer and follow the steps below:
            <ol>
              {% comment %} Git 2.27.0 Setup {% endcomment %}
              <li>
                Click on "Next" four times (two times if you've previously
                installed Git).  You don't need to change anything
                in the Information, location, components, and start menu screens.
              </li>
              <li>
                <strong>
                  From the dropdown menu select "Use the nano editor by default" and click on "Next".
                </strong>
              </li>
              {% comment %} Adjusting your PATH environment {% endcomment %}
              <li>
                Ensure that "Git from the command line and also from 3rd-party software" is selected and
                click on "Next". (If you don't do this Git Bash will not work properly, requiring you to
                remove the Git Bash installation, re-run the installer and to select the "Git from the
                command line and also from 3rd-party software" option.)
              </li>
              {% comment %} Choosing the SSH executable {% endcomment %}
              {% comment %} Choosing HTTPS transport backend {% endcomment %}
              <li>
		Ensure that "Use the native Windows Secure Channel library" is selected and click on "Next".
	      </li>
              {% comment %} This should mean that people stuck behind corporate firewalls that do MITM attacks
                                 with their own root CA are still able to access remote git repos. {% endcomment %}
              {% comment %} Configuring the line ending conversions {% endcomment %}
              <li>
                Ensure that "Checkout Windows-style, commit Unix-style line endings" is selected and click on "Next".
              </li>
              {% comment %} Configuring the terminal emulator to use with Git Bash {% endcomment %}
              <li>
                <strong>
                  Ensure that "Use Windows' default console window" is selected and click on "Next".
                </strong>
              </li>
              {% comment %} Configuring extra options {% endcomment %}
              <li>
		Ensure that "Default (fast-forward or merge) is selected and click "Next"
              </li>
              <li>
		Ensure that "Enable file system caching" and "Enable Git Credential Manager" are selected
		and click on "Next".
              </li>
              {% comment %} Configuring experimental options {% endcomment %}
              <li>Click on "Install".</li>
              {% comment %} Installing {% endcomment %}
              {% comment %} Completing the Git Setup Wizard {% endcomment %}
              {% comment %} as of 2020-06-02, the Window will say "click Finish", but the button is labelled as "Next" {% endcomment %}
              <li>Click on "Finish" or "Next".</li>
            </ol>
          </li>
          <li>
            If your "HOME" environment variable is not set (or you don't know what this is):
            <ol>
              <li>Open command prompt (Open Start Menu then type <code>cmd</code> and press <kbd>Enter</kbd>)</li>
              <li>
                Type the following line into the command prompt window exactly as shown:
                <p><code>setx HOME "%USERPROFILE%"</code></p>
              </li>
              <li>Press <kbd>Enter</kbd>, you should see <code>SUCCESS: Specified value was saved.</code></li>
              <li>Quit command prompt by typing <code>exit</code> then pressing <kbd>Enter</kbd></li>
            </ol>
	  </li>
        </ol>
        <p>This will provide you with both Git and Bash in the Git Bash program.</p>
        <h4>Video Tutorial</h4>
        <div class="yt-wrapper2">
        <div class="yt-wrapper">
        <iframe type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/339AEqk9c-8?modestbranding=1&playsinline=1&iv_load_policy=3&rel=0" class="yt-frame" allowfullscreen></iframe>
        </div>
        </div>
      </article>
      <article role="tabpanel" class="tab-pane" id="shell-macos">
        <p>
          The default shell in some versions of macOS is Bash, and
	  Bash is available in all versions, so no need to install anything.
	  You access Bash from the Terminal (found in
	  <code>/Applications/Utilities</code>).
          See the Git installation <a href="#shell-macos-video-tutorial">video tutorial</a>
          for an example on how to open the Terminal.
          You may want to keep Terminal in your dock for this workshop.
        </p>
        <p>
            To see if your default shell is Bash type <code>echo $SHELL</code>
            in Terminal and press the <kbd>Return</kbd> key. If the message
            printed does not end with '/bash' then your default is something
            else and you can run Bash by typing <code>bash</code>
        </p>
        <p>
          If you want to change your default shell, see <a href="https://support.apple.com/en-au/HT208050" rel="noopener">
          this Apple Support article</a> and follow the instructions on "How to change your default shell".
        </p>
        <h4 id="shell-macos-video-tutorial">Video Tutorial</h4>
        <div class="yt-wrapper2">
        <div class="yt-wrapper">
        <iframe type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/9LQhwETCdwY?modestbranding=1&playsinline=1&iv_load_policy=3&rel=0" class="yt-frame" allowfullscreen></iframe>
        </div>
        </div>
      </article>
      <article role="tabpanel" class="tab-pane" id="shell-linux">
        <p>
          The default shell is usually Bash and there is usually no need to
          install anything.
        </p>
        <p>
          To see if your default shell is Bash type <code>echo $SHELL</code> in
          a terminal and press the <kbd>Enter</kbd> key. If the message printed
          does not end with '/bash' then your default is something else and you
          can run Bash by typing <code>bash</code>.
        </p>
      </article>
    </div>
  </div>
</div>

{% comment %}
Git Setup instructions rely on Shell instructions. If you don't include
Shell instructions as part of your workshop website, make sure to adjust
the text below accordingly.
{% endcomment %}
<div id="git">
  <h3>Git</h3>
  <p>
    Git is a version control system that lets you track who made changes
    to what when and has options for easily updating a shared or public
    version of your code
    on <a href="https://github.com/">github.com</a>. You will need a
    <a href="https://help.github.com/articles/supported-browsers/">supported
    web browser</a>.
  </p>
  <p>
    You will need an account at <a href="https://github.com/">github.com</a>
    for parts of the Git lesson. Basic GitHub accounts are free. We encourage
    you to create a GitHub account if you don't have one already.
    Please consider what personal information you'd like to reveal. For
    example, you may want to review these
    <a href="https://help.github.com/articles/keeping-your-email-address-private/">instructions
      for keeping your email address private</a> provided at GitHub.
  </p>

  <div>
    <ul class="nav nav-tabs" role="tablist">
      <li role="presentation" class="active"><a data-os="windows" href="#git-windows" aria-controls="Windows" role="tab" data-toggle="tab">Windows</a></li>
      <li role="presentation"><a data-os="macos" href="#git-macos" aria-controls="MacOS" role="tab" data-toggle="tab">MacOS</a></li>
      <li role="presentation"><a data-os="linux" href="#git-linux" aria-controls="Linux" role="tab" data-toggle="tab">Linux</a></li>
    </ul>

    <div class="tab-content">
      <article role="tabpanel" class="tab-pane active" id="git-windows">
        <p>
          Git should be installed on your computer as part of your Bash
          install (see the
          <a href="#shell">Shell installation instructions</a>).
        </p>
      </article>
      <article role="tabpanel" class="tab-pane" id="git-macos">
        <p>
          <strong>For macOS</strong>, install Git for Mac
          by downloading and running the most recent "mavericks" installer from
          <a href="http://sourceforge.net/projects/git-osx-installer/files/">this list</a>.
          Because this installer is not signed by the developer, you may have to
          right click (control click) on the .pkg file, click Open, and click
          Open on the pop up window.
          After installing Git, there will not be anything in your <code>/Applications</code> folder,
          as Git is a command line program.
          <strong>For older versions of OS X (10.5-10.8)</strong> use the
          most recent available installer labelled "snow-leopard"
          <a href="http://sourceforge.net/projects/git-osx-installer/files/">available here</a>.
        </p>
        <h4>Video Tutorial</h4>
        <div class="yt-wrapper2">
        <div class="yt-wrapper">
          <iframe type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/9LQhwETCdwY?modestbranding=1&playsinline=1&iv_load_policy=3&rel=0" class="yt-frame" allowfullscreen></iframe>
        </div>
        </div>
      </article>
      <article role="tabpanel" class="tab-pane" id="git-linux">
        <p>
          If Git is not already available on your machine you can try to
          install it via your distro's package manager. For Debian/Ubuntu run
          <code>sudo apt-get install git</code> and for Fedora run
          <code>sudo dnf install git</code>.
        </p>
      </article>
    </div>
  </div>
</div>

We'll do our work in the `Desktop` folder so make sure you change your working directory to it with:

~~~
$ cd
$ cd Desktop
~~~
{: .bash}

[workshop-setup]: https://swcarpentry.github.io/workshop-template/#git
