# stickers/egans/

Egan stickers for **Egan Mode** — the milestone minigame in Nazan Dodge (`game.html`).

Drop funny PNG/JPG/WEBP/GIF stickers of Egan in here. During an Egan round each sticker
flies across the screen exactly once for the player to catch (+10 points each).
Transparent PNGs look best.

These are loaded **separately** from the main Nazan stickers in `../` and are only ever
fetched when Egan Mode is enabled. Egan Mode is now **ON** (it triggers at score
milestones 1000, 2500, 4000, …). Until files are added here, Egan Mode falls back to
plain badges.

To bug-test Egan Mode on its own without grinding to 1000, open the game with
`?egan=test` (e.g. `game.html?egan=test`) and a round drops in almost immediately.
