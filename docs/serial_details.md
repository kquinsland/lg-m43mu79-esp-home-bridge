# EXTERNAL CONTROL DEVICE SETUP

This is a rip right from the manual.
**Note:** Use a "reverse cable"

## Communication Parameters

- Baud rate: 9600 bps (UART)
- Data length: 8 bits
- Parity: None
- Stop bit: 1 bit
- ASCII codes


## Transmission

Communication code : ASCII code Use a crossed (reverse) cable.

`[Command1][Command2][ ][Set ID][ ][Data][Cr]`

- `[Command 1]`: First command to control the Monitor.
- `[Command 2]`: Second command to control the Monitor.
- `[Set ID]`: the address of the specific monitor
- `[DATA]`: To transmit command data.
- `[Cr]`: Carriage Return (ASCII code `0x0D`)
- `[ ]`: ASCII code for space (`0x20`)


### OK Acknowledgement

[Command2][ ][Set ID][ ][OK][Data][x]

* The Monitor transmits ACK (acknowledgement) based on this format when receiving normal data. At this time, if the data is in data read mode, it indicates present status data. If the data is in data write mode, it returns the data of the PC computer.

### Error Acknowledgement

[Command2][ ][Set ID][ ][NG][Data][x]

* The Monitor transmits ACK (acknowledgement) based on this format when receiving abnormal data from nonviable functions or communication errors.


## Examples

Since the documentation is not super clear here's a few *WORKING* examples.
The proper format was defined / tipped off to me here:
https://support.justaddpower.com/kb/article/36-lg-rs232-control/

```
# Note: both of these commands are for set 01 (0x30 0x31 = 01)
Power ON:
    data: [0x6B, 0x61, 0x20, 0x30, 0x31, 0x20, 0x30, 0x31, 0x0D]

Power OFF:
    data: [0x6B, 0x61, 0x20, 0x30, 0x31, 0x20, 0x30, 0x30, 0x0D]
```



# Command Reference List

| Function                 	| CMD1 (ascii/hex) 	| CMD2 (ascii/hex) 	| Data (HEX) 	|
|--------------------------	|------------------	|------------------	|------------	|
| Power                    	| k                	| a                	| 00~01      	|
| Screen Mute              	| k                	| d                	| 00~01      	|
| Input select (Main)      	| x                	| b                	| 00~FF      	|
| Input select (Sub)       	| x                	| c                	| 00~FF      	|
| Input select (Sub2)      	| x                	| d                	| 00~FF      	|
| Input select (Sub3)      	| x                	| e                	| 00~FF      	|
| Aspect Ratio (Main)      	| x                	| f                	| 00~02      	|
| Aspect Ratio (Sub)       	| x                	| g                	| 00~01      	|
| Aspect Ratio (Sub2)      	| x                	| h                	| 00~01      	|
| Aspect Ratio (Sub3)      	| x                	| i                	| 00~01      	|
| PBP/PIP                  	| k                	| n                	| 00~09      	|
| PIP Size                 	| k                	| p                	| 00~02      	|
| Main/Sub Screen Change   	| m                	| a                	| 1          	|
| Picture Mode             	| d                	| x                	| 00~14      	|
| Brightness               	| k                	| h                	| 00~64      	|
| Contrast                 	| k                	| g                	| 00~64      	|
| Sharpness                	| k                	| k                	| 00~64      	|
| Brightness Stabilization 	| m                	| b                	| 00~01      	|
| SUPERRESOLUTION+         	| m                	| c                	| 00~03      	|
| BlackLevel               	| m                	| d                	| 00~01      	|
| HDMIULTRAHD DeepColor    	| m                	| e                	| 00~01      	|
| DFC                      	| m                	| f                	| 00~01      	|
| Response Time            	| m                	| g                	| 00~03      	|
| Black Stablilzer         	| m                	| h                	| 00~64      	|
| Uniformity               	| m                	| i                	| 00~01      	|
| Gamma                    	| m                	| j                	| 00~09      	|
| Color Temp               	| k                	| u                	| 00~04      	|
| Red Gain                 	| j                	| w                	| 00~64      	|
| Green Gain               	| j                	| y                	| 00~64      	|
| Blue Gain                	| j                	| z                	| 00~64      	|
| Language                 	| f                	| i                	| 00~10      	|
| SMART ENERGY SAVING      	| m                	| k                	| 00~02      	|
| LED Control Button       	| m                	| l                	| 00~03      	|
| DVI Power Supply         	| m                	| m                	| 00~01      	|
| Auto Screen Off          	| m                	| n                	| 00~01      	|
| DisplayPort1.2           	| m                	| o                	| 00~01      	|
| OSDLock                  	| k                	| m                	| 00~01      	|
| Reset                    	| f                	| k                	| 00~01      	|


