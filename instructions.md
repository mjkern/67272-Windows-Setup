## 67272 Windows Setup
Welcome to 67272 and congratulations on using windows. Let's get your tech
stack up and running.

### Setup Windows Subsystem for Linux (WSL)

If you already have WSL 2 setup you can skip until at least step 6 section.
If you already have WSL 1 setup you can skip to step 2.

Installation instructions are based on [these Windows docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

1) Enable WSL

    Open windows powershell as an administrator and enter:
    ```powershell
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```

2) Enable extra option for WSL 2

    In the same powershell window:
    ```powershell
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```

    Note: 
    We recommend WSL 2 for this class for performance and support reasons,
    but there are a few reasons you might not want it:

    1) You are running a [very old version](https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-2---check-requirements-for-running-wsl-2)
    of windows and it is not supported (probably only a problem if you have
    avoided updates for over a year)
    2) You need to run virtual machines on out-of-date vm software (older
    than VMware 15.5.5 or VirtualBox 6)
    3) You computer is managed by a mischevious power-hunger admin who has
    locked virtualization off in the BIOS

    Chances are that none of these are an issue but talk to Matt (mjkern) if
    you have questions or concerns.

3) Restart your computer

4) Download and run the [WSL2 Linux kernel update package for x64 machines](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

    Note: if you are running an ARM64 machine then you should instead use
    the [ARM64 package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi). This probably is not you, but you can double
    check with `systeminfo | find "System Type"` in powershell.

5) Set the default WSL version to 2 for new installations with this powershell
    command:

    ```powershell
    wsl --set-default-version 2
    ```

    Note: you can always change this to version 1 later (with
    `wsl --set-default-version 1`) if for some reason you want to install a
    distribution on WSL 1 instead of WSL 2.    

6) Install Ubuntu 20.04 on WSL

    Find [Ubuntu 20.04 LTS in the Windows store](https://www.microsoft.com/en-us/p/ubuntu-2004-lts/9n6svws3rx71?activetab=pivot:overviewtab)
    and select "Get" on the distro page. Then select "Install".

7) Initialize your Ubuntu installation

    1) Launch an Ubuntu 20.04 terminal (it will take a few minutes)

        Note: you can do this by searching for `Ubuntu 20.04`. You may want
        to pin this to your start menu for easy access in the future

    2) When prompted, enter a username of your choice
    3) When prompted, enter a password of your choice
    4) Record the credentials for the account you just created somewhere
    that you will not lose them
    5) Make sure you are running the most recent software (and will use
    it in the future)

        Enter this in terminal:
        ```bash
        sudo apt update -y && sudo apt upgrade -y
        ```

        When prompted, enter the password you just created. You will not see
        the cursor move as you type - this is expected and is a security
        feature. Press enter after typing your password.

        Remember how this password process works - this will often happen
        when you use the `sudo` keyword (which is essentially running the
        command as an administrator).

        This will take a few minutes.

8) Nice work! Now a few things you should know:

    - you can paste into the terminal from you windows clip board by
    right-clicking
    - you can get to your windows files if you really need to, although this
    is slower and we will recommend that you keep files for this class all
    in the linux file system that you are in right now

        ```bash
        cd /mnt/c
        ```

        or, you can probably get all the way to your Documents folder with
        ```bash
        cd /mnt/c/Documents\ and\ Settings/<your windows username>/Documents
        ```
        where `<your windows username>` is the first 4 characters of your
        windows username.

        Note: on wsl 1 this is more likely
        ```bash
        cd /mnt/c/Users/<your windows username>/Documents
        ```

    - if you are new to linux, here is
    [a cheat sheet for common terminal commands](http://www.mathcs.emory.edu/~valerie/courses/fall10/155/resources/unix_cheatsheet.html)

    - if you start typing something terminal, entering a tab will try to
    autocomplete the command 

### Install Ruby 2.6.6
1) Install gpg2 (a prerequisite for rvm)

    ```bash
    sudo apt install -y gnupg2
    ```
    Note: unless otherwise specified all of these instructions are meant
    to be run in a terminal for the Ubuntu distribution you just set up.

