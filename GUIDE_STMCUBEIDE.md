# GUIDE_STMCUBEIDE.md

## Setting Up STM32CubeIDE for STM32F103C6T6 Blue Pill

This guide will walk you through the process of setting up STM32CubeIDE for the STM32F103C6T6 Blue Pill board, configuring ADC, SPI for SD card module, and integrating FatFS.

### 1. Installing STM32CubeIDE
   - Download the latest version of STM32CubeIDE from the [STMicroelectronics website](https://www.st.com/en/development-tools/stm32cubeide.html).
   - Follow the installation instructions for your operating system.

### 2. Creating a New Project
   - Open STM32CubeIDE and select `File` -> `New` -> `STM32 Project`.
   - In the project wizard, select the STM32F103C6T6 microcontroller from the list or use the board selector for the Blue Pill.
   - Choose the firmware package appropriate for your MCU version if prompted.
   - Fill in the project name and select the project location.
   - Click `Finish` to create the project.

### 3. Configuring the Project
   - Open the `.ioc` file in your project. This will launch the STM32CubeMX configuration tool.
   - In the `Pinout & Configuration` tab, configure the following:
     - **ADC** (Analog-to-Digital Converter): 
       - Enable ADC1 and configure the desired channels (e.g., PA0).
     - **SPI** (Serial Peripheral Interface): 
       - Enable SPI1 and assign it to appropriate pins (PA5 for SCK, PA6 for MISO, PA7 for MOSI).
     
   - Go to the `Clock Configuration` tab to ensure the clocks are set correctly for your application.
   - Click on `Project` -> `Settings` and select the required options like compiler flags and optimization levels depending on your application needs.

### 4. Generating Code
   - After configuration, press the `Save` icon.
   - Click on the `Project` then select `Generate Code`.
   - STM32CubeIDE will create the required files and folders for your project.

### 5. Integrating FatFS
   - Download the FatFS library from [ChaN's website](http://elm-chan.org/fsw/ff/). 
   - Add the FatFS source files to your project by copying them into the `Core` folder and including the necessary headers in your main program.
   - Configure FatFS by adjusting `ffconf.h` in the FatFS directory according to your requirements.

### 6. Configuring SPI for SD Card
   - In your project, create a new source file for the SD card interface, where you will initialize SPI for communication with the SD card.
   - Use the FatFS functions to open, read, write, and close files on the SD card.
   - Ensure that the appropriate SPI initialization code is placed in your `main.c` file, and call it before accessing the SD card.

### 7. Writing Your Code
   - Write the code to initialize ADC, SPI, and FatFS.
   - Make sure to call the initialization functions in the correct order. Example:
   ```c
   HAL_Init(); // Initialize the Hardware Abstraction Layer
   SystemClock_Config(); // Configure system clock
   MX_GPIO_Init(); // Initialize GPIO pins
   MX_ADC1_Init(); // Initialize ADC
   MX_SPI1_Init(); // Initialize SPI
   FATFS_FS_Init(); // Mount the SD card
   ```

### 8. Building and Uploading the Code
   - Connect your Blue Pill board to your computer using a USB to serial adapter or ST-Link.
   - Click on the `Build` icon to compile your project.
   - Upload the code to your Blue Pill using the appropriate method (serial upload or ST-Link).

### 9. Testing
   - After uploading the code, test the ADC and SD card functionalities by reading values from the ADC and attempting to create/read a file on the SD card.

### Conclusion
This guide provided a step-by-step approach to set up STM32CubeIDE for the STM32F103C6T6 Blue Pill, configure ADC and SPI, and integrate FatFS. Happy coding with your STM32 projects!