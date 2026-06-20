# stickers/clock/

The **MUN clock** — one "My honest _\<time\>_ reaction" sticker for every hour of
the day. Together they form a 24-hour joke clock that both the main site
(`index.html`) and the minigame (`game.html`) read to show *the sticker for the
current hour*.

## Naming convention (important!)

Each file is named `HH-label.webp`, where `HH` is the **two-digit 24-hour hour**
(`00`–`23`) that the sticker represents, followed by a human-readable label:

| File | Hour |
| --- | --- |
| `00-midnight.webp` | 00:00 |
| `01-1am.webp` … `11-11am.webp` | 01:00 – 11:00 |
| `12-noon.webp` | 12:00 |
| `13-1pm.webp` … `23-11pm.webp` | 13:00 – 23:00 |

The site parses the leading two digits to pick the right sticker for
`new Date().getHours()`, so **the `HH-` prefix must stay** and exactly one file
must exist per hour. Add a new reaction by dropping in a `HH-label.<ext>` file,
where `<ext>` can be any of `.png/.jpg/.jpeg/.webp/.gif`, that overrides the
matching hour.

These stickers are loaded **separately** from the loose Nazan stickers in `../`
(the GitHub contents API only lists top-level files there, so this subfolder is
never scattered as a movable Nazan).
