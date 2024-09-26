## System's minimal installation steps

- <b>Download Rufus Iso burner at:</b> [Rufus link](https://rufus.ie/en/)

### Steps for installing versions prior to Debian 12 
- [Click me to access the recipe for installing older Debian versions](debian-11-and-bellow-additional-steps.md)

### Steps for installing the current version of Debian

- <b>Download stable version of Debian iso at:</b> 
[Debian iso folder link](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)

## System's post installation steps (desktop and utilities)

Debian provides a wide selction of desktop and window managers, the following options are minimal selections of packages for a comfortable usage for low and midium budget hardware:

### Option 1: KDE Plasma 5

* For <code>kde-plasma</code> and its the minimal set of utilities:

      sudo apt install kde-plasma-desktop kdeconnect- plasma-nm papirus-icon-theme -y
      sudo apt install ark kwrite gwenview qapt-deb-installer okular okular-extra-backends -y

* The following command sets <code>kde-plasma theme</code> for <code>libreoffice</code>:

      sudo apt install libreoffice-kf5

### Option 2: XFCE4

* For <code>xfce4</code> and its the minimal set of utilities:

      sudo apt install xfce4 xfce4-power-manager xfce4-battery-plugin xfce4-terminal nm-tray lightdm slick-greeter -y
      sudo apt install gdebi unzip mousepad atril menulibre papirus-icon-theme greybird-gtk-theme blackbird-gtk-theme -y

* The following command sets <code>gtk theme</code> for <code>libreoffice</code>:

      sudo apt install libreoffice-gtk

### Option 3: LXQt

* For <code>lxqt</code> and its the minimal set of utilities:

      sudo apt install openbox nm-tray papirus-icon-theme -y
      sudo apt install lxqt-core qterminal xfwm4*- xarchiver- xscreensaver- gnome*- diodon- -y
      sudo apt install ark qpdfview lightdm slick-greeter dmz-cursor-theme -y

* Persist custom cursor size

      echo 'Xcursor.size: 28' >> ~/.Xresource

* To set brightness control [click me](lxqt-brightness.md)

## Hardware clock settings for dualboot

* Set the system to local time if you have dualboot
   
      sudo timedatectl set-local-rtc 1

## Removing static wifi credentials

* Delete the following content from <code>/etc/network/interfaces</code> file

      allow-hotplug wlp2s0
      iface wlp2s0 inet dhcp
          wpa-essid Put_Your_Router_SSID_Name_Here
          wpa-psk Put_Your_Router_Password_Here

* Refresh NetworkManager configuration
  
      sudo service NetworkManager restart

* Reboot the system if you will (Optional)

      sudo init 0

## Changing GRUB's boot order

* If your hardware is a dualboot and you want to change grub order, then

      sudo mv /etc/grub.d/30_os-prober /etc/grub.d/09_os-prober && sudo update-grub  

* If your are using UEFI <i>configure the bootloader at the BIOS</i>
