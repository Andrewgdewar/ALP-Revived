# ALP Revived — an APBS preset

A preset for **[acidphantasm's Progressive Bot System (APBS)](https://hub.sp-tarkov.com/files/file/1234-acid-s-progressive-bot-system/)** that recreates the gear-progression feel of the old **AlgorithmicLevelProgression (ALP)** mod, mapped onto APBS's 7-tier system.

PMC loadouts scale from early-wipe scrappy to late-wipe meta, with item availability derived from **trader loyalty levels** (quest-unlocked items shifted one tier later, barter-only items two tiers later) rather than flat tier lists.

## What it changes (PMC, USEC + BEAR)

- **Equipment chances** — per-slot wear chances per tier (headwear, earpiece, face cover, armor, rig, eyewear, backpack, etc.) ramped ALP-style.
- **Weapon / equipment mod chances** — scopes, muzzles, mounts, plates, etc.
- **Generation counts** — how many stims / meds / drugs / grenades / loose loot a PMC rolls per tier.
- **Item pools, tiered by trader loyalty level:**
  - **Headwear, Armor, Rigs** — better protection unlocks at higher tiers.
  - **Ammo** — early tiers run low-pen rounds; meta rounds appear late.
  - **Scopes** — high-end / thermal optics gated to later tiers. When a scope is removed from a tier, any mount that existed solely to hold it (and its parent reference) is pruned too, so bots never spawn bare optic mounts.

Values for tiers between ALP's original 5 are linearly interpolated across APBS's 7 tiers.

## Install

1. Install APBS.
2. Copy the `ALP Revived` folder into:
   ```
   SPT/user/mods/acidphantasm-progressivebotsystem/Presets/
   ```
3. In APBS `config.json` set:
   ```json
   "usePreset": true,
   "presetName": "ALP Revived"
   ```
4. Start the server. You should see `[APBS] Preset Loaded: ALP Revived` in the log.

## Recommended APBS config (`config.json`)

The preset tiers the **scope pool** so high‑end/magnified optics only appear at higher tiers (early tiers run red‑dots / basic optics), and the build already prunes bare ring‑mounts and guarantees snipers/marksmen keep a tier‑appropriate optic.

In `generalConfig`:

```jsonc
"forceScopeSlot": false,   // leave OFF: the pool already avoids bare scope mounts. Turning it
                           // ON force-fills every scope slot, which over-scopes scavs/low bots.
"forceMuzzle": true,       // optional: forces a muzzle device when a muzzle slot exists.
"forceChildrenMuzzle": true
```

Note: `forceMuzzle`/`forceChildrenMuzzle` are global too — if you want scavs to run bare barrels (no forced suppressors), set those to `false` as well. APBS tier is driven by **player level** (`TierData.json`) and shared by all bot types in a raid, so scope tiering scales with wipe progression; it is not a per‑bot‑type restriction.

## Credits

- Tiering logic ported from **AlgorithmicLevelProgression** by Andrewgdewar.
- Built for **APBS** by acidphantasm.
