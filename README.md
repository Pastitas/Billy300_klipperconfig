# Setup instructions for Billy300
Billy300 is a heavily modded ender3 with skr1.3, direct drive bmg extruder,tmc2208, rpi and screen and klipper.

## Fluidd/Klipper https://docs.fluidd.xyz/
Use the default image from fluidd and recompile the firmware with the following instructions: https://www.voron.dev/home/voron-2-2-supplement/skr-1-3-configuration/SKR%201.3%20Setup%20Guide.pdf
There is a setting to switch the relay in gpio21 on moonraker.

## LCD screen
The lcd screen is the following:
https://www.waveshare.com/wiki/3.5inch_RPi_LCD_(A)

With added modded circuitry to control backlight brightness with pin 18 of the rpi.

```bash
git clone https://github.com/goodtft/LCD-show.git
chmod -R 755 LCD-show
cd LCD-show/
```
Screen should show console after reboot.

## Kliperscreen https://klipperscreen.readthedocs.io/en/latest/

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
