Object Detection on Google AIY Vision Kit
=========================================

Modified from the included AIY Joy detection demo.

Instead of detecting faces, this detects cats, dogs and humans in real time
from the Pi Camera module.

Brief Instructions
------------------

1. Start off from  Raspbian Buter Lite (image)[https://www.raspberrypi.org/downloads/raspbian/]
2. `touch ssh` on boot partition
3. Edit `config.txt`, add/uncomment:
```
dtparam=i2c_arm=on
dtparam=spi=on

start_x=1
gpu_mem=128
over_voltage=4
force_turbo=1
```
4. SDCard can be used now
5. Add AIY repo and update (more
   (details)[https://github.com/google/aiyprojects-raspbian/blob/aiyprojects/HACKING.md])
```
echo "deb https://packages.cloud.google.com/apt aiyprojects-stable main" | sudo tee /etc/apt/sources.list.d/aiyprojects.list
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-get update
sudo apt-get upgrade
```
6. reboot
7. Install packages
```
sudo apt-get install -y leds-ktd202x-dkms
sudo apt-get install -y pwm-soft-dkms
sudo apt-get install -y aiy-usb-gadget
sudo apt-get install -y aiy-bt-prov-server

sudo apt-get install -y aiy-vision-dkms
sudo apt-get install -y aiy-models
sudo apt-get install -y aiy-python-wheels
```
8. reboot
9. Check myraid
```
dmesg | grep -i "Myriad ready"
```
10. Check camera over network stream
```
ssh pi@raspberrypi.local "raspivid --nopreview --timeout 0 -o -" | ffplay -loglevel panic -
```
11. Clone AIY repo (optional, maybe run tests)
12. Clone this repo
13. run the setup script

Notes
-----

If not using the pre-built image, and starting from a bare minimal raspbian,
`libopenjpg2-7-dev` is required for the unit tests in the AIY project to run.
Also, `/opt/aiy/models` needs to be symlinked to `/home/pi/models`.

Additionally, starting this service (and the joy detection demo) needs:

- `avahi-utils`
- `fonts-freefont-ttf`

Troubleshooting
---------------

Some Pi Zeros W seems to crash whenever the camera is started in video mode.
adding `force_turbo=1` and `over_voltage=4` to `config.txt` seems to fix this.
