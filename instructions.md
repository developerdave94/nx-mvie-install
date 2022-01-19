# MVI Edge 8.4 Installation on NVIDIA Jetson Xavier NX

</br>

## Setting Up the Host VM
Insert Description
> NOTE

### Obtaining VMWare Fusion 12 Pro (OPTIONAL)
> NOTE: This step is only required if you DO NOT have access to VMWare Fusion.
  1. Send an email to atwreqs@us.ibm.com with the following information to request access to VMWare Fusion 12 Pro.</br>
    a. Job Role (ex. Solutions Engineer)</br>
    b. Request Reason (ex. MVI Edge Client Demo Install)</br> 
    c. Lotus Notes ID (ex. John Doe/Location/IBM)</br>
    d. Operating System (ex. MacOS)</br>
  2. Within 3 days you'll receive an email containing a license key and a link to download VMWare Fusion 12 Pro. Download the software and upon configuration you'll be prompted to enter you license key. 

### Creating an Ubuntu 18.04 VM
  1. Download the Ubuntu 18.04.6 LTS (Bionic Beaver) Desktop Image ISO from the following site (https://releases.ubuntu.com/18.04/).
  2. Launch VMWare Fusion and in the top right corner hit the Plus Sign and select New. From there you'll be asked to select the Installation Method. Drag and drop the recently downloaded ISO to where it says 'Install From Disc or Image'. The ISO should now appear under the Create New Virtual Machine window. Hit Continue.
  3. Provide a Display Name, Account Name, and Password. Choose anything you'd like, but it's recommended to keep it simple (ex. ubuntu). Hit Continue and Finish. Save the VM as 'ubuntu-18.04.6' in the Virtual Machines folder and hit Save. Your VM should start building immediately and once finished, go ahead and login.     

### Using GParted to Increase Disk Space
  1. Download the GParted 1.3.1 AMD64 ISO from the following site (https://gparted.org/download.php) to your PC.
  2. Open up the Terminal on the VM and type `df -h` to get the name of the Filesystem Root. It should appear as `/dev/sda(x)`. 
  3. Shut Down the VM. On VMWare Fusion under the list of Virtual Machines hold CTRL + Right Click on the VM to display the 'Show Config File in Finder' option. Select it to be brought to the VM's .vmx file. Open up the .vmx file with TextEdit and add `biosbootDelay="5000"` to the top of the file then hit Save.
  4. Back on VMWare Fusion, Right Click the VM and go to Settings. Select CD/DVD (SATA) and from the dropdown you'll want to Choose Disc or Image and grab the GParted ISO. Once you've done that, go back to Settings and select Hard Disk (SCSI). Drag the slider to increase the Disk Size to ~ 75GB and hit Apply. You can now close out of the Settings. 
  5. Start the VM and while booting, click inside the VM while repeatedly pressing F2 to be brought to the BIOS. Tab over to the Boot page using the Arrow keys and go down to where it lists CD-ROM Drive. Hit the (+) key to move it to the top of the list. Once you've done that, tab over to Exit and then go down to Save Changes and hit Enter twice. Finally, press F10 and Enter to boot.
  6. GParted should immediately launch. Hit Enter to go with the Default Settings, then press Enter 3 more times to continue with the defaults. You will now be brought to a page where you can view your /dev/sda1 partition. 
  7. Select the /dev/sda1 partition and then click the Resize/Move option. Increase the New Size from ~ 20GB to ~ 65GB and then hit Resize/Move. To apply the changes, hit the green Apply Check Mark and Apply. To exit, click GParted in the top left corner then select Quit. 
  8. Restart the Virtual Machine and upon restarting, click inside the VM while repeatedly pressing F2 to be brought back to the BIOS. Tab over to the Boot page using the Arrow keys and go down to where it lists Hard Drive. Hit the (+) key to move it to the top of the list. Once you've done that, tab over to the Exit and then go down to Save Changes and hit Enter twice. Finally, press F10 and Enter to boot.
  9. Open up the Terminal and type `df -h` to validate that /dev/sda1 was increased. The output should look like `/dev/sda1   63G   5.8G    54G   10%   /`. 

</br>

## Flashing the Jetson Xavier NX

### Preparing and Executing the Flash
  1. On the VM, download the following .zip file (https://ibm.box.com/v/ssd-disk-mount). Once the download is complete, Right Click the .zip and Extract this to the Desktop location. This should expose the MIC-710AIX_NX_4.6_V0.2_DiskFlash.tbz2 file.
  2. Open up the casing surrounding the Jetson Xavier NX to expose the Micro USB and REC Button (as shown below).</br>  
![Hatch Internals](images/hatch_internals.png)  </br>
  3. Use the following sequence to put the Jetson NX into Recovery Mode:</br>
    a. Unplug the Jetson NX Power Cable</br>
    b. Connect your PC to the Micro USB Port</br>
    c. Hold the REC Button while plugging in the Power Cable</br>
    d. Continue to hold the REC Button for 5s</br>
    e. Release the REC Button</br>
  4. Your PC should then ask whether you'd like to Connect to PC or Connect to Linux. Select Connect to Linux. To confirm that the Jetson NX is connected, open up the Terminal on the VM and type `lsusb`. The output should show something similar to this `Bus Device 003 ID: 0955:7e19 NVidia Corp.`.
  5. In the Terminal, type `cd Desktop` and `sudo tar xvpf MIC-710AIX_NX_4.6_V0.2_DiskFlash.tbz2` to extract the BSP. Once you've done that, type `cd MIC-710AIX_NX_4.6_V0.2` and `sudo ./nvmflash.sh`. This should begin the flash process which takes about 15 to 20 mins. It should look as follows `Start flashing device: 1-2, PID: XXXX   Ongoing processes: XXXX`.
  6. During the boot process, you'll notice a prompt asking you to Select a Storage to Boot or Install OS. Enter `2` which is the dev/sda. Let the boot process continue until you're brought to the home screen.
  7. Validate that the /dev/sda (which represents the attached SATA SDD) is mounted as the Filesystem Root by typing `df -h` into the Terminal on the Jetson NX. You should see something like this `/dev/sda1  229G  14G 204G  7%  /`.
