# Setup instructions for Billy300
Billy300 is a heavily modded ender3 with direct drive afterburner, tmc2208 in a skr1.3, touchscreen and running klipper firmware.

## LCD screen
The lcd screen is the following:
https://www.waveshare.com/wiki/3.5inch_RPi_LCD_(A)

With added modded circuitry to control backlight brightness with pin 18 of the rpi.


```bash
cd ~
git clone https://github.com/goodtft/LCD-show.git
chmod +x LCD-show/LCD35-show
cd LCD-show/
sudo ./LCD35-show lite
```
Screen should show console after reboot.

## Static ip changes
add to /etc/dhcpcd.conf
```
interface wlan0
static ip_address=192.168.1.**/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.**
```

# klipper, fluidd and kliperscreen install
## Configs

```bash
cd ~
git clone https://github.com/Pastitas/billy3000_klipper_config.git klipper_config
```

## Kiauh
https://github.com/th33xitus/kiauh

```bash
cd ~
git clone https://github.com/th33xitus/kiauh.git
./kiauh/kiauh.sh

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
