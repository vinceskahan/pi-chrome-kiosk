
## setup for a pi-based browser kiosk

This is how I set up my pi with a 10" screen to display my Home Assistant dashboard.  On a pi3 the system boots and runs chrome rather quickly.  On an original zero with a usb wifi dongle it takes a minute or two to get to the dashboard finally, but it is quite stable and low power using a zero for a web kiosk.

### Prerequisites

These instructions assume that:
* you are familiar with installing a pi
* you know how to get it onto your wired or wifi network
* you can edit a simple text file with any editor of your choosing
* you remember to preface commands with `sudo` as needed

### Installation

Image the SD card:

* install Raspbian 'full' version to get the desktop with gui.  I use Balena Etcher on a Mac to image the SD card.
* enable remote ssh access to your pi
** eject the SD card and put it back into your host that you imaged it on
** simply 'touch' a file named 'ssh' in the /boot directory of the SD card you imaged
** eject the SD card

At this point you can boot the pi:

* log in as the default user 'pi' with the default os password of 'raspberry'
* when prompted, change your default password to something non-trivial that you can remember
* turn off run `sudo raspi-config` and turn screen blanking off in 'display'
* remove the firstboot wizard by running `sudo apt purge piwiz -y`
* edit `etc/xdg/lxsession/LXDE-pi/autostart` with your editor of choice.  Use sudo.

```
@lxpanel --profile LXDE-pi
@pcmanfm --desktop --profile LXDE-pi
@xscreensaver -no-splash

#---------------------------------------------------------------------------------
#  Add the following line to run a browser at boot
#
# this example brings up my home assistant dashboard, edit the url to taste
# you might want to try --kiosk mode as well to see if you like that look'n'feel
#

/usr/bin/chromium-browser --start-fullscreen http://192.168.1.171:8123/local/tileboard/index.html

#---------------------------------------------------------------------------------

```

* sudo reboot

At this point the pi should reboot and run the Chromium browser automatically.

