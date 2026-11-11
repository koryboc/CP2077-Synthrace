# Synthrace – Race Music Overhaul

A Cyberpunk 2077 mod that completely replaces the dull, repetitive vanilla race music with a dynamic arcade‑style soundtrack system.
Every race becomes more energetic, more atmospheric, and far more satisfying — with fully randomized songs, custom playlists, win/lose outros, and support for external music sources.

---

## ✨ Features

- High‑energy arcade‑style soundtrack for all street races
- Random song selection per race — no more fixed repetitive music
- Short win/lose outro stingers for smoother race endings
- Fully customizable playlists
- Support for `.mp3` and `.ogg`
- Optional JSON playlists for linking music from other mods (e.g., RadioExt)
- Default fallback outros included
- Works with all vanilla street race events

---

## 📦 Installation

1. Install [RadioExt](https://github.com/justarandomguyintheinternet/CP77_radioExt) (required):
   *Its [RED4ext](https://github.com/WopsS/RED4ext) extension is used as the audio backend.*

2. Extract the `Synthrace` folder into:
   ```
   <GameDir>/bin/x64/plugins/cyber_engine_tweaks/mods/
   ```

3. Launch the game.
   The mod activates automatically when entering any street race.

---

## 🎧 Creating Custom Playlists (Method 1 – Folder Based)

You can create playlists by adding folders inside:

```
<GameDir>/bin/x64/plugins/cyber_engine_tweaks/mods/Synthrace/music
```

**Rules:**
- Folder name = playlist name
- Must NOT start with a special character
- Place any number of `.mp3` or `.ogg` files inside
- Optional outros:
  - `RaceEnd1.mp3` → win
  - `RaceEnd2.mp3` → loss
- Missing outros automatically fall back to defaults

**Example structure:**

```
Synthrace/music/
└── My Playlist/
    ├── Song A.mp3
    ├── Song B.ogg
    ├── Song C.mp3
    ├── RaceEnd1.mp3   ← win outro
    └── RaceEnd2.mp3   ← loss outro
```

During races:
- A random **Song** will play
- After the race:
  - **RaceEnd1** for winning
  - **RaceEnd2** for losing

---

## 🎧 Creating Custom Playlists (Method 2 – JSON Based)

Use this method if you want to **link existing music from other mods**, such as RadioExt radios — without copying files.

Create:

```
Synthrace/music/My Playlist.json
```

**Example JSON:**

```json
{
    "songs": [
        "radioExt\\radios\\100.1 Night City Faves\\Friday Night Fire Fight.mp3",
        "radioExt\\radios\\100.1 Night City Faves\\Trauma.mp3",
        "radioExt\\radios\\199,2 Lotus Ultimate\\Lotus III - Metal Machine (Remix).mp3"
    ],
    "outros": [
        "Synthrace\\music\\#Default\\RaceEnd1.mp3",
        "Synthrace\\music\\#Default\\RaceEnd2.mp3"
    ]
}
```

**Rules:**
- Songs must be `.mp3` or `.ogg`
- Paths start at the `mods` folder
- At least one song required
- Outros optional (max 2 entries)

JSON gives full flexibility for multi‑mod music collections.

---

## 📁 File Structure (Included)

```
Synthrace/
├── init.lua      → core logic
├── text.lua      → UI text and labels
├── api.lua       → IntelliSense type stubs
└── music/        → default music + user playlists
```

---

## 🧩 Public API (for Mod Developers)

Synthrace exposes a small set of playback functions via `GetMod("Synthrace")`.

```lua
local sr = GetMod("Synthrace")
if not sr then return end

sr.PlayOnce()       --Plays a random song once.
sr.PlayOnce(3)      --Plays song #3 of the active playlist once.
sr.PlayLoop()       --Starts a randomized loop — new track per iteration.
sr.PlayLoop(3)      --Loops song #3 repeatedly (same track every iteration).
sr.PlayWinOutro()   --Plays the win outro once (RaceEnd1).
sr.PlayLossOutro()  --Plays the loss outro once (RaceEnd2).
sr.StopAll()        --Stops all playback and restores game audio.
```

---

## ✔ Requirements

- [Cyberpunk 2077](https://www.gog.com/de/game/cyberpunk_2077) **2.21+**
- [Cyber Engine Tweaks](https://github.com/maximegmd/CyberEngineTweaks) **1.35+**
- [RadioExt](https://github.com/justarandomguyintheinternet/CP77_radioExt) (required — provides the audio player)
- [Native Settings UI](https://github.com/justarandomguyintheinternet/CP77_nativeSettings) (optional — provides a native location for the settings)

---

## 🎵 Music Credits

The tracks featured in this mod include works from the following artists:
- [Patrick Phelan](https://en.wikipedia.org/wiki/Patrick_Phelan_(composer))
- [Hugo Lopes](https://www.youtube.com/@HugoLopesGuitar)
- [Arcade Music Tribute](https://www.youtube.com/@ArcadeMusicTribute)

All tracks used in this mod are the property of their respective creators and rights holders. This mod is a fan-made project intended for entertainment purposes only and is not affiliated with or endorsed by the artists or their labels.

---

## 💬 Support

Bug reports are accepted only when:
- game version is 2.21+
- CET version is 1.35+
- all required dependencies are installed
- you are using the latest version of this mod
