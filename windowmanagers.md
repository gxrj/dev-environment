## Window manager installation recipe ( Work in Progress )
The <b>window managers bellow rely on a dependency that is <ins>the X window server</ins></b>. 
So before choosing any window manager xorg must be installed first

### Mandatory: Install X window server

    sudo apt install xinit x11-xserver-utils

### Option 1: IceWm

    sudo apt install icewm

* Set icewm preferences

      mkdir ~/.icewm
  
      echo -e 'ContinuousEdgeSwitch = 0 \nCPUStatusShowRamUsage = 0 \nCPUStatusShowSwapUsage = 0' \
      '\nTaskBarFullscreenAutoShow = 0 \nTaskBarShowCPUStatus = 0 \nTaskBarShowMailboxStatus = 0' \
      '\nTaskBarShowMEMStatus = 0 \nTaskBarShowShowDesktopButton = 0 \nTaskBarShowWindowListMenu = 0' \
      '\nTaskBarShowWorkspaces = 0 \nTimeFormat = "%H:%M"' >> ~/.icewm/preferences

### Option 2: Fluxbox

    sudo apt install --no-install-recommends fluxbox 
    sudo apt install nm-tray volumeicon-alsa cbatticon laptopmode-tools

* in <code>~/.fluxbox/init</code> make an edition so that it can have the following line:

      session.screen0.toolbar.tools: iconbar, prevwindow, nextwindow, systemtray, clock

* in <code>~/.fluxbox/startup</code> make sure it's content is like:

      xmodmap "~/.Xmodmap"

      which fbautostart > /dev/null
      if [ $? -eq 0 ]; then
	      fbautostart
      fi

      nm-tray &
      volumeicon &
      cbatticon &
      start fluxbox

### Option 3: JWM

      sudo apt install jwm


[Return to installation steps](debian-install.md#option-4-use-window-managers)
