- Contents of the file system:
  - rootfs.img
    The image is editable without extract it:
    - $ mount -o loop rootfs.img /mount_point
      If the abobe command fails, try next:
    - $ losetup -f rootfs.img
    - $ losetup --list
    - $ mount /dev/loop
  - android-rootfs.img # Linux filesystem data
    - /userdata: It's a link to "/halium-system/var/lib/lxc/android/android-rootfs.img"
    - /var/lib/lxc/android/android-rootfs.img
    - File size:
      - lavender-droidian-bullseye: 575836160B(550MB)
      - lavender-droidian-bookworm: 575852544B(550MB)

BOOT PROCESS
  - /var/lib/lxc/android/config
    LXC container config. Defines android rootfs path, apparmor_status, exec pre-start.sh, create devs...
  - /var/lib/lxc/android/pre-start.sh
    Mounts android lxc container
  - /var/lib/lxc/android/rootfs
  - 
