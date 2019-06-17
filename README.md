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
8. disconnect the ethernet and ssh over wifi to the pi (new ip address)

9. Connect the pi with thymio over a micro-usb cable
10. list connected devices on raspberry pi with `lsusb` in the ssh-console
    - Thymio is from `Swiss Federal Insitute of Technology`