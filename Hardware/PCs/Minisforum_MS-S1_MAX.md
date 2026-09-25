# Minisforum MS-S1 MAX

![Minisforum MS-S1 MAX](./Minisforum_MS-S1_MAX/minisforum-ms-s1-max.jpg)

[[OFFICIAL PRODUCT PAGE](https://store.minisforum.com/products/minisforum-ms-s1-max-mini-pc)]

Something interesting with unique(?) board, cooling, 2x10G ethernet and integrated PSU.

### User Manual
- [User Manual zip](https://pc-file.s3.us-west-1.amazonaws.com/MS-S1+MAX/user+manual/%E7%94%B5%E5%AD%90%E6%A1%A3%E8%AF%B4%E6%98%8E%E4%B9%A6+SHWSA+(10%E4%B8%AA%E8%AF%AD%E8%A8%80+V1)+2025.10.23.zip)

Availability: September 2025.

> [!NOTE]
> The included 10G NICs are unstable on Linux with older kernels. More info:  
> - https://www.reddit.com/r/MINISFORUM/comments/1ovcph0/mss1_max_arrived_both_realtek_nics_missing_from/
> - https://bugzilla.kernel.org/show_bug.cgi?id=220770
> 
> Make sure that you're running kernel 6.17.11 or 6.18+ to avoid problems.

### Fan control (Linux)

The stock fan curve is conservative (~40% duty only at 93 °C), so under sustained CPU/GPU load (e.g. local LLM inference) the APU reaches Tjmax and throttles. The MS-S1 MAX exposes no standard Linux fan control (no hwmon PWM, no tachometer, no ACPI fan object), and on Fedora `ec_sys` is unavailable while Secure Boot lockdown blocks debugfs.

Open-source tool for this board: **[ms-s1-max-fans-control](https://github.com/raimondomartire/ms-s1-max-fans-control)** — a small signed kernel module exposes the EC as `/dev/strixec` (works under Secure Boot + SELinux), with CLI/GUI fan-curve profiles and systemd persistence.

Reverse-engineered EC map: CPU temperature at `0x09`; fan-curve tables at `0x11` (fan 1) and `0x31` (fan 2), 7 × 3-byte records `[temp, hysteresis, duty%]` read live by the firmware. Note: this board is **not** a Sixunited AXB35-02 (different EC layout). Full details in the repo's `docs/EC-MAP.md`.
