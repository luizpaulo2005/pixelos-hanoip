# PixelOS for Motorola Moto G60 (hanoip)

Unofficial PixelOS builds for the Motorola Moto G60 (hanoip).

PixelOS is an AOSP-based custom ROM that brings the Pixel look and features, with Google apps included.

## Current build: PixelOS 17

| | |
|---|---|
| **Device** | Motorola Moto G60 (hanoip) |
| **Android** | 17 (security patch 2026-11-01) |
| **Kernel** | Linux 4.14 |
| **Based on** | PixelOS 17 and jonashofficial's (formerly PianoDev0) hanoip sources |
| **Build type** | user, signed with private release keys |
| **Status** | Beta |
| **Maintainer** | [luizpaulo2005](https://github.com/luizpaulo2005) |

## Requirements

- Unlocked bootloader.
- **Stock Android 12 firmware.** These builds don't include firmware (modem, DSP, bootloader). Flash the latest stock Android 12 for your region before installing.

## Downloads

- **ROM zip:** [SourceForge](https://sourceforge.net/projects/pixelos-hanoip/files/). The zip is larger than GitHub's 2 GiB limit.
- **Fastboot images and source manifest:** [GitHub Releases](https://github.com/luizpaulo2005/pixelos-hanoip/releases)
- **Support and discussion:** [XDA thread](https://xdaforums.com/t/rom-17-unofficial-pixelos-17-for-motorola-moto-g60-hanoip.4810210/)

| File | Use |
|---|---|
| `boot.img` | Kernel |
| `vendor_boot.img` | Vendor ramdisk and recovery |
| `dtbo.img` | Device tree overlay |
| `vbmeta.img` | Verified boot metadata |
| `build-manifest.xml` | Exact commit of every repository in the build |
| `sha256sums.txt` | Checksums of every file, including the ROM zip |

## What works

- Boot, SELinux Enforcing, encryption
- Calls, SMS, mobile data
- VoLTE and Wi-Fi calling, tested on Vivo (Brazil)
- Wi-Fi, Bluetooth, NFC, GPS
- Moto Camera 5 (rear and front)
- Audio with Dolby Atmos
- Fingerprint, vibration
- Sensors and auto-brightness
- Charging
- Google apps and Play Store

## Known issues

- During setup, the Play Store may install the **Moto** app (`com.motorola.moto`). It needs Motorola's stock framework and crashes on custom ROMs. Uninstall it. Moto gestures are in Settings (MotoActions).

Please report other issues with logs.

## Installation

Clean install, also required when coming from PixelOS 16. Your bootloader must be unlocked. **This wipes all your data.**

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
   adb sideload PixelOS_hanoip-17.0-<date>-UNOFFICIAL-signed.zip
   ```
8. **Reboot system now.** The first boot takes 5 to 10 minutes.

## Updating

From a previous PixelOS 17 build of this ROM: Recovery > **Apply update > Apply from ADB** > `adb sideload` the new zip > Reboot. No wipe needed.

## Changes in these builds

- System, system_ext, product and vendor use EROFS (lz4hc), which frees about 1.8 GB in the super partition.
- Moto Camera 5 and Dolby Atmos from jonashofficial's 17.0 device tree.
- Fixed a bootloop: the Power HAL couldn't find `libperfmgr` (its Soong namespace moved in PixelOS 17).
- Fixed build conflicts with PixelOS's own Dolby package and duplicate Dolby properties.
- Signed with private release keys.

## Previous builds

- PixelOS 16.2: [GitHub release](https://github.com/luizpaulo2005/pixelos-hanoip/releases/tag/16.2-20261102), zip in the SourceForge `16/` folder, [XDA thread](https://xdaforums.com/t/rom-16-unofficial-pixelos-16-for-motorola-moto-g60-hanoip.4807454/)

## Sources

- Device tree: [luizpaulo2005/android_device_motorola_hanoip](https://github.com/luizpaulo2005/android_device_motorola_hanoip/tree/pixelos-17)
- Vendor: [luizpaulo2005/android_vendor_motorola_hanoip](https://github.com/luizpaulo2005/android_vendor_motorola_hanoip/tree/pixelos-17)
- Kernel: [jonashofficial/android_kernel_motorola_sm6150](https://github.com/jonashofficial/android_kernel_motorola_sm6150/tree/17.0)
- Motorola hardware (Dolby): [jonashofficial/android_hardware_motorola](https://github.com/jonashofficial/android_hardware_motorola/tree/17.0)
- Local manifest: [hanoip.xml](hanoip.xml)
- PixelOS: [PixelOS-AOSP](https://github.com/PixelOS-AOSP)

## Credits

- PixelOS team
- jonashofficial (PianoDev0) for the hanoip device, vendor and kernel sources
- LineageOS
