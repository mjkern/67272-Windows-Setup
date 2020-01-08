# 67272 Windows Setup
Welcome to 67272 and congratulations on using windows. Let's get your tech
stack up and running.

1) Windows Subsystem for Linux (WSL)

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

3) Visual Studio Code
