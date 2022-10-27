# Firmware

You can use the pre-compiled firmware or custom firmware for  FYSETC Prusa mini clone plus machine.

## 1. Pre-build firmware

### 1.1 For plus kit

There is pre-build firmware for you. It is ```RELEASE-4.3.3-Modified-boot2.0.2.zip```(You need to unzip it to get .hex file) beside this `README` file which is base on PRUSA firmware `RELEASE-4.3.3` version. You can directly upload this firmware to the board. Follow the [Upload firmware](#jump) instructions.

### 1.2 Back to prusa firmware

You can upload the firmware `Buddy_4.4.0-RC1.hex` (Unzip Buddy_4.4.0-RC1.zip to get it) to go back to original prusa firmware.

## 3. Custom firmware

### 3.1 Generate firmware from Prusa firmware

And if you think the firmware is too old and you want to build your own firmware base on the Prusa release firmware. Then let me tell you what need to change for FYSETC Prusa mini clone plus machine. 

#### Base on RELEASE-4.3.3 version

There is patch file named ```0001-Patch-for-FYSETC-Prusa-mini-clone-plus-base-on-4.3.3.patch``` . So if you know ```git diff``` ,then it's easy for you to know the changes. And if not,  below are the changes

In file `src/gui/gui_config_mini.h` following variable is changed.

```
static const uint8_t Y_LEN = 253;
```

In file ```include/marlin/Configuration_A3ides_2209_MINI.h``` following defines are changed.

```
#define Y_BED_SIZE 250
#define Y_MIN_POS -6
```

In file `src/common/selftest/selftest_MINI.cpp` following variable is changed.

```
static const selftest_axis_config_t Config_YAxis = { .partname = "Y-Axis", .length = 255, .fr_table = XYfr_table, .length_min = 249, .length_max = 259, .axis = Y_AXIS, .steps = 4, .dir = 1 };
```

### 3.2 Build firmware

After you finish the changes, then please follow Prusa buddy firmware build instructions to build your firmware, it is [here](https://github.com/prusa3d/Prusa-Firmware-Buddy).

## 4 <span id="jump">Upload firmware</span>

If you generate a ```.bbf``` file , you just need to copy the file to USB disk and plug it into machine and then reboot the machine.

If you want to upload ```.hex``` file , following are the instructions.

### Step 1: download STM32CubeProgrammer

You can download it from ST website.

https://www.st.com/zh/development-tools/stm32cubeprog.html

### Step 2: Close the jumper,and connect motherboard to your computer with USB cable

<img src="boot3v3.png" style="zoom:50%;" />

---

### Step 3: Download

![STM32CUBEP](upload.png)

Note: 

On step 5, choose `RELEASE-4.3.3-Modified.hex`.
