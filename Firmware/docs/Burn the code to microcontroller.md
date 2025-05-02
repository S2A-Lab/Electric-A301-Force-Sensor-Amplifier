# Burn the code to microcontroller
A [ST-Link](https://www.amazon.com/HiLetgo-Emulator-Downloader-Programmer-STM32F103C8T6/dp/B07SQV6VLZ/ref=sr_1_1_pp?crid=1V43PBOV8LRL7&dib=eyJ2IjoiMSJ9.qqFD5Om07FWVxJ7mURnZvOJuFzQUJ4hCm5d1K_q_tbYH59Xj1NidkfWhPLRXnD0RmgKjuvxbExbRyj21tTHiOebXEBVeuTbzHIZd0pGrOvgyu4s89AKoc0jtnrOPqOL7UJB0yJpUq697WMEtvL6geYcDXQqFCfDKmGSHTRNhO4KspaL27c94xJhEBxXezBSJGHSpIY1LPtPUTBcqhv3Z78UhKzVtq7korHfX1yDv9_g.x-0iuqYA9tbwy42fONr6I7utDrX4GAFu6m3uPQy2oLk&dib_tag=se&keywords=STLink&qid=1746219215&sprefix=stlink%2Caps%2C120&sr=8-1) and [PB1.25 to 2.54 cable](https://www.amazon.com/PB1-25-Dupont-Connectors-Compatible-PicoBlade/dp/B0BMDNQWF7/ref=sr_1_1?crid=1YBDG1L8Y19H4&dib=eyJ2IjoiMSJ9.y2Zo4Ml__6ZTp25dJdqlX72FRVN9Ayt_OLLhdSxYuPQPFyYYhANc3Eui-QRFdk1mcUOklBzCRNT5pqNHJWcxEqJCQFpmncXD7E4e1IJTxLPZn3ugFkHiXYYRhwoaMcodZBgrkfeujYAPZEWAdXYiAkfrzvYU-SU3Nll0AgDW-ssZyW9RiJqAyHoGBrwxbRf59XMntL6CUvMdH4IB0z6COMDSJeAzNwXHYh8Vm6grCMw.UP_znP-2I6dfwBLNOtFTL36Y9aPBHmLCkrqB_Vwi1Cg&dib_tag=se&keywords=ph1.25+to+2.54&qid=1746219391&sprefix=ph1.25+to+2.54%2Caps%2C102&sr=8-1) are required. 

<img src="https://github.com/user-attachments/assets/4f853dba-53d2-4be8-b2bd-ea1423424696" alt="drawing" width="45%"/>
<img src="https://github.com/user-attachments/assets/6f873ac8-2157-4eea-a7cc-1db6c5496ef4" alt="drawing" width="45%"/>

First, wire the SWDIO, SWCLK, 3.3V and GND from your ST-Link to the 4Pin PH1.25 connector, with the PB1.25 to 2.54 cable.

![image](https://github.com/user-attachments/assets/a59ffb09-fd73-4b23-9c5c-499758ce711a)

Download the [driver for ST-Link](https://www.st.com/en/development-tools/stsw-link009.html) and install.

Connect the STLink to the PCB and then plug in the STLink to your computer. An inversed operation might causing failure connection or damage the microchip if the connector is mis-plugged.

## Windows

You need to prepare another powershell code in this template:

```
openocd.exe -s "[OpenOCD Scripts Directory]" -f openocd.cfg -c "tcl_port disabled" -c "gdb_port disabled" -c "tcl_port disabled" -c "program 'cmake\Firmware.elf'" -c reset -c shutdown
```

Locate your OpenOCD installation directory and find the scripts folder under it. Then replace the **[OpenOCD Scripts Directory]** with the 'script' directory. 

If you completely follows the previous instruction, the final command is most likely to be this:

```
openocd -s "C:\Program Files\xpack-openocd-0.12.0-4-win32-x64\scripts" -f openocd.cfg -c "tcl_port disabled" -c "gdb_port disabled" -c "tcl_port disabled" -c "program 'cmake\Firmware.elf'" -c reset -c shutdown
```

Under the `Firmware` folder, hit `Enter` and the program will be flashed to the microcontroller.
