# Setup instructions for Billy300
Billy300 is a heavily modded ender3 with direct drive afterburner, tmc2208 in a skr1.3, touchscreen and running klipper firmware.

## Fluidd/Klipper https://docs.fluidd.xyz/
Use the default image from fluidd and recompile the firmware for skr 1.3 with the following instructions: https://docs.vorondesign.com/build/software/skr13_klipper.html

Set up host_mcu: https://www.klipper3d.org/RPi_microcontroller.html
There is a setting to switch the relay in gpio21 on moonraker.

## LCD screen
The lcd screen is the following:
https://www.waveshare.com/wiki/3.5inch_RPi_LCD_(A)

With added modded circuitry to control backlight brightness with pin 18 of the rpi.

```bash
git clone https://github.com/goodtft/LCD-show.git
cd LCD-show/
chmod +x LCD35-show
./LCD35-show
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
