# Notes about testing Droidian on xiaomi lavender

BOOKWORM BUGS
- The bookworm rootfs images are booting fine on xiaomi lavender, but screen is not displaying anything.

- By connecting with ssh over RNDIS and issuing next command,  instantly desktop is showed on screer.
     $ sudo echo "2047" > /sys/class/leds/lcd-backlight/brightness
     NOTE: 2047 is the defaut value on the file. So the solution is not the value itself, but the file edition itself with some permited value that modifies the file.
  But this solution is not permanent, and using it causes a one time bootloop in next reboot or poweron.

- Also tried sleeping 5 seconds phosh.service before it starts, but not works. I guess i'ts a very early problem.

- Also tried with kernel rebuild and diff of kernel .config with other working devices.

- The problem did not exist since Droidian bullseye snapshot 22, so i'm currently testing on it.

SOLVED:
The problem is caused by missing udev rules.
Also patches for device led.
Simply add "/etc/udev/rules.d/90-backlght.rules" with the contents:
#Rules to allow controlling of backlight and leds for video group
ACTION=="add", SUBSYSTEM=="backlight", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="leds", RUN+="/bin/chgrp input /sys/class/leds/%k/brightness"
ACTION=="add", SUBSYSTEM=="leds", RUN+="/bin/chmod g+w /sys/class/leds/%k/brightness"


The solution has taken from the next url:
https://gitlab.com/Bettehem/op3-gsi-fix-droidian/-/blob/main/gsi-fix/files/90-backlight.rules
Also there are other gsi fixes that may been usefull.

TO DO:

- Compare boot.img from zip with a yet booted one.
- Create fastboot rootfs image.
