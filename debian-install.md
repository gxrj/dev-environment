## Preamble

<b>Warning</b>: The following recipe was applied for a machine that uses <code>atheros</code> and <code>realtek</code> wireless drivers. Ignore anything related to it if your machine does not need those and search for your missing drivers at this [link](http://ftp.debian.org/debian/pool/non-free/f/firmware-nonfree).

### Download Debian non-free iso at: 
[Debian Version 11.5 link](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/current/amd64/iso-cd/firmware-11.5.0-amd64-netinst.iso)

### Download missing network driver at:
[Atheros firmware link](http://ftp.debian.org/debian/pool/non-free/f/firmware-nonfree/firmware-atheros_20210818-1_all.deb)

### Download Rufus Iso burner at:
[Rufus link](https://rufus.ie/en/)

## Installation steps

* Burn debian iso into Rufus software

* After the iso is burnt, open its pendrive file system and the add the missing network driver at pendrive´s <code>firmware</code> folder

* Reboot the hardware with the pendrive plugged in

* Proceed the steps

* At <code>Detect Network Hardware</code> step ignore missing firmwares that contais <b>cal-pci</b> or <b>pre-cal-pci</b> words

* When you get to <code>Configure Network</code> step it will try first to use the ethernet interface and then will fail

* After failing to reach internet by using ethernet interface for the first time it will display which network interface you would like to use

* Select the wireless interface and then proceed with the installation steps

* When finished, reboot and start the new installed system

* Add your credentials, then use the following commands to make wireless interface work:

      sudo iwlist scan
      sudo iw dev
      sudo ip link set wlp2s0 up
    
* Then scan the available access points

      sudo iwlist scan | less
    
* After finding your router, persist its credentials at <code>/etc/network/interfaces</code> for a short period
    
      sudo nano /etc/network/interfaces

* Inside this file the following commands set the wireless interface with the router credentials, those commands should be added at the end of the file

      allow-hotplug wlp2s0
      iface wlp2s0 inet dhcp
          wpa-essid Put_Your_Router_SSID_Name_Here
          wpa-psk Put_Your_Router_Password_Here

* Update your wireless interface with the chosen router's credentials

      sudo ifup wlp2s0
      sudo iw wlp2s0 link
      ip a
    
* By suceeding to get an ip showed by the last command above, search for the necessary missing packages 

      sudo dmesg

In the example used to install debian, the missing firmwares were: <code>rtl_nic/rtl8168h-2.fw</code>, <code>ath10k/pre-cal-pci-0000:02:00.0.bin</code>, <code>ath10k/cal-pci-0000:02:00.0.bin</code> and <code>i915/icl_dmc_ver1_09.bin</code>. So use <code>apt-cache search</code> command followed by the firmware's name to find the correspoding package as it follows:<br>

* <code>firmware-realtek</code> package contains <b>rtl_nic/rtl8168h-2.fw</b> driver

      sudo apt-cache search rtl_nic/rtl8168h-2.fw
      sudo apt install firmware-realtek
      

* <code>firmware-misc-nonfree</code> package contains <b>search i915/icl_dmc_ver1_09.bin</b> driver

      sudo apt-cache search i915/icl_dmc_ver1_09.bin
      sudo apt install firmware-misc-nonfree

* <code>firmware-atheros</code> package contains <b>ath10k/pre-cal-pci-0000:02:00.0.bin</b> and <b>ath10k/pre-cal-pci-0000:02:00.0.bin</b> drivers
      
      sudo apt-cache search ath10k/
      sudo apt install firmware-atheros
      
* Install your desired packages like desktop environment and other things, in this case its installing kde plasma desktop environment and other utilities

      sudo apt install kde-plasma-desktop plasma-nm ark kwrite gwenview qapt-deb-installer okular okular-extra-backends -y
      sudo apt purge kdeconnect -y

* Set the system to local time if you have dualboot
   
      sudo timedatectl set-local-rtc 1
   
* Reboot the system if you will (Optional)

      sudo init 0

* Delete the wireless interface's configuration previous added (mainly the router credentials) and reset the wireless interface

      sudo nano /etc/network/interfaces
      sudo service NetworkManager restart

* If your are using UEFI configure the bootloader at the BIOS
