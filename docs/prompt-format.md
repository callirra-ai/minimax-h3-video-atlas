# The prompt format MiniMax actually documents

Almost every H3 prompt you will find in the wild is a paragraph. MiniMax's own guides
define something more specific: a **named-field document**. This page is the format,
quoted from the official sources, plus the parts the community gets wrong.

Sources: `docs/VIDEO_PROMPT_WRITING_GUIDE_base_en.md` and `..._ref_en.md` on the
[MiniMax-H3 model card](https://huggingface.co/MiniMaxAI/MiniMax-H3), the
[Video Generation guide](https://platform.minimax.io/docs/guides/video-generation.md),
and the [H3 Feature Highlights](https://platform.minimax.io/docs/guides/video-prompt.md).

---

## 1. Two shapes, chosen by what you feed the model

| What you are doing | Shape | Sections |
|---|---|---|
| Text-to-video, or first/last-frame | **base** | 3 |
| Reference-driven (images, video, audio) | **full-reference** | 6 |

**Base** — the three fields, in this order:

```text
integrated_multimodal_description: [Shot 1] ...

overall_soundscape: ...

non_diegetic_music: ...
```

**Full-reference** — six sections, in this order:

```text
subject_definitions:
summary:
retention_analysis:
detailed_description:
overall_soundscape:
non_diegetic_music:
```

The field names are not decoration. MiniMax trains the model against this structure, and
the guide's own worked examples use it verbatim.

---

## 2. What each field is for

| Field | Holds | Does not hold |
|---|---|---|
| `integrated_multimodal_description` | visuals, action, shots, speakers, dialogue, singing, diegetic audio, on the timeline | — |
| `overall_soundscape` | ambience, physical action sounds, non-verbal human sounds | **dialogue** |
| `non_diegetic_music` | score the characters cannot hear | anything diegetic |

Write `N/A` when a field is genuinely empty. Do not pad it.

---

## 3. Shots, and the one rule about `[Shot 1]`

`[Shot 1]` carries **no timestamp**. Every later shot does:

```text
[Shot 1] ... the camera holds a static shot as she opens the folded letter ...
[Shot 2] At 00:03.500, the camera cuts to a tight close-up of the handwriting ...
```

Cut on the action, not before it — the official examples cut *when* the water strikes the
bed, never ahead of it.

---

## 4. Camera: type + amplitude + speed, as prose

The official vocabulary:

| | |
|---|---|
| **Type** | Zoom In/Out · Push In/Pull Out · Pan Left/Right · Truck Left/Right · Tilt Up/Down · Pedestal Up/Down · Arc Shot · Tracking Shot · Static Shot · Shake Slightly/Strongly · POV · Roll Clockwise/Counterclockwise |
| **Amplitude** | `with small amplitude` · `with large amplitude` |
| **Speed** | `at slow speed` · `at fast speed` |

**The rule that matters:** write the move as a natural action inside the sentence, not as
a label stacked at the end.

```text
✔  The camera pushes in with small amplitude at slow speed toward the folded letter in her hands.
✘  [Push in] [Slow] Letter in her hands.
```

Medium amplitude and normal speed are the defaults — leave them out.

**Zoom is not push.** Zoom changes focal length with the body stationary; push moves the
body. Practitioners report that "the subject keeps leaving frame" is usually this
distinction, not a length problem: switch from outcome language (`the entire subject
remains visible`) to camera grammar (`the camera pulls out with large amplitude at the
same speed as the subject walks forward`).

### Bracket commands are dead

`[Pan left]`, `[Zoom in]` and the rest belong to the earlier **Hailuo Director** models.
They are not H3's camera syntax. Brackets survive in H3 prompts only as *structure* —
`[Shot N]`, or a creator's own `[FORMAT]` / `[LOCK]` section headers — never as camera
operands.

---

## 5. References are named with angle brackets

| Label | Means |
|---|---|
| `<Subject N>` | reusable visible content: a character, animal, object, scene, costume, prop, interface, style, action, expression, pose |
| `<Picture N>` | a reference image used as a concrete first frame, keyframe, last frame or composition anchor |
| `<Video N>` | whole-video relationships: edit source, continuation start, temporal structure |
| `<Audio N>` | a standalone audio asset, or the synchronised audio track of a reference video |

Gotchas from the official guide:

- `<Video N>` and `<Audio N>` are **numbered independently** and do not pair by index.
- An ordinary reference video does **not** create `<Audio N>` merely because the file has sound.
- If an image only *defines* a character, scene or style, do **not** give it its own
  `<Picture N>` — cite it inside the `<Subject N>` definition.

### `@image1` is not H3 syntax

The community writes `@image1`, `@Image 1`, `[Image1]` and bare `Image 1`. None of these
are MiniMax's. `<Picture 1>` is. Tooling that accepts `@image1` is resolving it to
`<Picture 1>` on your behalf; the mapping is a convenience, not the format.

`<Image 1>` in particular is a defect, not a synonym.

### Keyframe alignment goes first

When you condition on frames, the alignment statement is the **first line** of the
prompt, then a blank line:

```text
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] ...
```

With two frames:

```text
How the reference pictures align with the target video — Picture 1 (from Shot 1) aligns with the 0.00-second mark of the target video; Picture 2 (from Shot N) aligns with the S.SS-second mark of the target video.
```

---

## 6. Dialogue and sound

**Speaker IDs.** A speaker gets a stable ID, `(S1)`, `(S2)`, and keeps it across shots.
Simultaneous speech is `(S1,S2)`. Non-vocal characters get no ID.

**Dialogue lives in the shot description**, inside `<d>` with a language tag, punctuation
preserved exactly:

```text
The young woman with a quiet, breathy voice (S1) says: <d>[English] I get off at the next station.</d>
The two children (S1,S2) shout together, <d>[English] Wait for us!</d>
```

**Off-screen voiceover needs two clauses.** Without the second, the model animates the mouth:

```text
The man (S1) says in an off-screen voiceover: <d>[English] I still remember that road.</d> while his lips remain completely closed.
```

**A line that crosses a cut** gets `<scenetrans>` at both connecting points plus explicit
continuity wording. A line truncated by the end of the video gets `<cutoff>`.

**Binding a sound to a moment in the frame** — timestamp it:

```text
[5.4s] The glass touches the table with a quiet ceramic click.
```

**On-screen text** goes in English double quotes, verbatim and untranslated:

```text
A red neon sign reading "营业中" glows above the doorway.
```

---

## 7. Full-reference: the retention vocabulary

`retention_analysis` uses fixed English enums, not adjectives:

| Visual | Audio |
|---|---|
| `fully_preserved` | `fully_copy` |
| `partially_preserved` | `partially_copy` |
| `attribute_transfer` | `reference` |
| `weak_reference` | `weak_reference` |

`summary` opens with a bracketed task tag, e.g. `[video editing + audio reference + audio reuse]`.

`detailed_description` targets **350–500 English words**.

---

## 8. Limits

| | |
|---|---|
| Prompt length | **7,000 characters** per `text` item |
| Duration | **4–15 s**, integer (`MiniMax-H3-Max`: 5–15) |
| Aspect ratio | `adaptive`, `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16` |
| Text-to-video ratio | concrete values only — `adaptive` is rejected |
| Image/video/audio references | 9 / 3 / 3, 12 files total |
| Reference clip length | 2–15 s each, ≤ 15 s per medium |
| Output | 24 fps, 32 kHz stereo audio |
| Every request | needs one non-empty `text` item, even with references |

---

## 9. Worked example

A complete base-shaped prompt, exactly as it would be sent:

```text
integrated_multimodal_description: [Shot 1] Live-action, cinematic, shallow depth of field. A single paper lantern drifts down a narrow canal at night in a southern Chinese water town, seen from a low camera just above the waterline. The lantern's warm orange glow is the only light source near the camera, and it throws a soft moving pool of colour across the wet stone walls on either side. The camera holds a static shot, letting the lantern travel from the upper third of the frame down toward the lower right, then the camera pushes in with small amplitude at slow speed as the lantern passes and its reflection breaks apart on the ripples and reforms. Background: whitewashed houses with dark tiled roofs, a few windows still lit. Light rain has just stopped; the air is thick and the far end of the canal dissolves into mist.

overall_soundscape: Quiet night in a water town. Water laps gently against stone, the rain that has just stopped drips from the eaves into the canal at irregular intervals, and the lantern's paper and thin bamboo frame creak faintly as it turns. A distant dog barks once, and a single bicycle bell rings far away.

non_diegetic_music: A sparse solo guzheng melody at a slow tempo, played with long pauses between phrases, the strings allowed to ring and decay. No percussion.
```

That is [case 01](../showcase/01-lantern-canal/) in this repository, and `showcase/01-lantern-canal/prompt.txt`
is byte-identical to it.

---

[← Back to the gallery](../README.md)
