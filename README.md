# Setup instructions for Klipper

## Prerequisites
```bash
sudo apt-get install tmux git neovim
```
edit /etc/default/locale to:
```
LANG=en_GB.UTF-8
LC_TYPE=en_GB.UTF-8
LC_MESSAGES=en_GB.UTF-8
LC_ALL=en_GB.UTF-8
```

### Static ip changes
add to /etc/dhcpcd.conf
```
interface wlan0
static ip_address=192.168.1.**/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.**
```

### Create extra user
```
sudo useradd -G tty,dialout -m -d /home/klipper pastitas
sudo usermod -a -G sudo pastitas
sudo passwd pastitas
```

## Touchscreen
The lcd dsi touchscreen is similar to https://www.waveshare.com/wiki/5inch_DSI_LCD

```bash nano /boot/config.txt
dtoverlay=vc4-kms-v3d
dtoverlay=vc4-kms-dsi-7inch
```

```bash /boot/cmdline.txt
video=DSI-1:800x480@60,rotate=90
```

The lcd touchscreen is the following:
https://www.waveshare.com/wiki/3.5inch_RPi_LCD_(A)
With added modded circuitry to control backlight brightness with PWM in pin 18 of the rpi.

```bash
cd ~
git clone https://github.com/goodtft/LCD-show.git
chmod +x LCD-show/LCD35-show
cd LCD-show/
export LC_ALL=en_GB.UTF-8
sudo ./LCD35-show lite
```
Screen should show console after reboot.

# klipper, fluidd and kliperscreen install
## Configs

```bash
cd ~
mkdir printer_data
git clone https://github.com/Pastitas/billy3000_klipper_config.git printer_data/config
```

## Kiauh
https://github.com/th33xitus/kiauh

```bash
cd ~
git clone https://github.com/th33xitus/kiauh.git 
./kiauh/kiauh.sh

```
## KAMP
https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging

```bash
cd
git clone https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.git
ln -s ~/Klipper-Adaptive-Meshing-Purging/Configuration printer_data/config/KAMP
```
## ADXL345
https://github.com/EsserPrototyping/Seeed-XIAO-with-ADXL345-for-Klipper


### Cleanup (OPTIONAL)
https://www.nerdsmith.co.uk/?p=163
```
sudo passwd -l klipper
sudo deluser klipper sudo
```

# OLD
## Fluidd/Klipper https://docs.fluidd.xyz/
Use the default image from fluidd and recompile the firmware for skr 1.3 with the following instructions: https://docs.vorondesign.com/build/software/skr13_klipper.html

Set up host_mcu: https://www.klipper3d.org/RPi_microcontroller.html
set up polkit for moonraker: https://moonraker.readthedocs.io/en/latest/installation/#policykit-permissions
There is a setting to switch the relay in gpio21 on moonraker.

## Kliperscreen https://klipperscreen.readthedocs.io/en/latest/

https://github.com/th33xitus/kiauh
plugin installer

install from the repo:
```bash
cd ~/
git clone https://github.com/jordanruthe/KlipperScreen.git
cd ~/KlipperScreen
./scripts/KlipperScreen-install.sh
ln -s /home/pi/klipper_config/KlipperScreen.conf /home/pi/KlipperScreen/
```
It should work straight away, if the config file does not exist these commands get the default:
```bash
cp ~/KlipperScreen/ks_includes/KlipperScreen.conf ~/klipper_config/
ln -s /home/pi/klipper_config/KlipperScreen.conf /home/pi/KlipperScreen/
```


