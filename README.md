EFI Firmware Recovery

This project documents how I diagnosed and resolved a failed firmware update on a Dell Latitude 7330. The failure was caused by limited space in the EFI partition and included GNOME and system-related startup errors.

The fix involved backing up and recreating the EFI partition, analyzing performance logs, and confirming a successful firmware update.

Summary

- Firmware update failed due to insufficient EFI partition space.
- GNOME services (keyring, display) failed to start properly.
- Logs revealed multiple service-related errors.
- Snap-based applications were removed to improve stability.
- After rebuilding the EFI partition and re-running updates, the firmware installed successfully.
- Final performance checks confirmed normal operation.

Screenshots

Screenshots documenting the full process are located in the `images/` folder:

- `efi-error.png` — `df -h /boot/efi` showing limited space
- `update-fail.png` — `fwupdmgr` firmware update failed
- `firmware-success.png` — successful update confirmation
- `boot-log-before.png` — `journalctl` errors before recovery
- `boot-log-after.png` — improved logs after fixes
- `system-performance.png` — output of `free -h`, `uptime`, and `top`

Commands Used

These were run throughout the recovery and verification process.

bash
Check EFI usage
'df -h /boot/efi'

Backup and rebuild EFI partition
sudo cp -r /boot/efi/* ~/efi-backup/
sudo umount /boot/efi
sudo mkfs.fat -F32 /dev/nvme0n1p1
sudo mount /dev/nvme0n1p1 /boot/efi
sudo cp -r ~/efi-backup/* /boot/efi/

Attempt firmware update again
sudo fwupdmgr get-updates
sudo fwupdmgr update

System performance checks
free -h
uptime
top
systemd-analyze blame

Check boot-time errors
journalctl -b -p err

Remove unused Snap apps (optional cleanup)
sudo snap remove firefox
sudo snap remove snap-store
sudo snap remove snapd-desktop-integration

System Info
Dell Latitude 7330
Firmware version upgraded from 1.34.1 to 1.37.0
Ubuntu with GNOME Desktop
EFI partition: 96MB FAT32 (cleaned for space)
