# nodejs-install-recipe

<b>Preamble</b>: To follow this recipe you need linuxbrew package manager installed. If you haven't installed yet check it's [installation recipe right here.](./linuxbrew-install.md)

- First, install nodejs using homebrew package manager

      brew install node
      
- Change <code>npm</code>'s default directory location by creating a folder for global installations

      mkdir ~/.npm-global
      
- Configure npm to use the new directory path

      npm config set prefix '~/.npm-global'
     
- Make system remenber npm modules default folder at startup and refresh the terminal

      echo -e '# Nodejs modules default folder \nexport PATH=~/.npm-global/bin:$PATH' >> ~/.profile && source ~/.profile
