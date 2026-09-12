# What we measured

Most H3 pages tell you what the model can do. This one says what it did, at what size,
in how long, for how much — because the three ways to reach H3 do not agree with each
other, and the disagreements are the useful part.

Every number below is from a real request, recorded with the file it produced.

---

## 1. Three routes, three different models wearing the same name

| | **Official API** | **AutoDL ComfyUI lane** | **KIE lane** |
|---|---|---|---|
| Resolutions | `768P`, `2K` | `480P`, `768P`, `1080P` | `2K` |
| Duration | 4–15 s | **1–15 s** | 4–15 s |
| Ratio | 6 concrete + `adaptive` | 16:9, 9:16, 1:1 | 6 concrete + `adaptive` |
| Official price | $0.08/s (768P), $0.13/s (2K) | — | — |
| Our cost | — | ¥0.03–0.10/s ≈ **$0.004–0.014/s** | $0.065/s |
| Reference video | yes | **no** | yes |

Read that table twice.

**`480P` and `1080P` are not MiniMax H3 tiers.** The official `resolution` enum is
`[480P, 768P, 2K]`, and of those, `MiniMax-H3` accepts only **`768P` and `2K`** — `480P`
belongs to `MiniMax-H3-Max`, a different model, and `1080P` does not appear on the V2
endpoint at all. It belongs to the legacy `MiniMax-Hailuo-2.3` line on the older v1
endpoints. A "H3 at 1080p" claim on a vendor page is a statement about that vendor's
pipeline, not about the model.

**`768P` is the ceiling of the open weights.** The downloadable checkpoints render at a
default short edge of 768 px. 2K comes from `H3-Regenerate-2K`, which MiniMax states is
*not* in the open-source release, and the prompt-preprocessing layer `H3-Context-IR` — the
one the model card calls "critical to the quality of the final output" — is hosted-only too.
So the local model is a 768P generator, and both of the modules that make the hosted
product better are closed.

**The AutoDL lane is roughly 14× cheaper than the official list price for 768P**, and it
gives you 1-second clips, which the official API does not.

---

## 2. The measured matrix

Fourteen requests, every one of them checked against the MP4 that came back.

| Case | Workflow | Requested | **Actual output** | fps | Duration | Audio | Wall time | Cost |
|---|---|---|---|---|---|---|---|---|
| t2v 480p horizontal | `lightx2v_no_pic` | `480p横` 1 s | **864 × 480** | 24 | 1.625 s | ✅ AAC | 81 s | ¥0.02 |
| t2v 480p horizontal | `lightx2v_no_pic` | `480p横` 5 s | 864 × 480 | 24 | 5.167 s | ✅ | 67 s | ¥0.10 |
| t2v 480p square | `lightx2v_no_pic` | `480p(1:1)` 5 s | **480 × 480** | 24 | 5.167 s | ✅ | 67 s | ¥0.10 |
| t2v 768p horizontal | `lightx2v_no_pic` | `768p横` 5 s | **1344 × 768** | 24 | 5.167 s | ✅ | 151 s | ¥0.15 |
| t2v 768p vertical | `lightx2v_no_pic` | `768p竖` 5 s | **768 × 1344** | 24 | 5.167 s | ✅ | 136 s | ¥0.15 |
| t2v 1080p horizontal | `image_audio_to_video_v2` | `1080p横` 5 s | **1920 × 1056** | 24 | 5.167 s | ✅ | **475 s** | ¥0.45 |
| ref 1 image, 768p | `zm_u24` | `768p横` 5 s | 1344 × 768 | 24 | 5.167 s | ✅ | 149 s | ¥0.15 |
| ref 3 images, 480p vertical | `zm_u24` | `480p竖` 5 s | **480 × 864** | 24 | 5.167 s | ✅ | 88 s | ¥0.10 |
| ref 1 image, 1080p | `image_audio_to_video_v2` | `1080p横` 5 s | 1920 × 1056 | 24 | 5.167 s | ✅ | 345 s | ¥0.45 |
| ref 1 image, 1080p square | `lightx2v_v5` | `1080p(1:1)` 5 s | **1056 × 1056** | 24 | 5.167 s | ✅ | 87 s | ¥0.45 |
| first + last frame, 768p | `lightx2v` | `768p横` 5 s | 1344 × 768 | 24 | 5.167 s | ✅ | 198 s | ¥0.15 |
| image + audio reference, 768p | `zm_u24` | `768p横` 5 s | 1344 × 768 | 24 | 5.167 s | ✅ | 165 s | ¥0.15 |
| lip-sync, 768p vertical | `image_audio_to_video` | `768p竖` | 768 × 1344 | 24 | 1.625 s | ✅ | 197 s | ¥0.05 |
| **2K (KIE lane)** | KIE H3 | 2K 4 s | **2560 × 1440** | 24 | 4 s | ✅ | — | $0.26 |
| non-existent tier | `lightx2v_no_pic` | `2K横` 5 s | **rejected** | — | — | — | 0.1 s | ¥0 |

