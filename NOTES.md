# Frasi Vive · Il sabato di Giulia (v1.0 pilot)

Live: https://appuccinohub.github.io/frasi-vive/
Repo: https://github.com/AppuccinoHub/frasi-vive  (commit 4961c52)
File: index.html, single self-contained file, 478,116 bytes. The only network request is the song preview, and it happens only when a student taps Play.

## What it is
A 10-card phrase-chunk pilot for Italian 3 Honors. On each card students LISTEN to, READ and SAY one whole chunk, then complete a graded recall task.
- Level 1: presente chunks, plus the Sono / Ero / Sono stata mall trio and a contrast card.
- Level 2: imperfetto vs passato prossimo, including 2 song cards.
- Level 3: type the full chunk from English.
Unlock rule: 3 of 4 correct. Missed cards come back later in the feed. Streak milestones at 3 and 5. Best streak and progress are saved in localStorage, and the app still works if storage is blocked.

## Build
- `src/` holds content.json, app.js, style.css and shell.html.
- `python3 build.py` builds index.html, then copy it to `site/` and push.
- Art: original SVG in `art/scenes.py` rendered to WebP by `art/render.py`. It's vector art because no image generator was available.
- Audio: Kokoro-82M (kokoro-onnx, Apache-2.0), voice if_sara at speed 0.92, MP3 48 kbps with loudnorm. whisper medium scored 10/10 exact (`tts/asr_report.txt`). Piper it_IT paola was rejected (6/10).
- Songs: previews come from the iTunes lookup API. Azzurro (trackId 1775198614) plays 15.9–24.3 s; Volare (trackId 41663237) plays 21.0–28.3 s.

## Tests
`tests/play.py W H [mobile] [--url URL] [--block-net] [--tag]`, `tests/storage_blocked.py`, `tests/check_chunks.py`.

## Open items
- Swap in generated scene art if an image tool becomes available.
- Apple could change preview URLs. The app re-looks up the trackId, and if that fails it falls back to the lyric line.
