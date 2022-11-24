# Setup instructions for Billy300
Billy300 is a heavily modded ender3 with direct drive afterburner, tmc2208 in a skr1.3, touchscreen and running klipper firmware.

## Fluidd/Klipper https://docs.fluidd.xyz/
Use the default image from fluidd and recompile the firmware for skr 1.3 with the following instructions: https://docs.vorondesign.com/build/software/skr13_klipper.html

Set up host_mcu: https://www.klipper3d.org/RPi_microcontroller.html
set up polkit for moonraker: https://moonraker.readthedocs.io/en/latest/installation/#policykit-permissions

There is a setting to switch the relay in gpio21 on moonraker.

## LCD screen
The lcd screen is the following:
https://www.waveshare.com/wiki/3.5inch_RPi_LCD_(A)

With added modded circuitry to control backlight brightness with pin 18 of the rpi.

```bash
cd ~/
git clone https://github.com/goodtft/LCD-show.git
cd LCD-show/
chmod +x LCD35-show
./LCD35-show
```
Screen should show console after reboot.

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

## Static ip changes
add to /etc/dhcpcd.conf
```
interface wlan0
static ip_address=192.168.1.**/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.**
```

# Prusaslicer novnc docker
Following https://github.com/helfrichmichael/prusaslicer-novnc
docker container allows to run prusaslicer on the pi.
## Set up docker

``` 
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker pi
```

Then add the user and run the docker container

``` sudo usermod -aG docker pi

And start the container:
```docker run --detach --volume=prusaslicer-novnc-data:/configs/ --volume=prusaslicer-novnc-prints:/prints/ -p 8080:8080 -e SSL_CERT_FILE="/etc/ssl/certs/ca-certificates.crt" --name=prusaslicer-novnc prusaslicer-novnc

