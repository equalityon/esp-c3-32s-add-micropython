# Installation of Micropython for esp-c3-32s :raccoon:
![ESP Board](/assets/esp32_board.png?raw=true)

**How to install Micropython on an ESP-C3-32S Board from AI-thinker**

# Debian 11
## Enviroment preparation

You can **become root or use the sudo** command for the process, but the easiest way it to add your current user to the dialout group (This will be needed for reading and writing on the Microcontroller with the USB interface)

    sudo adduser $USER dialout
    # reboot (if needed)

Be sure to have python3 and python3-dev packages installed

    # For virtual enviroment
    sudo apt install python3 python3-dev -y
    # For comunnication with the ESP32
    sudo apt install minicom -y 

Create a python a virtual enviroment to make the development easier.

    python3 -m venv venvesp
    source venvesp/bin/activate
    pip install pip --upgrade
    pip install esptool
    pip install ampy



## Flashing and installing

If you found trouble with any of the steps, first check of

Connect the ESP module with an USB cable and check the device Serial Port.

    esptool.py flash_id | grep "Serial port"
Then try to find the serial port parameter, it will be something like **"/dev/ttyUSB0"**

After finding the serial port, we will erase the flash (This is mandatory if is the first time you install MicroPython on this board)

    esptool.py --port /dev/ttyUSB0 erase_flash

Then download the latest version of the MicroPython bin from https://micropython.org/download/esp32c3/ (At the time of writing this, is the **esp32c3-20220117-v1.18.bin**, included on the repo, which will be used from now on).

The we will flash the binary to the board

    esptool.py --chip esp32c3 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x0 esp32c3-20220117-v1.18.bin --verify

If everything is done correctly now you will be able to communicate directly with the board using minicom

    minicom -D /dev/ttyUSB0 -b 115200

And you should be prompted with something like.

![Image_All_OK](/assets/everything_ok.png?raw=true "OK Results")

