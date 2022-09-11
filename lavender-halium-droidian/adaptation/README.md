## Adaptation files for Xiaomi Redmi Note 7 (lavender) running Droidian Bookworm.
In this folder you will find some adaptation zips with fixes and customizations for **xiaomi lavender**. 
The zips are prepared to be flashed from a custom recovery.

## List of files
### 1. Fix blackscreen:
> Download: [droidian-unofficial-recovery-adaptation-blackscreen-fix-lavender_2022-09-11.zip](https://github.com/berbascum/droidian-tools-collection-unofficial/blob/main/lavender-halium-droidian/adaptation/droidian-unofficial-recovery-adaptation-blackscreen-fix-lavender_2022-09-11.zip).

This zip fixes the black screen issue after booting Droidian.
This fix can solve the problem if phosh service can start, and you can establish a RNDIS ssh connection to device.
To trouble if this is your scenario, after connecting over ssh, try this command:

```
cat /sys/class/leds/lcd-backlight/max_brightness > /sys/class/leds/lcd-backlight/brightness
```
If the screen appears, probably this fix will help you, but must be noted that i have only tested on **xiaomi lavender**!
> I have take the rules applied by this zip from a One Plus 3 image, so it may work on other devices.
 \
 \
> This zip only contains the black screen fix so you can try it without other fixes or customizations.



### 2. General fixes for xiaomi lavender:
Download: [droidian-unofficial-recovery-adaptation-lavender_2022-09-11.zip](https://github.com/berbascum/droidian-tools-collection-unofficial/blob/main/lavender-halium-droidian/adaptation/droidian-unofficial-recovery-adaptation-lavender_2022-09-11.zip).

This zip applies all tested fixes for **xiaomi lavender** running Droidian.
Currently supports **two** fixes:
#### - Black screen fix:
  > Same as fix 1.
#### - Bluebinder service chash fix
  Bluebinder service crashes on **xiaomi lavender** while booting, and bluetooth can not be started once device is booted.
  > Thies fix solves this problem.


### 3. Custom phoc.ini scale to "2":
> Download: [droidian-unofficial-recovery-adaptation-scale-2_2022-09-11.zip](https://github.com/berbascum/droidian-tools-collection-unofficial/blob/main/lavender-halium-droidian/adaptation/droidian-unofficial-recovery-adaptation-scale-2_2022-09-11.zip).

This zip changes any **scale = 3** existing value in **phoc.ini** to **scale = 2**. When it's applied just after flashing Droidian rootfs, the changes will take effect in first boot.
> Whith scale != 3, Droidian 1st time configuration assistant is not usable on portrait mode, but it is in landscape.

 \
Thanks to Droidian Team for their constant help!
