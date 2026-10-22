# 07 — Game Benchmarks

> Community-tested performance data for the BC-250 (Cyan Skillfish APU).
> Most tests at 1080p — the sweet spot for this hardware (~RX 6600 level).

---

## Performance Expectations

| Resolution | Quality | Typical FPS Range | Notes |
|------------|---------|-------------------|-------|
| 1080p | Low | 100–144+ | Esports, older titles |
| 1080p | Medium | 80–120+ | Sweet spot for most games (elektricM docs) |
| 1080p | High | 60–100+ | Most titles (elektricM docs) |
| 1080p + FSR Quality | High + FSR | 70–100+ | Free performance boost [confirmed: @1_gec, 04/12/2025]
| 1440p | Medium + FSR | 50–80 | Playable with upscaling (elektricM docs) |
| 4K | Low + FSR | 30–40 | Older/less demanding titles only |

---

## AAA Titles

### Cyberpunk 2077

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p High + FSR, no RT | 70–90 | elektricM docs |
| 1080p High + FSR + RT (lighting only) | 50–60 | elektricM docs |
| 1080p Ultra + FSR3.1 | 100+ | elektricM docs |
| 1080p CPU-bound areas | <60 even at lowest (attribution pending) | CPU bottleneck in dense areas — "heavily CPU bound, graphic settings do not matter" (hecto_77113, 09/07/2026) |
| Power draw | Up to 235W | Most demanding game in the library (elektricM docs) |

**Benchmark scores:**
- Stock (2000 MHz, 1000 mV): **57.66 FPS** — elektricM docs
- OC (2230 MHz, 1035 mV): **60.82 FPS** — elektricM docs
- With `mitigations=off`: **+18 FPS** boost — elektricM docs
- **38 CU, 2270 MHz GPU, 4050 MHz CPU, 1975 MT Memory, Ultra no FSR: min FPS >60** — dznuts (May 2026). Matched RTX 3060 performance level. Memory OC gave **+18.4% min FPS boost**.

**6-core vs 8-core unlock (40 CU, 1900 MHz GPU @ 880 mV, 3900 MHz CPU @ 1150 mV, FHD, _kierownik, 30/07/2026):**

| Settings | 6-core FPS | 8-core FPS | Gain |
|----------|-----------|-----------|------|
| Low, no upscale | 80 (170W) | 89 (180W) | +11% |
| Low, FSR2 | 85 (160W) | 93 (173W) | +9% |
| Low, FSR3 | 83 (160W) | 93 (162W) | +12% |
| Medium, no upscale | 72 (178W) | 76 (187W) | +6% |
| Medium, FSR2 | 79 (170W) | 90 (178W) | +14% |
| High, no upscale | 63 (180W) | 66 (189W) | +5% |
| High, FSR2 | 73 (170W) | 80 (180W) | +10% |
| Ultra, no upscale | 55 (180W) | 58 (189W) | +5% |
| Ultra, FSR2 | 63 (175W) | 70 (185W) | +11% |
| Ultra, FSR3 | 64 (175W) | 70 (184W) | +9% |

8 cores give a consistent **+5-14% FPS** in Cyberpunk with ~8-10W higher power draw. See [02-BIOS & Firmware](02-bios-and-firmware.md) for core unlock methods.

**8-core 40CU Cyberpunk results (Jul 30 2026):**

| User | Config | Settings | FPS | Notes |
|------|--------|----------|-----|-------|
| dbkretro | 8 core + 40 CU | 1080p | ~60 | Up from ~52 with 6 core — "8 core 40cu gang" |
| qwert9811 | 8 core unlocked | Dogtown (CPU-heavy area) | Early 50s | Up from early 40s — ~10 FPS gain in most demanding area |

