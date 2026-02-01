# EFI Partition Mount Fix (`/etc/fstab`)

## Why I Edited This File

The firmware update failed because the EFI system partition wasn’t mounting properly.  
To fix this, I added a line to `/etc/fstab` to ensure it mounts correctly at boot time.

---

## What I Added

```fstab
UUID=40A2-5917 /boot/efi vfat defaults,nofail,x-systemd.device-timeout=5s 0 1
