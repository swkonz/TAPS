# TAPS Schedule Display
A rapsberry pi setup to display a single webpage upon bootup in a no desktop environment

### Materials
- Raspberry Pi Zero (would likely work for any RPi running any linux distro. Only tested with Raspian)
- Wifi connection on RPi
- Keyboard, HDMI, Monitor, mouse (all the things to actually configure the Pi)

### Process
1. Install Raspian Lite on the RPi Zero using the preset boot loader on the RPi Zero
2. Boot into the terminal, type `sudo raspi-config`
	- Change the password (default is raspberry)
	- Set the wifi network to connect to 
	- In `Boot Options > Desktop / CLI` select "Console Autologin" to ensure that the Pi boots and logs in automatically
3. Update the pi by running:
```
sudo apt-get update
sudo apt-get upgrade
```
4. In order to run a graphic program (chromium browser), we need to create an x server to launch x screens, and install a window manager
	- X.Org as our X Server
	- openbox as our Window manager
	- xdotool for simulating keystrokes
```
sudo apt-get install --no-install-recommends xserver-xorg x11-xserver-utils xinit openbox xdotool
```
5. We need to install our browser (Chromium) in order to launch the actual site
```
sudo apt-get install --no-install-recommends chromium-browser
```
6. We can now write the configuration script for openbox to launch when it starts a window. Use the script in the autologin file. Copy this file to /etc/xdg/openbox/autostart after editing the link you'd like to open up upon launch.
7. Tell the RPi to launch a window on start by editting the .bash_profile file
```
cd ~
nano .bash_profile
```
And then add the following line:
```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && startx -- -nocursor
```

Now restart the Pi and after about a 3 minute boot up (RPi Zero is slow) you should see your webpage