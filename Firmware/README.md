# Table of Content
1. Compile the code
2. Burn the firmware to microcontroller
3. Installing driver for amplifier
4. Data transmission protocol

# Compile the code
## Environment setup
### Installing toolchain for stm32
Go to this [link](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) to download the newest toolchain for your computer.
For Windows users, search for the `AArch32 bare-metal target (arm-none-eabi)` under `Windows (mingw-w64-x86_64) hosted cross toolchains`. 
For Mac (Intel) users, search for the `AArch32 bare-metal target (arm-none-eabi)` under `macOS (x86_64) hosted cross toolchains`.
For Mac (Apple Silicone) users, search for the `AArch32 bare-metal target (arm-none-eabi)` under `macOS (Apple silicon) hosted cross toolchains`.

Download corresponding installation package (with extension `exe`, `pkg`) and install them. 
#### Note for Windows users
For windows users, please check `Add path to environment variable` option when installing your toolchain.

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

#### For Mac users (Mandatory)

First, a command needs to be prepared. The command has a template of

```export PATH=$PATH:/Applications/ArmGNUToolchain/[VER]/arm-none-eabi/bin```

[VER] Is a number you need to identify. It's the toolchain version you installed. It is contained in the filename of your installation package (See image below).

![image](https://github.com/user-attachments/assets/93fe81b2-9f14-4c57-9e7a-b5370465fa7f)

For example, in the case of the image shows, the command will be 

export PATH=$PATH:/Applications/ArmGNUToolchain/**14.2.rel1**/arm-none-eabi/bin

For Mac users, using `⌘+[space]` to open spotlight and type `terminal` to open the `Terminal.app`. Alternative terminal software works. 

Type `vi .zshrc`. This command will modify the .zshrc file with vim. Enter `Go` and you will find you are able to modify the content.

Copy the previously prepared command and then paste it at the end of file. Then press `esc` and input `:wq` to save the `.zshrc` file. 

This allows your CMake detect the toolchain you just installed.



#### Mac

#### Windows

### Installing MinGW environment (Windows only)

### Installing STM32CubeMX

### Installing CLion (or other alternative coding tools, if you like)

### Installing OpenOCD