2) Install rvm (based on [these instructions](https://rvm.io/))

    ```bash
    gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
    \curl -sSL https://get.rvm.io | bash -s stable
    ```

    If this fails, try changing the keyserver url to one of the other
    options listed on the [rvm troubleshooting page](https://rvm.io/rvm/security)

3) Close your terminal and open a new one (or `source ~/.bashrc` should work)

4) Install Ruby 2.6.6 (this may take a minute)

    ```bash
    rvm install 2.6.6
    ```

5) Set default Ruby version

    ```bash
    bash --login
    rvm --default use 2.6.6
    ```

6) Close and re-open the terminal

7) Check installation

    ```bash
    rvm list
    ```
    You should see `=* ruby-2.6.6` in the output.

### Install Rails 5.2.4.4
1) Install nodejs (a prerequisite)

    ```bash
    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - && sudo apt install -y nodejs
    ```

2) Install Rails 5.2.4.4 (this may take a few minutes)

    ```bash
    gem install rails -v=5.2.4.4
    ```

3) Test installation
    1) Pick a good directory

        We are going to create a trivial web app. Make sure you are in a
        folder that you want to be in.

        I recommend creating a folder for each lab (and phase) right where
        you are, the `home` directory. You will be here by default when you
        open a terminal, and can always get back here with `cd ~`.
        
        **Avoid working in any path that begins with `/mnt/c/`** as this will
        almost certainly cause issues with `rails new`, `git init`, `chmod`,
        and other important commands because of the way that wsl translates (or
        fails to translate) file permissions. If you're intersted, there is 
        [more info and a potential work-around](https://github.com/microsoft/WSL/issues/81#issuecomment-409620796).

        So use `mkdir` and `cd` to get where you want to be. For example:
        ```bash
        mkdir lab01
        cd lab01
        ```           

    2) Create an application with the name "testapp"

        ```bash
        rails new testapp
        ```
        (this may take a minute)

        Debugging Tip - If you executed this command in you windows file system
        (any path that begins with `/mnt/c/`) then you probably get this error:
        > error: chmod on /mnt/c/Users/mjker/Documents/TAing/testapp2/.git/config.lock failed: Operation not permitted
        >
        > fatal: could not set 'core.filemode' to 'false'

        Solution - work in a directory that does not begin with `/mnt/c/`,
        probably `~`.

    3) Change diretories into the new application

        ```bash
        cd testapp
        ```

    4) Install the new app's dependencies

        ```bash
        bundle install
        ```
        
        Note: this command can be slow and buggy, especially if you are
        using wsl 1. If the terminal hangs (nothing changes for a few
        minutes) then try pressing enter. You may have to try this command
        multiple times. If it fails in a consistent way seek help from a TA.

    4) Run the application

        ```bash
        rails server
        ```

    5) Open your browser and put [localhost:3000](http://localhost:3000) in
    the address bar (or open the link)

        You should see the basic rails splash page:
        ![splash page image](https://github.com/mjkern/67272-Windows-Setup/blob/master/rails_welcome.png?raw=true)

        Congrats, you did it! (When you're done the key combination `CTRL c`
        will stop the server)

### Install Visual Studio Code

Note: Visual Studio Code is the *required* editor for this class. You also
must have the extensions mentioned in these instructions. If you already
have VS Code installed then skip to step 3.

1) Go to [https://code.visualstudio.com/](https://code.visualstudio.com/)
and select "Download for Windows"

2) After the download completes run the installer and click through the
prompts

3) Open Visual Studio Code from the start menu

4) [Install the `Remote - WSL` extention](vscode:extension/ms-vscode-remote.remote-wsl)
for Visual Studion Code (click this link and then click "Install")

    If requested, reload Visual Studio Code.

5) Open the command palette

    View > Command palette...

    Or use the shortcut `Crtl+Shift+P`

