# AVCME API for mod developers

API version **1** · package `dev.cptgummiball.avcme.api` · mod id `avcme`

**Most mods need nothing from this page** if AVCME uses the standard loader interfaces.

## Getting the API

`avcme-api-1.jar` and `avcme-api-1-javadoc.jar` from the [releases](../../../releases),
as a **compile-only** dependency. Do not ship the API or any AVCME files in your mod. If
AVCME is optional for your mod, check that the mod `avcme` is loaded before touching its
classes.

The license (section 5) allows compiling against the API and publishing mods that use it.
