# 08 — Display & Audio

> The BC-250 has **one DisplayPort 1.4 output** and **no HDMI**. Audio must be routed through DP or a USB adapter.

---

## Display Connection Options

| Method | Quality | Audio | Recommended? |
|--------|---------|-------|--------------|
| **Native DisplayPort** | Best (up to 4K@120Hz, HDR10) | ✅ Works (most users) | ✅ Best option if monitor supports DP |
| **Passive DP-to-HDMI** | Good (1080p60 / 1440p60) | ✅ Usually works | ✅ Good value (~$5–10) |
| **Active DP-to-HDMI** | Up to 4K@60Hz+ | Broken on BC-250 (direct connection). Works on MST hub outputs (pops1cl/Discord). | Not recommended for direct use; usable with MST hubs |
| **DP-to-USB-C** | Good | ✅ Works | ✅ Good for USB-C monitors | [confirmed: @locoman009, 11/04/2026]

### Recommended Cable/Adapter

| Product | Type | Notes |
|---------|------|-------|
| Passive DP-to-HDMI (generic) | Passive adapter | Best value — works at 1080p60/1440p60 with audio, ~$5–10 |
| AmazonBasics DP to HDMI (`B015OW3M1W`) | Passive | Video works, audio hit-or-miss |
| UANTIN DP to HDMI (`B0CYHB956B`) | Passive | Confirmed working, Amazon UK | [confirmed: @biohazardv2.0, 13/02/2026]
| UGREEN DP to HDMI (`B0FCLXJHTX`) | Passive | Recommended by community — 4K@30Hz / 2K@60Hz / 1080P@120Hz; confirmed working with BC-250 (Aug 2026) |

### BIOS Display Issue — "No Display in BIOS"

If you can't see the BIOS screen but the OS boots fine:
- **Use a native DP cable** instead of adapters
- Some adapters don't initialize fast enough for BIOS — try a different adapter or cable

---

## Audio Solutions

### Option 1: Audio Over DisplayPort (Best)

Audio is transmitted natively through DisplayPort. If your monitor has speakers or you use a DP-to-HDMI passive adapter, audio should work automatically.

**DP audio fix:** Fixed in **Linux 6.19.10+** (included in CachyOS, available in Bazzite desktop testing branch). Fix contributed by TheFloW (PS5 Linux developer), relayed by _fanoush_. The spread-spectrum audio disable landed in the **7.1 stable** kernel line (big_trov, 20/08/2026). **Resolved in 7.2:** the audio-clock fix was merged for 7.2 (patch submitted by Trov, per _mastag, 25/09/2026).

**DP→DP audio desync — root cause found and upstreamed (Oct 2026):** the remaining desync on DP-to-DP links was a driver bug: a bad order of hw-revision checks meant the **DCN3 clock table (700 kHz refclk) was loaded instead of the correct DCN2 one (600 kHz)** for gfx1013; plus the driver assumed spread-spectrum downspread while the board's clock doesn't use it — "the fix there was to assume no spread spectrum on dcn201" (big_trov, 04/10/2026, discussing the upstream `dcn201_clk_mgr` vs `dcn30_clk_mgr` values) [confirmed: @big_trov, 04/10/2026]. Fix is upstream in Linux; DP→HDMI adapters were never affected by the downspread half of the bug.

**HDMI CEC:** supported via the MastaG `bc250-cec` kernel package (auto-installed with `linux-cachyos-bc250`; needs a CEC-capable HDMI link) (_mastag, 25/09/2026, CachyOS repo thread:391); the UGREEN 8K DP→HDMI adapter is confirmed CEC-capable (keroppl_wizard reply, 09/10/2026, chat:25925). On Bazzite, CEC is enabled from the Bazzite Portal app with the UGREEN adapter — worked on a TCL Fire TV, but it is TV-dependent (u/Nova2127u, 25/10/2026, reddit).

**Washed-out colours:** if the desktop and games look desaturated versus another PC on the same monitor and cable, turn **HDR off** — "counterintuitively, be sure to turn HDR OFF" (u/toomanypubes, 28/10/2026, reddit, in a thread about a CachyOS board with a direct DP cable).

