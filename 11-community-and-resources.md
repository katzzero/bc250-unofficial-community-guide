# 11 -- Community & Resources

> The BC-250 community is active and growing. Here is where to find help, share builds, and stay updated.

---

## Primary Documentation

| Resource | URL | Notes |
|----------|-----|-------|
| **elektricM Docs** (most comprehensive) | https://elektricM.github.io/amd-bc250-docs/ | 33+ pages, searchable, community-maintained [confirmed: @bishopahre, 04/06/2026] |
| **mothenjoyer69 Docs** (original) | https://github.com/mothenjoyer69/bc250-documentation | Hardware pinouts, specifications |
| **vietsman Docs** (setup scripts) | https://github.com/vietsman/bc250-documentation | Automated setup scripts [confirmed: @vietsman, 14/05/2025] |
| **BC-250.info** | https://www.bc250.info/ | Quick reference site [confirmed: @arthurdept44s4_13234, 18/04/2026] |
| **BC250DB** | https://bc250db.com | Community-driven platform: game compatibility reports, benchmark results, configuration presets; PT-BR + EN; open beta since 13/10/2026 (u/Daivit_Charles, 13/10/2026, reddit) |
| **This guide** | This repository | Restructured from community data |

---

## GitHub Repositories

Grouped by purpose (one entry per repo). Alphabetical within each group.

### Core Documentation & References

