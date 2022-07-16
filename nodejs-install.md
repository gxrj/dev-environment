# nodejs-install-recipe

<b>Preamble</b>: it uses snap format because there are lots of benefits with it (security and dependencies, for instance), if you do not have snap installed and don´t mind installing it the run <code>sudo apt install snapd -y</code> if you're running a debian-based distro

- First, install nodejs using snap

      $ sudo snap install node --classic
      
- Change <code>npm</code>'s default directory location by creating a folder for global installations

      $ mkdir ~/.npm-global
      
- Configure npm to use the new directory path

      $ npm config set prefix '~/.npm-global'
     
- Make system remenber npm modules default folder at startup and refresh the terminal

      $ echo -e '# Nodejs modules default folder \nexport PATH=~/.npm-global/bin:$PATH' >> ~/.profile && source ~/.profile
