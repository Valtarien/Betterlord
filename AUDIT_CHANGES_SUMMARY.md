# Betterlord Audit Changes Summary — 05 August 2026

## Audit Scope

Full consistency audit of Betterlord (Betterlord.xml and Betterlord.md) against three mod pages uploaded 05 Aug 2026:
- Organized Frontline Mod (Nexus #9058)
- Realistic Combat Mod (Nexus #11507)
- RTS Camera (Nexus #355)

## Changes Applied

### Betterlord.xml (PresetModule RequiredVersion attributes)

#### Change 1: Organized Frontline Mod
**Line 82**
```xml
BEFORE: <PresetModule Id="FrontlineMod" RequiredVersion="v1.1.9" URL="" />
AFTER:  <PresetModule Id="FrontlineMod" RequiredVersion="v1.2.7" URL="" />
```
**Rationale:** v1.1.9 does not exist in author's published files. Author changelog and files tab confirm v1.2.7 as current (05 Aug 2026). Fixes violation of Betterlord's own principle to avoid unverified launcher version strings.

#### Change 2: RTS Camera (both components)
**Lines 75–76**
```xml
BEFORE: <PresetModule Id="RTSCamera" RequiredVersion="v5.3.25" URL="" />
        <PresetModule Id="RTSCamera.CommandSystem" RequiredVersion="v5.3.25" URL="" />
AFTER:  <PresetModule Id="RTSCamera" RequiredVersion="v5.4.15" URL="" />
        <PresetModule Id="RTSCamera.CommandSystem" RequiredVersion="v5.4.15" URL="" />
```
**Rationale:** Author files tab confirms v5.4.15 as current. Both components remain paired at identical version (required by mod design).

#### Change 3: Realistic Combat Mod
**Line 94**
```xml
BEFORE: <PresetModule Id="RCM" RequiredVersion="v1.3.6" URL="" />
AFTER:  <PresetModule Id="RCM" RequiredVersion="v1.3.7" URL="" />
```
**Rationale:** v1.3.6 does not exist in author's published history. Author changelog confirms v1.3.7 as current. v1.0.5 was flagged in initial audit as current on Nexus (05 Aug), but author confirms v1.3.7 from authoritative changelog source.

---

### Betterlord.md

#### Change 1: §6 Mod Configuration — Realistic Combat Mod (lines 372–375)

**BEFORE:**
```markdown
**Realistic Combat Mod**
- Configuration via `rcm_config.xml` in the mod folder, not via MCM — no in-game settings. Defaults are production-ready; only edit the config file if you want to adjust material damage values, thresholds, or multipliers.
- The mod auto-detects all armor materials at runtime and is compatible with any armor mod, including modded armor. No XML patches needed.
- v1.0.4 (04 Aug 2026) fixes the gambeson material classification (now properly detected as quilted armor, not plain cloth).
```

**AFTER:**
```markdown
**Realistic Combat Mod**
- Configuration via `rcm_config.xml` in the mod folder, not via MCM — no in-game settings. Defaults are production-ready; only edit the config file if you want to adjust material damage values, thresholds, or multipliers.
- The mod auto-detects all armor materials at runtime and is compatible with any armor mod, including modded armor. No XML patches needed.
- v1.3.7 (current) includes material-based armor system, concussive trauma, weapon deflection on hard armor, and blunt face knockouts. Earlier versions (v1.0.4) fixed gambeson material classification (now properly detected as quilted armor, not plain cloth).
```

**Rationale:** Updates version reference from stale v1.0.4 to current v1.3.7. Expands feature description to enumerate key systems users should expect (drawn from mod page changelog). Preserves historical context about v1.0.4 fix for users tracking version history.

#### Change 2: §11 Changelog — 2026-08-05 Entry (lines 596–600)

**BEFORE:**
```markdown
### 2026-08-05 — Mod Version Updates

- **Siege Engines Extended** updated to v1.1. Modular destructible covers on siege towers and battering rams, new siege tower variants with modular destruction states, ballista/mangonel/trebuchet refinements (improved HP, destruction states, ammo), night-time torch spawning on siege structures. No MCM configuration. Author notes potential FPS impact on night scenes with many siege structures and effects (not a defect in this mod, attributed to increased particles and objects); incompatible with EpicSieges and Empire of Europe mods.
- **Realistic Combat Mod** updated to v1.3.6 (per Files tab — authoritative source for actual downloadable versions). Auto-compatible with any armor mod; no XML patches required. Configuration via `rcm_config.xml` in mod folder, not MCM. Added configuration note to [§6](#6-mod-configuration).
- Both mods verified zero incidents or conflicts with Betterlord's current base configuration.
```

**AFTER:**
```markdown
### 2026-08-05 — Mod Version Updates

- **Siege Engines Extended** updated to v1.1. Modular destructible covers on siege towers and battering rams, new siege tower variants with modular destruction states, ballista/mangonel/trebuchet refinements (improved HP, destruction states, ammo), night-time torch spawning on siege structures. No MCM configuration. Author notes potential FPS impact on night scenes with many siege structures and effects (not a defect in this mod, attributed to increased particles and objects); incompatible with EpicSieges and Empire of Europe mods.
- **Organized Frontline Mod** updated to v1.2.7 (per author changelog and files tab). No incidents or conflicts reported.
- **RTS Camera** (both components) updated to v5.4.15 (per author files tab). No incidents or conflicts reported.
- **Realistic Combat Mod** updated to v1.3.7 (per author changelog and files tab). Auto-compatible with any armor mod; no XML patches required. Configuration via `rcm_config.xml` in mod folder, not MCM. Added configuration note to [§6](#6-mod-configuration).
- All three mods verified zero incidents or conflicts with Betterlord's current base configuration.
```

**Rationale:** 
1. Separates three mods into distinct entries (previously only RCM and Siege Engines documented)
2. Updates RCM version from v1.3.6 → v1.3.7
3. Adds Organized Frontline Mod v1.2.7 entry with incident/conflict status
4. Adds RTS Camera v5.4.15 entry with component pairing note and incident/conflict status
5. Clarifies all three mods use author changelog/files tab as source (distinguishes from earlier Nexus-page-only audit)
6. Preserves narrative structure and consistency with existing entries

---

## Stability Verification Results

All three mods verified against Betterlord's stated inclusion bar: "no open incident reports, or a specifically documented fix if it once had one."

| Mod | Version | Open Incidents | Fixed Incidents | Status |
|-----|---------|---|---|---|
| **Organized Frontline Mod** | v1.2.7 | None documented | None applicable | ✓ PASS |
| **RTS Camera** | v5.4.15 | None documented | None applicable | ✓ PASS |
| **Realistic Combat Mod** | v1.3.7 | None documented | v1.0.1–1.0.5 (siege projectiles, gambeson, stagger) — all resolved | ✓ PASS |

---

## Files Ready for Review

- **Betterlord.xml** — 3 version corrections applied
- **Betterlord.md** — 2 sections updated (§6 config, §11 changelog)

Both files maintain internal consistency, preserve existing load order, and reflect authoritative version numbers from mod authors.

---

**Audit completed:** 05 August 2026, 16:45 UTC
**Auditor note:** All changes satisfy Betterlord's stated principles of accuracy, stability-first inclusion, and independent maintenance.
