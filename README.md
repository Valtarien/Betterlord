# Betterlord

A curated Mount & Blade II: Bannerlord modlist by Valtarien (ACE). **Version 1.4.7.1.0**

## Specifications

- **Game:** Bannerlord v1.4.7 (build 117484)
- **DLC:** War Sails 1.2.7
- **Launcher:** Novus Bannerlord Launcher
- **Content:** 112 third-party mods + 7 official modules
- **Modes:** Sandbox (default) and Campaign share the same module list (4 MCM settings differ)

## Philosophy

Stability first. A mod earns inclusion by clearing one bar: no open incident reports, or a specifically documented fix if it once had one. Popularity and feature richness don't override this. The result plays like Bannerlord — no total overhauls, fantasy content, OP trees, or systems carried forward on feature strength alone.

## Maintenance

Betterlord began as a stability-focused fork of Valorlord and is maintained independently from here forward. Each decision — incident history, module choices, audits — stands on its own terms.

---

## Contents

1. [Before you start](#1-before-you-start)
2. [Game client settings](#2-game-client-settings)
3. [Launcher](#3-launcher)
4. [Installing the mods](#4-installing-the-mods)
5. [Load order](#5-load-order)
6. [Mod configuration](#6-mod-configuration)
7. [Starting a new game](#7-starting-a-new-game)
8. [Design philosophy and scope](#8-design-philosophy-and-scope)
9. [Known issues](#9-known-issues)
10. [Maintaining the list](#10-maintaining-the-list)
11. [Changelog](#11-changelog)

---

## 1. Before you start

**You need a clean 1.4.7 install** — not 1.4.6 or earlier. Verify the build number in the bottom corner of the main menu.

Update your graphics drivers, then delete these two directories:

```
%USERPROFILE%\Documents\Mount and Blade II Bannerlord
C:\ProgramData\Mount and Blade II Bannerlord
```

The first holds saves, mod settings and logs; the second holds compiled shaders. Both regenerate on next launch. **Back up any saves you want to keep first** — they will not be compatible with this list anyway.

**Launch the game once with the official launcher** before installing anything, to recreate the configuration files the list depends on.

**Extract every mod with [7-Zip](https://www.7-zip.org/).** Windows' built-in extractor can leave DLLs blocked, failing to load silently. If you already extracted with something else, right-click each DLL → Properties → Unblock.

Mods install to:

```
...\Mount & Blade II Bannerlord\Modules\<ModuleName>
```

Each archive contains one folder that goes directly there.

### A note on updates

Mod versions move constantly, so rather than pin them here — wrong within a week — the approach is:

- Track every mod on its source page so you get update notifications
- Read changelogs before applying updates; a "fix" in one mod is often a behaviour change that collides with another
- Update in small batches and verify with [Harmony Patch Scanner](https://www.nexusmods.com/mountandblade2bannerlord/mods/9179) before committing to a campaign
- Prefer the version shown on a mod's own Nexus page or Files tab over any other source — tracking-centre feeds and launcher-reported required versions are both known to lag or misreport

The core libraries are worth pinning here, because everything depends on them and mismatches are silent:

| Library | Known-good |
|---|---|
| Harmony | 2.4.2.225 |
| ButterLib | 2.10.4 |
| UIExtenderEx | 2.13.2 |
| Mod Configuration Menu | 5.12.0 |

Some mods list a required MCM version that does not exist on the download page — authors sometimes quote the NuGet package number, which runs slightly ahead. Install the newest published release and ignore the discrepancy.

**Flagged for verification (04 Aug 2026 audit):** the upstream guide this list originated from currently displays ButterLib at 2.11.0 and MCM at 5.12.1 — both a small step ahead of the versions pinned in `Betterlord.xml` (2.10.4 and 5.11.4). Per the project's own standing caution above, a displayed version isn't confirmation of what you should install — check each library's own Files tab before updating, and update in isolation with a scan before and after, since these two sit underneath everything else in the list.

---

## 2. Game client settings

These prevent engine-level crashes in a heavily modded install. Set them before installing anything.

**Video**
- Disable **Force VSync in Menus**
- Frame Limiter → **89**

**Performance**
- Shader Quality → **Medium** — higher settings can produce stretched textures with exported shaders
- Number Of Corpses → **High (125)** — **never Unlimited**, this reliably causes battle crashes
- Number Of Ragdolls → **10**
- Disable **Motion Blur**
- Sound Channels → **Medium (256)**

**NVIDIA Control Panel → Manage 3D Settings → Program Settings → `bannerlord.exe`**
- Low Latency Mode → **Ultra**
- Max Frame Rate → **90**
- Power management mode → **Prefer maximum performance**
- Vertical sync → **Off**

---

## 3. Launcher

Betterlord uses [Novus Bannerlord Launcher](https://www.nexusmods.com/mountandblade2bannerlord/mods/4924), which supports saved presets and named divider entries. The dividers (`divCore`, `divUtil`, and so on) are cosmetic grouping entries — they load nothing, they just make the list navigable.

**Do not use Vortex.** Beyond general reliability problems, it has a documented history of writing a module string the engine resolves differently, producing bizarre symptoms. If something looks wrong, verify that the launcher's module string matches your intended order before suspecting a mod.

**Do not use Steam Workshop mods** alongside this list. Automatic updates mean changes land without you reading the changelog.

---

## 4. Installing the mods

Work down the table in [§5](#5-load-order) in order. For each entry:

1. Download the archive from the linked page
2. Extract with 7-Zip into `Modules\`
3. Confirm the extracted folder name matches the **Module ID** column

Some mods ship multiple builds on their download page — pick the one for game version 1.4.7. Where a mod offers an MCM and a non-MCM variant, take the MCM variant.

Enable everything in Novus in the order shown, save the preset, then launch once and check the log at:

```
C:\ProgramData\Mount and Blade II Bannerlord\logs\rgl_log_<pid>.txt
```

Search for `Assembly load result`. Every entry should read `SUCCESS`. Anything else means a blocked DLL, a missing dependency, or a mod built for the wrong game version.

**Stealth Flag Fix** is not a standalone mod. It is a file hosted on the Files tab of the Nexus page linked in the load-order table below (originally posted alongside an unrelated modding-notes guide; the file itself has no dependency on that guide).

**Dynamic Looks Change** — the link points to the `1.3.X` build. An earlier, separate mod of the same name also exists and uses the same module folder; take the linked one.

The `div*` entries are supplied by [Dividers – Mod List Load Order Organizers](https://www.nexusmods.com/mountandblade2bannerlord/mods/11686). Install it first if you want the same visual grouping. Novus only.

---

## 5. Load order

Order matters. Harmony resolves same-priority patches by registration order, which follows load order, so moving a mod can silently change which of two competing patches wins.

**RTS Camera** and **RTS Camera - Command System** are two components of a single mod (same Nexus page, same author) — they must be installed and load together, never one without the other.

<!-- BEGIN LOAD ORDER TABLE -->
| # | Module ID | Mod |
|---|---|---|
| 1 | `Bannerlord.Harmony` | [Harmony](https://www.nexusmods.com/mountandblade2bannerlord/mods/2006) |
| 2 | `BetterExceptionWindow` | [Better Exception Window](https://www.nexusmods.com/mountandblade2bannerlord/mods/404) |
| 3 | `Bannerlord.ButterLib` | [ButterLib](https://www.nexusmods.com/mountandblade2bannerlord/mods/2018) |
| 4 | `Bannerlord.UIExtenderEx` | [UIExtenderEx](https://www.nexusmods.com/mountandblade2bannerlord/mods/2102) |
| 5 | `Bannerlord.MBOptionScreen` | [Mod Configuration Menu (MCM)](https://www.nexusmods.com/mountandblade2bannerlord/mods/612) |
| | **`divCore`** | **Core — official modules** |
| 6 | `Native` | *(official — enable in launcher)* |
| 7 | `SandBoxCore` | *(official — enable in launcher)* |
| 8 | `Sandbox` | *(official — enable in launcher)* |
| 9 | `StoryMode` | *(official — enable in launcher)* |
| 10 | `CustomBattle` | *(official — enable in launcher)* |
| 11 | `BirthAndDeath` | *(official — enable in launcher)* |
| 12 | `NavalDLC` | *(official — enable in launcher)* |
| | **`divUtil`** | **Utilities, fixes and quality of life** |
| 13 | `HarmonyPatchScanner` | [Harmony Patch Scanner](https://www.nexusmods.com/mountandblade2bannerlord/mods/9179) |
| 14 | `AttributePointFix` | [Attribute Point Fix](https://www.nexusmods.com/mountandblade2bannerlord/mods/9631) |
| 15 | `BanditVoiceFix` | [Bandit Voice Fix - v1.3.x](https://www.nexusmods.com/mountandblade2bannerlord/mods/10374) |
| 16 | `BannerFix` | [Banner Fix](https://www.nexusmods.com/mountandblade2bannerlord/mods/4600) |
| 17 | `BetterSaveLoad` | [Better Save and Load](https://www.nexusmods.com/mountandblade2bannerlord/mods/3128) |
| 18 | `Butter_Fix` | [Butter Icon Fix](https://www.nexusmods.com/mountandblade2bannerlord/mods/2245) |
| 19 | `CharacterReload` | [Character Reload Fix](https://www.nexusmods.com/mountandblade2bannerlord/mods/3700) |
| 20 | `FixForRaidingCultureInfluence` | [Fix For Raiding Cultures Influence Loss](https://www.nexusmods.com/mountandblade2bannerlord/mods/1718) |
| 21 | `SavePortraitFix` | [Save Menu Portrait Fix for 1.4.7](https://www.nexusmods.com/mountandblade2bannerlord/mods/12011) |
| 22 | `TroopSort` | [Troop Sorting](https://www.nexusmods.com/mountandblade2bannerlord/mods/3596) |
| 23 | `TrueCulturalNames` | [True Cultural Names](https://www.nexusmods.com/mountandblade2bannerlord/mods/8305) |
| 24 | `UnitSpawnPrioritizationForAI` | [Unit Spawn Prioritization For AI](https://www.nexusmods.com/mountandblade2bannerlord/mods/9153) |
| 25 | `UsefulSkips` | [Useful Skips](https://www.nexusmods.com/mountandblade2bannerlord/mods/4896) |
| | **`divUI`** | **User interface** |
| 26 | `HighSellPrice` | [Alert on High Selling Price](https://www.nexusmods.com/mountandblade2bannerlord/mods/2645) |
| 27 | `BannerEditor` | [Banner Editor](https://www.nexusmods.com/mountandblade2bannerlord/mods/4944) |
| 28 | `BestTradePrice` | [BestTradePrice - Smarter Trading](https://www.nexusmods.com/mountandblade2bannerlord/mods/8474) |
| 29 | `BetterHideoutTroopSelection` | [Better Hideout Troop Selection](https://www.nexusmods.com/mountandblade2bannerlord/mods/10660) |
| 30 | `BetterPortraitsLite` | [Better Portraits for Heroes](https://www.nexusmods.com/mountandblade2bannerlord/mods/11876) |
| 31 | `EquipmentUIHelper` | [Equipment UI Helper](https://www.nexusmods.com/mountandblade2bannerlord/mods/9968) |
| 32 | `HistoricalBannerIcons` | [Historical Banner Icons](https://www.nexusmods.com/mountandblade2bannerlord/mods/9340) |
| 33 | `AIBannerIcons` | [AI Banner Icons](https://www.nexusmods.com/mountandblade2bannerlord/mods/9512) |
| 34 | `HorseCounter` | [Horse Counter (and Manager)](https://www.nexusmods.com/mountandblade2bannerlord/mods/9075) |
| 35 | `InventoryFilter` | [Inventory Filter](https://www.nexusmods.com/mountandblade2bannerlord/mods/9725) |
| 36 | `ItemQualityVisuals` | [Item Quality Visuals](https://www.nexusmods.com/mountandblade2bannerlord/mods/9440) |
| 37 | `KillCounters` | [Kill Counter](https://www.nexusmods.com/mountandblade2bannerlord/mods/11867) |
| 38 | `NoRelation` | [No Relation](https://www.nexusmods.com/mountandblade2bannerlord/mods/9556) |
| 39 | `LevelUpNotifications` | [Notifications for Level Up](https://www.nexusmods.com/mountandblade2bannerlord/mods/2550) |
| 40 | `ShowCompanionRequirements` | [Show Companion Requirements for Issues](https://www.nexusmods.com/mountandblade2bannerlord/mods/2937) |
| 41 | `ShowMilitaryPower` | [Show Military Power](https://www.nexusmods.com/mountandblade2bannerlord/mods/10767) |
| 42 | `ShowSkillLimit` | [Show Skill Limit](https://www.nexusmods.com/mountandblade2bannerlord/mods/9209) |
| 43 | `PartyLowFood` | [Warning on Party Low Food](https://www.nexusmods.com/mountandblade2bannerlord/mods/2551) |
| 44 | `WorldEventsAnnouncer` | [World Events Announcer - Updated for 1.3.15](https://www.nexusmods.com/mountandblade2bannerlord/mods/10559) |
| | **`divGameplay`** | **Gameplay** |
| 45 | `AskWhereALordIs` | [Ask Where A Lord Is](https://www.nexusmods.com/mountandblade2bannerlord/mods/8842) |
| 46 | `BanditBlackHole` | [Bandit Black Hole](https://www.nexusmods.com/mountandblade2bannerlord/mods/7433) |
| 47 | `BanditsDontDropEpicLoot` | [Bandits Don't Drop Epic Loot](https://www.nexusmods.com/mountandblade2bannerlord/mods/9009) |
| 48 | `BannerlordExpanded.CompanionExpanded` | [Bannerlord Expanded - Companion Expanded](https://www.nexusmods.com/mountandblade2bannerlord/mods/6736) |
| 49 | `CompleteQuestsToGainSkills` | [Complete Quests To Gain Skills](https://www.nexusmods.com/mountandblade2bannerlord/mods/8024) |
| 50 | `Docks` | [Docks](https://www.nexusmods.com/mountandblade2bannerlord/mods/10060) |
| 51 | `Horses` | [Horses](https://www.nexusmods.com/mountandblade2bannerlord/mods/6230) |
| 52 | `MorePrisonerInteractions` | [More Prisoner Interactions (reloaded)](https://www.nexusmods.com/mountandblade2bannerlord/mods/9396) |
| 53 | `SkillMastery` | [Skill Mastery](https://www.nexusmods.com/mountandblade2bannerlord/mods/8280) |
| 54 | `Overfleet` | [Overfleet](https://www.nexusmods.com/mountandblade2bannerlord/mods/9382) |
| 55 | `PlayerExecuteEdit` | [Player Execution](https://www.nexusmods.com/mountandblade2bannerlord/mods/1210) |
| 56 | `ImprisonScumbags` | [Town Magistrates](https://www.nexusmods.com/mountandblade2bannerlord/mods/1188) |
| 57 | `TrueController` | [True Controller](https://www.nexusmods.com/mountandblade2bannerlord/mods/3543) |
| 58 | `TrueRelations` | [True Relations](https://www.nexusmods.com/mountandblade2bannerlord/mods/2000) |
| 59 | `VassalBarons` | [Vassal Baron - Creation of Vassals](https://www.nexusmods.com/mountandblade2bannerlord/mods/8579) |
| | **`divPersistent`** | **Persistent adjustments** |
| 60 | `BetterCore` | [Better Core](https://www.nexusmods.com/mountandblade2bannerlord/mods/6367) |
| 61 | `BetterAttributes` | [Better Attributes (maintained fork)](https://www.nexusmods.com/mountandblade2bannerlord/mods/11811) |
| 62 | `BetterHUD` | [Better HUD](https://www.nexusmods.com/mountandblade2bannerlord/mods/3234) |
| 63 | `MinimumLearningRate` | [Minimum Learning Rate](https://www.nexusmods.com/mountandblade2bannerlord/mods/10465) |
| | **`divCombat`** | **Combat** |
| 64 | `DefendYourself` | [AI Defend Yourself](https://www.nexusmods.com/mountandblade2bannerlord/mods/897) |
| 65 | `AIKickNBash` | [AI Kick N Bash](https://www.nexusmods.com/mountandblade2bannerlord/mods/11019) |
| 66 | `AllHeroesAreVisibleInBattle` | [All Heroes Are Visible In Battle](https://www.nexusmods.com/mountandblade2bannerlord/mods/9587) |
| 67 | `CatapultGuide` | [Catapult Guide](https://www.nexusmods.com/mountandblade2bannerlord/mods/9383) |
| 68 | `RTSCamera` | [RTS Camera (War Sails compatible)](https://www.nexusmods.com/mountandblade2bannerlord/mods/355) |
| 69 | `RTSCamera.CommandSystem` | [RTS Camera - Command System](https://www.nexusmods.com/mountandblade2bannerlord/mods/355) |
| 70 | `BreakablePolearms` | [Breakable Polearms](https://www.nexusmods.com/mountandblade2bannerlord/mods/5285) |
| 71 | `HealingOnKillBasedOnMedicineSkill` | [Healing On Kill Based On Medicine Skill](https://www.nexusmods.com/mountandblade2bannerlord/mods/7574) |
| 72 | `ImmersiveBattlefields` | [Immersive Battlefields](https://www.nexusmods.com/mountandblade2bannerlord/mods/4633) |
| 73 | `ImmersiveCombat` | [Immersive Combat](https://www.nexusmods.com/mountandblade2bannerlord/mods/7868) |
| 74 | `KnockedDownHeroesInfluencesTroops` | [Knocked Down Heroes Influences Troops](https://www.nexusmods.com/mountandblade2bannerlord/mods/7955) |
| 75 | `FrontlineMod` | [Organized Frontline Mod](https://www.nexusmods.com/mountandblade2bannerlord/mods/9058) |
| 76 | `PerfectFireArrows` | [Perfect Fire Arrows](https://www.nexusmods.com/mountandblade2bannerlord/mods/3303) |
| 77 | `PickupMeleeWeapons` | [Pick Up Melee Weapons](https://www.nexusmods.com/mountandblade2bannerlord/mods/9793) |
| 78 | `RaiseYourBanner` | [Raise Your Banner](https://www.nexusmods.com/mountandblade2bannerlord/mods/3253) |
| 79 | `RaiseYourTorch` | [Raise Your Torch](https://www.nexusmods.com/mountandblade2bannerlord/mods/3289) |
| 80 | `NoMoreStuckProjectilesRedux` | [No More Stuck Projectiles Redux](https://www.nexusmods.com/mountandblade2bannerlord/mods/10760) |
| 81 | `RealisticCombatAdjustments` | [Realistic Combat Adjustments](https://www.nexusmods.com/mountandblade2bannerlord/mods/7116) |
| 82 | `RealisticWeaponMastery` | [Realistic Weapon Mastery](https://www.nexusmods.com/mountandblade2bannerlord/mods/11920) |
| 83 | `SiegeAIFix` | [Siege AI Fix](https://www.nexusmods.com/mountandblade2bannerlord/mods/11728) |
| 84 | `TroopsDropAllWeapons` | [Troops Drop All Weapons](https://www.nexusmods.com/mountandblade2bannerlord/mods/10639) |
| | **`divItemsTroops`** | **Items and troops** |
| 85 | `PracticalHolsters` | [Realistic Practical Holsters](https://www.nexusmods.com/mountandblade2bannerlord/mods/5935) |
| 86 | `RCM` | [Realistic Combat Mod](https://www.nexusmods.com/mountandblade2bannerlord/mods/11507) |
| | **`divCrafting`** | **Crafting** |
| 87 | `BetterSmithingContinued` | [Better Smithing Continued](https://www.nexusmods.com/mountandblade2bannerlord/mods/4318) |
| 88 | `CraftingPieceSorter` | [Crafting Piece Sorter](https://www.nexusmods.com/mountandblade2bannerlord/mods/6961) |
| 89 | `Bannerlord.BannerCraft` | [BannerCraft (Updated)](https://www.nexusmods.com/mountandblade2bannerlord/mods/5932) |
| 90 | `VisibleSmithingStaminaWhileWaiting` | [Visible Smithing Stamina While Waiting](https://www.nexusmods.com/mountandblade2bannerlord/mods/7561) |
| | **`divNPC`** | **NPCs** |
| 91 | `AliveScenes` | [Alive Scenes](https://www.nexusmods.com/mountandblade2bannerlord/mods/8138) |
| 92 | `AmazingNpcs` | [Amazing NPC Lords](https://www.nexusmods.com/mountandblade2bannerlord/mods/11878) |
| 93 | `MoreNotables` | [More Notables](https://www.nexusmods.com/mountandblade2bannerlord/mods/5231) |
| 94 | `UsefulWanderersv12` | [Truly Useful Wanderers](https://www.nexusmods.com/mountandblade2bannerlord/mods/8660) |
| 95 | `DressTheWandererv8` | [Dress The Wanderer](https://www.nexusmods.com/mountandblade2bannerlord/mods/8644) |
| 96 | `WanderersInParties` | [Nobles and Wanderers In AI Parties](https://www.nexusmods.com/mountandblade2bannerlord/mods/8600) |
| | **`divWMapStatic`** | **World map — static** |
| 97 | `AIExecutioner` | [AI Executioner](https://www.nexusmods.com/mountandblade2bannerlord/mods/3917) |
| 98 | `AIValuesLife` | [AI Values Life (NPC Surrender and Death)](https://www.nexusmods.com/mountandblade2bannerlord/mods/481) |
| 99 | `Memoria` | [Memoria](https://www.nexusmods.com/mountandblade2bannerlord/mods/11919) |
| 100 | `RealisticPrisoner` | [Realistic Prisoner](https://www.nexusmods.com/mountandblade2bannerlord/mods/2413) |
| | **`divWMapCont`** | **World map — continuous** |
| 101 | `AutoBestRole` | [Auto Best Role (Companion Role Auto-Assign)](https://www.nexusmods.com/mountandblade2bannerlord/mods/8454) |
| 102 | `AutoResolveRebalanced` | [Auto Resolve Rebalanced](https://www.nexusmods.com/mountandblade2bannerlord/mods/3453) |
| 103 | `ChildrenGrowFasterRedux` | [Children Grow Faster Redux](https://www.nexusmods.com/mountandblade2bannerlord/mods/8200) |
| 104 | `DynamicLooksChange` | [Dynamic Looks Change - 1.3.X](https://www.nexusmods.com/mountandblade2bannerlord/mods/10335) |
| 105 | `LordsGear` | [Lord's Gear](https://www.nexusmods.com/mountandblade2bannerlord/mods/8299) |
| 106 | `NoLordFreeTroops` | [No Lord Free Troops - Realistic AI Spawning](https://www.nexusmods.com/mountandblade2bannerlord/mods/9882) |
| 107 | `RealisticWeather` | [Realistic Weather](https://www.nexusmods.com/mountandblade2bannerlord/mods/4367) |
| | **`divScenes`** | **Scenes** |
| 108 | `Arenas_extended` | [Arenas Extended](https://www.nexusmods.com/mountandblade2bannerlord/mods/6137) |
| 109 | `Cutscenes_Extended` | [Cutscenes Extended](https://www.nexusmods.com/mountandblade2bannerlord/mods/10354) |
| 110 | `SiegeEngines_Extended_Vanilla+` | [Siege Engines Extended](https://www.nexusmods.com/mountandblade2bannerlord/mods/8958) |
| | **`divTourney`** | **Tournaments** |
| 111 | `BalancedTournamentArmor` | [Balanced Tournament Armor](https://www.nexusmods.com/mountandblade2bannerlord/mods/3471) |
| | **`divClans`** | **Clans and factions** |
| 112 | `ExtraClans` | [Extra Clans](https://www.nexusmods.com/mountandblade2bannerlord/mods/7833) |
| 113 | `ExtraClansAIBannerIcons` | [Extra Clans AI Banner Icons](https://www.nexusmods.com/mountandblade2bannerlord/mods/11942) |
| 114 | `ExtraClansWS` | [Extra Clans Warsails](https://www.nexusmods.com/mountandblade2bannerlord/mods/11536) |
| 115 | `VanillaMinorFactions` | [Vanilla Minor Factions](https://www.nexusmods.com/mountandblade2bannerlord/mods/8342) |
| | **`divDiplo`** | **Diplomacy and economy** |
| 116 | `Bannerlord.Diplomacy` | [Diplomacy](https://www.nexusmods.com/mountandblade2bannerlord/mods/832) |
| 117 | `ImprovedEconomyForAILords` | [Improved Economy For AI Lords](https://www.nexusmods.com/mountandblade2bannerlord/mods/8698) |
| | **`divBM`** | **Large gameplay mods** |
| 118 | `Nepotism` | [Nepotism](https://www.nexusmods.com/mountandblade2bannerlord/mods/4677) |
| | **`divGraphics`** | **Graphics** |
| 119 | `KingdomBorders` | [Kingdom Borders](https://www.nexusmods.com/mountandblade2bannerlord/mods/10699) |
| 120 | `WarSailsBannerSails` | [War Sails Banner Sails](https://www.nexusmods.com/mountandblade2bannerlord/mods/10696) |
| | **`divAudio`** | **Audio** |
| 121 | `RealisticCombatSounds` | [Realistic Combat Sounds](https://www.nexusmods.com/mountandblade2bannerlord/mods/3765) |
| 122 | `IB_Addon_UCH` | [Ulfkarl Cultured Horns (Immersive Battlefields addon)](https://www.nexusmods.com/mountandblade2bannerlord/mods/6040) |
| | **`divPatches`** | **Compatibility patches** |
| 123 | `zzzUniversalPatch` | [Universal Patch](https://www.nexusmods.com/mountandblade2bannerlord/mods/9638) |
| 124 | `StealthFlagFix` | [Stealth Flag Fix](https://www.nexusmods.com/mountandblade2bannerlord/mods/11354?tab=files) |
| | **`divCheat`** | **Cheat (empty)** |
| | **`divTest`** | **Test (empty)** |
<!-- END LOAD ORDER TABLE -->

---

## 6. Mod configuration

Every setting below is applied through the **Mod Configuration Menu**, reachable from the main menu (Options → Mod Options) unless noted otherwise. Mods not listed here need no configuration.

### Utilities

**Bandit Voice Fix**
- Debug Logging → **off** (the default). Only enable it if you find a silent bandit and intend to file a report.
- No load-order sensitivity in this list — its one documented conflict partner isn't present in Betterlord.

**Fix For Raiding Cultures Influence Loss**
- Misc → Non Raiding Culture Influence Change → `-10`

**Unit Spawn Prioritization For AI**
- Main Settings → AI Spawn Prioritization Mode → **Homogeneous**
- Set the matching option in the game's own Gameplay settings too

### User interface

**Horse Counter (and Manager)**
- Disable **Handle Horses Hourly**

**Item Quality Visuals**
- General → Visual Style → **Colored Icons**
- Enable the Tier 5, Tier 6 and Tier 7 icons

### Gameplay

**Bannerlord Expanded — Companion Expanded**
- Disable **Wanderer Join Request**
- Disable **Enable Companion To Sibling Conversation**
- Disable **Enable Companion To Son/Daughter Conversation**
- Disable **Additional Companion Slots**

**True Relations**
- Relations → Radius of Impact → `100`
- Relation Change Chance → `50%`

**Vassal Baron**
- Costs → Denars Cost → `100000`

### Persistent adjustments

**Better Attributes**
- Disable **Player Only** everywhere — 22 separate checkboxes
- Disable **Crush Through Chance**
- Disable **Healing Rate Bonus**
- Disable **Slice Through Chance**
- Enable **Support for more Bonuses** (at the very bottom)

> Use the maintained fork linked in the table. An earlier build of this mod silently failed to register most of its patch classes on 1.4.7; the fork resolves this. Confirm you're on the fork's own version line, not the original.

**Better HUD**
- Disable **Enemy Info**

### Combat

**AI Kick N Bash**
- No MCM configuration needed — defaults are correct. (An "Injured Animations → HP Threshold" setting was previously listed here; cross-checking the upstream guide's source list structure and this mod's own feature description — kicks, shield bashes, weapon bashes, cooldowns, no injury-triggered animation system — indicates that setting actually belongs to Artem's Lively Animations, which upstream lists immediately after this mod and which isn't part of Betterlord. Removed as a likely long-standing misattribution rather than left in place unverified.)

**Knocked Down Heroes Influences Troops**
- Enable **Disable Hero Knockdown Sounds**

**Siege AI Fix**
- Defaults are fine to start — the mod adds casualty-based retreat, army disbandment and cohesion loss on failed sieges. Fight one siege as attacker and one as defender before adjusting anything.
- It spawns cover and replacement ladders into siege scenes at runtime — if another mod alters siege scene props, watch for misplaced geometry during the wall-breach phase.

**Realistic Combat Mod**
- Configuration via `rcm_config.xml` in the mod folder, not via MCM — no in-game settings. Defaults are production-ready; only edit the config file if you want to adjust material damage values, thresholds, or multipliers.
- The mod auto-detects all armor materials at runtime and is compatible with any armor mod, including modded armor. No XML patches needed.
- v1.3.7 (current) includes material-based armor system, concussive trauma, weapon deflection on hard armor, and blunt face knockouts. Earlier versions (v1.0.4) fixed gambeson material classification (now properly detected as quilted armor, not plain cloth).

### Crafting

**Visible Smithing Stamina While Waiting**
- Additional options → Enable **[Town] Show current stamina percent**

### NPCs

**Truly Useful Wanderers**
- General Settings:
  - Disable **Use 6 Attribute Templates For All Heroes**
  - Enable **Enable Wanderer Level Scaling**
  - Disable **Enable Skill prefixes**
  - Enable **Age scaling for wanderers**
  - Enable **Age-based skill count for wanderers**
  - Wanderer Max / Min Skill → `200` / `50`
  - Minor Lords Max / Min Skill → `200` / `50`
  - Children Max / Min Skill → `250` / `20`
  - Disable **Enable Elders & Smiths**
  - Disable **Enable Ordinary Lords**

**Dress The Wanderer**
- Misc → Enable **Disable equipment for Main Hero**
- Maximum Tier → `3`, Minimum Tier → `1`
- Takes effect on new games only

**Nobles and Wanderers In AI Parties**
- General:
  - Disable **Only Clan Leaders Can Hire Wanderers**
  - Enable **Recruit Same Culture**
  - Buy Missing Equipment Chance → `0%` — Lord's Gear owns AI equipment purchasing
  - Upgrade Equipment Chance → `0%`
  - Disable **Enable Tavern Spawns** — Companion Expanded owns tavern spawns
  - Disable **Enable Companion Limit Options**
  - Disable **Enable 'Make Family' Dialogue**
  - Disable **Enable 'Make Noble' Dialogue**

### World map

**AI Executioner**
- **Hero Protection → off in Sandbox, on in Campaign** — see [§7](#sandbox-or-campaign).

**AI Values Life**
- Surrender Notifications → Enable **Surrender Banners**
- Disable **Player Faction Only**
- Death % → `0.03`
- **Death Protection → off in Sandbox, on in Campaign** — see [§7](#sandbox-or-campaign).

**Realistic Prisoner**
- Player → Max Loss % → `0.80`
- Enable **Surrender w/ Honor**
- Disable **Stealth Too**
- Disable **Civilian Too**
- NPC → Disable **Stealth Too**, Disable **Civilian Too**
- Do not enable **Preserve Economy** — Lord's Gear owns AI equipment-loss economics; leave this at default.

**Auto Best Role**
- Battle & Army → disable all three options. **Enable Battle Auto Assignment** is the important one — Immersive Battlefields owns battle formation assignment
- Auto Assign Messages → **Disabled**
- Enable **Skip Player Party**
- Assignment Check Intervals → `24` hours

**Auto Resolve Rebalanced**
- Siege Rebalance Settings → Settlement Advantage Multiplier → `1.5` — leaving this at its default value produces badly unbalanced auto-resolved sieges. This was missing from Betterlord's configuration entirely prior to this audit; add it now if you haven't.

**Lord's Gear**
- AI Gear Purchase:
  - AI Gold Spending Percentage → `0.20`
  - Disable **AI Restrict Weapon to Culture**
  - Clan Shop Visit Chance → `5%`
  - Clan Gold Spending Percentage → `0.20`
  - Enable **Clan Restrict to Culture**
  - Disable **Clan Restrict Weapon to Culture**
- Do not enable **Enable Gear Loss on Capture** — Realistic Prisoner owns gear loss on capture; leave this at default.

**No Lord Free Troops**
- Interface → Disable **Show spawn messages**
- Enable **Remove troops on new game start**
- Initial troop count → `7`

### Tournaments

**Balanced Tournament Armor**
- Change Armor → Troop Tier → `4`
- Enable **Wear Armor of Own Culture**

### Diplomacy and economy

Betterlord runs **Diplomacy alone** in this category — no second mod contests war, peace, rebellion, or succession. This is a simpler ownership picture than a list that also runs a dedicated war/peace overhaul, and it means Diplomacy's settings should be left closer to their own defaults rather than tuned down for a second system that isn't present.

**Diplomacy**
- Leave **Civil Wars** (Daily Chance To Start/Join Rebel Faction, Daily Chance To Start Civil War), **War Exhaustion**, **Fief Repatriation**, **Minimum War Duration**, and **Declare War Cooldown** at the mod's own defaults, or set them to your own preference. There is no longer a second system these need to be cleared for — reconfigure deliberately rather than carrying forward settings tuned for a mod that isn't in this list.
- Kingdom Diplomacy → your preference on **Delay Fiefless Kingdom Elimination**.

**Improved Economy For AI Lords**
- Enable **Enable Towns Denars Increase**. This was disabled in this list's predecessor specifically because Harvest And Production owned town economy there; Harvest And Production isn't part of Betterlord, and no other mod claims this system. The setting's own name indicates its shipped default is enabled — disabling it here would leave AI-lord town income with neither Harvest And Production's handling nor this mod's own, which serves no one. Restored to default.

### Compatibility patches

**Universal Patch**
- Disable **Armor Standardization**
- Disable **Debug** (at the bottom)

---

## 7. Starting a new game

### Sandbox or Campaign

Betterlord defaults to **Sandbox**. **Campaign** works with the identical module list — `StoryMode` is already enabled at position 9, so nothing is installed, removed or reordered. One setting changes.

| Setting | Sandbox *(default)* | Campaign |
|---|---|---|
| AI Executioner → **Hero Protection** | Off | **On** |
| AI Values Life → **Death Protection** | Off | **On** |
| Diplomacy → **Enable Storyline Protection** | Either — inert | **On** |

**Why Campaign needs these.** The main quest requires specific nobles to remain alive, and both AI Executioner (through executions) and AI Values Life (in battle) can kill them. With protection off, a Campaign run can quietly become unfinishable: no warning, no error, the quest simply cannot be completed. Set these **before** starting, because turning protection on later will not bring anyone back.

Heroes Must Die — a third mod that contributed to this same hero-protection system in this list's predecessor — is not part of Betterlord's base configuration. Its absence means one fewer death vector to protect against, not one fewer setting to configure: the two toggles above are the complete set for this list as shipped. If you add Heroes Must Die back later, it brings its own Hero Protection toggle and this table grows to three rows again.

**Player death.** No mod in Betterlord currently modifies player death probability on knockdown — vanilla rules apply in both Sandbox and Campaign.

### Game options

Set these in the game's own settings, not MCM:

| Setting | Value |
|---|---|
| Unit Spawn Prioritization | Homogeneous |
| Auto Save Interval | 60 |
| UI Scale | 0.75 |
| Report Casualties | Enabled |
| Player Received Damage | Realistic |
| Third Person Camera Distance | 1.10 |
| Show Attack Direction | Disabled |
| Friendly Troops Banner Opacity | 0.50 (0.00 for no banners) |
| Always Show Friendly Troops Banner Indicators | Enabled |
| Show Formation Distance Texts | Enabled |
| Troop Highlight (Character Mode) | No |
| Troop Highlight (RTS Mode) | No |

Suggested keybinds: Fast Forward → `Up Arrow`, Toggle HUD → `]`, take/release ship helm → `F5`.

Additional in-game shortcuts for mods in this list:
- **RTS Camera** — `F10` to toggle free camera mode in battles, `L` to open its own mod configuration (separate from MCM).
- **Catapult Guide** — `Middle Mouse Button` while operating a mangonel, ballista, or trebuchet.
- **Horses** — `Q` to call your horse when it's out of reach; `Q` to replenish arrows/quivers/throwables when the horse is adjacent; `Ctrl+Q` while mounted.
- **Inventory Filter** — `Shift+Click` on an item slot in the inventory to filter by that item type.

### Session hygiene

**Exit to desktop between loading saves — do not return to the main menu.** Some mods re-register their Harmony patches when a campaign initialises, and going back to the menu and loading again stacks a second copy of those patches on top of the first, with the effects compounding over a session.

---

## 8. Design philosophy and scope

Betterlord's ordering principle: **stability first, everything else second.** A mod earns a place by having no documented incident against it and, where its history includes one, by having that incident resolved and verified — not merely time having passed. Feature richness was not a design goal in itself; several capable, popular mods are absent here specifically because their update cadence, patch-conflict footprint, or open bug history didn't clear that bar as of this list's last audit.

**What that excludes, in brief:** custom troop-tree systems, a dedicated civil-war/succession overhaul, bandit-militia economy mods, and any mod whose only public distribution channel (e.g., Patreon-only) prevents verifying its update history the same way every other entry in this list can be verified. None of these are excluded on the belief that they're bad mods — several are well-regarded — they simply didn't meet this list's specific evidentiary bar for inclusion at time of writing. Re-evaluate any of them individually if their circumstances change.

**What's included but worth knowing:** a small number of mods here touch systems (NPC appearance generation, in particular) that a related — now-excluded — mod had a confirmed defect in. None of the included mods have any incident of their own; the caution is about the system they touch, not anything they've done. Treat this as a standing note to watch, not a reason for concern.

**Two components travel together by necessity, not by mod count:** RTS Camera and RTS Camera - Command System are one mod's two parts. Betterlord's true independent mod count is 111 once you account for this — 112 module IDs, but 111 things you're actually choosing between.

---

## 9. Known issues

None currently open. Every specific Harmony patch conflict and crash report on record from this list's development history involves at least one mod that isn't part of Betterlord's base configuration — so as shipped, there is nothing outstanding to work around.

This will not stay true forever: adding any excluded mod back in may reintroduce a conflict that was previously documented against it. Before reintroducing anything, check whether it has a known conflict partner, and whether that partner is also present.

---

## 10. Maintaining the list

**Scan in-campaign, not from the main menu.** [Harmony Patch Scanner](https://www.nexusmods.com/mountandblade2bannerlord/mods/9179) only sees patches actually registered, and some register only when a campaign or mission starts, not at load. A main-menu scan understates your conflict count. Load a save, fight one field battle, then scan.

Betterlord does not yet have its own in-campaign scan baseline — run one after your first session and treat that as the reference point for all future diffs. Do not assume any numbers from this list's predecessor apply; the module set has changed enough that a fresh baseline is the only honest one.

**Do not trust launcher version strings.** Novus reads `RequiredVersion` from each mod's `SubModule.xml`, and many authors never update it. Verify by DLL timestamp, or by checking whether a mod's expected patches actually appear in a scan.

**Diagnostic workflow when something breaks:**

1. Better Exception Window report, if one appears
2. `rgl_log_<pid>.txt` and `rgl_log_errors_<pid>.txt` from that session
3. Harmony scan diff against your last known-good baseline
4. Mod toggling, guided by which mods updated most recently
5. Windows Event Viewer for crashes that produce no log at all — stack overflows in particular

**Back up before every update batch**, and before running any save-repair command.

**Considering an addition?** Apply the same bar as everything already here: no open incident, or a specific verified fix if one existed previously. A mod that merely hasn't broken *yet* is not the same as a mod with a track record.

---

## 11. Changelog

### 2026-08-04 — Betterlord v1.4.7.1.0

- Initial release. Forked from a personal predecessor list at the module-selection level: every third-party mod evaluated individually against a stability-first bar (no open incident, or a verified-resolved one) rather than carried forward by default.
- 112 third-party modules (111 independent mods — RTS Camera's two components count as one), 7 official modules, 5 foundation libraries.
- Diplomacy's settings reconfigured to run standalone rather than paired with a second war/peace system — see [§6](#6-mod-configuration).
- Improved Economy For AI Lords' town-income setting reverted to default (see revision below — resolved same day, not left pending).
- No open known issues at time of release — see [§9](#9-known-issues).
- **Same-day audit against the upstream guide's current text** (Vanilla 1.4.7 Plus Modding Notes, mods/11354, last updated 04 Aug 2026): every MCM setting for every mod present in Betterlord cross-checked line by line.
  - Removed a likely long-standing misattributed setting from AI Kick N Bash ("Injured Animations → HP Threshold") — upstream's list structure and the mod's own feature description both indicate this setting belongs to Artem's Lively Animations, which isn't part of Betterlord.
  - Added Auto Resolve Rebalanced's Settlement Advantage Multiplier (`1.5`) — present in the mod, present in this list, but its configuration had been omitted entirely until now. Upstream flags the default as producing badly unbalanced auto-resolved sieges.
  - Corrected Balanced Tournament Armor's Troop Tier from `3` to `4` and added the missing "Wear Armor of Own Culture" toggle, matching upstream's current recommendation.
  - Expanded Realistic Prisoner's config with its separate NPC-side settings and a "Preserve Economy" caution (owned by Lord's Gear), and added the matching "Gear Loss on Capture" caution to Lord's Gear itself.
  - Added in-game keybinds for RTS Camera (F10, L), Catapult Guide, Horses, and Inventory Filter — all present in Betterlord, none previously documented here.
  - Flagged ButterLib and MCM as a small step behind the versions upstream currently displays — see [§1](#1-before-you-start).
- **Second same-day pass: audited every cross-mod ownership rationale in §6 against both upstream's current text and this list's own predecessor notes**, specifically checking whether each stated reason for a non-default setting still holds given which mods are actually present in Betterlord.
  - Confirmed five ownership rationales still valid as written (referenced mod present, reasoning unchanged): Nobles and Wanderers In AI Parties' two cross-references to Lord's Gear and Companion Expanded, Auto Best Role's reference to Immersive Battlefields, and the Realistic Prisoner ↔ Lord's Gear pairing.
  - **Improved Economy For AI Lords' "Enable Towns Denars Increase" resolved, not just flagged.** Its disabled state existed only to defer to Harvest And Production, which isn't part of Betterlord. No other mod claims this system, and the setting's own default is enabled. Committed to enabling it rather than leaving it as an open question — this list's own principle (assume defaults when a stated reason no longer applies) requires a decision, not a caveat.
  - Diplomacy's standalone reconfiguration (previous session) re-verified against this same principle — already correct as written, no further change.
  - No other stale ownership rationale found. Every other cross-mod reference in §6 either points to a mod that's present and still accurate, or belongs to a mod that's excluded from Betterlord entirely (making the question moot rather than open).

### 2026-08-05 — Mod Version Updates

- **Siege Engines Extended** updated to v1.1. Modular destructible covers on siege towers and battering rams, new siege tower variants with modular destruction states, ballista/mangonel/trebuchet refinements (improved HP, destruction states, ammo), night-time torch spawning on siege structures. No MCM configuration. Author notes potential FPS impact on night scenes with many siege structures and effects (not a defect in this mod, attributed to increased particles and objects); incompatible with EpicSieges and Empire of Europe mods.
- **Organized Frontline Mod** updated to v1.2.7 (per author changelog and files tab). No incidents or conflicts reported.
- **RTS Camera** (both components) updated to v5.4.15 (per author files tab). No incidents or conflicts reported.
- **Realistic Combat Mod** updated to v1.3.7 (per author changelog and files tab). Auto-compatible with any armor mod; no XML patches required. Configuration via `rcm_config.xml` in mod folder, not MCM. Added configuration note to [§6](#6-mod-configuration).
- All three mods verified zero incidents or conflicts with Betterlord's current base configuration.

---

## Credits

All credit for the mods themselves belongs to their authors, linked in [§5](#5-load-order).

---

*Betterlord is maintained by Valtarien (ACE) and published in case it is useful to others. It carries no warranty and no support commitment, and it claims nothing over the mods it lists — those belong to their authors under their own terms.*
