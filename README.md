Object Detection on Google AIY Vision Kit
=========================================

Modified from the included AIY Joy detection demo.

Instead of detecting faces, this detects cats, dogs and humans in real time
from the Pi Camera module.


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