**Dolby Digital 5.1 via HDMI/eARC on SteamOS (rpf16rj, 17/08/2026):** if your BC-250 connects to a receiver/soundbar through the TV, TVs downmix multichannel audio to PCM stereo over eARC. SteamOS never enabled its built-in AC-3 profile because the board identifies as "AMD BC-250" in DMI instead of Valve's "OEM F7F". The toolkit ([rpf16rj/bc250-steamos-real-toolkit](https://github.com/rpf16rj/bc250-steamos-real-toolkit) **v1.3.0**) adds a udev rule + WirePlumber config that activates it: real-time Dolby Digital 5.1 encoding for all system audio (~1–2% CPU, zero latency), automatic stereo upmix, works with any active DP-to-HDMI adapter. Setup: run the toolkit → option 13 inside option 2 (manual) → Install AC-3 Surround Encoding; in KDE audio settings select "HD-Audio Generic Digital Surround 5.1 (HDMI/AC3)". Tested on SteamOS v3.18.25 (kernel 6.18.42-valve2). 

**Adapter audio status (May 2026):**
- **Passive adapters:** Audio works correctly, no issues reported with kernel 6.19+.
- **Active DP-to-HDMI (UGREEN 8K60Hz):** Audio dropouts every ~38 seconds (essdee4336). Active adapters enable 1440p@120Hz but audio quality suffers. 4K not recommended on this board.
- **Passive DP-to-HDMI (generic):** Limited to HDMI 1.4 (1080p60 / 1440p60, no 120Hz). Audio works fine.
- **Note:** Some Bazzite users still report pitch-shifted audio via DP→HDMI even on recent kernels (nataliezaki, May 2026). Native DP connection avoids all audio issues.

**TV handshake / flicker (Oct 2026):** board fine on all monitors but flashing black/white/gray screens on a TV via adapters — plain **DP→HDMI cable, no adapter dongle** fixed it for multiple users: "I've had the best luck without using adapters, just a plain DP to HDMI cable. Everything from multiple TVs, good PC monitors and cheap portable [screens]" (u/jordanka161, corroborated by u/Chemical_Reaction69, 08/10/2026, reddit). If you must use an adapter, see the EDID/DSC notes above.

### Option 2: USB Sound Card (Most Reliable Fix)

If audio over DP isn't working, use a USB audio adapter:

| Product | ASIN | Notes |
|---------|------|-------|
| **Creative Sound Blaster Play! 4** | `B08T9LM3LM` | 24-bit/192 kHz, ~$25-34. Note: not frequently mentioned in community — most users prefer generic USB audio dongles (Sabrent, UGREEN, Apple). |
| **SABRENT AU-EMCB** | `B00XM883BK` | Budget option, confirmed working, plug and play (ASIN verified) |
| Cheap USB-C phone dongle | Various | Works with USB-C to A adapter; Apple USB-C adapter + A-C adapter confirmed |

> ⚠️ The ASIN `B0BQ5VJVWB` that appeared in some older guides is an **Amazon Renewed listing** and may not always be available. The standard retail ASIN is **`B08T9LM3LM`** (Play! 4) or **`B06XBZ38ZJ`** (Play! 3).

## VRR (Variable Refresh Rate)

VRR is now achievable through multiple paths:

1. **CachyOS** (kernel 6.19): VRR works natively (steffman_, help-thread). Tested with UGREEN 8K DP-to-HDMI 2.1 adapter at 4K 120Hz with VRR and sound all working simultaneously via USB sound card.
2. **Custom Bazzite image**: Community image with AMD VRR kernel patches confirmed working on Bazzite Deck with OLED. Audio desyncs on expensive DP>HDMI adapters, but cheap Aliexpress 4k60hz adapters support VRR without audio issues.
3. **Kernel 6.19+**: Built-in VRR fixes (fforduck/Discord).

