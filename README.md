# Webserver-rethink #

# Introduction #
Since every one of us has at least one or two unused "old" smartphone laying around at home, it gave me the idea to repurpose them for future plans. Since they are no less than a small computer, with some modifiction they can be among other things e.g. web servers for smaller web based projects, or even as a network attached storage (NAS).

#Setup Guide#

/ I used for this purpose a Motorola Moto G8+, which has an official unlocking [process](https://en-us.support.motorola.com/app/standalone/bootloader/unlock-your-device-a/) support, which make work with Motorla much easier. /

1. Prepare the necessary environment on the PC (in my chase, on debian based OS(Ubuntu 22.04 jammy)):
			-	sudo apt update
			-	sudo apt install adb fastboot

2. Unlock the smartphones bootloader (**save your data beforehead, because unlocking the bootloader wipes the device**)
			- Go to settings -> About Phone -> and tap "Build numbers" 7 times, to enable developer mode.
			-	Go to Settings -> Developer Options -> Enable USB Debugging and OEM Unlocking
			- Connect the phone to yout PC via USB cable
			- Use the *adb reboot bootloader* command from the command line to boot the device into bootloader mode
			- Use the *fastboot oem unlock* command from the command line to unlock your device

3. Set up the necessary support environment:
			- [Download](https://f-droid.org/en/packages/com.termux/) and install Termux to your phone for a Linux terminal emuator for a 						covinient linux experience.
 			- Run Termux, 
     
. Set up the webserver on the smartphone:
			-       
	
