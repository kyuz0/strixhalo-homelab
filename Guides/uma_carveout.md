# Set the AMD GPU UMA carveout to 512 MB on the GMKtec EVO-X2

## Background

GMKtec introduced changes to the smallest UMA carveout setting available in the BIOS setup from 512 MB to 1 GB, and later to 2 GB.

On a system whose BIOS/VBIOS supports AMD's UMA allocation interface, the Linux `amdgpu` driver can expose a sysfs setting for changing the carveout from Linux. This provides a way to select the 512 MB option even when that setting is no longer available in the BIOS graphical interface.

This was tested on the GMKtec EVO-X2 described below. It has not been verified here on other systems or firmware versions.

## Kernel version

The `amdgpu` UMA carveout sysfs interface was merged upstream for Linux **7.0-rc1**. Some distributions may backport the feature to earlier kernel versions.

The sysfs files are only created when the platform firmware exposes the necessary UMA carveout support. If the `uma` directory or its files are missing, your BIOS/VBIOS or kernel may not support the interface.

## Example system

```text
Linux x2 7.4.0-0.rc1.261108.fa4ad798.516.vanilla.fc46.x86_64 #1 SMP PREEMPT_DYNAMIC Sun Nov 8 08:22:35 UTC 2026 x86_64 GNU/Linux
```

## Check the current carveout

List the available options and current setting:

```bash
grep . /sys/class/drm/card*/device/uma/carveout_options \
        /sys/class/drm/card*/device/uma/carveout
```

On my system, the current setting was `2`, corresponding to 2 GB:

```text
/sys/class/drm/card1/device/uma/carveout_options:0: Minimum (512 MB)
/sys/class/drm/card1/device/uma/carveout_options:1:  (1 GB)
/sys/class/drm/card1/device/uma/carveout_options:2:  (2 GB)
/sys/class/drm/card1/device/uma/carveout_options:3:  (4 GB)
/sys/class/drm/card1/device/uma/carveout_options:4:  (8 GB)
/sys/class/drm/card1/device/uma/carveout_options:5:  (16 GB)
/sys/class/drm/card1/device/uma/carveout_options:6: Medium (32 GB)
/sys/class/drm/card1/device/uma/carveout_options:7: High (64 GB)
/sys/class/drm/card1/device/uma/carveout:2
```

The GPU reported 2048 MB of VRAM:

```bash
sudo dmesg | grep -i "amdgpu.*memory"
```

Example output:

```text
[    4.963880] amdgpu 0000:c5:00.0: Trusted Memory Zone (TMZ) feature disabled as experimental (default)
[    4.964694] amdgpu 0000:c5:00.0:  2048M of VRAM memory ready
[    4.964701] amdgpu 0000:c5:00.0:  126411M of GTT memory ready.
```

## Set the carveout to 512 MB

In the options list, `0` corresponds to **Minimum (512 MB)**. On my system, the path was under `card1`. Check your own path before running the command.

```bash
echo 0 | sudo tee /sys/class/drm/card1/device/uma/carveout
sudo reboot
```

## Verify after reboot

Check the options and current setting again:

```bash
grep . /sys/class/drm/card*/device/uma/carveout_options \
        /sys/class/drm/card*/device/uma/carveout
```

After reboot, my system showed `carveout:0`:

```text
/sys/class/drm/card0/device/uma/carveout_options:0: Minimum (512 MB)
/sys/class/drm/card0/device/uma/carveout_options:1:  (1 GB)
/sys/class/drm/card0/device/uma/carveout_options:2:  (2 GB)
/sys/class/drm/card0/device/uma/carveout_options:3:  (4 GB)
/sys/class/drm/card0/device/uma/carveout_options:4:  (8 GB)
/sys/class/drm/card0/device/uma/carveout_options:5:  (16 GB)
/sys/class/drm/card0/device/uma/carveout_options:6: Medium (32 GB)
/sys/class/drm/card0/device/uma/carveout_options:7: High (64 GB)
/sys/class/drm/card0/device/uma/carveout:0
```

The GPU then reported 512 MB of VRAM:

```bash
sudo dmesg | grep -i "amdgpu.*memory"
```

Example output:

```text
[    5.079347] amdgpu 0000:c5:00.0: Trusted Memory Zone (TMZ) feature disabled as experimental (default)
[    5.080155] amdgpu 0000:c5:00.0:  512M of VRAM memory ready
[    5.080156] amdgpu 0000:c5:00.0:  126976M of GTT memory ready.
```

The DRM card index changed from `card1` to `card0` after reboot in this example. Re-check the sysfs path rather than assuming the card number will stay the same.

## References

- [Linux kernel AMDGPU documentation: UMA Carveout](https://www.kernel.org/doc/Documentation/gpu/amdgpu/driver-misc.rst)
- [AMD SMI documentation: Memory Configuration](https://rocm.docs.amd.com/projects/amdsmi/en/7.13.0-preview/doxygen/docBin/html/group__tagMemConfig.html)