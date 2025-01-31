# Webserver-rethink #
![PHP Webserver](https://www.zend.com/sites/default/files/image/2023-07/image-zend-getting-started-php-linux.jpg)

**Introduction:**

Since most of us have at least one or two unused "old" smartphone lying around at home, it gave me the idea to repurpose them for future projects. Since they are essencially small computers, with some modification they can othe puposes e.g. web servers for smaller web based projects, or even as a network attached storage (NAS). 
_For this purpose I used a Motorola Moto G8+, which has an official unlocking [process](https://en-us.support.motorola.com/app/standalone/bootloader/unlock-your-device-a/) support, which making to work with Motorola devices much easier._

## Setup Guide: ##

**1.** Prepare the necessary environment on the PC (in my chase a debian based OS(Ubuntu 22.04 jammy)):
- `sudo apt update`
- `sudo apt install adb fastboot`

**2.** Unlock the smartphone's bootloader (**back up your data beforehandd, as unlocking the bootloader will wipe the device**):
- Go to **Settings** -> **About Phone** -> and tap **Build number** 7 times, to enable developer mode.
- Go to **Settings** -> **Developer Options** -> **Enable USB Debugging** and **OEM Unlocking**.
- Connect the phone to yout PC via USB cable
- Verify the device connections with the `adb devices` command.
- Use the `adb reboot bootloader` command from the command line to boot the device into bootloader mode
- Use the `fastboot oem unlock` command from the command line to unlock your device
- Verify bootloader unlock with `fastboot gervar unlocked`command.
	- If it says: `unlocked: yes`, you're good to go.

**(3. Optional)Remove unwanted software(Bloatware)**
As your old phone now will have a new purpose, you may wan to clean it up from unnecessary pre installed softwares, which would be only acting as bloatwares (like android auto, AR Emoji, Bixby, etc.)

- Connect your phone to the PC via USB
- Go to **Settings** -> **Developer Options** -> **Enable USB Debugging**
- Verify the device connections with the `adb devices` command.
- List all installed packages with `adb shell pm list packages` command.
- Uninstall the selected app permanently:
	- `adb shell pm uninstall -k --user 0 <package_name>`
		- Example: `adb shell pm uninstall -k --user 0 com.facebook.katana`
    	


**4.** Set up the necessary environment on the phone:
- **(Optional)** [Download](https://solid-explorer-file-manager.en.uptodown.com/android)  **Solid Explorer File Manager** for a convenient file management (or config file handle instead of using nano).   
- [Download](https://f-droid.org/en/packages/com.termux/) and install **Termux** to your phone a Linux terminal 			  emuator for a lightweight Linux experience.
	- Run Termux:
   		- Since Termux could not handle a full LAMP environment (as it does not officially support the **libapache2-mod-php** package which is essential for Apache to process PHP correctly) we are going with PHP's built-in server solution instead.    
   		- Install the necessary packages:
			- `pkg update`
			- `pkg upgrade`
   			- `pkg install php mariadb`
   		- Read out your phone's IP address with the `ifconfig` command, and look for an IP adress similar to this: "**192.168.1.1**".
   		- Create the directory for your website (for the necessary files):
			- `mkdir ~/mywebsite`
- Copy the necessary files and resources (e.g. "index.php") for your project to your directory (from your PC via cable).    	 
     
**5.** Set up the [PHP webserver](https://www.php.net/manual/en/features.commandline.webserver.php) on the smartphone:
- Run Termux
	- Run the PHP webserver with **your** IP address: `php -S 192.168.1.1:8000 -t ~/mywebsite`
 		- The -S argument starts a embedded web server from the php executable.
   		- ":8000" is necessary to run the server on this port
     	- The -t argument specify the root directory the server should use (in this chase ~/mywebsite)
  
- For local testing environment run: `http://localhost:8000/index.php` on your phones browser.
  		
      	 
**6.** If you started the server using **your** IP address, you should be able to access to your project from any device in your local network with the following example URL in your browser: `http://192.168.1.1:8000/index.php`.  
