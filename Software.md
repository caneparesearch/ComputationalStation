

# Creating mini cluster with Raspberry Pi 5 and Rocky Linux

## Basic materials 
-Raspberry Pi 5 and Raspberry Imager
-Monitor, Mouse and Keyboard
-5-port gigabyte desktop switch 
-Ethernet, Raspberry Pi HDMI, and Raspberry power cables
-Sd card (Running Rocky Linux)
-Rocky Linux file

## Installing Rocky Linux onto the SD
Firstly you're going to need to install Rocky Linux onto the SD/USB using this file [here](https://rockyrepos.gnulab.org/RockyRpi-sda.raw.xz). It's the only version we've found that currently works right off the bat when you use the Raspberry Pi imager (Which you can install from [here](https://www.raspberrypi.com/software/) if you don't have it).

After you've downloaded the file and have downloaded the Raspberry Pi imager, you'll need to select the Raspberry Pi 5, select "custom" and choose the file, then select the USB/SD you'll be installing Rocky Linux onto. Once verified and the imager tells you to remove the storage device, you'll have Rocky Linux ready to be opened on the Raspberry Pi.

## Post-Installation
If everything's done right, you should now be seeing a bare-bones version of Rocky with the terminal telling you to sign in (Username: rocky, Password: rockylinux).

There are a few key things you're going to need to do next. Changing the keyboard mapping (if you want to of course), Connecting to the internet, Expanding the partition, Changing the password, and Installing the desktop environment.

### Changing the keyboard
Whether you prefer a different key-map setup, or you're from a different part of the world, you're comfort is important. So here's how to change the key-mapping to what you like.


$ <localectl> (Check current settings)
$ <localectl list-keymaps> (List the other available keyboard layouts)
$ <localectl set-keymap> <keymap> (Set new keyboard layout, for example: [$ localectl set-keymap fr])

Once you change your keyboard layout to whatever you like you can move on! Just remember these commands for when you want to come back and change the layout again.


### Connecting to the Internet
To connect the raspberry Pi to the internet, you'll need a desktop switch and a few ethernet cables. You're going to connect one cable to a router/modem and into the switch, then you're going to connect the other into the switch and out into the Pi5. This should allow for your Pi5 to automatically get an IP address assigned (this, of course, is if you have a network with a DHCP server enabled).

#### commands for checking IP
If you want to check and make sure you're computer is connected to the internet, and has an IP, simply use the command <$ ip a>

If you're trying to connect using Wi-Fi, you're going to need a Wi-Fi dongle.

Afterwards you're going to use the command <$ sudo nmtui> and enter the "rockylinux" password (if asked). You're going to choose "Activate a connection" and looks through the list of networks till you find yours. Enter your wifi password and you should be connected.

### Expanding the partition
Your disk size isn't gonna match the SD/USB capacity, this needs to be fixed. 

#### Commands for partition expansion
Use the command <$ sudo rootfs-expand> in order to make the root partition use all of the hard drive space

### Changing the password
To change the password from the default one, you're going to use the command <$ passwd> followed by inputting the current password twice and the new password twice.

### Installing a desktop environment on Rocky Linux
So, as you've probably noticed, Rocky is only in server edition. But you can install a desktop environment on it!

#### Commands for Installation
You're going to use the command <$ sudo dnf group list> to see all the packages/environments. There will be one titled "Server with GUI". That is the one that's going to be the desktop environment. 

Now that we know the environment is there, we're going to us the command <$ sudo dnf group install "Server with GUI">. Give it a minute to install and answer the questions that pop up after the download phase. After about 15-20 minutes (or less) use the command <$ sudo reboot> and see the results of your labor!

You should now be seeing a full desktop environment!
