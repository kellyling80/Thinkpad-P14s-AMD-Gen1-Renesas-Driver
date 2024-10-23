********************************************************************************
*
* ROM Writing tool for uPD720201/uPD720202 (For Windows)
*
*                                                                     2012/09/07
********************************************************************************

--------------------------------------------------------------------------------
Table of Contents
--------------------------------------------------------------------------------
1. Notes
2. Supported Serial Flash ROM List
3. Usage
4. Return Code
5. Configuration file(.ini) format

--------------------------------------------------------------------------------
1. Notes
--------------------------------------------------------------------------------
Note1: If the file name is changed, this tool does not work.

Note2: This tool is for the following devices.
      - uPD720201 ES2.0 sample whose revision ID of PCI Configuration 
       Register is 2h.
      - uPD720201 ES2.1 sample & CS sample & Mass product whose revision
       ID of PCI Configuration Register is 3h.
      - uPD720202 ES 2.0 sample & CS sample & Mass product whose revision
       ID of PCI Configuration Register is 2h.

Note3: Please use FW file for uPD720201/uPD720202 released at 2012/09/07.
       This version is v2.0.1.8.
       
--------------------------------------------------------------------------------
2. Supported Serial Flash ROM List
--------------------------------------------------------------------------------

  -MACRONIX
   MX25L512E/1006E/2006E/4006E
   MX25L5121E/1021E/2006E/4006E
  -WINBOND
   W25X10BV/20BV/40BV
  -Micron(Numonyx)
   M25P05-A/10-A/20/40
  -Chingis
   Pm25LD512C2
  -ATMEL
   AT25F512B
  -AMIC
   A25L512/010/020/040
  -EON
   EN25F05/10/20/40
  -SST
   SST25VF512A/010A

--------------------------------------------------------------------------------
3. Usage
--------------------------------------------------------------------------------
W201FWxx [ /? |  /srom romtype | /write file1 [file2] [file3] | dump file1 |
         /erase | /noerase | /log [file4] | /address deviceaddress |
         /fout file6 | /verify file1 [file2] [file3] |
         /writeall file1 [file2] [file3] ]

