# 67272 Windows Setup
Welcome to 67272 and congratulations on using windows. Let's get your tech
stack up and running.

1) Windows Subsystem for Linux (WSL)

    TODO: make sure students know how to use cd /mnt/ to get to the windows partition

2) Ruby 2.4.3
    1) Open a bash shell

        This is what you just set up and the rest of the Ruby and Rails
        installation instructions will be run in this shell window. When
        you see a command in these instructions you can simply enter it after
        the `$` in your shell window.

    2) Install gpg2 (a prerequisite for rvm)

        ```
        sudo apt-get install gnupg2
        ```

    3) Install rvm (based on [these instructions](https://rvm.io/))

        ```
        gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
        \curl -sSL https://get.rvm.io | bash -s stable
        ```

    4) Close your bash shell and open a new one (or `source ~/.bashrc` should work)

    5) Install Ruby 2.4.3

        ```
        rvm install 2.4.3
        ```

    6) Check installation

        ```
        rvm list
        ```
        You should see `=* ruby-2.4.3` in the output.

3) Rails 5.1.6
    1) Install nodejs (a prerequisite)

        ```
        curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
        sudo apt-get install -y nodejs
        ```

    2) Install Rails 5.1.6

        ```
        gem install rails -v=5.1.6
        ```

    3) Test installation
        1) Pick a good dictory

            We are going to create a trivial web app. Make sure you are in a
            folder that you want to be in. Use `cd` (and maybe `mkdir`) as expained
            in the WSL setup instructions. The new app will be created in it's own
            folder so no need to make a specific one.

        2) Create an application with the name "testapp"

            ```
            rails new testapp
            ```

        3) Change diretories into the new application

            ```
            cd testapp
            ```

        4) Run the application

            ```
            rails server
            ```

        5) Open your browser and put [localhost:3000](localhost:3000) in the
        address bar (or open the link)

            You should see the basic rails splash page:
            ![splash page image](rails-welcome.png)

            Congrats, you did it!

4) Visual Studio Code

