# 67272 Windows Setup
Welcome to 67272 and congratulations on using windows. Let's get your tech
stack up and running.

1) Windows Subsystem for Linux (WSL)

    Installation instructions are based on [these Windows docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

    1) Enable the feature

        Open windows powershell as an administrator and enter:
        ```
        Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
        ```

    2) Restart your computer when prompted

    3) Install Ubuntu 18.04 on WSL

        Find [Ubuntu 18.04 in the Windows store](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
        and select "Get" on the distro page. Then select "Install".

    4) Initialize your Ubuntu installation

        1) Launch Ubuntu 18.04 (it will take a minute to open)
        2) When prompted, enter a username of your choice
        3) When prompted, enter a password of your choice
        4) Record the credentials for the account you just created somewhere
        that you will not lose them
        5) Make sure you are running the most recent software (and will use
        it in the future)

            Enter this in the bash shell:
            ```
            sudo apt update && sudo apt upgrade
            ```
            Running this will take a while. You may be prompted about restarting
            services (such as ssh), this is fine.

    5) Nice work, now a few helpful things

        1) Entering `ls` will list everything in the working directory. Right
        now you will probably see nothing.
        2) `pwd` will print the working directory (where you are right now)
        3) Entering `cd [some path]` will change the current directory to the
        given path.
        4) *Important:* you can get to your windows files (and you will likely
          want to do this for the rest of this class)

            ```
            cd /mnt/
            ```
            or, you can probably get all the way to your Documents folder with
            ```
            cd /mnt/c/Users/[your windows username]/Documents
            ```

        5) *Important:* you can paste from you windows clip board into wsl by
        right-clicking. You will likely find this very useful.

        6) (Recommended) Create a folder for this class in your Documents
        folder (or somewhere you prefer)

            ```
            mkdir 67272 # creates a folder named 67272
            ```

2) Ruby 2.5.7
    1) Install gpg2 (a prerequisite for rvm)

        ```
        sudo apt-get install gnupg2
        ```
        Note: unless otherwise specified all of these instructions are meant
        to be run in the Ubuntu installation you just set up.

    2) Install rvm (based on [these instructions](https://rvm.io/))

        ```
        gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
        \curl -sSL https://get.rvm.io | bash -s stable
        ```

    3) Close your bash shell and open a new one (or `source ~/.bashrc` should work)

    4) Install Ruby 2.5.7 (this will take a while)

        ```
        rvm install 2.5.7
        ```

    5) Set default Ruby version

        ```
        bash --login
        rvm --default use 2.5.7
        ```

    6) Close and re-open WSL

    7) Check installation

        ```
        rvm list
        ```
        You should see `=* ruby-2.5.7` in the output.

3) Rails 5.2.3
    1) Install nodejs (a prerequisite)

        ```
        curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
        sudo apt-get install -y nodejs
        ```

    2) Install Rails 5.2.3 (this will take a while)

        ```
        gem install rails -v=5.2.3
        ```

    3) Test installation
        1) Pick a good directory

            We are going to create a trivial web app. Make sure you are in a
            folder that you want to be in. Use `cd` (and maybe `mkdir`) as expained
            in the WSL setup instructions. The new app will be created in it's own
            folder so no need to make a specific one.

        2) Create an application with the name "testapp"

            ```
            rails new testapp
            ```
            (this may take a little while)

        3) Change diretories into the new application

            ```
            cd testapp
            ```

        4) Install the new app's dependencies

            ```
            bundle install
            ```
            You may have to try this command multiple times. If it fails in a
            consistent way then seek help.

        4) Run the application

            ```
            rails server
            ```

        5) Open your browser and put [localhost:3000](localhost:3000) in the
        address bar (or open the link)

            You should see the basic rails splash page:
            ![splash page image](https://github.com/mjkern/67272-Windows-Setup/blob/master/rails_welcome.png?raw=true)

            Congrats, you did it! (When you're done the key combination CTRL c
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

