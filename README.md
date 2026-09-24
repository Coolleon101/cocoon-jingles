# Cocoon Jingles

A jingle pack for [Cocoon](https://github.com/inssekt/CocoonFE) — the short audio sting that plays
when you highlight a game in the frontend.

**179 jingles across 7 platforms.** The focus is on titles the larger community packs do not
reach: ROM hacks, European and Australian releases, and games whose filenames follow
[No-Intro](https://no-intro.org/) conventions.

> ## ⚠️ Read this before you install
>
> **This pack was generated automatically, with AI, and most of it has never been listened to.**
>
> The clips were produced by scripts that boot each game in an emulator, record its audio, and pick
> a window algorithmically — the longest sustained run of non-silence after the boot logos. Nothing
> about that process understands music. It cannot tell a title theme from a menu sting, an ambient
> loop, or a character grunt that happened to last six seconds.
>
> A rough quality pass was done using measurable signals only: how far into the recording the audio
> starts, how long the sustained run is, and the encoded file size. Clips that failed those checks
> were re-recorded or replaced. **That is not the same as someone hearing them.** Fewer than twenty
> of these have actually been played back by a human.
>
> Known consequences, all of which have been seen in this pack at some point:
>
> - Some clips are **emulator boot chimes** rather than game music. The obvious ones were caught and
>   fixed by a size heuristic, but the heuristic is crude.
> - Some are the **wrong part of the track** — an intro swell, a quiet bar, a loop point.
> - A few games produce **no audio at all** without a button press, so their clip may be silence or
>   near-silence that slipped past the threshold.
> - A handful came from **soundtrack rips rather than the game itself**, so they are the right music
>   but not necessarily what the game plays on its title screen.
>
> Treat it as a starting point that saves you recording 179 clips by hand, not as a curated set. If
> something sounds wrong, it probably is — please
> [open an issue](https://github.com/Coolleon101/cocoon-jingles/issues) naming the game, and it will
> be re-done or removed.

| Platform | Jingles |
|---|---|
| `nds` | 80 |
| `gba` | 59 |
| `switch` | 13 |
| `gamecube` / `gc` | 9 each |
| `n3ds` | 8 |
| `wii` | 1 |

## Installing

In Cocoon, add the repository by its `owner/repository` string:

```
Coolleon101/cocoon-jingles
```

The setting has moved between Cocoon releases. Depending on your build it is under
**Settings → Personalization** or **Settings → Library & Data**, so check the version you are
running rather than following a screenshot.

## Why another pack

Most packs anchor their match patterns to a tidied-up game title. That works until it meets a real
ROM library, where two things break it.

**Article placement.** No-Intro moves leading articles to the end of the title, so the file is
`Legend of Zelda, The - The Wind Waker (USA)`, not `The Legend of Zelda - The Wind Waker`. Patterns
anchored with `$` to the latter will never match the former.

**Region and revision tags.** A pattern ending `...wind waker$` cannot match a name ending
`(USA)` or `(Rev 1)`.

The effect is measurable. Tested against a 24-title GameCube set:

| Match attempt | Titles matched |
|---|---|
| Community pack patterns, region tags present | **0 of 24** |
| Community pack patterns, region tags stripped | 14 of 24 |
| Patterns generated from the real filenames | **24 of 24** |

Every pattern here is generated from the actual ROM filename, which is why this pack sits
alongside the bigger ones rather than replacing them. Run both.

## Conventions

```
index.json
jingles/<platform>/<creator>/<Game Name> (Creator).ogg
```

Each `index.json` entry carries a `game` label, the `file` path, and a `regex` matched against the
game name.

Clips are 6 seconds, normalised to **-16 LUFS** with **-1.5 dB** true peak, short fades at both
ends, Ogg Vorbis q4. They land between 90 and 125 KB. Anything much smaller is usually a boot
chime or a menu blip that slipped through rather than a theme.

GameCube entries are published under **both** `gamecube` and `gc`. The platform key Cocoon expects
and the folder name a library uses are not always the same, and duplicating the entry costs a few
kilobytes.

## Contributing

Pull requests are welcome, particularly for platforms thin on coverage here. Match the naming
convention above, keep clips to roughly 6 seconds, and normalise before submitting so the volume
sits alongside everything else.

If a pattern fails to match a filename you use, open an issue with the exact filename. That is
more useful than a corrected title, because the filename is what the matching actually sees.

## Credits

Most clips were captured directly from the games by an automated pipeline: scripts that launch each
title in an emulator, record the audio, detect where the music starts, then trim, normalise and
encode. A smaller number were cut from soundtrack rips where a game would not produce audio
unattended. See the warning at the top for what that means for quality.

Nine GameCube entries are re-hosted from the
[Cocoon Community Jingles](https://github.com/Flapperultra02/Cocoon-Community-Jingles) pack,
renamed to match No-Intro filenames so they match. Original creators stay in the filename, which
is that pack's own convention:

| Creator | Titles |
|---|---|
| CirnoWaifu | Spyro: A New Beginning, Four Swords Adventures, Ocarina of Time, Wind Waker, Twilight Princess |
| Felipne87r | Mario Power Tennis |
| Gracie Failfox | Mega Man X: Command Mission |
| RetroWave64 | Mega Man X Collection |
| Natalie | Metroid Prime 2 |

If you made one of these and would rather it were not re-hosted here, open an issue and it will be
removed.

## Licence

Game audio remains the property of its copyright holders. These are short excerpts published for
use in a personal game frontend, and no ownership is claimed over any of it.
