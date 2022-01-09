
## setup for a pi-based browser kiosk

This is how I set up my pi with a 10" screen to display my Home Assistant dashboard.  On a pi3 the system boots and runs chrome rather quickly.  On an original zero with a usb wifi dongle it takes a minute or two to get to the dashboard finally, but it is quite stable and low power using a zero for a web kiosk.

### Installation

* install Raspbian 'full' version to get the desktop with gui
* run raspi-config and turn screen blanking off in 'display'
* edit /etc/xdg/lxsession/LXDE-pi/autostart

```
@lxpanel --profile LXDE-pi
@pcmanfm --desktop --profile LXDE-pi
@xscreensaver -no-splash

#------------------
# this brings up my home assistant dashboard, edit the url to taste
# you might want to try --kiosk mode as well
#------------------
/usr/bin/chromium-browser --start-fullscreen http://192.168.1.171:8123/local/tileboard/index.html

#------------------
```

* optional: remove the firstboot wizard
```
sudo apt purge piwiz -y
```

* reboot

Note - on firstboot the os will run the firstboot wizard for setting up the usual things, and there's little way around that unless you removed 'piwiz' in the optional step above.  FWIW - I configure my pi with ansible and do all the normal firstboot things scripted via ansible, so I remove the wizard to get it out of my way.
