# What breaks

H3 is good at motion and atmosphere and unreliable at four specific things. Every item on
this page comes from observable failure, most of it reported by people running the model
in production, and every one of them has a fix that is **shot design or field syntax, not
a longer prompt**. Adding words does not recover a face that is six pixels wide.

---

## 1. Faces in wide shots

The most reported H3 defect, and the one that surprises people most because it does not
improve with resolution.

> "MiniMax heavily distorts faces on wide shots. Distortions happen regardless of input
> res (even at 720p, very bad). Close/medium shots look fine!"
> — Hugging Face `Comfy-Org/MiniMax-H3` discussion #30, *"Why MiniMax H3 Ruins Faces on
> Wide Shots?"*, 25 replies

The mechanism is area, not pixels: **the smaller the head is on screen, the worse it
looks.** There is also a VAE limitation underneath it — encode/decode tests show fine
facial detail is softened before sampling begins, so more denoise steps cannot recover it.

**The fix is the shot list, not the prompt.** MiniMax's own guidance is to generate a
close-up when faces matter, and to keep wide shots for other work. One of the official
worked examples encodes this directly:

```text
Show the face only in close-up or extreme close-up. In wide shots, use back view,
rear three-quarter view, or empty environment shots; never show a distant frontal face.
```

That is a director's instruction, not a model workaround — which is the point. If your
prompt has a character walking away from camera into a wide, put them in a wide and show
the back of their head, and save the identity read for the medium shot.

---

## 2. Audio

H3 generates 32 kHz stereo sound in the same pass as the picture. It is the headline
feature and the least trustworthy layer. Reported failure modes:

- **`non_diegetic_music: N/A` still produces music** a meaningful fraction of the time
  (~20% in community testing).
- **With all three audio references supplied**, creators still report getting "a random
  voice, or not the audio I assign to the characters".
- **Audio artefacts at clip boundaries**, characters speaking gibberish, and lines
  delivered by the wrong speaker.
- **Turbo LoRAs distort audio** badly. Community reports tie this to ComfyUI version drift,
  not the model.
- **Dropping 20 steps to 10 hurt audio badly while barely changing the picture** — the
  audio degrades before the video does, so a step-count cut shows up as a sound problem.
- **Off-screen voiceover animates the mouth** unless you write the second clause. This is
  exactly why the official guide mandates `while his lips remain completely closed`.

**Fix:** name the sounds you want, explicitly, or the mix is a coin toss — `rain ambience,
one soft shutter rattle, no dialogue` beats "add realistic audio" every time. And treat the
audio as a separate deliverable worth re-rolling: if the picture is right and the sound is
wrong, generate again with the same prompt rather than accepting it.

---

## 3. Bracketed camera commands

`[Pan left]`, `[Zoom in]`, `[Static shot]` and the rest are **Hailuo Director** syntax from
the previous generation of models. They are not H3's camera language and they do not work
as operands here.

```text
✘  [Push in] [Slow] she opens the letter
✔  The camera pushes in with small amplitude at slow speed toward the folded letter in her hands.
```

Brackets still appear in H3 prompts as *structure* — `[Shot 1]`, or a creator's own
`[FORMAT]` / `[LOCK]` headers — and that is fine. It is the camera operand form that died.

A related confusion worth separating: **zoom is not push.** Zoom changes focal length with
the camera body stationary; push moves the body through space. "My subject keeps leaving
frame" is usually someone asking for a zoom and describing an outcome instead of asking
for a pull that matches the subject's speed.

---

## 4. Long takes

Anything past 15 seconds is not one shot, and treating it as one is where continuity goes.
Community reports of a single long prompt flattening objects and drifting the scene are
consistent with the model's own limit: H3's duration enum stops at 15.

**Fix:** cut into ≤15 s segments and carry continuity in the prompt rather than in one
generation. Repeated identity, wardrobe and location statements in every segment —
a garment named only in `[Shot 1]` is a known drift source, common enough that an
independent H3 prompt validator ships a rule specifically for it
(`R15-wardrobe-not-restated`).

---

## 5. Undefined or overlapping references

The number-one reported cause of incoherent output:

> "Overlapping roles create an undefined contest between inputs."
> "Overlapping roles blur the assignment of the clip's controls across camera, identity,
> and performance decisions."

Give each input exactly one job. If image 1 is the face and image 2 is the location, say
so; if image 1 is *both*, the model has to guess which one wins when they disagree.

And the counter-intuitive corollary the community keeps rediscovering: **when references
carry identity and motion, the prompt should get shorter, not longer.** The references are
the specification; the prose is the choreography.

---

## 6. The negative-constraint census

A literal list of what creators actually put in `Avoid:` / `No …` tails. It is effectively
H3's defect surface, and a good checklist:

**Identity and body** — face drift · body changes · face morphing · character duplication ·
hairstyle changes · outfit changes · beauty-filter effect · chibi/schoolgirl styling

**Anatomy** — malformed hands · distorted hands

**Motion** — motion blur on stationary objects · morphing geometry · teleportation ·
camera shake

**Text and marks** — unreadable text · distorted typography · logos, labels, signs, UI,
watermarks, licence plates

**Framing** — extreme wide shots · harsh directional shadows · breaking eye contact

---

## 7. What to do instead of adding words

| Symptom | Wrong fix | Right fix |
|---|---|---|
| Face is mush | more detail about the face | move to a closer shot; keep the wide for backs and scenery |
| Motion smears | "no motion blur" | slow the action down in the description |
| Sound is wrong | "add realistic audio" | name every sound; re-roll the take |
| Character drifts | restate the whole design | restate identity **and** wardrobe in every segment |
| Camera ignores you | repeat in brackets | type + amplitude + speed as natural prose |
| References fight | describe both in more detail | give each reference one job |

---

## 8. Provenance, since this page is full of other people's findings

The composite failure list above draws on community reports from Hugging Face discussions,
the open-source prompt validator `ruashots/open-h3-ir`, and the field notes published by
the larger H3 galleries. Where a claim is a single report rather than a pattern, it is
written that way. Nothing here is reconstructed or inferred — if a failure mode is not
backed by someone who hit it, it is not on this page.

---

[← Back to the gallery](../README.md)
