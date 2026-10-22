# BC-250 Unofficial Community Guide

> **Turn a $100-175 mining board into a Linux gaming PC.** The BC-250 carries a cut-down PS5 "Oberon" APU — 6 Zen 2 cores (up to 8 unlockable), 24 RDNA 2 CUs (up to 40 unlockable), 16 GB GDDR6. Performance: RX 6600–RX 6700 level with CU/core unlocks (see price history below). Total build: **~$150-275**.
>
> **Linux is the recommended target.** An open Windows 11 driver now exists (`amdgpu-wddm` / "Nagi" — desktop, D3D12 with RT, and Vulkan on the GPU) but it is experimental and test-signed (no anticheat games); still expect Linux for a smooth experience (see [11 — Community & Resources](11-community-and-resources.md)).
>
> [Discord](https://discord.gg/8eZfFWhczz) · [Wiki](https://github.com/katzzero/bc250-unofficial-community-guide/wiki) · [Changelog](changelog.md) · [Contribute](CONTRIBUTING.md)

---

## Start Here

If you just bought a BC-250, follow this step-by-step guide:

### [00 — From Zero to Gaming](00-from-zero-to-gaming.md)

Linear walkthrough: purchase → assembly → BIOS flash → OS install → first game running. Takes about 2 hours.

---

## Is This Guide for You?

- **Yes, if** you're comfortable in Linux (or willing to learn) and want maximum performance per dollar on a tinkering project.
- **No, if** you need a polished plug-and-play Windows experience, or warranty support — the community Windows driver is experimental and this is niche, community-maintained hardware.

---

## What's in This Guide

| # | File | Topic |
|---|------|-------|
| **00** | **[From Zero to Gaming](00-from-zero-to-gaming.md)** | **Start here — complete setup walkthrough** |
| 01 | [Hardware Specifications](01-hardware-specs.md) | Board specs, APU details, connectors, pinouts |
| 02 | [BIOS & Firmware](02-bios-and-firmware.md) | BIOS flashing, VRAM config, 40 CU unlock |
| 03 | [Power Supply Guide](03-power-supply-guide.md) | PSU options with verified specs & purchase links |
| 04 | [Cooling Guide](04-cooling-guide.md) | Heatsink mods, fans, thermal pads, temps |
| 05 | [OS Installation](05-os-installation.md) | CachyOS (recommended), Bazzite, Fedora, Arch, Debian, Ubuntu |
| 06 | [GPU Governor](06-gpu-governor.md) | Governor install, tuning, overclocking |
| 07 | [Game Benchmarks](07-game-benchmarks.md) | 60+ community-tested games with FPS data |
| 08 | [Display & Audio](08-display-and-audio.md) | DP/HDMI, audio, VRR, multi-monitor |
| 09 | [WiFi & Peripherals](09-wifi-and-peripherals.md) | WiFi/BT adapters, SSDs, USB accessories |
| 10 | [Troubleshooting](10-troubleshooting.md) | Error reference, fixes, debugging commands |
| 11 | [Community & Resources](11-community-and-resources.md) | Discord, repos, timeline, YouTube coverage |
| 12 | [AI Inference & LLMs](12-ai-inference.md) | llama.cpp, Ollama, Stable Diffusion, ROCm |
| 13 | [Case Mods & Custom Enclosures](13-case-mods.md) | 3D-printable cases, commercial sources |
| 14 | [Reddit Community (r/BC250Gaming)](14-reddit.md) | Subreddit roundup: builds, technical leads, price signals |

---

## Quick Specs

| Spec | Value |
|------|-------|
| **APU** | AMD BC-250 "Cyan Skillfish" — cut-down PS5 Oberon |
| **CPU** | 6× Zen 2 (@ ~3.5 GHz, up to 8 unlockable via SMU BIOS shim) |
| **GPU** | 24 RDNA 2 CUs (up to 40 unlockable), 1500–2300 MHz |
| **Memory** | 16 GB GDDR6 shared — 14 Gbps, 256-bit, ~448 GB/s |
| **Storage** | 1× M.2 2280 (PCIe 2.0 x2 — ~1 GB/s max, don't overspend) |
| **Display** | 1× DisplayPort 1.4 (no HDMI — passive adapter ~$5) |
| **Network** | 1× Gigabit Ethernet (no WiFi — USB adapter needed) |
| **USB** | 2× USB 3.0 + 2× USB 2.0 |
| **TDP** | 220W typical, 235W peak gaming, 250–320W Furmark |
| **OS** | Linux only — CachyOS (recommended), Bazzite, Fedora 43+, Arch, Debian |

---

## Quick Shopping

| Item | Recommendation | Price |
|------|---------------|-------|
| **Board** | BC-250, BIOS P2.00–P3.00 or P5.00 (avoid P4.00) | ~$80–150 |
| **PSU** | FSP500-30AS Flex ATX (eBay `389522369783`) or Mean Well LOP-400 | ~$15–65 |
| **Fan** | Arctic P12 Pro / P12 Max 120mm | ~$8–12 |
| **Thermal pad** | PTM7950 phase-change pad (Amazon `B0F9Y5SCK2`) | ~$10 |
| **Thermal pads** | 1.5mm front + 2.0mm back for VRAM | ~$8 |
| **Display cable** | Passive DP-to-HDMI adapter | ~$5 |
| **WiFi adapter** | TP-Link Archer TX10UB Nano (WiFi 6 + BT 5.3) | ~$20 |
| **SSD** | Any M.2 NVMe (PCIe 2.0 x2 — cheap drives saturate the bus) | ~$25 |
| | **Total (approx)** | **~$150–275** |

**Board price history** (community data): Dec 2025 ~$62–125 (new $125, used $65, some $62 — gadgetgeek., 29/11–19/12/2025) → Dec 2025 ~$175 (gennro, 28/12/2025) → Jan 2026 settled at **$150–200** (iambryan_x1, 24/01/2026; predicted $200–250 new / $150 used — vicomte.me, 10/01/2026) → Apr 2026 still under $150 (essdee4336, 23/04/2026) → Aug 2026 back down to ~$100–125 (strykur, 03/08/2026) → **Mid–Late Oct 2026: spike** — AliExpress main listing briefly went off-site (10/12), Canada boards reported near $400 (was $250 two months earlier), EU eBay 400–450 €, with the community openly discussing a $500 target (u/Sudowoodo-Official / u/redfoxkiller / u/fabulot, 12–20/10/2026, reddit). Prices are volatile — verify current listings before buying.

---

## Important Warnings

1. **Linux-first** — a functional-but-experimental Windows 11 driver (`amdgpu-wddm`/Nagi) exists, test-signed with no anticheat support — see [05 → Windows 11 (Experimental)](05-os-installation.md#windows-11-experimental)
2. **Always clear CMOS** after BIOS flash — settings won't stick otherwise
3. **Disable IOMMU** in BIOS — broken, causes display failures
4. **Use kernel 7.2.x (current CachyOS standard) or 6.18 LTS** — avoid 6.15.0–6.15.6 and 6.17.8–6.17.10; on 8-core boards the CachyOS kernel needs its `0001` telemetry patch; roll back via boot menu if an update breaks display (Sep 2026). Canonical table: [Kernel Support Matrix (05)](05-os-installation.md#kernel-support-matrix-canonical--as-of-2026-10-09)
5. **Governor voltage: minimum 700 mV** — below that GPU locks to 1500 MHz
6. **Never use 6-pin to 8-pin PCIe adapters** — fire hazard
7. **Never use Smokeless_UMAF** — can permanently damage the board
8. **Don't lose the 4 nylon washers** under heatsink screws — missing = 90–100°C idle
9. **VRAM has no temperature sensor** — must cool backplate actively
10. **No usable hardware video encode/decode today** — VCN 2.0.3 present but power-gated; an opt-in RC-kernel firmware path (`bc250-vcn-fw`) is emerging but the PSP still rejects the blob and **only ~40% of chips have a functional VCN block**. A private H.264 demo exists but is reboot-fragile — [02 VCN research](02-bios-and-firmware.md#vcn-hardware-video-decode), [10](10-troubleshooting.md#vcn-still-not-working)
11. **CPU core voltage ("Vid") must never exceed 1.325 V** — exceeding it can permanently brick the board (yrouel86, 07/10/2026)

---

## Performance Unlocks

The BC-250 ships lock-down — the PS5 "Oberon" APU was cut down to 6 CPU cores and 24 Compute Units. Both are unlockable with community tools:

### 40 CU GPU Unlock (RDNA 2)

Stock board has 24 of 40 CUs active. All 16 harvested can be re-enabled:

- **Live Manager** (recommended): [WinnieLV/bc250-cu-live-manager](https://github.com/WinnieLV/bc250-cu-live-manager) — TUI on the fly, no reboot. Works on stock kernel.
- **Kernel patch**: [duggasco/bc250-40cu-unlock](https://github.com/duggasco/bc250-40cu-unlock) — legacy method, rebuilds amdgpu module.
- **Runtime script** (Jul 2026): [big_trov's runtime_40cu Unlock.sh](https://discord.gg/8eZfFWhczz) — patches module in-memory without kernel recompile.

Full guide: [02-BIOS & Firmware](02-bios-and-firmware.md#40-cu-unlock). Benchmarks: [07-Game Benchmarks](07-game-benchmarks.md).

### 8 CPU Core Unlock (Zen 2 — New!)

Board ships with 6 of 8 Zen 2 cores active. As of **Aug 2026**, three working methods exist:

| Method | Type | Risk |
|--------|------|------|
| **RescueMei/BC250-DXE-SMU-Core-Unlock** | Patched BIOS (DXE/SMU) — permanent unlock | If cores don't work, need external flash programmer to recover |
| **Hexxeh/bc250-efi-core-unlock** | EFI shim at boot — semi-permanent, no BIOS modification | Safer option |
| **GabriWar/bc250-core-cu-unlock** | Linux SMU mailbox 0x98 tool — 8 cores + 40 CU, no BIOS flash, systemd unit re-applies after cold boot | Reverts on cold boot (guaranteed escape hatch) |

8-core benchmark in Cyberpunk 2077: **+5-14% FPS** (6 cores → 8 cores: 72→93 fps Low FSR2). The unlock itself costs nothing. After unlocking, apply the **8-core ACPI fix** (CPUs 12-15 need C-states) and the **8-core metrics fix** (`fix-freq = true` governor option, no kernel patch needed) — see [02-bios-and-firmware.md](02-bios-and-firmware.md) and [06-gpu-governor.md](06-gpu-governor.md).

### Stock Performance Baseline

| Config | Game Level | Notes |
|--------|-----------|-------|
| **6 cores, 24 CU stock** | RX 6600–6600 XT level | Solid 1080p gaming baseline |
| **40 CU unlocked** | RX 6700 / GTX 1080 Ti | See [game benchmarks](07-game-benchmarks.md) for details |
| **40 CU + 8 cores** | ~60 FPS Cyberpunk 2077 (dbkretro) | ~10 FPS gain in CPU-heavy areas (Dogtown, qwert9811) |

Full benchmark suite: [07 — Game Benchmarks](07-game-benchmarks.md) (60+ community-tested games).

---

## Join the Community

- **[BC250 Community Discord](https://discord.gg/8eZfFWhczz)** — the hub: setup help, benchmarks, WIP research (member count fluctuates; typically thousands)
- **Reference links & repos** (elektricM Docs, bc250-collective, drivers, tools): see [11 — Community & Resources](11-community-and-resources.md)

---

## What's New

**October 2026 (Oct 9–22, Discord + Reddit):**
- **Windows 11 now works for real:** D-Ogi's **`amdgpu-wddm` ("Nagi")** driver runs the desktop, D3D12 with ray tracing and Vulkan on the BC-250 (Mesa RADV/ACO + DXVK/vkd3d underneath) — "It's operational already" (13/10). Experimental/test-signed, no anticheat yet, 23H2 recommended ([11](11-community-and-resources.md)).
- **VCN enters drivers, with a hard caveat:** the ps5-linux power-on patch is packaged opt-in in `linux-cachyos-rc-bc250` (`bc250-vcn-fw`), but the PSP still refuses the firmware and **only ~40% of chips physically have a functional VCN block** (holde); H.265's failure cause is now known (per-codec register init) ([02](02-bios-and-firmware.md#vcn-hardware-video-decode)).
- **Upscaler default shifted:** **HelixSR Scaler** (OptiScaler + HelixSR) is now the Proton default — runs NVIDIA **DLSS Model E** as D3D12 compute plus experimental **DLSS Frame Generation** on the BC-250; **HelixSR 2.0.0 + Scaler 1.1.0** (19/10) and opt-in **FreeFG** Intel XeSS frame-gen (`PROTON_USE_OPTISCALER=freefg`) ([07](07-game-benchmarks.md)).
- **UGREEN adapter firmware:** `bc250-ch7218-fw` — UGREEN 07.00.69 + patched `tmds` images restore **VRR** (needs `amdgpu.bc250_ch7218_vrr=1` + power-cycle) ([08](08-display-and-audio.md)).
- **Idle power sub-50 W:** a filippor governor branch that also governs memory+fabric reaches 44–49 W at wall (P-state cycling not yet stable) ([06](06-gpu-governor.md)).
- **macOS:** jwagnervaz says a separate release resolves all issues incl. audio (08/10); MLX/Metal is *not* faster than Linux/Vulkan for inference ([11](11-community-and-resources.md), [12](12-ai-inference.md)).
- **Cooling (open question):** board-orientation study — heat-pipe gravity may swing up to ~20 °C on some stock-heatsink boards, zero on others ([04](04-cooling-guide.md)).
- New repos / coverage: `kalpakprod/bc250-vcn-psp-findings`, Digital Foundry + Old Lamer "Nagi vs Linux"; Moraine v0.2.1 (~14.7 GiB usable for inference).
- **Reddit sweep adds:** [BC250DB](https://bc250db.com) community compatibility/benchmark platform (open beta, 13/10); [phiiaz/bc250-ha-bridge](https://github.com/phiiaz/bc250-ha-bridge) — Home Assistant MQTT integration (temps, GPU clock, WoL; drives the governor's D-Bus); PSA — **USB 3.0 rear-I/O noise jams 2.4 GHz dongles**, use USB 2.0 / extension / M.2 Key-E (19/10); independent Reddit orientation confirmation (+10 °C on stock heatsink when rotated to fit an mATX case, 19/10); Epic Games native-Linux launcher preview (14/10, requires Secure Boot+TPM2+IOMMU — not a BC-250 path today); Animaltech **Cub Ice V2 / Project 5 / Cub Twin** cases teased (14/10, 13-case-mods.md).

**October 2026 (Sep 26–Oct 9, 142 channels):**
- **VCN breakthrough:** holde got the actual VCN block doing H.264 (~4 ms encode at 1080p) with a self-signed driver + tweaked BIOS — janky, not reboot-persistent, H.265 still broken, unpublished; VCPU never fetches under stock firmware because the KDB lacks the usage-6 entry and the harvest latch is firmware-written, **not fused** (04/10/2026, [02 → VCN](02-bios-and-firmware.md#vcn-hardware-video-decode))
- **In-SMU GPU governor works** in dev BIOS builds: 500 MHz idle without any software governor, AVFS at SMU SRAM `0x18760`, proposed defaults 350–2000 MHz; planned for the next community BIOS patch menu (rescuemei/punsh1734, 04–07/10/2026, [02](02-bios-and-firmware.md#smu-governor--injectable-dxe-driver-sep-2026))
- **DirectMesh 1.3.1 default-on** in CachyOS Mesa (no `RADV_DIRECTMESH=1`; fixes 4K hang); **HelixSR is now the default upscaler** in the bc250 Proton packages (1.4.1) — "fsr4 got obsoleted with helix" (_mastag/hojnikb, 05–09/10/2026); XeFG/XeMFG frame-gen: CP2077 2× = +48% over no FG, Discord-only, no GitHub (iamastrangeloop)
- **Kernel matrix updated**: 7.2.8/7.2.9 + Mesa 26.2.4 in the bc250 repo; DP audio clock fix merged in 7.2; UGREEN-DP→HDMI audio regression on the patched 7.2 kernel (fixed in 7.3-rc4); SteamOS 3.8.28 → 6.18.50 with OOTB wifi dongles ([05](05-os-installation.md#kernel-support-matrix-canonical--as-of-2026-10-09))
- **Superposition 40 CU record 5865** @ 2350 MHz (nhoj0176, confirmed big_trov 07/10/2026); new benchmarks: Star Wars Galactic Racer (1440p locked 60), Witcher 3 RT Ultra + FSR4 (60+ 1080p), Clair Obscur (68–75), Control Resonant w/ XeMFG x4 (80 fps), Geekbench Vulkan 93k–95k ([07](07-game-benchmarks.md))
- **P5 experimental BIOS caveat:** disables EFI-script changes; ReBAR is only a BIOS option on P5 ([02](02-bios-and-firmware.md#recommended-modded-bios)); "official 5.00 BIOS + runtime unlock" claimed for the upcoming Bazzite suite — unconfirmed
- Troubleshooting added: `radv_enable_unified_heap_on_apu` breaks VRAM reporting (TLOU), Game Mode D3D12 crashes → `-dx11`, encoding-fix perms on Bazzite 44, repaste "dead board" = dislodged CMOS pins, CPU 50→95 °C spike = TIM/pressure failure, VRM no power-limit only thermal (119 °C trip) + overcurrent, 8-pin connector melts past ~250 W ([10](10-troubleshooting.md), [03](03-power-supply-guide.md))
- New tools: RobertoTorino bisect suite (CU/CPU/GPU-OC) + persistent ACPI fix + Governor Manager + Bazzite Suite; e-tho ACPI v1.1.1; Hexxeh VRM/VRAM DKMS modules; punsh1734 metrics-fix for Bazzite; evilpotato partial-core-unlock (7c/14t); loddio Pico DualSense power bridge; macOS Tahoe with Metal 3 via MetalCyan kext ([11](11-community-and-resources.md))
- Inference: Moraine (Alpine distro, +1.5–2 GB VRAM, sub-200 MB idle), 2-node rack & 6-board cluster reports ([12](12-ai-inference.md)); Reddit sweep: price $281 list → ~$47.85 with $200 cashback stack (u/Tama47_, 09/10/2026) ([14](14-reddit.md))
- Staff note (05/10/2026): PS5 compat-layer / RE material discussion paused on the server ([11](11-community-and-resources.md))
- Follow-up sweep found more: hidden **NVRAM VRM current limits (TDC 65 A / EDC 95 A)** + power-limit crash signature (reset dead, wall <30 W) ([02](02-bios-and-firmware.md#vrm--power-limit-constraints-oct-2026)); cross-OS 7-game shootout — CachyOS best 1% lows, gains rank "CUs → GPU clock → cores" ([07](07-game-benchmarks.md)); orbital-sander fin removal ([04](04-cooling-guide.md)); CH341A pins-7/8 unbrick trick ([02](02-bios-and-firmware.md)); PyTorch/ROCm **PPO training** works via `bc250_flush_by_runlist=1` ([12](12-ai-inference.md)); Digital Foundry coverage ([11](11-community-and-resources.md#youtube-coverage)); subtly-broken CU PSA — RT/HelixSR-only freezes ([02](02-bios-and-firmware.md#cu-health-testing)); ESP32 power bridges + Meshroom-D ATX adapter ([11](11-community-and-resources.md), [13](13-case-mods.md))
- Safety: **CPU Vid must never exceed 1.325 V** — bricking risk (yrouel86, 07/10/2026)

**September 2026 (Sep 15–26, 135 channels):**
- CachyOS standard kernel now **7.2.x** (7.2.4/7.2.6); 8-core boards need the MastaG `0001` telemetry patch (stock kernel assumes a 6-core SMU layout); `bc250_hdmi21` enabled by default; 7.3-rc4 in testing (_mastag, 15–20/09/2026)
- **Vulkan-compute encode stopgap** — simpmix/bc250-encoding-decoding-fix v0.4.0–0.4.2: H.264/HEVC via RDNA 2 compute shaders, does **not** enable VCN; falls back to software in Sunshine, modest CPU gain, bundled `bc250-audio-fix` DKMS can break audio (_mastag, mix2.6, 13–25/09/2026)
- VCN: Shalasere/bc250-vcn-research — PSP route "make the vcn power on and start talking" (shalasere, 15–16/09/2026)
- FSR 4 community fork (daniel-h-0/bc250-fsr4-fork) and experimental RADV R2 mesh package (luckiskind/bc250-radv-r2) (16–24/09/2026)
- SteamOS toolkit v1.9.6: 4K120 over DP→HDMI 2.1 cold-boot fix, DSC debugfs override sticks (rpf16rj, 20/09/2026)
- New benchmarks: Control Resonant (1080p FSR Quality; FSR3 fallback ~94 FPS vs mesh ~84) and A Plague Tale: Requiem (~75 FPS FSR4 Quality)
- New case resource: complete-ish ASRock BC-250 CAD model on Printables (jackjt8, 15/09/2026)

**September 2026 (Sep 2–14, 140 channels):**
- GDDR6 per-chip temps via SMU/UMC MR3 (pan_rijovich) — 8 chips + hotspot, P3.00 only; integrated in BC250-Telemetry v0.3 (`--memory-temp`)
- Intermittent no-POST fix 1750→1650 MHz (Dream-Cypher) — CMOS script for aging VRAM, ~5% bandwidth cost
- VRM Telemetry v0.2.0 (FAULT/WARN, CoolerControl/MangoHud, v2 dashboard) and v0.3 (GDDR6 temps); 120 °C Furmark within spec
- DSC investigation — 4K@120Hz 4:4:4 DSC over HBR3 + HDMI 2.1 FRL PCON first time on Cyan Skillfish (_tayne_); PSVR2 DRM lease still blocked
- Heatsink variant C beats B by 8–9 °C (serverror)
- Additional VRAM flex PCB interposer (big_trov 0402) + EMFI injection testing + SMU governor injectable DXE (rescuemei)
- **VCN Sep 2–14:** cold reset `0x0900c004` via SMU toggles but MMIO still `0xffffffff` (rxl8819516); 31-entry `0x5244` gate table drives clamp release (rukkusireland); 2-byte patch `0x9970F4` NOP (thelamer); PSP APCB→ABL→SVC hijack CCP proven, privileged PSP not yet (mergeconflicted); `bc250sim.tar.gz` + kernel patches `vcn_arm_fire/engage` (benpeterson)
- New benchmarks: Where Winds Meet, Blood of Dawnwalker, Bodycam, Dead Space Remastered; RDR2 70–80 FPS, Cyberpunk 90–110 FSR3+FG, Superposition 2350@1000 record
- 3 cases: Minimalist Sep update (slide grills), BeamCase Dupe (MakerBeam XL), Yet Another (SGI/Memphis, Qidi 245³)

**August 2026:**
- VCN research advances — register map + PSP decode (daveconde), CVE-2023-31316 protected-memory write primitive (mergeconflicted), cold-reset register identified (SMN 0x0900c004)
- Optimized FSR 4 RADV build (dmoraza/rescuemei) — ~82–85 FPS vs ~70–75 in Cyberpunk high-FPS test
- FSR4 vs XeSS RT comparison: XeSS Balanced 78 FPS > FSR2/3 75 FPS > FSR4 73 FPS (RT Low)
- CachyOS standard kernel now 7.1.x-based; 7.2 imminent; Linux 7.3 rc1 expected ~30 Aug
- Unified ACPI fix repo (e-tho): C1/C2 idle states + 8 P-state steps, 6c/8c, all BIOS releases
- Native Mesh Shaders V1 works for mesh-only games (lonewolf0622)
- Dolby Digital 5.1 via HDMI/eARC on SteamOS (rpf16rj toolkit v1.3.0)
- Governor v0.4.12 tagged release with `fix-freq`
- CPU core unlock matures — Linux SMU mailbox 0x98 tool (GabriWar) with systemd re-apply, warm/cold boot behavior, core test script (+26.9% 7-zip)
- `fix-freq` governor option fixes 8-core GPU clock reporting (no kernel patch)
- 8-core ACPI fix (mendesrr)
- Async compute queue fix (DryhoppedIPA, +25% FPS Cyberpunk, in Toolkit v1.1.0)
- VRM telemetry via I2C/PMBus + web dashboard (punsh1734, 2-wire mod)
- Forbidden-Darkness V3 DXE BIOS — ACPI patching, SMU Unlock, Core Unlock, manual core selection (RescueMei)
- Unified toolkit orchestrator (chelmooz) — wraps community tools behind one config-driven script
- QuarkStar inference engine — Qwen3.8-27b support, 20+ t/s, 100k context (Ninnix)
- Pump-out warning: repaste without over-tightening to avoid thermal paste ejection (sametklou)
- VCN research consolidated into doc 02 (Research & Active Projects section)

**July 2026:**
- CPU core unlock functional (RescueMei patched BIOS + Hexxeh EFI shim + rw-r-r-0644 Python script)
- Alternate bitmask testing (7-of-8 cores possible)
- OS-independent SMN/PSP mechanism proven
- 8-core benchmark: +5-14% FPS in Cyberpunk
- jwagnervaz independent BIOS rev eng (4700S BIOS testing)

**June 2026:**
- Black Myth: Wukong benchmark (edges RX 6700)
- Binary search artifact hunting
- Live-manager stock WGP disabling
- OCP power limit documented
- VCN confirmed NOT fused off (partial decode)
- Kernel 6.19.x recommended · Mesa 26.x standard

**May 2026:**
- CU Live Manager (toggle 40 CUs without kernel patch)
- Cyberpunk 2077 38 CU record (matches RTX 3060)
- BIOS P4.00 discovered
- AIOs confirmed (Thermalright Aqua Elite 240)
- Micro-Fit power mod
- Dell DA2 220W undervolted success
- Mesa 26 + VRR on CachyOS/Bazzite

---

## How This Guide Is Maintained

Maintained by **katzzero** from BC-250 Discord community data using a semi-automated pipeline: export → RAG indexing → audit → cross-reference → edit → commit. Every claim verified against [elektricM docs](https://elektricm.github.io/amd-bc250-docs/) and Discord exports.

---

*Unofficial — not endorsed by AMD or any community. Prices change often, verify before buying. [Changelog](changelog.md) · [Contribute](CONTRIBUTING.md) · [Discord](https://discord.gg/8eZfFWhczz)*

**Last verified: 2026-10-22**
