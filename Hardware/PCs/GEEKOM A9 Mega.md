# GEEKOM A9 Mega

![Geekom A9 Mega](./GEEKOM A9 Mega/geekom-a9-mega.png)

[[OFFICIAL PRODUCT PAGE](https://www.geekompc.com/geekom-a9-mega-mini-pc/)]

Something interesting with unique(?) board, 2x2.5G ethernet and a case in Mac Studio style. Originally appeared [on Kickstarter](https://www.kickstarter.com/projects/1906688106/geekom-a9-mega-the-most-powerful-mini-pc-on-earth).

Availability: available since November 2025.

### Specifications

- **CPU:** AMD Ryzen AI Max+ 388 / Max+ 395 (16C/32T, up to 5.1 GHz, cTDP 45–120 W); a Max+ 495 configuration is also offered
- **GPU:** Radeon 8060S (Max+ 395), up to 4 display outputs
- **NPU:** 50 TOPS
- **Memory:** onboard LPDDR5X-8000 — 64 GB (388), 128 GB (395), 192 GB (495)
- **Storage:** 2× M.2 2280 PCIe Gen4 x4 NVMe, RAID 0/1 supported
- **Networking:** 2× 2.5 GbE RJ45 (dual 10 GbE on some SKUs), Wi-Fi 7 (802.11be)
- **I/O:** 2× USB4 40 Gb/s (rear, with DisplayPort 2.1), 2× HDMI 2.1 FRL (up to 8K/60 Hz), USB 3.2 Gen 2 Type-A / Type-C, SDXC card reader, fingerprint button
- **Cooling:** dual fans + vapor chamber
- **Power:** 330 W external adapter (20 V)
- **Dimensions / weight:** 171 × 171 × 71 mm, 1.9 kg, aluminium-alloy chassis, silver
- **OS support:** Windows 11, Linux

### Local LLM performance — open benchmark data

GEEKOM publishes its local-LLM benchmark records for this machine openly (llama.cpp on ROCm, Ubuntu): 72 measured records covering single-node runs, 2- and 3-node clusters linked over the 40 Gb/s USB4 ports, and contexts up to 256K — including the failed runs.

- Dataset (CC BY 4.0): https://huggingface.co/datasets/geekom-ai/a9-mega-local-llm-benchmarks
- Source repository: https://github.com/GEEKOMOfficial/geekom-a9-mega-local-llm-benchmarks
- Interactive explorer: https://huggingface.co/spaces/geekom-ai/a9-mega-benchmark-explorer
