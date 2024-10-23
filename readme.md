## Renesas USB 3.0 Firrmware for Lenovo P14s AMD Gen-1

**The issue:** After BIOS 1.3x , Lenovo P14s / T14 AMD Gen-1 laptops will have their webcams disabled (in Windows 10/11)

**The cause:** Firmware for Renesas UPD72002 chip which runs the internal webcam is not loaded/missing from the BIOS update

**The solution:** Users need to install the firmware manually

Lenovo support site for both laptop models does not have the firmware. Therefore, you will have to use a 3rd party firmware updater to write to the rom. 

1.  To check if you have this problem, check the Device Manager in Windows. You should have a yellow exclamation mark next to the "USB 3.0 extensible USB...'
2.  Download the Firmware and read the Installation method pdf
3.  Original site of firmware and driver : https://www.startech.com/en-nz/cards-adapters/pexusb3s44v HardwareIDs: PCI\\VEN_1912&DEV_0015 ; PCI\\VEN_1912&DEV_0015&SUBSYS_00000000&REV_02


