```bash
# Set flash parallelism mode to 32, 16, or 8 bit when using STM32 F2/F4 microcontrollers

# Uncomment next line, 2=32 bit, 1=16 bit and 0=8 bit parallelism mode

#monitor flash set_parallelism_mode 2

# Set character encoding
set host-charset CP1252
set target-charset CP1252

# Reset to known state
monitor reset

# Load the program executable
#load        

# Reset the chip to get to a known state. Remove "monitor reset" command
# if the code is not located at default address and does not run by reset.
monitor reset

# Enable Debug connection in low power modes (DBGMCU->CR)
set *0xE0042004 = (*0xE0042004) | 0x7

# Set a breakpoint at main().
tbreak main

# Run to the breakpoint.
continue
```