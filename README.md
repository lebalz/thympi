# Setup Raspberry Pi

1. Download [raspbian .zip](https://www.raspberrypi.org/downloads/raspbian/) and follow the instructions to flash to `.img` to an sd card
2. initial setup over screen
    - setup ssh: `sudo systemctl enable ssh && sudo systemctl start ssh`
3. Copy the aseba: Copy `aseba_1.5.5_armhf.deb` to `/home/pi` (if there is a newer build,download it from [here](http://wiki.thymio.org/en:linuxinstall))
4. put the sd card in the raspberry pi, boot it up. Make sure your raspberry is connected via ethernet to your local network.
5. ssh to your pi : `ssh pi@<local-ip-address-of-pi>`, the default raspbian password is `raspberry`
6. install aseba and it's dependencies:
    - `sudo dpkg -i aseba_1.5.5_armhf.deb`
    - `sudo apt-get update && sudo apt-get -f install`
    ```sh
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install --no-install-recommends xserver-xorg
    sudo apt-get install --no-install-recommends xinit
    sudo apt-get install raspberrypi-ui-mods
    sudo apt-get install --no-install-recommends raspberrypi-ui-mods lxterminal gvfs
    sudo apt-get install rc-gui
    ```
    - `sudo apt-get install python-dbus` (dbus)
    - `sudo apt-get install python-gtk2` (glib)
    - 
7. connect to the local wifi: run `sudo raspi-config`, go to *Network Options* and follow instructions.
8. disconnect the ethernet and ssh over wifi to the pi (new ip address). To get all ip addresses of connected network devices, use either
    - the userinterface of your router. Visit the local ip address of your network with a browser, usually it is `192.168.1.1`. Usually there you'll find an option to show all connected network devices and it's ip's. 
    - or use `nmap` in a shell:
        ```sh
        nmap -sn 192.168.1.1-254/24 | egrep "scan report" | awk '{print $6 " -> " $5}'
        ```
        (you may need to install it with `sudo apt-get install nmap`)


9. Connect the pi with thymio over a micro-usb cable
10. list connected devices on raspberry pi with `lsusb` in the ssh-console and check if the thymio is listed
    - Look for `Swiss Federal Insitute of Technology` (yes, there is a typo...)

The Setup is done, now we can start to code

## Setup development environment

[VS Code Insiders](https://code.visualstudio.com/insiders/) provides an easy way to develop and even debug directly on the raspberry pi. Download and install vs code locally on your machine. Open it and install the following extension:
- [Remote - SSH (Nightly)](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh-nightly)