Options::

 /?          :Display this help message.

 /srom       :Specify SPI-Flash-ROM device type. When only using this command,
              FW version, PCI Subsystem Vender ID and PCI Subsystem ID in the 
              SPI-Flash-ROM are shown.

 /write      :Write both filename1(.mem) and filename2(.ini) to SPI-Flash-ROM.
              If write EUI-64 to SPI-Flash-ROM, specify the filename3.

 /dump       :Dump ROM Image from SPI-Flash-ROM.

 /erase      :Erase all of the data in SPI-Flash-ROM.

 /noerase    :SPI-Flash-ROM isn't erased before SPI-Flash-ROM is written.
             (Erase process is skipped by using this command. If the rom is not
              erased, any data can't be written to the rom in spite of using 
              this command.)

 /log        :Generates log file named filenmae4.
             (Default log file named "log.txt")

 /address    :Specify one target device with PCI Device Address.

 /fout       :File out to file5 (Don't write to SPI-Flash-ROM)

 /verify     :Verify the ROM image data (Don't write to SPI-Flash-ROM).
 
 /writeall   :Write both file1(.mem) and file2(.ini) to SPI Flash ROMs
              of multi Host controllers on same system(computer).
              If need to write EUI-64, specify file3(.eui).


Where::

romtype 	  :Serial ROM type number. 
                0. Auto Select (check serial rom type automatically)
                ?. Check Serial ROM Information.

filename1	  :Firmware File (extension is mem) released from Renesas Electronics.

filename2	  :Configuration File (extension is ini) including system dependent
	           Parameters such as PCI Subsystem ID or PCI Subsystem Vendor ID.
	           Renesas Electronics releases a sample file. User need to modify those
	           parameters in accordance with the customer system.

filename3	  :EUI-64 file(extension is eui) that includes EUI-64(XX-XX-XX-XX-
	           XX-XX-XX-XX). If the Product is hot-plug device such as Express
	           Card, the EUI-64 must be set. This requirement is released from
	           Microsoft Windows Logo Program. As for the EUI-64, refer to the
	           following WEB site. 
                   http://standards.ieee.org/regauth/oui/tutorials/EUI64.html
				   
filename4	  :LOG File Name. In case of skipping the fielname4, log.txt is 
	           generated on the current directory.

filename5     :Output Serial ROM Image File.
			   
deviceaddress :Format is XX-YY-ZZ. XX is PCI Bus Number(HEX). YY is PCI Device 
			   Number(HEX). ZZ is PCI Function Number(HEX). If there are 
			   multiple devices on the system, user can specify one device.

Example::

	>W201FWXX
	>W201FWXX /srom 0 /write KXXXXXXX.mem cfg_201.ini
	>W201FWXX /srom 0 /write KXXXXXXX.mem cfg_202.ini
	>W201FWXX /srom 0 /address 04-00-00 /write Kxxxxxx.mem cfg_201.ini
	>W201FWXX /srom 0 /address 04-00-00 /write Kxxxxxx.mem cfg_202.ini
	>W201FWXX /srom 0 /verify Kxxxxxx.mem cfg_201.ini
	>W201FWXX /srom 0 /verify Kxxxxxx.mem cfg_202.ini
	>W201FWXX /srom 0 /writeall Kxxxxxx.mem cfg_201.ini
	>W201FWXX /srom 0 /writeall Kxxxxxx.mem cfg_202.ini

--------------------------------------------------------------------------------
4. Return Code
--------------------------------------------------------------------------------

0   : Success.
-1  : Fatal Error is detected.
-2  : Memory allocate is failed.
-3  : Filename is changed.
-4  : Wrong command line option is found.
-5  : Can't access uPD720201/uPD720202
-6  : Can't detect uPD720201/uPD720202
-7  : Can't find designated file
-8  : Verify Error is detected.
-9  : Can't read FW file
-10 : Can't read ini file
-11 : Can't read EUI64 file
-12 : Failed to write FW to Serial ROM.
-13 : Failed to write log to log file.
-14 : Failed to read/write temporary file.
-16 : Unsupported revision ID.
-17 : Unsupported Serial ROM.

--------------------------------------------------------------------------------
6. Configuration file(.ini) format
--------------------------------------------------------------------------------
[SubSystemVendorID]
FFFF

[SubSystemID]
FFFF

[EnableDeviceNonRemovalPort1]
0
; When set to '1', the uPD720201 forces the Device Removal(DR) bit to '1b' 
; in both the PORT1 PORTSC and PORT5 PORTSC. The uPD720202 forces the DR bit to
; '1b' in both the PORT1 PORTSC and PORT3 PORTSC. Default value is '0'

[EnableDeviceNonRemovalPort2]
0
; When set to '1', the uPD720201 forces the Device Removal(DR) bit to '1b' 
; in both the PORT2 PORTSC and PORT6 PORTSC. The uPD720202 forces the DR bit to
; '1b' in both the PORT2 PORTSC and PORT4 PORTSC. Default value is '0'

[EnableDeviceNonRemovalPort3]
0
; When set to '1', the uPD720201 forces the Device Removal(DR) bit to '1b' 
; in both the PORT3 PORTSC and PORT7 PORTSC. Default value is '0'

[EnableDeviceNonRemovalPort4]
0
; When set to '1', the uPD720201 forces the Device Removal(DR) bit to '1b' 
; in both the PORT4 PORTSC and PORT8 PORTSC. Default value is '0'

[UsePPON]
1
; When set to '0', the uPD720201 and uPD720202 force the Port Power Control (PPC)
; bit to '0b' in the HCCPARAMS register. When VBUS is not controlled by the PPON
; pin, this bit should be set to '0b'. Default value is '1'

[DisablePortCount]
0
;uPD720201
;0 : All ports are enabled.
;1 : Port 4 and Port 8 are disabled
;2 : Port 3,4,7 and 8 are disabled.
;3 : Port 2,3,4,6,7 and 8 are disabled.
;uPD720202
;0 : All ports are enabled.
;1 : Port 2 and 4 are disabled,

[PSEL]
1
;When set to '1', the default value of the Active State Power Management Control
;fields in the PCI Express Link Control Register is 00b. 
;When this bit is '0', the default value is 11b.

[AUXDET]
1
;Auxiliary Power Detect. When the system supports remote wakeup from D3cold, 
;this bit should be set to '1'.

[EnableClockRequest]
1
; Set to '0', if you want to disable the CLKREQ#(ClockRequest). 
; There exist PCs which has problem in its CLKREQ# function for ExpressCard slot.
; It is recommended to disable CLKREQ# function, if the product is ExpressCard.
; Default value is "1". 

[SerialNumCapEnable]
0
;When set to '1b', Serial Number Capability area is enabled.

[FWUpdateProperty]
0
;This flag is checked by the "FW Updater" that is the executable file for
;Windows OS and can update old firmware in the external rom to new firmware.
;When the "FWUpdateProperty" is set to '1', the FW Updater updates the firmware
;only when the SSID and SVID of the PCI Configuration Register of the 
;uPD720201/202 match the SSID and SVID in the vendor specific FW Updater file. 
;Vendors can generate the vendor specific FW Updater including thier SSID and 
;SVID for their products with the FW Updater Generator. 
;When it is set to '0', the firmware is updated by "FW Updater" that is included
;the SSID & SVID and isn't included the SSID & SVID updates the firmware.

[BatteryChargeModePort1]
0
;Battery charging port type for PORT1. Can be set to one of the following:.
;0 : SDP only
;1 : CDP only
;2 : SDP - DCP
;3 : CDP - DCP

[BatteryChargeModePort2]
0
;Battery charging port type for PORT2. Can be set to one of the following:.
;0 : SDP only
;1 : CDP only
;2 : SDP - DCP
;3 : CDP - DCP

[BatteryChargeModePort3]
0
;Battery charging port type for PORT3(Only uPD720201). Can be set to one 
;of the following:.
;0 : SDP only
;1 : CDP only
;2 : SDP - DCP
;3 : CDP - DCP

[BatteryChargeModePort4]
0
;Battery charging port type for PORT4(Only uPD720201). Can be set to one 
;of the following:.
;0 : SDP only
;1 : CDP only
;2 : SDP - DCP
;3 : CDP - DCP

[TRTFCTLU2Dx1]
1
;High Speed Eye Tr/Tf fine control for PORT1.
;0 : -1 (make low pitch)
;1 : 0 (default)
;2 : +1
;3 : +2 (make steep pitch)?

[TRTFCTLU2Dx2]
1
;High Speed Eye Tr/Tf fine control for PORT2.
;0 : -1 (make low pitch)
;1 : 0 (default)
;2 : +1
;3 : +2 (make steep pitch)?

[TRTFCTLU2Dx3]
1
;High Speed Eye Tr/Tf fine control for PORT3(Only uPD720201).
;0 : -1 (make low pitch)
;1 : 0 (default)
;2 : +1
;3 : +2 (make steep pitch)?

[TRTFCTLU2Dx4]
1
;High Speed Eye Tr/Tf fine control for PORT4(Only uPD720201).
;0 : -1 (make low pitch)
;1 : 0 (default)
;2 : +1
;3 : +2 (make steep pitch)?
[DisableCompletionTimeout]
0
; When a system requires default value of "Completion Timeout Disable" bit in
;PCI Configuration Space is '1b', this value should be set to '1'.
; ##Note##
;To use this section, you should write the firmware(v2.0.1.8 or later).
