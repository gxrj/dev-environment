# linuxbrew-install-recipe

- Install homebrew dependencies

       sudo apt install build-essential procps curl file git

- Install Homebrew

        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

- Add Homebrew to the <code>PATH</code> variable

        (echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> $HOME/.bashrc
        
        eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

- Check brew status

        brew doctor

- Set off analytics

        brew analytics off

    or

        echo 'export HOMEBREW_NO_ANALYTICS=1' >> $HOME/.bashrc

## Miscellaneous

- Installing a package

        brew instal package_name

- Removing a package

        brew remove package_name

- Removing unecessary dependencies

        brew autoremove


## Uninstalling Homebrew from linux

        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"