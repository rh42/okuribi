# 送り火 okuribi (the send-off fire)

A page with nothing but a place to write. What you write burns.

On the first keystroke an ember drifts in from the edge of the page; about fifteen seconds later it reaches your first word and starts eating along the line you laid down — ash, char, a bright tip, scorch, then ink. Behind it, nothing.

- **Tap** the page: you try to stamp it out. It flares and burns faster.
- **Hold** the page: you cup a hand over it. It slows. It never stops.
- **Write** more: more fuel ahead of the tip, the faster it moves.
- Stop writing and it catches up, waits at the caret, and goes out. The next keystroke strikes again.

Backspace works until a glyph is already burning; then it belongs to the fire. 

One room, lights off. There is no light mode.

## Nothing is stored

That is the whole feature, so it is built to be checkable:

- Static files, no build, no dependencies. The page loads only its own fonts and icon from the folder it lives in.
- A `Content-Security-Policy` with `connect-src 'none'` — the page cannot reach any network.
- No `localStorage`, `sessionStorage`, `IndexedDB`, cookies, or form fields holding text.
- The text is cleared on `pagehide`, so the back button brings back a blank page.
- It keeps burning while the tab is hidden. Time away is simulated on return, and past long enough, everything is simply gone.

## How the fire is drawn

- The ink is a `background-clip: text` gradient, so the burn paints through the glyphs without splitting the text node. Shaping and wrapping stay the browser's job, which is why it burns any script — CJK, RTL — along its own reading direction.
- Fire does not travel across a line break. It dies where the line ends, and the start of the next line smolders up on its own: scorch, glow, catch.
- Keystrokes land in a hidden textarea kept under the visible caret, so IME candidate windows open where the text is. Graphemes are segmented with `Intl.Segmenter`.
- The ember, sparks and ash are one `<canvas>` on top; the burn front itself is pure CSS on the paragraph.

## Fonts

A typewriter for the Latin: [Courier Prime](https://github.com/quoteunquoteapps/CourierPrime), regular only, self-hosted in `fonts/`. SIL Open Font License; see `fonts/courier-prime/OFL.txt`. CJK falls through to the system's book faces (Hiragino Mincho, Yu Mincho, Songti), a chosen contrast.

## Run

Open `index.html`, or serve the folder. Nothing else.
