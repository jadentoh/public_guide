# How to setup Vesta Hub and update 

1. Get IP address of the Hub connected via lan/ethernet on RDNS router
2. Log-in to Hub via Putty
   1. Generate private key 
      - Open puttygen
      - Click file 
      - Load private key
      - On the file type select 'All Files(*.*)'
      - Browse to the 'vesta-keyfile' location
      - Select the vesta-keyfile'
      - Enter the passphrase for key (see password file)
      - Click save as private key 
   2. setup and save putty config
      - Open putty
      - Click on SSH '+' on Category side 
      - Click on th Auth
      - Under Authentication parameters click Browse
      - Select the Generated private key
      - Click on Session 
      - Enter the IP address found on step 1
      - Enter the Port as 2867
      - Under Save Sessions enter a name (eg hub_login)
      - Click on the Save
   3. Login in Hub
      - Select the name (eg hub_login) 
      - Click on load
      - Click on Open
      - Enter vesta
      - Enter key file password (see password file)
3. Log-in to Hub vs Windows Terminal SSH (command line )
   1. Generate pub key 
      - Copy the vesta-keyfile to user folder/.ssh
      - cd to .ssh folder 
      - Enter the command 'ssh-keygen -y -f vesta-keyfile > keyfile_pub'
      - Enter the command 'ssh-keygen -l -f vesta-keyfile' to check the key is generated
   2. Log-in to Hub
      - Enter the command 'ssh vesta@IP_ADDR -p <PORT_NUMBER> -i .ssh\vesta-keyfile'
      - Enter key file password (see password file)
4. Transfer Ocupdater-hubctrl.zip into Hub
   1. Setup WinSCP
      - Open WinSCP
      - Click on New Site
      - Select SCP under File protocol:
      - Enter IP Address under Host name:
      - Enter 2867 under Port number:
      - Enter vesta under User name:
      - Click on Advanced 
      - Click on SSH > Authentication
      - Under Authentication parameters > Private key file :
      - Browse the generated key via puttygen
      - Click on OK
      - Click on Save
      - Enter the Site name: (eg hub_login)
      - Click OK
   2. log-in to transfer zip file
      - Select the hub_login
      - Click on Login
      - Enter key file password (see password file)
      - Browse to zip location 
      - Drag and drop to right side of the Hub directory 
      - Done
5. Move zip file to /tmp directory
   1. On the putty or windows terminal command line
   2. Enter 'mv ocupdater-hubctrl.zip /tmp/'
6. Unzip the ocupdater-hubctrl.zip
   1. On the putty or windows terminal command line
   2. Enter 'cd /tmp'
   3. Enter 'unzip ocupdater-hubctrl.zip'
7. Run Update.sh file
   1. On the putty or windows terminal command line
   2. Enter 'chmod +x update.sh'
   3. Enter './update.sh'
   4. It will run for 3-5mins
   5. The update.sh will end but the update is still run in the background
8. Check the update is done
   1. On the putty or windows terminal command line
   2. Enter 'tail -f /ocupdater/logs/oc_updater.log'
   3. Check the Current version is 0.0.902 
   4. done9. Add Z-wave device on backend
   5. On Chrome enter the IP address
   6. Log-in to the Z-wave backend (see password file)
   7. Check the top left corner anything is blinking
   8. if that is please reboot the hub and wait for 3mins
   9. re-login the Z-wave website again
   10. Should not have anything blink if have try reboot again 
   11. In the Devices should have only 1 controller 0
   12. Click add device to add the devices and follow the step shown (stay as close as possible to Hub)
   13. If the device is added to another but forgotten it will not be added
   14. Remove the device and readd again
   15. Click on More > Maintenance > remove device and follow the step shown (stay as close as possible to Hub)
   16. You can reset device on More > Maintenance

## note
1. The alarm notification timing bug 
   1. If you are in the app, you receive the correct timing in SGT
   2. If you enter the app to see alarm notification timing it will be in india timing 
   3. If you saw it in app, exit out and launch the app again it will change to india timing too.
2. In home device section swipe down to refresh not working
3. nanomote all 4 button are panic button
4. tri-sensor took 4 mins to clear motion detected and every 35seconds update motion detected
