# github-tokens-recipe 4 Linux/MacOS

### After getting your token hit the following command to store your token:
    echo 'your-token' >> ~/.git-credentials
 
### Make sure your ~./gitconfig does not have a '[credential]' session like the example bellow, if it does just remove it before the following step.
    [credential]
        helper = store 

### Then set ~/.gitconfig to search for credentials whenever needed, by hitting the command bellow:
    echo -e '[credential] \n\thelper = store --file ~/.git-credentials' > ~/.gitconfig

Reference:
https://git-scm.com/docs/git-credential-store

# Extra steps

### Set username globally
    git config --global user.name "Your username"
      
### Set email globally
    git config --global user.email "youremail@yourdomain.com" 
