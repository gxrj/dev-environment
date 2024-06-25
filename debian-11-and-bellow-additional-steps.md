## Preamble

<b>Attention</b>: Debian version 11 and bellow do not come with proprietary drivers bundled in the installer so it might be run issues. This recipe is intended to help on installing those missing drivers like wifi (most important for a <code>d-i installer</code>).

<b>Warning</b>: The following recipe was applied for a machine that uses <code>atheros</code> and <code>realtek</code> wireless drivers. Ignore anything related to it if your machine does not need those and search for your missing drivers at this [link](http://ftp.debian.org/debian/pool/non-free/f/firmware-nonfree).


### Download Debian 11 iso at: 
[Debian iso folder link](https://cdimage.debian.org/cdimage/archive/11.9.0/amd64/iso-cd/)

### Download missing network driver at:
[Atheros firmware link](http://ftp.debian.org/debian/pool/non-free/f/firmware-nonfree/firmware-atheros_20210818-1_all.deb)

## Preparation steps

* Burn debian iso into Rufus software

* After the iso is burnt, open its pendrive file system and the add the missing network driver at pendrive´s <code>firmware</code> folder

* Reboot the hardware with the pendrive plugged in

## Installation steps

* Follow the steps provided and prompted by <b>expert install</b>

* At <code>Detect Network Hardware</code> step ignore missing firmwares that contais <b>cal-pci</b> or <b>pre-cal-pci</b> words

* When you get to <code>Configure Network</code> step it will try first to use the ethernet interface and then will fail

* After failing to reach internet by using ethernet interface for the first time it will display which network interface you would like to use

* Select the wireless interface and then proceed with the installation steps

* When finished, reboot and start the new installed system

## Post install wifi-setup

* After rebooting your system and logging, check if your wireless interface is already working:

      sudo iwlist scan
      
* If not, try search for your wireless network interface name:
 
      sudo iw dev
      
 Wireless interface names starts with the 'w' letter. In my example the wireless interface found was <code>wlp2s0</code> but it could be <code>wlan0</code> it may vary from each hardware/operating system.
 
 * With the wireless network interface label found (e.g. <code>wlp2s0</code>), set it up:
      
       sudo ip link set wlp2s0 up
    
* Then test if it works by scanning the available access points

      sudo iw dev wlp2s0 scan | less
    
* After finding your router, persist its credentials at <code>/etc/network/interfaces</code> for a short period
    
      sudo nano /etc/network/interfaces

* Inside this file the following commands set the wireless interface with the router credentials, those commands should be added at the end of the file

      #put the following contents in /etc/network/interfaces file:
      
      allow-hotplug wlp2s0
      iface wlp2s0 inet dhcp
          wpa-essid Put_Your_Router_SSID_Name_Here
          wpa-psk Put_Your_Router_Password_Here

<b>Warning:</b> Do no forget to *remove all those contents provided above* after install your desktop environment

* Update your wireless interface with the chosen router's credentials

      sudo ifup wlp2s0
      sudo iw wlp2s0 link
      ip a
    
* By suceeding to get an ip showed by the last command above, search for the necessary missing packages 

      sudo dmesg

## Missing driver fixes (Optional/Specific)

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

## Desktop and utilities install

Proceed the steps at [this link to install desktop and utilities](debian-install.md#systems-post-installation-steps-desktop-and-utilities)