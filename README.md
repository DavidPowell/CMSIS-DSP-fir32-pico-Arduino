# ARM CMSIS-DSP example for Raspberry Pi Pico

This respository contains an adaptation of the [ARM CMSIS-DSP](https://arm-software.github.io/CMSIS_5/DSP/html/index.html) example `arm_fir_example_f32` for the Raspberry
Pi Pico, running the Arduino core, and compiled under [PlatformIO](https://platformio.org).

This example takes an input containing 1kHz and 15kHz sine waves, and passes them through an FIR filter to
remove the high frequency component.

This example uses 32-bit floating point data types, however the Raspberry Pi Pico's Cortex M0+ processor has
no floating point unit. For good performance, the whole program needs to be adapted for fixed point data types.

Note the following modifications:
* The build flag `-DARM_MATH_CM0_FAMILY` has been added so that assembler optimized code is generated for the correct ARM Cortex Core
* The main file has been converted to a `.ino` Arduino file, with `setup()` and `loop()` functions
* Since Arduino code is based on C++, the ARM CMSIS includes are wrapped in `extern "C" {}` to prevent linker errors
* The input and output waveforms are sent to the serial monitor for plotting (e.g. with the Arduino Serial Plotter).
