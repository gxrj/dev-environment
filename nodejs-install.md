# nodejs-install-recipe

- First, install nodejs using snap

      $ sudo snap install node --classic
      
- Change <code>npm</code>'s default directory location by creating a folder for global installations

      $ mkdir ~/.npm-global
      
- Configure npm to use the new directory path

      $ npm config set prefix '~/.npm-global'
     
- Make system remenber npm modules default folder at startup and refresh the terminal

      $ echo -e '# Nodejs modules default folder \nexport PATH=~/.npm-global/bin:$PATH' >> ~/.profile && source ~/.profile
