Mac OS X Build Instructions and Notes
======================================

### Install

It's important to recursively clone our repository:

```bash
$ git clone --recursive https://github.com/joltwallet/jolt_wallet.git
```

### Dependencies

Jolt depends on a few external tools that must be properly setup before we can run.

**CMake**

If you are on a Mac, you can easily get CMake with Brew:

```bash
$ brew install cmake
```

For other users, please follow this tutorial: https://cmake.org/cmake-tutorial/

**ESP-IDF**

There is an excellent guide on how to setup the framework here: http://esp-idf.readthedocs.io/en/latest/get-started/macos-setup.html

Once you've completed the setup, be sure to move your `esp-idf` and `xtensa-esp32-elf` folders to the same directory you downloaded the Jolt repository.

**CP210x Driver**

Please download and run the drivers for your Operating System here: https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers

### Paths

Open up your local bash profile configuration and be sure to add the following:

```bash
  export NANOHOME=/your/root/path/where/Jolt/and/ESP/folders/are
  export PATH=$PATH:$NANOHOME/xtensa-esp32-elf/bin
  export IDF_PATH=$NANOHOME/esp-idf
  export MSYS_FLAGS=""
  export VERBOSE=""
```

_**NOTE:** If your computer has issues creating a `/dev/tty.USB0` folder when connecting your device, then be sure to add the following to your local bash:_

```bash
  # my be required if /dev/tty.USB0 does not exist
  export ESPPORT=/dev/cu.SLAB_USBtoUART
```

### Setup

Before we can start to build and run, there are a few final pieces that need to be done.

**Menu Config**

Run the following:

```bash
  cd $NANOHOME
  make menuconfig
```

You will then be prompted with a blue screen. Using the Enter and arrow keys, go to:
1. Component config
2. ESP32-specific
3. Main XTAL frequency
4. select 26 for the value
5. Save and Exit

**Wifi**

```bash
cd $NANOHOME/main
cp example_wifi.h wifi.h
vi wifi.h
```

Be sure to set the values of `AP_TARGET_SSID` and `AP_TARGET_PASSWORD` to your router's wireless network name and password, respectively.

### Build + Run

Once you're ready, you can run any of the following to either build, run, or both!

**Build and Flash**

To build your project and flash to your device, run:

```bash
cd $NANOHOME
make flash
```

**Build, Flash, and Monitor**

To build, flash, and monitor your device, run:

```bash
cd $NANOHOME
make flash monitor
```


**Monitor**

To simply re-launch and monitor your device, run:

```bash
cd $NANOHOME
make monitor
```

### Additional Resources

**Useful Links**

* http://esp-idf.readthedocs.io
* https://www.silabs.com
* https://joltwallet.com
* https://leanpub.com/kolban-ESP32

**Useful Commands**

```bash
$ make menuconfig
$ make flash
$ make monitor
$ make flash monitor
$ make erase_flash
```
