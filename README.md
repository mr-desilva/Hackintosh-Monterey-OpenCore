# Hackintosh-Ventura-OpenCore
 Acer-Swift3-SF31552G Hackintosh Ventura Guide using Opencore. You can dual boot both windows and macOS using this guide seamlessly. Kext and patches may different from laptop model, I recommend you to follow [OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/) to understand your hardware and gather necessary files.

<img src="https://github.com/mr-desilva/Hackintosh-Ventura-OpenCore/blob/main/images/home.png">
 
 # What's new ?
 Main problem with the opencore guide is that you will require a internet connection for downloading the macOS within the recovery process. Unlike the traditional method of opencore, this guide can help you to setup a hackintosh without using the macOS Recovery method. You will requires following.

- Downloaded macOS dmg
- Pre configured EFI folder
- USB drive (minimum of 16GB)


# Creating the bootable macOS

1. Download the desired macOS dmg from a trusted source. [Visit Olarila](https://www.olarila.com/)
2. After downloading the dmg, you need to use the [balenaEtcher](https://www.balena.io/etcher/) to create a bootable macOS. Drag and drop the downloaded dmg to the USB drive. (Alternatively you can use [Rufus](https://rufus.ie/en/) )
3. Next you need to mount the EFI partition of the bootable drive. Use a partition software and assign a letter to mount the EFI partition. Recommended -> [MiniTool](https://www.partitionwizard.com/free-partition-manager.html)
4. Next you need to open the mounted EFI partition. You cannot use the windows file explorer, it will give you a "permission denied" warning. If you are using windows you can try [Explorer++](https://explorerplusplus.com/) to open the mounted EFI partition (Run as administrator).
5. Copy and paste the pre configured EFI folder to the bootable drive.
6. Now we have completed the creating the bootable drive.

----------
# Installation
1. Make these changes to the BIOS- first. For dual booting windows won't work with `Sata Mode : AHCI` . You need to change back the `Sata Mode : RST with OPTANE` to boot windows.
    - Sata Mode - AHCI 
    - Secure BOOT - Disabled

2. Boot from the bootable drive and select install macintosh.
3. In the macOS installer, go to disk utility and create a partition to install the macOS. Format the partition with following settings.
    - Format - APFS
    - Scheme - GUID Partition Map
    
    Troubleshooting - If you cannot see the disk, go to view and select `Show All Devices`, make sure your disks partition scheme is GPT. You cannot use MBR. You can use MiniTool to change the partition scheme from MBR to GPT.
4. Goto install macOS and select the created partition. Installation time will be depends on the USB drive and your disk speed. It will restarts at least 3 times.
5. Yeehaa ! now you got macOS installed in your device. Next download the [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) . 
6. Open the Clover and mount the EFI partition. You can modify the kext files and config.plist files from here.


----------
You will required to boot the macOS from the bootable drive always. In this way windows can't make any changes to the macOS bootloader.  Once the macOS is loaded you can unplug the usb and continue as usual.
# Wifi with WPA2 Enterprise
WPA2 Enterprise is not supported by itlwm, if you are going to use the hackintosh with a institutional wifi you may use Airportitlwm.kext. Download using this link. [OpenintelWireless/itlwm](https://github.com/OpenIntelWireless/itlwm) . Download the stable version. Also download the [OpenintelWireless/HeliPort](https://github.com/OpenIntelWireless/HeliPort).

Make sure you update the config.plist file after adding the kext.


----------
# Adding a Kext file

When you added a kext file to the `EFI > OC > Kext` folder, you need to update the config.plist file with necessary changes. You can use the [PlistEditor Pro](https://www.fatcatsoftware.com/plisteditpro/) or similar software.

For a example if you want to add the `CodecCommander.kext` to your EFI  partition. You can follow bellow steps.

1. Step 1 - place the kext file in the correct folder. `EFI > OC > Kext`
<img src="https://github.com/mr-desilva/Hackintosh-Ventura-OpenCore/blob/main/images/step1.png" width="712" height="465">
2. second - locate the config.plist file and open it with a editor.
<img src="https://github.com/mr-desilva/Hackintosh-Ventura-OpenCore/blob/main/images/step2.png" width="712" height="465">
3. third - Go to `Root > Kernal > Add` and duplicate a entry.
<img src="https://github.com/mr-desilva/Hackintosh-Ventura-OpenCore/blob/main/images/step 3.png" width="812" height="465">
4. fourth - Here we duplicate entry 30 and edit the 31 entry for the codeCommander
<img src="https://github.com/mr-desilva/Hackintosh-Ventura-OpenCore/blob/main/images/step 4.png" width="812" height="465">
5. Save the file and restart the system.

----------