| Repository | Description |
|------------|-------------|
| [bangstk/amd-bc250-docs](https://github.com/bangstk/amd-bc250-docs) | Community-driven documentation fork for AMD BC-250 (Cyan Skillfish) |
| [elektricM/amd-bc250-docs](https://github.com/elektricM/amd-bc250-docs) | Main documentation (commit/star counts not re-verified — community report) |
| [vietsman/bc250-documentation](https://github.com/vietsman/bc250-documentation) | Setup scripts (Bazzite/Fedora/Ubuntu) [confirmed: @vietsman, 22/05/2025] |

### BIOS, Firmware & Flashing

| Repository | Description |
|------------|-------------|
| [kenavru/BC-250](https://github.com/kenavru/BC-250) | EFI flash tool (no hardware programmer needed) [confirmed: @kitsunechan7118, 21/07/2025] |
| [RescueMei/BC250-DXE-SMU-Core-Unlock](https://github.com/RescueMei/BC250-DXE-SMU-Core-Unlock) | Patched BIOS (DXE/SMU) that unlocks all 8 CPU cores — permanent, needs external programmer for recovery (Jul 2026) |
| [RescueMei/BC250-DXEv2-BIOSMOD](https://github.com/RescueMei/BC250-DXEv2-BIOSMOD) | MeiMeiDXE V2.1 BIOS mod — 8-core unlock toggle + ACPI options in BIOS menu, themed boot images, auto cold boot via RTC (compatible boards with standby power) (Aug 2026) |
| [Forbidden-Darkness/AMD-BC-250-UEFI-v2.2-Firmware-Menu-Script](https://github.com/Forbidden-Darkness/AMD-BC-250-UEFI-v2.2-Firmware-Menu-Script) | Interactive UEFI flashing script — automated BIOS backup + modded P3.00 (incl. 8-core unlock BIOS) flash with themed menus. **Release v0.5.0** (Aug 2026) — prerequisite: "Deploy only on AMD BC-250 platforms verified 100% stable with all 8 CPU silicon cores active under legacy validation methods"; v0.5.0 release reused Oct 2026 as the "flash and enable in bios" path bundling core unlock + SMU patch (hojnikb, 27/09/2026) |
| [RescueMei/BC250-DXEv3-BIOSMOD](https://github.com/RescueMei/BC250-DXEv3-BIOSMOD) | MeiMeiDXE V3 BIOS mod — DXE drivers for ACPI patching, SMU unlock, core unlock and **manual core selection**; restores PXE/network boot lost on older 8-CU images (jakdaw., 28/09/2026) |
| [onlinermm/bc250-efi-cu-and-memory-temperature](https://github.com/onlinermm/bc250-efi-cu-and-memory-temperature) | EFI patch set: CU unlock + memory-temperature reading via EFI (based on DP4a/Astra research); early — "Stable results haven't been achieved yet" (punsh1734, 02–04/10/2026) |
| [onlinermm/bc250-metrics-fix-bazzite](https://github.com/onlinermm/bc250-metrics-fix-bazzite) | BC-250 Bazzite Metrics Fix 1.0 — kernel module alongside stock `amdgpu` correcting 8-core-BIOS telemetry (4150 MHz clock / 5.9 V / L3-as-GPU-temp reads) on Bazzite without a custom kernel or image (punsh1734, 29/09/2026) |
| [evilpotato/bc250-partial-core-unlock](https://github.com/evilpotato/bc250-partial-core-unlock) | Enable fused-off cores while parking one defective core — persistent 7c/14t on Bazzite + C-state/P-state fix, no reboot needed; AI-generated method, published by user (.mightymike., 28–29/09/2026) |
| [TuxThePenguin0/bc250-bios](https://gitlab.com/TuxThePenguin0/bc250-bios) | Modded BIOS files [confirmed: @dznuts, 13/01/2026] |
| [Dream-Cypher/bc250-memory-timing-boot-fix](https://github.com/Dream-Cypher/bc250-memory-timing-boot-fix) | Boot-time memory timing fix — lowers GDDR6 1750→1650 MHz via CMOS to fix intermittent no-POST on aging VRAM; ~5% bandwidth cost, survives BIOS flash but not CMOS clear (Sep 2026) [confirmed: @brain_cylinder, 13/09/2026] |
| [tmghd272/bc250-custom-bios-logo](https://github.com/tmghd272/bc250-custom-bios-logo) | BC250 BIOS boot logo theme — AMI OEM "ChangeLogo.exe" for DIY mods |
| [tmghd272/bc250-custom-overlays](https://github.com/tmghd272/bc250-custom-overlays) | Custom overlays/logos (Turzx, MangoHud presets, BIOS) |

### CPU & GPU Unlocks

| Repository | Description |
|------------|-------------|
| [bc250-collective/SomnacinDumper-CPUCoreMod](https://github.com/bc250-collective/SomnacinDumper-CPUCoreMod) | CPU core unlock mod tool (WIP, unconfirmed — requires Pi Pico 2 hardware) |
| [duggasco/bc250-40cu-unlock](https://github.com/duggasco/bc250-40cu-unlock) | 40 CU unlock kernel patch (legacy) |
| [F5GO/bc250-cu-live-manager-SteamOS](https://github.com/F5GO/bc250-cu-live-manager-SteamOS) | CU live manager variant for real SteamOS |
| [GabriWar/bc250-core-cu-unlock](https://github.com/GabriWar/bc250-core-cu-unlock) | Linux SMU mailbox 0x98 unlock — 8 CPU cores + 40 CU, systemd unit, core test script, bundled 8-core BIOS + ACPI fix (Aug 2026) |
| [GreatApo/bc250-40cu-unlock](https://github.com/GreatApo/bc250-40cu-unlock) | 40 CU unlock fork with corrected CU masking docs |
| [Hexxeh/bc250-efi-core-unlock](https://github.com/Hexxeh/bc250-efi-core-unlock) | EFI boot shim that unlocks extra CPU cores without BIOS modification (semi-permanent, Jul 2026) |
| [leafyjerk/BC-250-CPU-Core-Map](https://github.com/leafyjerk/BC-250-CPU-Core-Map) | Read-only CPU core layout diagnostic (does not unlock anything) |
| [movacx/bc250-control-center](https://github.com/movacx/bc250-control-center) | Linux control center for BC-250 — monitoring, GPU SMU control, CPU OC, fan PWM, 40 CU tools + one-click 8-core unlock (Aug 2026). Community favourite by late Oct: "movacx Control Center is fantastic… it's made the entire BC250 setup a breeze" (zenith251, 25/10/2026) — note that its unlock does **not** survive a cold power cycle (BIOS flash is the only permanent route). **v1.21.x (08–09/10/2026):** self-updating app, async compute on CachyOS 7.2, per-game FSR4 via OptiScaler, VRAM size from Game Mode, GDDR6 temps (P3.00 BIOS only); v1.21.1 "ASPI fix" support for Bazzite (no longer Arch-only), "Upscaling" section for FSR/HelixSR configs, Steam memory swap/TTM — author flags it "still in the testing phase" (_movacx, 08–09/10/2026) ⚠️ its governor edits can conflict with a hand-edited config.toml — duplicate-key TOML crash reported (brian_aniki, 27/09/2026) |
| [ProjectSomnacin/somnacin-hardware](https://github.com/ProjectSomnacin/somnacin-hardware) | Somnacin project hardware |
| [RobertoTorino/bc250-cu-bisect](https://github.com/RobertoTorino/bc250-cu-bisect) | Runtime GPU CU bisect — does its own unlock via register writes and "Tells **bad CUs** apart from an **unstable CU unlock**"; persistent unlock survives reboot without a modded BIOS (game_play267_84989, 03/10/2026) |
| [RobertoTorino/bc250-cores-bisect](https://github.com/RobertoTorino/bc250-cores-bisect) | "Finding and unlocking healthy cores on a BC-250 board" — CPU-core version of the bisect strategy; beta (game_play267_84989, 04/10/2026) |
| [RobertoTorino/bc250-gpu-oc-bisect](https://github.com/RobertoTorino/bc250-gpu-oc-bisect) | Safe GPU overclock bisect — finds the stable clock ceiling per board (game_play267_84989, 07/10/2026) |
| [rw-r-r-0644/bc250-core-unlock](https://github.com/rw-r-r-0644/bc250-core-unlock) | Original CPU core unlock Python script — SMU mailbox, userspace, no BIOS flash (Jul 2026) |
| [WinnieLV/bc250-cu-live-manager](https://github.com/WinnieLV/bc250-cu-live-manager) | 40 CU live manager — no kernel patch needed. Interactive TUI (UMR-based) |

### SMU, ACPI & Firmware Research

| Repository | Description |
|------------|-------------|
| [bc250-collective](https://github.com/bc250-collective) | Community org: ACPI fix, SMU OC tool, governor, and more |
| [bc250-collective/amd_smu_reverse_engineering](https://github.com/bc250-collective/amd_smu_reverse_engineering) | SMU firmware reverse engineering for BC-250 / PS5 — Ghidra scripts, message tables, BIOS extraction tools [ded811, big_trov, keroppl_wizard, Jul 2026] |
| [bc250-collective/bc250-acpi-fix](https://github.com/bc250-collective/bc250-acpi-fix) | SSDT tables for CPU C-States (P-States experimental per repo README) |
| [bc250-collective/bc250_smu_oc](https://github.com/bc250-collective/bc250_smu_oc) | CPU SMU overclocking tool (4 GHz+) |
| [daveconde/bc250-vcn-enable](https://github.com/daveconde/bc250-vcn-enable) | VCN register map + PSP t28 firmware decode — identified SMN 0x0900c004 as the cold-reset register for UVD; fw_type 13/58 mapping; clamp-release candidate (Aug 2026) |
| [e-tho/bc250-acpi-fix](https://github.com/e-tho/bc250-acpi-fix) | Unified ACPI fix — C1/C2 idle states, 8 P-state steps 800 MHz–3.2 GHz, stubs undefined methods, replaces broken idle table; works 6c and 8c on every BIOS (Aug 2026). **v1.1.1** fixes C3 idle-state freezes; perf impact within noise — Superposition 1080p high 10312 vs 10182 stock (e_tho/big_trov, 05/10/2026) |
| [RobertoTorino/bc250-persistent-acpi](https://github.com/RobertoTorino/bc250-persistent-acpi) | **Persistent** ACPI fix without modded BIOS — C-states + frequency scaling (800 MHz–3.2 GHz, 8 steps) on Linux; only tested on Bazzite; builds on e-tho/bc250-collective/rw-r-r-0644/mendesrr work (game_play267_84989, 06/10/2026) |
| [higorprado/bc250-8core-telemetry-report](https://github.com/higorprado/bc250-8core-telemetry-report) | 8-core SMU metrics layout — maps the per-core arrays that displace GPU clock reporting (Aug 2026) |
| [mendesrr/bc250-acpi-fix-updated-8c](https://github.com/mendesrr/bc250-acpi-fix-updated-8c) | 8-core ACPI tables (SSDT C-states extended to 16 threads) — required after CPU core unlock (Aug 2026) |
| [rw-r-r-0644/bc250-smu-unlock](https://github.com/rw-r-r-0644/bc250-smu-unlock) | Fully arbitrary read/write and code execution on the BC-250 SMU — RPC-style patches from Python (Aug 2026); foundation of current VCN power-on research |
| [Shalasere/bc250-vcn-research](https://github.com/Shalasere/bc250-vcn-research) | VCN research run log/notebook — PSP route toward powering VCN on (Sep 2026) |
| [m2jgh8tg7r-bot/bc250-vcn-linux-research](https://github.com/m2jgh8tg7r-bot/bc250-vcn-linux-research) | "Reverse-engineering and Linux enablement research for AMD BC-250 / Cyan Skillfish VCN 2.0.3" — PSP/TOS service analysis (gennai0211, 26/09/2026) |
| [hciengr/bc250-vcn-community (site)](https://hciengr.github.io/bc250-vcn-community/) | Community VCN research lab / coordination hub — "promising leads, scattered evidence, and unanswered questions" (shalsere, 02/10/2026) |
| [thelamer/bc250-lab-image](https://github.com/thelamer/bc250-lab-image) | Dedicated experiment image — v0.3.0 ships the SMU unlock plus rw_r_r_0644's power-on method as helpers for VCN research (Aug 2026) |

### Governor, Monitoring & Control

| Repository | Description |
|------------|-------------|
| [phiiaz/bc250-ha-bridge](https://github.com/phiiaz/bc250-ha-bridge) | Home Assistant ↔ BC-250 bridge over MQTT (Python 3 stdlib, MIT). Sensors: CPU/GPU/NVMe temps, GPU clock + load, pump RPM, uptime, current Steam game, active CU count, governor threshold; Controls: Sleep/Reboot/Shutdown, Restart Steam, Game/Desktop mode switch, GPU min/max clock range. Uses the `cyan-skillfish-governor-smu` **runtime D-Bus interface** (no persistence — reboot restores defaults; voltage + CU count intentionally read-only for safety; commands from a fixed whitelist, MQTT payloads never reach a shell). Default clock ceiling 2200 MHz (raise with `BRIDGE_CLOCK_CEIL`). Wake-on-LAN tested (r8169). Bazzite-tested; ships a ready-made HA dashboard + HACS custom card (u/Affectionate_Bid5696, 15/10/2026, reddit) [confirmed: @Affectionate_Bid5696, 15/10/2026] |
| [bc250-collective/cyan-skillfish-governor](https://github.com/bc250-collective/cyan-skillfish-governor) | GPU governor (community fork, v0.4.0+ adds CPU-based memory clock control) |
| [fanoush/bc250_memcfg](https://github.com/fanoush/bc250_memcfg) | Memory configuration tool — set VRAM size and timings from Linux (works with stock P3.00/P5.00) |
| [filippor/cyan-skillfish-governor](https://github.com/filippor/cyan-skillfish-governor) | GPU governor (original repo, SMU + TT branches; `fix-freq = true` option for 8-core GPU clock reporting, commit `be9537f` Aug 2026) |
| [Fred78290/nct6687d](https://github.com/Fred78290/nct6687d) | lm-sensors monitoring driver + PWM fan control [confirmed: elektricM docs] |
| [Hexxeh/bc250-vrm-dkms](https://github.com/Hexxeh/bc250-vrm-dkms) | VRM hwmon kernel module (DKMS, auto-updates) — exposes rail temps/power to `sensors` (hexxeh, 28/09–01/10/2026) |
| [Hexxeh/bc250-memory-dkms](https://github.com/Hexxeh/bc250-memory-dkms) | GDDR6 temperature hwmon module — VRAM hotspot/average/chip 0-7 in `sensors`; requires SMU-unlocked BIOS (hexxeh, 28/09–01/10/2026) [confirmed: @hexxeh, 01/10/2026] |
| [jurkovic-nikola/OpenLinkHub](https://github.com/jurkovic-nikola/OpenLinkHub) | Open source fan/RGB controller hub |
| [katzzero/250mon](https://github.com/katzzero/250mon) | Lightweight hardware monitor for BC-250 — temperature, frequency, power stats |
| [Magnap/cyan-skillfish-governor](https://github.com/Magnap/cyan-skillfish-governor) | SMU governor Debian/Ubuntu package — upstream for Debian builds |
| [mix3d/bc250-perf-profile-switcher](https://github.com/mix3d/bc250-perf-profile-switcher) | Decky Loader plugin — GPU clock slider + telemetry overlay in Quick Access Menu |
| [onlinermm/BC250-Telemetry](https://github.com/onlinermm/BC250-Telemetry) | VRM telemetry daemon + web dashboard — PMBus over I2C (per-rail voltage/current/power/temp), 2-wire hardware mod (Aug 2026); v0.2.0 adds FAULT/WARN + CoolerControl/MangoHud + v2 dashboard, v0.3 adds per-chip GDDR6 temps (Sep 2026) [confirmed: @punsh1734, 13/09/2026] |
| [pan-Rijovich/bc250-memory-temperature](https://github.com/pan-Rijovich/bc250-memory-temperature) | GDDR6 per-chip temperature via SMU/UMC MR3 — 8 chips + hotspot/average, P3.00 BIOS only, DQ-bus read (Sep 2026) [confirmed: @pan_rijovich, 12/09/2026] |
| [RobertoTorino/bc250-governor-manager](https://github.com/RobertoTorino/bc250-governor-manager) | "PyQt6 front-end for cyan-skillfish-governor-smu … running Bazzite" (game_play267_84989, 06/10/2026) |
| [RobertoTorino/bc250-bazzite-suite](https://github.com/RobertoTorino/bc250-bazzite-suite) | "Collection of apps for Bazzite running on a BC-250 board" — will fold in governor manager, test app, CU bisect and HelixSR GUI; announced 09/10/2026, not released yet |
| [RobertoTorino/bc250-bazzite-helixsr-gui](https://github.com/RobertoTorino/bc250-bazzite-helixsr-gui) | GUI frontend automating HelixSR + OptiScaler setup on Bazzite (07/10/2026) |
| [Umio-Yasuno/amdgpu_top](https://github.com/Umio-Yasuno/amdgpu_top) | AMD GPU top — live GPU monitoring tool |
| [ZEROAESQUERDA/PS5GPU-BC250](https://github.com/ZEROAESQUERDA/PS5GPU-BC250) | GUI GPU controller [confirmed: @tom97br, 07/03/2026] |

### OS Toolkits & Install Automation

| Repository | Description |
|------------|-------------|
| [borwtf/bc250-tuner](https://github.com/borwtf/bc250-tuner) | Setup helper — CPU/GPU core unlock, governor install, undervolt (u/boR-, 29/10/2026, reddit; unverified by the maintainers) |
| [cachenetics/bc250-nixos](https://github.com/cachenetics/bc250-nixos) | NixOS configuration for BC-250 |
| [cachenetics/project-ariel](https://github.com/cachenetics/project-ariel) | Project Ariel |
| [chelmooz/AMD-BC-250-at-his-Best](https://github.com/chelmooz/AMD-BC-250-at-his-Best) | Unified orchestrator — wraps community tools (core-unlock, cu-live-manager, 40cu-unlock, smu_oc, Forbidden-Darkness UEFI) behind one config-driven install.sh; 1300mV ceiling, dry-run mode; works on Bazzite/Fedora/Arch/CachyOS (Aug 2026) |
| [eabarriosTGC/BC250--ARCH](https://github.com/eabarriosTGC/BC250--ARCH) | Arch Linux automated setup script |
| [gennro/bc250-toolkit](https://github.com/gennro/bc250-toolkit) | CachyOS 40CU unlock + governor automation toolkit |
| [keyboardspecialist/bc250-steamos](https://github.com/keyboardspecialist/bc250-steamos) | SteamOS setup for BC-250 |
| [NeOdYmS/bazzite-bc250-toolkit](https://github.com/NeOdYmS/bazzite-bc250-toolkit) | Bazzite-specific setup toolkit |
| [pnbarbeito/bc250-arch](https://github.com/pnbarbeito/bc250-arch) | Arch Linux setup with governor + 40 CU unlock |
| [redbeard1083/bc250-toolkit](https://github.com/redbeard1083/bc250-toolkit) | CachyOS setup toolkit |
| [TesseractCat/bc250-nixos](https://github.com/TesseractCat/bc250-nixos) | NixOS configuration for BC-250 — reported working 100% first boot combined with Jovian-NixOS on stock BIOS ("now I have another remotely manageable NixOS machine with a fully declarative system config") (stephen.judkins, 04/10/2026) [confirmed: @stephen.judkins, 04/10/2026] |
| [amethyst8118/BC-250-Hackintosh-OpenCore](https://github.com/amethyst8118/BC-250-Hackintosh-OpenCore) | macOS Tahoe 26.7.1 on BC-250 via OpenCore — "Everything mostly works, with CPU, GPU OC and CU+core unlock" (tier3retard, 01/10/2026). Companion GPU patch kext [amethyst8118/MetalCyan](https://github.com/amethyst8118/MetalCyan) gives Metal 3 acceleration (board recognized as RX 5700 by PID rename); **VCN stubbed out on macOS** (tier3retard, 01/10/2026, VCN thread:3301-3305) [confirmed: @tier3retard, 01/10/2026]. **Update 08/10/2026:** jwagnervaz has a separate release coming and "says all issues are resolved. Audio working etc." (djaykay, 08/10/2026) — not yet published/reproduced (open question). MLX/Metal is **not** a faster inference path than Linux/Vulkan here (see [12](12-ai-inference.md)) |
| [rpf16rj/bc250-steamos-real-toolkit](https://github.com/rpf16rj/bc250-steamos-real-toolkit) | Real SteamOS toolkit — 40 CU + 8-core unlock surviving cold boot and SteamOS updates without a BIOS flash. **v1.3.0** adds Dolby Digital 5.1 via HDMI/eARC (option 13, Aug 2026). **v1.9.x (Sep–Oct 2026):** DSC credits + patch replacement + FSR4 SLR Proton variant (v1.9.1), 4K120 cold-boot fix + sticky DSC debugfs override (v1.9.6, 20/09/2026); integrates VA-API h264/hevc encode+decode + pwm fan control + Decky plugin — encode path "tested, not ready for release" (toolkit thread, 29–30/09/2026). Latest release **v1.10.4** (16/10/2026) — repo ships fast; check its release page for the current version rather than pinning |
| [tmghd272/bc250-batocera-tools](https://github.com/tmghd272/bc250-batocera-tools) | Batocera Linux tools for BC-250 |
| [tmghd272/bc250-toolkit-lite](https://github.com/tmghd272/bc250-toolkit-lite) | Lighter toolkit variant |

### Power Delivery & Remote Control

| Repository | Description |
|------------|-------------|
| [1mathp/ESP32C3-ATX-Blynk](https://github.com/1mathp/ESP32C3-ATX-Blynk) | ESP32-C3 remote power-on via Blynk app — works outside local network (Aug 2026) |
| [ded811/BC250-Power-Adapter](https://github.com/ded811/BC250-Power-Adapter) | BC-250 J2000/J2001 Micro-Fit power adapter PCB (UNTESTED — waiting for fab boards, build at own risk) |
| [dexikdex/ESP32-BC250-LOP_PSU-PowerON-Xbox](https://github.com/dexikdex/ESP32-BC250-LOP_PSU-PowerON-Xbox) | ESP32_Relay X2 — Xbox BLE wake, sniper pairing, zombie-wake protection (LOP PSU) |
| [huzhekun/bt-dongle-with-pc-wake](https://github.com/huzhekun/bt-dongle-with-pc-wake) | Pi Pico 2W as BT dongle with controller wake (Linux, early stage) |
| [mosfetparty/bc250-psu-adapter](https://github.com/mosfetparty/bc250-psu-adapter) | ATX PSU control adapter (pilimmm) — plug-and-play PS_ON board for FSP500 + 24-pin ATX, [mosfet.party](https://mosfet.party) |
| [PetteriLah/BC-250-PC-Remote-Control](https://github.com/PetteriLah/BC-250-PC-Remote-Control) | ESP32 remote PSU controller — PS5 DualSense BLE wake, web interface (wisserbasser) |
| [GreatApo/BC250_ESP32_ATX_PSU](https://github.com/GreatApo/BC250_ESP32_ATX_PSU) | ESP32 ATX power-on bridge — "built 3 of these and they have worked 100% every time no matter how long it just sits" (u/jordanka161, 07/10/2026, reddit) |
| [Thunkar/bc250-esp32-switch](https://github.com/Thunkar/bc250-esp32-switch) | ESP32 DualSense wake — originally ESP32-C3; a user ported it to the original ESP32 because "the dual sense is Bluetooth classic only", pairs by MAC address + push-button fallback (u/Stormbringer1225, 07/10/2026, reddit). Wiring pattern from the same thread: case momentary button drives an optocoupler that bridges PS_ON to ground (u/rufiohProbably, 07/10/2026) |
| [suapapa/rusty-bc250-atx](https://github.com/suapapa/rusty-bc250-atx) | ATX PSU power control (Rust) |
| [sungnanda/bc250-power-controller](https://github.com/sungnanda/bc250-power-controller) | BC-250 power controller (sungnanda, 26/10/2026) |
| [Thunkar/bc250-esp32-switch](https://github.com/Thunkar/bc250-esp32-switch) | ESP32-C3 power switch — BLE controller wake, WiFi config portal, boot watchdog (ATX PSU) |

### Display, Audio & Peripherals

| Repository | Description |
|------------|-------------|
| [awalol/DS5Dongle](https://github.com/awalol/DS5Dongle) | Pico2W DualSense bridge — HD haptics, headset audio, wireless BT bridging |
| [bangstk/Vulkan_NullVRS](https://github.com/bangstk/Vulkan_NullVRS) | Vulkan layer that nullifies VRS commands — fixes 640x480 rendering |
| [djanice1980/DS5_Bridge](https://github.com/djanice1980/DS5_Bridge) | DS5 Bridge Linux/CachyOS port — PipeWire audio, audio-driven haptics, uinput chord injection |
| [dyllan500/bazzite-amd-hdmi-kde](https://github.com/dyllan500/bazzite-amd-hdmi-kde) | VRR fixes for Bazzite KDE |
| [Koloses/Solarflare](https://github.com/Koloses/Solarflare) | Moonlight/Sunshine fork with Pyrowave for BC-250 |
| [loddio/bc250-pico-power-bridge](https://github.com/loddio/bc250-pico-power-bridge) | "Press PS on the DualSense and the PSU turns on, then the BC-250 boots / Shut down from Bazzite/SteamOS and the PSU goes back to standby on its own" — Raspberry Pi Pico 2 W console-style power bridge, printed STLs + manual, MIT (loddio, 09/10/2026) [confirmed: @loddio, 09/10/2026] |
| [peterdk31/bc250_ws2812b_controller](https://github.com/peterdk31/bc250_ws2812b_controller) | WS2812B LED controller for BC-250 |
| [Redemp/Interlaced-Linux-amdgpu-Driver](https://github.com/Redemp/Interlaced-Linux-amdgpu-Driver) | Interlaced display support for amdgpu — supports GC 10.1.3 / Cyan Skillfish (Aug 2026) |
| [rpf16rj/steamos-led-wled](https://github.com/rpf16rj/steamos-led-wled) | DIY LED bar replica for BC-250 controlled from SteamOS Game Mode via WLED (Aug 2026) |
| [SamSkjord/ubazzite600](https://github.com/SamSkjord/ubazzite600) | TP-Link UB600 (RTL8761BU) Bluetooth fix for Bazzite / atomic Fedora via out-of-tree btusb rebuild |
| [simpmix/bc250-encoding-decoding-fix](https://github.com/simpmix/bc250-encoding-decoding-fix) | Experimental VA-API driver doing H.264/HEVC encode via Vulkan RDNA 2 compute shaders — **does not enable the VCN block**; stopgap only, modest gain over CPU encode, bundled `bc250-audio-fix` DKMS can conflict with the kernel audio driver (v0.4.0–0.4.2, Sep 2026) [confirmed: @_mastag, 25/09/2026] |
| [tdakhran/wl-ambilight](https://github.com/tdakhran/wl-ambilight) | Wayland Ambilight project |

### Graphics & Performance Fixes

| Repository | Description |
|------------|-------------|
| [daniel-h-0/bc250-fsr4-fork](https://github.com/daniel-h-0/bc250-fsr4-fork) | Community FSR 4 fork, branch `v4`, active through v23 (25/09/2026, fish) — bundled by the XeFG enabler (below) |
| [daniel-h-0/freefg](https://github.com/daniel-h-0/freefg) | FreeFG — Intel XeSS frame generation with BC-250-accelerated shaders. **v1.1.0–1.1.4 (21–27/10/2026):** +1.4–2.6% generated frames, `XeFGModel=default` fix for MFG Unlocker conflicts, big 3×/4× pacing fix in 1.1.3, optional generated-frame scaling back in 1.1.4 (50–100 % or 720p/1080p/1440p presets). Bundled by MastaG's Proton packages as `PROTON_USE_OPTISCALER=freefg` / `freefg-helixsr` [confirmed: @iamastrangeloop, 27/10/2026] |
| [dmorazasanchez/bc250-fsr4](https://github.com/dmorazasanchez/bc250-fsr4) | Experimental FSR 4 optimization for GFX1013 — Mesa/RADV INT8 dot-product fallback via i24 instead of broken native DP4A; FSR 4.1.1 shader dropped 64k→37k instructions, ~306k→104k throughput; "huge performance improvement" in Cyberpunk 2077 (Aug 2026) |
| [DryhoppedIPA/bc250-gfx1013-fix](https://github.com/DryhoppedIPA/bc250-gfx1013-fix) | Async compute queue (ACE) fix for GFX1013 — kernel + Mesa/RADV patches, +25% FPS (Aug 2026) |
| [HHHHanasak1/xess-xmx-linux](https://github.com/HHHHanasak1/xess-xmx-linux) | Patched Mesa ANV drivers + `igdext64.dll` enabling **XeSS/XeMFG with XMX acceleration on Linux** for Intel Arc cards — not BC-250-specific, flagged in the XeFG thread as possibly useful (20261025 release; dmoraza, 25/10/2026) |
| [keyboardspecialist/GoldenEye-Recomp](https://github.com/keyboardspecialist/GoldenEye-Recomp) | GoldenEye (N64) Recompilation port patched for BC-250/SteamOS (keroppl_wizard, 08/10/2026, chat:23654) |
| [lonewolf0622/bc250meshtaskwork](https://github.com/lonewolf0622/bc250meshtaskwork) | **DirectMesh** — "Mesh shaders for the AMD BC-250 (GFX1013) in RADV", branches/tags v1.0–v1.3 (indexed mesh draws 1.5–1.8× faster for meshlets ≥96 verts). **Shipped in CachyOS mesa/mesa-git and ON BY DEFAULT as of DirectMesh 1.3.1 (09/10/2026)** — fixes the 4K GPU hang, GTT index storage, Mesh CTS 1,902/1,902 (_mastag, 09/10/2026) [confirmed: @_mastag, 09/10/2026]. Earlier listed as `lonewolf0622/BC250-Native-Mesh-Shaders-`; enable-by-env (`RADV_DIRECTMESH=1`) since superseded. Alt per-game path: `luckiskind/bc250-radv-r2` below |
| [lonewolf0622/HelixSR](https://github.com/lonewolf0622/HelixSR) | **HelixSR** — "hybrid neural upscaler that combines DLSS neural reconstruction with FSR 3.1's interface"; D3D12-only; default upscaler in the three CachyOS bc250 Proton packages (v1.0.2 → **3.2.0**, Oct 2026); Apache-2.0 (DLSS network weights remain NVIDIA property) (lonewolf0622x/_mastag, 05/10–29/10/2026) [confirmed: @_mastag, 29/10/2026]. **Oct 22–29 wave:** Scaler 2.1.0 + HelixSR 3.1.0 start on **HLX FSR 4** with optional FSR frame-gen (28/10); HelixSR 3.2.0 pre-release (29/10); per-game upscaler menu with FreeFG + HelixSR as default (27/10). HelixSR also runs on non-BC-250 RDNA1/Vega and even GTX cards (lonewolf0622x, 21/10/2026). See [07 → upscaler landscape](07-game-benchmarks.md) for measured results |
| [luckiskind/bc250-radv-r2](https://github.com/luckiskind/bc250-radv-r2) | Experimental BC250/GFX1013 RADV R2 per-game package with patched vkd3d queue workaround; useful only for native mesh/task/hybrid-shader games — ~84 FPS vs ~94 FPS for the FSR3 fallback in a scene test (nonu0038, 24/09/2026) [confirmed: @nonu0038, 24/09/2026]. Integrated as the alt path in the CachyOS/SteamOS toolkits; keroppl_wizard: "more broadly compatible, as well as without gpu hangs" (25/09/2026) |
| [MastaG/linux-cachyos-bc250](https://github.com/MastaG/linux-cachyos-bc250) | CachyOS BC-250 kernel + Mesa repo — kernel-7.1 patches (audio, compute queue fix), updated Mesa, telemetry fixed at source in-kernel (`gpu_metrics`, `gpu_busy_percent`, real `freq1_input`). On this kernel, governor `fix-freq`/`fix-metrics` are redundant bind mounts (Aug 2026). Mesa **26.2.5** + **Linux 7.3** since 22/10/2026, DirectMesh default since 09/10/2026 (see [05 → Kernel Support Matrix](05-os-installation.md#kernel-support-matrix-canonical--as-of-2026-10-29)). DirectMesh 1.3.1 was rebased for `mesa-git` on 22/10/2026 [confirmed: @_mastag, 22/10/2026]. |
| XeFG / XeMFG Enabler (iamastrangeloop) | Intel XeSS frame-gen enabler + BC-250-accelerated shaders for DX12/Proton — **+22% over Intel's shaders, +48% over no FG** in CP2077 (2×), settings pre-verified for 19 games, includes the `daniel-h-0` accelerated FSR4. **Discord-only distribution, no GitHub repo** — "staying off GitHub for this project due to restrictive XeFG modification TOS" (29/09–01/10/2026) [confirmed: @iamastrangeloop, 29/09/2026] |

### Emulation & VR

| Repository | Description |
|------------|-------------|
| [superkeka/KytyPS5-bc250](https://github.com/superkeka/KytyPS5-bc250) | Kyty (PS5) fork with the Vulkan renderer removed — PS5 titles run with **native GPU execution** through amdgpu. Reported: Astro Bot 45–55 FPS on a heavy level, Gran Turismo 7 40–60 FPS (u/Several-System1535 26/10/2026, u/icepatfork 28/10/2026, reddit); "KytyPS5-Native" release announced 29/10/2026. Shader-compile stutter is expected on first runs |
| PSVR2 on BC-250 (DSC wiring patch) | Five-line DSC enablement for DCN 2.0.1 (see [08 → DSC](08-display-and-audio.md#dsc-display-stream-compression--4k120-and-pcvr-sep-2026)) — full SteamVR at 1520×1548/eye, 40–55 FPS in VRChat; patch not yet published as a repo (u/Neat-Significance275, 29/10/2026, reddit) |

### AI Inference

| Repository | Description |
|------------|-------------|
| [akandr/bc250](https://github.com/akandr/bc250) | Ollama + Vulkan inference guide for BC-250 |
| [GabriWar/bc250-rocm-working](https://github.com/GabriWar/bc250-rocm-working) | Stable Diffusion on BC-250 via ROCm/HIP — kernel patches, rocBLAS gfx1013 kernels, runlist TLB flush fix — the `amdgpu.bc250_flush_by_runlist=1` module option later credited with fixing PPO-training GPU faults (u/redfoxkiller, 04/10/2026, reddit), full investigation (Aug 2026) |
| [JustVugg/colibri](https://github.com/JustVugg/colibri) | Run GLM-5.2 (744B MoE) on 25GB-RAM machine — pure C, zero deps, experts streamed from disk |
| [LaurentZuijdwijk/llama.cpp](https://github.com/LaurentZuijdwijk/llama.cpp) | llama.cpp with adaptive speculative decoding (`--spec-draft-adaptive`) + Vulkan backend tuned for AMD Strix Halo — 4.7x on structured output, 1.9x mainline prefill on MoE (Aug 2026) |
| [TechMakesArt/llama.cpp-bc250](https://github.com/TechMakesArt/llama.cpp-bc250) | llama.cpp fork tuned for the BC-250 (Aug 2026) |
| [thelamer/bc250-ollama-openwebui](https://github.com/thelamer/bc250-ollama-openwebui) | Ollama + OpenWebUI setup guide |
| [wdonega/bc250-llm-setup](https://github.com/wdonega/bc250-llm-setup) | Host setup scripts for a 2× BC-250 llama.cpp node (Sep 2026) |
| [4claps/bc250-llama-cluster](https://github.com/4claps/bc250-llama-cluster) | Automated two-node BC-250 Fedora llama.cpp Vulkan/RPC inference cluster with Ansible (goricito.thevulpix, 07/10/2026) |
| [hojnikb/moraine](https://github.com/hojnikb/moraine) | **Moraine** — Alpine-based inference distro for the BC-250: "about 1.5-2GB more vram to play with than regular desktop distros like cachy or bazzite"; v0.2.1 "Up to 137MiB more memory available. Now idles at sub 200MB"; web UI + model profiles (hojnikb, 25/09–03/10/2026) [confirmed: @hojnikb, 03/10/2026]. See [12 → Moraine](12-ai-inference.md) |

### Cases & Physical Mods

| Repository | Description |
|------------|-------------|
| [isaacalvex/BC-250-Custom-Case](https://github.com/isaacalvex/BC-250-Custom-Case) | Alternative 3D-printable enclosure |
| [NexGen-3D-Printing/SteamMachine](https://github.com/NexGen-3D-Printing/SteamMachine) | Steam Machine cases + setup scripts [confirmed: @nexgen3d, 11/12/2025] |
| [onemorecap/bc-250-sleeve-adapter](https://github.com/onemorecap/bc-250-sleeve-adapter) | 120mm fan adapter for stock heatsink |
| [safwyls/BC-250_ATXCase](https://github.com/safwyls/BC-250_ATXCase) | ATX case design for BC-250 |

### Windows Drivers

**[D-Ogi/amdgpu-wddm](https://github.com/D-Ogi/amdgpu-wddm) ("Nagi") is functional, not just a stub** — an open Windows 11 x64 driver where the desktop, **Direct3D 12 with ray tracing, and Vulkan** run on the BC-250 GPU (gfx1013). Underneath it reuses Mesa RADV + the ACO compiler, and DX12 games go through DXVK/vkd3d-proton inside the driver. "It's operational already" as of 13/10/2026; what's still being fixed is third-party hardware compat (DP→HDMI adapters) and broader game coverage. Practical notes: **Windows 11 x64 23H2 or newer with Secure Boot disabled** (the driver repo README is authoritative here; the earlier "use 23H2 only" guidance was based on the tester-29/30 devlog and has since been relaxed); the **Nagi Control App** switches VRAM between 8/8 and 12/4 and ships a small debloater; a fixed 512 MB carve-out is too small (Windows caps dynamic GPU memory at 50% of system RAM). The driver ships frequent **test-signed GitHub Releases** (do not pin the build number — check the repo's release page; latest at audit was `v0.7.216.103-tester.31v3`, 20/10/2026). Quirks reported on recent testers: install-time Code 43 (workaround `bcdedit /set {globalsettings} highestmode on`) and a blank output on 2560×1440 panels pending a fix. **Drivers are test-signed, so anticheat games stay blocked until a signed release** [confirmed: @dogi013495, 13/10/2026]. License **PolyForm Noncommercial 1.0.0** (no commercial use / no bundling into hardware or OS images for sale). **Distributions come from GitHub Releases only** — the README warns about fakes on file hosts and BIOS images (see `SECURITY.md`). Star count at last check: 74. **Why no existing AMD driver works off-the-shelf:** the Cyan Skillfish GPU is "a weird mix of two different RDNA generations" so a stock Windows driver cannot be tweaked into supporting it — this is why the community had to build `amdgpu-wddm` from scratch (u/pja, 20/10/2026, reddit).

Earlier community experiments (all WIP/untested, superseded by Nagi):

| Repository | Description |
|------------|-------------|
| [gottmoz/BC-250-Windows-graphics-driver](https://github.com/gottmoz/BC-250-Windows-graphics-driver) | Windows graphics driver experiment (WIP, untested) |
| [Keshas-dev/AMD-BC-250-Windows-Driver](https://github.com/Keshas-dev/AMD-BC-250-Windows-Driver) | Windows display driver for BC-250 (WIP, untested) |
| [ZEROAESQUERDA/BC250-windowsDriverTest](https://github.com/ZEROAESQUERDA/BC250-windowsDriverTest) | Windows display driver experiment for BC-250 (WIP, untested) |

---

## Discord Community

- **Server:** [BC250 Community Discord](https://discord.gg/8eZfFWhczz)
- **Channels:**
- `#bc250-chat` -- general discussion [confirmed: @Discord]
  - `#benchmarks` -- game performance sharing [confirmed: @odinforrest, 10/04/2026] |
  - `#help-thread` -- troubleshooting [confirmed: @mothenjoyer69, 27/01/2025] |
- `#bc250-flex-chat` -- build showcases [confirmed: @codyrainy, 30/05/2026]
- `#bc250-resources` -- shared resources [confirmed: @deathstalkerjr, 19/11/2025]
- **Members:** 3,500+ | **Messages:** 9,716 technical messages (elektricM docs)

Note: mkdocs.yml contains a different invite code (`discord.com/invite/uDvkhNpxRQ`) -- the README link is used here as the primary source.

**Server notes (Oct 2026):** staff moderation — "I'd like everyone to refrain from discussing the ps5 compatibility layers and to refrain from posting any ps5 reverse engineering material here" (realderyn, 05/10/2026, announcements); plus a general "don't break the law here" reminder (realderyn, 04/10/2026). Expect PS5-adjacent VCN material to be scarce on the server; a benchmark thread was renamed "[removed by staff]" after an NSFW post got its author banned (biohazardv2.0 note, 08/10/2026). Community culture: a "Heroes of BC250" thread was opened where capt.cat_13 tagged the long list of tool authors (filippor, Humvee55, _mastag, Forbidden-Darkness, rescuemei/The Mei™, rw-r-r-0644, mrfrakes, movacx, dmoraza, fish, gennro, punsh, lonewolf0622x…) and proposed coordinated **testing contributions for Control Center** — "Control Center is not appearing out of nowhere. Most of its functionality is based on work that already exists" (01/10/2026, project-forums/Heroes of BC250:10-32).

---

## Useful Hashtags for Searching

When searching for help, try these identifiers:
- `#bc250` or `#amd-bc250`
- `#cyan-skillfish`
- `#bazzite`
- `#BC250Community`

---

## Timeline -- Key Milestones

| Date | Event |
|------|-------|
| Oct 2024 | First BC-250 boards appear on eBay/AliExpress (~$50-80) [confirmed: @david_manigo, 16/11/2025] |
| Dec 2024 | BC-250 Community Discord launches [confirmed: @Discord] |
| Feb 2025 | KDE RDSEED fix lands in kernel -- KDE becomes usable [confirmed: @astrocast, 08/01/2026] |
| May 2025 | **Mesa 25.1 released** -- official Cyan Skillfish GPU support (HUGE milestone) |
| May 2025 | vietsman's one-click Bazzite installer published [confirmed: @hahahahahhaha3733, 12/04/2026] |
| Jul 2025 | Patched Bazzite fork with GPU OC (2230 MHz) by filippor [confirmed: @filippor, 29/07/2025] |
| Aug 2025 | COPR repository launches -- one-command governor install [confirmed: @mothenjoyer69, 13/11/2025] |
| Sep 2025 | GPU frequency patch lands in official Bazzite [confirmed: @filippor, 28/08/2025] |
| Nov 2025 | elektricM documentation site launches (33+ pages) [confirmed: @dantistnfs, 12/05/2026] |
| Dec 2025 | CPU SMU overclocking tool released (4 GHz achieved!) [confirmed: @big_trov, 29/01/2026] |
| Jan 2026 | cyan-skillfish-governor-smu v0.4.0 released (SMU-based, no kernel patch) [confirmed: @Discord] |
| Mar 2026 | All docs updated to latest state |
| May 2026 | VRR working on Bazzite Deck via custom kernel patch image (fforduck) [confirmed: @fforduck, 14/04/2026] |
| May 2026 | VCN partial decode achieved via SMU poking (holde, Angablade) - active research |
| Jul-Aug 2026 | 8-core CPU unlock (SMU mailbox exploit), 40 CU unlock, BIOS mods, gfx1013-fix — major performance unlocks |
| Aug 2026 | BIOS mod becomes the dominant 8-core method; ACPI fix extended to 16 threads; `fix-freq` governor option for 8-core GPU clock reporting |
| Aug 2026 | VCN 2.0.3 confirmed present and NOT fused off; power-path root cause identified (no `dpm_set_vcn_enable`); "VCN: The final boss" research thread opened (thelamer, Aug 14 2026) |
| Aug 2026 | rw_r_r_0644 achieves arbitrary code execution on the SMU at runtime (Cyan Skillfish only) — possible VCN power-up path (Aug 15 2026) |
| Aug 2026 | dmorazasanchez/bc250-fsr4 published — FSR 4 running on GFX1013 with i24 fallback (Aug 14 2026) |
| Sep 2026 | CachyOS bc250 kernel line moves to 7.2.x with Mesa 26.2.x; DP audio clock fix merged for 7.2 (Aug–Sep 2026) |
| Sep 26 2026 | **r/BC250Gaming** archive starts being tracked for this guide (doc [14](14-reddit.md)) |
| Oct 2026 | Superposition 40 CU record **5865** @ 2350 MHz confirmed by big_trov (nhoj0176, 07/10/2026) |
| Oct 2026 | In-SMU GPU governor functional in development BIOS builds (rescuemei, 04/10/2026) |
| Oct 4 2026 | VCN H.264 demonstrated running on the actual VCN block via a self-signed driver + tweaked BIOS (holde; unpublished, janky — see [02](02-bios-and-firmware.md#vcn-hardware-video-decode)) |
| Oct 5 2026 | Staff asks the server to refrain from PS5 compatibility-layer / PS5 reverse-engineering material (realderyn, 05/10/2026, announcements) |
| Oct 9 2026 | **DirectMesh 1.3.1 on by default** in CachyOS Mesa when a BC-250 is detected; **HelixSR** is the default upscaler in the bc250 Proton packages (_mastag, 09/10/2026) |

---

## Price History (BC-250 Board)

| Period | Price Range | Trend |
|--------|-------------|-------|
| Late 2024 | $50-80 | Low (mining surplus) [confirmed: @david_manigo, 16/11/2025] |
| Mid 2025 | $80-100 | Rising [confirmed: @Discord] |
| Oct 2025 | $100-130 | YouTube coverage increased demand [confirmed: @dapping, 20/03/2026] |
| Early 2026 | $150-200+ | Current -- still climbing [confirmed: @dartzon, 10/06/2026] |
| May 2026 | ~$130-140 | Some deals at $130-140, trending up [confirmed: @Discord] |
| Aug 2026 | $150-200 (AliExpress) | Active listings: $166.54 US / AUD$211 AU (~$150); users report seeing $188–196 with occasional $166 flash listings [confirmed: @chu, @j0shm1lls, @alexxxor_, @dderps, 14-17/08/2026]
| Oct 2026 | ~$281 list (US AliExpress main listing), stackable to ~$241 with code, "under $50" best-case with $200 Rakuten cashback (u/Tama47_, 09/10/2026, reddit); community trades: EU WTB max €175 (ziporah, 08/10/2026, shilling-adverts), UK flashed 38/40-CU board sold privately (maxshanly → troutsky, 07/10/2026, price not stated), 7× lot US-MN sold out (27/09/2026) | Coupon/cashback stacking keeps effective prices well below list; private sales cluster €125–175 |
| Mid Oct 2026 | ~$250→$400+ (AliExpress/US + eBay) | Spike after LTT/YouTube coverage briefly pulled the main listing off AliExpress (10/12, back up within ~24 h); Canada users reporting $400+ per board after buying at $250 (u/redfoxkiller, 12/10/2026, reddit); EU eBay listings 400–450 € (u/fabulot, 20/10/2026, reddit); community thread title: "$500 price tag coming soon" (u/Sudowoodo-Official, 20/10/2026, reddit) |
| Late Oct 2026 | ~$150–240 tested / $70–200 outliers | Market partially cooled: eBay **$200–240** for tested boards, one seller with >10 units at **$207** US, a $150 no-BIOS unit, $148 paid by a buyer, $70 "joined the club" find; AliExpress ~$207–209 before coupons. Sellers re-using photos and hiking after sales reported. PS5 comparison (~$220 used locally) is now the standard objection (xerxes3rd/magiksmoke/brammmmmmmmm/zerosumpr/d0rkch0c0late, 22–27/10/2026, chat + reddit) [confirmed: @zerosumpr, 27/10/2026] |

> Prices continue to rise as supply dwindles and demand grows from the gaming community. Expect $150-200+ in active listings. [confirmed: @iambryan_x1, 24/01/2026] — as of Oct 2026 main-listing sticker reached $281 (before discounts; u/Tama47_, 09/10/2026, reddit). **Late Oct 2026 update:** sticker ~$400+ in some regions with the main AliExpress listing briefly disappearing (10/12), driven by YouTube-creator amplification and finite used-stock; several threads now openly discuss a sub-$500 target (u/Sudowoodo-Official, u/redfoxkiller, u/fabulot, 12–20/10/2026, reddit)

---

## YouTube Coverage

| Creator | Period | Notes |
|---------|--------|-------|
| Budget Builds Official | Oct 2025 | First major coverage -- prices started climbing [confirmed: @cliff_86, 29/11/2025] |
| **Digital Foundry — Direct Weekly #284** | 05/10/2026 | Covered the BC-250 and its FSR 4 capability — second mainstream-press attention wave; longevity/price discussion followed (u/BdogMcCool1, 05/10/2026, reddit) |
| Old Lamer — HelixSR vs FSR4-r11 comparison | 06/10/2026 | Fresh head-to-head video after HelixSR landed; community verdict: "might replace all of my games with DLSS 3.7 instead" (u/Sudowoodo-Official, 06/10/2026, reddit) |
| Old Lamer — Windows 11 Gaming on BC-250?! Nagi Driver vs Linux | 19/10/2026 | Independent install/compat/performance test of the amdgpu-wddm (Nagi) Windows driver vs Linux — "promising progress, but there's still a long way to go" (shared by capt.cat_13, 19/10/2026) |
| oldlamer | Late 2025 | Most technically accurate guides [confirmed: @Discord] |
| CraftComputing | Late 2025 | Early coverage, some buggy results [confirmed: @Discord] |
| ToastyBros | Dec 2025 | Criticized for not using governor/OC [confirmed: @selectivelygood_16010, 03/01/2026]
| TechDweeb | Jan 2026 | ChimeraOS coverage [confirmed: @Discord] |
| NexGen3D | Feb 2026 | Case design channel [confirmed: @nexgen3d, 11/12/2025] |
---

## Contributing

Found a solution to a problem? Help others by adding it to the documentation.

**Easy way:** Click "Edit on GitHub" on any page of the [elektricM docs](https://github.com/elektricM/amd-bc250-docs) and submit a pull request.

**What is needed:**
- Tested hardware configurations
- Game compatibility reports
- Troubleshooting solutions
- Distribution-specific setup steps
- Fixes for outdated information

---

## Complete Index of Revised Files

| # | File | Description |
|---|------|-------------|
| 01 | [Hardware Specifications](01-hardware-specs.md) | Board specs, APU details, connectors |
| 02 | [BIOS & Firmware](02-bios-and-firmware.md) | Flashing guides, VRAM config, component map |
| 03 | [Power Supply Guide](03-power-supply-guide.md) | All PSU options with verified specs & prices |
| 04 | [Cooling Guide](04-cooling-guide.md) | Heatsink mods, fans, thermal interface, temps |
| 05 | [OS Installation](05-os-installation.md) | Step-by-step for every supported distro |
| 06 | [GPU Governor](06-gpu-governor.md) | Governor options, OC, tuning, benchmarks |
| 07 | [Game Benchmarks](07-game-benchmarks.md) | Community-tested FPS data for 60+ games |
| 08 | [Display & Audio](08-display-and-audio.md) | DP/HDMI, audio solutions, cable guide |
| 09 | [WiFi & Peripherals](09-wifi-and-peripherals.md) | Adapters, storage, accessories |
| 10 | [Troubleshooting](10-troubleshooting.md) | Error fixes, debugging commands |
| 11 | [Community & Resources](11-community-and-resources.md) | Links, Discord, timeline, credits |
| 12 | [AI Inference & LLMs](12-ai-inference.md) | llama.cpp, Ollama, Stable Diffusion, ROCm status |
| 13 | [Case Mods & Custom Enclosures](13-case-mods.md) | Community case designs, commercial sources, 3D-printable files |
| 14 | [Reddit Community (r/BC250Gaming)](14-reddit.md) | Subreddit roundup: builds, findings, prices |

---

*This revised documentation was compiled from the original resume files, 9,716 Discord messages (elektricM docs), the elektricM/amd-bc250-docs repository (commit/star counts not re-verified — community report), and verified against current internet sources (March 2026). All errors from the original documents have been corrected.*

**Last verified: 2026-10-29**