**Optimized FSR 4 RADV build (rescuemei/dmoraza, Aug 14 2026):** a community-patched RADV (Mesa 26.1.6 base) optimizing the FSR 4.1.1 INT8 fallback with i24 arithmetic reaches **~82–85 FPS vs ~70–75 with the previous "Golden" build** in a high-FPS test scene — shader dropped from 64k → 37k instructions ([github.com/dmorazasanchez/bc250-fsr4](https://github.com/dmorazasanchez/bc250-fsr4)). See [11-community-and-resources](11-community-and-resources.md).

**FSR4 vs XeSS vs FSR2/3 RT comparison (Aug 2026):** in RT Low tests (game unspecified), native = 56 FPS, FSR2/3 Quality = 75 FPS, FSR4 = 73 FPS, XeSS Balanced = 78 FPS. XeSS balanced outperforms both FSR2 and FSR4 in RT but image quality is worse. FSR4 balanced/performance is preferred for solid 60 FPS with frame generation, though input latency equals base FPS (e.g. FG from 30→60 has 30 FPS latency). Async compute patch alone gave ~10 FPS uplift (70→80 native) (dmoraza, community, Aug 2026).

**FSR 4 forks and the mesh driver (Sep 2026):** [daniel-h-0/bc250-fsr4-fork](https://github.com/daniel-h-0/bc250-fsr4-fork) (branch `v4`) is a community FSR 4 fork (capt.cat_13, 16/09/2026) [confirmed: @capt.cat_13, 16/09/2026]. For games that require native mesh/task shaders, [luckiskind/bc250-radv-r2](https://github.com/luckiskind/bc250-radv-r2) packages an experimental RADV R2 path (baseline credit: lonewolf0622) — in a scene-by-scene test it landed ~84 FPS versus ~94 FPS for the standard FSR3 fallback, so it is only worth it for the few games that need true mesh shaders (nonu0038, 24/09/2026) [confirmed: @nonu0038, 24/09/2026].

**Oct 2026 upscaler landscape — HelixSR takes over:**
- **HelixSR** ([lonewolf0622/HelixSR](https://github.com/lonewolf0622/HelixSR)) — "a hybrid neural upscaler that combines DLSS neural reconstruction with FSR 3.1's interface and temporal inputs" (D3D12 games only; Vulkan/D3D11 unsupported/untested as of 05/10/2026). Since 05/10 it is the **default upscaler in all three CachyOS bc250 Proton packages** (`proton-cachyos-native-bc250`, `proton-cachyos-slr-bc250`, `protonge-latest-bc250`) — "one package, nothing to set up by hand"; `PROTON_USE_OPTISCALER=helixsr` / `=fsr411f` switches between HelixSR and the old FSR4 default (_mastag, 05–09/10/2026) [confirmed: @_mastag, 05/10/2026]. Author's BC-250 numbers at 2000 MHz: ~1.4 ms/frame at 1080p Quality, ~4.4 ms at 4K Performance; HelixSR 1.4.1 QSSM Light 1.80 ms, QSSM Ultra 2.00 ms at 1080p (_mastag, 09/10/2026). Field results: CP2077 High preset Quality ~94 fps "within a maximum of 2fps of FSR3 but better image quality" (dmooney65, 05/10/2026); Black Myth: Wukong "nice uplift compared to fsr4r11" (hojnikb, 05/10/2026) — "fsr4 got obsoleted with helix" (hojnikb, 05/10/2026). Known early issue: Diablo IV reported "Not using FSR Upscaling" because Prism expects 15 required / 48 optional resources while 1.0.2 reported 7/24 — addressed in subsequent releases (Snk B / lonewolf0622x, 05/10/2026). A Bazzite GUI frontend automating HelixSR + OptiScaler setup exists: [RobertoTorino/bc250-bazzite-helixsr-gui](https://github.com/RobertoTorino/bc250-bazzite-helixsr-gui) (07/10/2026).
- **HelixSR Scaler is now the default (15–20/10/2026).** The default in the three Proton packages became **HelixSR Scaler** — OptiScaler with HelixSR built in, by lonewolf0622x — which runs NVIDIA's **DLSS network (Model E) as plain D3D12 compute**, so you pick DLSS/XeSS/FSR in-game as usual and `Insert` opens the menu (shows ONLINE when HelixSR is active). It also runs **experimental DLSS Frame Generation on the BC-250** (Halo: Campaign Evolved, 2259×1271→4K, 2× FG, ~3.2 ms upscaler). HelixSR stays **D3D12-only** — D3D11 and Vulkan games keep the FSR4 path. Version path: HelixSR **1.9.0 + Scaler 1.0.3** (15/10, OptiScaler nightly 20261015) → **2.0.0 + Scaler 1.1.0** (19/10), where a single `amd_fidelityfx_dx12.dll` now does upscaling *and* DLSS FG (the standalone `helixsr.dll` is gone; FG has light/full modes, OptiScaler-first auto-discovery — `pacman -Syu`, nothing to set by hand) (_mastag, 15–19/10/2026) [confirmed: @_mastag, 15/10/2026].
- **FreeFG (opt-in frame-gen, 20/10/2026):** [daniel-h-0/freefg](https://github.com/daniel-h-0/freefg) by daniel-h-0/@fish adds **Intel XeSS frame-gen at 2×** with part of the GPU work done by BC-250 shaders plus a Vulkan layer that paces frames for VRR. `PROTON_USE_OPTISCALER=freefg` (FSR4 upscaler) or `=freefg-helixsr` (HelixSR 2.0.0 — Spider-Man 2 on BC-250: HelixSR ~1.7 ms/frame vs ~5.3 ms for FSR4 RC11). DX12-only and experimental; FG input defaults to OptiFG, and a game with its own DLSS/FSR FG can use it via `BC250_OPTISCALER_EXTRA="FrameGen.FGInput=dlssg"`. New anticheat opt-out for players who accept the ban risk: `BC250_FSR4_IGNORE_ANTICHEAT=1` per game, or `~/.config/bc250-fsr4/ignore-anticheat` globally (_mastag, 20/10/2026) [confirmed: @_mastag, 20/10/2026].
- **Community framing:** "DLSS3.7 = FSR4.1 with costs comparable to FSR3" (u/Pla-C-Bo, 05/10/2026, reddit) and, from the FSR4-optimizer author: "I published the most recent round of work on fsr4.1 optimization and I'm just delighted to see it effectively obsoleted in a manner of weeks" (u/_I_AM_A_STRANGE_LOOP, 05/10/2026, reddit).
- **DirectMesh on by default:** Mesh/task-shader support ([lonewolf0622/bc250meshtaskwork](https://github.com/lonewolf0622/bc250meshtaskwork), DirectMesh v1.3 — indexed mesh draws 1.5–1.8× faster for meshlets ≥96 vertices) ships in CachyOS `mesa`/`mesa-git` and since **DirectMesh 1.3.1 (09/10/2026) is on by default whenever a BC-250 is detected** — `RADV_DIRECTMESH=1` no longer needed (`RADV_DIRECTMESH=0` opts out). v1.3.1 fixes the 4K GPU hang (23,000 frames clean), moves index-route storage VRAM→GTT (stops filling the 512 MiB carve-out), passes Mesh CTS 1,902/1,902, and is within ~1% of v1.3 in all 44 benchmark cases (_mastag, 09/10/2026) [confirmed: @_mastag, 09/10/2026]. The old workaround `RADV_BC250_MESH_IDXPASS=0` can be removed. Timeline: MastaG dropped the game-specific workaround patches from his repo in favor of shipping DirectMesh ("that is not supported any longer in my repository… I now carry DirectMesh 1.2", FF7 Rebirth thread, 04/10/2026; v1.3 "all fixed, I'll ship with v1.3 today" — lonewolf0622x, 04/10/2026). A Control Center × HelixSR/OptiScaler integration was agreed in-discussion (cassettesgoboom/_movacx/lonewolf0622x, 06–07/10/2026) but not shipped as of 09/10.
- **XeFG/XeMFG frame-gen:** Intel XeSS frame-gen enabled and BC-250-accelerated for DX12 games on Linux/Proton (GE-Proton 11-6/11-7 verified) — Cyberpunk 2077 2× = "+22% over Intel's shaders, +48% over no FG", 3×/4× sit at a 120 Hz ceiling (40 CU @ 1850 MHz, 1440p High, RT off); pre-verified settings for 19 games (~750 more via OptiScaler wiki). **Discord-only distribution — no GitHub** — because of restrictive XeFG modification TOS (iamastrangeloop, 29/09–01/10/2026) [confirmed: @iamastrangeloop, 29/09/2026].

**Tips:** Enable FSR Quality for a significant boost. DLSS/FSR Frame Generation works well. (elektricM docs)

**Sep 2026 benchmarks (40 CU, 8 cores):**
- Default High, 40 CU, 8 cores @ 2000 MHz (Bazzite) — baseline before tweaks (dbkretro, 06/09/2026) [confirmed: @dbkretro, 06/09/2026]
- Default High, 36 CU @ 2 GHz, 8 cores @ 3.85 GHz (Bazzite) — comparable (capt.cat_13, 06/09/2026)
- **1080p High (RT off) + FSR3 Native AA + FG 3.1:** **90–110 FPS** on 40 CU @ 2000 MHz (peak 1850 due to governor), 3.7 GHz CPU, 6 cores, stock pads/paste, 2x front +1 back P12 Pro — without case (halil_iboo, 06/09/2026). With `mitigations=off` + unlocked frame cap: **85 FPS** rock-solid 60 with cap re-enabled, no frame drops (dbkretro, 07/09/2026) [confirmed: @dbkretro, 07/09/2026].

---

### Black Myth: Wukong

| Settings | FPS | Notes |
|----------|-----|-------|
| 40 CU, 1080p Low (FSR off) | 61 avg | Old Lamer YouTube benchmark (June 2026) |
| RX 6700 (reference) | 59 avg | Same test conditions for comparison |
| RX 7600 (reference) | 71 avg | Same test conditions for comparison |

**Source:** Old Lamer YouTube benchmark (40CU BC-250 vs RX6700 & RX7600). The BC-250 at 40 CU slightly edges the RX 6700 in this title. See [11-community-and-resources](11-community-and-resources.md) for link.

**Sep 2026 FSR4 evaluation (hojnikb, 08–10/09/2026, CachyOS mastaG 7.2 kernel + Mesa, FSR3 V3 patch, 40 CU @ 2100 MHz 8c @ 3.8 GHz):** purpose was to evaluate FSR4 in this title — **FSR4 360p→1440p matches FSR3 908p→1440p, not worth it**; V4 patch adds ~13% uplift at 1440p (hojnikb, 08–09/09/2026); retest with Proton + FSR4 4.1.1b no real difference (hojnikb, 10/09/2026) [confirmed: @hojnikb, 08/09/2026].

**Oct 2026 HelixSR retest (hojnikb, 05/10/2026):** re-ran the benchmark with HelixSR 1.0.3 Performance — "nice uplift compared to fsr4r11, retested here" [confirmed: @hojnikb, 05/10/2026] — the community verdict in-thread became "fsr4 got obsoleted with helix" (hojnikb, 05/10/2026). See the upscaler section below.

---

### Hogwarts Legacy

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p Medium | ~60 (nexgen3d, 26/12/2025) | Needs zswap or zram enabled (16 GB RAM is tight) |
| With FSR4 on Proton GE | Playable [confirmed: @lonewolf05849, 16/01/2026]
| 4K, 60 FPS | Playable | "Playing Hogwarts at 4k 60fps on the bc250" [confirmed: @cubehacker8107, 19/08/2026] — settings not shared |

> Game needs ~16.5 GB RAM. Enable zswap + swapfile (preferred) or zram (`zram-size = ram x 0.75`) and close background apps — see [05-OS Installation → Memory Configuration](05-os-installation.md#memory-configuration-zswap-vs-zram) (zram note: hojnikb, 08/03/2026; zswap preferred: pops1cl/essdee4336, 23/06/2026).
> Use 6 GB static VRAM allocation to avoid OOM crashes. [confirmed: @big_trov, 28/02/2026]

---

### Red Dead Redemption 2

| Settings | FPS | Notes |
|----------|-----|-------|
| Full graphics (DX11) | Smooth (45+ FPS min — elektricM docs) | Heatsink barely warm with 120mm fan |
| 2230 MHz GPU | Crashes (i_guess_im_a_girl, 20/11/2025) | Reduce to 2150 MHz for stability (i_guess_im_a_girl, 20/11/2025) |
| 10/6 VRAM split | Fixed crash | Static allocation avoids ZRAM conflicts [confirmed: @xseol, 12/07/2025] |

**Launch flag:** `-useMaximumSettings` — elektricM docs
**Adapter fix:** May detect as software rendering — change adapter in graphics settings to match `vulkaninfo --summary` output (elektricM docs)
**Temps:** ~75C during gameplay. [confirmed: @.strykur, 15/01/2026]

**8-core 40CU RDR2 (dbkretro, Jul 30 2026):** 1080p, decent quality settings — near 60 FPS with main dip during snow scenes. GPU bound in most scenarios but less stutter in city areas with extra cores.

**8-core 38CU RDR2 benchmark (sho.ta, Aug 13 2026):** ~65 FPS in benchmark, 55–85 real FPS, High-Ultra 1080p on Bazzite with **0.5/15.5 memory split** (38 CU @ 1900 MHz 900 mV, 8 cores @ 3.85 GHz 1150 mV). "Timegraph is smooth most of the time" — FPS drops significantly in Saint Denis (~40–45 FPS) with spiky timegraph due to poor CPU performance.

**VRAM split doubles 1440p performance (Sep 2026):** jamdoggie's 40 CU/8c CachyOS board ran "40 fps in most areas of rdr2 at 1440p native" with ~30–40% GPU utilization; switching the BIOS split to **512 MB dynamic** produced 80–90 fps in the benchmark with full GPU utilization (25/09/2026) [confirmed: @jamdoggie, 25/09/2026]. big_trov's explanation: the default 8/8 fixed split lets the game map up to 12 GB, starving system RAM and forcing swap; the 512 MB setting caps GPU use at ~8 GB and leaves RAM for the OS (25/09/2026) — see [02 → VRAM Allocation Options](02-bios-and-firmware.md#vram-allocation-options).

**Sep 2026 update (38 CU, 8 cores, 2000 MHz, 3.9 GHz):** 1080p Ultra **70–80 FPS** at 67–70 °C after 1h without crash, MangoHud overlay ~70 FPS average; benchmark peak ~70–80 FPS under 70 °C (shibly_91236, 04/09/2026 and 07/09/2026, Proton GE) [confirmed: @shibly_91236, 04/09/2026].

---

### Spider-Man 2

| Settings | FPS | Notes |
|----------|-----|-------|
| Medium, 6 GB VRAM | ~60 | GPU/CPU around 65C | [confirmed: community reports]
| 1080p native AA, Medium | 55–60 | Textures Medium, rest Low |
| 1440p FSR3 Quality | ~55–60 | Similar to 1080p native | [confirmed: @nexgen3d, 09/12/2025]
| Auto VRAM | Crashes after 5–10 min | Must use 6 GB+ static allocation | [confirmed: @bigmedi, 02/05/2026]

**Fix:** Add kernel params: `ttm.pages_limit=3959290 ttm.page_pool_size=3959290`

---

### Elden Ring

| Settings | FPS | Notes |
|----------|-----|-------|
| Any settings | 45–50 (mzk10, 06/11/2025: "hangs around 45fps... nothing gets it above 50fps") | CPU-bound — elektricM docs report expected 60 FPS with settings adjustments |
| 4K | 30–40 | Playable but choppy | [confirmed: @imeden, 09/12/2025]

> Changing resolution/settings may not help.
> Fix skybox artifacts: `RADV_DEBUG=nohiz` in Steam launch options.

**8-core GPU unlock boost (glide_2026, Aug 3 2026):** Temporary unlock of extra cores gave **~10 more FPS** ("definitely added 10ish frames"), though still fluctuates around 60 — gains are CPU-dependent and vary by scene.

> *Source: [glide_2026], Discord chat; also confirmed in-field reports.*

---

### The Crew Motorfest

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p High | 60 capped | GPU OC 2100 MHz, CachyOS with Proton-Cachy |

### Borderlands 3

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p Medium, 8x AA | ~62 | Eden-6 benchmark (whomstdv, 26/11/2025); inventory has black box background (cosmetic only) |
| 1080p Ultra, 2 GHz OC | 68 → 82 | OC uplift (.warlocksyno, 25/05/2026) |
| Default (low/medium mix) | ~60 | (selectivelygood_16010, 27/11/2025) |

### Starfield (vvaaron, Dec 2025 - Jan 2026)

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p Medium | 48–60 | 60 FPS capped with frame gen |
| 1080p High | 39–60 | FG: 58–60 FPS |
| 1080p Ultra | 35–60 | FG: 58–60 FPS, temps 64C max |
| 1080p Medium (New Atlantis) | 48–53 | Most demanding location |

> vvaaron (08/12/2025): "playing Starfield at 1080 stock ultra settings. With frame gen enabled (gpu intensive). Getting a really good experience at a capped 60fps"; (06/01/2026): "holds a stable 60fps on ultra with frame gen (although a slightly nicer experience at mid-high without frame gen)". GPU OC 1000–2220 MHz, P12 Pro fan.

---

### Alan Wake 2

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p | ~100 with FG | Reported playable, frame gen recommended | [confirmed: @chiribayashepherd, 10/06/2026]

---

## Shooters & Action

### Doom Eternal

| Settings | FPS | Notes |
|----------|-----|-------|
| Ultra (not max VRAM) | 100 | Loves Vulkan | [confirmed: @spitko, 03/02/2025]
| 512 MB VRAM | Heavy stuttering | Needs higher VRAM allocation | [confirmed: @fforduck, 02/05/2026]

### Doom: The Dark Ages (Update 2+)

| Settings | FPS | Notes |
|----------|-----|-------|
| Low / Handheld preset, 1080p, FSR Quality | ~60 | GPU 2230 MHz, CPU stock |

**Fix:** VRS crash — use [Vulkan_NullVRS](https://github.com/bangstk/Vulkan_NullVRS) layer (bangstk, May 2026).

### Crimson Desert

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p Medium, no scaling | 38–42 | |
| Ultra (textures High), 4K + FG | ~60 solid | Open world with fast-flight mod; drops in dense towns [confirmed: @dmoraza, 14/08/2026] |

**Fix:** Use Proton Experimental Bleeding-Edge branch with VKD3D RDNA1 fix. Version 1.02 works. [confirmed: @nohanmv, 01/04/2026]

> The **v1.18.00 game update broke launch on Proton 11** for some users; `proton-cachy` and Proton Experimental work (.crotch, 19/08/2026). VRAM split: fixed 3–4 GB works best — games detect 6 GB and can use up to 8 GB; forcing 6 GB static broke some games, and dynamic 512 MB loads lowest-quality textures in this title (@cubehacker8107, @h00man._., @_mastag, Aug 16 2026).
> At 38–40 CU: ~55 FPS FHD no scaling — +10–15 FPS over 24 CU (pijuli.); CPU-limited in some areas (vfxmz).

### Space Marine 2

| Settings | FPS | Notes |
|----------|-----|-------|
| 8 cores unlocked | ~2x vs 6 cores | smcelrea, Aug 10 2026 — "almost double the perf in space marine 2, in the rippers section of the campaign, with 8 cores unlocked" |

> Severely CPU-bound on this board; the 8-core unlock is the single biggest win for this title.

### Pragmata

| Settings | FPS | Notes |
|----------|-----|-------|
| 8 cores + governor tweaks | High | lovelifetrustfaith, Aug 10 2026 — "pragmata ran pretty good before the cpu core unlock and additional tweakings"; later "pragmata now on stock governor values, just insane..." |

> First launched unreliably ("For some weird reason it won't start") — resolved after additional tweaks from MastaG's GitHub (see [11-community-and-resources](11-community-and-resources.md)).

### Death Stranding 2

| Settings | FPS | Notes |
|----------|-----|-------|
| 36 CU, ultrawide 1440p High + frame gen | 60 locked | dartzon, CachyOS, Thermalright PA120, GPU backplate cooler, <72C |
| 36 CU, 1440p High, no frame gen | Dips under 60 | CPU bottleneck (dartzon) |
| 1080p Low, FSR 3.1.5 | ~60 dips to 45 | CPU limited |

**PICO upscaler:** PlayStation's FSR equivalent was ported to PC as "PICO" — works on Decima engine games (Horizon, Death Stranding). User reports it's superior to AMD FSR3 (dartzon, May 2026).

**Cooling:** dartzon used Thermalright Peerless Assassin 120 + GPU backplate cooler with fans for VRAM chips. Temps never exceeded 72C with 36 CU unlocked.

### Monster Hunter Wilds

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p Medium | +12% with `mitigations=off` | |

**Fix:** `sudo rpm-ostree kargs --append='mitigations=off'` [confirmed: @filippor, 09/12/2025]

### Doom 2016

| Settings | FPS | Notes |
|----------|-----|-------|
| Max graphics | 100 | Spanish community benchmark |

### Forza Horizon 6 [Discord user, May 2026]

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p High + FSR 3.1.5 | 40–60 | Preset High, FSR helped fix pixelated textures |
| Proton (CachyOS) | Playable | Low memory warning after prologue — try 512MB split + zswap (antmagl, jeffr7814); menu FPS drops to 15 (capt.cat_13) |

### Genshin Impact

| Settings | FPS | Notes |
|----------|-----|-------|
| 1080p Ultra | 60 locked | 65–68C after 4 hours. Runs great. [confirmed: @daniifreitas, 08/12/2025] |

---

## Competitive / Esports

### CS2 (Counter-Strike 2)

| Aspect | Detail |
|--------|--------|
| Performance (elektricM docs) | **100+ FPS expected at 1080p** |
| Community test | 60–80 FPS with stuttering in some configurations | [confirmed: @nonu0038, 14/05/2025]
| Stability test | Unstable OC crashes CS2 first — add +30 mV if crashes occur | [confirmed: @jayrule, 03/12/2025]

### Rocket League

| Aspect | Detail |
|--------|--------|
| Performance (elektricM docs) | **120+ FPS expected at 1080p** |
| Community test | 60 FPS locked at 1080p — settings maxed | [confirmed: @codyrainy, 23/04/2026]

### Valorant

Expected: Technical challenges — anti-cheat may have issues on Linux (elektricM docs).

---

## Single-Player / Story Games

| Game | Performance | Notes |
|------|-------------|-------|
| Half-Life: Alyx | ~80 FPS | CachyOS [confirmed: @nataliezaki, 27/05/2026]; VR via Monado runs well but not at max settings (ithinkibrokeit_, Apr 2026); ~120W TDP cap tested (kilrah) |
| Hellblade: Senua's Sacrifice | ~180 FPS | High FPS, well-optimized |
| Hellblade II: Senua's Saga | 60fps FSR4 Quality / 65 balance / 73 performance | Medium settings, 1080p. 60fps on FSR4 Quality requires the gfx1013 compute queue patch. [lonewolf05849, Aug 8 2026] |
| Mortal Kombat 1 | Struggles to stay locked at 60 FPS | GPU refuses to fully boost (felingreenleaf, Aug 6 2026). [verified: Steam appid 1971870] |
| Resident Evil 9 | Solid 60 FPS (dbkretro, Aug 9 2026) | "Solid 60fps on RE4 and RE9" (dbkretro, Aug 9 2026); appears in Old Lamer BC-250 benchmark video. 1080p high manual + hair strands, FSR quality (dbkretro); frame gen crashes on Bazzite with REFramework (.strykur, 25/05/2026) |
| Assassin's Creed IV: Black Flag – Resynced | Playable (dmoraza, Aug 5 2026) | 2K FSR Quality + FG, max details no RT; TAA native 1080p: 45–50 FPS city / 60+ sea (g_sh0ck., 15/07/2026). Tested with broken RAM at 1600 MHz. [Steam appid 242050] |
| Resident Evil 4 (2023 Remake) | ~60 FPS stable — dbkretro, Aug 9 2026 | Bazzite + governor + 8-core/40 CU at 1750 MHz. Previously reported crashes (May 2026) no longer reproducible. [Steam appid 2050650] |
| Arc Raiders | 60+ | Medium, FSR Quality — 60+ FPS, ~69C (maty99, 26/03/2026 benchmark post) |
| Ghost of Tsushima | 45–60 at 1080p Low | Crashes without game update v1053.5+ (dryadalis5392, 13/12/2025; no crash on v1053.0718+ — sinh_28065, 12/02/2026); 1.7–1.9 GHz GPU OC (attribution pending). Check ProtonDB for AMD GPU fixes. |
| Final Fantasy VII Remake | Playable | Rebirth broken: "DX12 is not supported on your system" — game checks for specific GPU compatibility (elektricM docs). 512 MB allocation: "ff7 tend to crash while playing on 512mb" (lonewolf05849, 11/01/2026) [confirmed: @dwtoledo, 12/10/2025] |
| Horizon: Zero Dawn | Great at 1080p High | No upscaling needed [confirmed: @nexgen3d, 09/12/2025] |
| Horizon: Forbidden West | 45–60 / 70–90 with FG | FSR + frame gen, low settings; low GPU usage at 1080p — settings changes don't help (_titotito, 08/06/2026) [confirmed: @_nk10, 15/12/2025] |
| Hunt: Showdown 1896 | 90–120 with FSR / 20–40 without | |
| Forza Horizon 5 | 40–100 FPS | "40fps" → "now I have 100 fps" depending on settings (ungamead, 21/02/2026); 1440p TAA High hovers 50–60 (antmagl, 16/05/2026) |
| Stellar Blade [fforduck, Discord user] | 50–80 FPS at 1440p | Medium settings, FSR4 |
| Helldivers 2 | 40–60 FPS | "frames around the 40-60fps" (eurobirb, 27/11/2025) |
| Valheim | 40–80 FPS | "solid 100% boost by disabling mitigations" (imeden, 05/12/2025) |
| GTA V Enhanced (RT) | Smooth on Mesa 26 | "go from 70fps to 3-5fps abruptly" before Mesa 26 (soulnull, 14/02/2026); 1440p High FSR3 Quality, 65C, 40 CU @ 1500 MHz (fontanedo, 29/05/2026) |
| Oblivion Remaster | 30–75 FPS at 3440x1440 | "30fps+ with fsr set to balance and no framegen" / "75fps with frame gen" (gennro, 28/03/2026) |
| Oblivion Remastered — no FG | 25–30 FPS in forest; cities/dungeons run well | Frame gen helps a lot but forest stutters remain [confirmed: @zerosumpr, 23/08/2026] |
| No Man's Sky (40 CU) | Playable, rendering artifacts | Missing specular highlights vs NVIDIA reference even with GTAO off [confirmed: @cubehacker8107, 16/08/2026] |
| Marvel Rivals | 100–190 FPS | "went from like 190fps ➡️ 100fps" (jainator, 10/05/2026); Season 8 perf mod on NexusMods (graytl) |
| Warframe | 75 FPS at 1080p | V-Sync ON, no FSR [confirmed: @whomstdv, 02/12/2025]; 120 FPS @ 1440p — "cruising at 120fps 1440p no issues" (discombobulateddunce, 04/06/2026) |
| War Thunder | Playable at 1080p High | Max GPU OC, no RT |
| The Last of Us Part I | 60 FPS locked, 1080p Medium-High | elektricM docs; FSR caps GPU clock at 1000 MHz — workaround in elektricM docs |
| The Callisto Protocol | 60–85 at 1080p Medium | 60 locked, hits 85 frequently (nexgen3d, 04/12/2025 benchmark) |
| Tomb Raider (2013) | 100–140 FPS at 1080p Max | |
| Death Stranding | 40–50 FPS at 1080p Max | [confirmed: @pijuli., 24/03/2026] |
| Zenless Zone Zero | Crashes with "Memory shortage" error (pm_me_kitsunemimi, 31/03/2026) | May need workaround |
| Diablo IV | Playable | Medium-high settings; 1440p max + FSR "rolling that fps" (bobafettm, 16/02/2026) |
| Baldur's Gate 3 | Playable at 1080p | Lower settings in cities |
| Detroit: Become Human | 60 FPS capped, 1080p Medium | elektricM docs |
| Devil May Cry 5 | 100 FPS, 1080p High | elektricM docs |
| Where Winds Meet | 20–60 FPS | 4K: CPU-bound drops to 20s at 50% GPU util (40 CU @2 GHz, 8c 4 GHz — dejan_994, 07/09/2026); 4K balanced FSR 45% quality 50–60 FPS with occasional stutter (cubehacker8107, 08/09/2026) [confirmed: @dejan_994, 07/09/2026] |
| The Blood of the Dawnwalker (1.0.4–1.0.5) | 60 FPS locked | 1080p High FSR Quality, 40 CU 8c 1500/3500 MHz, dynamic UMA 512 MB, CachyOS RC + Proton 11, zswap active — 60 locked with dips (lovelifetrustfaith, 10/09/2026); 1750/3700 MHz + undervolt smoother but stutter in towns persists; GPU throttling 80 °C, barely 75 °C (12/09/2026) [confirmed: @lovelifetrustfaith, 10/09/2026] |
| Bodycam | 40–55 FPS | With ini tweaks (settings + 2 .ini edits): consistent 40 FPS, 50–55 at 60 cap, 60+ some instances — smooth after tweaks; without: 25–30 FPS with stuttering (zerosumpr, 06/09/2026) [confirmed: @zerosumpr, 06/09/2026] |
| Dead Space Remastered | Stutters 5–10s | Runs but significant stutters/freezes 5–10s while moving, all resolutions 1080p–4K; shadows/post/global illumination to low helps (cubehacker8107, 03/09/2026); ~65–70 °C (05/09/2026) [confirmed: @cubehacker8107, 03/09/2026] |
| Control Resonant (Remedy) | 1080p FSR Quality, runs well | 40 CU, 8c @ 3.5 GHz, GPU 2000 MHz; scene comparison: fallback FSR3 ~94 FPS vs experimental mesh driver ~84 FPS — mesh path only helps games requiring native mesh/task shaders (nonu0038, 24/09/2026) [confirmed: @nonu0038, 24/09/2026]; another user runs it out of the box at 1080p FSR Quality (mahmudnaqi, 25/09/2026); one report of crash right after the Remedy logo on a fresh CachyOS 8c/40CU install (methisfaction, 25/09/2026); **XeMFG frame-gen:** 2k, FSR4 Performance, everything Ultra / RT Medium — "60 FPS x3, 80 FPS x4" (dmoraza, 25/09/2026) [confirmed: @dmoraza, 25/09/2026] |
| A Plague Tale: Requiem | ~75 FPS FSR4 Quality | dmooney65, 13/09/2026 [confirmed: @dmooney65, 13/09/2026] |

### S.T.A.L.K.E.R. 2 (May 2026)

| Config | FPS | Notes |
|--------|-----|-------|
| Stock 24 CU, 2000 MHz | ~55 (drops to high 40s) | Area after opening cinematic |
| Stock + FSR frame gen | High 90s | |
| 36 CU, 2000 MHz | Mostly 60 (drops to high 50s) | |
| 36 CU + FSR frame gen | 110-120 | |

### Subnautica 2 (May 2026)

Runs on CachyOS with Proton Experimental, 40 CU, lower settings (biohazardv2.0).

---

### Cities: Skylines 2 (200k population)
**20–30 FPS** — CPU limited (simulation-heavy).

---

## Emulation

| System / Game | FPS | Notes |
|---------------|-----|-------|
| Ryujinx (Switch) — TOTK | 20 FPS consistent | Appears to be board limitation (elektricM docs) |
| Eden (Switch) — TOTK, 36 CU + 8 core | ~35 FPS @ 4K (Kakariko Village) | With NX Optimizer applied [confirmed: @mitchthepreacher, 18/08/2026] — "miles more playable than my Legion Go" |
| Eden (Switch) — general | 4K 60 in most titles | Switch emulation is CPU-bound; render high since CPU limits anyway (@loris_kujo, @jackjt8, Aug 2026); Xenoblade-class games are the exception |
| Ratchet & Clank (RPCS3) | 45–60 | Playable | [confirmed: @whomstdv, 25/11/2025]
| Breath of the Wild (Cemu) | Works | With 8 cores at stock clocks: ~50 FPS in open-field combat, dips to 40; dungeons smooth 60 [confirmed: @loris_kujo, 18/08/2026] |
| Xenia (Xbox 360) | Does not work — freezes system | |
| PCSX2 (PS2) | Excellent | elektricM docs |
| Dolphin (GameCube/Wii) | Excellent | elektricM docs |
| RPCS3 (PS3) | Good for lighter titles | elektricM docs |

---

## Newly Tested Games (Late May 2026)

| Game | Performance | Notes |
|------|-------------|-------|
| Hitman 2 (40 CU, 1500 MHz) | 160 FPS vs 120 FPS stock | 1.33x CU scaling (itsanarse) |
| Fatal Frame 2 (40 CU) | 60 FPS at 1400-1500 MHz | 24 CU needed 1850-2000 MHz for same -- lower temps/power (maskofsin) |
| MGS3 Delta (40 CU) | 66% FPS boost over 24 CU | big_trov |
| Returnal | Heavy artifacts on marginal 40 CU boards | Good test game for CU health (capt.cat_13) |
| New Batman (2026) | Runs, GPU bound | 40 CU (codyrainy) |

---

## Games That Don't Work

| Game | Reason | Source |
|------|--------|--------|
| Fortnite | Easy Anti-Cheat on Linux -- cannot run | elektricM docs |
| Final Fantasy VII Rebirth | "DX12 is not supported on your system" -- game checks for specific GPU compatibility, no fix for BC-250 yet | elektricM docs |
| Spider-Man 2 | Out-of-memory crash with 512MB VRAM. Fixes (help-thread): set 6GB static VRAM in BIOS (_nk10), add TTM kernel params (hojnikb), run 32GB swap script from NexGen3D repo, lower in-game settings (zerosumpr), or add DXVK config overrides (newgbaxl) |
| Expedition 33 (Clair Obscur) | Crashes with 512 MB VRAM -- use 6 GB static allocation or `RADV_DEBUG=nohiz` | Community report | [confirmed: @fforduck, 12/05/2026]
| Expedition 33 (Clair Obscur) — 40 CU | 35 → 60 FPS | "40cu boosted my expedition 33 35 fps to 60" [confirmed: @josuee34, 14/08/2026] |
| Palia | Crashes without workaround (swap may help) (dillydilly_91, 23/02/2026) | Community report |

**EAC / Epic note (Oct 2026):** Epic Games shipped a **native-Linux launcher preview** with upgraded EAC (GamingOnLinux, 14/10/2026 — u/A7XFAN1998, reddit); Fortnite for Linux was announced alongside. However the launcher preview requires **Secure Boot + TPM 2.0 + IOMMU**, which the BC-250's platform does not provide in a stock BIOS — treat "Fortnite soon on BC-250" as an (open question), not a working path (u/Jakdaw1, 14/10/2026, reddit).

---

## Launch Options & Tweaks (Quick Reference)

| Game / Fix | Launch Option | Source |
|------------|---------------|--------|
| Fix artifacts (general, Mesa 25.1+) | `RADV_DEBUG=nohiz %command%` | elektricM docs |
| FPS overlay (any game) | `mangohud %command%` | elektricM docs |
| CPU optimization | `gamemoderun %command%` | elektricM docs |
| Combined (Mesa 25.1+) | `RADV_DEBUG=nohiz mangohud gamemoderun %command%` | elektricM docs |
| Fix compute queue (Mesa < 25.1) | `RADV_DEBUG=nocompute %command%` | elektricM docs |
| Combined with debug (Mesa < 25.1) | `RADV_DEBUG=nohiz DXVK_HUD=fps,gpu MANGOHUD=1 %command%` | elektricM docs |
| Force Vulkan driver | `VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/radeon_icd.x86_64.json %command%` | elektricM docs |
| Steam Deck compat (Fallout 4, Skyrim SE) | `SteamDeck=0 %command%` | Community |
| FSR4 upgrade for FSR3 | `FSR4_UPGRADE=1 %command%` | Community |
| VRS crash fix (Doom TDA) | Use [Vulkan_NullVRS](https://github.com/bangstk/Vulkan_NullVRS) layer (bangstk) | bangstk, May 2026 |
| CPU performance boost | `mitigations=off` (kernel param) | elektricM docs |
| Larger shader cache | `__GL_SHADER_DISK_CACHE_SIZE=10737418240` in `/etc/environment` | elektricM docs |

### Environment Variables (Add to `/etc/environment`)

```bash
VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/radeon_icd.x86_64.json:/usr/share/vulkan/icd.d/radeon_icd.i686.json
RADV_DEBUG=nohiz
__GL_SHADER_DISK_CACHE_SIZE=10737418240
```

---

## Performance Optimization Tips

1. **1080p is the sweet spot** — 1440p works with FSR, 4K only for older titles (elektricM docs)
2. **CPU is the main bottleneck** in most modern games (GDDR6 shared memory latency) [confirmed: @corbanitevevo, 08/12/2025]
3. **VRAM: 4 GB for most games, 6 GB for demanding AAA titles** (elektricM docs: 4 GB recommended; 6 GB from community)
4. **Use FSR** for free performance boost (elektricM docs)
5. **Update to Mesa 26.x+** for best compatibility and performance (elektricM docs)
6. **Try Proton-GE** for better compatibility (elektricM docs)
7. **Kernel 6.19.x** for VRR and DP audio fixes (gennro); 6.18 LTS as stable fallback
8. **Mesa 26.x recommended** — significant RT and performance improvements; 25.1+ minimum
9. **`mitigations=off`** gives ~10–15% FPS boost in CPU-bound games (elektricM docs: "mitigations=off for +10-15% FPS")
10. **Keep GPU under 85C** for long-term stability (elektricM docs)
11. **Disable Handheld Daemon** if using Bazzite for gaming (elektricM docs):
    ```bash
    sudo systemctl disable --now hhd && sudo systemctl mask hhd
    ```
12. **CachyOS may be ~5–10% faster** than Bazzite in raw benchmarks [confirmed: @.captainwasabi, 23/05/2026]
13. **40 CU unlock: more CUs at lower clocks** match higher clocks at stock 24 CU — cooler and less power (big_trov: 40 CU at 1200 MHz = 60 FPS at 73C, 30W less than 24 CU at 2000 MHz achieving same FPS). See [02-BIOS](02-bios-and-firmware.md).

---

## 40 CU Unlock — Gaming Benchmarks

Community-tested by big_trov and essdee4336 (May 2026). All runs with P12 Pro fan, opened mid fins, PTM7950, 80mm back fan unless noted.

### Furmark (Vulkan, 1080p)

| Config | FPS | Temp | Power | User |
|--------|-----|------|-------|------|
| 24 CU, 2000 MHz stock | 57 | 77C | — | big_trov |
| 40 CU, 2000 MHz | 91 | 90C | — | big_trov |
| 40 CU, 1850 MHz / 910 mV | 137 | 71C | — | essdee4336 |
| 40 CU, 2000 MHz / 950 mV | 145 | 75C | — | essdee4336 |
| 40 CU, 2150 MHz / 990 mV | 153 | 79C | ~200W | essdee4336 |
| 40 CU, 2200 MHz | — | 98C (instant) | — | big_trov |
| 40 CU, 2230 MHz / 1050 mV | — | — | — | mrfrakes |
| 40 CU, 2300 MHz | 150 | 85C | ~288W | big_trov |
| 40 CU, 1850 MHz / 960 mV (2x 120mm fans) | — | — | — | soulygenius |
| 40 CU, 2000 MHz / 1000 mV (SMU_OC 78C tctl) | — | — | — | stevounit |
| 40 CU, 2300 MHz / 4100 MHz CPU | — | — | — | adixd90 |
| 40 CU, 1920 MHz / 960 mV (MX-7, triple fan) | — | throttled | — | linepanda (May 2026) |
| **38/40 CU, 1900 MHz** | **130** | **84C** | **336W wall** | **pijuli.** |
| **24/40 CU, 2130 MHz (same board)** | **95** | **84C** | **320W wall** | **pijuli.** |
| 38 CU, 2100 MHz / 920 mV — **FurMark score 8000+** | — | — | — | shibly_91236, 17/08/2026 (score metric, not FPS) |

pijuli. tested a 38/40 CU board (2 harvested in SE1 SH0). At 1900 MHz with 38 CUs: 130 FPS, 84C, 336W from wall. Same board at 24 CU/2130 MHz: 95 FPS, 84C, 320W. **35% FPS increase** at equivalent temps with only 16W more from wall. Cooling: P12 Max, middle fins removed, PTM7950, new thermal pads, no cage/no back fan.

**Sep 2026 Furmark updates:** 40 CU @ 2300 MHz on AIO 280 mm MSI MEG CoreLiquid S280 (adixd90, 02–03/09/2026); 38 CU @ 2100 MHz 930 mV PTM7950 single Foxconn 120 mm @100% — "Hell loud at 100%, I usually run fan at 67% while gaming" (shibly_91236, 04/09/2026); 2230 MHz @ 960 mV P12 Pro 100% PTM7950 (antmagl, 03/09/2026); 40 CU 8c @ 2000 MHz 960 mV Bazzite stock pads single P12 centre fins open (dbkretro, 06/09/2026); **score 8300 @ 38 CU 2100 MHz temp 82 °C** (shibly_91236, 06/09/2026) [confirmed: @shibly_91236, 06/09/2026]; 40 CU @ 2000 MHz 8c @ 3500 MHz "good silicon" (alchemy07011976, 06/09/2026); 2230 MHz @ 1050 mV / 4000 MHz @ 1275 mV (meme_meme, 07/09/2026); 3.9 GHz @ 1150 mV (940 mV stable) 75 °C OCCT, <70 °C gaming (shibly_91236, 07/09/2026); **8500+ @ 38 CU 2200 MHz** (shibly_91236, 09/09/2026); power cable 95 °C warning on second board 38 CU only (expand, 10/09/2026).

### Superposition (40 CU @ 2200 MHz)

| Preset | Score | GPU Clock | CPU Clock | Notes | User |
|--------|-------|-----------|-----------|-------|------|
| Medium | 13507 | 2200 MHz | stock | — | big_trov |
| High | 12491 | 2200 MHz | stock | — | big_trov |
| Medium (4 GHz CPU) | 14004 | 2200 MHz | 4000 MHz | Meager boost from CPU OC | big_trov |
| Extreme (2300 MHz) | 5759 | 2300 MHz | 3500 MHz UV | ~250W at wall | big_trov |
| Extreme (2230 MHz) | — | 2230 MHz | — | 24CU was 235W at 2230 | big_trov |
| Extreme (2100 MHz) | — | 2100 MHz | 4000 MHz | 1020 mV, 40CU | codyrainy |

---

## New Benchmark Data (Sep 26 – Oct 9 2026)

| Game | Config | Result | Source |
|------|--------|--------|--------|
| Star Wars Galactic Racer | 2100 MHz GPU, 40 CU, 8c @ 3.9 GHz | 1440p Medium: "mostly locked 60fps with minor dips into the mid 50's"; 1800p High + FSR Perf ≈ same; 4K High = 30 fps lock | (_wesk, 06/10/2026, benchmarks/Star wars galactic racer:11) [confirmed: @_wesk, 06/10/2026] |
| The Witcher 3: Wild Hunt Remastered | see note | RT Ultra preset + FSR4 Quality, dynamic scaling off: "Rarely goes below 60fps in 1080p… FSR4 mod helps a lot with RT. Looks better than native too" (dmooney65, 30/09/2026) [confirmed: @dmooney65, 30/09/2026]. Reference rig from the thread's benchmark video: 36 CU 2 GHz @ 960 mV, 8c 3.8 GHz @ 1170 mV, stock heatsink + Arctic P12 Pro with PTM7950, Mean Well 280 W brick | (benchmarks/Witcher III:35; config chat:12739-12745, 30/09/2026) |
| Clair Obscur: Expedition 33 | 40 CU 1850 MHz, 8c @ 3.85 GHz | FSR4 High 1080p, no frame-gen: 68–75 fps; battle minimum 56 fps ("Oh just tested in battle now the lowest it dropped to is 56fps"); another user sees battle drops into the 40s with heavy effects | (mavcom + zerosumpr, 27/09/2026, benchmarks/Clair Obscur:8-24) [confirmed: @mavcom, 27/09/2026] |
| NTE: Neverness to Everness | High preset, FSR3 Quality | 1080p: 50–55 fps DX11; 40–50 fps DX12 with stutters | (shanty_339, 01/10/2026, benchmarks/NTE:18) [confirmed: @shanty_339, 01/10/2026] |
| Arc Raiders | 4K, mix High/Medium + FSR | "With a bit of tweaking I got the game running at 4k 60. Some small drops" | (cubehacker8107, 05/10/2026, benchmarks/Arc Raiders:8) [confirmed: @cubehacker8107, 05/10/2026] |
| Furmark (Vulkan, 1080p) | 40 CU | 139 fps @ 1850 MHz; 151 fps @ 2150 MHz (2150 @ 1030 mV); "3.8cpu with 1850-2000gpu, games fine anyway… the sweet spot for my board" | (vvaaron, 28/09/2026, benchmarks/Furmark:10-34) [confirmed: @vvaaron, 28/09/2026] |

### Cross-OS FPS shootout: Bazzite vs CachyOS vs SteamOS vs Steam Machine (u/HTWingNut, 08/10/2026, reddit — score 72)

7 games at 1080p, no frame-gen, no upscaling, no RT (AC Black Flag Resynced Low, Black Myth Wukong Medium, Cyberpunk High, Doom The Dark Ages High, Forza Horizon 6 High, Gears of War E-Day Medium, Horizon Zero Dawn "Original"), same board: **40 CU @ 2000 MHz, 6c/12t @ 3900 MHz**, open air with Jiushark JF13K (rarely exceeds 55 °C). Verdict with per-run avg/1%-low charts: "There are no clear winners here, really" — **CachyOS** (kernel 7.2.9) most stable with better 1% lows and "generally felt better"; **SteamOS 3.8.28** "performed well, but surprisingly was not very stable" on BC-250; **Bazzite 44** "was good"; the stock **Steam Machine on Windows 11 26H2** "performed remarkably well despite using aged drivers from Valve". HTWingNut (multi-board owner, 8-core unstable on this unit) ranks real-world gains: **"CU's -> GPU Clock -> CPU cores"** — CU unlock pays off first. Commenters note SteamOS stable still uses the older kernel while the beta channel (3.9/3.10) carries 7.2-class fixes (u/hhnnngg, u/rufiohProbably, 08/10/2026) — see [05 → SteamOS Versions](05-os-installation.md#steamos-versions-on-bc-250). (FPS chart values live in the thread images; only conclusions summarized here.)

---

## Superposition Leaderboard (Extreme, 1080p)

### 24 CU (Stock, Unharvest Disabled)

| Rank | User | Score | GPU Clock | CPU Clock | mV | Date |
|------|------|-------|-----------|-----------|-----|------|
| 1 | nexgen3d | 4713 | 2530 MHz | 4175 MHz | 1165 | Jan 2026 |
| 2 | nexgen3d | 4690 | 2530 MHz | 4150 MHz | 1150 | Jan 2026 |
| 3 | nexgen3d | 4668 | 2500 MHz | — | — | Jan 2026 |
| 4 | nexgen3d | 4576 | 2400 MHz | 3850 MHz | — | Mar 2026 |
| 5 | nexgen3d | 4329 | — | — | — | Jan 2026 |
| 6 | nexgen3d | 4317 | — | — | — | Dec 2025 |
| 7 | nexgen3d | 4280 | — | — | — | Dec 2025 |
| 8 | big_trov | ~4200 | 2200 MHz | stock | — | Feb 2026 |
| 9 | big_trov | 3975 | 2000 MHz | 3500 MHz | — | Apr 2026 |
| 10 | .captainwasabi | ~3700 | — | — | — | May 2026 |

nexgen3d runs liquid cooling (MSI AIO), CachyOS, SMU governor. 24 CU community target is 5000 (uncracked).

### 40 CU (Unharvest Enabled)

| Rank | User | Score | GPU Clock | CPU Clock | mV | Notes | Date |
|------|------|-------|-----------|-----------|-----|-------|------|
| 1 | nhoj0176 | **5865** | 2350 MHz | 2500 MHz | 1000 (GPU) | 40 CU, Linux/CachyOS; confirmed as the record in-thread by big_trov: "I think Nonu has the record, and it was still on the Linux version… 5865… He says 2350" (07/10/2026) [confirmed: @big_trov, 07/10/2026] | Oct 2026 |
| 2 | gennro | ~5900 | — | — | — | — | May 2026. ⚠️ Disputed: big_trov's in-thread record checks (Aug 12 + Oct 07) both put the record at "5800 something", not ~5900 — treat this row as unverified (need confirmation) | May 2026 |
| 3 | big_trov | 5759 | 2300 MHz | 3500 MHz UV | — | — | May 2026 |
| 4 | codyrainy | ~5400 | 2100 MHz | 4000 MHz | 1020 | 40 CU | May 2026 |
| 5 | cralant | ~5400 | 2150 MHz | 3800 MHz -15 | 1035 | 40 CU | May 2026 |
| 6 | pm_me_kitsunemimi | 5320 | 2250 MHz | 4000 MHz | — | 36 CU, 8 cores, Bazzite, OpenGL; "76 max iirc" | Aug 2026 |
| 7 | dznuts | 5300 | 2270 MHz | 4000 MHz | — | 38 CU | May 2026 |
| 8 | dznuts | 5300 | 2200 MHz | — | 1060 | 38 CU, CachyOS | May 2026 |
| 9 | mitchthepreacher | 5150 | — | — | — | Redux case; "Temps are 75 but its a jet engine" | Aug 2026 |
| 10 | land_and_air | — | 2000 MHz | stock | — | — | May 2026 |

40 CU Extreme already surpasses the 24 CU record (4713) by 22%+ at lower clocks (2300 vs 2530 MHz). Theoretically should reach ~6500+ at equivalent clocks. More scores expected as community adopts the unlock. Post your results in the Discord `#benchmarks` channel.

**Aug 2026 updates:** big_trov confirmed the current record is "5800 or so" (Aug 12 2026). pm_me_kitsunemimi hit 5320 @ 2250 MHz GPU / 4 GHz CPU on Bazzite with 8 cores unlocked — "Not sure what the average score is but 5320 is good" (rocksalt_, Aug 12 2026), max temps "76 max iirc". mitchthepreacher reached 5150 after a CachyOS update with no unlock/OC changes, in a Redux case, "Temps are 75 but its a jet engine" (Aug 13 2026).

**Sep 2026 updates:** vvaaron averaging ~4900 at 2300 MHz GPU / 4.0 GHz CPU on full 40 CU + 8 cores, Bazzite (08/09/2026); expected score at 2300 MHz is ~5700 — "plenty of people cant get much past 2200 MHz" and VRMs shut off with reset button dead (big_trov, 08/09/2026) [confirmed: @vvaaron, 08/09/2026]. dbkretro 40 CU 8c @ 2000 MHz 960 mV Bazzite stock clocks/paste (06/09/2026); .lordantares 2230 MHz @ 1030 mV on Mesa 26.2 / CachyOS 7.2.2 (06–07/09/2026), noting 2300 MHz artifacts unless fans 100% and >70 °C triggers black screen [confirmed: @.lordantares, 07/09/2026]. nhoj0176 record **2350 MHz @ 1000 mV** (2500 MHz CPU @ 800 mV) — temps 66 °C at 2100 MHz, 60 °C at 1900 MHz in Superposition; Bykski Icedragon fan, PTM7950 die + thermal putty front, 2.0 mm pads on VRAM (12–13/09/2026) [confirmed: @nhoj0176, 12/09/2026].

**38 CU = 36 CU (Aug 12 2026):** a "38 CU" config is effectively 36 CU — the Shader Engines (SE0/SE1) must have symmetric WGP counts. fforduck: "You have 36 unlocked 😉 SE0 and SE01 need the same amount. If you have disabled one in SE0 it will automatically disable one in SE1" — and per hashtagoctothorp, disabling another WGP in SE1 gives the *same* score. The only meaningful CU counts are 24/28/32/36/40 (counting full pairs); the dznuts "38 CU" runs above are the same silicon configuration as 36 CU. Confirmed again in-thread (dreamtheduk/jackjt8, 04/10/2026): with 38 enabled "the 37th and 38th dont contribute work… but they do use power".

**Oct 2026 updates:**
- **Record 5865 confirmed** by big_trov in `#benchmarks` (07/10/2026, config above). .lordantares posted a 2350 MHz run on 05/10 that did not beat it ("Not even close… The record is above 5800" — .lordantares, 07/10/2026); zerosumpr at the same clock "got almost 100pts less" — hojnikb: "you gotta optimize cpu and gddr clocks/latencies" (07/10/2026). The community target is now "reaching that 6000 milestone on superposition 1080p extreme" (vvaaron, 05/10/2026).
- **PTM7950 lift:** dominic61 measured "My Superposition benchmark also went up by almost 10%" after PTM7950 repaste (with idle 48.6 → 44 °C, CPU capped at 81 °C) (04/10/2026) [confirmed: @dominic61, 04/10/2026] — thermal headroom converts directly into sustained clocks (see [04](04-cooling-guide.md)).
- **Geekbench 6 Vulkan (40 CU):** 1900 → 2000 MHz lifted one board from 88,000 to 93,000; 95,000 peak reported same week (halil_iboo, 26/09/2026) [confirmed: @halil_iboo, 26/09/2026].

**Max clock findings:** 2400 MHz at 40 CU causes hard OCP lockup requiring power cable pull (reset/power buttons unresponsive) across multiple boards (big_trov, codyrainy, cralant). 2100-2300 MHz is the stable range for most boards. Trimming CUs for higher clocks is not advantageous: big_trov's 32CU @ 2400 MHz scored worse than 40CU @ 2300 MHz, with similar power draw (~270W).

**38 CU voltage findings (May 2026):** 38 CU at 2200 MHz requires ~1050-1060 mV (dznuts). 1085 mV not enough for 2230 MHz with 38 CU. At 2200 MHz, 995 mV is stable for some boards (codyrainy). Power limit and voltage ceiling intersect at ~2200 MHz for most boards, creating a hard stability ceiling.

**Memory OC (May 2026):** dznuts tested memory OC at 1975 MHz CL26 using RobinMemTiming. Only +80 points in Superposition and +1 FPS in Cyberpunk — not worth the instability risk. Memory OC causes 1-in-20 boot failures (no POST).

### Gaming (40 CU)

| Game | Config | FPS | User |
|------|--------|-----|------|
| Furmark VK 1080p | 1200 MHz | 60 FPS at 73C | big_trov |
| Furmark VK 1440p | 2000 MHz | 91 FPS at 90C | big_trov |
| Doom TDA | 1440p, 40 CU | Same FPS as 1080p before unlock | Community report |
| **007 First Light** | **1440p Medium + FSR** | **72 FPS** | **big_trov, paul_lionking (May 2026)** |
| **007 First Light** | **1440p Medium no FSR** | **48 FPS** | **big_trov (May 2026)** |
| **007 First Light** | **1080p High no FSR** | **60 FPS locked** | **paul_lionking (May 2026)** |
| Forza Horizon 6 | 3840x1600 | ~60 FPS | paul_lionking (May 2026) |
| Forza Horizon 6 | 1080p Ultra, 40 CU | ~60 FPS | Community report |
| **Monster Hunter Wilds** | **1080p Medium + FSR Frame Gen** | **50-60 FPS** | **irontsuki (Jun 2026)** |
| **Death Stranding 2** | **High settings** | **40-60 FPS** | **gaboggamer (Jun 2026)** |
| **Death Stranding 2** | **3440x1440 Medium-High + PICO + FSR FG** | **60 FPS** | **dartzon (Jun 2026)** |
| **Counter-Strike 2** | **1440p High, 40CU @ 2GHz** | **<100 FPS, stutter** | **weabchan (Jun 2026)** |
| **Arc Raiders** | **1080p Medium no FSR, 40CU @ 2GHz** | **~65 FPS** | **marine1067 (Jun 2026)** |
| **Shadow of the Tomb Raider** | **1080p Highest, 40CU @ 2GHz** | **90 FPS avg** | **bytepond (Jun 2026)** |
| **Shadow of the Tomb Raider** | **4K Highest + CAS (50% scale)** | **~63 FPS** | **bytepond (Jun 2026)** |
| **FF7 Remake** | **1080p High** | **80-90 FPS** | **nataliezaki (Jun 2026)** |
| **FF7 Remake** | **1440p, 120 FPS cap** | **Solid, rare stutter to 50** | **zerosumpr (Jun 2026)** |
| Helldivers 2 | 40 CU, 2350 MHz | Stable | Community report |
| RE4 Remake (2023) | 40 CU, 1750 MHz | ~60 FPS stable (dbkretro, Aug 9 2026 — Bazzite + governor + 8-core/40 CU unlock). |

> **Efficiency insight (big_trov):** More CUs at lower clocks match the performance of fewer CUs at higher clocks, at lower temperature and power. 40 CU @ 1200 MHz = 60 FPS (73C, 30W less than 24 CU @ 2000 MHz achieving same FPS).
> **OCP hard lockup (big_trov, codyrainy, cralant):** 2400 MHz at 40 CU causes hard lockup where reset and power buttons do nothing -- requires pulling power cable. Likely Over Current Protection triggering. Consistent across multiple boards regardless of cooling. One user with AIO reported 2400 MHz stable at 1120 mV.
> **CPU OC affects GPU stability (big_trov, hojnikb):** Increasing CPU from 3500 to 4000 MHz lowered the GPU voltage threshold for hard lockup. Total system power draw matters -- undervolt CPU when pushing GPU limits.
> **Game-specific instability (May 2026):** RE4 Remake crashes even with stable stress tests (nataliezaki, May 21 2026). Games need more voltage on GPU than synthetic benchmarks to be stable. If benchmarks pass but games crash, increase voltage by 10-15 mV.
> **Voltage wall at 40 CU (big_trov, May 2026):** Two limit curves govern 40 CU stability -- a voltage ceiling and a power limit. These curves intersect at approximately 2200 MHz, creating a hard stability ceiling. Above this point, diminishing returns are severe regardless of cooling. Power consumption: ~250W from wall during gaming, ~350W during Furmark at 40 CU (bytepond, May 2026).
> **Hard limit:** 2300 MHz at 40 CU = ~288W. Stay at or below 2200 MHz for safety with 40 CU.

---

## Games Mentioned in Community (Limited Data)

Games with verified community mentions but limited sample size — use with caution. Sources cross-checked against export scans (2025-11 to 2026-08). Games with fuller data live in the sections above; each game appears exactly once in this file.

| Game | Report | Notes |
|------|--------|-------|
| Lies of P | 90 FPS @ 1440p on high | |
| RoboCop: Rogue City | Picked up FPS after tweaks | |
| Overwatch | Drops to ~30 FPS on low with heavy effects | |
| Forza Horizon 4 | Suspected memory leak; VRAM never frees | |
| Resident Evil series incl. Requiem | 60 FPS no problems | "Every Resi game inc Requiem is 60fps no probs" [confirmed: @dbkretro, 18/08/2026] |
| Resident Evil 7 | Runs very well, everything high, ~64C | |
| Stardew Valley | Runs fine at 4K 60 FPS | |
| Hollow Knight | 4K playable (lighter game) | |
| Star Wars Battlefront II | 80-85 → 120-130 FPS after SMU governor + kernel patch (juancarlos24691, Aug 2025) | |
**Last verified: 2026-10-22**