6) Enter `Remote-WSL: New window` to open a Visual Studio Code window that
is running from Ubuntu 20.04 on WSL instead of the current window which is
running from Windows 10.

    Note: if you have more than one distribution installed you should use
    the `Remote-WSL: New Window using Distro...` command and then specify
    Ubuntu 20.04.

7) When the new Visual Studio Code window opens, close the one that you were
working from

8) Find and open the extensions sidebar via the menu on the left side of the
screen. It should be the 5th option from the top.

9) Search for and install these extensions, as follows:

    1) **Live Share** by Microsoft

        A few seconds after you install you will see a toast in the
        bottom-right corner of your screen with the message:
        > We were unable to install support for joining sessions using a browser link. You may be missing key Linux libraries. Install them now?

        Click `Install` on the toast message.

        When promped, enter your password (the one you created today).

        Reload VS Code when prompted.

        There will be another toast:
        > To support joining a session using a browser link, we need permission to run an installer on your system. Your OS may ask you for your admin (sudo) password in a terminal. Install now?

        Once again, click `Install` and enter you password.
    
    2) **Live Server** by Ritwick Dey

10) Configure the terminal

    1) Open settings

        File > Preferences > Settings

        Or `Ctrl+,`

    2) Search for `Shell Args` and find the setting entitled
        *Terminal > Integrated > Sell Args: Linux*

    3) Click the `Add Option` button under this setting

    4) Enter `-l` and click `OK`. FYI, that is a lowercase l, as in lion.

        FYI, this configures you terminal to open as a login shell by
        default. This is important for `rails` and a number of other tools.

11) Select `File>Open Folder` and then give the directory to the `testapp`
folder in the prompt. Click `OK`.

    Note: if you followed the recommendation above then this will be
    `/home/<your Ubuntu username>/lab01/testapp/`

12) You should now be able to see all of the files in the `testapp`
application that you created earlier. Open a few of them to get used to
Visual Studio Code.

13) Open a terminal through VS Code

    Terminal > New Terminal

    Or `` Ctrl+Shift+` ``

    Note: This terminal is almost exactly like the one you used outside of
    Visual Studio Code earlier, but notice a few things:

    - You can paste into this terminal with `Ctrl+Shift+V` or `Shift+Insert`
    or right-click
    - You can copy from this terminal with `Ctrl+Shift+C`
    - It defaults to the project directory that you have open instead of
    your home directory
    - There is nice syntax highlighting and hyperlinks are clickable

14) In this new terminal, run the web application

    ```bash
    rails server
    ```
15) Once again, open your browser and put
[localhost:3000](http://localhost:3000) in the address bar (or open the
link)

    You should see the same welcome page that you saw before.
    Congratulations, you are all setup!

    Use `Ctrl+c` in the terminal to stop the server when you are finished.

### [Optional] More tools & configuration

**These is not required, encouraged, or tested.**

#### Terminal Configuration

Proh H has a
[customized variation of `oh-my-zsh`](https://github.com/profh/ohmyzsh) that he
allows students to use. Joao Grassi has an explanation of how he set this up on
Windows
[in this blog post](https://blog.joaograssi.com/windows-subsystem-for-linux-with-oh-my-zsh-conemu/).
You are welcome to try this out if you so desire. Notice that you will have to
change the install script url to match that of Prof H's repo.

Alternatively, you can use
[Prof H's dotfiles](https://github.com/profh/dotfiles) as a means of customizing
the default (bash) shell instead of installing zsh.

That said, I personally would not worry about any of these customizations. It is
good to be familiar with the default tools before you customize them, and I use
almost no modifications to this day.

#### Windows Terminal

[Windows Terminal](https://aka.ms/terminal)
provides a cleaner terminal than what comes with WSL by default. It allows for
multiple tabs and makes it easy to work between powershell, command prompt, and
(potentially multiple) WSL distributions.

## Author's Note

These instructions were written by Matt Kern for use in Carnegie Mellon
Univeristy's 67272.

Please let me know if you have any problems, find typos, or have
questions:

mjkern@andrew.cmu.edu

qapla'
