## Preamble

<p> It uses snap format because there are lots of benefits with it (security and dependencies, for instance), if you do not have snap installed and don´t mind installing it the run <code>sudo apt install snapd -y</code> if you're running a debian-based distro</p>

## Installation steps

### With snap installed, perform docker installation
    sudo snap install docker --classic

### The forthcomming snippet allows its invocation whithout the need for privileges
    sudo addgroup --system docker
    sudo adduser $USER docker
    newgrp docker

### Necessary reboot docker to make changes take effect
    sudo snap disable docker
    sudo snap enable docker

<br><br><br>
## Miscellaneous

### Shutting down docker daemon service
    sudo snap stop docker.dockerd
    
### Booting up docker daemon service
    sudo snap start docker.dockerd