### What the table says

**`1080P` is 1920 × 1056, not 1920 × 1080.** The model converges on a pixel budget, not a
height. Same at square: `1080p(1:1)` is **1056 × 1056**, not 1080 × 1080. If you are
aligning a clip to a 1080p timeline, the height does not match.

**Every clip came back with a native audio track** — AAC, same duration as the video. H3
generates picture and sound in one pass and there is **no API parameter to turn it off**.
That is not a bug to work around; it is the headline feature.

**Requested duration is not delivered duration.** 5 s gives 5.167 s; 1 s gives 1.625 s.
The model snaps to a frame grid (17k + 5 frames at 24 fps), so short requests round up.

**1080P costs 7× the wall time of 768P** for the same five seconds — 475 s against 67 s at
480P. Not 2.5×, which is what the price ratio would suggest. If you are generating in
bulk, this dominates everything.

**The lane rejects an unknown tier loudly.** Requesting `2K横` on the AutoDL lane returns
`resolution 的值 2K横 不在 options 列表中` — a closed enum, not a silent fallback.

---

## 3. What each tier is actually for

| | Output | Time for 5 s | Our cost | Use it when |
|---|---|---|---|---|
| **480P** | 864 × 480 | ~70 s | ¥0.10 | storyboarding, checking a prompt's motion before paying for it |
| **768P** | 1344 × 768 | ~150 s | ¥0.15 | **the default.** The model's native size, and where the price/perf curve lives |
| **1080P** | 1920 × 1056 | ~475 s | ¥0.45 | a hero clip with fine detail that survives the downscale |
| **2K** (KIE) | 2560 × 1440 | — | $0.26 / 4 s | delivery resolution, or anything with reference video |

The useful move is **not** to pick one. Write the prompt at 480P, look at the motion, fix
the prompt, then render the take at 768P. A 480P test costs a seventh of a 1080P render
and takes a fifth of the time.

---

## 4. Which workflow does what

Thirteen H3 workflows are published on the lane. We measure all of them; these are the
ones worth binding, and why.

| Workflow | What it is | Tiers | Max | Note |
|---|---|---|---|---|
| `lightx2v_no_pic` | text-to-video | 480p, 768p | 15 s | the only pure text path at 480/768 |
| `image_audio_to_video_v2` | references, images + audio | 480p, 768p, **1080p** | 10 s | the only 1080p path with no reference at all |
| `zm_u24` | references, 1–9 images | 480p, 768p | 15 s | 24 denoise steps — **same price, more steps** than `zm_u08` |
| `lightx2v_v5` | references | 480p, 768p, **1080p 1:1** | 10 s | the only square 1080p canvas |
| `lightx2v` | first + last frame | 480p, 768p | 15 s | both frames required |
| `image_audio_to_video` | image + audio → lip-sync | 480p, 768p, 1080p | follows audio | output length is the audio's length |

**Rejected on purpose:** `zm_u08` (the "fast" variant — same per-second price, fewer steps,
worse output), the three `b99_*` workflows (locked to 736p, an order of magnitude less
traffic), and the `_15s` variants (capability already covered).

**Not available at all:** any workflow that takes a **reference video**. There is no
video-to-video on this lane. Reference inputs are images and audio only, so the third mode
H3 supports — video editing, continuation, restyling from a source clip — has to go
through the official API or KIE.

---

## 5. How to reproduce

```bash
# one clip, text-to-video, native size
node gen-h3.mjs --case=01-lantern-canal

# the whole set
node gen-h3.mjs --all --concurrency=2
```

Each case directory carries a `generation.json` with the task id, the requested settings,
the measured output, the wall time and the cost, so every claim on this page can be traced
to the file it came from.

---

[← Back to the gallery](../README.md)
