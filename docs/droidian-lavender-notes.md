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

TESTING IN BUYSELLE
- After flashing Droidian rootfs snapshot 22, device boots fine and image is swhowed on screen.

- After an update and upgrade (not dist-upgrade or full-upgrade) device reboot fine

- In next steep i have updated from bookworm nightly rootfs.img next dirs:
  - "etc/apt"
  - "usr/share/droidian-apt-config"
  - "/var/lib/extrepo" (wich have updated keys for mobian and hybris repos)
