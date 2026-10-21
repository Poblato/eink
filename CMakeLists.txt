cmake_minimum_required(VERSION 3.13)
include(pico-sdk/pico_sdk_init.cmake)
project(Pico_ePaper_Code)

# add a compilation subdirectory
add_subdirectory(lib/Config)
add_subdirectory(lib/e-Paper)
add_subdirectory(lib/Fonts)
add_subdirectory(lib/GUI)
add_subdirectory(examples)

# add a header directory
include_directories(examples)
include_directories(./lib/Config)
include_directories(./lib/GUI)

# generate an executable file
add_executable(epd 
main.c
)

pico_sdk_init()

# enable usb output, disable uart output
pico_enable_stdio_usb(epd 1)
pico_enable_stdio_uart(epd 0)

# create map/bin/hex/uf2 file etc.
pico_add_extra_outputs(epd)

target_link_libraries(epd examples ePaper GUI Fonts Config pico_stdlib hardware_spi)