# Big Solitaire / Großes Solitär

**Download:** [Big-Solitaire.apk](https://github.com/booskers/big-solitaire/releases/latest/download/Big-Solitaire.apk) (latest release). Free and open
source under the MIT licence. Made with love by booskers / Polychrome.

English or German, following the phone's language (German: polite "Sie", card names like "die Herz-Sieben", B/D/K). Double Klondike (two decks, 104 cards, 9 columns, 8 top piles, one card at a time from the deck) for Android phones,
made for older players and people with low vision. Landscape only.

- **Big, high-contrast cards**: large rank and suit at the top of every card, a big suit symbol below, face-down cards
  in solid blue with stripes so they never look like open cards. Red cards can have a pale pink tint (on by default).
- **Tap to move**: one tap sends a card (or the pile on top of it) to the best place. Dragging works too.
  Aces go up by themselves, and when every card is open the game finishes itself.
- **Hint** (yellow button) shows a good move with a pointing hand and says it in words. **Undo** has no limit.
- **The coach** steps in when the gestures aren't working out: repeated taps on a card that can't move, tapping
  face-down cards, holding a finger down, failed drags, tapping the empty table, double taps, pinch-zooming, or a long
  time without a move. Each guide has a small animated picture and plain words, shows at most three times, and closes with a tap anywhere; messages close when tapped.
- **Settings**: helper tips (the coach, on/off), extra-big numbers, pink tint, read cards aloud (the phone's text-to-speech, in its language), sounds, vibration,
  deck on the right for left-handed players.
- The game is saved after every move and comes back after the app is closed.

## Layout

- `web/index.html` — the whole game (one file, no internet needed).
- `android/` — one WebView activity, locked to landscape, full screen; `python build.py` makes
  `android/dist/Big-Solitaire.apk` (no Gradle; needs JDK 17 and Android SDK platform 35 / build-tools 35.0.0).
  The signing key is made on the first build in `%USERPROFILE%\.bigsolitaire\` — keep it, or updates won't install.
- `tools/serve.mjs` — `node tools/serve.mjs` serves the game at http://localhost:5190/ for testing in a browser.

## Updates

The game updates itself from this repository's releases, unnoticed: it looks for a new version when it is left and
every hour in the background, and installs it only while the game is closed. Next time it opens it simply is the new
version, with the saved game kept. Android allows that from Android 12 on, after **Automatische Updates einschalten**
in Einstellungen has been tapped once (Android asks one time). On Android 11 and older each update needs a tap there.

**Releasing:** raise `versionCode` and `versionName` in `android/AndroidManifest.xml`, run `python android/build.py`
(signs with the key in `%USERPROFILE%\.bigsolitaire\`; keep it, or updates won't install), add a section to
`CHANGELOG.md`, commit, then attach **both** files from `android/dist/`:

    gh release create vX.Y.Z android/dist/Big-Solitaire.apk android/dist/big-solitaire.json --title "Big Solitaire X.Y.Z" --notes "…"

Phones read `releases/latest/download/big-solitaire.json`; a release without it is never installed.
