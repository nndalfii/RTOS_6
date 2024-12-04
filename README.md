# README: STM32 FreeRTOS LED Control Program

## Overview
This project is an STM32-based application using FreeRTOS to demonstrate multitasking and shared resource access. It involves controlling three LEDs (Green, Red, and Blue) and managing a critical section in a multitasking environment. The program uses two FreeRTOS threads (`GreenLedTask` and `RedLedTask`) to simulate concurrent access to a shared resource, represented by the `AccessSharedData` function. A blue LED indicates resource contention.

## Features
- **FreeRTOS Multitasking:** Two tasks (`GreenLedTask` and `RedLedTask`) run independently, controlling the Green and Red LEDs.
- **Critical Section Management:** Shared resource access is protected using FreeRTOS critical section APIs (`taskENTER_CRITICAL` and `taskEXIT_CRITICAL`).
- **Contention Handling:** A blue LED is turned on if resource contention is detected.

## Hardware Requirements
- STM32 microcontroller (e.g., STM32F4xx series)
- Three LEDs connected to GPIO pins:
  - Green LED: GPIOA Pin 0
  - Red LED: GPIOA Pin 1
  - Blue LED: GPIOA Pin 2
- FreeRTOS enabled in the project

## File Structure
- **`main.c`**: Contains the main program logic, FreeRTOS task definitions, and critical section handling.
- **CMSIS/FreeRTOS Files**: FreeRTOS kernel files for multitasking.

## Setup and Configuration
### GPIO Configuration
1. Enable GPIOA clock in the `MX_GPIO_Init` function.
2. Configure GPIO pins for the LEDs:
   - **Mode:** Output Push-Pull
   - **Speed:** Low frequency
   - **Pull:** No pull-up/down resistors

### FreeRTOS Configuration
1. Add FreeRTOS middleware to your STM32CubeMX project.
2. Define two tasks in the `osThreadNew` function:
   - `GreenLedTask`: Controls the Green LED.
   - `RedLedTask`: Controls the Red LED.
3. Set task priorities and stack sizes.

### Task Description
#### `GreenLedTask`
- Turns on the Green LED.
- Accesses the shared resource using `AccessSharedData`.
- Delays for 100ms before repeating.

#### `RedLedTask`
- Turns on the Red LED.
- Accesses the shared resource using `AccessSharedData`.
- Delays for 500ms before repeating.

### Shared Resource: `AccessSharedData`
This function simulates accessing a shared resource with contention handling:
1. Checks the `StartFlag` variable to determine if the resource is free.
2. Simulates read/write operations with a delay.
3. Indicates contention by turning on the Blue LED.

## How to Build and Run
1. Open the project in your STM32 IDE (e.g., STM32CubeIDE).
2. Build the project to generate the firmware.
3. Flash the firmware to the STM32 microcontroller.
4. Monitor LED behavior:
   - Green and Red LEDs blink according to their respective task delays.
   - Blue LED lights up briefly if resource contention occurs.

## Known Issues
- Resource contention is handled only through a visual indicator (Blue LED). Further enhancements can include using semaphores or mutexes.

## Future Enhancements
- Replace critical section handling with FreeRTOS semaphores or mutexes for more robust resource management.
- Add UART communication to log task behavior.
- Integrate an OLED display to visualize task status and resource access logs.


https://github.com/user-attachments/assets/c0390d61-9f11-496b-adc0-1aae8a89cdab


