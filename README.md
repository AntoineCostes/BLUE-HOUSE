# Blue House inc. since 2189
Self-service vending machine for time travelers
https://www.behance.net/gallery/135711283/Blue-House-2189

# Raspberry Setup from Buster Lite

#### update & install lightdm
`sudo apt-get update -y && sudo apt-get upgrade`
`sudo apt-get install -y lightdm`

#### configure raspberry
`sudo raspi-config`
- setup Wifi and password and hostname
- enable SSH and VNC
- disable Serial console and enable serial port
- boot console
`sudo reboot`

#### install Xorg Display Server
`sudo apt-get install --no-install-recommends xinit`
`sudo apt-get install --no-install-recommends xserver-xorg`
`sudo apt-get install raspberrypi-ui-mods`

#### setup boot
`sudo raspi-config`
- boot Desktop autologin
`sudo reboot`

## Install dependencies

`sudo apt-get install -y libbluetooth-dev` for Chataigne
`sudo apt-get install -y omxplayer` for videos
`sudo apt-get install python3-serial`for printer
`sudo apt-get install -y git cups wiringpi build-essential libcups2-dev libcupsimage2-dev python-serial python-pil python-unidecode` for thermal printer
`sudo apt-get install -y python3-pip`
`pip3 install python-osc`

## Get BlueHouse files folder in /home/pi
`sudo mv /media/pi/USBXXX/BlueHoue /home/pi/BlueHouse/`
`sudo chmod a+x /home/pi/BlueHouse/Chataigne1.8.2.AppImage`

## Setup chataigne preferences (as root)
`sudo /home/pi/BlueHouse/Chataigne1.8.2.AppImage`
- disable check updates
- disable update help
- enable load last noisette on startup
- close Chataigne
- `sudo /home/pi/BlueHouse/Chataigne1.8.2.AppImage`
open bluehouse.noisette

## Setup autostart
`cd .config`
`mkdir autostart`
`cd autostart`
`sudo nano chataigne.desktop`
>[Desktop Entry]
>Type=Application
>Name=sudo /home/pi/BlueHouse/Chataigne1.8.2.AppImage
>Exec=vncserver :1
>StartupNotify=false
```bash
sudo nano /etc/xdg/autostart/printer.desktop
```
```bash
[Desktop Entry]
Exec=lxterminal --command”/bin/bash -c ‘sudo python3 /home/pi/BlueHouse/printer_osc.py; /bin/bash’”
```
