# MVI Edge 8.4 Installation on NVIDIA Jetson Xavier NX

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
  2. Shut Down the VM. On VMWare Fusion under the list of Virtual Machines hold CTRL + Right Click on the VM to display the 'Show Config File in Finder' option. Select it to be brought to the VM's .vmx file. Open up the .vmx file with TextEdit and add `biosbootDelay="5000"` to the top of the file then hit Save.
  3. Back on VMWare Fusion, Right Click the VM and go to Settings. Select CD/DVD (SATA) and from the dropdown you'll want to Choose Disc or Image and grab the GParted ISO. Once you've done that, go back to Settings and select Hard Disk (SCSI). Drag the slider to increase the Disk Size to ~ 75GB and hit Apply. You can now close out of the Settings. 
  4. 
