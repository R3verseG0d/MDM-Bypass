# MDM-Bypass
This is a method for bypassing MDM using the checkra1n exploit.

This method assumes you have a checkra1n vulnerable device and assumes that you have access to macOS. 

Tools: 
checkra1n: https://checkra.in/
Apple Configurator: https://apps.apple.com/us/app/apple-configurator/id1037126344?mt=12
Terminal knowledge
Homebrew: https://brew.sh/
iproxy and usbmuxd
My mobile config file.

Setup:
After installing homebrew, you'll need to run the following.
brew install iproxy
brew install usbmuxd

Now you'll want to go ahead and jailbreak your iDevice with checkra1n. Follow the on screen prompts to jailbreak. The device needs to be activated!
Now you'll want to SSH into the device. To do this follow the following steps.

Run 'iproxy 2222 44' (Feel free to play around with the number if you get an error. In my case 2222 didn't work but 2022, 2002 and 2202 did. If you get an error then play around with the number.)
Then run in another terminal tab or window 'ssh root@localhost -p 2222' NOTE: This number will be whatever you put into the iproxy command. The number has to match.
When prompted follow the on screen prompt and type 'yes'
You will be prompted for a password. The password is alpine.
Once in, you should be in root. If you're not in root then navigate there by typing 'cd /'
Now navigate to the location where the current MDM profile is. You can do so by typing 'cd /private/var/containers/Shared/SystemGroup/'
Once inside this directory run 'rm -rf systemgroup.com.apple.configurationprofiles/'
Now you should see in settings that the MDM profile is removed. You are not done yet because as soon as you reboot, the jailbreak will be cleared and the MDM profile may be reinstalled.
Now that the current MDM profile is removed, open Apple Configurator and navigate to your iDevice. Double click on it and you should see the device info and a list of tabs on the left. Download the MDM profile from this repo. This will be your new DeviceManager.mobileconfig. Once you have that you can proceed. Click on Profiles and Add Profile. Import the MDM profile and follow the on screen instructions. You will need to install it from Settings on your iDevice (General/Profile). Click install when prompted. 

This MDM profile will block the installation of any new MDM profiles including after the device reboots effectively kicking the old MDM off of the device Persistently. I also added settings to block connections to apple.com but I can still connect to apple's website. I haven't tested it with iCloud yet. I will ammend this readme when I do. 
