# What we measured

Most H3 pages tell you what the model can do. This one says what it did, at what size, in
how long, for how much — because the documented spec and a real render do not agree, and
the disagreements are the useful part.

Every number below is from a real request, recorded with the file it produced.

---

## 1. Two documented sizes, and one common mistake

MiniMax documents **two** output sizes for H3: `768P` and `2K`. The official `resolution`
enum on the V2 endpoint is `[480P, 768P, 2K]`, and of those `MiniMax-H3` accepts only
**`768P` and `2K`**:

- **`480P` belongs to `MiniMax-H3-Max`** — a different model, with its own duration range
  (5–15 s against H3's 4–15 s).
- **`1080P` is not an H3 value at all.** It belongs to the legacy `MiniMax-Hailuo-2.3` and
  `MiniMax-Hailuo-02` line on the older v1 endpoints. Searching the entire official English
  documentation for `4K` and for `native1080` returns **zero hits**; the only `4K` string
  anywhere in it is inside a user-authored example prompt.

So a vendor page advertising "H3 at 1080p" is describing that vendor's own pipeline, not the
model. That is worth knowing before you pick a size for a project.

### `768P` is the ceiling of the open weights

The downloadable checkpoints render at a default short edge of **768 px**. The 2K path comes
from `H3-Regenerate-2K` — a second pass that feeds the 768P result and the original context
back through H3 — and MiniMax states it is **not** in the open-source release. The
prompt-preprocessing layer, `H3-Context-IR`, is hosted-only too, and the model card calls it
"critical to the quality of the final output".

So the local model is a 768P generator, and both of the modules that make the hosted product
better are closed. Labelling a clip with a resolution is labelling the *pipeline*, not the
checkpoint.

### The rest of the spec

| | |
|---|---|
| Duration | **4–15 s**, integer (`MiniMax-H3-Max`: 5–15) |
| Aspect ratios | `adaptive`, `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16` |
| Text-to-video ratio | concrete values only — `adaptive` is rejected |
| Output | 24 fps, 32 kHz stereo audio |
| Prompt length | 7,000 characters per `text` item |
| References | 9 images, 3 videos, 3 audio clips; 12 files total |

---

## 2. The measured matrix

Fourteen requests, every one of them checked against the MP4 that came back.

| Case | Requested | **Actual output** | fps | Duration | Audio | Wall time |
|---|---|---|---|---|---|---|
| t2v 480p horizontal | `480p横` 1 s | **864 × 480** | 24 | 1.625 s | ✅ AAC | 81 s |
| t2v 480p horizontal | `480p横` 5 s | 864 × 480 | 24 | 5.167 s | ✅ | 67 s |
| t2v 480p square | `480p(1:1)` 5 s | **480 × 480** | 24 | 5.167 s | ✅ | 67 s |
| t2v 768p horizontal | `768p横` 5 s | **1344 × 768** | 24 | 5.167 s | ✅ | 151 s |
| t2v 768p vertical | `768p竖` 5 s | **768 × 1344** | 24 | 5.167 s | ✅ | 136 s |
| t2v 1080p horizontal | `1080p横` 5 s | **1920 × 1056** | 24 | 5.167 s | ✅ | **475 s** |
| ref 1 image, 768p | `768p横` 5 s | 1344 × 768 | 24 | 5.167 s | ✅ | 149 s |
| ref 3 images, 480p vertical | `480p竖` 5 s | **480 × 864** | 24 | 5.167 s | ✅ | 88 s |
| ref 1 image, 1080p | `1080p横` 5 s | 1920 × 1056 | 24 | 5.167 s | ✅ | 345 s |
| ref 1 image, 1080p square | `1080p(1:1)` 5 s | **1056 × 1056** | 24 | 5.167 s | ✅ | 87 s |
| first + last frame, 768p | `768p横` 5 s | 1344 × 768 | 24 | 5.167 s | ✅ | 198 s |
| image + audio reference, 768p | `768p横` 5 s | 1344 × 768 | 24 | 5.167 s | ✅ | 165 s |
| lip-sync, 768p vertical | `768p竖` | 768 × 1344 | 24 | 1.625 s | ✅ | 197 s |
| 2K | 2K 4 s | **2560 × 1440** | 24 | 4 s | ✅ | — |
| non-existent size | `2K横` 5 s | **rejected** | — | — | — | 0.1 s |

### What the table says

**`1080P` is 1920 × 1056, not 1920 × 1080.** The model converges on a pixel budget rather
than a height. Same at square: `1080p(1:1)` returns **1056 × 1056**, not 1080 × 1080. If you
are cutting into a 1080p timeline the height will not match, and you will need to scale or
letterbox.

**Every clip came back with a native audio track** — AAC, stereo, 32 kHz, the same duration
as the picture. H3 generates picture and sound in one pass and there is **no API parameter to
turn it off**. That is the headline feature, not a side effect.

**Requested duration is not delivered duration.** 5 s returns 5.167 s; 1 s returns 1.625 s.
The model snaps to a frame grid — 17k + 5 frames at 24 fps — so short requests round up.

**1080P costs roughly seven times the wall time of 480P** for the same five seconds: 475 s
against 67 s. Not 2.5×, which is what the size ratio would suggest. In a batch, this
dominates everything else.

**An unknown size is rejected loudly**, never silently substituted. Asking for a tier the
endpoint does not publish returns a parameter error naming the valid options.

---

## 3. What each size is for

| | Output | Time for 5 s | Use it when |
|---|---|---|---|
| **480P** | 864 × 480 | ~70 s | storyboarding, and checking a prompt's motion before paying for the take |
| **768P** | 1344 × 768 | ~150 s | **the default.** The model's native size, and where the price/perf curve lives |
| **1080P** | 1920 × 1056 | ~475 s | a hero clip with fine detail that survives the downscale |
| **2K** | 2560 × 1440 | — | delivery resolution, or anything driven by a reference video |

The useful move is **not** to pick one. Write the prompt at 480P, look at the motion, fix the
prompt, then render the take at 768P. A 480P test costs a fraction of a 1080P render and
takes a fifth of the time.

---

## 4. Modes

H3 accepts text, images, video and audio in a unified multimodal input, and the modes are
not freely mixable.

| Mode | Accepts | Note |
|---|---|---|
| **Text to video** | text only | ratio is required and **cannot** be `adaptive` |
| **Image to video** | up to 2 frames (first and/or last) | ratio is **always** `adaptive`, taken from the image |
| **Reference to video** | up to 9 images, 3 video clips, 3 audio clips | ratio optional, defaults to `adaptive` |
| **Video to video** | a source clip among the references | needs the multimodal endpoint, not the frame path |

**First/last-frame mode and reference mode are mutually exclusive in one request.** If any
reference image, video or audio role appears, `first_frame` and `last_frame` must not — and
vice versa. Every request also needs one non-empty `text` item, even when the references
carry everything.

---

## 5. How to reproduce

Each case directory carries a `generation.json` with the task id, the requested settings, the
measured output, the wall time and the cost, so every claim on this page can be traced to the
file it came from.

```bash
ffprobe -v error -show_entries \
  stream=codec_type,codec_name,width,height,r_frame_rate,sample_rate,channels \
  -show_entries format=duration,size \
  showcase/01-lantern-canal/768p-h.mp4
```

---

[← Back to the gallery](../README.md)
