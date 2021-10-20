# Firmware

You can use the pre-compiled firmware or custom firmware for  FYSETC Prusa mini clone plus machine.

## Pre-compiled firmware

There are two pre-build firmware for you. One is ```RELEASE-4.0.5-Modified.hex``` beside this `README` file which is base on PRUSA firmware `RELEASE-4.0.5`, the other is `RELEASE-4.3.3-Modified.hex` which is base on PRUSA firmware `RELEASE-4.3.3` version. You can choose on and directly upload this firmware to the board. Follow the [Upload firmware](#jump) instructions.

## Custom firmware

### Generate firmware from Prusa firmware

And if you think the firmware is too old , and you want to build your own firmware base on the Prusa release firmware. Then let me tell you what need to change for FYSETC Prusa mini clone plus machine. We give you two samples, one is base on `RELEASE-4.0.5` versions and the other is base on `RELEASE-4.3.3`

#### 1. Base on RELEASE-4.3.3 version

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

#### 2. Base on RELEASE-4.0.5 version

There are patch files named ```0001-Patch-for-FYSETC-Prusa-mini-clone-plus.patch``` and `0002-Fix-y-axis-self-test-bug.patch`. So if you know ```git diff``` ,then it's easy for you to know the changes. And if not,  below are the changes

In file `src/gui/gui_config_mini.h` following define is changed.

```
#define Y_LEN 253
```

In file ```include/marlin/Configuration_A3ides_2209_MINI.h``` following defines are changed.

```
#define Y_BED_SIZE 250
#define Y_MIN_POS -6
```

In file ```src/gui/wizard/firstlay.c``` , change following

```
 const char *V2_gcodes_body[] = {
     "G1 Z4 F1000",
     "G1 X0 Y-2 Z0.2 F3000.0",
     "G1 E6 F2000",
     "G1 X60 E9 F1000.0",
     "G1 X100 E12.5 F1000.0",
```

to
```
 const char *V2_gcodes_body[] = {
     "G1 Z4 F1000",
     "G1 X0 Y0 Z0.2 F3000.0",
     "G1 E6 F2000",
     "G1 X60 E9 F1000.0",
     "G1 X100 E12.5 F1000.0",
```

### Build firmware

After you finish the changes, then please follow Prusa buddy firmware build instructions to build your firmware, it is [here](https://github.com/prusa3d/Prusa-Firmware-Buddy).

## <span id="jump">Upload firmware</span>

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

On step 5, choose `RELEASE-4.3.3-Modified.hex` or `RELEASE-4.0.5-Modified.hex`
