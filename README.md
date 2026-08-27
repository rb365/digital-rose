# Digital Rose

One file. Upload `digital-rose.html` to any static host — that is the whole piece.

2021 hic et nunc remake of Jonathan Puckey’s Paper.js [division raster](https://paperjs.org/examples/division-raster/) plus two new modes: **genome** and **live**.

## Open it

Rose and genome work from `file://`. Live camera needs a secure origin (localhost or https).

```bash
python3 -m http.server 8765
```

Then:

- [http://127.0.0.1:8765/digital-rose.html](http://127.0.0.1:8765/digital-rose.html) — rose (default)
- `?mode=genome`
- `?mode=live`
- `?mode=live&src=axial` — Axial Seamount HLS
- `?mode=live&src=reel` — Mux test reel
- `?mode=live&src=https://…` — any HLS / MJPEG URL

Deep links are shareable. The corner switcher updates the query string.

## Modes

**rose** — the photo stays hidden. The first frame is one rectangle filled with the cover-fit average of the whole rose (that muddy taupe/olive is the average, not a designed overlay). Moving or swiping splits the cell under the pointer in half along its long axis — landscape into two columns, portrait into two rows — and each child is filled with the average color of its region. You work the rose into existence as an irreversible mosaic; nothing photographic is drawn until cells are tiny. Soft ticks + short vibrate on each split. Remaining unworked area in the corner.

**genome** — no hidden photo. The swipe *is* the plant. Fast = skinny, noisy, high; slow circles / lingering = fat petals and a held note. `new` reseeds. Tweak the `GENOME` object near the top of the script.

**live** — same division mosaic, sampling the current video frame instead of the still. Default is your camera (“scratch opens you”). Presets: **you** / **seamount** / **reel**. If a stream is idle or blocked, it falls back to camera, then to the rose still.

## Sound & haptic

♪ and ∴ default **on**. First pointer-down unlocks Web Audio (required on iOS). iPhone has no Vibration API — the tick is the stand-in. Nothing is loud; there is no fail state.

Swipe hint (ghost finger + “swipe”) fades after the first stroke.

## Swap the rose

In `digital-rose.html`, replace the `const ROSE = "data:image/…"` string with another data URI (jpeg or png).

The inlined still is a Wikimedia Commons photo: *Pink rose bloom of a climbing rose at Boreham, Essex, England* (Acabashi, CC BY-SA). To use the 2021 mosaic pixels instead, data-URI `/workspace/digital-rose-shots/revealed_final.png` or `f5.png`.

## Genome knobs

`GENOME` at the top of the script: `fastSpeed`, `slowSpeed`, `circleCurv`, `dwellMs`, stem/petal sizes, branch/leaf odds, HSL colors, `tickHzLo` / `tickHzHi`, `holdGain`, `tickGain`.

## Live streams

| preset | URL | notes |
| --- | --- | --- |
| seamount | `https://elem-delta.oceanobservatories.org/out/u/camhd.m3u8` | NSF OOI Axial Seamount. 14 min at 2/5/8/11 Eastern, not 24/7. Empty playlist → fallback. |
| reel | `https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8` | CORS-friendly Mux demo; verified reachable. |
| you | `getUserMedia` | needs permission + https/localhost |

`hls.js` loads from jsDelivr only when an HLS source is chosen. If the CDN is blocked, Safari native HLS still works; otherwise camera / still.

## Taste

Quiet gallery toy. No accounts, no NFT chrome, no analytics.
