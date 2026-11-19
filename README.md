<h1 align="center">AVCME</h1>

<p align="center">
  <b>Adaptive Volumetric Chunk Management Engine</b><br>
  A server-side Fabric mod that looks at chunk sections in 3D – observe first, change nothing unproven.
</p>

<p align="center">
  <a href="#status">Status</a> ·
  <a href="#what-avcme-is">What it is</a> ·
  <a href="#what-avcme-is-not">What it is not</a> ·
  <a href="#compatibility">Compatibility</a> ·
  <a href="#reporting-bugs">Bugs</a> ·
  <a href="#license">License</a>
</p>

> [!WARNING]
> **AVCME is EXPERIMENTAL – early versions are highly experimental.**
>
> * **Back up your world** before installing it, and keep backups while you use it.
> * Do **not** use it on worlds or servers you cannot afford to lose.
> * There is **no promise of better performance** and **no promise of compatibility** with any other mod.
>   Everything stated here is limited to what was actually tested, on the versions named.
> * Behaviour, configuration and commands can change between versions without notice.

This repository holds the documentation, the [wiki](../../wiki) and the [issue tracker](../../issues).
The mod itself will be downloaded from Modrinth or CurseForge. AVCME is not open source; see [License](#license).

## Status

AVCME is **in development. No version has been released yet.**

| | |
|---|---|
| Minecraft | 1.21.1 (first target) |
| Loader | Fabric only (Fabric Loader + Fabric API) |
| Side | server (dedicated server and the integrated singleplayer server); no client mod required |
| Default mode | `observe` – measures and reports, changes no game behaviour |
| Releases | none yet; the first public builds will be marked **alpha / experimental** |

## What AVCME is

Minecraft manages chunks as 16 × 16 columns that reach from the bottom to the top of the world, but
the place where something actually matters is three-dimensional. AVCME adds a **3D interest model per
16 × 16 × 16 chunk section** next to vanilla:

* Every player is an interest source. Each loaded section gets an interest band – **near**, **mid** or
  **far** – from its horizontal *and* vertical distance to all players (the strongest band wins).
* An **observer** reports, per band, how many sections are loaded, how many of them vanilla really
  random-ticks, and how many block entities they hold – read-only, with a fixed work budget per tick.
* **Diagnostics** for server owners: `/avcme status`, `/avcme metrics` (tick time percentiles and the
  mod's own cost), `/avcme census`, `/avcme compatibility` (operator only).
* A strict **safety switch**: if AVCME's own work ever fails or runs over its time budget, that part
  switches itself off and vanilla keeps running untouched.

The interest bands are **hints, never commands**: in the current mode they do not pause, skip, delay
or reorder anything in the game.

## What AVCME is not

* It does **not** pause redstone, fluids, farms, mobs, block entities, scheduled ticks, lighting or
  anything else because it is far away – vertically or horizontally.
* It does **not** change the world format, region files, chunk loading, chunk tickets or network packets.
  Removing the mod leaves a normal vanilla world, no migration needed.
* It does **not** replace Sodium (rendering), Lithium (game logic), C2ME (chunk generation and I/O)
  or LOD mods, and it does not hook into their internals.

Optimisations will only be added where measurements show a real cost **and** tests show that the
game behaves exactly as before. If a measurement shows no benefit, the idea is dropped and the
result is documented – also negative results.

## Compatibility

Nothing is marked as compatible until it was tested with the exact versions. Planned test stacks
(Fabric, 1.21.1) – all **untested** at the moment:

| Mod | Area | Status |
|---|---|---|
| Fabric API | runtime, events | required |
| Lithium | game logic | untested |
| C2ME | chunk generation, I/O | untested |
| Sodium (client) | rendering | untested |
| FerriteCore, ModernFix, Moonrise, VMP | memory, misc., chunk system, multiplayer | untested |
| Iris, Distant Horizons, Voxy | shaders, LOD | untested (tested separately, never together by default) |

Test results with versions, logs and dates will be listed in the wiki under
[Supported Versions](../../wiki/Supported-Versions).

## Performance

Not measured for a release yet. Numbers will only be published together with the hardware, game
version, mod list, world and method – including results that show no gain.

## Reporting bugs

Please open an [issue](../../issues/new/choose) with the Minecraft version, Fabric Loader and Fabric
API versions, the AVCME jar name, the other mods involved, your `config/avcme.properties`, and
`logs/latest.log` (plus a crash report if there is one). Please mention whether the world was backed up.

## License

AVCME is **not open source**. All rights reserved by cptgummiball; see [`LICENSE`](LICENSE).
In short:

* You may play with AVCME, use it on any server and show it in videos and streams.
* You may put AVCME into **modpacks**, as long as the jar files stay exactly as published.
* You may **not** modify, decompile, re-upload or otherwise redistribute AVCME, or use its assets elsewhere.
* AVCME is provided **as is, without any warranty**; experimental versions are used at your own risk
  (section 6 of the license).
* For anything else, open a [permission request](../../issues/new?template=permission_request.yml).

AVCME is made by **cptgummiball**. It is not an official Minecraft product and is not associated
with Mojang or Microsoft.
