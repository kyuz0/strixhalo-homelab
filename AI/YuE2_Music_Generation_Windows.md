# Running YuE2 music generation on Strix Halo (Windows)

YuE2 is an open music model from the Multimodal Art Projection (M-A-P) team that writes full songs (vocals and music) from your lyrics. This page describes how to run it locally on a Strix Halo PC under Windows 11 using the free *One Click Local AI* installer, with no NVIDIA GPU and no cloud.

## Requirements

| | |
|---|---|
| OS | Windows 11, 64-bit |
| PC | AMD Ryzen AI Max PC with Radeon 8060S / 8050S graphics (for example 96 GB or 128 GB mini PCs) |
| Driver | AMD Adrenalin 26.1.1 or newer |
| Graphics memory | AMD Variable Graphics Memory (VGM) of at least 32 GB, 48 GB recommended |
| Disk / network | About 40 GB free disk space and an internet connection for the downloads |

## Setting Variable Graphics Memory

YuE2 needs at least 32 GB of VGM; 48 GB is recommended. The installer checks the current VGM value during its hardware check and, if it is too low, shows you how to change it. Raise it before generating songs.

## Install

1. Download `OneClickLocalAI-Setup-0.8.0-public.exe` (free): https://github.com/HiImHal/one-click-local-ai/releases/latest
   Optionally verify it in PowerShell with `Get-FileHash .\OneClickLocalAI-Setup-0.8.0-public.exe`. Expected SHA-256: `d21d83c456fbd4fe2fe0459e9d6c9c2680a3bc277b07eb12609c8b2f56a87c5d`
2. Run it.
3. Open **One Click Local AI** from your Desktop.
4. Click **Install** on the **YuE2 music pack** and follow the setup window. You must accept the YuE2 licence. Downloads take a while; if interrupted, run the installer again and it continues where it stopped.
5. When done, open **YuE2 song generator (One Click)** from your Desktop, type a style and your lyrics, and add the song to the queue.

> [!NOTE]
> The installer is not code-signed, so Windows SmartScreen shows **"Unknown publisher"** / "Windows protected your PC". Click **More info** > **Run anyway**. Some antivirus programs may also flag it as a false positive.

Only the YuE2 music pack can be installed in the free edition; other packs are shown as *Coming in a future version*. The app is free but not open source.

**Uninstall:** Start menu > One Click Local AI > Uninstall (your songs are kept).

## Performance

On a Strix Halo test PC, a 28-second song took about 2.5 minutes to generate.

## Output

Songs are saved in `Music\YuE2-OneClick`.

## Licence

YuE2 code and model weights are **CC BY-NC 4.0** (non-commercial use only) by the M-A-P team. They are downloaded from the original publishers at install time. Songs you make are for personal, non-commercial use only.

## Links

- Installer and documentation: https://github.com/HiImHal/one-click-local-ai
- Developer: https://www.hiimhal.com
