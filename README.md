# unchained-labs.github.io

The Unchained Labs landing page — **[unchained-labs.github.io](https://unchained-labs.github.io/)**.

Served from the root of `main` (that is the convention for a `<org>.github.io`
repo, not `/docs`).

## What is here

```
index.html            the page
assets/tokens.css     vendored from Unchained-Labs/branding
assets/brand.css      vendored from Unchained-Labs/branding
assets/video/*.mp4    the terminal demos, one per tool
assets/video/*-poster.jpg   first-paint poster per demo
```

`tokens.css` and `brand.css` are **vendored, not authored here**. If a colour
needs to change it changes in
[branding](https://github.com/Unchained-Labs/branding) and is re-copied — that
repo wins.

## The videos

Every demo is real CLI output, rendered frame by frame by
[`branding/tools/video/mkvideo.py`](https://github.com/Unchained-Labs/branding/tree/main/tools/video)
from a cast file. Nothing is screen-captured and nothing is invented: a promo
video with fabricated output would be a lie told in the most persuasive available
medium.

Only the hero video autoplays. The six per-tool clips use `preload="none"` with a
poster and start via `IntersectionObserver` when they scroll into view — six
autoplaying videos would be ~1.9MB on first load. `prefers-reduced-motion` pauses
everything and leaves the posters.

## Rebuilding a demo

```sh
git clone https://github.com/Unchained-Labs/branding
cd branding/tools/video
python3 mkvideo.py casts/graphlint.json /tmp/out
```

Then copy `/tmp/out/graphlint.mp4` here and regenerate its poster:

```sh
ffmpeg -ss 15.5 -i assets/video/graphlint.mp4 -frames:v 1 /tmp/p.png
convert /tmp/p.png -resize 900x -quality 82 assets/video/graphlint-poster.jpg
```

## Licence

MIT for the page and the tooling. The Unchained Labs name and marks are not —
see [TRADEMARK.md](https://github.com/Unchained-Labs/branding/blob/main/TRADEMARK.md).
