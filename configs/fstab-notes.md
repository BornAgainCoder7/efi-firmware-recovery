EFI Partition Mount Fix (`/etc/fstab`)

Why I Edited This File

The firmware update failed because the EFI system partition wasn’t mounting properly.  
To fix this, I added a line to `/etc/fstab` to ensure it mounts correctly at boot time.

What I Added

fstab
UUID=40A2-5917 /boot/efi vfat defaults,nofail,x-systemd.device-timeout=5s 0 1

What This Line Does

- `UUID=40A2-5917`: This is the unique ID for my EFI partition.
- `/boot/efi`: This is where the EFI partition should be mounted.
- `vfat`: The partition is formatted as VFAT (FAT32), required by UEFI systems.
- `defaults`: Uses default mount options.
- `nofail`: Prevents the system from stopping boot if this partition isn't found.
- `x-systemd.device-timeout=5s`: Sets a 5-second timeout to wait for the device before continuing boot.
