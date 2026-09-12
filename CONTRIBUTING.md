# Contributing

Two kinds of contribution, and they have different rules.

---

## Adding one of your own clips

Most welcome. Open a PR with a new directory under `showcase/`:

```
showcase/<nn>-<slug>/
  prompt.txt          the complete prompt, exactly as sent
  poster.jpg          a still from the clip, ~1280px wide
  <tier>.mp4          the clip (keep it under ~10 MB if you can)
  generation.json     the machine-readable record — see below
  README.md           optional: what it is, how to adapt it, what to watch
```

`generation.json` looks like this. The `measured` block must be what came **back**,
not what you asked for — that distinction is the point of this repository.

```json
{
  "slug": "12-your-case",
  "title": "Your Case Title",
  "mode": "text-to-video",
  "workflow": "minimax_h3_lightx2v_no_pic",
  "taskId": "…",
  "requested": { "resolution": "768p横", "duration": 6 },
  "measured": {
    "width": 1344, "height": 768, "fps": 24,
    "durationSec": 6.167, "hasAudio": true, "audioHz": 32000,
    "fileBytes": 3145728
  },
  "cost": { "cny": 0.24, "wallSec": 152 },
  "file": "768p.mp4"
}
```

You can produce it automatically — `ffprobe -v error -show_entries stream=… your.mp4`
gives you width, height, fps, duration and the audio track.

**What gets rejected:** a clip with no prompt, a clip whose prompt is not the one that
produced it, and a clip with invented settings. If you no longer have the exact prompt,
say so and leave it out of the gallery rather than reconstructing it.

---

## Adding a community case

This is where most ground is to be gained, and where the rules are strict.

**A community entry must have a prompt its creator actually published.** Not one you
inferred, not one written by describing the video to a vision model, not one "close
enough". If the creator did not post the prompt, the entry cannot be included — there is
nothing to include. A reconstruction describes an *output*; presenting it as the creator's
prompt is a fabrication, and it is the single biggest credibility problem in this space.

What a community PR needs:

| Field | Required | Notes |
|---|---|---|
| `sourceUrl` | yes | the creator's own post — X, Bilibili, their site |
| `author` | yes | their handle as it appears on the source |
| `prompt` | yes | **byte-for-byte** as published, including typos and bracket tags |
| `promptProvenance` | yes | `creator-verbatim` or `official-verbatim` |
| `title` / `titleEn` | yes | |
| `mode` | yes | `T2VA` · `Ref2VA` · `FL2VA` |
| `duration` · `resolution` · `aspectRatio` | if stated | write `not stated by the creator` rather than guessing |
| `posterUrl` | yes | a still for the gallery |
| `mediaUrl` | optional | link only — **do not download someone else's video into this repo** |

**Video is never re-hosted here.** Every entry links to the creator's own post. Posters
are stored locally only so the gallery does not break when a third-party host disappears,
and the poster links straight back to the source.

### Removal

If you are a creator and want your work out of this repository, open an issue titled
`removal: <your handle>` and it will be removed without discussion. You do not need to
give a reason.

### Broken links

Posters, source links and prompts all rot. If you find a dead one, an issue with the case
name is enough.

---

## What we will not merge

- Reconstructed or inferred prompts, labelled or unlabelled.
- Prompts copied from another gallery without checking they trace back to the creator.
- Clips or prompt text taken from a repository whose licence does not permit it.
- Anything that presents a vendor's pipeline result as the model's capability — a
  "1080P H3" clip is fine, but it must say what produced it, because `1080P` is not an
  H3 size.

---

## Style

Prompts are quoted verbatim. Do not fix anyone's spelling, do not normalise `@image1` to
`<Picture 1>`, do not reformat their whitespace. If a prompt uses a convention the model
does not formally accept, that is a fact about the prompt worth preserving — the gallery
records what people write, not what it wishes they wrote.
