# Raspberry PI - Boot from SSD

## Prequisities
- We want speed, stability and size compared to the built in micro-SD card, therefore we add an SSD drive to the RPI configuration.
- We need first a suitable SSD drive, choose one that can carry load and lots of updates. I chose: Samsung 870 EVO 500GB (MZ-77E500B/EU).
- We also need a RPI compatible SATA to USB cable, see [Compatible cables here](https://jamesachambers.com/raspberry-pi-4-usb-boot-config-guide-for-ssd-flash-drives/), I chose: StarTech USB 3.0 to 2.5" SATA HDD/SDD Cable w/UASP (USB3S2SAT3CB).
- Install first according to the [RPI installation notes](https://github.com/slittorin/raspberrypi-install).
  - The installation enables boot from SSD.
- Add the SSD Disk with the cable RPI, to the USB 3 ports (blue).

## Installation

1. Logon to RPI desktop:
2. Verify that the SDD is registered by the OS with command `lsblk`, the output should read something like the following:
   ```shell
   pi@server1:~ $ lsblk
   NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
   sda           8:0    0 465.8G  0 disk 
   mmcblk0     179:0    0  29.8G  0 disk 
   ├─mmcblk0p1 179:1    0   256M  0 part /boot
   └─mmcblk0p2 179:2    0  29.6G  0 part /
   ```
   - The SSD is here registered as `sda`.
   - The micro-SD card is here registered as `mmcblk0`.
   - If the SSD is not registered, well, then we need to find the problem.
3. Choose  `Accessories` -> `SD Card Copier` on the desktop.
   - Choose Copy from Device and the one that has `/dev/mmcblk0` (as found through lsblck above).
   - Choose Copy to Device and the one that has `/dev/sda` (as found through lsblck above).
   - Press Start and agree to overwrite, wait for the application to finish.
4. Shutdown RPI.
5. Remove the micro-SD Card on the RPI (keep it preferably in the RPI but not fully inserted).
6. Start RPI.
   - If the RPI do not boot, well, then we need to find the problem.
7. Logon and run the following command to verify `lsblk`, the output should read something like the following:
   ```shell
   pi@server1:~ $ lsblk
   NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
   sda      8:0    0 465.8G  0 disk 
   ├─sda1   8:1    0   256M  0 part /boot
   └─sda2   8:2    0 465.5G  0 part /
   ```
   - The SSD drive is now enabled and running on the RPI, with full disk enabled.
