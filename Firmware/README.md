# Table of Content
1. [Compile the code]
2. [Burn the firmware to microcontroller]
3. [Driver for the microcontroller and data transmission protocol]

# Compile the code
## Environment setup
### Install toolchain for stm32
Go to this [link](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) to download the newest toolchain for your computer.
For Windows users, search for the `AArch32 bare-metal target (arm-none-eabi)` under `Windows (mingw-w64-x86_64) hosted cross toolchains`. 
For Mac (Intel) users, search for the `AArch32 bare-metal target (arm-none-eabi)` under `macOS (x86_64) hosted cross toolchains`.
For Mac (Apple Silicone) users, search for the `AArch32 bare-metal target (arm-none-eabi)` under `macOS (Apple silicon) hosted cross toolchains`.

#### Windows users

Run the `exe` installation package you just downloaded and follow the prompt instruction. 

Please check `Add path to environment variable` option on the page after the progress bar.

![image](https://github.com/user-attachments/assets/bafc52fa-b82f-45d3-a9b1-ec1871dc3e53)

**If you have already close the installation window without check that button**, you can still setup the environment variables. Press `Windows + r` and type `rundll32 sysdm.cpl,EditEnvironmentVariables` and `Enter`. A new window will pop up.

<img src="https://github.com/user-attachments/assets/3015e0ed-8232-4d21-8e63-7bfb7334ef79" alt="drawing" width="45%"/>

Double click "Path" and click "New" button

<img src="https://github.com/user-attachments/assets/5ec41ee5-fbae-418a-8af8-38d814e83794" alt="drawing" width="45%"/>
<img src="https://github.com/user-attachments/assets/bf80251c-a250-4b36-a892-6af397b2e733" alt="drawing" width="45%"/>

Then, you need to find your toolchain location you just installed. It's usually under `C:\Program Files (x86)\Arm GNU Toolchain arm-none-eabi`. 

<img src="https://github.com/user-attachments/assets/95728b9b-d72c-410d-9d64-d276b9462429" alt="drawing" width="45%"/>

Open the folder and find the `bin` folder under it. 

<img src="https://github.com/user-attachments/assets/cd8823e6-8f85-46d9-b979-3244d001fc62" alt="drawing" width="45%"/>

Open this `bin` folder. You will find there are a lot of `exe` files under it. 

<img src="https://github.com/user-attachments/assets/78ff0d6a-137c-470b-987c-33f515ada4fe" alt="drawing" width="45%"/>

Click on the top address bar and copy the file name and paste it in the previous editing window.

<img src="https://github.com/user-attachments/assets/52bb5d90-545d-4ca1-b7e6-418351e72af7" alt="drawing" width="45%"/>

Click "Ok" to save the system variable you added.


##### Install MinGW environment (Windows only)
Download the MinGW GUI from this [page](https://sourceforge.net/projects/mingw/). Open it and click `Install`.

<img src="https://github.com/user-attachments/assets/2335307e-4f3c-418a-9dec-a892ad7b53aa" alt="drawing" width="45%"/>

Open MinGW Installation Manager and then select `mingw-developer-toolkit`, `mingw32-base`, `mingw32-gcc-g++`, `msys-base`. Then click Installation and apply changes

<img src="https://github.com/user-attachments/assets/47d826d6-8519-4f51-b6c3-0272b8989f8e" alt="drawing" width="30%"/>
<img src="https://github.com/user-attachments/assets/c7680d1a-45b2-43e8-be67-eff9d1133c20" alt="drawing" width="30%"/>
<img src="https://github.com/user-attachments/assets/b11dec77-7143-4567-9951-a12b02ddab8a" alt="drawing" width="30%"/>

Similarly, you will find a bin foler under the MinGW folder. Copy the path (e.g. `C:\MinGW\bin`).

Press `Windows + r` and type `rundll32 sysdm.cpl,EditEnvironmentVariables` and `Enter`. 

<img src="https://github.com/user-attachments/assets/3015e0ed-8232-4d21-8e63-7bfb7334ef79" alt="drawing" width="45%"/>

Double click "Path" and click "New" button

<img src="https://github.com/user-attachments/assets/5ec41ee5-fbae-418a-8af8-38d814e83794" alt="drawing" width="45%"/>
<img src="https://github.com/user-attachments/assets/bf80251c-a250-4b36-a892-6af397b2e733" alt="drawing" width="45%"/>

Paste the path you just copied and click "OK".

<img src="https://github.com/user-attachments/assets/0a3db346-a8af-4b5b-994a-a50be8ccbb4b" alt="drawing" width="45%"/>

##### Install CMake environment (Windows only)

Go to [CMake page](https://cmake.org/download/) to download the CMake. Download the `Windows x64 Installer` and install.

#### Mac users
Run the `pkg` installation package you just downloaded and follow the prompt instruction. 

After the installation is finished, we need to add your installed toolchain to your computer environment.

A command needs to be prepared. The command has a template of

```export PATH=$PATH:/Applications/ArmGNUToolchain/[VER]/arm-none-eabi/bin```

[VER] Is a number you need to identify. It's the toolchain version you installed. It is contained in the filename of your installation package (See image below).

<img src="https://github.com/user-attachments/assets/93fe81b2-9f14-4c57-9e7a-b5370465fa7f" alt="drawing" width="45%"/>

For example, in the case of the image shows, the command will be 

export PATH=$PATH:/Applications/ArmGNUToolchain/**14.2.rel1**/arm-none-eabi/bin

Using `⌘+[space]` to open spotlight and type `terminal` to open the `Terminal.app`. Alternative terminal software works. 

Type `vi .zshrc`. This command will modify the .zshrc file with vim. Enter `Go` and you will find you are able to modify the content.

Copy the previously prepared command and then paste it at the end of file. Then press `esc` and input `:wq` to save the `.zshrc` file. 

This allows your CMake detect the toolchain you just installed.

### Install STM32CubeMX

Download STM32CubeMX from this [website](https://www.st.com/en/development-tools/stm32cubemx.html) and install it.

### Install OpenOCD

#### Windows

Download OpenOCD through [Github](https://github.com/xpack-dev-tools/openocd-xpack/releases/tag/v0.12.0-4). Unpack this zip file under `C:\Program Files (x86)` directory.

Similarly, you will find a bin foler under the unzipped directory. Copy the path (e.g. `C:\Program Files\xpack-openocd-0.12.0-4-win32-x64\bin`).

Press `Windows + r` and type `rundll32 sysdm.cpl,EditEnvironmentVariables` and `Enter`. 

<img src="https://github.com/user-attachments/assets/3015e0ed-8232-4d21-8e63-7bfb7334ef79" alt="drawing" width="45%"/>

Double click "Path" and click "New" button

<img src="https://github.com/user-attachments/assets/5ec41ee5-fbae-418a-8af8-38d814e83794" alt="drawing" width="45%"/>
<img src="https://github.com/user-attachments/assets/bf80251c-a250-4b36-a892-6af397b2e733" alt="drawing" width="45%"/>

Paste the path you just copied and click "OK".

<img src="https://github.com/user-attachments/assets/8b9e50de-9ccc-4464-9f9c-bb0007a7ce77" alt="drawing" width="45%"/>


#### Mac

Install [homebrew](https://brew.sh/). Then using `⌘+[space]` to open spotlight and type `terminal` to open the `Terminal.app`. Type 

```
brew install openocd
```

In the terminal to install openocd.

## Generate code in STM32CubeMX

Open the `Firmware.ioc` under `Firmware` folder. Under `Project Manager` page, check if the toolchain / IDE is `CMake`. If not, change it to `CMake`.

<img src="https://github.com/user-attachments/assets/cc8bc868-eafd-4dcf-ba75-33a80d1f181b" alt="drawing" width="100%"/>

Then click on the "GENERATE CODE" button on the top right.

<img src="https://github.com/user-attachments/assets/4328de6b-861e-4eed-bfb1-25d94355cbd9" alt="drawing" width="100%"/>

## Compile the code

### Windows

After generating the code, a `cmake` folder will be created under the `Firmware` folder.

Navigate to the `cmake` folder under the `Firmware` folder, right click and open a terminal window. You can use either PowerShell or CMD.

![image](https://github.com/user-attachments/assets/6907d354-ce37-40c7-a3d8-3ac603551f6a)

Type `cmake -G "MinGW Makefiles" ..` and hit `Enter`. 

![image](https://github.com/user-attachments/assets/f2886201-1d25-4d09-b6b1-e70e4a1218c9)

CMake will configure the build profile.

Then type 

```cmake --build . --target Firmware -j 8```

and hit `Enter`

![image](https://github.com/user-attachments/assets/01377e39-75c8-474c-8333-ffd70dd0eb1b)

It will compile the `Firmware.elf` under `cmake` directory. The `Firmware.elf` is the firmware compiled.

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

Hit `Enter` and the program will be flashed to the microcontroller.

# Driver for the microcontroller and data transmission protocol

## Install driver for microcontroller

install the [STM32 Virtual COM Port Driver](https://www.st.com/en/development-tools/stsw-stm32102.html).

After you install the driver, COM device or serial port device will show when the amplifier board is plugged to your computer through the microUSB port.

## Communication protocol

The microcontroller encodes the analog reading and system time to a 11 byte package. The first 5 bytes are for analog reading data and last 5 bytes are for time. The last byte is a `0xFF` byte for frame check. 

|   TxFrame[0]   |   TxFrame[1]   |   TxFrame[2]   |   TxFrame[3]  |  TxFrame[4]  |  TxFrame[5]  |  TxFrame[6]  |  TxFrame[7]  |  TxFrame[8] | TxFrame[9] | TxFrame[10] |
|   ----------   |   ----------   |   ----------   |   ----------  |  ----------  |  ----------  |  ----------  |  ----------  |  ---------- | ---------- | ----------- |
|Analog (31 - 28)|Analog (27 - 21)|Analog (20 - 14)|Analog (13 - 7)|Analog (6 - 0)|Time (31 - 28)|Time (27 - 21)|Time (20 - 14)|Time (13 - 7)|Time (6 - 0)|     0xFF    |

Here is an example code to decode the data stream in Matlab: 

```Matlab
clear;clc;close all;
% === USER CONFIGURATION ===
comPort = "COM4";         % Change to your STM32 COM port
baudRate = 115200;        % Make sure it matches your USB CDC config
bufferSize = 11;          % One packet is 11 bytes

% === SETUP ===
s = serialport(comPort, baudRate);
% configureTerminator(s, "none");  % We're using custom delimiters
flush(s);  % Clear existing data

% === REAL-TIME PLOTTING ===
figure;
h = animatedline;
xlabel('Time (s)');
ylabel('ADC Value');
title('Live ADC Plot');
grid on;

startTime = datetime('now');
tic;
count = 0;
% === MAIN LOOP ===
while ishandle(h)
    if s.NumBytesAvailable >= bufferSize*100
        bytes = read(s, bufferSize*100, "uint8");
        % Decode 7-bit packed values
        [t, raw_data] = process_ADC7bit_data(bytes);
        
        % Add to plot
        addpoints(h, mean(double(t)/1000), mean(double(raw_data)));
        drawnow limitrate
        % count = count+length(raw_data);
    end
end

% === CLEANUP ===
clear s;

% === HELPER FUNCTION ===
function [t, v] = process_ADC7bit_data(raw_stream)
    % Find all potential frame endings
    frame_divide_idxes = [0; find(raw_stream == 255)'];
    frame_lengths = diff(frame_divide_idxes);
    
    % Only keep valid 11-byte frames
    valid_frame_idxes = frame_divide_idxes(frame_lengths == 11);
    if isempty(valid_frame_idxes)
        t = [];
        v = [];
        return;
    end

    % Index into raw_stream to extract all 11-byte frames
    data_indexes = repmat(valid_frame_idxes', 1, 11) + repelem(1:11,1,length(valid_frame_idxes));
    raw_data = reshape(raw_stream(data_indexes),[],11)';

    % raw_data(:,end)
    v4 = bitand(uint32(bitor(bitshift(raw_data(1,:),4), bitshift(raw_data(2,:),-3))),255);
    v3 = bitand(uint32(bitor(bitshift(raw_data(2,:),5), bitshift(raw_data(3,:),-2))),255);
    v2 = bitand(uint32(bitor(bitshift(raw_data(3,:),6), bitshift(raw_data(4,:),-1))),255);
    v1 = bitand(uint32(bitor(bitshift(raw_data(4,:),7), raw_data(5,:))),255);

    t4 = bitand(uint32(bitor(bitshift(raw_data(6,:),4), bitshift(raw_data(7,:),-3))),255);
    t3 = bitand(uint32(bitor(bitshift(raw_data(7,:),5), bitshift(raw_data(8,:),-2))),255);
    t2 = bitand(uint32(bitor(bitshift(raw_data(8,:),6), bitshift(raw_data(9,:),-1))),255);
    t1 = bitand(uint32(bitor(bitshift(raw_data(9,:),7), raw_data(10,:))),255);
    
    v = bitshift(v4,24)+bitshift(v3,16)+bitshift(v2,8)+v1;
    t = bitshift(t4,24)+bitshift(t3,16)+bitshift(t2,8)+t1;
    % t(t < 0) = t(t < 0) + 2^32;
end
```
