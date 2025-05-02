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
