# nodejs-install-recipe

<b>Preamble</b>: To follow this recipe you need <code>linuxbrew package manager</code> installed. If you haven't installed yet check it's [installation recipe right here.](./linuxbrew-install.md)

- Install nodejs using homebrew package manager

      brew install node

## Optional steps

### Option 1: Stick with <code>NPM</code> 

- Change <code>npm</code>'s default directory location by creating a folder for global installations

      mkdir ~/.npm-global
      
- Configure npm to use the new directory path

      npm config set prefix '~/.npm-global'
     
- Make system remenber npm modules default folder at startup and refresh the terminal

      echo -e '# Nodejs modules default folder \nexport PATH=~/.npm-global/bin:$PATH' >> ~/.profile && source ~/.profile

### Option 2: Ditch <code>NPM</code> in favor of <code>PNPM</code>

- Install <code>corepack</code>

        brew install corepack

- Install <code>PNPM</code>

        corepack enable pnpm

- Create an alias for <code>PNPM</code>

        echo -e '\nalias pn=pnpm' >> .bashrc

- Set a location for modules installed by pnpm

        pn config set store-dir ~/.pnpm-store
  