**Adapter notes for VRR:**
- **UGREEN 8K DP-to-HDMI 2.1**: Would give 4K 120Hz HDR + VRR if audio gets sorted (currently desyncs on custom Bazzite build). The audio-desync root cause has since been identified and upstreamed (see DP audio fix above); on `linux-cachyos-bc250` 7.2 at least one user lost audio on cheap UGREEN DP→HDMI adapters while standard CachyOS 7.2 / 7.3-rc4 kept it (keiser1080, 25/09/2026) — see the [Kernel Support Matrix (05)](05-os-installation.md#kernel-support-matrix-canonical--as-of-2026-10-29).
- **Cheap Aliexpress 4K 60Hz adapters**: Support VRR on kernel 6.19+ and do NOT have audio desync issues -- best current option (fforduck, Apr 2026). Note: earlier community reports (essdee4336, Apr 2026) said cheap adapters do NOT support VRR; resolved by kernel 6.19+ patches. One user went further: a custom **EDID-override kernel module** makes a cheap adapter report 4K@120 capabilities ("pushes 4k 120hz on it"), and reports finding a kernel bug that was limiting adapters below even their stated capabilities (dropbomb__, 06/10/2026) — not published/reviewed yet (open question).
- **Expensive DP>HDMI adapters**: VRR not supported, audio desync on custom Bazzite builds.
- **UGREEN active-adapter firmware (`bc250-ch7218-fw`):** the UGREEN 8K DP→HDMI adapter's CH7218 bridge now has a community-maintained flasher. UGREEN shipped firmware **07.00.69** after the community's technical report (initially untested; the old watchdog code stayed in it, so the black-picture-after-AVR-input-switch bug was *not* fixed). 07.00.69 then **regressed VRR** (it doesn't advertise VRR, so KDE/Gamescope hide the option), resolved in package **v1-5** + a kernel toggle: `sudo bc250-ch7218-flash flash tmds --yes`, unplug the DP end for ~5 s, and/or boot with `amdgpu.bc250_ch7218_vrr=1` — VRR then works on 07.00.69 (tested on an LG OLED G5, adapter directly connected). Images: `original`=07.00.54, `ugreen-69`=stock 69, `tmds-69`/`tmds`=patched (needs v1-3+). Inspect with `bc250-ch7218-flash status`/`list`; README at `/usr/share/doc/bc250-ch7218-fw/README.md`. **Flash over SSH, not from the display the adapter drives** (_mastag, 10–20/10/2026) [confirmed: @_mastag, 20/10/2026].

### DSC (Display Stream Compression) — 4K120 and PCVR (Sep 2026)

**Problem (alexxxor_, 13/09/2026):** DisplayPort DSC was not enabled in the kernel DCN 2.0.1 driver — DCN201 is a 98.6% compatible subset of DCN2.0/2.1, but DSC engine, power domain, and bitfields were missing. This blocked **PSVR2 headset** connection and **4K120Hz 4:4:4 via DP→HDMI** adapters (alexxxor_, 13/09/2026) [confirmed: @alexxxor_, 13/09/2026].

**Investigation (Sep 2026):** alexxxor_ started investigating for PSVR2 (DRM lease / Handoff doc in gist); _tayne_ in parallel for 4K120Hz 4:4:4 via DP→HDMI (13/09/2026). Prevailing theory: Sony did not intentionally disable it — likely neglect, like VCN ( _tayne_, 13/09/2026).

**Breakthrough (_tayne_, 13/09/2026):** `DSC is functional, thank you Claude Sonnet 4.6` — full operational log:
`DP-1 (active — your LG CX): dsc_clock_en: 1 ... dsc_pic_width: 3840, dsc_pic_height: 2160 ... dsc_bits_per_pixel: 224 ... Link: 4 lanes × 0x1e (HBR3 = 8.1 Gbps) = 32.4 Gbps raw ... You're running 4K@120Hz with DSC over HBR3 + HDMI 2.1 FRL PCON on AMD Cyan Skillfish — something the driver shipped as explicitly disabled. This is the first time this hardware has done this on Linux.` [confirmed: @_tayne, 13/09/2026]

- **VRR** also works with the CableMatters 102101 adapter ( _tayne_, 13/09/2026).
- **PCON** fully functional; MST use-case unknown ( _tayne_, 14/09/2026).
- **Kernel patch (upstream WIP):** _mastag_ `0011-gud-bound-tv-mode-count.patch` in [MastaG/linux-cachyos-bc250](https://github.com/MastaG/linux-cachyos-bc250/blob/main/patches/linux-cachyos/0011-gud-bound-tv-mode-count.patch) (13/09/2026); anonymized SteamOS 3.9 package: `DSC_PCON_SteamOS_3.9.zip` ( _tayne_, 13/09/2026).
- **PSVR2 — working via a DCN 2.0.1 DSC wiring patch (29/10/2026).** The headset negotiates only a 2-lane HBR3 link but wants 4000×2040 @ ~120 Hz, so it requires DSC. The patch is five changes in one amdgpu file: declare the DSC blocks to the resource allocator, create them, tear them down on unload, point one function at the DCN 2.0 implementation that already works, and teach the bandwidth validator about them ("miss that last one and it still prunes your mode"). Result: headset comes up at 4000×2040, DSC engaged at 10 bpp over two HBR3 lanes, full SteamVR with both Sense controllers, VRChat at **40–55 FPS at 1520×1548 per eye** (u/Neat-Significance275, 29/10/2026, reddit). No byte of it is BC-250-specific — it is DCN 2.0.1 missing wiring its neighbour has. Caveats: one board, one kernel, rebuilt after every kernel update; back up the stock module first. Userspace gotchas found along the way: use the Ignition build of PSVR2Toolkit (not the Windows one), set the SteamVR compositor environment fix, and clear Steam's SDL ignore list for the Sense controller IDs under Wine (u/Neat-Significance275, 29/10/2026, reddit).
- **Toolkit v1.9.6 (rpf16rj, 20/09/2026):** 4K120 over DP→HDMI 2.1 adapters fixed — no more black screen or artifacts at cold boot or when booting straight into Game Mode; the toolkit now auto-limits color depth to what the TV/adapter can carry. The debugfs `dsc_bits_per_pixel` override now sticks even with the display off or mid-transition [confirmed: @rpf16rj, 20/09/2026].
- **Caution — DSC patch vs governor race (Sep 2026):** the DSC patch introduces a race window with the GPU governor on reboot; the DP→HDMI PCON can fail link training and the display stays unstable until the PCON is reconnected (at either end). Seen on CachyOS and SteamOS 3.9; no root cause yet, reverting the DSC patch was suggested (_tayne, 18/09/2026) [confirmed: @_tayne, 18/09/2026].

---

## Multi-Monitor Setup

| Method | Notes |
|--------|-------|
| **DisplayPort MST Hub** | Works on Bazzite. Maximum 2 screens via MST on BC-250 (elektricM). Active DP→HDMI adapters work on hub outputs (pops1cl/Discord). ⚠️ More than 2 monitors on an MST hub can crash the amdgpu driver (pops1cl/Discord). |

**Tested MST Hub Compatibility (elektricM docs):**

| Adapter | Display-out | DP | Display | Audio | Notes |
|---------|-------------|----|---------|-------|-------|
| StarTech MST14DP122DP | DP (2) | 1.4 | Yes | Yes | Worked consistently across different monitors/cables |
| Monoprice 21972 | DP (2) | 1.2 | Mirror only | Yes | Unable to extend displays |
| ENBUER | DP (2) | 1.2? | Mirror only | Yes | Unable to extend displays |
| Generic | HDMI (2) | N/A | No | No | No video or audio |
| **DisplayLink Dock** | USB (DisplayLink) | N/A | Yes (desktop only) | Yes | Desktop use only, not gaming. V7 Universal (Best Buy `10872445`) claimed dual HDMI on Bazzite. | [confirmed: @toastboy6035, 12/02/2026]
| **Dell ACP075EU** | USB (DisplayLink) | N/A | Yes (desktop only) | Yes | Docking station with DisplayLink + USB DAC — claimed works | [confirmed: @toastboy6035, 12/02/2026]

---

## Monitor Recommendations

| Use Case | Recommended Spec |
|----------|-----------------|
| General gaming | 1080p, 144 Hz, IPS panel, DP 1.4 certified cable |
| Best value | 1080p 60 Hz (you won't miss higher refresh at 60 FPS) |
| 1440p gaming | 1440p@144Hz DP monitor, DP 1.4 cable <2m; use FSR Quality to hit 60 FPS |
| 4K | 4K@60Hz monitor with DP; use active DP-to-HDMI adapter for HDMI display + USB audio |

> At 1080p native with the BC-250, you'll get the sharpest image and best performance. FSR handles upscaling well if you go higher resolution.

### VRS 640x480 Resolution Fix

Some games render at 640x480 due to broken Variable Rate Shading on Cyan Skillfish. bangstk's [Vulkan_NullVRS](https://github.com/bangstk/Vulkan_NullVRS) layer nullifies VRS commands:

```bash
git clone https://github.com/bangstk/Vulkan_NullVRS.git
cd Vulkan_NullVRS
make
mkdir -p ~/.local/share/vulkan/implicit_layer.d
cp ./Vulkan_NullVRS.json ~/.local/share/vulkan/implicit_layer.d/
cp ./libVulkan_NullVRS.so ~/.local/share/vulkan/implicit_layer.d/
```

Steam launch option: `ENABLE_VK_NULLVRS_1=1 %command%`

## Streaming (Sunshine + Moonlight)

**Black screen after Bazzite 44 update (Aug 2026):** multiple users report Sunshine + Moonlight streams show a black screen in game mode after updating to Bazzite deck 44. Issue persists across SteamOS and CachyOS as well. Cause unknown — may be related to hardware encoder/decoder initialization. Workaround: pyrowave (Vulkan-based encoder) is an alternative that bypasses the hardware encoder entirely (autistic_neckbeard, 24/08/2026).

**Last verified: 2026-10-29**