# PAYLOADS
| Title                    	| Item                                                                                                                                                                                                                                                     	|            	|             	|
|--------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|------------	|-------------	|
| Power                    	| 00:PowerOff, 01:PowerOn                                                                                                                                                                                                                                  	|            	|             	|
| Screen Mute              	| 00:ScreenMuteOff, 01:ScreenMuteOn                                                                                                                                                                                                                        	|            	|             	|
| Input select (Main)      	| 90:HDMI1, 91:HDMI2, 92:HDMI3, 93:HDMI4, C0:DP, E0:USB-C                                                                                                                                                                                                  	|            	|             	|
| Input select (Sub)       	| 90:HDMI1, 91:HDMI2, 92:HDMI3, 93:HDMI4, C0:DP, E0:USB-C                                                                                                                                                                                                  	|            	|             	|
| Input select (Sub2)      	| 90:HDMI1, 91:HDMI2, 92:HDMI3, 93:HDMI4, C0:DP, E0:USB-C                                                                                                                                                                                                  	|            	|             	|
| Input select (Sub3)      	| 90:HDMI1, 91:HDMI2, 92:HDMI3, 93:HDMI4, C0:DP, E0:USB-C                                                                                                                                                                                                  	|            	|             	|
| Aspect Ratio (Main)      	| 00:Full Wide, 01:Original, 02: "1 : 1""                                                                                                                                                                                                                  	| 03:Cinema1 	| 04:Cinema2" 	|
| Aspect Ratio (Sub)       	| 00:Full Wide, 01:Original                                                                                                                                                                                                                                	|            	|             	|
| Aspect Ratio (Sub2)      	| 00:Full Wide, 01:Original                                                                                                                                                                                                                                	|            	|             	|
| Aspect Ratio (Sub3)      	| 00:Full Wide, 01:Original                                                                                                                                                                                                                                	|            	|             	|
| PBP/PIP                  	| 00:OFF, 01:PBP, 02:PBP2, 03:PIP_LT, 04:PIP_RT, 05:PIP_LB, 06:PIP_RB,07:PBP_3P(NA), 08:PBP_L1P_R2P(NA), 09:PBP_4P                                                                                                                                         	|            	|             	|
| PIP Size                 	| 00:Small, 01:Medium, 02:Large                                                                                                                                                                                                                            	|            	|             	|
| Main/Sub Screen Change   	| 01: Main/Sub Screen exchange                                                                                                                                                                                                                             	|            	|             	|
| Picture Mode             	| 00:custom, 01:mono, 02:Reader, 04:Photo, 05:Cinema,06:sRGB, 07:Color Weakness, 08:Game, 09:FPS Game1, 0A:FPS Game2, 0B:RTS Game, 0C:Custom Game, 0D:EBU, 0E:REC 709, 0F:SMPTE C, 10:DICOM, 11:Calibration1, 12:Calibration2, 13:DarkRoom1, 14:DarkRoom2, 	|            	|             	|
| Brightness               	| 0~64(Hex)?AutoBrightness :BacklightStabilizationOn                                                                                                                                                                                                       	|            	|             	|
| Contrast                 	| 0~64(Hex)                                                                                                                                                                                                                                                	|            	|             	|
| Sharpness                	| 0~64(Hex)                                                                                                                                                                                                                                                	|            	|             	|
| Brightness Stabilization 	| 00: Off, 01: On                                                                                                                                                                                                                                          	|            	|             	|
| SUPERRESOLUTION+         	| 00: High, 01:Middle, 02:Low, 03:Off                                                                                                                                                                                                                      	|            	|             	|
| BlackLevel               	| 00:High, 01:Low                                                                                                                                                                                                                                          	|            	|             	|
| HDMIULTRAHD DeepColor    	| 00: On, 01: Off                                                                                                                                                                                                                                          	|            	|             	|
| DFC                      	| 00: On, 01: Off                                                                                                                                                                                                                                          	|            	|             	|
| Response Time            	| 00:Fast, 01:Normal, 02:Slow, 03:Off                                                                                                                                                                                                                      	|            	|             	|
| Black Stablilzer         	| 0~64(Hex)                                                                                                                                                                                                                                                	|            	|             	|
| Uniformity               	| 00: On, 01: Off                                                                                                                                                                                                                                          	|            	|             	|
| Gamma                    	| 00:Mode4, 01:Mode1, 02:Mode2, 03Mode3, 04:Gamma 1.8,05:Gamma 2.0, 06:Gamma 2.2, 07:Gamma 2.4, 08:Gamma 2.6, 09:DICOM Gamma                                                                                                                               	|            	|             	|
| Color Temp               	| 00:Manual, 01:Custom, 02:WARM, 03:MEDIUM, 04:COOL                                                                                                                                                                                                        	|            	|             	|
| Red Gain                 	| 0~64(Hex)                                                                                                                                                                                                                                                	|            	|             	|
| Green Gain               	| 0~64(Hex)                                                                                                                                                                                                                                                	|            	|             	|
| Blue Gain                	| 0~64(Hex)                                                                                                                                                                                                                                                	|            	|             	|
| Language                 	| 00:Eng, 01:Ger, 02:Fre, 03:Spa, 04:Ita, 05:Swe, 06:Fin, 07:Por, 08:Bra, 09:Pol, 0A:Rus, 0B:Grc, 0C:Ukr, 0D:Chi, 0E:ChiT, 0F:Jap, 10:Kor                                                                                                                  	|            	|             	|
| SMART ENERGY SAVING      	| 00:High, 01:Low, 02:Off                                                                                                                                                                                                                                  	|            	|             	|
| LED Control Button       	| 00:Always On, 01:20sec Time out, 02:10sec Time out, 03:5sec Time out                                                                                                                                                                                     	|            	|             	|
| DVI Power Supply         	| 00: On, 01: Off                                                                                                                                                                                                                                          	|            	|             	|
| Auto Screen Off          	| 00: On, 01: Off                                                                                                                                                                                                                                          	|            	|             	|
| DisplayPort1.2           	| 00:Enable, 01:Disable,                                                                                                                                                                                                                                   	|            	|             	|
| OSDLock                  	| 00: Off, 01: On                                                                                                                                                                                                                                          	|            	|             	|
| Reset                    	| 00: Picture Reset, 01:Factory Reset                                                                                                                                                                                                                      	|            	|             	|
