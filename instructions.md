# 67272 Windows Setup
Welcome to 67272 and congratulations on using windows. Let's get your tech
stack up and running.

1) Windows Subsystem for Linux (WSL)

    If you already have WSL 2 setup you can skip until at least step 6 section.
    If you already have WSL 1 setup you can skip to step 2.
    
    Installation instructions are based on [these Windows docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

    1) Enable WSL

        Open windows powershell as an administrator and enter:
        ```
        dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
        ```
    
    2) Enable extra option for WSL 2

        In the same powershell window:
        ```
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
    
    5) Set the default WSL version to 2 for new installations

        ```
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
            ```
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

            ```
            cd /mnt/c
            ```

            or, you can probably get all the way to your Documents folder with
            ```
            cd /mnt/c/Documents\ and\ Settings/<your windows username>/Documents
            ```
            where `<your windows username>` is the first 4 characters of your
            windows username.

            Note: on wsl 1 this is more likely
            ```
            cd /mnt/c/Users/<your windows username>/Documents
            ```

        - if you are new to linux, here is
        [a cheat sheet for common terminal commands](http://www.mathcs.emory.edu/~valerie/courses/fall10/155/resources/unix_cheatsheet.html)

        - if you start typing something terminal, entering a tab will try to
        autocomplete the command 

2) Ruby 2.6.6
    1) Install gpg2 (a prerequisite for rvm)

        ```
        sudo apt install -y gnupg2
        ```
        Note: unless otherwise specified all of these instructions are meant
        to be run in a terminal for the Ubuntu distribution you just set up.

    2) Install rvm (based on [these instructions](https://rvm.io/))

        ```
        gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
        \curl -sSL https://get.rvm.io | bash -s stable
        ```

        If this fails, try changing the keyserver url to one of the other
        options listed on the [rvm troubleshooting page](https://rvm.io/rvm/security)

    3) Close your terminal and open a new one (or `source ~/.bashrc` should work)

    4) Install Ruby 2.6.6 (this may take a minute)

        ```
        rvm install 2.6.6
        ```

    5) Set default Ruby version

        ```
        bash --login
        rvm --default use 2.6.6
        ```

    6) Close and re-open the terminal

    7) Check installation

        ```
        rvm list
        ```
        You should see `=* ruby-2.6.6` in the output.

3) Rails 5.2.4.4
    1) Install nodejs (a prerequisite)

        ```
        curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
        sudo apt install -y nodejs
        ```

    2) Install Rails 5.2.4.4 (this may take a few minutes)

        ```
        gem install rails -v=5.2.4.4
        ```

    3) Test installation
        1) Pick a good directory

            We are going to create a trivial web app. Make sure you are in a
            folder that you want to be in.

            I recommend creating a folder for each lab (and phase) right where
            you are, the `home` directory. You will be here by default when you
            open a terminal, and can always get back here with `cd ~`. You
            should avoid working in any path that begins with `/mnt/` for
            performance reasons (if you are using WSL 2).

            So use `mkdir` and `cd` to get where you want to be. For example:
            ```
            mkdir lab01
            cd lab01
            ```           

        2) Create an application with the name "testapp"

            ```
            rails new testapp
            ```
            (this may take a minute)

        3) Change diretories into the new application

            ```
            cd testapp
            ```

        4) Install the new app's dependencies

            ```
            bundle install
            ```
            
            Note: this command can be slow and buggy, especially if you are
            using wsl 1. If the terminal hangs (nothing changes for a few
            minutes) then try pressing enter. You may have to try this command
            multiple times. If it fails in a consistent way seek help from a TA.

        4) Run the application

            ```
            rails server
            ```

        5) Open your browser and put [localhost:3000](http://localhost:3000) in
        the address bar (or open the link)

            You should see the basic rails splash page:
            ![splash page image](https://github.com/mjkern/67272-Windows-Setup/blob/master/rails_welcome.png?raw=true)

            Congrats, you did it! (When you're done the key combination `CTRL c`
            will stop the server)

4) Visual Studio Code

    1) Go to [https://code.visualstudio.com/](https://code.visualstudio.com/)
    and select "Download for Windows"
    2) After the download completes run the installer and click through the
    prompts
    3) Open Visual Studio Code from the start menu
    4) Select `File>Open Folder` and then select the `testapp` you created
    5) You can now inspect all the files of your first rails app in VS Code, Congrats!

## Advanced Notes

* "Remote - WSL" looks like an interesting Visual Studio Code extension but I
don't know much about it. There may also be other helpful ones
* Other versions of Ubuntu will almost certainly work fine, I just suggest
bionic beaver (18.04) here for simplicity. If you simply choose "Ubuntu" in
the windows store then I believe it will keep you up to date with the most recent version
* A note WSL:

    There are currently two versions of WSL. I suspect that we all have the
    original version but it may be possible that someone has WSL2. These are
    fundamentally different - the original is a compatability layer around the
    Windows kernal while WSL2 manages an entirely seperate kernal via a
    hypervisor. I believe all of these instructions will work just as well
    (probably better) on WSL2, but don't have an easy way to test that.

## Author's Note

These instructions were written by Matt Kern for use in Carnegie Mellon
Univeristy's 67272.

Please let me know if you have any problems with this, find typos, or have
questions:

mjkern@andrew.cmu.edu

qapla'

