# PixelOS for Motorola Moto G60 (hanoip)

Unofficial PixelOS builds for the Motorola Moto G60 (hanoip).

PixelOS is an AOSP-based custom ROM that brings the Pixel look and features, with Google apps included.

## Current build: PixelOS 16

| | |
|---|---|
| **Device** | Motorola Moto G60 (hanoip) |
| **Android** | 16 (security patch 2026-06-01) |
| **Kernel** | Linux 4.14 |
| **Based on** | PixelOS 16 (sixteen-qpr2) and PianoDev0's hanoip sources |
| **Build type** | user, signed with private release keys |
| **Status** | Beta |
| **Maintainer** | [luizpaulo2005](https://github.com/luizpaulo2005) |

## Requirements

- Unlocked bootloader.
- **Stock Android 12 firmware.** These builds don't include firmware (modem, DSP, bootloader). Flash the latest stock Android 12 for your region before installing.

## Downloads

- **ROM zip:** [SourceForge](https://sourceforge.net/projects/pixelos-hanoip/files/)
- **Fastboot images and source manifest:** [GitHub Releases](https://github.com/luizpaulo2005/pixelos-hanoip/releases)
- **Support and discussion:** XDA thread (coming soon)

| File | Use |
|---|---|
| `boot.img` | Kernel |
| `vendor_boot.img` | Vendor ramdisk and recovery |
| `dtbo.img` | Device tree overlay |
| `vbmeta.img` | Verified boot metadata |
| `build-manifest.xml` | Exact commit of every repository in the build |
| `sha256sums.txt` | Checksums |

## What works

Tested without a SIM card:

- Boot, SELinux Enforcing, file-based encryption, verified boot (green)
- Wi-Fi, Bluetooth, NFC, GPS
- Camera, audio, fingerprint, charging
- Google apps and Play Store

## Not tested yet

- Calls, SMS, mobile data, VoLTE (no SIM was available). Reports are welcome.
- Vibration, auto-brightness

## Known issues

- The kernel version ends in `UNSTABLE`. That is just the name of the upstream kernel, not a debug build.

Please report other issues with logs.

## Installation

Clean install. Your bootloader must be unlocked. **This wipes all your data.**

1. Make sure the phone is on stock Android 12 firmware.
2. Download the zip and `boot.img`, `vendor_boot.img`, `dtbo.img`, `vbmeta.img`.
3. Reboot to bootloader (power off, hold Volume Down + Power).
4. Flash the partitions:
   ```
   fastboot flash boot boot.img
   fastboot flash vendor_boot vendor_boot.img
   fastboot flash dtbo dtbo.img
   fastboot flash vbmeta vbmeta.img
   ```
5. Using the volume keys, choose **Recovery Mode** and confirm with Power.
6. In recovery: **Factory reset > Format data / factory reset**.
7. **Apply update > Apply from ADB**, then on your computer:
   ```
   adb sideload PixelOS_hanoip-16.2-<date>-UNOFFICIAL-signed.zip
   ```
8. **Reboot system now.** The first boot takes 5 to 10 minutes.

## Updating

From a previous build of this ROM: Recovery > **Apply update > Apply from ADB** > `adb sideload` the new zip > Reboot. No wipe needed.

## Changes in these builds

- Ported PianoDev0's device tree to PixelOS.
- Fixed a bootloop: the Power HAL couldn't find `libperfmgr` (wrong Soong namespace).
- Fixed a `system_server` hang: added sepolicy for the LineageOS health HAL (charging control).
- Fixed the dynamic partition sizes for builds with Google apps.
- Signed with private release keys.

## Sources

- Device tree: [luizpaulo2005/android_device_motorola_hanoip](https://github.com/luizpaulo2005/android_device_motorola_hanoip/tree/16.0)
- Vendor: [luizpaulo2005/android_vendor_motorola_hanoip](https://github.com/luizpaulo2005/android_vendor_motorola_hanoip/tree/16.0)
- Kernel: [PianoDev0/android_kernel_motorola_sm6150](https://github.com/PianoDev0/android_kernel_motorola_sm6150/tree/16.0)
- Motorola hardware (Dolby): [PianoDev0/android_hardware_motorola](https://github.com/PianoDev0/android_hardware_motorola/tree/16.0)
- Local manifest: [hanoip.xml](hanoip.xml)
- PixelOS: [PixelOS-AOSP](https://github.com/PixelOS-AOSP)

## Credits

- PixelOS team
- PianoDev0 for the hanoip device, vendor and kernel sources
- LineageOS
