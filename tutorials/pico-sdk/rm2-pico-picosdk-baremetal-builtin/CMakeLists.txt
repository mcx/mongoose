cmake_minimum_required(VERSION 3.13)
include(pico-sdk/pico_sdk_init.cmake)

project(firmware)
pico_sdk_init()

add_executable(firmware
	main.c
	mongoose.c
)

target_include_directories(firmware PUBLIC
	.
)

target_link_libraries(firmware hardware_pio pico_stdlib pico_rand)
pico_add_extra_outputs(firmware)     # create map/bin/hex file etc.

pico_enable_stdio_usb(firmware 1)    # Route stdio
pico_enable_stdio_uart(firmware 0)   # to USB

# Mongoose build flags in mongoose_config.h

# Example build options
