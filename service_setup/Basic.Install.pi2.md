### Instructions for setting up your Raspberry PI
##### Mesh with a friend today!
___
A Raspberry Pi 2 may be used as a meshnet node by installing the necessary software. The steps below describe how this may be done.

1. Download Raspbian

Raspbian is a Linux distribution customized for the Raspberry Pi.  It may be downloaded from https://www.raspberrypi.org/downloads/raspbian/

From the Downloads page select Zip downloads under Raspbian Jesse Lite. The Download Torrent option may also be used but requires a bittorrent client.

Information on this page regarding “NOOBS” may be disregarded as we will not be using that system.

The downloaded file should have an .zip extension. It must be extracted to the SD card correctly so that the Raspberry Pi may be booted from it. 

2. Unzip the image file
Various applications may be used to unzip. 7-zip is one common example:
PC/MAC/Linux:
http://www.7-zip.org/download.html

Unzip the .zip file and extract it to the location of your choice on your local computer hard drive. Once extracted the image file will display an .img extension.


3. Create a Bootable SD card

Once the image file has been unzipped, the resulting .img file must be loaded onto the sd card properly so that the Raspberry Pi can boot from it. 
Raspberrypi.org provide instructions for doing this at the following locations: 
[Linux](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md)
[MAC](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)
[Windows](https://www.raspberrypi.org/documentation/installation/installing-images/windows.md)

4. Boot Raspbian
Connect any peripherals to the Pi such as keyboard/mouse/display and ethernet. 
A live internet connection will be needed to download the mesh software. 

a. Insert the sd card into the PI’s on board card reader and connect power. 

b. Once the bootup sequence completes you will see the Raspberry Pi desktop. You’ve installed Raspbian.

5. Install the mesh software.
TOMESH software can be installed either using the graphical desktop or by logging into the node remotely using SSH, user: **pi** and password **raspberry**. 
If using the desktop, click the terminal icon to launch a command prompt.
 desk.png 

At the prompt, enter/paste the following line of commands:
```
wget https://raw.githubusercontent.com/tomeshnet/prototype-cjdns-pi2/master/scripts/install && chmod +x install && ./install
```
After a few minutes of compiling, the scripts will complete and cjdns will automatically be launched (cjdroute). The user will be logged out of the system if using SSH but can log back in immediately.
6. Uninstall
To uninstall the software, run the script at the location below:
```
prototype-cjdns-pi2/scripts/uninstall
```
This will remove all symlinks, after which the cjdns and prototype-cjdns-pi2 folders may be deleted.