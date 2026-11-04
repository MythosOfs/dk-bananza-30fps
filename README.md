# Donkey Kong Bananza: 30 FPS Lock

ExeFS patch for [Orchid](https://github.com/MythosOfs/Orchid) (also works in other emulators that load yuzu/Eden-style mods). It makes the game always request swap interval 2, so it runs at a steady 30 fps at normal game speed instead of jumping between 60, 30 and 20 fps.

Download: [dk-bananza-30fps.zip](dk-bananza-30fps.zip)

## Built into Orchid

Orchid has this patch built in as an option, so you don't need the zip there:
right-click Donkey Kong Bananza → **Properties → System** → check **Lock to 30 FPS (game patch)**.
It does the same as this mod, only for the same game version. The option lands with the next Orchid build; until then, or in other emulators, use the zip below.

## Requirements

- Title ID `040074A01BF12000`
- Main module build ID `E25C90C1C136638885659FD55BF8A03B3403489D`. On any other game version the patch is not applied and does nothing.

## Install the zip

Option A, from inside Orchid:

1. Right-click Donkey Kong Bananza in the game list, then **Properties → Add-Ons**.
2. Click **Import Mod from ZIP**, pick `dk-bananza-30fps.zip` and confirm the name `30 FPS Lock`.
3. Make sure **30 FPS Lock** is checked.

Option B, by hand:

1. Extract the zip.
2. Drag the `040074A01BF12000` folder into the emulator's `load` folder (Orchid on Linux: `~/.local/share/eden/load/`; or right-click the game → **Open Mod Data Location** and drop the `30 FPS Lock` folder in there).

Result:

```
load/040074A01BF12000/30 FPS Lock/exefs/E25C90C1C136638885659FD55BF8A03B3403489D.ips
```

To turn it off, uncheck **30 FPS Lock** in the game's Add-Ons tab. Use either the mod or the built-in option, not both.

## What it changes

One instruction in the main module at `0x204ac4`: `csel w10, w8, w9, lt` (`0x1a89b10a`) becomes `mov w10, #2` (`0x5280004a`). The game ties its game step to the swap interval it requests itself, which is why the game keeps normal speed. Forcing 30 fps from outside the game would make it run at half speed.
