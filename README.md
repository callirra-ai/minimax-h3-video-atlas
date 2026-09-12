<div align="center">

# MiniMax H3 Prompt Atlas

**50 prompts for `MiniMax-H3`, each with the clip it produced — 40 curated from the creators who published them, 10 rendered here with the settings, wall time and cost measured — plus the prompt format MiniMax actually documents.**

<img src="https://img.shields.io/badge/model-MiniMax-H3-412991?style=flat-square" alt="model: MiniMax-H3">
<img src="https://img.shields.io/badge/prompts-50-0969da?style=flat-square" alt="prompts: 50">
<img src="https://img.shields.io/badge/community%20cases-40-8250df?style=flat-square" alt="community cases: 40">
<img src="https://img.shields.io/badge/ours%2C%20measured-10-1f9c6b?style=flat-square" alt="ours, measured: 10">
<img src="https://img.shields.io/badge/sizes%20compared-4-bf8700?style=flat-square" alt="sizes compared: 4">
<img src="https://img.shields.io/badge/licence-CC%20BY%204.0-555555?style=flat-square" alt="licence: CC BY 4.0">
<img src="https://img.shields.io/github/stars/callirra-ai/minimax-h3-video-atlas?style=flat-square&label=stars&color=bf8700" alt="stars">
<img src="https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square" alt="PRs welcome">

<sub><b>Start here</b> · <a href="#the-prompt-format">Prompt format</a> · <a href="#our-cases-measured">Measured cases</a> · <a href="#community-gallery">Community gallery</a> · <a href="#the-size-comparison">Size comparison</a> · <a href="#what-breaks">What breaks</a></sub>

**[▶ Try any prompt in this repository — it opens with everything already filled in](https://callirra.com/minimax-h3?utm_source=github&utm_medium=h3-atlas&utm_campaign=home)**

<sub>Every entry has its own deep link. Each fills the form; none of them submits it.</sub>

</div>

---

## Two sizes, and one common mistake

MiniMax documents **two** output sizes for H3: `768P` and `2K`. The official
`resolution` enum is `[480P, 768P, 2K]`, and of those `MiniMax-H3` accepts only
**`768P` and `2K`** — `480P` belongs to `MiniMax-H3-Max`, a different model, and
**`1080P` is not an H3 value at all.** It belongs to the legacy Hailuo 2.3 line on the
older v1 endpoints. A page advertising "H3 at 1080p" is describing that vendor's pipeline,
not the model.

**`768P` is the ceiling of the open weights.** The downloadable checkpoints render at a
default short edge of 768 px. The 2K path and the prompt-preprocessing layer are both
hosted-only, and MiniMax says so in its own release notes.

**Duration is 4–15 seconds, integer.** Aspect ratios are `adaptive`, `21:9`, `16:9`,
`4:3`, `1:1`, `3:4`, `9:16` — and text-to-video may not use `adaptive`.

**[The request matrix and the size comparison →](docs/what-we-measured.md)**

---

## The prompt format

MiniMax does not ask for a paragraph. It documents a **named-field document**, and the
model is trained against it.

**Base** — text-to-video and first/last-frame — three fields, in this order:

```text
integrated_multimodal_description: [Shot 1] ...

overall_soundscape: ...

non_diegetic_music: ...
```

**Full-reference** — six sections, in order: `subject_definitions` →
`summary` → `retention_analysis` → `detailed_description` →
`overall_soundscape` → `non_diegetic_music`.

**[The complete format — camera vocabulary, reference labels, dialogue syntax, field rules →](docs/prompt-format.md)**

Three things most prompts get wrong, all covered there:

- Camera moves are **type + amplitude + speed written as natural prose** —
  `The camera pushes in with small amplitude at slow speed toward the folded letter.`
  Bracket commands like `[Pan left]` belong to the **previous** generation of Hailuo models
  and do not work as operands here.
- References are labelled **`<Picture 1>`**, `<Subject 1>`, `<Video 1>`, `<Audio 1>` —
  **not** `@image1`, and `<Image 1>` is a defect, not a synonym.
- An off-screen voiceover needs a second clause — `while his lips remain completely
  closed` — or the model animates the mouth.

---

## Our cases, measured

Ten clips rendered for this repository at 768P and 1080P. Every
settings line under a clip is **what came back**, not what was asked for, and the machine
readable record sits next to each prompt in `generation.json`.

### 01 · Lantern on a Canal

<sub>Cinematic &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 5.17s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/01-lantern-canal/768p-h.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/01-lantern-canal/preview.webp" alt="Lantern on a Canal — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/01-lantern-canal/768p-h.mp4">watch the full 5.17s clip (3.2 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 6s &nbsp;·&nbsp; rendered in 512s &nbsp;·&nbsp; ¥0.2 &nbsp;·&nbsp; 3.2 MB</sub>

One light source, one moving subject, one small push. Written in the official three-field format — this is the entry to read if you only read one.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Live-action%2C+cinematic%2C+shallow+depth+of+field.+A+single+paper+lantern+drifts+down+a+narrow+canal+at+night+in+a+southern+Chinese+water+town%2C+seen+from+a+low+camera+just+above+the+waterline.+The+lantern%27s+warm+orange+glow+is+the+only+light+source+near+the+camera%2C+and+it+throws+a+soft+moving+pool+of+colour+across+the+wet+stone+walls+on+either+side.+The+camera+holds+a+static+shot%2C+letting+the+lantern+travel+from+the+upper+third+of+the+frame+down+toward+the+lower+right%2C+then+the+camera+pushes+in+with+small+amplitude+at+slow+speed+as+the+lantern+passes+and+its+reflection+breaks+apart+on+the+ripples+and+reforms.+Background%3A+whitewashed+houses+with+dark+tiled+roofs%2C+a+few+windows+still+lit.+Light+rain+has+just+stopped%3B+the+air+is+thick+and+the+far+end+of+the+canal+dissolves+into+mist.%0A%0Aoverall_soundscape%3A+Quiet+night+in+a+water+town.+Water+laps+gently+against+stone%2C+the+rain+that+has+just+stopped+drips+from+the+eaves+into+the+canal+at+irregular+intervals%2C+and+the+lantern%27s+paper+and+thin+bamboo+frame+creak+faintly+as+it+turns.+A+distant+dog+barks+once%2C+and+a+single+bicycle+bell+rings+far+away.%0A%0Anon_diegetic_music%3A+A+sparse+solo+guzheng+melody+at+a+slow+tempo%2C+played+with+long+pauses+between+phrases%2C+the+strings+allowed+to+ring+and+decay.+No+percussion.&duration=6&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=01-lantern-canal)**

```text
integrated_multimodal_description: [Shot 1] Live-action, cinematic, shallow depth of field. A single paper lantern drifts down a narrow canal at night in a southern Chinese water town, seen from a low camera just above the waterline. The lantern's warm orange glow is the only light source near the camera, and it throws a soft moving pool of colour across the wet stone walls on either side. The camera holds a static shot, letting the lantern travel from the upper third of the frame down toward the lower right, then the camera pushes in with small amplitude at slow speed as the lantern passes and its reflection breaks apart on the ripples and reforms. Background: whitewashed houses with dark tiled roofs, a few windows still lit. Light rain has just stopped; the air is thick and the far end of the canal dissolves into mist.

overall_soundscape: Quiet night in a water town. Water laps gently against stone, the rain that has just stopped drips from the eaves into the canal at irregular intervals, and the lantern's paper and thin bamboo frame creak faintly as it turns. A distant dog barks once, and a single bicycle bell rings far away.

non_diegetic_music: A sparse solo guzheng melody at a slow tempo, played with long pauses between phrases, the strings allowed to ring and decay. No percussion.
```

[Prompt file](showcase/01-lantern-canal/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/01-lantern-canal/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/01-lantern-canal/768p-h.mp4)

---

### 02 · Alley After Rain

<sub>Cinematic &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 5.17s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/02-alley-after-rain/768p-h.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/02-alley-after-rain/preview.webp" alt="Alley After Rain — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/02-alley-after-rain/768p-h.mp4">watch the full 5.17s clip (8.4 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 5s &nbsp;·&nbsp; rendered in 139s &nbsp;·&nbsp; ¥0.2 &nbsp;·&nbsp; 8.4 MB</sub>

The same model, written the community way: one paragraph, no field labels. Steam, wet asphalt and a rider held at a constant size by a backward tracking shot.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=A+neon-lit+alley+in+the+rain+at+night%2C+shot+on+a+35mm+lens+at+eye+level.+Steam+rises+from+a+food+stall+on+the+left+and+drifts+across+the+frame.+A+delivery+rider+in+a+yellow+rain+jacket+walks+a+scooter+through+the+middle+of+the+alley+toward+the+camera%2C+water+sheeting+off+the+wheels.+The+camera+tracks+backward+slowly+at+walking+pace%2C+keeping+the+rider+the+same+size+in+frame+the+whole+time.+Reflections+of+pink+and+green+signs+break+and+reform+on+the+wet+asphalt.+The+alley+opens+onto+a+wider+street+at+the+far+end%2C+where+headlights+pass.+Handheld%2C+subtle+shake.+Photoreal%2C+no+colour+grading%2C+natural+street+lighting+only.&duration=5&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=02-alley-after-rain)**

```text
A neon-lit alley in the rain at night, shot on a 35mm lens at eye level. Steam rises from a food stall on the left and drifts across the frame. A delivery rider in a yellow rain jacket walks a scooter through the middle of the alley toward the camera, water sheeting off the wheels. The camera tracks backward slowly at walking pace, keeping the rider the same size in frame the whole time. Reflections of pink and green signs break and reform on the wet asphalt. The alley opens onto a wider street at the far end, where headlights pass. Handheld, subtle shake. Photoreal, no colour grading, natural street lighting only.
```

[Prompt file](showcase/02-alley-after-rain/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/02-alley-after-rain/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/02-alley-after-rain/768p-h.mp4)

---

### 03 · One Stroke of Ink

<sub>Cinematic &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1920 × 1056</b> &nbsp;·&nbsp; 5.17s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/03-ink-1080p/1080p-h.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/03-ink-1080p/preview.webp" alt="One Stroke of Ink — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/03-ink-1080p/1080p-h.mp4">watch the full 5.17s clip (4.8 MB MP4)</a></sub>

<sub>requested <code>1080p landscape</code> for 5s &nbsp;·&nbsp; rendered in 235s &nbsp;·&nbsp; ¥0.5 &nbsp;·&nbsp; 4.8 MB</sub>

The top tier, on a subject whose entire value is fine texture — paper fibre and wet ink. Kept in the set so the size comparison has a 1080P column.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Live-action%2C+cinematic%2C+high+detail.+A+single+sheet+of+thin+rice+paper+is+laid+on+a+dark+wooden+table%2C+and+a+brush+loaded+with+black+ink+is+held+just+above+it%2C+motionless.+The+camera+holds+a+static+shot+in+a+tight+top-down+view.+After+a+beat+the+hand+begins+to+write+a+single+character%2C+the+ink+bleeding+slightly+into+the+paper%27s+fibre+as+the+stroke+is+laid+down.+The+camera+pushes+in+with+small+amplitude+at+slow+speed%2C+tightening+until+the+wet+ink+and+the+paper%27s+texture+fill+the+frame.+Warm+afternoon+light+comes+from+a+window+at+the+left+edge+and+rakes+across+the+paper%2C+so+the+raised+grain+casts+a+short+shadow.+Dust+motes+are+visible+in+the+light.%0A%0Aoverall_soundscape%3A+A+quiet+room.+The+brush+bristles+drag+audibly+across+the+paper%2C+the+ink+makes+a+faint+wet+ticking+as+the+stroke+is+drawn%2C+and+the+wooden+table+creaks+once+under+the+pressure+of+the+hand.+A+clock+ticks+slowly+somewhere+behind+the+camera.%0A%0Anon_diegetic_music%3A+N%2FA&duration=5&resolution=1080P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=03-ink-1080p)**

```text
integrated_multimodal_description: [Shot 1] Live-action, cinematic, high detail. A single sheet of thin rice paper is laid on a dark wooden table, and a brush loaded with black ink is held just above it, motionless. The camera holds a static shot in a tight top-down view. After a beat the hand begins to write a single character, the ink bleeding slightly into the paper's fibre as the stroke is laid down. The camera pushes in with small amplitude at slow speed, tightening until the wet ink and the paper's texture fill the frame. Warm afternoon light comes from a window at the left edge and rakes across the paper, so the raised grain casts a short shadow. Dust motes are visible in the light.

overall_soundscape: A quiet room. The brush bristles drag audibly across the paper, the ink makes a faint wet ticking as the stroke is drawn, and the wooden table creaks once under the pressure of the hand. A clock ticks slowly somewhere behind the camera.

non_diegetic_music: N/A
```

[Prompt file](showcase/03-ink-1080p/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/03-ink-1080p/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/03-ink-1080p/1080p-h.mp4)

---

### 04 · Caravan at Dusk

<sub>World building &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 6.58s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/04-caravan-dusk/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/04-caravan-dusk/preview.webp" alt="Caravan at Dusk — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/04-caravan-dusk/768p.mp4">watch the full 6.58s clip (8.0 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 6s &nbsp;·&nbsp; rendered in 185s &nbsp;·&nbsp; ¥0.24 &nbsp;·&nbsp; 8.0 MB</sub>

A wide shot with deliberately small figures — the framing H3 is worst at, used where no face needs to read.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Live-action%2C+anamorphic+wide.+A+line+of+seven+camels+carrying+riders+and+rolled+carpets+crosses+a+flat+gravel+plain+at+last+light%2C+moving+right+to+left.+They+are+small+in+the+frame%3B+the+caravan+occupies+the+middle+third+and+the+horizon+sits+high%2C+so+the+plain+dominates.+Low+sun+from+behind+the+caravan+throws+long+shadows+forward+toward+the+camera+and+turns+the+dust+the+animals+raise+into+a+bright+haze.+The+camera+holds+a+static+shot+for+the+first+beats%2C+then+trucks+right+with+large+amplitude+at+slow+speed%2C+matching+the+caravan%27s+pace%2C+so+the+animals+stay+in+the+same+place+in+frame+while+the+plain+slides+past+behind+them.+No+faces+are+visible+at+any+point%3B+the+riders+read+as+silhouettes+against+the+light.%0A%0Aoverall_soundscape%3A+Wind+moving+across+open+ground+with+nothing+to+obstruct+it%2C+the+soft+irregular+thud+of+hooves+on+dry+gravel%2C+tack+creaking+with+each+step%2C+and+a+long+low+bird+call+somewhere+behind+the+camera.%0A%0Anon_diegetic_music%3A+A+single+sustained+cello+note%2C+very+low%2C+held+under+the+whole+shot+without+changing.+No+melody%2C+no+percussion.&duration=6&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=04-caravan-dusk)**

```text
integrated_multimodal_description: [Shot 1] Live-action, anamorphic wide. A line of seven camels carrying riders and rolled carpets crosses a flat gravel plain at last light, moving right to left. They are small in the frame; the caravan occupies the middle third and the horizon sits high, so the plain dominates. Low sun from behind the caravan throws long shadows forward toward the camera and turns the dust the animals raise into a bright haze. The camera holds a static shot for the first beats, then trucks right with large amplitude at slow speed, matching the caravan's pace, so the animals stay in the same place in frame while the plain slides past behind them. No faces are visible at any point; the riders read as silhouettes against the light.

overall_soundscape: Wind moving across open ground with nothing to obstruct it, the soft irregular thud of hooves on dry gravel, tack creaking with each step, and a long low bird call somewhere behind the camera.

non_diegetic_music: A single sustained cello note, very low, held under the whole shot without changing. No melody, no percussion.
```

[Prompt file](showcase/04-caravan-dusk/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/04-caravan-dusk/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/04-caravan-dusk/768p.mp4)

---

### 05 · Dragon Made of Seeds

<sub>Motion graphics &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 6.58s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/05-seed-dragon/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/05-seed-dragon/preview.webp" alt="Dragon Made of Seeds — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/05-seed-dragon/768p.mp4">watch the full 6.58s clip (3.3 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 6s &nbsp;·&nbsp; rendered in 253s &nbsp;·&nbsp; ¥0.24 &nbsp;·&nbsp; 3.3 MB</sub>

Stop-motion assembled from dried pulses — a shot about material and assembly rather than camera movement.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Stop-motion+animation+shot+on+a+tabletop%2C+visible+frame-to-frame+stutter%2C+no+motion+blur.+A+dragon+is+assembled+from+dried+beans%2C+lentils%2C+rice+grains+and+split+peas+on+a+plain+grey+card+surface%2C+in+a+tight+top-down+view.+The+camera+holds+a+static+shot+throughout.+The+head+forms+first+from+black+beans%2C+then+the+spine+assembles+itself+from+alternating+red+lentils+and+white+rice%2C+segment+by+segment%2C+each+new+grain+appearing+between+frames+rather+than+sliding+into+place.+The+tail+unrolls+last%2C+curling+toward+the+upper+right+of+the+frame.+Soft+even+studio+light+from+directly+above%3B+each+pulse+casts+a+small+hard+shadow+to+the+lower+left.+The+palette+is+limited+to+the+natural+colours+of+the+pulses%3A+black%2C+red%2C+cream+and+pale+green.%0A%0Aoverall_soundscape%3A+Dry%2C+quiet+and+close.+Individual+hard+grains+clicking+against+card+as+they+are+set+down+one+at+a+time%2C+a+faint+rustle+as+a+handful+is+moved%2C+and+the+low+hum+of+the+room.%0A%0Anon_diegetic_music%3A+A+light+pizzicato+cello+figure+at+a+moderate+walking+tempo%2C+matched+to+the+rhythm+of+the+grains+being+placed.&duration=6&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=05-seed-dragon)**

```text
integrated_multimodal_description: [Shot 1] Stop-motion animation shot on a tabletop, visible frame-to-frame stutter, no motion blur. A dragon is assembled from dried beans, lentils, rice grains and split peas on a plain grey card surface, in a tight top-down view. The camera holds a static shot throughout. The head forms first from black beans, then the spine assembles itself from alternating red lentils and white rice, segment by segment, each new grain appearing between frames rather than sliding into place. The tail unrolls last, curling toward the upper right of the frame. Soft even studio light from directly above; each pulse casts a small hard shadow to the lower left. The palette is limited to the natural colours of the pulses: black, red, cream and pale green.

overall_soundscape: Dry, quiet and close. Individual hard grains clicking against card as they are set down one at a time, a faint rustle as a handful is moved, and the low hum of the room.

non_diegetic_music: A light pizzicato cello figure at a moderate walking tempo, matched to the rhythm of the grains being placed.
```

[Prompt file](showcase/05-seed-dragon/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/05-seed-dragon/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/05-seed-dragon/768p.mp4)

---

### 06 · First-Person Corridor

<sub>Game &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 6.58s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/06-fps-corridor/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/06-fps-corridor/preview.webp" alt="First-Person Corridor — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/06-fps-corridor/768p.mp4">watch the full 6.58s clip (6.1 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 6s &nbsp;·&nbsp; rendered in 180s &nbsp;·&nbsp; ¥0.24 &nbsp;·&nbsp; 6.1 MB</sub>

First-person is H3's native grammar — no faces, no wide shots, and every frame is a camera move.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+First-person%2C+eye+level%2C+handheld+gameplay+camera%2C+as+if+recorded+from+a+modern+first-person+game.+The+camera+advances+down+a+narrow+concrete+service+corridor+lit+by+a+single+row+of+caged+bulbs+along+the+ceiling%2C+some+of+them+flickering.+Both+gloved+hands+are+visible+in+the+lower+part+of+the+frame+holding+a+compact+device%3B+the+hands+sway+slightly+with+each+footstep+and+the+device+dips+when+the+operator+turns.+The+camera+moves+forward+at+a+steady+walking+pace%2C+stops+completely+for+a+beat+as+a+door+at+the+end+of+the+corridor+opens+on+its+own%2C+then+continues+forward+with+small+amplitude+at+slow+speed.+Dust+hangs+in+the+light.+The+palette+is+cold+concrete+and+blue-grey%3B+there+is+no+warm+light+anywhere+in+the+frame.+Do+not+show+a+crosshair+or+any+interface.%0A%0Aoverall_soundscape%3A+Footsteps+on+concrete+with+a+short+hard+reverb+down+the+corridor%2C+the+hum+of+the+caged+bulbs%2C+a+faint+electrical+buzz+from+the+flickering+one%2C+and+the+dry+clack+of+the+door+mechanism+at+the+end+before+it+swings.%0A%0Anon_diegetic_music%3A+A+slow+low+drone+in+a+minor+key+with+no+rhythm%2C+rising+very+slightly+in+volume+across+the+shot.&duration=6&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=06-fps-corridor)**

```text
integrated_multimodal_description: [Shot 1] First-person, eye level, handheld gameplay camera, as if recorded from a modern first-person game. The camera advances down a narrow concrete service corridor lit by a single row of caged bulbs along the ceiling, some of them flickering. Both gloved hands are visible in the lower part of the frame holding a compact device; the hands sway slightly with each footstep and the device dips when the operator turns. The camera moves forward at a steady walking pace, stops completely for a beat as a door at the end of the corridor opens on its own, then continues forward with small amplitude at slow speed. Dust hangs in the light. The palette is cold concrete and blue-grey; there is no warm light anywhere in the frame. Do not show a crosshair or any interface.

overall_soundscape: Footsteps on concrete with a short hard reverb down the corridor, the hum of the caged bulbs, a faint electrical buzz from the flickering one, and the dry clack of the door mechanism at the end before it swings.

non_diegetic_music: A slow low drone in a minor key with no rhythm, rising very slightly in volume across the shot.
```

[Prompt file](showcase/06-fps-corridor/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/06-fps-corridor/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/06-fps-corridor/768p.mp4)

---

### 07 · Lighthouse in a Storm

<sub>Cinematic &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>768 × 1344</b> &nbsp;·&nbsp; 6.58s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/07-storm-lighthouse/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/07-storm-lighthouse/preview.webp" alt="Lighthouse in a Storm — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/07-storm-lighthouse/768p.mp4">watch the full 6.58s clip (4.4 MB MP4)</a></sub>

<sub>requested <code>768p portrait</code> for 6s &nbsp;·&nbsp; rendered in 161s &nbsp;·&nbsp; ¥0.24 &nbsp;·&nbsp; 4.4 MB</sub>

The vertical canvas, where the tower fills the frame and the sea does the moving.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Live-action%2C+vertical+composition%2C+night%2C+storm.+A+stone+lighthouse+stands+on+a+rock+at+the+edge+of+a+heavy+sea%2C+filling+the+centre+of+the+frame+from+the+waterline+to+the+base+of+the+lantern+room%2C+with+dark+storm+cloud+occupying+the+top+third.+A+large+swell+runs+in+from+the+left+and+breaks+against+the+rock%2C+throwing+spray+up+past+the+midpoint+of+the+tower.+The+beam+sweeps+through+frame+from+left+to+right+twice+during+the+shot%2C+lighting+the+spray+from+the+inside+each+time.+The+camera+holds+a+static+shot+at+a+slight+low+angle%2C+so+the+tower+leans+away+from+the+viewer.+Rain+falls+heavily+and+is+visible+as+streaks+against+the+beam%2C+not+against+the+sky.+Everything+outside+the+beam+is+near+black.%0A%0Aoverall_soundscape%3A+Heavy+surf+breaking+on+rock+and+draining+back+with+a+long+drawn-out+hiss%2C+unbroken+rain+on+stone%2C+and+wind+steady+at+high+speed+around+the+tower+with+no+gusts.+Under+all+of+it%2C+a+low+continuous+roar+from+the+sea.%0A%0Anon_diegetic_music%3A+N%2FA&duration=6&resolution=768P&aspect_ratio=9%3A16&utm_source=github&utm_medium=h3-atlas&utm_campaign=07-storm-lighthouse)**

```text
integrated_multimodal_description: [Shot 1] Live-action, vertical composition, night, storm. A stone lighthouse stands on a rock at the edge of a heavy sea, filling the centre of the frame from the waterline to the base of the lantern room, with dark storm cloud occupying the top third. A large swell runs in from the left and breaks against the rock, throwing spray up past the midpoint of the tower. The beam sweeps through frame from left to right twice during the shot, lighting the spray from the inside each time. The camera holds a static shot at a slight low angle, so the tower leans away from the viewer. Rain falls heavily and is visible as streaks against the beam, not against the sky. Everything outside the beam is near black.

overall_soundscape: Heavy surf breaking on rock and draining back with a long drawn-out hiss, unbroken rain on stone, and wind steady at high speed around the tower with no gusts. Under all of it, a low continuous roar from the sea.

non_diegetic_music: N/A
```

[Prompt file](showcase/07-storm-lighthouse/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/07-storm-lighthouse/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/07-storm-lighthouse/768p.mp4)

---

### 08 · Night Market, Square

<sub>Documentary &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>768 × 768</b> &nbsp;·&nbsp; 6.58s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/08-night-market-square/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/08-night-market-square/preview.webp" alt="Night Market, Square — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/08-night-market-square/768p.mp4">watch the full 6.58s clip (4.6 MB MP4)</a></sub>

<sub>requested <code>768p(1:1)</code> for 6s &nbsp;·&nbsp; rendered in 135s &nbsp;·&nbsp; ¥0.24 &nbsp;·&nbsp; 4.6 MB</sub>

The square canvas, which the official H3 endpoint lists and almost no gallery ever shows.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Documentary%2C+handheld%2C+square+composition%2C+available+light+only.+A+night+market+food+stall+seen+from+directly+in+front%2C+filling+the+frame.+Two+cooks+work+behind+a+counter+of+scratched+stainless+steel%3B+the+one+on+the+left+turns+skewers+over+a+charcoal+trough+and+the+one+on+the+right+ladles+broth+from+a+pot+into+a+bowl+and+hands+it+forward%2C+off+frame.+Steam+rises+continuously+between+the+camera+and+the+stall%2C+catching+the+row+of+bare+bulbs+hanging+above+the+counter+and+going+bright+where+it+crosses+them.+The+queue+is+visible+only+as+out-of-focus+dark+shapes+at+the+left+and+right+edges+of+the+frame%2C+never+in+the+centre.+The+camera+holds+a+static+shot+with+small+handheld+drift.+The+colour+temperature+is+mixed%3A+warm+tungsten+from+the+bulbs%2C+a+cooler+spill+from+the+neighbouring+stall+at+the+right+edge%2C+and+the+orange+glow+of+the+charcoal+from+below.%0A%0Aoverall_soundscape%3A+A+busy+market+at+close+range.+Charcoal+ticking%2C+skewers+turning+against+a+metal+grill%2C+broth+being+poured%2C+several+conversations+overlapping+so+that+no+single+word+is+intelligible%2C+and+a+stack+of+bowls+being+set+down.%0A%0Anon_diegetic_music%3A+N%2FA&duration=6&resolution=768P&aspect_ratio=1%3A1&utm_source=github&utm_medium=h3-atlas&utm_campaign=08-night-market-square)**

```text
integrated_multimodal_description: [Shot 1] Documentary, handheld, square composition, available light only. A night market food stall seen from directly in front, filling the frame. Two cooks work behind a counter of scratched stainless steel; the one on the left turns skewers over a charcoal trough and the one on the right ladles broth from a pot into a bowl and hands it forward, off frame. Steam rises continuously between the camera and the stall, catching the row of bare bulbs hanging above the counter and going bright where it crosses them. The queue is visible only as out-of-focus dark shapes at the left and right edges of the frame, never in the centre. The camera holds a static shot with small handheld drift. The colour temperature is mixed: warm tungsten from the bulbs, a cooler spill from the neighbouring stall at the right edge, and the orange glow of the charcoal from below.

overall_soundscape: A busy market at close range. Charcoal ticking, skewers turning against a metal grill, broth being poured, several conversations overlapping so that no single word is intelligible, and a stack of bowls being set down.

non_diegetic_music: N/A
```

[Prompt file](showcase/08-night-market-square/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/08-night-market-square/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/08-night-market-square/768p.mp4)

---

### 09 · Kite Festival, Full Length

<sub>Cinematic &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 15.08s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/09-kite-festival-15s/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/09-kite-festival-15s/preview.webp" alt="Kite Festival, Full Length — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/09-kite-festival-15s/768p.mp4">watch the full 15.08s clip (14.4 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 15s &nbsp;·&nbsp; rendered in 862s &nbsp;·&nbsp; ¥0.6 &nbsp;·&nbsp; 14.4 MB</sub>

A full fifteen seconds — the longest single generation H3 allows, and the duration the community has settled on almost universally.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Live-action%2C+cinematic%2C+golden+hour.+A+hilltop+covered+in+dry+grass%2C+with+a+large+crowd+of+people+flying+kites+of+every+colour+against+a+clear+evening+sky.+The+camera+starts+high%2C+looking+down+the+slope+toward+the+crowd+and+the+kites+above+them%2C+then+lowers+with+small+amplitude+at+slow+speed+until+it+sits+at+shoulder+height+among+the+people.+Kites+fill+the+upper+two+thirds+of+the+frame+throughout%2C+moving+in+different+directions+at+different+speeds+and+receding+into+the+distance+where+they+become+dots.+Adult+figures+are+seen+from+behind+or+from+the+side+at+middle+distance%3B+no+faces+are+visible.+Warm+low+sunlight+from+the+right+throws+long+shadows+down+the+slope%2C+and+the+grass+in+the+foreground+is+backlit+enough+to+glow+at+the+tips.%0A%0A%5BShot+2%5D+At+00%3A07.000%2C+the+camera+cuts+to+a+tighter+shot+inside+the+crowd+at+chest+height%2C+panning+right+at+slow+speed+across+a+row+of+people+holding+lines%2C+kites+pulling+above+them.+One+small+child+in+a+red+jacket+runs+across+the+frame+from+left+to+right+and+exits%2C+and+the+camera+continues+its+pan+without+following.+The+sun+is+now+partially+behind+a+kite%2C+causing+a+lens+flare+that+crosses+the+upper+left+of+the+frame.%0A%0Aoverall_soundscape%3A+Wind+moving+through+dry+grass+and+across+the+microphone%2C+the+paper-and-bamboo+rattle+of+many+kites+in+the+air%2C+distant+laughter+and+voices+from+the+crowd%2C+and+one+dog+barking+repeatedly+somewhere+down+the+slope.%0A%0Anon_diegetic_music%3A+A+warm+mid-tempo+acoustic+ensemble+%E2%80%94+guitar%2C+fiddle+and+light+hand+percussion+%E2%80%94+rising+gently+through+the+shot+and+settling+rather+than+resolving+at+the+end.&duration=15&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=09-kite-festival-15s)**

```text
integrated_multimodal_description: [Shot 1] Live-action, cinematic, golden hour. A hilltop covered in dry grass, with a large crowd of people flying kites of every colour against a clear evening sky. The camera starts high, looking down the slope toward the crowd and the kites above them, then lowers with small amplitude at slow speed until it sits at shoulder height among the people. Kites fill the upper two thirds of the frame throughout, moving in different directions at different speeds and receding into the distance where they become dots. Adult figures are seen from behind or from the side at middle distance; no faces are visible. Warm low sunlight from the right throws long shadows down the slope, and the grass in the foreground is backlit enough to glow at the tips.

[Shot 2] At 00:07.000, the camera cuts to a tighter shot inside the crowd at chest height, panning right at slow speed across a row of people holding lines, kites pulling above them. One small child in a red jacket runs across the frame from left to right and exits, and the camera continues its pan without following. The sun is now partially behind a kite, causing a lens flare that crosses the upper left of the frame.

overall_soundscape: Wind moving through dry grass and across the microphone, the paper-and-bamboo rattle of many kites in the air, distant laughter and voices from the crowd, and one dog barking repeatedly somewhere down the slope.

non_diegetic_music: A warm mid-tempo acoustic ensemble — guitar, fiddle and light hand percussion — rising gently through the shot and settling rather than resolving at the end.
```

[Prompt file](showcase/09-kite-festival-15s/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/09-kite-festival-15s/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/09-kite-festival-15s/768p.mp4)

---

### 10 · Two Speakers, One Line Each

<sub>Dialogue &nbsp;·&nbsp; text to video &nbsp;·&nbsp; <b>1344 × 768</b> &nbsp;·&nbsp; 8.00s &nbsp;·&nbsp; 24 fps &nbsp;·&nbsp; native stereo audio @ 32 kHz</sub>

<a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/10-two-speakers/768p.mp4"><img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/10-two-speakers/preview.webp" alt="Two Speakers, One Line Each — 3 second loop" width="100%"></a>

<sub>▶ 3-second loop, 10 fps — <a href="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/10-two-speakers/768p.mp4">watch the full 8.00s clip (2.1 MB MP4)</a></sub>

<sub>requested <code>768p landscape</code> for 8s &nbsp;·&nbsp; rendered in 215s &nbsp;·&nbsp; ¥0.32 &nbsp;·&nbsp; 2.1 MB</sub>

Speaker IDs, the <d> dialogue tag, and an off-screen voiceover with the lips-closed clause — the syntax almost nobody gets right.

**[▶ Try this prompt in a browser →](https://callirra.com/minimax-h3?model=minimax-h3&prompt=integrated_multimodal_description%3A+%5BShot+1%5D+Live-action%2C+cinematic%2C+shallow+depth+of+field%2C+night+interior.+A+small+kitchen+lit+by+one+bulb+over+a+table.+Two+people+sit+opposite+each+other%3A+an+older+man+in+a+dark+jacket+on+the+left%2C+a+young+woman+in+a+grey+sweater+on+the+right.+Both+are+in+medium+shot+from+the+chest+up.+The+camera+holds+a+static+shot.+The+man+%28S1%29+says+in+a+soft%2C+tired+voice%3A+%3Cd%3E%5BEnglish%5D+You+already+knew.+You+just+wanted+me+to+say+it.%3C%2Fd%3E+He+looks+down+at+the+table+as+he+finishes+and+does+not+lift+his+head.+The+woman+%28S2%29+replies%2C+quietly+and+without+moving+anything+but+her+mouth%3A+%3Cd%3E%5BEnglish%5D+I+wanted+you+to+say+it+first.%3C%2Fd%3E+Neither+of+them+leaves+their+seat+and+neither+of+them+touches+the+other.%0A%0A%5BShot+2%5D+At+00%3A05.000%2C+the+camera+cuts+to+a+tight+close-up+of+the+woman%27s+face%2C+unchanged+in+lighting+and+position.+The+man+%28S1%29+says+in+an+off-screen+voiceover%3A+%3Cd%3E%5BEnglish%5D+I+know.%3C%2Fd%3E+while+his+lips+remain+completely+closed%3B+he+is+not+in+this+shot.%0A%0Aoverall_soundscape%3A+A+quiet+kitchen+at+night.+A+refrigerator+compressor+running+steadily%2C+the+low+hum+of+the+bulb%2C+one+chair+shifting+under+weight%2C+and+a+clock+ticking+in+the+next+room.+No+traffic+and+no+diegetically+audible+music.%0A%0Anon_diegetic_music%3A+N%2FA&duration=8&resolution=768P&aspect_ratio=16%3A9&utm_source=github&utm_medium=h3-atlas&utm_campaign=10-two-speakers)**

```text
integrated_multimodal_description: [Shot 1] Live-action, cinematic, shallow depth of field, night interior. A small kitchen lit by one bulb over a table. Two people sit opposite each other: an older man in a dark jacket on the left, a young woman in a grey sweater on the right. Both are in medium shot from the chest up. The camera holds a static shot. The man (S1) says in a soft, tired voice: <d>[English] You already knew. You just wanted me to say it.</d> He looks down at the table as he finishes and does not lift his head. The woman (S2) replies, quietly and without moving anything but her mouth: <d>[English] I wanted you to say it first.</d> Neither of them leaves their seat and neither of them touches the other.

[Shot 2] At 00:05.000, the camera cuts to a tight close-up of the woman's face, unchanged in lighting and position. The man (S1) says in an off-screen voiceover: <d>[English] I know.</d> while his lips remain completely closed; he is not in this shot.

overall_soundscape: A quiet kitchen at night. A refrigerator compressor running steadily, the low hum of the bulb, one chair shifting under weight, and a clock ticking in the next room. No traffic and no diegetically audible music.

non_diegetic_music: N/A
```

[Prompt file](showcase/10-two-speakers/prompt.txt) &nbsp;·&nbsp; [generation record](showcase/10-two-speakers/generation.json) &nbsp;·&nbsp; [download MP4](https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/showcase/10-two-speakers/768p.mp4)

---

## Community gallery

40 prompts published by their creators on X, curated and reproduced verbatim, with the
video staying on the creator's own post. Nothing here re-hosts another person's footage.

**On provenance, because this is where H3 galleries go wrong.** A prompt that was never
published cannot be recovered by watching the video — a reconstruction describes the
*output*, not the prompt, and publishing one as the creator's work is a fabrication. Every
entry in this section carries a prompt its creator actually posted, and the
`promptProvenance` field on each one says so. Entries whose prompt was never published are
not in this repository at all.

### 01 · Ramen Rack Focus

<sub>MiniMaxAI &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 8 &nbsp;·&nbsp; 768p &nbsp;·&nbsp; Auto</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/official-fl2va-ramen.webp" alt="Ramen Rack Focus" width="100%">](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-fl2va-request.sh)

<sub><b>▶ <a href="https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-fl2va-request.sh">Watch the clip on MiniMax's official reproducible script</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Uses a ramen image as the opening-frame constraint, then gradually racks focus so the foreground steam softens while the family in the background comes into view, testing depth of field and ensemble motion.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (4,534 characters)</summary>

```text
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] This is a live-action, cinematic shot with a shallow depth of field. The camera holds a perfectly static shot throughout the entire eight-second duration, capturing a cozy family gathering in a traditional Japanese dining room. The scene opens with a large, intricately patterned blue and white ceramic bowl of ramen in the immediate foreground, rendered in crisp, sharp focus. The bowl sits on a smooth, polished long wooden table. Inside the bowl, a rich, oily golden-brown broth surrounds yellow wavy noodles, topped with two thick, round slices of chashu pork featuring visible fat marbling and a distinct spiral meat pattern. A generous mound of freshly chopped, bright green scallions rests in the center, and a crisp, dark green rectangular sheet of nori seaweed is tucked into the right edge. To the left of the bowl, a pair of light brown wooden chopsticks rests horizontally on a small, dark rectangular chopstick rest, near a small cylindrical ceramic teacup with blue painted patterns. On the right side of the table, a spherical paper lantern with a ribbed bamboo frame sits on a black wooden base. In the background, a large family of seven is gathered around the table, initially appearing as a soft, blurred presence. Behind them, traditional Japanese sliding shoji screens with wooden lattice frames are open, revealing a bright outdoor scene with lush green trees. Early in the clip, the thick, white steam rising from the hot ramen broth immediately intensifies, billowing upwards in thick, swirling clouds that dance continuously above the bowl. As the clip progresses into the middle seconds, the camera maintains its static position while the focus begins a deliberate, smooth shift deeper into the room. The foreground ramen bowl, its vibrant ingredients, and the rising steam gradually soften into a hazy, out-of-focus blur. Simultaneously, the family members in the background come into sharp, detailed clarity. The heavy steam continues to rise from the foreground, creating a dynamic, translucent veil between the camera and the family. With the focus now firmly locked on the background, the vibrant family dinner comes alive. The man in the dark navy blue long-sleeved shirt on the left leans forward, his mouth moving animatedly in a silent exchange. The young girl in the crisp white short-sleeved t-shirt beside him smiles brightly, looking toward the center of the table. The woman on the far left, wearing a soft light blue long-sleeved blouse, turns her head slightly, smiling gently. Across the table, the woman in the light grey button-down shirt smiles broadly, her eyes crinkling, as she rests her hands near her plate. The woman in the dark grey top further back uses her wooden chopsticks to pick up a small piece of food from a central ceramic dish filled with bright red pickled vegetables. The woman in the center back in the light grey sweater smiles gently, her hands clasped softly in front of her, observing the interaction. Throughout the remainder of the clip, the family continues their lively physical interaction, their mouths moving in continuous, silent cadences of conversation, while the thick, white steam from the blurred ramen bowl in the foreground never stops rising, adding a comforting atmosphere to the warm gathering.

overall_soundscape: The soundscape begins with a quiet room tone mixed with the faint, airy rustle of the thick steam billowing from the hot ramen bowl in the foreground, accompanied by the subtle, continuous hissing and bubbling of the rich broth. As the visual focus shifts deeper into the room, the physical sounds of the bustling family dinner become dominant in the foreground. The clear, sharp clinking of ceramic bowls and wooden chopsticks touching plates is clearly heard as the family members reach for food. This is followed by the faint, muffled thud of a cup being set down on the smooth wooden table, and the subtle, rhythmic rustle of cotton and wool clothing as the family members lean forward and gesture, perfectly capturing the lively, physical atmosphere of the shared meal.

non_diegetic_music: A gentle, heartwarming acoustic guitar melody plays softly in the background, accompanied by the subtle, resonant notes of a traditional Japanese koto. The music maintains a slow, comforting tempo that enhances the cozy, nostalgic, and joyful atmosphere of the family gathering.
```

</details>

<sub>Source: <a href="https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-fl2va-request.sh">https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-fl2va-request.sh</a> &nbsp;·&nbsp; prompt provenance: <code>official-verbatim</code></sub>

---

### 02 · After the Fleet Jumps

<sub>MiniMaxAI &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 10 &nbsp;·&nbsp; 768p &nbsp;·&nbsp; 16:9</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/official-t2va-starship.webp" alt="After the Fleet Jumps" width="100%">](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-t2va-request.sh)

<sub><b>▶ <a href="https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-t2va-request.sh">Watch the clip on MiniMax's official reproducible script</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Moves from a medium-wide view of a starship bridge to a close-up of the captain, using native stereo audio to synchronize the fleet jump, spatial shock, and the suddenly quiet aftermath.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (2,504 characters)</summary>

```text
integrated_multimodal_description: [Shot 1] Cinematic, medium wide shot, pushing in slowly. In the cavernous, dimly lit bridge of a starship, sleek metallic consoles with glowing amber displays flank a massive, curved observation window. A female captain, in her late 40s with an athletic build and short silver-streaked black hair, stands in the center midground. She wears a structured, high-collared dark navy military tunic with silver chest insignias. Her back is to the camera, silhouetted against the cool, ambient starlight pouring through the thick glass. She stands perfectly still with her hands clasped tightly behind her back. Outside the window, a massive armada of jagged, dark grey dreadnoughts hovers in tight formation against a deep purple space nebula. The fleet's massive rear thrusters begin to glow with an intense, escalating bright blue light. [Shot 2] At 00:04.500, the camera cuts to a close-up of the captain's face and shakes strongly. The brilliant blue-white light from the fleet's gathering energy reflects vividly in her dark eyes. Suddenly, a blinding white flash floods through the window, completely washing out the background as the fleet jumps to hyperspace. The sheer spatial force violently jolts the bridge, causing the captain from Shot 1 to stagger slightly forward, her shoulders tensing as she visibly braces herself against the physical tremors. As the intense white light fades abruptly, leaving only the dim, empty expanse of the purple nebula reflected on her starkly lit skin, her jaw clenches, and she slowly closes her eyes in the newly emptied space.
overall_soundscape: A low, resonant hum of the ship's ambient life support systems serves as the baseline, soon drowned out by an audible, escalating, high-pitched electronic whine as the fleet outside charges its hyperdrives. A massive, deafening, bass-heavy boom and sharp crackle erupts during the blinding flash, accompanied by the loud metallic creaking, rattling, and deep thuds of the bridge's bulkheads vibrating under immense physical stress. The intense roaring impact then cuts abruptly back to a hollow, echoing room tone, leaving only the faint, steady hum of the isolated bridge.
non_diegetic_music: Cinematic space-opera orchestral score, slow tempo, featuring a solitary, mournful French horn melody over deep, sustained string dissonances that build rapidly in volume and intensity, swelling to a massive orchestral peak before snapping immediately into silence right after the jump.
```

</details>

<sub>Source: <a href="https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-t2va-request.sh">https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/scripts/readme/reproducible-768p-t2va-request.sh</a> &nbsp;·&nbsp; prompt provenance: <code>official-verbatim</code></sub>

---

### 03 · Jade Panic: A Yellow-and-Green Character Entrance

<sub>Just_sharon7 &nbsp;·&nbsp; Unknown &nbsp;·&nbsp; 15.168 &nbsp;·&nbsp; 1440p &nbsp;·&nbsp; 16:9</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2094305294117429711.jpg" alt="Jade Panic: A Yellow-and-Green Character Entrance" width="100%">](https://x.com/Just_sharon7/status/2094305294117429711)

<sub><b>▶ <a href="https://x.com/Just_sharon7/status/2094305294117429711">Watch the clip on the creator's post on X (@Just_sharon7)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A stylized anime character moves through bold yellow-and-green graphic compositions, action poses and impact typography. The prompt requires a character reference.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (5,491 characters)</summary>

```text
15s / 16:9 / high-energy 2D anime pop-punk MV — character-locked
Create a 15-second horizontal 16:9 high-energy 2D anime pop-punk music video featuring the exact heroine from the provided character reference. The entire sequence must feel like one continuous, tightly choreographed MV passage; each movement must motivate the next transition.
CHARACTER LOCK (absolute authority = the reference still)
Twin high black space-buns with messy volume and warm brown inner strands. Green jade disc clusters pinned into both buns. Straight blunt bangs with a small center split. Huge sharp green eyes, thick black outlines, strong lashes. Small mouth, warm cheek blush, pale skin. Green circular dangling jade earrings. Sleeveless lime-to-jade floral qipao with black piping, black frog-button placket, high collar, and black line-art lotuses on the fabric. Bare shoulders and arms. Stylized proportions: oversized head, compact torso, long simplified limbs, chunky hands. Bold black outlines, flat saturated colors, minimal cel shading, early-2000s TV-anime / handmade cartoon finish. Personality: loud, cheeky, rebellious, playful, hyperactive — the still’s fierce stare becomes motion, not a different face.

Do not change hair color, bun structure, eye color, earrings, qipao cut, floral linework, or outline weight. No pink hair, no red plaid uniform, no extra characters, no 3D, no photorealism, no glossy modern anime redesign.
GRAPHIC LANGUAGE (from the still)
Primary palette: lemon yellow, jade / lime green, ink black, paper white. Motifs: spinning jade discs, qipao lotus line-art, frog-button glyphs, circular earrings as motion graphics, torn yellow paper, black brush X’s, photocopy grain, tape strips, hand-drawn stars and crosses, rough ink splatters. Kinetic type must look stamped, ripped, or screen-printed — never clean corporate sans.
0.0–2.5s
Start in motion. She slides in from frame-left, one foot skidding across a clean yellow graphic floor. Body leans forward; both buns, earrings, and qipao hem trail behind. She stomps the second foot down, snaps her chin up, and flashes a mischievous grin over the reference’s fierce eye shape. Impact instantly tiles the yellow field into huge jade-and-black floral blocks. Bold kinetic type “JADE PANIC!” slams in, letters made from ripped yellow paper + green lotus outlines.

2.5–5.0s
No pause. Rebound into a small hop and sharp half-turn. Camera swings from front ¾ into a fast side-track as she takes two exaggerated cartoon steps. Feet hit on alternating beats, leaving jade discs, lotus scribbles, tape, crosses, and comic impact marks. Buns and earrings bounce hard; qipao hem flares.
5.0–7.5s
Side kick on the beat. Kick momentum spins her. The floral pattern on the qipao stretches into a giant rotating graphic plane and pulls the frame into an abstract 2D punk world: black brush strokes, green lotus line-art, yellow paper shards, jade lightning (mint/cyan accents only as small bolts, never as hair), photocopy texture. She flows straight into a bouncy phrase: head whip → shoulder hit → side step → small kick → fast turn. Poses stay cartoon-exaggerated.

7.5–10.0s
Turn accelerates; camera orbits close. Environment recomposes to the choreography: checker yellow/green slides, hand-drawn crosses rotate, torn-paper strips snap, oversized comic type hits on drums (BAM, 叩, 炸). She lands hard, feet apart. A huge hand-drawn “BAM!” bursts under her feet and shakes every graphic layer. She rebounds upward immediately with a cocky smile — no held fashion pose.
10.0–12.3s
Same continuous body motion, camera racing along it: whip of the head → bright green eye → jade bun ornament → swinging black bun → bouncing earring → frog-button collar → floral qipao panel → stomping foot. Not a beauty-cut montage; one traveling shot. The footfall fires a jade-floral shockwave across the frame.

12.3–15.0s
Ride the shockwave back to full body. Two confident bouncing steps, abrupt pivot, finish facing camera: weight on one leg, shoulders slightly forward, cheeky rebellious grin. Buns and earrings still swinging. Background erupts into layered yellow paper, black brush X’s, white stars, green lotus line-art, spinning jade discs, rough ink. Elements snap into a 2000s punk magazine-cover lockup. Large “JADE PANIC!” type stacks behind her silhouette on the final beat. Hold her recognizable twin-bun / qipao silhouette. No design drift.
MOTION
Fast, bouncy, limited-animation timing: strong keys, overshoot, smear frames, anticipation, cartoon impacts. Hair buns, earrings, and qipao hem are the secondary rhythm; feet are the downbeat. Transitions grow only from action: skid → pattern flood → kick → rotating floral plane → spin → orbit → stomp → shockwave. No random cuts, no palm-to-lens, no pointing at camera, no outfit/hair morph.

AUDIO
Tight sync to fast Japanese pop-punk vocals, punchy electronic drums, distorted guitar. SFX: boot/foot skids, stomps, paper snaps, cartoon hits, guitar chops, short graphic whooshes. Type slams on snare/crash.
NEGATIVES
No hand reaching toward camera, no palm covering the lens, no pointing into the lens, no outfit transformation, no hairstyle transformation, no extra characters, no realistic rooms, no photorealism, no 3D CGI, no modern glossy anime, no cyberpunk holograms, no slow fashion posing, no facial drift, no random accessories, no excessive jump cuts, no disconnected moves, no uncontrolled morphing, no unreadable type, no pink hair, no red plaid school uniform.
```

</details>

<sub>Source: <a href="https://x.com/Just_sharon7/status/2094305294117429711">https://x.com/Just_sharon7/status/2094305294117429711</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 04 · Turning an Educational Vision into an Experience

<sub>Umesh &nbsp;·&nbsp; Unknown &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2084227244533411987.jpg" alt="Turning an Educational Vision into an Experience" width="100%">](https://x.com/umesh_ai/status/2084227244533411987)

<sub><b>▶ <a href="https://x.com/umesh_ai/status/2084227244533411987">Watch the clip on the creator's post on X (@Umesh)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for turning an educational vision into an experience on X. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (4,307 characters)</summary>

```text
Create a 15-second animated educational video that teaches young children the letters A, B, C, and D.

The learning pattern for every letter must be:

LETTER → SOUND → OBJECT → PLAYFUL ACTION → OBJECT NAME

Target audience: children ages 3 to 6.

Visual style:
Use adorable rounded 3D characters, soft pastel colors, gentle facial expressions, and simple recognizable objects. Combine this with a premium minimalist technology aesthetic featuring clean white space, elegant composition, soft studio lighting, subtle reflections, smooth gradients, rounded geometry, crisp typography, and extremely polished transitions.

The animation should feel playful and child-friendly while remaining calm, uncluttered, and beautifully designed.

Use a clean off-white background with a different soft color glow behind each letter.

0:00–0:01 | Introduction
A small smiling star mascot bounces into the center of the screen.

Colorful letters briefly float around it.

Display the text:

“Let’s learn!”

The mascot taps the screen, creating a soft ripple that reveals the first letter.

0:01–0:04 | A is for Apple

Show a large uppercase “A” and smaller lowercase “a” beside it.
Use thick, rounded, highly readable typography.

The narrator says:

“A. A says ah. A is for Apple.”

The uppercase A gently inflates and transforms into a shiny red apple.

Its top point becomes the apple stem, and a small green leaf unfolds from the side.

The apple gains a cute smiling face and performs one soft bounce.

Display the word:

“APPLE”

Highlight the first letter A in red.

Add a soft pop and a tiny crunchy sound.

0:04–0:07 | B is for Ball

The apple rolls across the screen and leaves behind a curved red trail.

The trail loops twice and forms a large uppercase “B,” with a lowercase “b” appearing beside it.
The narrator says:

“B. B says buh. B is for Ball.”

The two rounded sections of the B expand and merge into a colorful striped ball.

The ball bounces twice with playful squash-and-stretch animation.

Display the word:

“BALL”

Highlight the first letter B in blue.

Synchronize each bounce with a soft musical note.

0:07–0:10 | C is for Cat

On its final bounce, the ball stretches into a curved shape and becomes a large uppercase “C.”

A lowercase “c” slides gently into place beside it.

The narrator says:
“C. C says kuh. C is for Cat.”

The C rotates and becomes the curled tail of a cute orange cat.

The rest of the cat forms from soft rounded shapes.

The cat stretches, blinks, and gives one gentle wave with its paw.

Display the word:

“CAT”

Highlight the first letter C in orange.

Add a quiet and friendly “meow.”

0:10–0:13 | D is for Duck

The cat’s tail uncurls and transforms into the curved side of a large uppercase “D.”

A lowercase “d” pops up beside it.

The narrator says:

“D. D says duh. D is for Duck.”
The straight line of the D becomes the duck’s neck.

The curved section becomes its round yellow body.

A small orange beak and two tiny wings pop into place.

The duck waddles forward, flaps its wings, and gives one cheerful quack.

Display the word:

“DUCK”

Highlight the first letter D in yellow.

Add tiny water ripples beneath its feet.

0:13–0:15 | Recap

The apple, ball, cat, and duck slide into four clean rounded tiles.

Place their letters above them:

“A  B  C  D”

The mascot returns and points to each object as they bounce once in sequence.

Narrator:
“A, B, C, D. Great job!”

Finish with the text:

“Great job!”

Use a small sparkle animation and a warm musical chime.

Animation requirements:

Keep each letter fully visible for a moment before it transforms.

Show uppercase and lowercase versions clearly.

Make every object instantly recognizable.

Use smooth shape morphing so children can visually understand how the letter becomes the object.

Maintain stable spelling, clean letterforms, accurate object shapes, and consistent character design.

Use gentle squash-and-stretch, soft motion blur, subtle shadows, polished lighting, and precisely synchronized sound effects.
Avoid fast camera movement, cluttered backgrounds, harsh colors, tiny text, warped letters, random symbols, duplicated objects, scary expressions, or overly complex transformations.

The final video should feel cute, educational, memorable, calming, and exceptionally polished.
```

</details>

<sub>Source: <a href="https://x.com/umesh_ai/status/2084227244533411987">https://x.com/umesh_ai/status/2084227244533411987</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 05 · Escaping a Manga Book, Meeting Another Self

<sub>ai_lifehack55 &nbsp;·&nbsp; Unknown &nbsp;·&nbsp; 15.139 &nbsp;·&nbsp; 1440p &nbsp;·&nbsp; 1:1</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2094985989404205107.jpg" alt="Escaping a Manga Book, Meeting Another Self" width="100%">](https://x.com/ai_lifehack55/status/2094985989404205107)

<sub><b>▶ <a href="https://x.com/ai_lifehack55/status/2094985989404205107">Watch the clip on the creator's post on X (@ai_lifehack55)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A manga character emerges from the pages into live action and discovers another version still inside. The prompt references multiple images; some panel and speech-bubble exclusions are not followed.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (2,767 characters)</summary>

```text
【REFERENCE】
Image1 `01 / SCENE_TRAPPED`：本の中に閉じ込められた第一場面、巨大本、室内、人物の位置とポーズ。
Image2 `02 / SCENE_BREAKTHROUGH`：ページを押し破る第二場面、動作、紙の亀裂。
Image3 `03 / SCENE_EMERGENCE`：現実へ出た第三場面、破れ穴、着地位置。
Image4 `04 / SCENE_ENCOUNTER`：本の中の自分と対面する第四場面の左右、指差し、巨大本。
Image5 `05 / WOMAN_MASTER`：利用者が差し替える女性全身アンカー。顔、髪、年齢感、肌、体型、全身比率、衣装、素材、配色、靴の唯一の正本。
`06 / MANGA_SELF`：05を同じ人物・衣装のままモノクロ漫画化した状態。
`07 / REAL_SELF`：05を正確に維持した実写状態。
`08 / BOOK_ROOM`：01～04共通の巨大な見開き本、木製床、寝具、カーテン、植物、暖かな昼光の寝室。

各ショットはIDだけで参照する。01～04の女性からは位置、ポーズ、動作だけを使い、外見は使わない。人物同一性は05を最優先し、06と07を同一人物の二状態とする。女性アンカーの差し替えごとに05から読み直す。場面アンカーの吹き出し、印刷文字、コマ枠、白い分割余白は使わない。

【CONDITION DEFINITION】
15秒、1:1。シネマティック実写と精密なモノクロ漫画の融合。実写は自然な肌、布、髪、暖かな立体光、漫画は紙目、網点、インク線を明瞭に分ける。4パネルは物語アンカーで、カット数は4つに限定しない。前半は真剣な脱出劇、最後は「自分が本の中に残る」不条理を驚きとパロディーへ転換。表情は困惑→恐怖→決意→安堵→違和感→強い驚き。顔を変形させず眉、瞳、口、顎、肩、呼吸を連動する。0.0～4.6秒は全身を本の印刷面内に閉じ込めた平面モノクロ漫画とし、紙の内側から現実側へ押す。肌色、実写衣装、立体化、身体突出、床への接地は4.6秒から。

【SHOT / FLOW】
0.0～1.0秒【参照：01、06、08】巨大本を低い広角で見せ、本の中へ高速プッシュイン。MANGA_SELFは困惑して見回し、眉が寄り呼吸が浅くなる。
1.0～3.3秒【参照：01、06】顔、境界を探る手、紙を押す横顔をハードカット。目が泳ぎ口元が震える。紙越しに「ここは……どこ？　出られない……」。継ぎ目を見つけ、恐怖から決意へ。
3.3～4.6秒【参照：02、06、08】低い斜め前方。踏ん張る靴、紙へ食い込む指、歯を食いしばる顔を三連続で切る。「あいて……！」。集中線と黒インクの圧力リングが手から広がる。
4.6～6.8秒【参照：02、05、06、07、08】紙が現実側へ膨らみ、手、顔、上半身、脚の順に平面のインクと紙繊維が07の肌、髪、衣装へ連続変換。境界で網点が色粒子へ変わる。カメラは裂け目を半周し、立体化に合わせ被写界深度を浅くする。破裂時、手描きの`バリッ！`が手前へ飛び、黒インク片へ砕け0.35秒以内に消える。女性は一人のまま05を維持する。
6.8～8.4秒【参照：03、05、07、08】REAL_SELFが紙片と床へ着地し少しよろける。低い追従から顔へ寄る。両手と参照衣装を確認し、驚きが安堵と小さな笑みへ。「出られた……？」。
8.4～10.3秒【参照：05、07、08】乾いたページ音。BGMに合わせ笑みが止まり、口角が落ち、眉が上がり、瞳だけ本へ動く。つばを飲み恐る恐る振り向く。顔から本へ高速ホイップパンし、肩越しのまま10.3秒の04へ接続。安堵が違和感へ変わる。
10.3～11.2秒【参照：04、05、06、07、08】左右が読める中広角。左のREAL_SELFと本の中央のMANGA_SELFが同時に指を差し、終端で短くヒットストップ。BGMはレコードスクラッチで急停止。
11.2～12.8秒【参照：04、05、06】MANGA_SELFへスマッシュズーム。目と口を大きく開き、頬のハッチングが増える。紙越しに「まさか……本当に出てきた！？」。背後に放射状の漫画線。
12.8～14.0秒【参照：04、05、07】85mm相当でREAL_SELFの顔へスマッシュズーム。05の顔比率を保ち、眉が跳ね、瞳孔が縮み、口が開き、肩が引ける。短い間の後、室内音声で「あなた……誰？」。
14.0～15.0秒【参照：04、05、07】85mmのまま一段近い驚き顔。顔と衣装はカラー、背景だけ白黒ハーフトーンと集中線へ変わり、巨大な`！？`が頭の後ろから出て一度弾む。本、カメラ、本の順に二度見し、コミカルな一音で終了。

【CAMERA / EDITING】
広角、顔、手元、低角度、短い回り込み、ホイップパン、交互スマッシュズームを使い、同じ中広角を続けない。動作か表情変化で切り、長い静止、スロー、無目的な360度回転、フェードなし。最終4.7秒は対面、交互リアクション、驚き顔アップの順に加速。

【MOTION GRAPHICS / TYPOGRAPHY】
集中線、ハーフトーン、インクの圧力リング、短いヒットストップ、紙片の奥行きを使う。`バリッ！`は黒インク、`！？`は白文字に赤いずれ影。わずかにオーバーシュートし、顔を隠さない。表示文字はこの二つだけで字幕や吹き出しにしない。

【SOUND】
overall_soundscape:
紙越しと室内の声は同じ基礎声質で距離感だけ変える。紙の張り、破裂、紙片、着地、衣擦れ、ページ音を画面へステレオ同期。台詞を重ねず、追加の声や笑い声なし。
non_diegetic_music:
0.2秒の演出無音を除き全編に約90 BPMのミステリーコメディーBGMを連続使用。ピチカート弦、バスクラリネット、チェレスタ、軽い打楽器。脱出まで上昇し、破裂で低音と打楽器を同期、着地後は一瞬明るくする。10.3秒でレコードスクラッチ後0.2秒だけ無音、以後は低いピチカート、最後は乾いた一音。台詞中はダッキング。

【NEGATIVE】
場面アンカーの吹き出し、縦書き文字、複数コマ、白い分割余白を出さない。許可した`バリッ！`と`！？`以外の文字、字幕、ロゴ、透かしなし。第三の女性、同一状態の重複、01～04の人物外見流用、別人化、05の人物・衣装・配色の逸脱、広角による顔変形、4.6秒前の肌色・実写化・立体化・身体突出・床接地、解剖学的変形、無表情、10.3秒以降の長い同一構図、指定0.2秒以外のBGM欠落、イベント順の変更を避ける。
```

</details>

<sub>Source: <a href="https://x.com/ai_lifehack55/status/2094985989404205107">https://x.com/ai_lifehack55/status/2094985989404205107</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 06 · A Live-Action Muse Meets a Tiny 2D Fairy

<sub>ImaStudio_ai &nbsp;·&nbsp; Unknown &nbsp;·&nbsp; 15.402 &nbsp;·&nbsp; 720p &nbsp;·&nbsp; 16:9</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2095357375549182080.jpg" alt="A Live-Action Muse Meets a Tiny 2D Fairy" width="100%">](https://x.com/ImaStudio_ai/status/2095357375549182080)

<sub><b>▶ <a href="https://x.com/ImaStudio_ai/status/2095357375549182080">Watch the clip on the creator's post on X (@ImaStudio_ai)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A tiny drawn fairy interacts with a live-action woman through palm contact and mirrored poses. Character reference images are required by the published prompt.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (4,871 characters)</summary>

```text
Create a 15-second, 16:9, 24fps ultra-photorealistic live-action Y2K fashion film blended with one pure 2D manga fairy.
HIGHEST-PRIORITY RULES
Exactly TWO characters: ONE fictional 22-year-old Korean female idol + ONE tiny 2D manga fairy. No extras, duplicates, clones, motion-trail copies, or identifiable reflections.
ZERO readable text or numbers anywhere: no captions, logos, labels, signs, UI, watermarks, license plates, posters, or environmental writing.
CHARACTER LOCK
Woman: elegant oval face, cool fair skin with realistic texture, almond eyes, glossy pink lips, extremely long silky straight black hair to the waist with thin bangs. Face, hair, proportions, makeup and wardrobe remain identical.
Wardrobe: black satin cropped camisole with lace detail, cropped glossy motorcycle jacket loosely around her arms, black low-rise pleated micro skirt, silver waist chain/jewelry, black over-the-knee boots. Premium, sensual, sophisticated K-pop editorial.
Fairy: tiny PURE 2D cel-shaded manga character with clean outlines, short black hair, elf ears, large pink eyes, pink-and-white cropped top, silver pleated skirt, translucent pink wings. Always flat 2D—never 3D, photorealistic, or humanized.
ENVIRONMENT
One continuous bright pink-and-ice-blue neon fashion studio. Black vintage convertible in the center, silver vanity mirror, transparent acrylic chair, chrome spheres, silver props, glossy floor. Style: K-pop comeback film × glossy Y2K campaign × cute high-energy MV.
PHYSICAL CONTINUITY
No teleportation, clipping, spawning, or passing through objects. Fairy must physically fly above, below, around, or beside the windshield, car, mirror, chair, props, and woman. Glossy surfaces show only abstract light, never recognizable reflections.

SHOT FLOW
0:00–0:01.5 — Low-angle wide shot. Only fairy is visible behind the wheel. She waves, opens wings on beat, flies vertically until fully above the windshield, exits through the open roof, half-spins, then flies toward the woman. Driver seat becomes empty.
0:01.5–0:03.5 — Reveal woman leaning outside the car door, looking down while adjusting a ring. Fairy curves toward her shoulder and gives a TA-DA pose. The same woman raises her head, looks at fairy, then camera. Diagonal push-in from headlight.
0:03.5–0:05.5 — Woman flicks one finger toward fairy on a sharp beat. Fairy reacts with one continuous half-spin to camera-right. Woman shifts into a mischievous smile. Fast side arc; car door briefly wipes foreground.
0:05.5–0:07.5 — Fairy flies around the OUTER edge of the vanity mirror, never through it. Camera follows and finds the same woman seated on the acrylic chair. She crosses her legs and makes a tiny finger heart. Fairy hovers beside her face and imitates it. Woman smiles.
0:07.5–0:09.5 — Woman opens her palm. Fairy descends continuously and visibly lands, feet making contact. Fairy poses proudly and copies woman’s head tilt. Woman pauses, then smiles warmly. Add a cute electronic bling; push from hand toward faces.
0:09.5–0:11.5 — Fairy physically takes off from palm first. Woman stands and walks 2–3 confident steps toward center studio. Camera tracks backward with a lateral arc while fairy flies backward in front of her.
0:11.5–0:13.0 — Woman strikes a sophisticated K-pop pose with convertible diagonally behind. She touches her long hair; fairy imitates fixing her own short hair. Woman notices and breaks into a smile. Slight low-angle push-in.
0:13.0–0:14.5 — Medium close-up. Woman makes a finger heart near her face while holding her hair. Fairy hovers beside her, wings open, cheerful double-V pose. Both look into camera. Final beat triggers ONE camera flash without washing out the studio.
0:14.5–0:15.0 — Freeze the ACTUAL previous frame. No new photo, card, border, or white background. Keep neon studio, car, silver props and depth visible. Add only 4–6 small clean pink hearts/stars/sparkles near the corners, inside frame, never covering either character.
CAMERA & PERFORMANCE
Use low angles, diagonal views, subtle ultra-wide shots, foreground occlusion, mirror framing, curved push-ins, short tracking, gentle rises/drops. Avoid repetitive static frontal framing.
Emotion: cool fashion pose → curiosity → playful interaction → amused smile → joyful final pose. Natural, confident, star-like, never childish.
MUSIC
Bubblegum Pop × Kawaii Pop × Y2K Dance Pop, 125–135 BPM, punchy drums, bouncing bass, crisp claps, sparkling synths. Sync wing opening, finger flick, fairy spin, finger-heart, palm landing, takeoff, hair imitation, final pose and camera flash to major beats.
NEGATIVE
No second human/fairy, duplicates, face drift, hairstyle/color/costume changes, malformed hands, clipping, teleportation, 3D or photorealistic fairy, white ending, Polaroid/frame/PIP, chaotic doodles, readable text, letters, numbers, logos, subtitles, labels, UI or watermarks.
```

</details>

<sub>Source: <a href="https://x.com/ImaStudio_ai/status/2095357375549182080">https://x.com/ImaStudio_ai/status/2095357375549182080</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 07 · A Lemon-Themed Girl Powers a Bright Motion Ad

<sub>Sharon Riley &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2544×1456 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2095516988743225637.jpg" alt="A Lemon-Themed Girl Powers a Bright Motion Ad" width="100%">](https://x.com/Just_sharon7/status/2095516988743225637)

<sub><b>▶ <a href="https://x.com/Just_sharon7/status/2095516988743225637">Watch the clip on the creator's post on X (@Sharon Riley)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A blonde anime girl presents lemonade through yellow typography, circular motifs, and fast graphic transitions. Native-video output: 15s · 2544×1456. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (4,664 characters)</summary>

```text
LUMI is an elegant, cheerful anime girl with long, vivid lemon-yellow hair with blunt bangs, honey-amber almond eyes with dramatic lashes, soft pink blush, a small mint-green hairpin, dangling lemon-slice earrings, a yellow ruffled off-shoulder top layered over a white halter crop top, and holds a tall glass of sparkling lemonade with ice and lemon slices. Preserve her exact face, proportions, hairstyle, outfit, materials, accessories and colors throughout; never redesign her.

This film is 80% bold graphic design in motion and 20% character action: giant kinetic typography, hard-edged citrus shapes, flat color fields, sunburst rays, halftone dots, juice-splash graphics, speed lines and shutter flashes. Palette: lemon yellow, citrus gold, cream white, soft blush pink, mint accent. Style: premium AAA motion-graphics title sequence x citrus lifestyle campaign film. Every graphic element moves fast and snaps hard on the beat.

CUT 01 | 0.00–1.00s – Pure graphics: a giant lemon-yellow wordmark "LUMI" slams onto a cream field with a sunburst-ray flash; halftone dots pulse and tiny citrus-slice UI ticks flicker along the frame edges.

CUT 02 | 1.00–2.10s – Cream-white field, huge black outline letters "FRESH" drop in and bounce; she twirls into frame holding her lemonade glass aloft, ruffles fluttering, sparkle particles trailing behind her.

CUT 03 | 2.10–3.10s – Close shot: she lifts the glass and takes a slow sip, eyes glinting; a fizz of golden bubbles erupts around her as kinetic type "ZEST" spins and locks into place behind her shoulder.

CUT 04 | 3.10–4.10s – Flat citrus-yellow field: she spins her glass and lemonade splashes upward in a stylized graphic arc that freezes mid-air as the wordmark "SPLASH" bursts through the liquid shape.

CUT 05 | 4.10–5.10s – Hard cut to cream field: giant outlined type "POUR" tilts diagonally; she pours a stream of golden lemonade into her glass, the falling stream morphing into the letterforms as it lands.

CUT 06 | 5.10–6.10s – Sunburst radial wipe: she flicks a lemon slice off the rim of her glass toward camera; it spins in slow motion catching the light, while the word "CITRUS" scatters into halftone dot particles.

CUT 07 | 6.10–7.10s – Slow hair-flip, her hair rippling like liquid gold; speed lines and sparkle bursts trail from it as the giant type "GOLDEN" ripples across the frame in sync with the movement.

CUT 08 | 7.10–8.10s – Kinetic type barrage: SWEET / COOL / BRIGHT / SUNNY slam in one per beat with shutter flashes and camera shake, while she raises her glass in a toast toward camera, ice clinking in slow motion.

CUT 09 | 8.10–9.10s – Cream cyclorama: she tilts her head back with a light laugh, hair catching the wind; a cluster of citrus-slice graphics and sparkle motes swirl around her in a slow orbiting halo.

CUT 10 | 9.10–10.10s – Layered flat-color glass panes (lemon yellow, cream, blush) shatter one by one, each revealing a bigger letter of "LUMI" underneath, as she steps forward through the breaking panes.

CUT 11 | 10.10–11.10s – Giant halftone sunburst rays pulse outward from behind her in rhythm with a bass drop, lemon-slice confetti raining down as she smiles and lightly lifts her glass higher.

CUT 12 | 11.10–13.00s – Hero moment on a clean cream cyclorama: she stands center frame, glass raised, warm confident smile, as a shockwave of concentric golden rings, citrus confetti and wind-rippled ruffles blasts outward from her; brief iconic freeze, overexpose to white.

CUT 13 | 13.00–15.00s – Final identity card: an enormous black "LUMI" wordmark dominates a pale cream field with translucent lemon-yellow rings, sunburst arcs, halftone dots and a circular emblem containing a lemon-slice motif; she stands relaxed beside the letters, glass in hand, hair rippling in the breeze; one last golden light pulse sweeps through the typography and a soft chime accent punctuates the end.

Editing: aggressive, stylish rhythm — hard cuts on every beat, graphic matches, snap zooms, speed ramps, shutter flashes and impact pulses; every cut must feel compositionally different; typography is always fully readable before the character overlaps it.

No weapons, no combat, no fire; all energy comes from motion design, light, liquid, glass and citrus.

BGM: bright, uptempo pop/electro-swing with fizzy drops and glitch fills locked to every cut; glass clinks, fizz pops, fabric flutter and sparkle chimes as rhythmic sound-design elements. Peak at CUT 12 and end with a warm chime logo stinger.

Premium AAA quality, anime-inspired cinematic rendering, stylish and vibrant, strong graphic-design identity, consistent character design, exactly 13 cuts
```

</details>

<sub>Source: <a href="https://x.com/Just_sharon7/status/2095516988743225637">https://x.com/Just_sharon7/status/2095516988743225637</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 08 · A City Painted into Existence

<sub>aimikoda &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15.168 &nbsp;·&nbsp; 1440p &nbsp;·&nbsp; 16:9</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2094490203335352524.jpg" alt="A City Painted into Existence" width="100%">](https://x.com/aimikoda/status/2094490203335352524)

<sub><b>▶ <a href="https://x.com/aimikoda/status/2094490203335352524">Watch the clip on the creator's post on X (@aimikoda)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Oil-paint ridges turn into streets and landmarks before resolving into an Edinburgh poster. The published prompt includes city and quote variables.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (3,294 characters)</summary>

```text
[CITY_NAME] = EDINBURGH
[QUOTE] = A city carved from stone and story.

Create a fast, dense, cinematic 16:9 macro travel film where the entire identity of [CITY_NAME] is continuously painted into existence by living oil paint.

Use a low grazing macro camera with extremely shallow depth of field. The world is a vast canvas covered in thick wet impasto paint, sculpted brushstroke ridges, carved grooves, glossy reflections and dense gold glitter. The paint must behave like an active force at all times. It flows like rivers, sweeps like brushwork, gathers like tides, curls at the edges, spills into new paths and physically constructs the city in real time.

The film must feel fast, rich and uninterrupted. Use one continuous flowing camera move with no cuts. The camera races across the canvas, skimming over wet paint valleys, weaving between rising structures, accelerating through the city as new landmarks constantly appear ahead. Avoid slow drifting. Keep the visual progression energetic and tightly packed.

Start with abstract moving pigment and rapidly transition into recognizable city formation. Show thick paint strokes being laid down, dragged, folded and pulled into shape by an invisible artistic force. Let streams of pigment split and merge like waterways, while dimensional brushstroke masses rise into streets, bridges, domes, towers, rooftops, plazas, canals and layered miniature architecture. Make the city feel as if it is being painted and built at the same time.

Reveal many landmarks across the journey, not just one. Let the camera travel seamlessly through the whole city, with one landmark flowing directly into the next. As the camera advances, fresh paint forms arches, facades, bell towers, canal edges, stairways, statues, porticoes and skyline silhouettes associated with [CITY_NAME]. The transitions between landmarks should feel fluid and continuous, with brushstrokes extending forward to pull the viewer deeper into the city.

Make the paint motion highly visible and expressive. Show pigment actively spreading across canvas, pouring into channels, stacking into forms, curving into structures and leaving wet textured trails behind. Gold glitter should move with the paint and collect along ridges and valleys, creating sparkling highlights that emphasize speed, direction and shape.

Use warm golden key light from the lower left to ignite glossy paint and glitter. Add cool purple-blue ambient fill from the upper right to maintain a dreamy dusk atmosphere. Keep the distant background soft with haze and circular bokeh, but preserve strong clarity on the active foreground paint and newly formed landmarks.

Toward the end, the camera rises and pulls back just enough to reveal a broader final view of the fully formed painted city, making it clear that the viewer has traveled through an entire living city built from moving paint.

End on a striking travel-poster composition. Place elegant typography in the top left with generous breathing room. Show [CITY_NAME] in refined serif uppercase, with [QUOTE] beneath it in smaller delicate type.

The overall feeling should be luxurious, poetic and visually intense, with continuous motion, dense landmark reveals and the clear impression that the whole city is being painted alive in real time.
```

</details>

<sub>Source: <a href="https://x.com/aimikoda/status/2094490203335352524">https://x.com/aimikoda/status/2094490203335352524</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 09 · Building a Character Bust from Scratch

<sub>aimikoda &nbsp;·&nbsp; Unknown &nbsp;·&nbsp; 15.168 &nbsp;·&nbsp; 1440p &nbsp;·&nbsp; 4:3</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2095141166962311555.jpg" alt="Building a Character Bust from Scratch" width="100%">](https://x.com/aimikoda/status/2095141166962311555)

<sub><b>▶ <a href="https://x.com/aimikoda/status/2095141166962311555">Watch the clip on the creator's post on X (@aimikoda)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Hands assemble an armature, sculpt a face and add paint, hair and accessories to a finished character bust. The prompt requires a character reference image.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (3,279 characters)</summary>

```text
A cinematic creation film follows one maker reconstructing the main subject shown in the referenced image completely from scratch. The referenced image defines the finished subject’s complete visible appearance, proportions, structure, materials, colors, clothing or surface details, and distinctive features; ignore its background, framing, lighting, and unrelated elements.  Begin directly on an empty, clean virtual workbench. Use a stable front three-quarter overhead view that keeps the developing subject readable. There is one maker throughout, represented by the same consistent left and right hands and forearms. Show no more than two hands at once.  From 0 to 14 seconds, the entire creation unfolds as a clearly accelerated timelapse with rapid, purposeful hand movement and restrained motion blur. Short jump cuts compress repetitive manual work only after each action has visibly completed. Every cut inherits the exact form and progress left by the previous action.  0-2 seconds: One hand enters already holding the first foundation material, armature, or base element appropriate to the referenced subject and places it at the center. The second hand steadies it as the maker establishes the initial supporting form.  2-8 seconds: The maker rapidly develops the subject’s major structure and volumes using one coherent creation method appropriate to what the referenced image depicts. A living subject is sculpted as one continuous, non-gory digital form from armature to anatomy; a vehicle or machine is built from chassis to functional structure; an object is formed or assembled from its supporting body outward. Each additional material or component enters from outside the frame while firmly held by one of the maker’s hands, is carried to its destination, and remains under hand control until attached or shaped.  8-12 seconds: The same hands develop the recognizable outer form and reference-specific features. The maker sculpts, fits, wraps, stitches, fastens, carves, or polishes only where appropriate to the subject. Facial features, hair, clothing, body panels, wheels, glass, surfaces, accessories, or equivalent defining elements emerge through visible hand and tool contact, never through spontaneous transformation.  12-14 seconds: The maker refines proportions, edges, joints, surface transitions, textures, colors, and distinctive details until the developing subject closely matches the referenced image. One hand stabilizes the form while the other performs each final adjustment with a hand-held tool.  14-15 seconds: The maker removes the last tool by hand and withdraws both hands. The timelapse returns to normal speed as the camera makes a restrained push toward the completed subject and holds on a clean final view.  Materials and components do not need to be visible before use, but anything newly introduced must enter the frame already held by one of the maker’s hands. Nothing moves, assembles, appears, disappears, or changes material independently. Maintain one maker, one continuous subject, one creation position, and one category-appropriate construction method. No assistants, extra hands, detached anatomy, duplicated elements, magical morphing, drawing phase, software interface, cursor, menus, annotations, or text overlays.
```

</details>

<sub>Source: <a href="https://x.com/aimikoda/status/2095141166962311555">https://x.com/aimikoda/status/2095141166962311555</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 10 · Two Hands Draw a Woman at Her Vanity from Blank Paper

<sub>Sharon Riley &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2544×1456 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2095473707611553897.jpg" alt="Two Hands Draw a Woman at Her Vanity from Blank Paper" width="100%">](https://x.com/Just_sharon7/status/2095473707611553897)

<sub><b>▶ <a href="https://x.com/Just_sharon7/status/2095473707611553897">Watch the clip on the creator's post on X (@Sharon Riley)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A pencil builds an outline, facial features, and vanity objects from blank paper until a detailed colored portrait is complete. Native-video output: 15s · 2544×1456. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (3,242 characters)</summary>

```text
A completely blank sheet of smooth white paper fills the frame. Two hands enter from the bottom. The right hand holds a sharpened graphite pencil; the left hand rests lightly at the lower-left corner of the paper to keep it still.
The right hand makes the first mark: a very light, loose oval in the center of the page for the head. Immediately add a faint vertical center line and a horizontal eye-line crossing the middle of the oval. Draw two short marks for the brow line and the base of the nose, then a light curve for the chin. All construction lines stay pale and barely visible.
Next, block in the neck as two simple sloping lines and a shallow U for the shoulders and collarbones. Sketch a rough rectangle for the torso and the square neckline of the top. Still using only the lightest pressure, place a large circle on the left for the round vanity mirror and a few vertical ovals and cylinders across the bottom for bottles and brush handles. Nothing is detailed yet—only placement.
Now the face. Darken the eye-line slightly and draw the almond shapes of both eyes, leaving a small highlight circle in each iris. Add the upper lids, a few lashes, and the gentle arch of the brows. Move to the nose: a soft wedge and two small nostril curves. Then the mouth: a short center dip, the full upper lip, and the slight upward curve of the smile. Keep every stroke inside the original oval.
Shift to the hair. Start at the hairline and draw the high, messy half-up bun with the flower-shaped clip on top and the two small barrettes on the right side. Pull long, wavy strands down the left side of the face and over the right shoulder, using loose, overlapping S-curves. Let a few shorter pieces fall across the forehead.
Refine the clothing: the ribbed texture of the white top, the thin orange trim around the neckline and sleeve, and the tiny bow at the center. Add the thin necklace chain and its small pendant. Darken the contour of the right hand resting against the cheek, fingers relaxed.
Move to the foreground still life. Outline the gold-framed round mirror on the left, then the cluster of bottles—tall toner bottle, perfume with a faceted cap, pump bottles, and the cup of makeup brushes on the right. Keep these objects slightly lighter so they sit in front of the figure without competing.
Begin shading. Hatch soft graphite under the chin, along the left side of the nose, beneath the lower lip, and in the hollow of the neck. Build darker value in the hair where strands overlap and around the clips. Add light cross-hatching on the fabric folds of the top and a faint cast shadow from the hand onto the cheek. Leave the paper white for the brightest highlights on the forehead, nose tip, and lip.
The left hand slides out of frame. The right hand makes a few final tightening strokes on the eyes and the edges of the hair, then rests the pencil at the top of the paper. The finished drawing is a complete graphite sketch of the blonde woman at her vanity, built entirely from the first faint oval to the last shadow, on otherwise empty white paper.
Satisfying, calm, close-up process video. Continuous take, no cuts, no extra motion except the hands and pencil. Soft natural light, visible pencil grain and paper tooth.
```

</details>

<sub>Source: <a href="https://x.com/Just_sharon7/status/2095473707611553897">https://x.com/Just_sharon7/status/2095473707611553897</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 11 · A Vintage 1947 Town Under Fire

<sub>Ruzaina &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1280×720 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2087117707816714552.jpg" alt="A Vintage 1947 Town Under Fire" width="100%">](https://x.com/RuzainaMeer/status/2087117707816714552)

<sub><b>▶ <a href="https://x.com/RuzainaMeer/status/2087117707816714552">Watch the clip on the creator's post on X (@Ruzaina)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Period buildings, vintage cars, soldiers, smoke, and debris form a documentary-like 1940s film sequence. Native-video output: 15s · 1280×720. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (3,119 characters)</summary>

```text
Create a 15-second ultra-photorealistic live-action war sequence set in the United States in 1947, designed to look like authentic historical footage captured on a 1940s film camera. The entire scene must feel grounded, documentary-like, raw, and physically realistic.
Environment: A rural American town in 1947 with wooden houses, old brick buildings, telephone poles, dirt roads, vintage American cars from the 1940s, wooden fences, farmland, and period-accurate street details. Overcast afternoon light, light fog, drifting smoke, dust in the air, damaged buildings, scattered debris, and a tense wartime atmosphere.
Characters: American soldiers wearing historically accurate late-1940s military uniforms, helmets, boots, and equipment. Civilians wear authentic 1940s American clothing. Natural faces, realistic skin texture, sweat, dirt, fatigue, and believable body movements.
0–3s — Establishing Shot:
Wide handheld shot of a quiet rural American street suddenly filled with smoke and confusion. Vintage 1940s vehicles are parked along the road while soldiers move quickly between wooden buildings. Civilians rush toward safer areas.
3–6s — Tension:
Camera moves through the street at shoulder height, following several soldiers as distant gunfire is heard. They immediately react and take cover behind a vintage vehicle and a brick wall. Their movements are cautious and realistic.
6–10s — Combat:
Fast handheld tracking shot as the soldiers move between cover while distant gunfire impacts the environment. Small pieces of wood, dust, and debris fall naturally from nearby impacts. Weapon recoil, movement, and body weight must be physically accurate. Keep the violence realistic and restrained.
10–13s — Human Moment:
Camera briefly focuses on a soldier helping an injured civilian move behind cover. Their breathing, facial expressions, body language, and movement should feel natural and unscripted.
13–15s — Final Shot:
Camera pulls back into a wide shot of the American town as smoke slowly moves through the street. Soldiers remain behind cover while vintage vehicles and damaged buildings fill the background. The scene ends with an authentic, tense 1940s documentary feeling.
Visual Style: Ultra-photorealistic live-action, authentic 1940s American environment, vintage 35mm film texture, subtle film grain, natural imperfections, realistic exposure, handheld documentary cinematography, muted historical color palette, realistic smoke and dust, natural shadows, accurate depth of field.
Physics: Strictly obey real-world gravity, momentum, inertia, friction, recoil, weight, collision physics, and human biomechanics. No exaggerated explosions, impossible movements, superhero behavior, or choreographed-looking combat.
Negative Prompt: modern buildings, modern cars, smartphones, modern clothing, modern weapons, futuristic technology, CGI appearance, video-game graphics, fantasy, superhero action, excessive explosions, excessive blood, gore, impossible physics, unrealistic recoil, slow-motion physics, distorted faces, extra limbs, floating objects, plastic skin, artificial-looking environments.
```

</details>

<sub>Source: <a href="https://x.com/RuzainaMeer/status/2087117707816714552">https://x.com/RuzainaMeer/status/2087117707816714552</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 12 · Kaze’s Player Stats Screen Powers Up

<sub>Kōda &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 720×1280 &nbsp;·&nbsp; portrait</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2086122377633575169.jpg" alt="Kaze’s Player Stats Screen Powers Up" width="100%">](https://x.com/aimikoda/status/2086122377633575169)

<sub><b>▶ <a href="https://x.com/aimikoda/status/2086122377633575169">Watch the clip on the creator's post on X (@Kōda)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Kaze and the football emerge from a dark scanner pass as the nameplate, level, overall rating, and attribute bars animate into place. Native-video output: 15s · 720×1280. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (2,925 characters)</summary>

```text
@[ref img] is the sole visual authority for Kaze, the football, the complete player-stats interface, typography, numbers, icons, colors, lighting, layout, and vertical composition. Animate this exact screen without redesigning it. Preserve all existing labels and final stat values.
[Goal]
Create a polished 15-second anime sports-game player stats screen opening. Use one continuous, locked, straight-on full-screen composition with no camera movement, cuts, cropping, or perspective distortion.

[Sequence]
0–2.2 seconds: Begin from near-black teal. A faint horizontal scanner passes downward, revealing Kaze’s silhouette and the outer edges of the interface. Fine particles and dim mint circuitry flicker awake.
2.2–5.5 seconds: The header, KAZE nameplate, role badge, level panel, and overall panel resolve through clean line-draw animations. Kaze emerges fully from shadow, takes a controlled breath, subtly shifts her shoulders and raised arm into the referenced pose, then fixes an intense gaze toward the viewer. Her hair, ribbons, and loose clothing react naturally to a growing current of wind. The football begins a slow, stable rotation beside her hand.

5.5–10.8 seconds: The large overall score counts rapidly upward and lands precisely on 92. The level settles on 46. Each attribute bar fills smoothly from left to right in sequence—Speed 93, Power 91, Control 88, Stamina 90, Agility 94, Technique 89—each landing with a restrained mint pulse. The radar chart draws outward from its center and locks into the exact final polygon. Skill cards activate from top to bottom; their icons flare briefly while the ACTIVE and ULTIMATE states illuminate.
10.8–13.3 seconds: The player ID strip and bottom navigation fade and slide into their exact final positions. The wind energy around Kaze accelerates clockwise, wrapping around the rotating ball and sweeping behind her body with layered luminous trails. Kaze tightens her hand, leans slightly into the current, and gives one natural blink; preserve her identity, anatomy, costume, and right-side placement.

13.3–15 seconds: The energy arc reaches a bright controlled crest, then settles into a living idle pulse. Hold the fully assembled screen matching @[ref img] exactly. Kaze continues subtle breathing; hair and ribbons drift, the football rotates slowly, particles shimmer, and all stats remain stable and readable.

Use crisp premium game-UI motion, clean 2D anime character animation, subtle depth between Kaze and the interface, and stable legible typography. Keep every panel, icon, label, number, and geometric boundary fixed once revealed. Do not introduce new text, extra characters, additional objects, logos, captions, or UI elements.

Audio: low electronic boot hum, delicate scanning ticks, short confirmation tones as values lock, rising airy wind around the ball, soft cloth movement, and one refined completion chime. No dialogue and no music.
```

</details>

<sub>Source: <a href="https://x.com/aimikoda/status/2086122377633575169">https://x.com/aimikoda/status/2086122377633575169</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 13 · A Cinematic Character Entrance in the Wind

<sub>Kōda &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2410×2560 &nbsp;·&nbsp; portrait</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2086412223061135392.jpg" alt="A Cinematic Character Entrance in the Wind" width="100%">](https://x.com/aimikoda/status/2086412223061135392)

<sub><b>▶ <a href="https://x.com/aimikoda/status/2086412223061135392">Watch the clip on the creator's post on X (@Kōda)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The camera rises from costume and body details into profile, silhouette, and final hero framing as the environment moves in the wind. Native-video output: 15s · 2410×2560. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (2,393 characters)</summary>

```text
Use @[char ref] as the sole character reference. Preserve the exact identity, face, body proportions, hairstyle, outfit, colors, materials and overall silhouette of the character throughout the entire video. Do not redesign, simplify or replace any defining visual features.

Create a cinematic character introduction focused on presence, silhouette, attitude and controlled motion.

0–4s
Begin with a close shot of a defining lower-body or detail element such as boots, shoes, feet, hands, clothing hem or an important accessory. The character enters frame or settles into position. The camera slowly tracks upward while hair, clothing and secondary elements move naturally in the wind or environment.

4–8s
Reveal more of the body with a medium or medium-wide shot from the back, side or three-quarter angle. The character stands in a calm, composed way inside the environment. The camera makes a smooth orbit, arc or lateral move to gradually reveal the character’s face and silhouette.

8–12s
Move into a tight cinematic portrait or upper-body shot. The character performs one subtle signature action that fits their personality, such as lifting the chin, turning the head, adjusting clothing, brushing hair aside, opening a hand, looking toward camera, or shifting posture. Keep the motion minimal and intentional. The expression should match the character’s vibe.

12–15s
End with a strong full-body hero shot that clearly presents the entire design and silhouette. Use a low-angle, eye-level or slightly dramatic framing depending on the character’s personality. The character settles into a natural final pose and holds it confidently for a clean final reveal.

VISUAL DIRECTION
Premium cinematic presentation. Match the visual medium and rendering style of @[char ref]. Emphasize clean silhouette, elegant staging, subtle secondary motion, believable hair and cloth movement, strong composition, atmospheric depth and polished lighting. The scene should feel like a high-end anime, game or film character introduction.

CAMERA
Use a clear progression from detail reveal to partial reveal to face reveal to full-body hero reveal. Camera movement should be smooth, controlled and intentional. Avoid chaotic motion.

ENVIRONMENT
Place the character in a fitting environment that supports their identity and mood. The background should enhance the character without distracting from them.
```

</details>

<sub>Source: <a href="https://x.com/aimikoda/status/2086412223061135392">https://x.com/aimikoda/status/2086412223061135392</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 14 · Multiplication Tables with Fish Pairs

<sub>タナベ | AI動画 × マーケティング &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2089141649503044017.jpg" alt="Multiplication Tables with Fish Pairs" width="100%">](https://x.com/tanabe_fragm/status/2089141649503044017)

<sub><b>▶ <a href="https://x.com/tanabe_fragm/status/2089141649503044017">Watch the clip on the creator's post on X (@タナベ | AI動画 × マーケティング)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>An orange cat guides a nine-pool grid where paired fish and beat-matched equations teach the two-times table. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,973 characters)</summary>

```text
integrated_multimodal_description: [Shot 1] Adorable rounded 3D animation for preschool children, soft studio lighting, subtle contact shadows, smooth gradients, and a calm uncluttered vertical composition on a clean off-white background with a very soft pale-blue glow behind the center. Use a restrained palette of off-white, warm orange, cream, turquoise blue, and dark gray: orange is the cat, turquoise is the fish and every correct answer, dark gray is the equation. The camera is a Static Shot for the entire film. A small smiling cat mascot bounces gently into the upper area: a big rounded head on a short chubby body, warm orange fur, a cream muzzle, cream belly and cream paw tips, two small rounded triangle ears with pale pink inner lining, round full cheeks, simple black dot eyes, tiny whiskers, and a thick rounded tail. It lands with a soft squash-and-stretch, its tail curls up once behind it, and it taps the air with one front paw, creating a spreading circular pale-blue water ripple. The ripple opens outward and reveals a three-by-three grid of nine small empty pale-blue water pools in the lower half of the frame, with a clear empty space for one large equation above them. A warm young Japanese female narrator with a bright, soft voice (S1) chants in a steady rhythmic sing-song counting cadence, one line per beat, and begins: <d>[Japanese] にのだん!</d>

[Shot 2] At 00:01.200, one large thick rounded dark-gray equation appears in the upper space and is rewritten twice in place, holding each state clearly on its own beat: first "2 × 1 = 2", then "2 × 2 = 4", then "2 × 3 = 6". On each new equation, exactly one matching pair of two plump turquoise-blue fish drops together into the next empty water pool with a small splash. The two fish of a pair are identical, side by side, both facing right and slightly offset so both are clearly countable, each with a cream belly, a triangular tail, and one round black eye. The pairs fill the top row from left to right, and the answer numeral turns turquoise as each pair lands. At the end of this shot exactly three pools in the top row are filled, each holding exactly two fish, for six fish in total; six pools remain empty. (S1) chants on the beat: <d>[Japanese] にいちがに。ににんがし。にさんがろく。</d>

[Shot 3] At 00:04.700, a soft pale-blue water ripple wipes across the frame and the same large equation continues to be rewritten in place on each beat: "2 × 4 = 8", then "2 × 5 = 10", then "2 × 6 = 12". One matching pair of two fish drops into the next empty pool on each new equation, filling the middle row from left to right, and the answer numeral turns turquoise as each pair lands. Two-digit answers stay large, correctly formed, and fully readable. The three pairs already in the top row stay exactly where they are and do not move, change, or multiply. At the end of this shot exactly six pools are filled, each holding exactly two fish, for twelve fish in total; three pools remain empty. (S1) chants on the beat: <d>[Japanese] にしがはち。にごじゅう。にろくじゅうに。</d>

[Shot 4] At 00:08.100, a soft pale-blue water ripple wipes across the frame and the large equation is rewritten in place on each beat for the last time: "2 × 7 = 14", then "2 × 8 = 16", then "2 × 9 = 18". One matching pair of two fish drops into the next empty pool on each new equation, filling the bottom row from left to right, and the answer numeral turns turquoise as each pair lands. The six pairs already placed stay exactly where they are and do not move, change, or multiply. At the end of this shot all nine pools are filled, each holding exactly two fish, for eighteen fish in total. (S1) chants on the beat: <d>[Japanese] にしちじゅうし。にはちじゅうろく。にくじゅうはち。</d>

[Shot 5] At 00:12.100, the final equation "2 × 9 = 18" stays in the upper space and its turquoise answer numeral "18" gently enlarges once and settles. Below it, the nine pairs of fish gain small friendly smiles and their tails flick once, in a quick wave from the top-left pool to the bottom-right pool, each pair flicking together as one. The same warm-orange cat mascot from [Shot 1], unchanged in every detail, bounces in at the lower edge beside the grid and points up toward it with one front paw while its tail curls once and small pale-blue sparkles rise around it. Exactly nine pools remain, each still holding exactly two fish, and no new objects enter. (S1) says: <d>[Japanese] よく できました!</d> Hold the complete grid, the equation, and the cat clearly and without further motion until the film ends exactly at 00:15.000.

Throughout the entire film, keep the camera a Static Shot, keep the off-white background clean and empty, keep the single equation large, thick, rounded, correctly shaped, and centered in the upper space, and keep the fish design identical in every shot. Every filled pool always holds exactly two fish - never one, never three - and the two fish of a pair always arrive together, land together, and stay together as one unit. The cat must look exactly the same in [Shot 1] and [Shot 5], identical in fur color, head and body shape, ears, eyes, and tail, and it never appears in [Shot 2], [Shot 3], or [Shot 4]. Only one cat is ever on screen, it stays beside or above the grid, and it never stands on, reaches into, covers, or eats any fish. Only one equation is ever visible at a time. Display only numerals and the symbols × and =. Do not generate any hiragana, katakana, kanji, Latin words, or any other written characters anywhere on screen. Fish only ever accumulate, never disappear, never leave their pool once placed, and never overlap; the number of filled pools must exactly match the multiplier of the current equation, and the total fish count must exactly match the answer numeral, reaching exactly eighteen fish in nine pools at the end. Avoid fast camera movement, sudden cuts, cluttered backgrounds, tiny typography, warped or duplicated numerals, reversed two-digit numbers, wrong counts, extra or missing fish, unpaired single fish, fish appearing before their equation, fish swimming freely around the frame, realistic or scaly fish anatomy, scary expressions, harsh colors, heavy motion blur, and loud or distracting sound effects.

overall_soundscape: A soft double water plop sounds each time a pair of fish drops into a pool. A light padded paw tap sounds when the cat touches the air, and one single soft kitten meow occurs as the cat first bounces into frame. Gentle spreading water ripples mark the two transitions, and a small confirmation chime sounds each time an answer numeral turns turquoise. Tiny shimmer sparkles occur around the cat at the end.

non_diegetic_music: A light nursery jingle at a steady moderate tempo using marimba, soft celesta, and gently plucked strings, with a clear repeating beat that the chant lands on. Begin with a single marimba figure, add one instrument at each row of the grid, and thin back out for the final line. Resolve with a clean rising three-note chime landing at 15.000 seconds.
```

</details>

<sub>Source: <a href="https://x.com/tanabe_fragm/status/2089141649503044017">https://x.com/tanabe_fragm/status/2089141649503044017</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 15 · Orange-and-Black Street Dance Commercial

<sub>タナベ | AI動画 × マーケティング &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2090306302966919515.jpg" alt="Orange-and-Black Street Dance Commercial" width="100%">](https://x.com/tanabe_fragm/status/2090306302966919515)

<sub><b>▶ <a href="https://x.com/tanabe_fragm/status/2090306302966919515">Watch the clip on the creator's post on X (@タナベ | AI動画 × マーケティング)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A street dancer performs through rapid orange-and-black geometric layouts before a giant Japanese title closes the spot. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (7,078 characters)</summary>

```text
----------------------
integrated_multimodal_description:
2D-animated, a bold graphic-design motion-graphics commercial in 16:9 with exactly 13
distinct cuts at 24fps. This film is 85% kinetic graphic design and 15% character action:
giant kinetic Japanese typography, hard-edged flat shapes, split screens, halftone, speed
lines, torn-paper reveals and shutter flashes. Palette, strictly four colors: fluorescent
orange, deep black, off-white, silver grey. The recurring character is a young anime street
dancer with a black chin-length bob and blunt bangs, sharp confident eyes, an oversized
off-white track jacket with fluorescent-orange sleeve stripes, black cargo shorts, and
chunky white sneakers with fluorescent-orange lines. Preserve her exact face, proportions,
hairstyle, outfit, materials and colors throughout; never redesign her. Every graphic
element moves fast and snaps hard on the beat.

[Shot 1] On a deep black field, a massive off-white circle slams into frame left of center,
then two fluorescent-orange bars wipe across the upper and lower thirds, then the Japanese
kanji "烈" builds itself stroke by stroke in off-white at the center until it is complete.
The camera shakes slightly with small amplitude at fast speed on each impact.

[Shot 2] At 00:01.000, the camera cuts to an off-white field where four black squares
rotate into the center one at a time. The largest square opens as a porthole revealing an
extreme close-up of the dancer's ice-sharp eye glancing up, then a red-and-cyan split flash
tears across the edges and the squares shatter into flat shards. The camera pushes in with
small amplitude at fast speed.

[Shot 3] At 00:02.000, the camera cuts to an off-white field filled by an enormous black
kanji "烈". The dancer sprints in from frame left, power-slides along the baseline of the
typography, and fluorescent-orange ink splatter trails behind her as speed lines streak
past. The camera trucks left with large amplitude at fast speed. The kanji stays fully
readable before she crosses in front of it.

[Shot 4] At 00:03.100, the camera cuts to a vertical triptych of fluorescent-orange, deep
black and off-white panels. Her flat silhouette appears in each panel in stroboscopic
freeze, one after another — takeoff, mid-air tuck, landing — while giant vertical silver
text "全速" scrolls upward behind the panels. Static shot.

[Shot 5] At 00:04.000, the camera cuts to a black field where a giant tilted ring of
fluorescent-orange Japanese characters reading "止マルナ" rotates. The dancer leaps through
the center of the ring, spins once in mid-air, and the characters break off and scatter
outward as flat shards. The camera arcs with large amplitude at fast speed, then snap-zooms
onto her confident face.

[Shot 6] At 00:05.100, the camera cuts to a clean off-white editorial card holding a huge
black kanji "跳" with one orange diagonal slash. She vaults over the word itself, plants her
palm on its left radical, the character compresses like a spring under her hand, then
rebounds as her legs whip across the frame. Static shot.

[Shot 7] At 00:06.000, the camera cuts to a full fluorescent-orange field crossed by one
thick black diagonal stripe. She back-flips along the stripe in three stroboscopic ghost
frames tinted black, off-white and silver grey, while a large outlined kanji "回" rotates
180 degrees in sync with her rotation. The camera rolls clockwise with small amplitude at
fast speed.

[Shot 8] At 00:07.000, the camera cuts to an off-white field with a hard black band. Four
bold black kanji slam in one at a time at different scales and angles — "速", then "鋭",
then "静", then "烈" — each landing with a white shutter flash and an orange impact mark,
while she slides on her knees across the foreground, jacket flaring. The camera shakes
slightly with small amplitude at fast speed.

[Shot 9] At 00:08.000, the camera cuts to a black frame where a white wireframe grid tilts
away in 3D. She runs up the grid like a wall, kicks off it, and hangs frozen in mid-air as
a fluorescent-orange circle stamps around her pose like a target lock with silver UI
brackets and tick marks. The camera tilts up with small amplitude at slow speed.

[Shot 10] At 00:09.000, the freeze releases and the camera cuts to layered flat-color panes
stacked toward the lens. She dives straight at the camera, the panes tear open one at a
time like thick paper, and each tear reveals a larger portion of the black kanji "烈"
behind, before her sneaker wipes across the foreground. The camera pulls out with large
amplitude at fast speed.

[Shot 11] At 00:10.100, the camera cuts to a rapid-fire montage of four full-screen graphic
posters of her in different action poses — mid-flip, sliding, landing, hands in pockets —
snapping past with hard cuts, each with an oversized silver number 01 to 04, a black
barcode strip and thick diagonal slashes. Static shot.

[Shot 12] At 00:11.100, the camera cuts to a clean off-white cyclorama for the hero moment.
She lands a final backflip dead center in slow motion, straightens with both hands in her
pockets, and a shockwave of concentric fluorescent-orange rings blasts outward from her feet
carrying shattered fragments of the kanji "烈" with it, then the frame overexposes toward
white. The camera pushes in with small amplitude at slow speed.

[Shot 13] At 00:13.000, the camera cuts to the final identity card on a pale off-white
field. An enormous black kanji "烈" dominates the frame with translucent orange rings and
thin technical arcs behind it, the silver-grey word "RETSU" sits directly beneath the kanji,
and she stands relaxed at the lower center overlapping the bottom of the strokes with her
jacket rippling. One thin orange pulse sweeps horizontally through the typography and holds
cleanly until exactly 15.000 seconds. Static shot.

Editing: extremely aggressive rhythm — hard cuts on every beat, graphic matches, whip pans,
snap zooms, stroboscopic freezes, foreground wipes, split flashes and impact shakes. Every
cut must feel compositionally different. All Japanese typography is always fully readable
before the character overlaps it. No weapons, no combat, no fire, no explosions; all energy
comes from motion design, ink, torn paper, wind and her street-dance athleticism. No
photorealism, no 3D rendering, no gradients, no browser interface, no player controls, no
subtitles, no captions, and no text other than the Japanese characters named above.
Exactly 13 cuts.

overall_soundscape:
Sneaker impacts, knee slides and landings hit hard against a clean room tone. Ink splatters
burst, thick paper tears open, and flat panels shatter like glass. Sharp whooshes carry the
color wipes and typography slams, with small shutter clicks on each flash. No dialogue.

non_diegetic_music:
An original 15-second drum-heavy breakbeat with a deep sub bass, hard snare hits, risers and
glitch fills locked to every cut. Begin with a single impact, build tightly through the
middle, peak at the landing at 00:11.100, and end with a cold electronic logo sting that
resolves at 15.000 seconds.
```

</details>

<sub>Source: <a href="https://x.com/tanabe_fragm/status/2090306302966919515">https://x.com/tanabe_fragm/status/2090306302966919515</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 16 · A Green Power Ring Constructs a Sports Car

<sub>FoldingEnd A.I. &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1280×736 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2092003946407870917.jpg" alt="A Green Power Ring Constructs a Sports Car" width="100%">](https://x.com/EndFolding79421/status/2092003946407870917)

<sub><b>▶ <a href="https://x.com/EndFolding79421/status/2092003946407870917">Watch the clip on the creator's post on X (@FoldingEnd A.I.)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A man projects green energy from a ring on his right hand, assembling a sports car layer by layer before it accelerates away across the landscape. Native-video output: 15s · 1280×736. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (7,280 characters)</summary>

```text
integrated_multimodal_description:

<Image 1> is the CHARACTER APPEARANCE REFERENCE.
<Image 0> is the BACKGROUND LOCATION REFERENCE.

Use <Image 1> to preserve the man's exact facial identity, age, dark hair with gray temples, rugged stubble, body proportions, green-and-black tactical suit, illuminated chest emblem, and power-ring design.

Use <Image 0> to preserve the open landscape, terrain, lighting, atmosphere, and general environmental appearance.

CRITICAL RIGHT-HAND CONTINUITY:
The power ring is worn ONLY on the man's anatomical RIGHT HAND throughout the entire video.
NEVER place the ring on his left hand.
Do NOT mirror or swap hands when the camera angle changes.
His LEFT HAND remains completely ringless throughout the entire sequence.
Every green energy projection originates directly from the ring on his RIGHT HAND.

Photorealistic live-action cinematic realism.

Environment: vast isolated American desert-like prairie, dry golden grass, dusty earth, scattered low scrub, distant low hills, huge open sky. Warm late-afternoon sunlight. No buildings, existing vehicles, roads, or other people visible.

The ONLY vehicle appearing in the scene is the futuristic sports-car construct created by the man's ring.

[00:00–00:02.0]

Wide cinematic tracking shot.

The man from <Image 1> walks casually through the open landscape.

His arms swing naturally as he walks.

After several steps he slows and stops.

He looks across the empty landscape in front of him as though deciding how he wants to travel.

Camera gently moves from the wider walking shot into a medium three-quarter view.

[00:02.0–00:03.0]

Medium shot.

He turns slightly toward an open patch of ground beside him.

He raises his anatomical RIGHT HAND and deliberately points the power ring toward the empty space.

His LEFT hand remains completely ringless.

The ring begins glowing with concentrated emerald-green energy.

[00:03.0–00:06.5]

A narrow, clearly defined GREEN ENERGY BEAM shoots directly from the ring on his RIGHT HAND into the empty space beside him.

CRITICAL:
From this moment through the FINAL FRAME, the green energy beam remains visibly and continuously connected between his RIGHT-HAND ring and the construct sports car.

The beam NEVER disconnects.
The beam NEVER disappears.
The beam NEVER switches hands.
The beam NEVER originates from his left hand.

Camera shifts to a wider three-quarter angle so both the man and the forming vehicle remain clearly visible.

The beam begins DRAWING A FUTURISTIC SPORTS CAR INTO EXISTENCE like a three-dimensional emerald sketch.

The construction is clearly progressive and physically understandable.

Bright emerald lines rapidly trace:

wheels → lower chassis → aerodynamic nose → side profile → rear body → windshield and cockpit → roofline → remaining body panels.

The glowing wireframe establishes the complete shape of a low, sleek, aggressive futuristic sports car.

As each section is drawn, the wireframe rapidly fills and solidifies into dense, physical-looking emerald-green construct energy.

The vehicle is NOT an ordinary green-painted automobile.

It is unmistakably a POWER-RING ENERGY CONSTRUCT: solid and physically usable, but composed entirely of luminous translucent emerald-green energy with subtle internal glowing structure.

Four clearly defined wheels.
Believable tires made from solid green construct energy.
Low aerodynamic body.
Futuristic cockpit.
Sleek windshield.
Aggressive but elegant proportions.

The DRIVER-SIDE DOOR AREA deliberately remains unfinished and open while the rest of the vehicle completes.

[00:06.5–00:08.0]

The sports car finishes forming except for the open driver's entrance.

The man lowers his right arm slightly while STILL maintaining the visible energy connection between his RIGHT-HAND ring and the construct car.

He looks over the completed futuristic car.

A confident, slightly cocky smirk appears on his face.

Hold just long enough to clearly read his expression.

No dialogue.

[00:08.0–00:10.5]

Camera moves into a dynamic medium-wide side angle.

The man walks directly to the open driver's side.

The continuous green energy beam remains connected from his RIGHT-HAND ring to the car throughout his movement.

He naturally steps into the driver's seat.

Do NOT make him teleport into the vehicle.

Do NOT have him pass through the bodywork.

He physically enters through the intentionally unfinished driver's-side opening and sits behind the wheel.

Once he is fully seated, glowing construct lines rapidly draw and solidify the final driver's-side door around him, completing the sports car.

The green beam STILL remains connected from the ring on his anatomical RIGHT HAND to the car.

[00:10.5–00:12.0]

Low cinematic three-quarter shot of the completed vehicle.

The futuristic emerald construct sports car powers up.

Internal green energy pulses subtly through its body.

The wheels begin turning.

Dust shifts beneath the tires.

Through the cockpit, the man gives another brief confident, cocky smirk.

His RIGHT HAND remains the hand sustaining the construct.

The continuous green energy connection remains active.

[00:12.0–00:15.0]

The construct sports car launches forward with powerful acceleration.

Real dust and loose dirt kick backward from beneath the glowing green construct wheels.

Camera briefly tracks alongside at a low angle as the vehicle rapidly gains speed.

A beautiful EMERALD-GREEN ENERGY TRAIL streams behind the construct car as it accelerates across the open landscape.

The car sweeps past the camera and drives COMPLETELY OUT OF FRAME.

Do NOT stop the car before it exits.

Do NOT dissolve the vehicle.

Do NOT transform it into another object.

The construct remains a complete futuristic sports car as it leaves the shot.

CRITICAL FINAL CONTINUITY:
The sports car remains actively sustained by the man's RIGHT-HAND power ring while he drives.

The visible green energy connection remains continuously linked to his RIGHT-hand ring and integrated into the construct car's glowing energy structure through the FINAL FRAME.

The ring NEVER appears on his left hand.

No dialogue.
No attack.
No explosion.
No additional constructs.
No additional characters.
No existing real-world vehicles.

overall_soundscape:

Natural open-land ambience with gentle dry wind moving through grass and subtle footsteps on dusty earth at the beginning.

When the RIGHT-HAND ring activates, introduce a clean concentrated emerald-energy hum.

The three-dimensional drawing process produces precise crystalline energy sounds as glowing lines trace the vehicle into existence, followed by deeper resonant energy tones as the wireframe solidifies into the physical construct.

Once completed, the sports car produces a smooth futuristic energy-powered motor sound rather than a conventional gasoline engine.

Subtle rising energy whine as the vehicle powers up.

Construct tires interact physically with the terrain: dirt crunch, tire movement, and a strong burst of dust and gravel as the car accelerates.

The energy motor rises rapidly in pitch as the car drives away, accompanied by a subtle sustained energy sound from the emerald trail.

Natural wind and landscape ambience remain underneath.

No dialogue.

non_diegetic_music:

None.
```

</details>

<sub>Source: <a href="https://x.com/EndFolding79421/status/2092003946407870917">https://x.com/EndFolding79421/status/2092003946407870917</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 17 · A Last Handhold on a Blizzard Cliff

<sub>Loriel.AI &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 3840×2160 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2096980289184805308.jpg" alt="A Last Handhold on a Blizzard Cliff" width="100%">](https://x.com/ou_zhen599/status/2096980289184805308)

<sub><b>▶ <a href="https://x.com/ou_zhen599/status/2096980289184805308">Watch the clip on the creator's post on X (@Loriel.AI)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A climber slips on a snowy cliff, drops until her rope catches, and finally secures the ledge below a buried mountain entrance. Native-video output: 15s · 3840×2160. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (4,542 characters)</summary>

```text
integrated_multimodal_description:
[Shot 1] Photorealistic cinematic survival action, 15 seconds. Lara climbs a steep cliff in a blizzard toward a snow-buried ancient entrance. Lock her identity, hair, clothing, injuries, and equipment. Keep one climbing-tool type, secured when released; maintain the same rope-to-harness connection and upper anchor throughout.

Extreme close tracking begins on her left hand gripping a snowy crack, then tilts rapidly along her arm to her tense profile. Her right hand pulls the rope, knee braces against rock, and she pushes upward half a step. Eyes target the next hold; jaw tightens during effort. Lara (S1), quietly breathless, says, <d>[English] Almost there…</d> Wind drives snow sideways; loosened powder falls and the rope trembles.

[Shot 2] At 00:02.000, cut over her shoulder into a slightly wide subjective view. Advance with her head lift, then tilt upward toward the ancient doorway emerging through snow. She judges the route for half a beat and points her climbing tool toward an upper-right hold. No frontal insert or dialogue. A ruined pinnacle appears briefly, valley clouds churn below, and wind sharpens.

[Shot 3] At 00:04.000, cut to a front-side medium close-up, tracking her lateral traverse. Her right foot loads a thin ice edge and slips. Only then do her eyes widen and breath catch; she checks her foot, tightens her jaw, and searches for another grip. Lara (S1) produces <d>[English] Tsk.</d> as one clipped tongue click, not spoken letters. Snow and stone fragments fall into the ravine.

[Shot 4] At 00:06.000, track her sudden drop, then arrest sharply as the rope loads through her harness. She swings outward beneath the anchor, left hand gripping rope, right hand reaching for projecting rock; the tool remains secured. Her breath stops, then her eyes lock onto the target. Lara (S1), through clenched teeth, says, <d>[English] Don’t fall now.</d> Finish on one short exhalation, slightly stressing "now." Rope vibration, crumbling rock, and falling snow follow the load.

[Shot 5] At 00:08.000, cut to a diving angle following her swing toward the new hold, then move rapidly back toward her face. She catches the projection and uses her core and momentum to return against the cliff. Her chest strikes snowy rock; eyes briefly close and breath is knocked out. She immediately looks upward and resumes short breaths without crying out. Impact throws snow outward; wind whips her hair and briefly reveals the ruins.

[Shot 6] At 00:10.000, frame her gripping hand, push toward her eyes, then tilt slightly toward the cliff lip. Two quick climbing movements bring her hand onto a projecting stone edge. As she pulls, it breaks. Alarm follows the fracture: eyes widen, inhalation catches, and her gaze tracks the failing hold. Lara (S1) says, <d>[English] Wait!</d> sharply, once. Rock tumbles, snow dust strikes her face, and wind curls over the lip.

[Shot 7] At 00:12.000, follow a half-torso drop, then stop on her hand catching the solid cliff edge. She brings the other hand up and stabilizes her weight below the lip; the rope remains connected and physically loaded. Only after securing both hands does she exhale. Slowly tilt upward with her gaze to the enormous snow-buried doorway. Her eyelids and jaw ease slightly, retaining exhaustion and vigilance. Lara (S1), low and breathless, says, <d>[English] Found you.</d> A gust clears the entrance, revealing faint cold light through its seam. Leave the doorway visible after the line. End at 15.00 seconds with Lara still braced at the edge, without standing, walking, or opening the door.

Preserve all seven intervals, camera movements, and action causality. Lara is the only speaker; each exact utterance finishes within its assigned interval. Keep one voice, natural lip synchronization, and physically motivated breathing. No extra dialogue, screams, narration, reaction inserts, or performance pauses. Fear follows danger; relief follows a secure grip. Maintain realistic gripping, rope tension, swing direction, impact, and falling debris. No identity drift, distorted anatomy, extra limbs, intersecting hands or ropes, drifting holds, disappearing equipment, unsupported hovering, exaggerated expressions, subtitles, text, or watermarks.

overall_soundscape:
Continuous blizzard wind, clothing friction, exertion breaths, rope loading, cracking rock, and falling debris. Synchronize the rope arrest and muffled chest impact precisely; keep dialogue intelligible beneath the storm.

non_diegetic_music:
N/A
```

</details>

<sub>Source: <a href="https://x.com/ou_zhen599/status/2096980289184805308">https://x.com/ou_zhen599/status/2096980289184805308</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 18 · A Teasing Conversation by the Starship Window

<sub>Loriel.AI &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 3840×2160 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2096921323624972600.jpg" alt="A Teasing Conversation by the Starship Window" width="100%">](https://x.com/ou_zhen599/status/2096921323624972600)

<sub><b>▶ <a href="https://x.com/ou_zhen599/status/2096921323624972600">Watch the clip on the creator's post on X (@Loriel.AI)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Two women and a cat share a warm spacecraft cabin as the camera moves between a mug, subtle expressions, and small gestures during a teasing exchange. Native-video output: 15s · 3840×2160. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (4,540 characters)</summary>

```text
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] Live-action, cinematic, ultra-realistic. The video starts exactly from <Picture 1>, preserving the warm spacecraft cabin, sofa area, porthole windows, pizza box, old astronaut helmet, candlelight, exposed wall wiring, and the full spatial continuity. The left girl is always A, the right girl is always B. Their identity, face, hairstyle, outfit, voice, and left-right relationship remain unchanged. A stays wrapped in a bathrobe and keeps holding the hot mug throughout. B stays side-lying close to her with both feet lifted behind her. The camera glides low across the pizza box, old helmet, candles, and wall wiring, then settles on both girls and the cat together. A looks down at the steam above the mug, thoughtful and avoiding eye contact; her eyelids are lowered, lips closed, shoulders slightly tucked, breathing shallow and even. B watches A with a restrained smile and softly swaying feet. Stars drift slowly outside, with a faint cool-blue reflection on the planetary curve. Thin steam rises from the mug; candle flames flicker gently without pulsing. [Shot 2] At 00:02.000, the camera gently pushes toward B while keeping her swaying calves and feet visible. B tilts her head slightly, hides a smile, then lets it show as she speaks and keeps watching A afterward. B, in a light teasing voice (S1), says, <d>[English] Daydreaming again? Who about?</d> “again” lifts slightly; there is a short pause before “Who about?”, which lands softer and more curious than pressing. [Shot 3] At 00:04.000, the shot cuts to A in close-up and sinks slightly with her movement. A freezes for a beat, blinks once, raises the mug to shield herself a little, lowers her head, and takes only a small sip. She swallows before speaking, keeping her gaze near the cup; the corner of her mouth almost lifts, then settles. A, in a soft inward voice (S2), says, <d>[English] No one… Don’t guess.</d> “No one” is short and quiet, followed by a brief hesitation; “Don’t guess” is soft, not angry. Drinking and speaking do not overlap. [Shot 4] At 00:06.000, the cat rises between them and the camera follows it naturally back into a medium close two-shot. A lightly strokes the cat’s ear to avoid B’s gaze. B inches closer, her feet still swaying, glances at A’s hands around the mug, then back to A’s face. Her smile deepens gently without exaggeration. B (S1), lowering her voice with playful warmth, says, <d>[English] Why so tight? You’re making the cup blush.</d> The first question is light and quick; “blush” lands with a smile. A begins to lose control of her smile by the end. [Shot 5] At 00:09.000, the camera returns to a slightly front-facing close two-shot favoring A. A lets out a small breathy laugh, shoulders relaxing. Keeping the mug upright in one hand, she lightly taps the back of B’s wrist with the other hand, then gently nudges B with one knee. Her eyes flick briefly toward B’s swinging feet, then toward B’s wrist, still not fully locking eye contact. B’s smile opens a little but she does not overreact. A (S2), smiling now, says, <d>[English] Keep your feet still. You’re flustering me even more.</d> The first sentence is playfully corrective; “even more” softens at the end. [Shot 6] At 00:12.000, the camera follows B in a tiny forward move. B shows a brief victorious smile, then softens; her feet gradually slow instead of stopping abruptly. She strokes the cat without pulling away. A finally raises her eyes and truly looks at her, keeping the faint smile from before and no longer looking away. B (S1) says, <d>[English] Then I’ll stop swinging my feet—and sway you.</d> The first half is light and playful; “sway you” becomes softer and more intimate, expressed only through voice and eyes, with no added pushing or body movement. After the line, the camera slowly pulls back to hold both girls, the cat between them, and the full warm cabin while they maintain eye contact. Dialogue order stays strictly B → A → B → A → B. No extra lines, no swapped roles, no axis crossing, no left-right swap, no cup hand change, no kiss, no hug, no subtitles, no text, no watermark.

overall_soundscape: Low steady spacecraft room tone throughout, with soft fabric movement, subtle sofa friction, faint mug handling, quiet breathing, light cat contact sounds, and gentle foot-sway rustle. Ambient sound stays restrained and never covers the dialogue.

non_diegetic_music: N/A
```

</details>

<sub>Source: <a href="https://x.com/ou_zhen599/status/2096921323624972600">https://x.com/ou_zhen599/status/2096921323624972600</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 19 · The Boy Who Chases a Midnight Dragon

<sub>ManuAGI 🤖 - ( ManuIn ) &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2086321605073105162.jpg" alt="The Boy Who Chases a Midnight Dragon" width="100%">](https://x.com/ManuAGI01/status/2086321605073105162)

<sub><b>▶ <a href="https://x.com/ManuAGI01/status/2086321605073105162">Watch the clip on the creator's post on X (@ManuAGI 🤖 - ( ManuIn ))</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Kael watches the silver moon crack, sees a midnight dragon carry away a shard, and pursues it toward a forbidden valley. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (24,378 characters)</summary>

```text
[REFERENCE CONTROL]

Use the uploaded PART 1 storyboard image for “THE BOY WHO RETURNED THE MOON” as the PRIMARY visual, character, environment, cinematography, lighting, scale, prop, performance, and narrative reference.

Generate a FINISHED cinematic animated sequence from the storyboard.

DO NOT reproduce the storyboard sheet itself.

The final video must NOT contain:
- storyboard panel borders
- panel numbers
- timestamps
- handwritten captions
- production notes
- character-reference sketches
- prop-reference drawings
- title/header
- page number
- off-white storyboard-paper texture
- camera-note boxes
- color swatches

The uploaded storyboard locks:

1. Kael’s exact face and body design
2. Kael’s swept-back black hairstyle
3. Kael’s dark tunic and trousers
4. Nyx’s exact black midnight-dragon design
5. Nyx’s long serpentine body
6. Nyx’s giant amber-orange eyes
7. Nyx’s luminous toothy grin
8. the enormous silver full moon
9. Noctara’s gothic castle architecture
10. orange-lit castle windows
11. reflective moonlit lake
12. dark lakeside rock and forest geography
13. exact glowing silver moon-fragment design
14. deep midnight-blue visual palette
15. Part 1 story progression
16. final Valley of Bones cliffhanger

The finished video must feel like these storyboard paintings have come alive as a premium cinematic 2D animated short.

IMPORTANT:

The storyboard contains 15 one-second panels.

DO NOT create fifteen frantic one-second cuts.

Consolidate them into approximately 8 cinematic shots with clear:

setup
→ disturbance
→ discovery
→ dragon reveal
→ misunderstanding
→ chase
→ forbidden-land cliffhanger.

--------------------------------------------------

[VIDEO GOAL]

Duration:
EXACTLY 15 seconds

Story range:
0:00–0:15 of the 1-minute film

Aspect ratio:
16:9 landscape

Frame-rate feeling:
cinematic 24 fps

Visual style:
premium hand-painted 2D dark-fantasy animation

Genre:
moonlit fantasy mystery / adventure

Audience:
family-friendly

Dialogue:
native synchronized English

Audio:
native dialogue + cinematic environment + magical SFX + original music

EMOTIONAL ARC:

peaceful moonlit wonder
→ subtle unease
→ impossible celestial event
→ shock
→ mysterious creature reveal
→ false villain assumption
→ determination
→ chase
→ ominous curiosity

Core Part 1 question:

“Why did the dragon take the moon fragment?”

--------------------------------------------------

[PART 1 STORY LIMIT]

PART 1 ONLY.

START:

Kael sits peacefully beside the moonlit lake watching the enormous full moon above Noctara.

END:

Kael reaches the ridge overlooking the Valley of Bones after Nyx disappears inside with the moon fragment.

The cracked moon is visibly dimmer above him.

Kael decides to follow.

DO NOT show:
- Zara
- skeleton guardians
- Bonekeeper reveal
- Nyx being innocent
- “He’s trying to return it”
- Moon Shrine
- Bone Bridge
- Nyx losing the shard
- Kael catching the shard
- shrine activation
- restored moon
- moon-fireflies
- final friendship scene

Those belong to later parts.

--------------------------------------------------

[CHARACTER IDENTITY LOCK — KAEL]

Match the uploaded storyboard EXACTLY.

KAEL:

Slim teenage moon-watcher.

Appearance:
- youthful stylized angular face
- cool pale-to-medium skin tone
- large expressive dark eyes
- thick black eyebrows
- swept-back tousled black hair
- pointed windswept hair silhouette
- lean narrow shoulders
- long thin limbs
- small athletic teenage build

Clothing:
- simple charcoal / black fantasy tunic
- slightly loose short sleeves
- dark fitted trousers
- dark practical boots
- subtle dark belt
- no armor
- no cape
- no weapons

Personality:
- quiet
- thoughtful
- curious
- emotionally intense when surprised
- brave
- impulsive
- deeply fascinated by the moon

PART 1 PERFORMANCE:

0–3 sec:
calm, reflective, mesmerized

3–5 sec:
uneasy → shocked

5–7 sec:
disbelief

7–9 sec:
fear mixed with anger

9–12 sec:
decisive pursuit

12–15 sec:
cautious but determined

CRITICAL:

Maintain exact:
- face
- hair
- clothing
- age
- proportions
- eye design
- silhouette

Do not make Kael older, more muscular, armored, or heroic-looking.

He is an ordinary boy who makes a brave decision.

--------------------------------------------------

[CHARACTER IDENTITY LOCK — NYX]

Match the uploaded storyboard EXACTLY.

NYX — THE MIDNIGHT DRAGON

Appearance:
- huge black dragon
- elongated serpentine body
- long narrow flexible neck
- layered feather-like black scales
- blue-black moonlit edge highlights
- dramatic backward-pointing head spines
- pointed ear-like horns
- enormous glowing amber-orange eyes
- vertical black slit pupils
- large luminous white toothy grin
- narrow expressive dragon snout
- long curved tail
- large dark wings matching his silhouette where visible

Personality in Part 1:
UNKNOWN to Kael.

Visually Nyx should seem:
- mysterious
- powerful
- intimidating
- slightly mischievous
- unreadable

But do NOT portray true cruelty.

Subtle clues may suggest he is protecting rather than stealing the fragment:
- careful grip on shard
- controlled flight
- no attacks
- no fire
- no aggression toward Kael

NYX MUST NOT SPEAK IN PART 1.

His intimidating appearance creates the misunderstanding.

--------------------------------------------------

[MOON FRAGMENT IDENTITY LOCK]

Match storyboard exactly.

ONE fragment only.

Appearance:
- irregular crescent / crystalline shard
- brilliant white-silver center
- translucent icy-blue edges
- faint silver particles
- small radiant aura
- roughly large enough for Nyx to carry carefully in his jaws

Timeline:

full moon cracks
→ fragment separates
→ begins falling
→ Nyx intercepts
→ Nyx carries same shard through chase

Do NOT:
- duplicate fragment
- change shape between shots
- let Nyx swallow it
- turn it gold
- create multiple moon pieces

--------------------------------------------------

[MOON IDENTITY / DAMAGE CONTINUITY]

Opening:
enormous perfect silver-blue full moon.

After crack:
one obvious glowing fracture.

After fragment breaks free:
missing wedge / damaged section remains visible.

During chase:
moon becomes subtly dimmer.

Final shot:
moon is still large and recognizable, but clearly:
- cracked
- missing fragment
- weaker in brightness

Do NOT restore it in Part 1.

--------------------------------------------------

[ENVIRONMENT LOCK — NOCTARA]

Maintain exact visual world from the storyboard.

NOCTARA:

A huge fantasy kingdom surrounding a moonlit lake.

Environment:
- towering gothic fantasy castles
- tall narrow spires
- ornate towers
- warm orange glowing windows
- dark blue stone architecture
- dense shadowy trees
- steep cliffs
- reflective lake
- rocky lakeshore
- narrow forest paths
- mountain silhouettes
- clear star-filled night sky
- enormous silver moon

Visual contrast:

MOON:
cool silver-blue.

CASTLES:
warm amber-orange.

FOREST / WATER:
deep midnight blue.

Atmosphere:
beautiful,
mysterious,
grand,
storybook-dark,
never horror.

--------------------------------------------------

[VALLEY OF BONES — PART 1 REVEAL ONLY]

Only reveal its exterior / entrance.

Design:
- deep forbidden canyon
- tall jagged black-blue stone spires
- pale mist
- huge ancient fossil-like rib structures
- distant mountain walls
- twisted trees
- barren rocky path
- very subtle ivory bone-like shapes

Do NOT show:
- active skeleton guardians
- Zara
- full bone structures in close disturbing detail
- gore
- corpses

The valley should feel ancient and mysterious, not horrific.

--------------------------------------------------

[WORLD / PHYSICS LOGIC]

Part 1 cause-and-effect must be crystal clear:

Kael watches moon
→ moon cracks

moon cracks
→ fragment breaks free

fragment falls
→ Nyx intercepts

Nyx catches fragment
→ Kael assumes theft

Nyx turns toward mountains
→ Kael decides to chase

Nyx enters forbidden valley
→ Kael must choose whether to follow

No unexplained teleportation.

--------------------------------------------------

integrated_multimodal_description:

[SHOT 1] — 0.00s–2.20s
NOCTARA BENEATH A PERFECT MOON

Open on a majestic ultra-wide establishing shot matching storyboard Panel 1.

An enormous silver full moon dominates the sky.

Below:

Noctara’s tall gothic towers rise on both sides of a perfectly still lake.

Warm amber-orange windows glow through the dark blue architecture.

The moon reflects in long silver ripples across the water.

Camera slowly glides toward a dark lakeside rock.

Reveal tiny KAEL sitting alone.

Kael sits with knees raised, arms resting casually, staring at the moon.

Very subtle breeze moves his hair and tunic.

Camera:
huge kingdom wide
→ slow dolly toward Kael
→ settle behind him with the full moon framed ahead.

No dialogue initially.

Sound:
- calm lake water
- soft night breeze
- distant forest insects
- very faint city bells
- distant night birds
- quiet cloth movement

Music:
soft piano,
airy flute,
very light strings,
subtle magical glass tones.

The feeling should be beautiful and peaceful.

--------------------------------------------------

[SHOT 2] — 2.20s–3.50s
KAEL WATCHES THE MOON

Move into an intimate side-profile / three-quarter close-up matching storyboard Panels 2–3.

Cool moonlight outlines Kael’s face.

Warm orange castle lights blur softly in the background.

His eyes track the moon.

He seems comfortable here, as if he does this every night.

Kael quietly says:

<d>[English] Still there.</d>

Tiny smile.

Then the smile weakens.

Something feels slightly unusual.

Kael narrows his eyes.

Dialogue:

<d>[English] ...Right?</d>

Camera:
medium profile
→ gentle push toward his eyes
→ rack focus from Kael to moon.

Sound:
breeze becomes slightly quieter.

Music:
remove a few warm notes,
introduce one subtle unresolved tone.

--------------------------------------------------

[SHOT 3] — 3.50s–5.20s
THE MOON CRACKS

Cut to the giant moon.

For one silent fraction of a second:

perfect.

Then—

A brilliant silver fracture appears.

CRAAACK.

Not an explosion.

A glowing line spreads across part of the moon’s surface.

Kael rises quickly in the foreground.

His face goes from confusion to disbelief.

A chunk of silver moonlight begins separating.

Dialogue:

Kael:
<d>[English] What...?</d>

The moon fragment breaks free.

It begins falling through the night sky, trailing beautiful silver particles.

Kael:
<d>[English] No!</d>

Camera:
moon close-up
→ crack spreading
→ fragment separation
→ tilt downward following falling shard
→ Kael reaction.

Sound:
- deep crystalline celestial crack
- distant harmonic resonance
- silver sparkling trail
- sudden gust

Music:
sharp orchestral/glass accent,
then urgent low strings begin.

No fiery explosion.

--------------------------------------------------

[SHOT 4] — 5.20s–7.20s
SOMETHING REACHES IT FIRST

Kael watches the shard fall.

Suddenly a huge BLACK silhouette streaks across frame.

The camera briefly struggles to follow its speed.

Kael turns sharply.

The dark creature curves upward.

Reveal NYX.

His long black serpentine body arcs across the giant moon.

His amber eyes glow intensely.

Nyx reaches the fragment just before it can fall farther.

He catches it CAREFULLY between his jaws.

Silver light illuminates his black scales from below.

Camera:
Kael POV toward falling shard
→ black silhouette enters
→ dynamic pan
→ wide Nyx arc against moon
→ close-up catch.

No bite/crunch.

The fragment remains fully intact.

Sound:
- strong but controlled wing rush
- scale / feather movement
- magical shard shimmer
- low dragon breath
- no roar

Kael, stunned:
<d>[English] A dragon...?</d>

Music:
mysterious low strings + brass swell,
not villain-horror music.

--------------------------------------------------

[SHOT 5] — 7.20s–8.80s
THE MIDNIGHT DRAGON

Close cinematic reveal matching storyboard Panels 7–8.

Nyx turns his long head.

For a brief moment he looks toward Kael.

Frame:
huge amber eyes,
black feathered scales,
wild head spines,
luminous exaggerated teeth,
silver fragment glowing between his jaws.

The visual should make him look like a villain from KAEL’S perspective.

Nyx’s enormous amber eye subtly narrows.

But he does NOT threaten Kael.

He simply turns away.

Kael’s expression changes:

shock
→ fear
→ certainty.

Dialogue:

Kael:
<d>[English] He took it...</d>

Nyx coils his body through the air and begins turning toward the mountains.

--------------------------------------------------

[SHOT 6] — 8.80s–10.40s
“HE STOLE THE MOON!”

Reaction close-up on Kael matching Panel 9.

Kael points toward Nyx.

His fear transforms into angry determination.

Dialogue:

Kael:
<d>[English] HE STOLE THE MOON!</d>

Nyx accelerates toward the dark mountain valley.

Wide composition:

Nyx flying across the skyline,
fragment glowing from his jaws,
Noctara towers beneath him,
cracked moon above.

Kael immediately jumps down from the rock.

He begins running.

Camera:
Kael close reaction
→ turn with his pointing arm
→ follow Nyx
→ snap back to Kael launching into pursuit.

Sound:
- Kael footsteps beginning
- night wind intensifying
- Nyx wing movement
- castle ambience fading behind

Music:
adventure rhythm begins,
strings + low percussion + light brass.

--------------------------------------------------

[SHOT 7] — 10.40s–12.80s
THE CHASE BENEATH A BROKEN MOON

Create a fluid cinematic chase montage rather than several separate cuts.

Kael runs along the lakeside path.

His dark tunic and hair move with his sprint.

Above and ahead:

Nyx races between castle towers carrying the fragment.

Show:

Kael running beside moonlit water
→ Nyx passing beyond gothic spires
→ Kael climbing a dark rocky path
→ castle lights progressively farther behind
→ trees becoming denser
→ moon still cracked overhead.

Kael breathes hard.

Dialogue:

Kael:
<d>[English] Stop!</d>

Nyx does not respond.

Kael:
<d>[English] Give it back!</d>

Nyx turns once in flight, briefly glancing toward Kael.

He does not attack.

He continues toward the mountains.

Camera:
side tracking with Kael
→ wide sky parallax with Nyx
→ forward-running camera
→ increasingly darker forest framing.

Sound:
- running footsteps
- branches
- gravel
- breath
- wing beats
- silver fragment hum

--------------------------------------------------

[SHOT 8] — 12.80s–15.00s
THE VALLEY OF BONES — CLIFFHANGER

Kael exits the darker forest path onto a high rocky ridge.

He stops.

Breathing heavily.

Camera slowly moves around him.

Reveal the enormous forbidden valley below.

Use the visual language of storyboard Panels 13–15:

- towering jagged stone spires
- deep canyon
- pale blue mist
- enormous ancient rib-like fossil arches
- narrow winding path
- dark mountain walls
- very distant cold landscape

Nyx becomes a small silhouette flying deeper into the valley.

The glowing moon fragment remains clearly visible in his jaws as a silver point of light.

Kael watches him disappear.

Then he slowly looks upward.

The moon is visibly dimmer now.

Cracked.

Missing its fragment.

Kael looks back into the forbidden valley.

A quiet fear crosses his face.

Then determination.

Dialogue:

Kael, quietly:
<d>[English] You’re not getting away.</d>

Beat.

He takes one step down the forbidden path.

Kael:
<d>[English] I’m getting it back.</d>

Camera:
behind Kael
→ giant valley reveal
→ Nyx disappearing
→ tilt to broken moon
→ return to Kael close-up
→ slow pull wide as Kael enters valley.

Music:
adventure rhythm fades into deep mysterious note.

CUT TO BLACK.

END PART 1.

--------------------------------------------------

[AUDIO DESCRIPTION]

Generate synchronized native stereo audio.

--------------------------------------------------

[KAEL VOICE]

Natural teenage-boy voice.

Age:
approximately mid-teens.

Voice qualities:
- youthful
- thoughtful
- emotionally expressive
- initially quiet
- clear English
- no exaggerated heroic delivery

Performance progression:

0–3 sec:
soft and reflective.

3–5 sec:
confused / shocked.

5–7 sec:
breathless disbelief.

7–9 sec:
suspicion becoming certainty.

9–12 sec:
urgent determination.

12–15 sec:
fear controlled by resolve.

IMPORTANT:

“He stole the moon!”

should sound like Kael genuinely believes what he has just witnessed.

Not comedic.

Not melodramatically shouted.

--------------------------------------------------

[NYX AUDIO]

No spoken words in PART 1.

Use:
- large controlled breathing
- deep throat resonance
- scale / feather movement
- powerful wing sweeps
- small curious exhale when looking toward Kael

Do NOT use:
- roaring
- evil laughter
- growling threats
- fire sounds

Nyx must remain ambiguous.

--------------------------------------------------

[MOON / MAGIC SOUND DESIGN]

Full moon:
subtle glassy harmonic ambience.

Crack:
deep celestial crystal fracture.

Fragment:
high silver shimmer,
soft harmonic resonance,
tiny star particles.

Nyx catches fragment:
low warm resonant pulse +
silver chime.

No explosive boom.

--------------------------------------------------

[ENVIRONMENT AUDIO]

NOCTARA:

- lake water
- night wind
- distant bells
- faint city ambience
- nocturnal insects
- tree leaves
- occasional distant bird

CHASE:

- footsteps
- gravel
- breath
- clothing
- faster wind
- Nyx’s wings

VALLEY:

- wider empty wind
- subtle echo
- distant stone resonance
- almost no wildlife

This sonic transition helps communicate leaving the safe kingdom.

--------------------------------------------------

[NON-DIEGETIC MUSIC]

Create an ORIGINAL cinematic fantasy score.

Instrumentation:

Opening:
- soft piano
- airy flute
- warm strings
- glockenspiel / celesta

Moon crack:
- glass harmonics
- low cello
- subtle brass

Nyx reveal:
- low strings
- bass clarinet
- restrained horns

Chase:
- rhythmic strings
- hand percussion
- low drums
- light brass pulses

Valley ending:
- low sustained strings
- distant choir texture without lyrics
- sparse metallic chime

MUSIC ARC:

0.00–2.20
peaceful wonder.

2.20–3.50
slight mystery.

3.50–5.20
celestial rupture.

5.20–7.20
mysterious Nyx reveal.

7.20–8.80
suspicion.

8.80–12.80
adventure/chase momentum.

12.80–15.00
ominous mystery cliffhanger.

No horror score.

No trailer-style massive percussion.

--------------------------------------------------

[CAMERA LANGUAGE]

Part 1 camera must move from calm cinematic observation into increasingly urgent adventure.

CAMERA ARC:

0–3.5 sec:
slow,
wide,
stable,
graceful.

3.5–5.2 sec:
sudden celestial focus.

5.2–8.8 sec:
dynamic sky tracking + reaction close-ups.

8.8–12.8 sec:
faster but smooth chase camera.

12.8–15 sec:
slow back down for giant valley reveal.

Use:
- slow dolly
- subtle crane
- elegant tilt
- rack focus
- giant moon compositions
- character profile close-up
- smooth aerial tracking of Nyx
- side-running tracking
- environmental parallax
- dramatic wide reveal

Avoid:
- handheld shake
- extreme fisheye
- constant fast cuts
- 360 spins
- Dutch angles
- chaotic action camera

--------------------------------------------------

[VISUAL STYLE]

Premium finished hand-painted 2D dark-fantasy animation.

MATCH THE STORYBOARD EXACTLY IN SPIRIT.

Use:

- delicate dark ink contours
- painterly 2D shading
- rich watercolor/gouache backgrounds
- stylized expressive faces
- cinematic blue-black environments
- silver atmospheric moonlight
- warm orange architecture lighting
- layered depth
- subtle soft bloom
- painterly dragon scales
- hand-crafted fantasy architecture

The finished film should feel like:

a premium illustrated fantasy movie brought to life.

NOT:
- photorealistic
- 3D CGI
- hyper-real dragon rendering
- anime
- flat vector
- storyboard animatic
- motion comic
- slideshow

--------------------------------------------------

[COLOR / LIGHTING ARC]

OPENING:

Deep navy sky.
Silver moon.
Warm orange castle lights.

Kael:
mostly cool moonlight with subtle warm bounce.

MOON CRACK:

Increase brilliant cool white-silver contrast.

NYX REVEAL:

Nyx remains near-black,
but use:
- blue rim light
- silver shard under-light
- intense amber eyes
- luminous pale teeth

CHASE:

Gradually reduce warm Noctara illumination as Kael leaves the kingdom.

VALLEY:

Palette becomes:
- colder blue
- gray
- charcoal
- pale cyan mist

Final composition:
Kael = dark silhouette
fragment = tiny bright silver point far away
moon = damaged silver
valley = cold mysterious blue-gray.

--------------------------------------------------

[KAEL MOTION RULES]

Opening:
natural seated breathing,
small head movement,
subtle hair flutter.

Reaction:
fast but believable rise to feet.

Running:
natural teenage sprint,
arms and legs follow realistic stylized physics,
tunic and hair respond to motion.

No:
- superhuman jumps
- parkour stunts
- magical powers
- impossible speed.

--------------------------------------------------

[NYX MOTION RULES]

Nyx must feel large and graceful.

Use:
- long serpentine body follow-through
- wings with convincing weight
- slight lag through tail
- flexible neck
- smooth aerial banking
- subtle head movements
- natural inertia

When catching shard:

Nyx approaches
→ matches shard trajectory
→ opens jaws
→ gently catches
→ closes jaw enough to secure it
→ banks away.

No violent snapping.

--------------------------------------------------

[MOON FRAGMENT MOTION]

Fragment falling:
follow gravity with magical slight drift.

Particle trail:
subtle silver sparks.

Once Nyx catches it:
remain physically fixed and stable in his grip.

Do not flicker in/out.

--------------------------------------------------

[CONTINUITY RULES]

Keep exactly:

ONE Kael.
ONE Nyx.
ONE moon fragment.
ONE moon.

Same:
- Kael design
- Nyx design
- castle architecture
- moon shape
- lake
- forest
- valley entrance
- night palette

Moon damage must persist after cracking.

Once Nyx catches fragment:
he retains it through all subsequent Part 1 shots.

Kael starts seated by lake.

He must physically stand and run.

Do not teleport him to the valley.

Castle lights gradually recede during chase.

--------------------------------------------------

[EMOTIONAL PERFORMANCE RULE]

Part 1 intentionally creates a FALSE interpretation.

The viewer should understand why Kael believes Nyx stole the fragment.

However, avoid proving Nyx evil.

Visual balance:

Nyx looks frightening
BUT
behaves carefully.

Kael sees:
giant black dragon + glowing moon shard + flying away.

Therefore he assumes:
“thief.”

This misunderstanding drives the next chapter.

--------------------------------------------------

[NEGATIVE CONSTRAINTS]

No storyboard sheet.
No panel borders.
No timestamps.
No captions.
No subtitles.
No production notes.
No title cards.
No watermark.
No logos.
No brands.

No duplicate Kael.
No duplicate Nyx.
No duplicate fragment.
No second moon.

No Kael costume change.
No hairstyle drift.
No older Kael.
No armor.
No weapons.

No Nyx redesign.
No red dragon.
No fire breathing.
No horns appearing/disappearing.
No eye-color changes.
No short-neck Nyx.
No bulky Western-dragon redesign.

No Zara.
No skeleton guardians.
No Bone Bridge.
No Moon Shrine reveal.

No blood.
No gore.
No injury.
No combat.
No attack.
No horror.
No dead bodies.

No moon explosion.
No planet destruction.
No falling castle.
No destroyed city.

No photorealism.
No 3D CGI.
No malformed anatomy.
No extra fingers.
No face flicker.
No scale inconsistency.
No teleportation.

--------------------------------------------------

[FINAL 3-SECOND PRIORITY]

The final sequence must provide a strong PART 2 hook.

Kael reaches the ridge.

He looks down.

Reveal:

THE VALLEY OF BONES.

Jagged cliffs.

Pale mist.

Ancient giant rib-like fossil formations.

Nyx flies deeper inside.

The silver moon fragment glows clearly from his jaws.

Then Kael looks upward.

The giant moon is:

cracked,
missing its shard,
noticeably dimmer.

Kael understands time may matter.

He looks back into the valley.

His fear becomes resolve.

Kael says:

<d>[English] You’re not getting away.</d>

Then:

<d>[English] I’m getting it back.</d>

He takes his first step into the valley.

Camera slowly pulls far backward.

Kael becomes tiny against the massive forbidden landscape.

The damaged moon hangs above everything.

Nyx’s distant silver shard-light disappears deeper into the canyon.

CUT TO BLACK.

END PART 1.

The viewer should immediately want to know:

“What is inside the Valley of Bones?”

and

“Did Nyx really steal the moon?”
```

</details>

<sub>Source: <a href="https://x.com/ManuAGI01/status/2086321605073105162">https://x.com/ManuAGI01/status/2086321605073105162</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 20 · 3,200 Paper Stars on a Rooftop

<sub>ManuAGI 🤖 - ( ManuIn ) &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2086294164409630916.jpg" alt="3,200 Paper Stars on a Rooftop" width="100%">](https://x.com/ManuAGI01/status/2086294164409630916)

<sub><b>▶ <a href="https://x.com/ManuAGI01/status/2086294164409630916">Watch the clip on the creator's post on X (@ManuAGI 🤖 - ( ManuIn ))</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Young creator Milo meets the giant paper lantern Luma on a nighttime rooftop and begins a chaptered story with glowing paper stars. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (23,253 characters)</summary>

```text
[REFERENCE CONTROL]

Use the uploaded PART 1 storyboard image for “The Little Creator and the 3,200 Paper Stars” as the PRIMARY visual, character, environment, scale, prop, lighting, performance, and narrative reference.

Generate a FINISHED cinematic animated sequence from this storyboard.

DO NOT reproduce the storyboard sheet itself.

The final video must NOT contain:
- storyboard borders
- storyboard panel layout
- panel numbers
- timestamps
- handwritten captions
- production notes
- character-reference drawings
- scale-reference diagrams
- storyboard title/header
- paper background
- footer decorations

The uploaded storyboard locks:

1. Milo’s exact character identity
2. Milo’s dark-blue oversized hoodie
3. Milo’s fluffy brown hair
4. Milo’s glowing-star satchel
5. Luma’s exact giant lantern design
6. Luma’s warm cream/orange paper texture
7. Luma’s sleepy face
8. Luma’s hanging ribbons and tassels
9. Pip’s exact firefly design
10. extreme Milo-vs-Luma scale
11. handmade glowing paper-star design
12. same magical rooftop environment
13. same distant nighttime city
14. deep indigo + warm amber palette
15. single-star placement story beat
16. final full-satchel cliffhanger

Translate the 15 storyboard panels into approximately 8 coherent cinematic shots.

DO NOT create fifteen one-second hard cuts.

Use clear:

cause → action → consequence → reaction.

--------------------------------------------------

[VIDEO GOAL]

Duration:
EXACTLY 15 seconds

Story time:
0:00–0:15

Aspect ratio:
16:9 landscape

Frame-rate feeling:
cinematic 24 fps

Visual medium:
premium painterly 2D animated short film

Genre:
magical gratitude story / whimsical rooftop fantasy

Audience:
family-friendly

Dialogue:
natural synchronized English

Audio:
native dialogue + character sounds + rooftop ambience + magical paper-star effects + original music

EMOTIONAL ARC:

quiet rooftop wonder
→ gratitude
→ magical giant reveal
→ tiny secret mission
→ difficult climb
→ first star placement
→ beautiful success
→ realization that thousands remain
→ mischievous cliffhanger

The overall feeling should be:

small creator,
huge dream,
warm gratitude.

--------------------------------------------------

[PART 1 STORY LIMIT]

PART 1 ONLY.

START:

Milo sits alone on a peaceful rooftop beneath a star-filled night sky with a satchel containing glowing handmade paper stars.

He is celebrating an important milestone:

3,200 supporters.

END:

Milo has attached EXACTLY ONE glowing paper star to Luma.

He then looks back at his still-overflowing satchel.

Milo gets a huge idea.

He whispers:

<d>[English] Maybe... all of them?</d>

Pip realizes what Milo means.

CUT TO BLACK.

DO NOT show:
- Milo attaching multiple stars
- Luma fully decorated
- hundreds of stars covering Luma
- Luma waking
- Luma flying higher
- stars leaving Luma
- sky formation
- giant “3200”
- “THANK YOU”
- full milestone celebration
- final hero shot

Those belong to PART 2.

--------------------------------------------------

[CHARACTER IDENTITY LOCK — MILO]

Match the uploaded storyboard EXACTLY.

MILO:

Tiny young creator.

Appearance:
- warm light skin
- soft rounded youthful face
- large expressive dark-brown eyes
- fluffy tousled medium-brown hair
- slightly oversized head for appealing animation proportions

Clothing:
- oversized dark navy-blue hoodie
- dark/simple trousers
- little shoes/boots
- small brown crossbody satchel
- satchel filled with glowing folded paper stars

Personality:
- grateful
- creative
- curious
- optimistic
- emotional
- slightly impulsive
- playful

PART 1 PERFORMANCE ARC:

0–3 sec:
quietly grateful

3–5 sec:
curious wonder

5–7 sec:
gets an idea

7–10 sec:
determined tiny climber

10–12 sec:
careful and emotionally invested

12–15 sec:
proud → inspired → mischievously ambitious

Milo should never feel arrogant.

The milestone means something because of the people represented by the stars.

CRITICAL:

Keep exact:
- face
- brown hair
- navy hoodie
- satchel
- body proportions
- age appearance
- scale

--------------------------------------------------

[CHARACTER IDENTITY LOCK — LUMA]

Match the uploaded storyboard exactly.

LUMA:

A gigantic living floating sky lantern.

Appearance:
- enormous rounded lantern body
- warm cream / parchment-orange paper surface
- handmade subtle paper texture
- decorative curved motifs
- gentle closed sleepy eyes
- tiny peaceful curved smile
- soft amber-gold inner illumination
- decorative frame underneath
- multiple long hanging ribbons / tassels
- huge scale relative to Milo

Personality:
- peaceful
- gentle
- warm
- sleepy
- safe
- quietly magical

PART 1:

Luma remains ASLEEP for the entire sequence.

Allowed:
- very subtle floating
- gentle vertical bob
- soft breathing-like light pulse
- tiny peaceful smile response when first star is attached

Do NOT:
- open her eyes
- speak
- rise dramatically
- intentionally move Milo
- activate celebration magic

Her awakening happens in PART 2.

--------------------------------------------------

[CHARACTER IDENTITY LOCK — PIP]

Match the storyboard.

PIP:

Tiny glowing firefly helper.

Appearance:
- small round yellow-gold body
- pale luminous glow
- large expressive eyes
- tiny antennae
- translucent wings
- much smaller than Milo

Personality:
- practical
- cautious
- loyal
- funny
- suspicious of Milo’s big ideas

Performance:

calm companion
→ curious
→ realizes Milo’s plan
→ worried during climb
→ nervous during star placement
→ pleased that it works
→ horrified by Milo’s final bigger idea

Pip may speak in short natural lines.

--------------------------------------------------

[GLOWING PAPER STAR LOCK]

All stars must match the storyboard.

Design:
- handmade folded paper stars
- cream / pale-gold paper
- visible folded facets
- warm golden light from inside
- physical tactile objects
- lightweight
- slightly magical

Close views should preserve real paper folds.

At the beginning:
the satchel contains many glowing stars.

During PART 1:
Milo removes ONLY ONE star for decoration.

At the final shot:
the satchel must still visibly overflow with stars.

--------------------------------------------------

[STAR SYMBOLISM]

The stars represent individual pieces of support from Milo’s audience/community.

The video should communicate this emotionally without showing social-media interfaces.

No:
- phones
- follower counters
- social-media app screens
- X logos
- Twitter logos
- platform branding

Milo may verbally reference:

“3,200”

but the milestone should primarily be represented by the glowing paper stars.

--------------------------------------------------

[ENVIRONMENT LOCK — ROOFTOP]

Maintain the exact nighttime rooftop world from the storyboard.

Include:
- cozy high rooftop
- old rooftop stone/brick surfaces
- chimney / small rooftop structures
- a few potted plants
- distant city buildings
- warm glowing windows
- layered rooftops
- deep blue night sky
- stars
- crescent moon
- subtle distant clouds
- warm rooftop accent lights

Mood:
quiet,
safe,
dreamlike,
intimate.

The city is far below.

No crowds.

No extra characters.

--------------------------------------------------

[SCALE RULES]

Extreme scale contrast is critical.

Milo is tiny compared with Luma.

Use storyboard scale:

- Milo smaller than one tassel knot
- Luma’s lantern body towers above Milo
- hanging ribbons are thick enough for Milo to climb like ropes
- one section of Luma’s body is enormous compared with Milo’s full height

Pip is much smaller than Milo.

Never accidentally render Milo human-sized beside Luma.

--------------------------------------------------

[WORLD / MOTION LOGIC]

Clear cause-and-effect:

Milo looks at stars
→ remembers milestone

Milo looks upward
→ notices sleeping Luma

Luma’s huge blank lantern surface
→ gives Milo decorating idea

Milo wants to celebrate
→ climbs ribbons

Milo reaches lantern
→ attaches ONE star

Star lights up beautifully
→ Milo feels successful

Milo looks down
→ sees full satchel

Full satchel + enormous lantern
→ Milo gets much bigger idea

Pip realizes what Milo is thinking
→ comic panic cliffhanger

No random magic.

--------------------------------------------------

integrated_multimodal_description:

[SHOT 1] — 0.00s–1.80s
A QUIET ROOFTOP AND 3,200 LITTLE LIGHTS

Open with a beautiful nighttime establishing shot.

Deep indigo sky.

Crescent moon.

Thousands of distant real stars.

Camera slowly descends toward a peaceful rooftop overlooking a softly glowing city.

Milo sits near the rooftop edge.

Beside him is his brown satchel.

Warm golden light leaks from inside.

Milo opens the satchel.

Reveal many handmade glowing paper stars.

He gently picks ONE up with both hands.

The warm star light illuminates his face.

Pip floats quietly beside him.

Camera:
wide skyline
→ slow dolly toward Milo
→ overhead satchel insert
→ intimate close-up on glowing star in his hands.

Dialogue:

Milo, softly:
<d>[English] Three thousand two hundred...</d>

Tiny pause.

Milo smiles.

<d>[English] That’s a lot of people.</d>

Pip gives a soft happy chirp.

Sound:
- distant nighttime city
- light rooftop breeze
- cloth movement
- satchel leather
- subtle paper rustle
- soft magical star hum

Music:
gentle piano + glockenspiel + warm strings.

--------------------------------------------------

[SHOT 2] — 1.80s–3.50s
A REASON TO SAY THANK YOU

Milo holds the glowing star near his chest.

His expression becomes warm and grateful.

He looks at the many remaining stars.

Dialogue:

Milo:
<d>[English] We should do something special.</d>

Pip tilts his head.

Then Milo notices an enormous warm amber light above him.

The light softly brightens his face.

Milo slowly looks upward.

Camera follows his gaze.

Reveal the lower edge of Luma entering frame.

Long decorative ribbons sway gently beneath her.

Milo’s eyes widen.

Dialogue:

Milo:
<d>[English] Oh...</d>

Pip slowly turns upward too.

Sound:
- gentle ribbon movement
- low warm lantern hum
- night breeze

Music:
introduce airy flute and soft wonder motif.

--------------------------------------------------

[SHOT 3] — 3.50s–5.20s
THE SLEEPY SKY LANTERN

Camera continues upward into a full magical reveal of Luma.

Luma floats above the city.

Huge.

Round.

Warmly illuminated.

Her eyes remain peacefully closed.

Her tiny smile is gentle.

She slowly bobs in the night air.

Milo is tiny at the bottom of frame.

This shot must strongly emphasize SCALE.

Milo looks at:
the glowing star in his hand...

then Luma’s enormous blank lantern surface.

Idea forming.

His mouth curls into a grin.

Pip notices Milo’s expression.

Dialogue:

Milo, whispering:
<d>[English] Pip...</d>

Pip:
<d>[English] What?</d>

Milo:
<d>[English] I have an idea.</d>

Pip immediately becomes suspicious.

Pip:
<d>[English] That face worries me.</d>

Music:
small mischievous plucked motif enters.

--------------------------------------------------

[SHOT 4] — 5.20s–7.00s
THE SECRET STAR MISSION

Milo walks beneath one long hanging Luma ribbon.

He grabs it with both hands.

Tests it.

Looks upward.

It extends far above him.

Milo puts the glowing star securely into his hoodie pocket / small pouch while keeping it visible and safe.

Then starts climbing.

Pip hovers beside him.

Dialogue:

Milo, whispering:
<d>[English] We should celebrate.</d>

Pip:
<d>[English] From the roof.</d>

Milo climbs higher.

Milo:
<d>[English] Too ordinary.</d>

Pip:
<d>[English] Of course.</d>

Camera:
low-angle ribbon shot
→ side tracking with Milo climbing
→ pull wide showing tiny Milo beneath giant lantern.

Sound:
- fabric ribbon strain
- Milo’s tiny climbing effort
- shoe taps
- Pip wing buzz
- soft Luma hum

--------------------------------------------------

[SHOT 5] — 7.00s–9.00s
MILO VS. LUMA

Milo reaches a large tassel knot.

He pauses and sits momentarily on it.

The knot itself is nearly Milo-sized.

He looks upward at the enormous lantern surface.

Pip floats beside him, slightly out of breath despite being a firefly.

Use a vertical scale composition.

Milo climbs the final short ribbon section.

He reaches Luma’s lower lantern edge.

Luma remains completely asleep.

Dialogue:

Milo:
<d>[English] Almost there...</d>

Pip:
<d>[English] Define “almost.”</d>

Milo pulls himself onto a decorative rim.

Dialogue:

Milo:
<d>[English] There.</d>

Sound:
- ribbon movement
- tiny climb grunt
- paper lantern creak
- soft floating ambience

--------------------------------------------------

[SHOT 6] — 9.00s–11.00s
THE FIRST STAR

Milo retrieves the ONE glowing folded star.

He looks at it.

Then at Luma’s huge lantern body.

He carefully presses the handmade star onto the lantern using a tiny clip / adhesive tab.

Take time with this.

The star gently settles.

For half a beat:

nothing.

Then its glow becomes slightly warmer.

The golden star light blends beautifully with Luma’s amber paper body.

Milo’s face lights up.

Pip watches cautiously.

Luma’s sleeping smile curves perhaps one tiny degree more.

She does NOT wake.

Dialogue:

Milo, whispering:
<d>[English] One little thank-you.</d>

Soft click.

Milo:
<d>[English] Perfect.</d>

Sound:
- paper touching paper
- tiny clip click
- warm magical “ting”
- Luma’s gentle light pulse

Camera:
close-up Milo’s hands
→ macro star attachment
→ reaction on Milo
→ Luma’s peaceful sleepy expression.

Music:
gentle emotional success note.

--------------------------------------------------

[SHOT 7] — 11.00s–12.80s
ONE VERY BIG SUCCESS

Milo leans back against Luma’s decorative rim.

He admires the glowing star.

The single paper star looks beautiful against the huge warm lantern surface.

Pip slowly smiles.

Milo:
<d>[English] Look at that.</d>

Pip:
<d>[English] Okay...</d>

Pip studies it.

<d>[English] That is actually nice.</d>

Milo beams.

Camera pulls out slightly.

Clearly show:

tiny Milo
+
one glowing star
+
enormous mostly undecorated Luma.

The contrast is important.

--------------------------------------------------

[SHOT 8] — 12.80s–15.00s
THE MUCH BIGGER IDEA — CLIFFHANGER

Milo’s proud smile suddenly pauses.

He remembers something.

He looks downward.

Camera follows his gaze toward the rooftop.

His satchel remains there / hangs securely nearby according to spatial setup, visibly overflowing with glowing paper stars.

Alternatively, if he carried the satchel during the climb, show it hanging securely from his shoulder and still overflowing.

CRITICAL:
do not teleport the satchel.

Use whichever configuration is established earlier and maintain it consistently.

Milo slowly opens / looks into it.

Dozens upon dozens of glowing folded stars illuminate his face.

Then he looks at:

the full satchel...

the ONE star on Luma...

Luma’s ENORMOUS remaining lantern surface.

Milo’s eyes widen.

A mischievous smile grows.

Pip looks at Milo.

Pip looks at the satchel.

Pip looks at enormous Luma.

Pip’s expression turns to immediate horror.

Pip:
<d>[English] Milo...</d>

Milo raises the satchel slightly.

Milo, delighted whisper:
<d>[English] Maybe... all of them?</d>

Pip’s eyes become huge.

Pip:
<d>[English] ALL?!</d>

Luma continues peacefully sleeping.

The ONE attached star glows softly.

Hold on:

Milo = enormous inspiration  
Pip = comic panic  
Luma = peacefully unaware  

CUT TO BLACK.

END PART 1.

--------------------------------------------------

[AUDIO DESCRIPTION]

Generate synchronized native stereo audio.

--------------------------------------------------

[MILO VOICE]

Natural young creator voice.

Age feeling:
young / youthful, not adult.

Qualities:
- warm
- sincere
- curious
- imaginative
- emotionally grateful
- playful
- clear English

Do not make Milo sound boastful.

His line:

<d>[English] Three thousand two hundred...</d>

should sound genuinely amazed and appreciative.

His final:

<d>[English] Maybe... all of them?</d>

should be playful, excited and slightly mischievous.

--------------------------------------------------

[PIP VOICE]

Small cute firefly voice.

Qualities:
- slightly higher pitch
- quick
- expressive
- cautious
- dry comic timing
- understandable English

Performance:

beginning:
supportive

middle:
increasing suspicion

climb:
slightly anxious

first star:
pleasantly surprised

ending:
immediate panic

Final:

<d>[English] ALL?!</d>

is the comedy punctuation.

--------------------------------------------------

[LUMA AUDIO]

No spoken dialogue in PART 1.

Use only:
- very soft floating-lantern hum
- subtle paper movement
- gentle inner magical resonance
- tiny warm pulse when star is attached

No snoring is necessary unless extremely soft and cute.

Luma remains asleep.

--------------------------------------------------

[ENVIRONMENT AUDIO]

Nighttime rooftop sound bed:

- soft breeze
- distant city ambience
- very faint traffic far below
- occasional distant bird/night insect
- fabric ribbon movement
- rooftop plants rustling
- subtle paper-star sounds
- Pip wing buzz
- lantern hum

Keep everything intimate.

--------------------------------------------------

[STAR SOUND DESIGN]

Paper stars need a signature sound identity.

Physical handling:
soft folded-paper rustle.

Glow:
delicate glassy/glockenspiel-like shimmer.

Attachment:
tiny paper “tap” + gentle magical “ting.”

Do NOT use:
- sci-fi electricity
- laser sounds
- aggressive magical effects

--------------------------------------------------

[NON-DIEGETIC MUSIC]

Use an ORIGINAL whimsical emotional score.

Instrumentation:
- soft piano
- delicate glockenspiel
- pizzicato strings
- airy flute
- light harp
- warm string pad
- subtle marimba
- tiny bell accents

MUSIC ARC:

0.00–1.80
quiet rooftop wonder.

1.80–3.50
gentle gratitude.

3.50–5.20
magical Luma reveal.

5.20–7.00
playful mission rhythm.

7.00–9.00
light climbing comedy.

9.00–11.00
small emotional star-placement motif.

11.00–12.80
warm success.

12.80–15.00
mischievous rising idea motif.

End with playful comic sting after Pip says:

<d>[English] ALL?!</d>

No epic trailer music.

No dramatic action score.

--------------------------------------------------

[CAMERA LANGUAGE]

PART 1 camera should gradually move from intimate to enormous scale.

CAMERA ARC:

0–3.5 sec:
quiet rooftop wides + emotional close-ups.

3.5–5.2 sec:
large upward reveal.

5.2–9 sec:
miniature adventure camera.

9–12.8 sec:
intimate star-placement coverage.

12.8–15 sec:
reaction-driven cliffhanger.

Use:
- slow dolly
- gentle tilt
- upward reveal
- macro star inserts
- low-angle climbing shots
- vertical scale compositions
- soft rack focus
- reaction close-ups
- gentle final push toward Milo

Avoid:
- handheld shaking
- crash zoom
- excessive cuts
- spinning camera
- action-movie camera movement
- Dutch angles

--------------------------------------------------

[VISUAL STYLE]

Premium finished painterly 2D animation.

Match the uploaded storyboard EXACTLY in spirit:

- hand-drawn ink-like contours
- watercolor/gouache-inspired fills
- deep painterly night skies
- warm paper-lantern textures
- expressive rounded characters
- cinematic glow
- delicate atmospheric city depth
- charming handmade objects
- subtle squash and stretch
- believable fabric/ribbon movement

The video should look like the storyboard artwork has come alive.

NOT:
- storyboard animatic
- slideshow
- motion comic
- photorealism
- 3D CGI
- anime
- vector animation
- cel-shaded 3D

--------------------------------------------------

[COLOR / LIGHTING]

Primary palette:

NIGHT:
- navy blue
- indigo
- subtle violet
- midnight teal

WARM LIGHT:
- amber
- golden yellow
- cream
- soft orange

MILO:
dark blue hoodie with warm star-light reflections.

PIP:
small yellow-gold glow.

LUMA:
largest warm amber light source.

Paper stars:
cream-gold.

Lighting progression:

0–3 sec:
mostly cool night with small warm star light.

3–5 sec:
Luma introduces large warm amber source.

5–9 sec:
mix of cool moonlight and warm lantern rim light.

9–12 sec:
single paper star becomes a delicate focal glow.

12–15 sec:
satchel illuminates Milo’s excited face with many warm points.

No neon colors.

No overexposure.

--------------------------------------------------

[MOTION RULES — MILO]

Natural tiny-character movement.

Use:
- soft seated posture
- careful star handling
- curious head tilts
- expressive eyes
- hoodie fabric reacting to breeze
- determined climbing
- hands gripping ribbons
- stable footing
- gentle placement of star

No:
- superhero jumping
- flying
- impossible leaps
- dangerous falls

--------------------------------------------------

[MOTION RULES — LUMA]

Luma floats gently.

Use:
- slow vertical bob
- minimal horizontal drift
- ribbons responding softly to air
- subtle paper flex
- gentle internal light breathing

During star attachment:
only a tiny warm light pulse.

No awakening.

--------------------------------------------------

[MOTION RULES — PIP]

Use:
- natural hovering
- fast tiny wings
- subtle inertia
- head tilts
- expressive eye widening
- small arcs around Milo

Do not have Pip carry Milo.

--------------------------------------------------

[CONTINUITY RULES]

Maintain:

one Milo
one Pip
one Luma

Same:
- rooftop
- skyline
- crescent moon
- satchel
- paper stars
- Luma ribbons
- character outfits
- scale
- night lighting direction

Milo begins on rooftop.

He climbs Luma using her ribbons.

Do NOT teleport him onto Luma.

Exactly ONE star is attached during Part 1.

Once attached, the star remains visible.

Luma stays asleep.

The satchel remains full at ending.

--------------------------------------------------

[NEGATIVE CONSTRAINTS]

No storyboard sheet.
No panel frames.
No numbers.
No timestamps.
No captions.
No subtitles.
No production notes.
No watermark.
No social-media logo.
No X logo.
No Twitter logo.
No platform UI.

No duplicate Milo.
No duplicate Pip.
No duplicate Luma.
No identity drift.
No clothing changes.
No hairstyle changes.
No scale inconsistency.

No awake Luma.
No talking Luma.
No angry Luma.
No fire.
No burning lantern.
No falling.
No injury.
No dangerous rooftop behavior.
No destructive magic.

No multiple stars attached in Part 1.
No fully decorated lantern.
No star explosion.
No “3200” sky formation yet.
No “THANK YOU” sky formation.
No Part 2 celebration.

No warped hands.
No extra fingers.
No malformed face.
No melting lantern.
No flickering character identity.
No disappearing satchel.

--------------------------------------------------

[FINAL 2.5-SECOND PRIORITY]

The ending must clearly create anticipation for PART 2.

Show:

ONE glowing paper star attached to Luma.

Milo proudly admires it.

Then Milo looks into his still-overflowing satchel.

Many warm paper stars glow inside.

Milo looks from:

satchel
→ single star
→ enormous empty lantern surface.

His expression becomes increasingly excited.

Pip slowly realizes what Milo is thinking.

Pip:

<d>[English] Milo...</d>

Milo smiles:

<d>[English] Maybe... all of them?</d>

Pip:

<d>[English] ALL?!</d>

Luma remains peacefully asleep.

Hold long enough for:

Milo = ambitious gratitude  
Pip = comic panic  
Luma = peacefully unaware  

to register clearly.

CUT TO BLACK.

END PART 1.

The viewer should immediately want to see how 3,200 tiny stars transform the night in PART 2.
```

</details>

<sub>Source: <a href="https://x.com/ManuAGI01/status/2086294164409630916">https://x.com/ManuAGI01/status/2086294164409630916</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 21 · Hawaii Grows From a Chocolate Egg

<sub>マグマグ &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 10 &nbsp;·&nbsp; 1344×768 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2096749565412331841.jpg" alt="Hawaii Grows From a Chocolate Egg" width="100%">](https://x.com/loglogrog/status/2096749565412331841)

<sub><b>▶ <a href="https://x.com/loglogrog/status/2096749565412331841">Watch the clip on the creator's post on X (@マグマグ)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A photoreal chocolate egg cracks open as its shell and filling continuously become a miniature Hawaii landscape, ending on a tourism-ad title card. Native-video output: 10s · 1344×768. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,308 characters)</summary>

```text
[CITY] = ハワイ
[CITY_NAME_DISPLAY] = ハワイ
[FINAL_TAGLINE] = ひらいて、旅がはじまる。

integrated_multimodal_description:

[Shot 1] A single continuous unbroken cinematic macro shot. No cuts, no scene changes, no teleporting, and no sudden replacements.

The scene begins with one realistic chocolate surprise egg placed upright on a simple elegant surface. The egg is the clear hero of the shot. It has a glossy chocolate shell with subtle handmade imperfections, soft highlights, delicate texture, and a premium confectionery feel. The lighting is warm, inviting, and slightly magical, with a shallow depth of field and a premium commercial look.

The egg must feel edible and real. The shell should look like real chocolate, not plastic, not ceramic, and not a toy. Fine surface texture, gentle gloss, tiny irregularities, and believable thickness should be visible.

At first, the chocolate egg is completely intact.

Gradually, subtle tension appears in the shell. Fine cracks begin to form naturally along the surface. The cracks spread slowly and elegantly, as if something beautiful is growing from within.

The transformation into [CITY] begins directly from this physical process.

Without interrupting the shot, the egg opens and transforms continuously.

The chocolate shell cracks, separates, curls, lifts, and unfolds in a graceful way. Pieces of the shell do not simply disappear. They remain physically connected to the transformation and become part of the emerging miniature city.

The inside of the egg reveals a warm, surprising inner world. The inner material may include soft chocolate layers, creamy confection-like texture, and delicate edible structural forms. Everything that appears must feel derived from the original egg.

As the egg opens, the miniature city of [CITY] begins to grow from inside it.

The transformation must feel like one continuous physical process:
sealed chocolate egg → fine cracks → shell opening → interior revealed → miniature city structures rising from within → the completed city unfolding from the egg.

Nothing pops into existence.
Nothing instantly swaps shape.
Nothing should feel like a hidden cut.

Before generation, infer a small number of visually iconic elements strongly associated with [CITY], then reinterpret only the most recognizable ones as part of this miniature edible city.

Do not turn the result into a crowded landmark collage.
Do not overfill the frame.
Keep the city readable, elegant, and beautiful.

The city should include a few recognizable urban and local elements such as streets, rooftops, bridges, towers, rail lines, rivers, trees, and culturally resonant architecture, but all reimagined as if they were born from the chocolate egg itself.

The shell edges may become ridges, terraces, or framing elements around the city.
Chocolate layers may become terrain and building mass.
Interior creamy or confection-like details may become roads, rooftops, pathways, and decorative city features.
The material continuity must always remain believable.

The city should look like an edible miniature diorama: intricate, tactile, warm, and slightly surreal, but still physically plausible.

Camera behavior:
The camera starts in tight macro close-up on the intact egg.
As the shell begins to crack and open, the camera remains intimate and steady, emphasizing material detail and the elegance of the transformation.
As the city becomes recognizable, the camera performs one extremely slow and smooth dolly backward with a subtle upward reveal.
No fast zoom.
No orbit.
No handheld movement.

In the final phase of the shot, reveal the completed miniature city of [CITY] emerging beautifully from the opened chocolate egg.

The final image should feel like a premium tourism commercial crossed with high-end confectionery advertising:
warm,
wonder-filled,
appetizing,
surprising,
and emotionally memorable.

Soft steam, glow, or delicate atmospheric motion may be present if appropriate, but keep it subtle and elegant.

Near the end, minimal clean typography appears at the lower portion of the frame:

"[CITY_NAME_DISPLAY]"

Directly beneath it, smaller:

"[FINAL_TAGLINE]"

The text must be simple, elegant, readable, correctly spelled, and visually integrated into the final composition.
No other text appears.

Hold briefly on the final hero composition:
the opened chocolate egg acting like a cradle for the miniature city,
beautiful lighting,
shallow depth of field,
rich chocolate texture,
and a visually irresistible tourism-commercial finish that makes the viewer want to visit [CITY].

Visual style:
photorealistic macro commercial cinematography, premium confectionery advertisement, edible miniature city diorama, warm luxury food lighting, tactile chocolate texture, elegant surreal transformation, cinematic shallow depth of field, highly detailed but restrained composition.

Critical continuity requirements:
The entire video is ONE continuous shot.
The entire city grows from ONE chocolate egg.
The egg remains the physical source of the entire transformation.
All changes are gradual, visible, and materially connected.
The shell must crack and open naturally.
The city must emerge progressively from within the egg.
No jump cuts.
No hidden transitions.
No sudden completed city.
No random fantasy city unrelated to [CITY].

Avoid:
plastic toy look,
cartoon toy appearance,
rubber texture,
ceramic egg appearance,
generic fantasy castle city,
instant morphing,
fast transformation,
jump cuts,
scene changes,
objects appearing from nowhere,
overcrowded landmarks,
unreadable text,
garbled Japanese characters,
misspelled city name,
extra captions,
extra logos,
cheap CGI feeling,
messy composition,
and any transformation that breaks physical continuity.

overall_soundscape:
Soft premium commercial ambience. Quiet room tone with subtle confectionery handling atmosphere. Gentle cracking sounds as the chocolate shell fractures. Delicate crisp chocolate break sounds, soft interior movement, faint textural shifting, and subtle reveal ambience as the city emerges. No dialogue.

non_diegetic_music:
A warm, elegant, slightly magical commercial score. Soft piano and delicate orchestral textures, building gently as the egg opens and the city emerges. Emotional but restrained, never overwhelming the tactile chocolate sounds.
```

</details>

<sub>Source: <a href="https://x.com/loglogrog/status/2096749565412331841">https://x.com/loglogrog/status/2096749565412331841</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 22 · A Train Window Travels through History

<sub>EndFolding79421 &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 8.064 &nbsp;·&nbsp; 360p &nbsp;·&nbsp; 161:90</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2088060516027785340.jpg" alt="A Train Window Travels through History" width="100%">](https://x.com/EndFolding79421/status/2088060516027785340)

<sub><b>▶ <a href="https://x.com/EndFolding79421/status/2088060516027785340">Watch the clip on the creator's post on X (@EndFolding79421)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The carriage and passenger remain in place while the window view shifts from snowy peaks to old streets and dinosaurs.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (8,897 characters)</summary>

```text
<Picture 1> is the EXACT first frame of the video.

Preserve the woman, her face, blonde hair, cream knit outfit, white boots, seated pose, brown leather seat, modern luxury high-speed train interior, panoramic windows, camera position, warm interior sunlight, and overall photorealistic cinematic appearance established by <Picture 1>.

no music

integrated_multimodal_description:

[Visual Anchor]
A photorealistic cinematic 8-second sequence inside a modern luxury high-speed train. The woman remains seated comfortably beside the panoramic windows while the train continuously moves forward at normal high-speed rail velocity.

ONLY THE WORLD OUTSIDE THE TRAIN travels backward through history.

The train interior NEVER changes.
The woman NEVER changes.
Her clothing NEVER changes.
The windows NEVER change.
The train NEVER changes into an older vehicle.

The woman remains in normal real-time throughout, calmly enjoying the impossible scenery. She breathes naturally, occasionally blinks, subtly follows the landscape with her eyes, and gives a faint knowing smile. She is never frightened, startled, confused, or alarmed. She behaves as though she already knew this would happen.

The historical effect uses a repeating rhythm:

STABLE ERA → RAPID BACKWARD TIME-LAPSE TRANSFORMATION → STABLE ERA → RAPID BACKWARD TIME-LAPSE TRANSFORMATION.

During each stable era, the exterior world moves and behaves at NORMAL REAL-TIME SPEED while the train continues traveling through it.

During each transition, ONLY the exterior environment rapidly rewinds through time.

[00:00.000–00:01.000 — PRESENT DAY]

Begin EXACTLY from <Picture 1>.

The modern train moves naturally forward through the cold snowy alpine landscape.

Strong realistic parallax is visible outside: nearby snow-covered terrain moves quickly past the windows while the distant mountains move more slowly.

The woman quietly watches the scenery.

Natural breathing.
One subtle blink.
Small relaxed eye movement.

The snowy mountain landscape remains stable long enough for the viewer to recognize the present-day setting.

[00:01.000–00:01.500 — FIRST TIME REWIND]

The ENTIRE exterior world suddenly begins rapidly traveling backward through time like an accelerated environmental time-lapse.

There is NO camera cut.

Snow rapidly retreats across the entire landscape.

Frozen ground becomes exposed earth.

Grass spreads rapidly.

Trees and vegetation appear and grow across the mountains and valleys.

The cold white alpine environment smoothly transforms into a lush green temperate landscape.

The transformation happens across ALL visible windows simultaneously.

The woman and modern train remain completely unchanged and continue moving in normal real-time.

[00:01.500–00:02.500 — LUSH GREEN LAND]

The time-lapse transformation STOPS.

The exterior is now a rich green countryside.

Forests, grassy hills, streams, wild vegetation, and distant mountains move naturally past the train.

Everything outside now behaves at normal real-time speed.

Leaves move in the wind.
Water flows naturally.
The train continues traveling forward.

The woman calmly watches and gives a very slight peaceful smile.

[00:02.500–00:03.000 — SECOND TIME REWIND]

The exterior world rapidly rewinds again.

The green countryside transforms through accelerated historical change.

Roads appear as dirt tracks.

Old fences develop.

Buildings rapidly emerge into 19th-century construction.

The entire landscape transitions smoothly into the 1800s.

No cut.

[00:03.000–00:04.100 — 1800s]

The transformation STOPS.

The train now passes through a living 19th-century town and countryside.

The exterior operates at NORMAL SPEED.

Horse-drawn carriages travel along dirt streets.

Horses walk and trot naturally.

People wearing 1800s clothing move along sidewalks and streets.

Old masonry and timber buildings, storefronts, chimneys, wooden fences, wagons, and period street activity pass naturally outside.

NO modern vehicles.
NO modern signs.
NO modern technology outside.

The train continues moving rapidly through the historical environment.

The woman remains relaxed and simply watches.

[00:04.100–00:04.600 — THIRD TIME REWIND]

History rapidly rewinds again.

The 1800s town begins disappearing through a smooth accelerated time-lapse.

Buildings regress and vanish.

Roads deteriorate into ancient tracks.

Modern-style structures disappear completely.

The landscape rapidly transforms into the ancient Roman era.

The transformation occurs across the ENTIRE exterior view simultaneously.

[00:04.600–00:05.800 — ROMAN ERA]

The transformation STOPS.

The train now passes beside a large ancient battlefield.

Everything outside moves at NORMAL REAL-TIME SPEED.

Roman soldiers in historically inspired armor fight opposing barbarian warriors across an open field.

Soldiers run.
Shields collide.
Spears move.
Banners flap in the wind.
Horses cross portions of the battlefield.
Dust rises beneath their feet.

The battle remains at a believable distance from the train and remains entirely outside.

No soldier notices the train.
No soldier approaches the windows.
No one interacts with the woman.

The woman watches the battle calmly.

She gives a small blink and remains completely composed, as though this is expected.

[00:05.800–00:06.300 — MASSIVE TIME REWIND]

The exterior suddenly accelerates backward across an enormous span of history.

The Roman soldiers rapidly disappear.

Battlefield activity vanishes.

Roads disappear.

Structures disappear.

Human civilization disappears completely.

Vegetation, terrain, climate, and geological features rapidly transform in a massive backward time-lapse spanning millions of years.

The modern train and woman remain completely unchanged.

[00:06.300–00:08.000 — PREHISTORIC WORLD]

The transformation STOPS.

The train is now traveling through a vast untouched prehistoric landscape.

Everything outside returns to NORMAL REAL-TIME SPEED.

No humans.
No cities.
No buildings.
No roads.
No modern objects.

A broad primitive landscape stretches toward distant mountains with exposed earth, ancient vegetation, sparse forests, mist, and untouched wilderness.

Several dinosaurs move naturally in the DISTANT landscape.

A huge long-necked dinosaur slowly walks across the far background.

Smaller dinosaurs move farther away among ancient vegetation.

Keep the dinosaurs at believable distances.

NO dinosaur approaches the train.
NO dinosaur looks through the windows.
NO dinosaur attacks.

The train continues traveling forward normally through this prehistoric world.

The woman quietly watches the dinosaurs.

Near the final moment, she gives a subtle knowing smile.

End while the train is still moving through the prehistoric landscape.

[CRITICAL WINDOW CONTINUITY]

ALL panoramic train windows show ONE SINGLE CONTINUOUS EXTERIOR WORLD.

The windows must NOT behave like separate television screens.

Do NOT place different eras in different window panes.

Do NOT show snow in one window and green countryside in another.

Do NOT show the 1800s in one window and Romans in another.

Do NOT show Romans in one window and dinosaurs in another.

Whenever time changes, the ENTIRE exterior environment visible through EVERY window changes together as one unified world.

The physical window frames remain normal structural parts of the train, but the exterior beyond them is one continuous landscape.

[CAMERA]

One continuous interior shot for the full 8 seconds.

Maintain approximately the camera composition established by <Picture 1>.

No cuts.
No exterior shots of the train.
No camera leaving the carriage.

Subtle realistic train vibration.

The woman remains clearly visible in the foreground while the panoramic windows remain large enough for the audience to clearly read every historical era.

Strong realistic exterior parallax continuously proves that the train is physically moving forward.

During historical transitions, the camera itself does NOT speed up and the train does NOT accelerate.

Only history outside rewinds rapidly.

overall_soundscape:

Continuous subdued interior ambience of a modern high-speed train: low rail rumble, soft mechanical vibration, subtle air-conditioning, and muted rushing sound from outside.

The woman breathes softly and naturally.

Each stable historical era contributes faint exterior ambience filtered realistically through the sealed train windows.

Present day: soft rushing alpine wind.

Green countryside: faint birds and natural countryside ambience.

1800s: distant horse hooves, carriage wheels, and faint town activity.

Roman era: distant muffled battle cries, shield impacts, horses, and battlefield movement.

Prehistoric era: distant wind, low animal calls, and faint dinosaur vocalizations.

Exterior sounds remain subdued and muffled by the train's glass.

No dialogue.

non_diegetic_music:
N/A
```
```

</details>

<sub>Source: <a href="https://x.com/EndFolding79421/status/2088060516027785340">https://x.com/EndFolding79421/status/2088060516027785340</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 23 · A White Cat Summer Calendar Animation

<sub>renataro9 &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15.168 &nbsp;·&nbsp; 720p &nbsp;·&nbsp; 7:4</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2089573433806098785.jpg" alt="A White Cat Summer Calendar Animation" width="100%">](https://x.com/renataro9/status/2089573433806098785)

<sub><b>▶ <a href="https://x.com/renataro9/status/2089573433806098785">Watch the clip on the creator's post on X (@renataro9)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A desk calendar turns through watercolor summer scenes with a white cat, goldfish and fireworks.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (3,627 characters)</summary>

```text
integrated_multimodal_description: [Shot 1] 15秒間の一続きの映像。「白猫の6日間の夏休み」を描く、可愛い水彩絵本風の日めくりカレンダー。 夏の午後の日差しが入る、涼しげな日本家屋。木製の机の中央に、二つの小さな金属リングで綴じた卓上型の日めくりカレンダーが置かれている。 窓辺には透明な青い風鈴。背景には緑の葉と眩しい夏空が柔らかくぼけて見える。机の端には青紫色の朝顔を一輪だけ置く。カレンダーを遮る物は置かない。 カメラはカレンダーを真正面から撮影したまま固定する。カメラ位置、焦点距離、カレンダーの位置、金属リング、紙の寸法を最後まで変えない。 カレンダーは少しざらついた生成り色の厚紙。全ページで書体、文字サイズ、日付位置、曜日位置、余白を完全に統一する。 今回存在するページは次の6枚だけ。 1枚目：「2026年8月 13 木」 2枚目：「2026年8月 14 金」 3枚目：「2026年8月 15 土」 4枚目：「2026年8月 16 日」 5枚目：「2026年8月 17 月」 6枚目：「2026年8月 18 火」 必ず、 「13 木」→「14 金」→「15 土」→「16 日」→「17 月」→「18 火」 の順番で一枚ずつ進める。 日付を飛ばさない。順番を変えない。逆戻りしない。同じ日付を二度表示しない。存在しない日付を追加しない。数字を別の数字へ変形させない。 各日付は、それぞれ別の紙の表面へ最初から印刷されている。日付は物理的なページめくりによってのみ切り替わる。 紙の裏面は、文字も絵も印刷されていない完全な生成り色の無地。めくられている紙の裏側へ、日付、曜日、数字、絵、鏡文字、反転文字を表示しない。 一度に読める日付は必ず一つだけ。次の日付は、上の紙が完全にめくられた後で現れる。途中の日付や余分なページを生成しない。 各ページ上部の左側に小さく「2026年8月」、中央に大きな日付数字、右側に曜日を一文字だけ表示する。「土」は青、「日」は赤、それ以外は濃いチャコールグレー。 日付以外の文章、タイトル、ロゴ、透かし、字幕、無関係な文字は一切表示しない。 各ページ下部には、柔らかな水彩と色鉛筆による日本の絵本風イラストが描かれている。 主人公は一匹の小さな白猫。丸い顔、小さな三角耳、黒い丸い瞳、小さな桃色の鼻、短い手足、ふっくらした尻尾を持つ。首輪、スカーフ、リボン、服、バッグなどの装飾品は何も身に着けていない。 全ページで白猫の顔、体形、耳、瞳、鼻、足、尻尾、大きさを完全に統一する。同じ一匹の白猫として維持する。 登場する動物は白猫と金魚だけ。星の子、蛍、妖精、発光する生物、不思議な物体は出現させない。 水彩絵本の配色は、夏空の青、ひまわりの黄色、葉の緑、夕焼けの桃色、提灯の赤、生成り色。輪郭は柔らかな茶色の色鉛筆。可愛いが幼児向けに単純化しすぎない、丁寧で温かく、少し懐かしい日本の絵本イラスト。 各ページには一つの明確な行動だけを描く。複数の出来事を同じページへ詰め込まない。白猫が何をしているか、一目で理解できる構図にする。 [0.00–2.50 seconds] 最初のページ「2026年8月 13 木」を2.5秒間、完全に明瞭な状態で表示する。まだページを動かさない。 ページ下部では、白猫が大きなひまわりの陰で丸くなり、気持ちよさそうに昼寝している。 ひまわりの葉が涼しい日陰を作っている。白猫の胸が呼吸でごくわずかに上下し、片耳が一度だけ小さく動く。ほかの行動はさせない。 [2.50–4.80 seconds] 一枚目を下端から上へゆっくりめくる。厚い紙が自然に反り、机へ柔らかな影を落とし、金属リングを通過して裏側へ着地する。紙の裏面は完全な無地。 紙が完全にめくられた後、「2026年8月 14 金」を表示する。 ページ下部では、白猫が涼しい縁側に座り、目の前に置かれた一切れの赤いスイカを興味深そうに見つめている。 白猫はスイカを食べない。前足で触らない。首を少し傾け、スイカの匂いを一度だけ嗅ぐ。背景には青空と入道雲。 [4.80–6.80 seconds] 二枚目を同じ方向へめくり、「2026年8月 15 土」を表示する。「土」は青。めくられた紙の裏面は完全な無地。 ページ下部では突然の夕立。白猫が大きな緑色の里芋の葉の下で小さく丸まり、雨宿りしている。 大きな葉が猫の屋根になっている。葉の縁から水滴が落ち、足元の水たまりへ丸い波紋が広がる。白猫は雨を見つめ、前足を身体の下へしまっている。 傘、衣服、人間の手は出さない。猫に葉を持たせない。白猫は葉の下へ座って雨をしのぐだけ。 [6.80–8.60 seconds] 三枚目を少し速くめくり、「2026年8月 16 日」を表示する。「日」は赤。紙の裏面は完全な無地。 雨上がり。白猫が水たまりの縁へ座り、水面に映った大きな虹を不思議そうに見つめている。 白猫が片方の前足で水面を一度だけ軽く触る。小さな波紋が広がり、虹の反射が優しく揺れる。白猫は水へ飛び込まない。 [8.60–10.20 seconds] 四枚目を軽快にめくり、「2026年8月 17 月」を表示する。紙の裏面は完全な無地。 夕暮れの夏祭り。白猫が透明な丸い金魚鉢の前へ座り、中を泳ぐ一匹の赤い金魚と見つめ合っている。 白猫の顔と金魚鉢を横から見た、分かりやすい構図。白猫が首をゆっくり右へ傾けると、金魚も同じ方向へ泳ぐ。 背景には赤い提灯と屋台の柔らかな光。人間は足元のシルエットだけにし、人間の顔を描かない。白猫は金魚へ前足を入れず、金魚を捕まえようとしない。 [10.20–11.70 seconds] 五枚目をめくり、最後のページ「2026年8月 18 火」を表示する。紙の裏面は完全な無地。 これ以降、絶対にページをめくらない。19日以降のページを表示しない。最後のページを交換しない。 夏祭りの夜。白猫が縁側に後ろ向きで座り、夜空いっぱいに広がる青、金、桃色の花火を見上げている。 最初の花火が開いた瞬間、白猫が少し驚いて両耳をまっすぐ立てる。その後、安心したように尻尾を身体の横へ置き、静かに花火を見上げる。 [Shot 2] At .700, 最終ページ「2026年8月 18 火」を完全に固定する。日付、曜日、紙、金属リングを動かさない。数字の「18」と曜日の「火」を最後まで変化させない。 ページ内の夜空と花火だけが繊細に動き続ける。金色の花火から生まれた小さな光粒が、紙の表面を越えて現実の机の上へ少しだけこぼれる。 光粒が青い風鈴の表面へ反射する。窓辺の風鈴が夏風で一度だけ揺れる。白猫の耳と尻尾がわずかに動く。 最後に、夜空の中央で大きな金色の花火が丸く開く。猫や文字の形にはしない。自然で美しい円形の花火にする。 At exactly 15.00 seconds, 「2026年8月 18 火」が完全に明瞭な状態で残る。白猫が縁側に座り、夏祭りの花火を静かに見上げている。 overall_soundscape: 日本の夏を感じるネイティブステレオ音声。開いた窓から聞こえる蝉、穏やかな夏風、遠くの鳥、木造家屋の静かな環境音から始める。 ページをめくるたびに、厚い紙が持ち上がり、反り、金属リングを越えて着地する柔らかな紙音を鳴らす。 最初の二枚は長くゆっくりした紙音。中盤から少しずつ短くする。ただし、各ページが完全に着地する音を明確に残す。 13日は蝉、葉の擦れる音、白猫の小さな寝息。 14日は穏やかな風、遠くの風鈴、白猫が匂いを嗅ぐ小さな鼻息。 15日は柔らかな夕立、葉へ当たる雨、水たまりへ落ちる水滴。 16日は雨上がりの鳥、水面の小さな波紋。 17日は遠い祭囃子、人々の控えめな賑わい、下駄、金魚鉢の小さな水音。 18日は遠くの花火、その少し遅れて届く柔らかな反響、窓辺の風鈴が一度だけ鳴る音。 猫の鳴き声、会話、ナレーション、歌声は入れない。 non_diegetic_music: 約94 BPMの温かく懐かしい夏のインストゥルメンタル。フェルトピアノ、グロッケン、ピチカート弦、柔らかなアコースティックギター、控えめな篠笛、軽いブラシパーカッションを使用する。 0.00秒から4.80秒までは音数を少なくし、白猫の穏やかな夏時間とゆっくりしたページめくりを見せる。 4.80秒から8.60秒はピチカートと軽いリズムを加える。夕立では音数を減らし、雨上がりの虹でグロッケンの明るい旋律を入れる。 8.60秒以降は祭りへ向かう温かな期待感を加える。最終ページではリズムを弱め、花火、風鈴、グロッケン、ピアノの余韻を中心にする。 歌詞、歌声、既存楽曲に似た旋律は使用しない。
```

</details>

<sub>Source: <a href="https://x.com/renataro9/status/2089573433806098785">https://x.com/renataro9/status/2089573433806098785</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 24 · A Cat-Eared Chef Finishes a Plate of Fried Rice

<sub>AI Bard Guild &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 480×800 &nbsp;·&nbsp; portrait</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2096577196915900712.jpg" alt="A Cat-Eared Chef Finishes a Plate of Fried Rice" width="100%">](https://x.com/IsekaiBardGuild/status/2096577196915900712)

<sub><b>▶ <a href="https://x.com/IsekaiBardGuild/status/2096577196915900712">Watch the clip on the creator's post on X (@AI Bard Guild)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A blue-haired cat-eared chef stir-fries rice in a Chinese restaurant, works through flame and exertion, plates the dish, and serves it to a customer. Native-video output: 15s · 480×800. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (3,019 characters)</summary>

```text
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] High-quality Japanese anime style, 2D illustration with cel-shading. (S1) is a character showen in the <Picture 1>. The camera cuts to a medium shot of the same character (S1), maintaining (S1)'s  exact appearance and outfit from <Picture 1>, now standing in a vibrant Chinese restaurant kitchen. (S1) is positioned before a large wok on a powerful burner, surrounded by rising steam, hanging menu boards with illegible characters, and warm red and gold lighting. S1 begins to cook fried rice with focused, energetic movements. [Shot 2] At 00:04.500, the camera cuts to a series of rapid, cinematic close-ups. First, a tight shot of S1's determined eyes, then a shot of (S1)'s  hands skillfully tossing the wok. The camera pushes in with small amplitude at fast speed as (S1) exerts force to flip the rice, causing a few grains to dance in the air. A sudden burst of orange flame from the burner illuminates (S1)'s  face. Tiny beads of sweat form on (S1)'s  cheeks; (S1) briefly wipes (S1)'s  brow with (S1)'s  forearm without stopping (S1)'s  rhythmic stirring. [Shot 3] From 00:10.500 to 00:13.000, show the complete transfer of fried rice FROM THE WOK INTO AN EMPTY CERAMIC PLATE in one uninterrupted close medium shot. Both the wok and the empty plate must be clearly visible together. S1 holds the wok above the plate, visibly tilts its rim down toward the plate, and uses the spatula to slide and scrape the cooked fried rice out of the wok. Show the rice physically falling from the rim of the wok and accumulating into a mound on the plate. The plate starts empty and becomes filled on camera. Do not cut away, skip this action, or show an already-filled plate in its place. Only AFTER the rice has been transferred completely, from 00:13.000 to 00:15.000, S1 sets the wok down, lifts the filled plate, moves to the counter, and extends it toward a customer. The camera pans right with small amplitude at slow speed to follow the serving action. S1's expression shifts from intense concentration to a sincere, tired but happy smile, (S1)'s  chest heaving slightly from the effort. The customer's hand enters the frame to accept the plate. S1 gives a small, proud nod of satisfaction, (S1)'s  eyes shimmering with relief and accomplishment under the warm glow of the kitchen lights.

overall_soundscape: The environment is filled with the rhythmic, metallic clanking of a spatula against a wok. Constant sizzling of rice and oil blends with the sudden, low-frequency "whoosh" of the burner's flames. The soft hiss of rising steam and the final, clean "clink" of a ceramic plate being placed on a wooden counter complete the atmosphere.

non_diegetic_music: An upbeat, heartwarming orchestral track with a fast tempo, featuring playful pizzicato strings and a bright flute melody that swells emotionally toward the end to emphasize a sense of accomplishment.
```

</details>

<sub>Source: <a href="https://x.com/IsekaiBardGuild/status/2096577196915900712">https://x.com/IsekaiBardGuild/status/2096577196915900712</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 25 · Rainy Bar Continuous-Tracking Comparison

<sub>FoldingEnd A.I. &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1376x768 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-endfolding-rainy-bar-comparison.jpg" alt="Rainy Bar Continuous-Tracking Comparison" width="100%">](https://x.com/EndFolding79421/status/2086584639091536239)

<sub><b>▶ <a href="https://x.com/EndFolding79421/status/2086584639091536239">Watch the clip on the creator's post on X (@FoldingEnd A.I.)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The same rainy-street concept is tested with Seedance 2.5 and ComfyUI MiniMax H3. The H3 version outputs a 15-second, 1376×768 continuous tracking shot with timed constraints for moving from a frontal approach to a rear follow. The post publishes both complete prompts.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (2,732 characters)</summary>

```text
<image 2>: location

<image 1>: Chris character reference 

integrated_multimodal_description:
Cinematic rain-slicked urban evening with deep teal shadows, warm amber highlights, wet asphalt, shallow puddles, and light mist in the air. ONE continuous shot with NO CUTS. There is only ONE Chris in the entire video. Chris must remain the SAME woman with the SAME face, hair, clothing, body, and appearance throughout the entire shot. Never duplicate Chris, never create a second version of her, and never have her disappear and re-enter.

[0s–4s] Medium tracking shot. Chris walks directly toward the camera along the wet street, looking toward the camera for approximately two beats. The camera smoothly tracks backward in front of her, keeping her face clearly visible and framed at medium distance. Warm amber streetlights reflect across the wet pavement behind her.

[4s–7s] Chris reaches the camera and naturally walks very close past the LEFT side of the camera. IMPORTANT CONTINUITY: the camera does NOT cut away and Chris does NOT leave the continuous action. As her body passes beside the lens, the camera immediately pivots left and rotates approximately 180 degrees with her movement, continuously tracking the SAME Chris as the viewpoint transitions naturally from facing her to following directly behind her.

[7s–15s] The camera finishes the pivot behind Chris and continues following the SAME woman from a medium rear tracking position. Ahead of her is the wet urban street and the Blackwood Bar and Grill storefront. Chris steps off the curb and crosses the street, moving carefully between parked cars with deliberate natural steps. She continues directly toward the Blackwood Bar and Grill. Its cool-white illuminated sign reads "Blackwood Bar and Grill" above dark wood-framed windows, creating a soft glow through the mist. Warm amber streetlights backlight Chris and produce long reflections across shallow puddles.

Camera behavior: one uninterrupted continuous tracking shot; no edits, no cuts, no teleportation, no character substitution. Natural handheld cinematography with subtle realistic movement and mild walking shake. During the crossover, maintain continuous visual tracking of Chris's physical movement past the camera so there is never an opportunity for a second Chris to appear. Keep Chris close enough to camera for stable character and facial consistency during the opening approach.

overall_soundscape:
Natural rainy urban evening ambience. Soft footsteps on wet pavement synchronized with Chris's movement, distant traffic hum, subtle tire noise on wet streets, occasional passing cars, faint environmental city sounds, and quiet atmospheric rain and water sounds.

non_diegetic_music:
None.
```

</details>

<sub>Source: <a href="https://x.com/EndFolding79421/status/2086584639091536239">https://x.com/EndFolding79421/status/2086584639091536239</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 26 · Dancing Across the Magical Islands of Malta

<sub>Syed Abuthahir ∞ &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2085793101600428386.jpg" alt="Dancing Across the Magical Islands of Malta" width="100%">](https://x.com/abulu8/status/2085793101600428386)

<sub><b>▶ <a href="https://x.com/abulu8/status/2085793101600428386">Watch the clip on the creator's post on X (@Syed Abuthahir ∞)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for dancing across the magical islands of malta on X. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,592 characters)</summary>

```text
{
  "format": { "duration": "15s", "bpm": 92, "total_shots": 10, "sync_type": "Dance to Playback Song — No Lip-Sync" },
  "style_reference": "Warm Mediterranean daylight, 35mm, fine organic grain, gentle bloom. Honey-gold limestone against deep cobalt sea and white sky. Saturated embroidery popping against neutral stone. Shallow depth on close work, crisp wides, natural sun flare. Never cold or desaturated.",
  "subject": {
    "description": "A young Mexican woman, mid-twenties, long dark wavy hair loose and moving, warm brown skin, serene expressive face, small gold earrings. Traditional Chiapaneco dress — deep-toned fabric densely embroidered with large multicolored floral bursts in magenta, gold, turquoise and crimson, wide flowing skirt, sheer embroidered overlay that catches air. Bare feet.",
    "consistency_note": "The dress is the co-star — keep embroidery pattern, colors and skirt volume consistent. Fabric behavior matters as much as her body. Keep her face large in close work to avoid drift."
  },
  "environment": {
    "setting": "Malta in bright daylight — honey limestone architecture, a sunlit stone terrace above the sea, narrow old-town steps.",
    "background": "Limestone walls and arches, traditional Maltese wooden balconies, worn steps, bougainvillea, the deep blue Mediterranean to the horizon.",
    "lighting": "Hard Mediterranean afternoon sun, crisp shadows across stone, warm limestone bounce filling her face, occasional flare, glittering sea behind."
  },
  "mood": "graceful, elegant, joyful, free, radiant, flowing",
  "music": {
    "genre": "Warm Latin folk-pop ballad, 92 BPM, acoustic and organic.",
    "instrumentation": "Nylon-string guitar arpeggios, soft cajón and hand percussion, warm upright bass, distant accordion, light strings on the big moments, rich female vocal on top.",
    "arrangement": "Shots 1-2: guitar and voice alone, sparse. Shots 3-5: percussion enters, groove opens. Shot 6: strips to a single held guitar note. Shot 7: full arrangement blooms with strings. Shots 8-9: percussion punches back, then softens. Shot 10: resolves warm on guitar and a sustained vocal note.",
    "language": "Spanish",
    "lyrics": "Que baile el sol sobre la piedra dorada / que el viento me lleve donde nadie me llama / Mi falda florece, la mar me responde / Aquí soy de nadie, aquí soy del aire / Vuelo, vuelo, vuelo — y nunca me caigo",
    "mix": "Warm, natural, acoustic-forward. Vocal present but not overpowering. Round percussion. Sun-soaked."
  },
  "style": "Ultra-Realistic",
  "logic_rule": "The song plays audibly IN the clip while she dances to it. She does NOT sing and does NOT lip-sync — mouth relaxed and natural, expression serene and absorbed, occasionally a soft smile. THE BODY LEADS: each shot built around one quality of motion — stretch, spin, suspended pause, weightlessness, impact, inner rhythm. Movement is GRACEFUL and ELEGANT: long extended lines, controlled turns, soft shaped arms, fluid transitions, classical poise with folkloric footwork — never frantic. Vary camera to serve movement: low angles for elevation, tracking for travel, macro for fabric and feet, wide for full body against architecture. Mandatory SPEED CHANGE: extreme slow motion at the leap's apex so skirt bloom, hair suspension and embroidery are fully legible, then snap back on landing. Fabric physics essential — the skirt must swing, flare, ripple and settle with real weight. Effects: dust off stone, hair whipping, shadow raking walls, sun flare. ENDING: hold on a still breathing frame, then slow fade.",
  "storyboard": [
    { "shot": 1, "camera": "Low wide, sun behind her, limestone wall behind.", "action": "THE STRETCH — she rises onto the balls of her bare feet, extending both arms overhead in a long elegant line, spine lengthening, sleeve falling back. Eyes closed, serene.", "sfx": "Wind, gulls, fabric settling; guitar and voice alone." },
    { "shot": 2, "camera": "Macro on her bare feet on warm stone, shallow focus.", "action": "THE RHYTHM UNDER THE SKIN — heel and toe begin a soft precise pattern, dust lifting with each strike, ankles articulate and controlled.", "sfx": "Delicate foot taps, dust scuff; guitar continuing." },
    { "shot": 3, "camera": "Tracking alongside her down a narrow sunlit alley.", "action": "She travels in flowing rhythmic steps, skirt swinging gracefully side to side, one hand trailing the warm stone wall.", "sfx": "Footfalls, fabric swish, alley echo; percussion entering." },
    { "shot": 4, "camera": "Medium, camera orbiting with her turn.", "action": "THE SPIN — one controlled elegant rotation, the embroidered skirt opening into a wide circle of color, hair fanning, arms soft and shaped.", "sfx": "Fabric whoosh, foot pivot; groove opening." },
    { "shot": 5, "camera": "Close-up on her face, sun raking across it.", "action": "Eyes closed, head tilted back, absorbed with the faintest smile — lost in the music. Mouth relaxed and closed, NOT singing.", "sfx": "Breath, wind; vocal carrying over." },
    { "shot": 6, "camera": "Wide low angle on the terrace, sea behind.", "action": "THE PAUSE — everything stills. She sinks into a deep controlled coil, weight low, skirt pooling, held one suspended beat.", "sfx": "Music strips to one held guitar note; a deep breath." },
    { "shot": 7, "camera": "EXTREME SLOW MOTION, low angle, sky and sea behind.", "action": "THE WEIGHTLESSNESS — she launches upward, body arced in an extended line, arms open, skirt blooming outward like a flower, hair suspended, every stitch legible against the blue.", "sfx": "Stretched fabric bloom, deep swell; full arrangement with strings." },
    { "shot": 8, "camera": "Snap to full speed. Low, close on her landing.", "action": "THE LANDING — she meets the stone softly, knees absorbing, skirt collapsing around her legs, dust puffing, hair falling forward.", "sfx": "Foot impact, fabric slap, exhale; percussion punching back." },
    { "shot": 9, "camera": "Macro on the embroidery settling, rack up to her chest.", "action": "The floral stitching ripples and stills; her chest rises and falls, a bead of sweat at her collarbone. The body after force.", "sfx": "Breathing, fabric settling, sea; arrangement softening." },
    { "shot": 10, "camera": "Slow pull-back to a wide — small against limestone and sea. Held.", "action": "She lifts her head, sweeps her hair back and settles into a final open-armed shape against the Mediterranean light, breathing, a slow warm smile. Hold, then slow fade.", "sfx": "Wind, gulls, sea; guitar and sustained vocal resolving." }
  ]
}
```

</details>

<sub>Source: <a href="https://x.com/abulu8/status/2085793101600428386">https://x.com/abulu8/status/2085793101600428386</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 27 · Eight Lyric Frames Become a K-Pop Performance

<sub>Larus Canus &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2085272318649987242.jpg" alt="Eight Lyric Frames Become a K-Pop Performance" width="100%">](https://x.com/MrLarus/status/2085272318649987242)

<sub><b>▶ <a href="https://x.com/MrLarus/status/2085272318649987242">Watch the clip on the creator's post on X (@Larus Canus)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for eight lyric frames become a k-pop performance on X. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (7,710 characters)</summary>

```text
② MiniMax H3 prompt

Create a photoreal 15-second K-pop lyric MV using Audio 1 and the eight reference images in upload order.

Keep the same Korean idol recognizable across every shot. Use Image 3 as the main facial anchor. She sings throughout with clear lip-sync and performs confident K-pop movement with turns, footwork, hip motion, arm lines, and camera-aware expressions.

The on-screen lyric text must animate in every shot, with clear motion design synced to the beat and the meaning of each line.

Cut once per lyric line:

1. Glitter on my waist — waist movement, sparkling type reveal
2. Give you just a taste — move toward camera, sliding type
3. Never be replaced — sharp hit pose, punch-scale type
4. Running through the space — run through the chrome corridor, motion-blur type
5. I’m feeling so gold — full spin in gold light, pulsing type
6. Stories to be told — walk-dance beside the rain window, drifting type
7. Baby watch the glow — moving beauty close-up, luminous type bloom
8. Welcome to the show — open-arm stage finale, billboard type zoom

Only display the lyric text shown in the reference images. Keep every line readable and correctly spelled.

1 · Glitter on my waist  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips. Honey-ash brown soft waves, middle part. Cream champagne satin crop bustier fully covered stylish, ice-blue sparkle mini skirt, crystal jewelry, nude heels. Fashion-sexy premium K-pop, dewy K-beauty. Medium shot emphasizing waist sparkle and glitter body shimmer, hand near hip, crystal studio set with floating glitter particles and chrome reflections, magenta cyan rim. Large bold white readable typography in frame exactly: Glitter on my waist. High-impact K-pop lyric MV still, photoreal cinematic 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

2 · Give you just a taste  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips. Honey-ash brown soft waves, middle part. Cream champagne satin crop bustier fully covered stylish, ice-blue sparkle mini skirt, crystal jewelry, nude heels. Fashion-sexy premium K-pop, dewy K-beauty. Intimate medium waist-up, soft teasing girl-crush eye contact, one hand near collarbone, velvet lounge corner with warm pink practical lights, shallow depth. Large bold white readable typography exactly: Give you just a taste. Photoreal K-pop MV still 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

3 · Never be replaced  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips. Honey-ash brown soft waves, middle part. Cream champagne satin crop bustier fully covered stylish, ice-blue sparkle mini skirt, crystal jewelry, nude heels. Fashion-sexy premium K-pop, dewy K-beauty. Confident full or three-quarter plant stance, strong eye contact, fashion power. Mirror black stage with vertical glass panels, not empty void only. Giant typography wall behind her reading exactly: Never be replaced. Photoreal cinematic 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

4 · Running through the space  
Keep the SAME Korean woman about 22 as the reference image: same facial identity. Black hair with vivid pink peekaboo underlights, high ponytail. Metallic silver tube crop top fully covered, black mini skirt, chunky silver belt, black platform boots. Y2K flashy K-pop fashion-sexy not vulgar. Mid-run motion inside endless chrome mirror corridor, pink hair tips flying, reflections. Semi-transparent or wall typography readable exactly: Running through the space. Kinetic K-pop MV still, photoreal 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

5 · I'm feeling so gold  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips. Honey-ash brown soft waves, middle part. Cream champagne satin crop bustier fully covered stylish, ice-blue sparkle mini skirt, crystal jewelry, nude heels. Fashion-sexy premium K-pop, dewy K-beauty. Power medium pose, warm golden gel lighting shift, gold glitter dust in air, gold-chrome corridor or gold-lit stage (not cold cyan only). Large bold typography readable exactly: I'm feeling so gold. Photoreal cinematic 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

6 · Stories to be told  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips. Honey-ash brown soft waves, middle part. Cream champagne satin crop bustier fully covered stylish, ice-blue sparkle mini skirt, crystal jewelry, nude heels. Fashion-sexy premium K-pop, dewy K-beauty. Profile or three-quarter storytelling pose near rain-streaked night glass window, soft city bokeh, cooler blue mood bridge scene, elegant modest fashion. Readable typography in frame exactly: Stories to be told. Photoreal 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

7 · Baby watch the glow  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips. Honey-ash brown soft waves, middle part. Cream champagne satin crop bustier fully covered stylish, ice-blue sparkle mini skirt, crystal jewelry, nude heels. Fashion-sexy premium K-pop, dewy K-beauty. Beauty close-up face and shoulders, strong glow rim light and lens flare, catchlights, dewy skin, dark stage with single luminous glow behind. Readable typography exactly: Baby watch the glow. Photoreal 16:9. Avoid different face, older look, explicit vulgar, extra fingers, gibberish unreadable letters, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD, ONE MORE TIME text, watermark, low-res, corporate black suit, childish loli

8 · Welcome to the show  
Keep the SAME Korean woman about 22 as the reference image: same facial identity, same eyes nose lips jaw. Ultra sharp photoreal face, tack-sharp eyes and eyelashes, clear skin micro-detail, no soft blur, no motion blur, no low-res mush. High sleek ponytail with balayage tips. White cropped bomber open over black crop top, black mini skirt, power street idol look. MEDIUM shot waist-up to mid-thigh, subject fills frame, confident show-entrance pose facing camera, open energy. Concert stage entrance with LED pillars and soft haze BEHIND her, shallow depth of field with face in perfect focus, background slightly softer. Huge billboard typography readable exactly: Welcome to the show. Cinematic 16:9, premium K-pop MV still, high detail. Avoid different face, soft focus on face, blurry face, plastic skin, extra fingers, gibberish text, wrong lyrics, DONT BLINK, MIDNIGHT RUN, MAKE IT LOUD text, watermark, low-res, explicit vulgar.
```

</details>

<sub>Source: <a href="https://x.com/MrLarus/status/2085272318649987242">https://x.com/MrLarus/status/2085272318649987242</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 28 · Cairn Munro Arrives in Motion Type

<sub>Dheepan Ratnam &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2084201268977844521.jpg" alt="Cairn Munro Arrives in Motion Type" width="100%">](https://x.com/Dheepanratnam/status/2084201268977844521)

<sub><b>▶ <a href="https://x.com/Dheepanratnam/status/2084201268977844521">Watch the clip on the creator's post on X (@Dheepan Ratnam)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for cairn munro arrives in motion type on X. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,511 characters)</summary>

```text
CAIRN MUNRO — "ARRIVE UNHEARD" — 14 CUTS · 15s · 2K · 24fps  REFERENCES: the attached PRODUCT SHEET@Image1 is the exact vehicle — match its proportion, stance, glasshouse angle, cladding, rack and light signature exactly, invent nothing. The attached TYPE SHEET@Image2 is the exact typeface, weight, tracking and scale for every overlay. Match it.  AUDIO LAW — HIGHEST PRIORITY. NO MUSIC ANYWHERE. Do not generate score, soundtrack, background music, beat, drums, percussion, bassline, synth pad, drone, melody, chord, ambient bed, riser, braam, trailer hit, stinger, swell, or any tonal instrument. Where music would normally be scored, render SILENCE. NO VOICE — no narration, dialogue, vocals, breath. ONLY PERMITTED AUDIO, all of it environmental: rain striking wet granite; rain drumming on metal and glass; wind over ridge grass; a burn running hard over rock; gravel shifting; distant thunder; and true silence. All of it recorded-real, close, dry, no reverb wash. Nothing sustains musically.  SILENCE LAW — the engine of the film. The landscape is loud. The vehicle adds nothing to it. No engine, no exhaust, no motor whine, no transmission, no tyre roar, no wind noise off the body, no door, no suspension. Rain striking its panels is permitted — that is the world touching the car, not the car making sound. Whenever the vehicle fills frame and nothing is striking it, the mix drops to near-silence. If an engine or tyre sound would normally be added to a moving vehicle, render silence instead. An engine sound anywhere in this film is a failure.  EDIT METRONOME — SILENT: cuts locked to 96 BPM, 1 beat = 0.625s, 24 beats. A timing grid for cutting ONLY. Do not generate audio to this tempo.  BRAND: CAIRN. PRODUCT: CAIRN MUNRO, a fully electric expedition overlander. It is silent because it is electric — the claim is literal.  SUBJECT: per the sheet — boxy full-size SUV, upright glasshouse, flat vertical sides, squared arches, short overhangs, high clearance. Matte peat green-black body, charcoal composite cladding and sliders, raw anodised aluminium rack and skid plate, bone-white roof, signal-orange recovery hooks, full-width thin white LED signature front and rear, no grille, all-terrain tyres on flat-faced aluminium wheels. No badging.  WORLD: the Scottish Highlands in heavy weather. Wet granite, peat, ridge grass and heather. Low cloud moving fast across the tops. Constant rain. A single unmade stone track. No road markings, no buildings, no fences.  PALETTE: peat #1B2320, granite #4A4E4B, mist #D9DDDB, aluminium #8E9490, heather #6B5470. Signal orange #E24E1B on the recovery hooks only, never more than a few pixels. Cold northern light, overcast, no sun, no warmth anywhere. Desaturated but never graded grey — these are true wet colours.  MIST LAW: mist is real volume. It moves, thins, and parts to reveal. It never becomes a soft filter — everything outside the mist stays razor sharp. It never glows, never catches a god ray, never becomes smoke.  TYPE LAW: every overlay uses the TYPE SHEET face, CAIRN EXTENDED — wide uppercase, medium weight, wide tracking, pure white, with the hairline contour rule beneath each line. Two positions only: body lines lower-left on the safe-area grid, the lockup dead centre. Type is revealed by a hard-edged horizontal wipe travelling left to right. It never fades, scales, rotates, skews, glows or casts a shadow. It cuts on with the cut and holds absolutely still until the next cut takes it. Always pure white.  TEXT ACCURACY: every overlay word is spelled exactly as written and appears exactly once. No extra letters, no duplicated lines, no garbled glyphs, no invented words. No text of any kind on the vehicle.  CAMERA: motion-control smooth and heavy, no handheld, no drift. Long-lens tracking and slow cranes. Clean digital, no grain. Directional blur in transit; everything arrives sharp and holds still.  RHYTHM: cuts 01–02 hold two beats. Cuts 03–10 are one beat apart, the spec run. Cuts 11–12 hold two beats. Cuts 13 and 14 hold four beats each.  01 · 0.000 · Wide. A granite ridge under fast-moving low cloud, rain falling hard across frame. No vehicle. SOUND: rain on stone and wind, loud.  02 · 1.250 · Macro. Rain hammering a wet granite face, water sheeting down the fractures. TYPE: EVERYTHING HERE  03 · 2.500 · A burn crashing white over black rock. TYPE: MAKES A SOUND  04 · 3.125 · Wind flattening ridge grass and heather in one long gust.  05 · 3.750 · The vehicle enters, low and wide, emerging from mist on the stone track. The mix drops away to rain only. TYPE: ONE THING DOESN'T  06 · 4.375 · Macro. A tyre rolling through standing water, the water throwing up hard. SOUND: water only, no tyre noise. TYPE: 800 VOLT  07 · 5.000 · Macro. Rain drumming on the bone-white roof panel. TYPE: 710 KM  08 · 5.625 · Macro. Water running off the anodised aluminium rack. TYPE: 900 NM  09 · 6.250 · Low long-lens track alongside the flat body side, mist parting off the panel. TYPE: 1050MM WADING  10 · 6.875 · Macro. The thin white LED signature cutting through mist. TYPE: 3.5T TOWING  11 · 7.500 · High wide. The vehicle small on a vast stone plateau, cloud dragging over it. SOUND: wind, distant thunder.  12 · 8.750 · Front three-quarter, wading a burn, water pushing up over the sills and breaking white. SOUND: water only.  13 · 10.000 · THE SHOT. A single mature red deer stag stands side-on on the ridge above the track, wet coat, broad antlers, head turned to camera. The vehicle passes below him in the same frame. The stag does not flinch, does not run, does not move at all. Hold on him. SOUND: rain and wind only — no vehicle sound whatsoever.  14 · 12.500 · The vehicle static on the ridge in moving mist, dead frontal. TYPE: CAIRN, dead centre. Two beats later MUNRO wipes on beneath it, then ARRIVE UNHEARD. beneath that. Hold, cut to black. SOUND: rain and wind, then hard silence on the cut. No end cue, no final hit.  NEGATIVE: no music, score, beat, instruments, narration, voice, engine noise, tyre noise. No people, hands, faces, drivers, passengers. No other vehicles, no roads, no road markings, no signage, no buildings, no fences, no power lines. No text other than the specified overlays — no captions, subtitles, watermarks, UI, timecode. No badging or lettering on the vehicle. No sun, no warm light, no golden hour, no lens flare, no god rays, no smoke, no snow. No glitch, scanlines, film burn, light leaks. The stag never runs. No colour outside the palette. No invented body parts.
```

</details>

<sub>Source: <a href="https://x.com/Dheepanratnam/status/2084201268977844521">https://x.com/Dheepanratnam/status/2084201268977844521</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 29 · A Y2K K-Pop Girl-Group Rap Sequence

<sub>Leo &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2083240416166748313.jpg" alt="A Y2K K-Pop Girl-Group Rap Sequence" width="100%">](https://x.com/LeoCreaIA/status/2083240416166748313)

<sub><b>▶ <a href="https://x.com/LeoCreaIA/status/2083240416166748313">Watch the clip on the creator's post on X (@Leo)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for a y2k k-pop girl-group rap sequence on X. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (7,059 characters)</summary>

```text
This is what H3 does with Omni Reference and one long prompt:

prompt：Soft cute Y2K crush K-pop girl group rap MV. High fashion performance film mixed with inflated 3D candy typography graphic system. Three female idols wearing pink, blue and purple luxury Y2K stage outfits. Cute 3D chibi doll face, big dewy eyes, porcelain skin, soft blush cheeks, chibi idol proportions. Reference typography: only the inflated 3D rubber bubble font language, pink/lavender/ice-blue chrome plastic material, not the whole layout. Visual style: soft pastel crush energy, Y2K game UI, candy glossy finish, milky translucent plastic × K-pop aggressive feminine rap energy. Texture: 35mm film grain + soft glow bloom + iridescent holographic foil + jelly plastic specular + Y2K scanline + candy dot halftone + VHS frame vibration + plastic toy surface reflection + glitter confetti rain. Editing: Fast rhythm editing. Only hard cuts. No fade. No smooth transitions. Every cut follows: bass hit, snare, rap vocal impact.

Character Performance Three female performers from reference image 1. Keep: same 3D chibi doll faces, big sparkling eyes, pastel Y2K idol makeup, pink/blue/purple fashion styling, soft cute cold expression. Each member has a signature prop: A holds a chunky rhinestone microphone, B has a plush bear shoulder bag, C wears oversized heart-shaped sunglasses pushed up on head. They are not posing. They are performing rap. Actions: aggressive eye contact, head nodding, shoulder movement, leaning toward camera, hand pushing toward lens, confident cute facial expression, sharp body movement, wink on snare hit, tongue-out on bass drop, hair flip on beat. Lip sync: perfect rap mouth synchronization. The performance should feel like a real K-pop rap unit MV with Y2K crush energy.

Typography Animation Typography is a visual weapon. Not subtitles. Not static graphics. Use: giant English words inflated 3D rubber bubble font, jelly plastic material, pink lavender ice-blue chrome, soft puffy candy letters, compressed bold balloon fonts, stretched vertical puffy letters, handwritten graffiti titles, 3D extruded candy text, glitch displacement, print error effect, Y2K game UI pixel corruption. Text appears only when the beat hits. Characters can cover the text. Text can cover parts of clothing. Never cover eyes or main facial expression. Tiny Y2K stickers burst on beat: heart, star, smiley, sparkle, chain link, bow, four-leaf clover, mini bear.

Shot 1 — Member A · Extreme Close-up「RUN NOW」 Character A face close-up, framed inside a pink heart-shaped iris wipe transition (in only, hard cut out). She looks directly into camera. Cute cold doll expression, big dewy eyes, soft blush, frosted pink lip gloss, rhinestone tear sticker under one eye. Starts rap. Chunky rhinestone microphone enters frame from below, she grips it tightly. Camera slowly pushes closer. Tiny pink heart stickers float up from bottom edge like bubbles. Huge inflated bubble letters crash into frame from left and right. Typography: "RUN NOW" — Pink jelly rubber 3D font, glossy candy surface, soft inner glow. Letters stretch vertically like puffy balloons. The word vibrates and squishes with bass, casts soft pink shadow on her cheek. Rap: "Run now, I don't chase." Confetti burst on final syllable. Hard cut.

Shot 2 — Member B · Rap Performance「BREAK LIMIT」 Member B medium close-up, slight low angle, camera orbits 15° around her during the take. Lavender fur jacket, Y2K layered top, plush bear bag bouncing on her hip, chunky pearl choker, star-shaped earrings. She performs aggressively. Shoulders hit the rhythm. Hair flips hard on the second snare, blue hair ties catch the light. Hair moves naturally. Background: pastel gradient pink-to-lavender with faint Y2K perspective grid lines floating. Behind her appears huge handwritten text. Typography: "BREAK LIMIT" — Ice-blue bubble graffiti brush writing, soft inflated stroke, candy-coated, letters appear one by one with bounce easing. Animation: letters tear apart, reassemble, rotate 360° on snare, shake with bass. Chain link graphic swings across frame, sparkle stickers pop on every beat. Rap: "Break limits, break rules." Hard cut.

Shot 3 — Member C · Hand Attack Shot「NO APOLOGY」 Member C moves close to camera. Top-down camera angle, she leans over the lens. Hand reaches toward lens. Nails are long pink acrylic with 3D star and heart charms. Focus: rings with mini plush bear charm, heart-cut gemstone, baby-pink leather texture, knit ribbed sleeve, plushy toy surface. Foreground vertical text: "NO APOLOGY" — Stretched vertical pink bubble letters, jelly puffy material, letters pierce through the back of her hand visually. Hand covers part of the typography. Fingers spread wide on the bass hit. Camera: handheld vibration. Film grain strong. Candy halftone dots bloom in shadow. Tiny "XOXO" sticker tag pulses in corner. Rap: "No apology, no regret." Hard cut.

Shot 4 — Fashion Magazine Impact Cut「UNSTOPPABLE」 Member A close-up. Her face appears inside a broken Y2K trading card / idol photo card frame, with barcode at bottom, "SYS.07-A" serial tag, holographic foil border torn on left side. Not a full layout. Only one graphic element. Typography: "UNSTOPPABLE" — Huge lavender handwritten bubble text, inflated 3D rubber, glossy plastic finish, letters explode outward from center of her forehead, push edges of the card frame. Animation: text suddenly expands from behind her. Card frame rips in half vertically, holographic confetti pours from the tear, revealing pastel gradient background underneath. A second smaller photo card of her winks in from the right, slightly rotated. Rap: "Can't stop my wave." Hard cut.

Shot 5 — Glitch Double Image「STATIC」 Member B close-up, slight Dutch angle (5° tilt). Create: duplicate frame, pastel RGB separation (pink/blue/lavender channels), xerox shadow, motion trail, VHS tracking line at bottom edge. Main face stays sharp. She holds a sparkly heart-shaped lollipop up beside her cheek, the lollipop leaves a trail of echo frames. Background text: "STATIC" — Y2K pixel font, candy pink chrome, letters flicker like broken game sprite, jump between frames, sometimes inverted color, sometimes missing entirely. Like corrupted music video signal + cute game glitch. A tiny "ERROR 404" sticker blinks in upper corner. Rap: "Static noise, I get louder." Hard cut.

Shot 6 — Pink Blue Purple Battle「PINK OUT」 Member A and C alternate close-ups, rhythm: A-A-C-A-C-C, two frames each. Fast switching. Visual split: each member sits in a vertical color block (A=pink, C=lavender, alternating). Center text: "PINK OUT" — Pastel pink-to-purple gradient bubble 3D, letters appear one word at a time, syncing to each cut. Words appear one by one. Each word: stretch vertically on entry, compress horizontally on hold, invert color on snare, explode into heart stickers and star confetti on exit. Tiny "1.2.3.GO!" counter graphic ticks in corner. Rap: "Lights out, pink out." Hard cut.

Shot 7 — Group Rap Performance「UNBREAKABLE」 Three members together.
```

</details>

<sub>Source: <a href="https://x.com/LeoCreaIA/status/2083240416166748313">https://x.com/LeoCreaIA/status/2083240416166748313</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 30 · A Magical Apprentice and Her Rabbits in a Character PV

<sub>mayv@簡単プロ級プロンプト公開中！ &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2092387240664326495.jpg" alt="A Magical Apprentice and Her Rabbits in a Character PV" width="100%">](https://x.com/haruuraeadss/status/2092387240664326495)

<sub><b>▶ <a href="https://x.com/haruuraeadss/status/2092387240664326495">Watch the clip on the creator's post on X (@mayv@簡単プロ級プロンプト公開中！)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A pink-haired magical apprentice interacts with white rabbits in an academy courtyard as character close-ups, a spellbook, and cute typography shape a bright anime PV. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,019 characters)</summary>

```text
Create a 14.8-second bright, colorful premium anime game character PV with cute motion typography. 16:9, high-quality 2D anime look, dreamy, magical, elegant, warm and adorable. No external player UI, no watermark.  REFERENCE RULES @Image1 = FACE REFERENCE ONLY. Use @Image1 as the sole authority for face, eyes, facial proportions, bangs, hairstyle around the face, expression style and identity. @Image2 = OUTFIT / BODY DESIGN REFERENCE ONLY. Use @Image2 as the sole authority for clothing, cape, blouse, ribbon, brooch, belt, potion bottles, crystals, boots, accessories, silhouette, spellbook, colors and overall design. Keep exactly the same girl in every shot. Never redesign or simplify her.  CHARACTER A magical academy apprentice with long pink twin-tails, purple flower hair ornaments, luminous blue-violet eyes, purple hooded cape with gold trim, white frilled blouse, dark ribbon, crystal jewelry, potion bottles and crystals on her belt, and an ornate grimoire.  ENVIRONMENT A lush magical academy courtyard with old stone archways, green gardens, flowers and warm daylight. Several small white rabbits interact naturally with her: gathering around her feet, hopping, nuzzling her hands, chasing petals and reacting to magic. Magic is gentle and cute: floating petals, tiny stars, glowing particles, translucent purple-pink magic circles and soft book-based spell effects. No combat, no dark atmosphere.  MOTION TYPOGRAPHY Integrate clearly visible but elegant cute motion typography throughout the PV. Style: rounded or refined fantasy type, pastel pink, lavender, cream, white and subtle gold; small editorial captions, curved text, ribbon-like labels, flower/star motifs and playful floating words. Motion: soft pop-in, bloom, gentle slide, tiny bounce, arc rotation around magic circles, petal-like scatter and sparkle dissolve. Typography must remain secondary to the girl. Never cover her face. Avoid giant text, cyber HUD, glitch, industrial graphics, aggressive trailer typography or heavy sci-fi UI.  Use short phrases such as: “LILIA ASTRA” “STARFLOWER APPRENTICE” “LITTLE MAGIC” “RABBIT FRIENDS” “BLOOMING SPELL” “TWINKLE BLOOM” “GENTLE WONDER” “MAGIC IN BLOOM”  TIMELINE  0:00.0-0:00.5 Face close-up. Gentle smile and soft eye contact. Twin-tails move slightly in the breeze. “LILIA ASTRA” blooms into one corner with tiny flowers and stars.  0:00.5-0:01.0 Full-body courtyard shot. White rabbits gather around her boots. “RABBIT FRIENDS” appears beside them with a soft bounce.  0:01.0-0:01.5 Medium close-up. She opens the grimoire slightly and purple-pink particles spill from the pages. Curved “LITTLE MAGIC” follows the glow near the book.  0:01.5-0:02.0 Low rabbit shot. One rabbit hops after drifting petals. A tiny “hop!” briefly follows the movement.  0:02.0-0:02.5 She crouches and gently pets one rabbit. Warm framing. “GENTLE WONDER” slides softly into empty space.  0:02.5-0:03.0 Another rabbit comes close. She looks slightly surprised, then smiles. A tiny sparkle or “!” pops beside her.  0:03.0-0:03.5 Close shot of the grimoire. A translucent magic circle forms above it. “BLOOMING SPELL” curves around the circle and rotates gently.  0:03.5-0:04.0 Wide shot. Rabbits move around her in a loose circle. Her cape and twin-tails follow naturally. Small curved decorative text briefly traces their motion.  0:04.0-0:04.5 She closes the grimoire and hugs it to her chest. Petals and sparkles drift behind her. “STARFLOWER APPRENTICE” appears as an elegant character-title card.  0:04.5-0:05.0 Face close-up. She gives a happy smile. Tiny star and flower graphics bloom around the frame edges.  0:05.0-0:05.5 Rabbit close-up. One rabbit lifts its ears and makes a small hop. A tiny “twinkle!” dissolves into sparkles.  0:05.5-0:06.0 She stands gracefully and watches the rabbits. Keep the frame clean with only small decorative stars.  0:06.0-0:06.5 Medium-wide shot. Rabbits scatter left, right and toward foreground, creating depth. Add subtle lateral camera movement and petals crossing the lens.  0:06.5-0:07.0 She places one hand near her chest and turns into a cute elegant pose. “TWINKLE BLOOM” rises beside her with flower-shaped sparkles.  0:07.0-0:08.0 Pacing becomes calmer. She blinks slowly while one rabbit sits beside her boots. Hair, cape and petals continue gentle secondary motion. Minimal typography.  0:08.0-0:09.0 Petals drift slowly and the magic circle fades. Small “MAGIC IN BLOOM” appears faintly and dissolves into glowing dust.  0:09.0-0:10.0 Medium shot. She holds the grimoire to her chest while rabbits gather from both sides. Warm sunlight and shallow depth of field.  0:10.0-0:11.0 One rabbit jumps toward the foreground and stops near camera. The girl remains visible behind it. A tiny star/flower graphic reacts to the landing.  0:11.0-0:12.0 She looks toward the rabbit and gives a small affectionate smile. Keep the courtyard calm. No large typography.  0:12.0-0:13.0 Lingering atmospheric shot. Only hair, cape, petals, grass, rabbit ears and light particles move gently.  0:13.0-0:14.8 Return naturally toward the opening face close-up. She keeps the same gentle expression and slowly blinks. Final elegant title: “LILIA ASTRA” “STARFLOWER APPRENTICE” The title blooms softly with purple flowers, gold stars and sparkles, then settles into a calm loop-like ending.  EDITING First 7 seconds: lively 0.5-second character-PV cuts with clear shot variation: face close-up, full-body, medium, rabbit close-up, grimoire detail, wide and low-angle shots. After 7 seconds: gradually slow the rhythm for a gentle emotional finish. Use subtle push-ins, lateral movement, foreground rabbits and petals so the PV never feels static.  Maintain consistent face, costume, pink twin-tails, purple/gold academy clothing, ornate grimoire and readable rabbit anatomy. The final result should feel like a premium cute magical-academy character reveal PV combined with polished editorial motion typography, with the girl and rabbits always remaining the main focus.
```

</details>

<sub>Source: <a href="https://x.com/haruuraeadss/status/2092387240664326495">https://x.com/haruuraeadss/status/2092387240664326495</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 31 · Nine Character Looks Tear into a Game Promo

<sub>C’est La Vie | AI Director &nbsp;·&nbsp; Ref2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2093842404159947111.jpg" alt="Nine Character Looks Tear into a Game Promo" width="100%">](https://x.com/sailorv321/status/2093842404159947111)

<sub><b>▶ <a href="https://x.com/sailorv321/status/2093842404159947111">Watch the clip on the creator's post on X (@C’est La Vie | AI Director)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Black-and-red ripped paper, neon city graphics, HUD elements, and multiple character looks connect at speed into a game promo. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,996 characters)</summary>

```text
MODEL：MiniMax H3｜15秒｜16:9｜24fps
REFERENCE：[@参照1] ONLY
STRUCTURE：9 LOOKS / ONE CONTINUOUS GAME-PV EDIT / EACH LOOK USES A DIFFERENT AE MOTION LANGUAGE
STYLE：premium anime game PV × fashion editorial × aggressive After Effects motion design × mixed-media collage × cinematic 2.5D。参照1枚に含まれる9つの完成ビジュアルを「9個のLOOK候補」として読み取り、それぞれの人物外見・衣装・色彩・背景世界・構図の差を維持しながら、15秒の中で高速に連結する。各LOOKは同じテンプレート動作を繰り返さず、必ず異なるAEモーション原理で見せる。

REFERENCE INTERPRETATION / ABSOLUTE CLEANUP：
[@参照1]は9面をまとめたコンタクトシートだが、映像内にコンタクトシートそのものを表示しない。参照画像上の「01〜09」「LOOK 01〜09」「0.0–1.5s等の時間表記」「FINAL」およびパネル境界線は制作指示用メタ情報としてのみ認識し、生成映像には出さない。ナンバリング、タイムコード、LOOK表記、白い区切り線、3×3グリッドを画面へコピーしない。人物、衣装、髪、色調、背景、タイポの視覚要素だけを抽出。各LOOKはフルスクリーンで展開し、前LOOKの要素を次LOOKの転換素材へ変換する。

CHARACTER / LOOK LOCK：
参照内の黒髪系キャラクターと銀〜ラベンダー髪系キャラクターを同一作品世界の成人女性キャラクターとして扱う。各LOOKで参照に描かれた顔、目、髪型、髪色、衣装、アクセサリー、メイク、身体比率を尊重し、そのLOOKの途中で別人化させない。LOOKが切り替わる瞬間にのみ参照通りのヘア、衣装、カラー、背景へ変化可能。顔モーフ、二重顔、余分な腕、人物融合は禁止。視線、瞬き、僅かな首振り、呼吸、髪や布の二次動作のみ。走る、歩き続ける、ジャンプ、ダンス、格闘でテンポを作らない。速度はAE、カメラ、レイヤー、タイポ、マスク、都市、光、原画素材から作る。

GLOBAL MOTION RULE：
15秒を9LOOKへ分けるが静止画スライドショーにはしない。前LOOKが止まる前に次LOOKを0.12〜0.30秒先行させ、FAST BUT FLUIDで連結。各LOOKの主役AE TECHNIQUEは重複禁止。単純CUT、FADE、CROSS DISSOLVE、均等GRID、カードSLIDE、同じZOOM反復は禁止。完成KVとして一瞬読めても0.7秒以上静止させない。

TEXT CONTROL：
参照画像に含まれる番号、時間、LOOK、FINALなどの管理文字は全削除。主要タイポは「H3」「MiniMax」「Design」のみ。字幕として下部へ置かない。巨大前景、MASK、TRACK MATTE、3D奥行き、壁面印刷、光学的遮蔽物として使用。ランダム英数字、日本語、中国語、偽UI文字、架空ブランド、追加ロゴ、ウォーターマークは禁止。

0.0–1.55s｜LOOK A — RIPPED PAPER TRACK MATTE：
参照左上の黒髪・赤アクセント・眼差しの強い世界から開始。最初から顔の極端なEYE CU。BLACK / RED / WHITEの紙面が人物の輪郭と髪の方向に沿って有機的に裂ける。AEのRIPPED-PAPER TRACK MATTE＋ROUGHEN EDGES＋TURBULENT DISPLACEを主役にし、破断面は直線ではなく繊維質で不規則。裂けた下層から夜の都市が見え、都市は2.5Dで逆PARALLAX。裂け目が目の横を通過するたびに背景深度だけが変わる。最後は一本の赤い裂傷を画面奥まで伸ばし、その裂傷そのものを次LOOKへのCAMERA PATHにする。小さな紙屑を大量に飛ばさない。

1.55–3.10s｜LOOK B — TYPOGRAPHY DEPTH TUNNEL：
裂傷へカメラが飛び込み、紫〜黒の世界へ色相を急転換。銀〜ラベンダー髪の人物を低い奥行きレイヤーに固定し、巨大「H3」をAE 3D LAYERとして超前景へ配置。Hと3を同一平面に置かず、数メートル離れたZ位置として扱う。カメラは文字の内側・隙間・エッジを縫って高速FLY-THROUGH。文字面には人物の目や都市をTRACK MATTEで一瞬だけ流す。MOTION BLURは文字と背景に強く、顔には最小限。紫のLIGHT SWEEPが文字のエッジを走り、最後に3の曲線が画面全体を覆うMATCH OCCLUSIONとなって次へ。

3.10–4.70s｜LOOK C — NEON SIGN REBUILD / LIGHT TRACE：
遮蔽が外れると赤いネオン都市と黒髪キャラクター。ここでは紙裂けも巨大文字トンネルも主役にしない。AEのSABER系NEON TRACE、LIGHT STREAK、GLOW PATH、MASK PATH ANIMATIONを主役にする。都市看板、窓枠、人物の髪外周、サングラスやアクセサリーの輪郭を赤い光が高速走査。光が通過した場所だけ背景の都市が別角度へREBUILDされる。MiniMaxはネオン看板のように一瞬形成されるが、固定看板ではなく光の軌跡から0.2秒で組み上がり、次の光が通ると解体。最後は一本の赤い光がカメラレンズを横断し、LUMA WIPEとして次の青紫世界を露出。

4.70–6.20s｜LOOK D — 2.5D FLORAL PARALLAX / DEPTH ORBIT：
青紫の夜、花、銀髪キャラクターのLOOKへ。人物を切り抜いた複数カードにしない。人物本体は一人のまま固定し、花びら、前景花、髪の一部、都市、遠景光だけを別深度へ分離。AE 2.5D CAMERA＋DEPTH MAP＋PARALLAX ORBITを主役に、カメラが人物の周囲を僅かに弧を描きながら高速PUSH。前景花は大きく逆方向へ流れ、背景ビルは遅れて動く。MiniMaxは遠景の巨大印刷面として斜めに現れ、カメラ移動に伴うPERSPECTIVEだけで読める。花びらが画面中央を覆う瞬間、その花びらをCOLOR MATTEへ変換して黄黒LOOKへ接続。

6.20–7.75s｜LOOK E — PRINT MISREGISTRATION / POSTER OFFSET：
黄・黒・白を主軸に、黒髪と銀髪の2人が同時に存在するファッションKV。主役はPRINT MISREGISTRATION、RGBではなくYELLOW / BLACK / WHITEの版ズレ、HALFTONE SCALE、POSTER OFFSET、FRAME ECHO。人物そのものを複製せず、人物の輪郭線・影・印刷版だけを0.03〜0.08秒ずらして追従させる。「Design」は巨大な白タイポとして中央を横断するが、文字面の一部を黒インク版と黄色版が時間差で印刷する。画面全体が印刷機を通過しているように上下の版が高速同期。最後は黄色インクの大きなSWASHが液体ではなく平面的なPRINT MATTEとして横切り、CYAN系の次LOOKを露出。

7.75–9.25s｜LOOK F — HUD VECTOR SCAN / TECHNICAL REVEAL：
CYAN / BLACK / SILVERへ一気に変更。銀髪キャラクターの顔を中心に、AE SHAPE LAYER、TRIM PATHS、VECTOR SCAN、RADIAL RETICLE、TEXTLESS HUDを主役にする。四角いUI箱を並べない。細いCYAN線が顔を避けながら髪、肩、背景都市を解析するように走り、線の交点から背景だけが別レイヤーへ切り替わる。円形RETICLEは人物の目に固定せず、その周囲を0.2秒で通過して都市の遠近へ吸収。ラインが高速で伸び縮みし、その端点をNULL OBJECTとしてカメラが追従。最後に全VECTOR LINEが一点へ収束し、極細の縦線へ圧縮。その線が左右へ開いて紫ゴシック世界を出す。

9.25–10.80s｜LOOK G — GOTHIC GLASS / DISPLACEMENT REFRACTION：
紫、黒、深紅のゴシック空間。黒髪キャラクターを静かに見せ、背景にステンドグラス、細い枝状構造、蝋燭のような点光源を配置。主役AEはREFRACTION MAP、DISPLACEMENT MAP、CAUSTIC GLASS、PRISMATIC EDGE。巨大「H3」は平面タイポではなく、半透明の割れたガラス越しに屈折して見える。ガラス片は爆発させず、画面手前で数枚だけゆっくり回転しつつ、カメラはその隙間を高速に抜ける。人物の顔は屈折させず、前景ガラスが顔を横切る瞬間だけ遮蔽として使用。最後に一枚のガラス面へ細い亀裂が走り、亀裂が全面へ広がる直前にSHATTERではなく屈折面だけが奥へ吸い込まれ、次LOOKへ。

10.80–12.35s｜LOOK H — CRYSTAL SHARD TIME-SLICE：
黒髪と銀髪の2人を同一画面へ。青黒の結晶・ガラス世界。LOOK Gの屈折とは異なり、ここではAE TIME DISPLACEMENT＋TIME SLICE＋SHARD MASKを主役にする。大小の結晶片それぞれに0.03〜0.12秒異なる時間位相を持たせ、同じ瞬間の複製ではなく、視線、瞬き、髪の揺れの異なる時間断片を一つの画面に再構成。顔そのものを複数生成せず、破片内にクロップされた部分だけ時間差表示。「H3」「MiniMax」「Design」はそれぞれ別の結晶面に反射したように断片表示し、カメラ移動で一瞬だけ3語が整列して読める。最後に全SHARDの時間差が一瞬同期し、同期フレームをMATCH FREEZEせずそのままFINALへ押し出す。

12.35–15.0s｜LOOK I — FINAL MULTI-LAYER KV / KINETIC ASSEMBLY：
最終LOOKは黒髪と銀髪の2人を中心に、RED / BLACK / WHITEへ回帰しつつ、これまでの色を小さなアクセントとして統合。ここだけは過去8LOOKの演出を単純再演せず、AE KINETIC ASSEMBLY＋3D CAMERA SOLVE＋TRACK MATTE CHAINで最終KVを組み上げる。最初の0.5秒で都市奥景がZ方向から収束、次に2人の人物レイヤーが別方向のMATCH OCCLUSIONから固定位置へ入り、H3が超前景、MiniMaxが中景、Designが斜め奥景へ配置される。文字を横一列に並べない。紫の細線、CYAN HUD断片、黄色PRINT EDGE、赤いNEON TRACEがそれぞれ0.05〜0.12秒差で最終画面へ吸収され、過去LOOKの色彩履歴を一枚のKVに統合。14.4秒以降もMICRO PARALLAX、髪の僅かな揺れ、都市光の走査を継続。14.8秒でほぼ完成し、最後0.2秒だけ視認可能なHERO FRAME。BLACK OUT、FADE OUTは禁止。

TRANSITION CHAIN：
A→B＝裂傷CAMERA PATH。B→C＝巨大3によるMATCH OCCLUSION。C→D＝NEON LUMA WIPE。D→E＝花びらCOLOR MATTE。E→F＝PRINT SWASH MATTE。F→G＝VECTOR LINE APERTURE。G→H＝REFRACTION SUCTION。H→I＝TIME-SLICE SYNCHRONIZATION。全転換を異なる原理で構成し、同じWHIP、同じZOOM、同じ紙裂けを連打しない。前シーンの最後の動体が次シーンの最初の構造へ物理的に変換されるため、9LOOKでも一本の連続PVとして感じさせる。

COLOR：
LOOK A＝RED / BLACK / WHITE、LOOK B＝VIOLET / BLACK / WHITE、LOOK C＝CRIMSON NEON / BLACK、LOOK D＝INDIGO / LAVENDER / FLORAL PURPLE、LOOK E＝YELLOW / BLACK / WHITE、LOOK F＝CYAN / BLACK / SILVER、LOOK G＝DEEP PURPLE / BLACK / BURGUNDY、LOOK H＝ICE BLUE / CYAN / BLACK、LOOK I＝RED / BLACK / WHITE＋過去LOOKの微量アクセント。全LOOKを同じ赤黒へ統一しない。LOOK切替時に色温度、光源、背景質感、衣装印象まで明確に変わること。ただし各LOOK内は参照外見を維持。

AUDIO / MUSIC：
MUSIC ON。15秒を一本で走る132 BPM前後のstylish urban JRPG × alternative hip-hop × acid-jazz edge × cinematic breakbeat。0秒から即BEAT開始。各LOOKで曲そのものを交換せず、同一グルーヴのORCHESTRATIONを映像色に合わせて変化。A＝dry kick＋sub bass＋distorted texture、B＝low synth＋reverse brass、C＝electric pulse＋short guitar stab、D＝Rhodes＋airy texture、E＝percussive bass＋dry snare、F＝tight electronic percussion＋mono synth、G＝low strings＋dark piano accent、H＝glass percussionを極少量＋sub pulse、I＝全要素を整理してFULL GROOVE。EDM DROP、idol pop、cheerful funk、trailer braam、choirは禁止。音楽は途中で停止しない。

SFX DESIGN：
各LOOKで音も差別化。A＝TEXTURED PAPER RIP、B＝DEEP TYPO WHOOSH、C＝ELECTRIC SWEEP、D＝SOFT AIR PASS、E＝DRY PRINT IMPACT、F＝DIGITAL SWEEP、G＝CRYSTAL RESONANCE、H＝REVERSE GRANULAR TICK、I＝SUB IMPACT＋METALLIC LOCK。papapa / tatata、連続click、cheap UI beep、cartoon popは禁止。SFXはMUSICへ埋め込み、大きな構造変化だけを強調。

ABSOLUTE NEGATIVE：
NO 3×3 GRID IN VIDEO、NO PANEL NUMBER、NO 01–09、NO LOOK LABEL、NO TIMECODE TEXT、NO FINAL LABEL、NO REFERENCE BORDER、NO CONTACT SHEET REPRODUCTION、NO RANDOM TEXT、NO SUBTITLE、NO WATERMARK、NO DUPLICATE PERSON、NO FACE MORPH、NO EXTRA LIMBS、NO RUNNING、NO WALKING MONTAGE、NO DANCE、NO FIGHTING、NO GENERIC ACTION POSE、NO REPEATED AE TRANSITION、NO RECTANGULAR TILE SLIDE、NO SLOW DISSOLVE、NO FADE、NO LONG STATIC HOLD、NO SAME COLOR FOR ALL LOOKS。

FINAL INTENT：
参照1枚を「そのまま9面表示する画像」として使うのではなく、9つの異なるアートディレクションを持つ完成LOOKの設計図として利用する。15秒の中で、黒赤の裂け紙、紫のタイポ空間、赤ネオン、青紫の花と2.5D、黄黒の印刷版ズレ、CYAN HUD、紫ゴシック屈折、青いTIME-SLICE結晶、最終GAME KVへと連続変形。人物が激しく動くのではなく、各LOOKごとに異なるAE技法が主役となって画面全体を動かす。9シーンすべての色、衣装、背景、質感、モーション原理を明確に差別化しながら、最後には同じ作品の一本の高級ANIME GAME PVとして収束させる。
```

</details>

<sub>Source: <a href="https://x.com/sailorv321/status/2093842404159947111">https://x.com/sailorv321/status/2093842404159947111</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 32 · A Streetwear Performer Breaks Through the Poster Grid

<sub>Riccardo &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 2560×1440 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2096761524698169807.jpg" alt="A Streetwear Performer Breaks Through the Poster Grid" width="100%">](https://x.com/RickTripstar/status/2096761524698169807)

<sub><b>▶ <a href="https://x.com/RickTripstar/status/2096761524698169807">Watch the clip on the creator's post on X (@Riccardo)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A black-clad performer crosses a poster wall, copy room, and rooftop, linking jumps, turns, and freezes into a high-contrast streetwear commercial. Native-video output: 15s · 2560×1440. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,641 characters)</summary>

```text
Create one coherent 15-second 16:9 MV with synchronized picture, original song, vocals, sound design, and cuts. Anime fused with live-action photography: a single original avant-garde street-fashion anime performer breaks through a street poster wall and travels through one connected nocturnal print route: poster corridor, copy room, tiled underpass/stairs, rooftop billboard. Gritty manga energy inspired by Gachiakuta, but no copied character, panel, logo, or artwork. Keep one face, hair silhouette, body proportions, cropped utility jacket, layered shirt, loose cargo trousers, high-tops, chain, and long strap in every shot. English-only on-screen text.

VISUAL: strict black #111111, paper white #F1EBDD, and aquamarine #49D6C5; grayscale photographic spaces and skin. Retro copy-zine, pasted street posters, halftone, torn paper, tape, scanlines, restrained VHS gate weave and fringe. Main type is ultra-black condensed grotesk, ALL CAPS, tight tracking, squared counters. Every text event has Layer A readable hero base, Layer B offset aquamarine/grayscale print plate, Layer C foreground paper/type occlusion; read clearly before transforming and recover within one beat. Use photocopy burst on snare, aquamarine misregistration on hi-hat, torn occlusion on vocal words, irregular split panels on 808, delayed double portrait on hi-hat, and a short black type field at the ending. No random print, fake logos, gibberish, or ordinary subtitles.

MUSIC/PERFORMANCE: original K-pop hip-hop/trap-rap, 128 BPM 4/4, double-time hats with half-time body feel, dry kick, snare on beat three, clipped clap, sparse hats and one roll, moving 3-note 808 with a slide and octave answer, metallic pluck and distorted electric-piano stab. One confident neutral-masculine voice: crisp aggressive rap, then chant-sung hook; final tag adds low-octave double. Structure: 0–1.875 intro tag “CUT IN”; 1.875–5.625 rap; 5.625–7.5 rising pre-hook and breath; 7.5–11.25 call-and-response hook; 11.25–13.125 kick-out beat switch; 13.125–15 final tag, bass hit, tiny tape-stop, clean hard stop, no fade. Lyrics: Rap A1 “Cut through the paper, make the dead wall shake”; Rap A2 “Ink in my jacket, every fake frame breaks”; Pre-hook “Hold that breath, let it rise”; Hook 1 “BREAK THE GRID”; Hook 2 “MAKE IT LIVE”; Response “Again!”; Final tag “BREAK THE GRID”. A1/A2 have connected meaning and rhyme, with straight-sixteenth then triplet cadence. Do not subtitle the lyrics; visual words are CUT IN, BREAK, THE GRID, HOLD, MAKE IT LIVE, AGAIN. Actions include diagonal power walk, cross-step, low drop/rebound, pivot freeze, jacket snap/strap swing, push-wall rebound, paper passage, and controlled stair step-down. Include three large actions, two space contacts, one clothing-inertia action, and two design-led still points. Align mouth, jaw, eyes, shoulders, footfalls, breath, type, snare, and 808.

SHOT 1 — 0.0–1.6s, wide low push-in, poster-wall entrance. Performer steps from deep background through torn seam, shoulder first; front foot transfers weight, jacket catches paper, strap trails, camera settles on face. Action: paper passage. Text “CUT IN”, 110% hero. Layer A behind shoulder; B aquamarine jitter; C taped strip crosses torso then peels. Rhythm/Cut: inhale tears paper, kick hard-cuts.
SHOT 2 — 1.6–3.4s, eye-level side track, poster corridor. Diagonal power walk left-to-right, foot on kick, body crosses seam, strap and hem trail, camera jolts. Action: power walk. Text “BREAK”, 70% split by poster columns. A clean by face; B slips on hats; C foreground strip passes arm. Rhythm/Cut: snare halftone and hard cut.
SHOT 3 — 3.4–5.2s, low close-medium backward dolly, copy doorway. Cross-step over floor strip, shoulder-led 90-degree pivot, elbow brushes copier, torso rebounds. Action: cross-step/half-turn. Text “THE GRID”, 90% across copier/body in two irregular panels. A reads; B scans on rhyme; C paper flap slices lower frame and recovers. Rhythm/Cut: triplet jumps, cut on 808.

SHOT 4 — 5.2–7.0s, locked eye-level close-up, copy-room still point. Pivot ends; one collar pull, shoulders freeze, eyes track, jaw releases on breath, strap settles. Action: jacket pull/freeze. Text “HOLD”, 125% behind head with face pocket. A readable; B returns to registration; C tiny monospaced “BREATHE” seam note vanishes. Rhythm/Cut: low end drops, hold, flash-cut on pre-hook end.
SHOT 5 — 7.0–8.9s, wide low orbit, tiled underpass. Hook hit: performer bursts through threshold, forearm contacts pillar, center drops, leg rebounds, jacket opens, camera orbits then snaps back. Action: push-wall rebound. Text “BREAK THE GRID”, 145% in three unequal panels. A reads; B jumps aquamarine on 808; C torn diagonal crosses pillar but reveals face. Rhythm/Cut: hook consonant and kick cut on rebound.
SHOT 6 — 8.9–10.8s, overhead-to-front whip tilt, stairs. Two steps up, axis turns down, controlled short step-down, knees absorb, upright hit. Action: high-low step. Text “MAKE”, 80% vertical along stair diagonal. A reads on rise; B duplicates one character per hat; C railing tape flicks away. Rhythm/Cut: response lands on step-down, photocopy flash restores grayscale.
SHOT 7 — 10.8–13.2s, lateral track into frontal, rooftop billboard. Shoulder parts hanging pasted sheet, torso follows, strap swings once, three-quarter turn, feet lock. Action: paper passage/strap swing/pivot freeze. Text “MAKE IT LIVE”, 115% two-line fold around body. A reads before turn; B aquamarine misregisters on hat roll; C strap briefly occludes lower words, then clear. Rhythm/Cut: beat switch removes kick half-bar, one frame jump at strap apex.
SHOT 8 — 13.2–15.0s, frontal close-up to black type field, rooftop billboard. Feet finish turn, shoulders square, chin lifts, jacket and strap settle late, camera holds, then hard-cuts to black. Action: final stance/release. Text “BREAK THE GRID”, 150%, same type family, paper-white on black with aquamarine offset. A clear; B low-octave visual duplicate; C compresses like tape stop but remains briefly readable. Rhythm/Cut: final bass hit and tag land together, two-frame tape tail, hard cut.

GLOBAL LOCKS: one protagonist only, stable anime identity and outfit integrated into real photographic spaces; connected route, strict three-color system, accurate English, clear face and mouth. Hard cuts, flash frames, paper occlusion, panel splits, misregistration, restrained VHS only. No soft dissolve, fade, generic dance loop, continuous shake, extra characters, face swap, outfit change, duplicate limbs, broken hands, covered eyes/mouth, watermark, logo, fake brand, gibberish, or unreadable text. End decisively.
```

</details>

<sub>Source: <a href="https://x.com/RickTripstar/status/2096761524698169807">https://x.com/RickTripstar/status/2096761524698169807</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 33 · An Anime Girl Takes Shape Stroke by Stroke

<sub>Photogenic Weekend &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1920×1070 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2093133440359317751.jpg" alt="An Anime Girl Takes Shape Stroke by Stroke" width="100%">](https://x.com/PhotogenicWeekE/status/2093133440359317751)

<sub><b>▶ <a href="https://x.com/PhotogenicWeekE/status/2093133440359317751">Watch the clip on the creator's post on X (@Photogenic Weekend)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A stylus builds a girl from a blank canvas, adding line art, color, and a potted plant through a complete drawing-timelapse sequence. Native-video output: 15s · 1920×1070. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (1,001 characters)</summary>

```text
How the reference pictures align with the target video — Picture 1 (from Shot 1) aligns with the 0.00-second mark of the target video.

integrated_multimodal_description: [Shot 1] 2D anime digital illustration, a high-quality digital drawing recorded as a timelapse, with the artist's hand holding a stylus pen visibly drawing on the canvas. The video starts from a white digital canvas and draws the basic forms and shapes first, starting from the general (big) outline sketch of the pose, then adding line after line to add new details on the face, hair, and clothes until a complete lineart sketch for the character is done. Then the coloring phase begins: flat base colors are filled evenly within the lineart, soft shading and highlights are layered on the face, hair, and clothes, and final finishing touches are added until the completed artwork matches <Picture 1> exactly.

overall_soundscape: The soft scratch of the stylus on the tablet screen, light desk ambience.

non_diegetic_music: N/A
```

</details>

<sub>Source: <a href="https://x.com/PhotogenicWeekE/status/2093133440359317751">https://x.com/PhotogenicWeekE/status/2093133440359317751</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 34 · Sheldon and Penny from Prompts Alone

<sub>Squeak Al-Gaib &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 12 &nbsp;·&nbsp; 1376×768 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-squeakalgaib-2086531027347144916.jpg" alt="Sheldon and Penny from Prompts Alone" width="100%">](https://x.com/SqueakAlGaib/status/2086531027347144916)

<sub><b>▶ <a href="https://x.com/SqueakAlGaib/status/2086531027347144916">Watch the clip on the creator's post on X (@Squeak Al-Gaib)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Uses Sheldon and Penny as characters defined in text instructions and generates the resulting scene directly with MiniMax H3.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (15,194 characters)</summary>

```text
Create a 12-second live-action sitcom-style scene in 16:9 aspect ratio featuring Sheldon Cooper and Penny from The Big Bang Theory. The scene is a very silly, funny, character-accurate conversation about artificial intelligence that ends with both characters realizing in horror that they are not real people, but prompts inside an AI-generated video. The tone should feel exactly like a classic Big Bang Theory hallway scene: fast, witty, natural, awkward, and playful, with precise comic timing and highly exaggerated, animated facial expressions. The pacing must feel natural and unforced, like an actual exchange from the original sitcom series.

IMPORTANT DIALOGUE RULE: Only the dialogue written in double quotes below may be spoken. There must be no extra dialogue, no improvisation, no narration, no voice-over, and no additional spoken words. Each line must be spoken exactly once, by the specific character assigned to it. Sheldon Cooper says: “AI language models predict the next most statistically probable word.” Penny says: “So what am I about to say?” Sheldon Cooper says: “Something intellectually disappointing.” Penny says: “Wait… somebody already wrote this sentence.” Sheldon Cooper says: “We’re scripted?” Penny says: “Worse. Prompted.” No other spoken words are allowed.

LOCATION AND SCENE SETTING: Set the entire scene in the iconic apartment hallway and elevator lobby area from The Big Bang Theory, outside Penny’s apartment 4B. The elevator is visibly broken as usual, with the dark empty elevator shaft area and caution-taped or damaged elevator look recognizable in the softly blurred background. Penny’s apartment door is already open at the start of the scene. Penny stands immediately inside the doorway of apartment 4B, facing outward into the hallway. Sheldon Cooper stands immediately outside the doorway, positioned very close to Penny so Sheldon Cooper and Penny can both fit naturally inside an extremely tight two-person close-up without requiring a wide composition. The visual style, set layout, hallway walls, warm apartment lighting, and sitcom staging should feel extremely faithful to the original series.

CRITICAL CAMERA FRAMING RESTRICTION: Use ONLY extremely tight close-ups, tight two-person close-ups, and individual close-ups. Absolutely no medium-wide shots, wide shots, waist-up two-shots, full-body shots, distant framing, establishing wide shots, or camera pullbacks at any moment. Sheldon Cooper’s face and Penny’s face must remain large, sharp, high-definition, and fully recognizable throughout the entire 12 seconds.

Whenever Sheldon Cooper and Penny are visible together, use an EXTREMELY TIGHT TWO-PERSON CLOSE-UP: frame both characters approximately from the upper chest or shoulders upward, with both complete faces occupying most of the 16:9 frame. Keep Sheldon Cooper and Penny close together near the apartment doorway and on nearly the same focal plane. Both heads, both complete faces, eyes, mouths, and facial expressions must remain fully inside the frame and sharply resolved. Allow only a small amount of hallway and doorway background around them.

Do not zoom out or pull back to accommodate both characters. Instead, physically compose Sheldon Cooper and Penny closer together inside the doorway area so both faces remain large. This tight two-person close-up requirement applies especially to the OPENING SHOT and the FINAL SHOT. The final second must NOT become wider under any circumstances.

CAMERA AND FRAMING: Begin immediately with an extremely tight two-person close-up showing Sheldon Cooper and Penny together from approximately the upper chest or shoulders upward. Sheldon Cooper stands immediately outside apartment 4B while Penny stands immediately inside the already-open doorway. Both faces occupy a large portion of the frame and remain simultaneously sharp.

After the opening, use clean sitcom-style cuts into individual close-ups and tight medium close-ups that never frame below the upper chest. Keep faces extremely large and detailed. Camera movement should remain minimal and controlled, similar to polished sitcom coverage, with subtle slow push-ins of very small amplitude for comedic emphasis. Never create additional distance from the subjects.

For the ending, return to an extremely tight two-person close-up with both Sheldon Cooper and Penny’s complete faces filling most of the frame. Do NOT pull out, zoom out, widen the lens, reveal their full bodies, or show additional hallway space during the final reaction.

LIGHTING AND VISUAL STYLE: Use warm, bright, natural sitcom interior lighting. Penny’s apartment interior should glow warmly behind Penny, while the hallway is evenly lit in the familiar Big Bang Theory style. Both faces must be extremely well-lit, clearly visible, and flattering, with natural skin tones, crisp facial detail, clear eyes, and strong separation from the background. The overall visual style should feel like a professionally shot network sitcom scene, not cinematic noir, not over-stylized, and not dark. Use shallow-to-moderate depth of field so the environment remains recognizable while Sheldon Cooper and Penny’s faces stay exceptionally sharp.

CHARACTER APPEARANCE AND MANNERISMS: Sheldon Cooper must look and behave exactly like Sheldon in the series: upright posture, slightly stiff body language, precise diction, intellectual smugness, mildly condescending confidence, quick blinking, intense focus, tiny head movements, tightly controlled hand gestures, and an overly serious tone even when saying ridiculous things. Sheldon Cooper should wear a typical Sheldon outfit, such as a bright geeky science-themed T-shirt layered over a long-sleeve shirt.

Penny must look and behave exactly like Penny in the series: relaxed posture, highly expressive face, grounded and casual energy, playful sarcasm, fast reaction timing, expressive eyebrows, animated eye movements, slight head tilts, knowing half-smiles, and a naturally conversational speaking style. Penny should wear a casual everyday apartment outfit appropriate to the series, such as a fitted top and jeans or a soft casual blouse.

EXAGGERATED FACIAL PERFORMANCE: Throughout the entire 12-second clip, both characters should use more animated, heightened sitcom expressions than before while remaining believable and human. Every comedic beat should register clearly through the eyes, eyebrows, mouth, cheeks, head position, and micro-reactions.

Sheldon Cooper’s smugness should be visibly exaggerated: raised chin, narrowed eyes, tiny superior smile, lifted eyebrow, precise mouth movements, and self-satisfied pauses. When Sheldon Cooper realizes something is wrong, Sheldon Cooper’s transformation must be dramatic and instantly readable: smug smile disappears, eyebrows lift sharply, eyes widen, mouth slightly opens, head freezes, then Sheldon Cooper slowly turns toward the camera with unmistakable existential dread.

Penny’s sarcasm should be equally animated: larger eyebrow raises, stronger skeptical looks, playful eye rolls, amused half-smiles, slight head tilts, and quick expressive changes. When Penny realizes that Penny’s sentence has already been written, Penny’s expression must visibly progress from casual confidence to confusion, then suspicion, then sudden wide-eyed realization. Penny’s final “Worse. Prompted.” reaction should combine alarm, disbelief, and deadpan comedic certainty.

PERFORMANCE AND COMEDIC RHYTHM: Sheldon Cooper begins the scene in full lecture mode, speaking as though giving a factual correction to Penny. Penny listens with exaggerated amused skepticism. Sheldon Cooper delivers the first line with smug certainty and clipped precision. Penny responds with casual, direct, slightly teasing confidence. Sheldon Cooper replies with a dry, superior, mildly insulting punchline.

Penny’s next line is the turning point: Penny suddenly becomes aware of the artificiality of the scene, pauses, looks toward the camera, and says the line with rapidly growing confusion. Sheldon Cooper’s expression visibly collapses from smug confidence into dawning existential panic. Sheldon Cooper then slowly looks toward the camera and says “We’re scripted?” with exaggerated worried disbelief. Penny delivers “Worse. Prompted.” with a horrified but matter-of-fact realization. Both Sheldon Cooper and Penny end by staring directly toward the camera in exaggerated shared existential horror.

TIMING, SHOTS, AND EXACT DIALOGUE ASSIGNMENT:

0.0 to 2.2 seconds: Begin on an EXTREMELY TIGHT TWO-PERSON CLOSE-UP outside apartment 4B. Sheldon Cooper and Penny are framed together only from approximately the upper chest or shoulders upward. Both complete faces are very large in frame, sharply detailed, and positioned close together on nearly the same focal plane. Penny remains just inside the already-open doorway while Sheldon Cooper stands immediately outside.

Use no establishing wide shot. The apartment doorway and a very small portion of the familiar hallway provide enough environmental context behind their large faces.

Sheldon Cooper faces Penny with an exaggeratedly serious, self-important expression and says exactly once: “AI language models predict the next most statistically probable word.”

Penny remains silent throughout Sheldon Cooper’s line. Penny reacts with animated skeptical eyebrows, a small amused smile, and a slight head tilt.

2.2 to 3.4 seconds: Cut to an extremely tight close-up of Penny from approximately shoulders upward. Penny’s face occupies most of the frame. Penny tilts Penny’s head, raises Penny’s eyebrows with exaggerated playful skepticism, gives Sheldon Cooper an amused look, and says exactly once: “So what am I about to say?”

Sheldon Cooper remains silent during Penny’s line.

3.4 to 5.3 seconds: Cut to an extremely tight close-up of Sheldon Cooper. Sheldon Cooper’s face fills most of the frame. Sheldon Cooper lifts one eyebrow, produces an exaggerated tiny smug smile, slightly raises Sheldon Cooper’s chin, and delivers the line with precise intellectual superiority.

Sheldon Cooper says exactly once: “Something intellectually disappointing.”

Immediately after Sheldon Cooper finishes the line, add a brief classic sitcom audience laugh. Sheldon Cooper maintains the exaggerated smug expression for a fraction of a second to let the punchline land.

5.3 to 7.8 seconds: Cut back to an extremely tight close-up of Penny. Penny begins with a sarcastic amused expression, then Penny’s expression changes dramatically and visibly in stages. Penny’s smile fades. Penny’s eyebrows draw together. Penny’s eyes shift as if thinking. Penny suddenly stops moving for a beat, then Penny’s eyes widen.

Penny slowly looks directly into the camera lens as if Penny has suddenly become aware of the artificial nature of the scene.

Penny says exactly once: “Wait… somebody already wrote this sentence.”

Penny’s delivery begins puzzled and ends genuinely disturbed. Add a smaller sitcom audience laugh that fades quickly into increasingly awkward silence.

7.8 to 9.7 seconds: Cut to an extremely tight close-up of Sheldon Cooper. Sheldon Cooper’s entire face remains sharply resolved and large in frame. Sheldon Cooper’s smug expression disappears completely. Sheldon Cooper’s eyebrows rise dramatically, Sheldon Cooper’s eyes widen, Sheldon Cooper’s lips part slightly, and Sheldon Cooper freezes for a beat.

Sheldon Cooper slowly shifts Sheldon Cooper’s gaze directly toward the camera with exaggerated dawning existential dread.

Sheldon Cooper says exactly once: “We’re scripted?”

Sheldon Cooper’s tone should be anxious, confused, and deeply disturbed.

9.7 to 11.0 seconds: Cut to an extremely tight close-up of Penny. Penny keeps looking directly toward the camera. Penny’s eyes are wide, Penny’s eyebrows remain raised, and Penny’s face combines horrified realization with Penny’s characteristic dry comedic delivery.

Penny says exactly once: “Worse. Prompted.”

Penny delivers “Worse” with a short deadpan pause before “Prompted,” allowing the final word to land clearly.

11.0 to 12.0 seconds: Cut to an EXTREMELY TIGHT TWO-PERSON CLOSE-UP. Absolutely DO NOT widen the framing for this ending. Sheldon Cooper and Penny are positioned very close together near the doorway, framed only from approximately the shoulders upward. Both complete faces occupy most of the 16:9 frame simultaneously and remain exceptionally sharp, detailed, undistorted, and clearly recognizable.

Sheldon Cooper and Penny both stare directly toward the camera lens in exaggerated shared existential horror. Sheldon Cooper’s eyes are extremely wide, eyebrows raised, jaw slightly dropped. Penny’s eyes are wide, Penny’s mouth slightly opens, and Penny exchanges one extremely quick horrified side-glance toward Sheldon Cooper before looking back into the camera.

Neither Sheldon Cooper nor Penny says anything further.

Add one final short sitcom audience laugh that initially reacts to “Worse. Prompted.” and then abruptly fades into awkward silence while Sheldon Cooper and Penny remain frozen in the extremely tight two-person close-up.

IMPORTANT ENDING CAMERA RULE: During 11.0–12.0 seconds, maintain the exact tight facial scale. No camera pullback. No zoom out. No transition to a medium shot. No waist-up framing. No reveal of additional hallway space. No wider composition whatsoever. End directly on the large, sharply rendered faces of Sheldon Cooper and Penny.

AUDIO DESIGN: No background music. No narration. No voice-over. No on-screen text. No watermark. No AI parody label. Use only the exact dialogue lines listed above, plus natural sitcom set ambience and classic audience laugh cues. Include subtle hallway room tone, faint apartment ambience, light clothing rustle, tiny foot shifts, and clean studio-style dialogue recording.

The audience laughter should feel like a classic Big Bang Theory studio-audience reaction: brief, well-timed, and placed after the strongest joke beats, especially after “Something intellectually disappointing,” after “somebody already wrote this sentence,” and a final shorter laugh sting after “Worse. Prompted.” before the awkward silence.

All dialogue must remain crystal clear and perfectly lip-synchronized. Sheldon Cooper’s voice must only come from Sheldon Cooper. Penny’s voice must only come from Penny. Never blend, swap, duplicate, overlap, or garble the voices.

FINAL RESTRICTIONS: No wide shots. No medium-wide shots. No waist-up two-shots. No full-body framing. No distant faces. No opening establishing wide shot. No wider ending shot. No camera pullback. No zoom-out. No distorted faces. No extra dialogue. No repeated dialogue. No ad-libs. No narration. No subtitles. No captions. No on-screen text of any kind. No watermark. No AI parody disclosure. No music. No other characters entering the frame. No door knocking. The door is already open at the beginning.

Maintain extremely tight facial framing, high-definition facial clarity, accurate speaker assignment, exaggerated animated expressions, natural sitcom pacing, faithful Sheldon Cooper and Penny mannerisms, and believable Big Bang Theory comedic rhythm throughout the entire 12-second clip.
```

</details>

<sub>Source: <a href="https://x.com/SqueakAlGaib/status/2086531027347144916">https://x.com/SqueakAlGaib/status/2086531027347144916</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 35 · A 2K-versus-720P Generation Face-Off

<sub>MadMax &nbsp;·&nbsp; FL2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1080×1080 &nbsp;·&nbsp; square</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2083855654205186452.jpg" alt="A 2K-versus-720P Generation Face-Off" width="100%">](https://x.com/MadMax_Series/status/2083855654205186452)

<sub><b>▶ <a href="https://x.com/MadMax_Series/status/2083855654205186452">Watch the clip on the creator's post on X (@MadMax)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for a 2k-versus-720p generation face-off on X. Native-video output: 15s · 1080×1080. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,905 characters)</summary>

```text
Create a 15-second photorealistic cinematic dark-fantasy sequence in 16:9 widescreen. The video must contain exactly three clearly separated cinematic shots connected by clean hard cuts. No dissolves, morphing transitions or continuous camera orbit.

MASTER DRAGON LOCK:
Show one enormous ancient dragon with a broad powerful body, charcoal-black overlapping scales, subtle dark crimson colouring across its head and neck, two swept-back horns, smaller facial spikes, glowing amber-orange eyes, one long tail and one pair of enormous bat-like wings with dark leathery membranes. The dragon has four legs: two forelegs and two hind legs. Its design, size, horns, colour, anatomy and facial structure remain identical in all three shots. The dragon must feel extremely heavy, ancient and physically realistic.

MASTER RIDER LOCK:
One adult armoured rider is already seated securely in a dark leather saddle on the dragon from the very first frame. The rider wears detailed weathered silver plate armour, dark under-clothing, a fitted medieval helmet with a narrow shadowed visor and a long dark cloak. The rider’s face is never clearly visible. The rider holds leather reins connected to the saddle and remains seated throughout the entire sequence. The rider does not suddenly appear, mount, dismount or change clothing. During the first shot, the rider is naturally hidden behind the dragon’s large head, neck and folded wings.

ENVIRONMENT AND LIGHTING:
The sequence takes place inside a gigantic ancient mountain cave. The cave contains rough black rock walls, enormous stone formations, drifting mist, scattered bones and faint glowing embers between cracks in the ground. The far interior is almost black, but the dragon must remain readable through soft amber reflections and cold blue rim light entering from the cave mouth. The cave entrance opens from a high mountain cliff into a vast dramatic landscape of jagged mountains, deep valleys, distant waterfalls, rolling clouds and pale stormy daylight. Maintain a cinematic cold-blue and muted-amber colour palette with deep shadows, volumetric light rays and realistic atmospheric haze. Dark and mysterious, but never so underexposed that the dragon or rider becomes blurry or invisible.

SHOT 1 — DRAGON EMERGES, 0–5 SECONDS:
Begin with a symmetrical low frontal wide shot positioned near the cave entrance, facing deep into the darkness. The camera slowly tracks backward toward the entrance as the enormous dragon walks forward out of the black cave interior. The dragon’s wings remain completely folded against both sides of its body. Its glowing amber eyes appear first, followed by its horned head, shoulders and powerful forelegs becoming visible through the mist.

Each heavy footstep shakes the cave floor and dislodges small stones and dust from the ceiling. The dragon exhales dense vapour from its nostrils and releases a deep restrained growl. Its head moves naturally with the weight of each step. The dragon looks directly past the camera toward the cave opening. The rider is already seated but remains hidden behind the dragon’s head and neck. Do not reveal the rider clearly during this shot.

SHOT 2 — RIDER REVEAL, 5–9 SECONDS:
Clean hard cut to a low three-quarter side tracking shot beside the moving dragon. Begin close to the dragon’s horned head and sharply detailed scales. Track smoothly backward along the dragon’s neck and folded wing while the dragon continues walking toward the cave entrance.

As the camera reaches the dragon’s shoulder, reveal the single armoured rider seated in the saddle between the folded wings. Hold the composition long enough to clearly show the rider’s silver armour, helmet, dark cloak and both hands gripping the reins. The rider looks toward the bright cave exit and leans slightly forward in preparation for takeoff. The dragon and rider remain in continuous forward motion. Do not show a separate rider anywhere else in the cave.

SHOT 3 — REAR TAKEOFF AND FLIGHT, 9–15 SECONDS:
Clean hard cut to an epic wide rear view positioned behind and slightly above the dragon and rider. The bright cave mouth and vast mountain landscape fill the background ahead of them. The dragon accelerates into a powerful run toward the cave opening while its wings remain folded enough to pass safely through the cave.

The dragon reaches the cliff edge and makes one forceful leap completely out of the cave. Only after clearing the rock opening, it spreads both enormous wings to their full symmetrical width. The sudden wing expansion pushes mist, dust and loose stones outward from the cave entrance. The rider leans forward, grips the reins and remains firmly attached to the saddle.

The dragon performs one enormous downward wingbeat, catches the air and transitions naturally into stable forward flight. Loose stones fall from the cliff beneath it. The camera rapidly follows from behind as the dragon and rider soar away over the deep valley between jagged mountain peaks. The long tail streams naturally behind the dragon and the rider’s cloak whips in the wind. End on a majestic wide rear silhouette of the dragon flying into the open mountain landscape as sunlight breaks through the storm clouds.

CAMERA AND MOTION:
Premium cinematic camera movement with realistic scale and parallax. Shot one is a controlled backward dolly. Shot two is a smooth low side-tracking reveal. Shot three is a dynamic rear pursuit shot that follows the takeoff out of the cave. Use natural motion blur only during the leap and wingbeat. Keep the dragon’s movement heavy on the ground and powerful but graceful in the air. No shaky chaotic framing and no extreme close-ups that obscure the action.

CINEMATIC QUALITY:
Big-budget photorealistic dark-fantasy visual effects, highly detailed scales and armour, realistic creature muscles beneath the skin, physically accurate wing membranes, believable foot contact, convincing dust and falling-rock physics, volumetric cave mist, dramatic rim lighting, strong depth, atmospheric perspective and stable character consistency.

AUDIO:
No dialogue and no music. Deep dragon breathing, restrained growl, heavy echoing footsteps, claws scraping stone, armour movement, leather saddle creaking, falling pebbles, rushing cave wind, powerful wingbeat and a deep dragon roar as it enters open air.

STRICT CONSISTENCY:
Exactly one dragon and one rider. The rider is seated on the dragon from the beginning and never disappears. No additional people, dragons or creatures. No dragon transformation or colour change. No extra heads, horns, tails, wings, legs or riders. The wings remain folded inside the cave and open only after the dragon has completely cleared the cave mouth. The wings must not clip through the cave walls. The rider must not float above the saddle or merge into the dragon. No fire breathing, combat, dialogue, text, logos, blood or visible injuries.
```

</details>

<sub>Source: <a href="https://x.com/MadMax_Series/status/2083855654205186452">https://x.com/MadMax_Series/status/2083855654205186452</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 36 · A Fantasy Face-Off from the Same Prompt

<sub>MadMax &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1080×1080 &nbsp;·&nbsp; square</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2083501727836225758.jpg" alt="A Fantasy Face-Off from the Same Prompt" width="100%">](https://x.com/MadMax_Series/status/2083501727836225758)

<sub><b>▶ <a href="https://x.com/MadMax_Series/status/2083501727836225758">Watch the clip on the creator's post on X (@MadMax)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>The original creator published the complete generation prompt for a fantasy face-off from the same prompt on X. Native-video output: 15s · 1080×1080. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,754 characters)</summary>

```text
Create a 15-second photorealistic cinematic dark-fantasy battlefield sequence in 16:9 widescreen. The video contains exactly two shots connected by one clean hard cut at approximately 11 seconds. No dissolves, morphing transitions or montage editing.

MASTER CREATURE LOCK:
Show exactly one colossal ash-white bat-dragon with wyvern anatomy. The creature has one broad skull-like head, two glowing ember-red eyes, one enormous mouth filled with long dark teeth, pale hairless scaled skin, a powerful chest, two muscular hind legs, one long narrow tail and one pair of gigantic bat-like wings. Its wings have strong finger-like bones supporting huge semi-translucent pale membranes. The wings glow warm orange when backlit by the battlefield fires.

The bat-dragon has no separate forelegs or human arms. Its wings are its only front limbs. Its design, colour, face, size, anatomy and wing structure remain identical throughout both shots. It never transforms, multiplies, changes colour or grows additional limbs.

BATTLEFIELD AND ARMY:
A vast apocalyptic fantasy battlefield beneath turbulent charcoal-grey storm clouds. The ground is dark, broken and covered with ash, embers, scorched rocks and drifting smoke. Large walls of orange fire burn across the distant horizon, strongly backlighting the approaching bat-dragon.

Hundreds of shadowy horned warriors crowd the battlefield. The warriors wear dark rough armour and simple horned helmets. Keep the warriors anonymous, visually similar and mostly seen as small silhouettes. No individual warrior is a main character and no faces require close detail. The army fills the foreground and middle distance to establish the impossible scale of the flying creature.

Use a cold grey-blue environment contrasted with intense orange firelight, glowing embers and warm translucent wing membranes. The environment must remain clearly visible through the smoke.

SHOT 1 — COLOSSAL LOW FLYOVER, 0–11 SECONDS:
Begin with a low ground-level ultra-wide camera positioned inside the tightly packed horned army, looking toward the burning horizon. Foreground warriors partially frame the bottom and sides of the image. The handheld camera moves slightly between the crowd while always looking forward.

Through the smoke and fire, the silhouette of one colossal bat-dragon appears in the sky. Its enormous folded wing shape initially resembles two mountains rising through the flames. The dragon then opens both wings to their full symmetrical width, completely dominating the sky. Bright orange fire shines through the pale wing membranes while the creature’s red eyes become visible.

The dragon performs one slow, immensely powerful downward wingbeat and descends toward the battlefield. The wingbeat pushes smoke outward in a huge circular pattern. The army looks upward and begins moving in panic as the creature rapidly approaches.

The bat-dragon glides extremely low above the battlefield without landing. Its chest and head pass just above the horned warriors. It banks slightly, bringing one enormous wing close over the foreground camera while the other wing remains fully visible and correctly attached. The wing itself does not physically strike the warriors.

The pressure wave created by the low flyover blasts across the army. Ash, embers, loose weapons, cloth and small pieces of debris surge sideways through the frame. Foreground warriors are knocked off balance, lifted briefly and scattered by the powerful wind, tumbling away from the creature without graphic impact or injury. Keep the movement chaotic but physically believable.

The camera shakes violently from the wing pressure and quickly pans to follow the dragon’s low flight across the battlefield. Flames bend beneath the airflow and smoke rolls outward behind the creature. Maintain a clear view of the same bat-dragon throughout the flyover. The dragon must not disappear completely behind its own wing or the smoke.

SHOT 2 — FRONTAL ROARING CHARGE, 11–15 SECONDS:
At approximately 11 seconds, make one clean hard cut to a frontal low-angle telephoto shot directly in the bat-dragon’s flight path. The creature is already flying forward through thick smoke and towering flames, coming straight toward the camera.

Keep both enormous wings visible on either side of its body as they perform one powerful coordinated wingbeat. The glowing red eyes remain locked directly on the camera. Burning embers stream around the creature while the orange flames behind it illuminate the translucent wing membranes.

As the bat-dragon rapidly closes the distance, it lowers its skull-like head and opens its enormous mouth, revealing multiple rows of long sharp teeth. It releases a deafening roar directly toward the camera. The force of the roar pushes smoke and embers outward from its face.

The camera retreats slightly while the dragon continues approaching, creating intense forward momentum. Finish just before impact with the creature’s roaring face, glowing eyes and wings dominating the frame. The dragon does not hit or pass through the camera.

CAMERA AND MOTION:
Shot one uses a low handheld battlefield perspective with strong scale, foreground silhouettes, realistic parallax and a fast pan following the flyover. Shot two uses a steady frontal tracking camera that retreats as the dragon approaches. Use cinematic motion blur on the wing tips, airborne ash and scattered debris, but keep the creature’s face and body sharply readable. The motion must feel fast, heavy and dangerous rather than weightless.

VISUAL QUALITY:
Premium big-budget dark-fantasy visual effects, photorealistic creature texture, physically accurate wing membranes, believable muscles moving beneath pale skin, enormous scale, detailed fire and smoke simulations, dense volumetric atmosphere, realistic aerodynamic pressure, strong depth, natural motion blur, sharp creature details and dramatic fire backlighting.

AUDIO:
No dialogue and no music. Roaring battlefield fire, panicked distant army sounds, rushing wind, deep leathery wingbeats, armour rattling, debris scraping across the ground, heavy low-frequency pressure wave and one terrifying creature roar during the final frontal approach.

STRICT CONSISTENCY:
Exactly one bat-dragon. No additional flying creatures. No rider. Exactly one head, two eyes, one mouth, two wings, two hind legs and one tail. No extra wings, arms, heads, faces or tails. The wings must remain attached to the same creature and must not turn into hands. The dragon never lands, breathes fire or changes design. Keep both wings intact and symmetrical. The horned warriors remain separate from the dragon and do not merge into its body. No visible casualties, blood, gore, text, subtitles, logos or real-world symbols.
```

</details>

<sub>Source: <a href="https://x.com/MadMax_Series/status/2083501727836225758">https://x.com/MadMax_Series/status/2083501727836225758</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 37 · Urban street superpowered punch action sequence

<sub>Shara I Ai Video Creator &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 28 &nbsp;·&nbsp; 1280×720 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2082892924694712509.jpg" alt="Urban street superpowered punch action sequence" width="100%">](https://x.com/itsshara_ai/status/2082892924694712509)

<sub><b>▶ <a href="https://x.com/itsshara_ai/status/2082892924694712509">Watch the clip on the creator's post on X (@Shara I Ai Video Creator)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>An H3 output for Urban street superpowered punch action sequence. This page retains the original X source link. The public Prompt is preserved verbatim without translation, rewriting, or completion. Hosted-video output: 28s · 1280×720.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (7,088 characters)</summary>

```text
PART 1 (0–15 SECONDS)

LOCATION DETAIL: Gritty urban street at golden hour dusk. Wet concrete ground reflecting golden-orange light. Industrial concrete pillars and brick walls frame both sides. Metal railings visible. Golden-orange sky in background. Blue shadows cast across street creating high-contrast cinematic look. Volumetric dust particles floating in air catching light.

CAMERA ANGLES & CINEMATOGRAPHY:

0-1s: WIDE ESTABLISHING SHOT, camera positioned at street level, tilted slightly Dutch angle to show desperation. Slow dolly-in toward the fighter
1-3s: LOW-ANGLE CLOSE-UP on beaten fighter's face as goons surround him. Camera slightly beneath eye-level looking upward at aggressive goons (makes them look menacing, him vulnerable)
3-5s: OVERHEAD SHOT as golden-blue energy beam descends. Camera positioned directly above, looking down at the beam engulfing him
5-7s: FAST 360-DEGREE ORBITAL CAMERA ROTATION around fighter during energy explosion. Energy aura visible radiating outward. Multiple angles showing transformation from all sides
7-8s: EXTREME CLOSE-UP on fighter's face as eyes glow. Camera inches from face, eyes filling 60% of frame. Electricity crackling visible around eyes
8-9s: LOW-ANGLE UPWARD SHOT as fighter stands fully transformed. Camera positioned beneath him looking up he now TOWERS over everyone. Shows dominance shift
9-12s: DYNAMIC WHIP-PAN following first goon's charge. Camera pans rapidly to track movement, then HARD CUT to:
12-14s: SLOW-MOTION SIDE PROFILE SHOT of devastating punch. Camera positioned at exact side angle to catch punch trajectory. Slow-motion impact  shockwave visible in air, goon's body reacting to force
14-15s: TRACKING SHOT following goon flying backward. Camera moves with the goon's body trajectory, then IMPACT SHOT from goon's POV as he crashes into wall (camera shakes violently on impact)

STORY BEATS:

A beaten-down fighter in torn shirt, bruises covering his face, blood dripping, is VICIOUSLY surrounded by three aggressive goons on a wet industrial street at golden hour. He's backed against a brick wall, barely defending himself as punches rain down. He's on the verge of collapse.

SUDDENLY  a massive golden-blue energy beam EXPLODES down from the sky with CATACLYSMIC force. The beam engulfs him in blinding light. Massive ENERGY EXPLOSION  the entire street SHAKES, dust clouds ERUPT, volumetric fog fills the air.

When the light clears, he stands COMPLETELY TRANSFORMED — eyes BLAZING with godly golden-blue power, energy aura RAGING violently around his entire body with visible electricity tendrils crackling, muscles VISIBLY ENHANCED and defined, face twisted in COLD RAGE and predatory intensity.

He breathes heavily, stares at the goons with KILLING INTENT. The goons freeze in ABSOLUTE TERROR.

First goon CHARGES desperately forward. The fighter EXPLODES into motion with IMPOSSIBLE SUPERHUMAN VELOCITY. DEVASTATING PUNCH  fist CRACKS through air with SONIC intensity. SLOW-MOTION IMPACT  shockwave visible, goon's face CONTORTS in agony, blood SPRAYS, body LAUNCHES like ragdoll 20 feet backward, CRASHES through brick wall with BONE-CRUSHING force, debris ERUPTS everywhere.

PART 2 -

LOCATION DETAIL (Escalated): Same urban street, now a DEMOLITION ZONE. Concrete cracked and breaking. Brick wall partially destroyed from first impact. Metal railings BENT and snapping. Wooden crates and boxes SPLINTERED. Pillars showing cracks spreading. Golden hour light now more dramatic with darker blue shadows. Heavy dust and debris particles in air. Total DEVASTATION visible.

CAMERA ANGLES & CINEMATOGRAPHY:

15-17s: WIDE SHOT showing street arena. Camera pulls back to show scale of destruction and two remaining enemies. High-angle shot showing ground cracks
17-19s: RAPID MULTI-ANGLE FIGHT EXCHANGE alternating extreme close-ups and medium shots. Fast cutting every 0.3-0.5 seconds matching fight tempo:
Close-up on second goon's face as he launches kicks (intensity capture)
Low-angle shot of fighter's parries
High-angle overhead shot of exchange
Side profile close-up on impact moments
19-21s: MID-AIR GRAB SHOT from side angle as fighter lifts goon. Camera positioned at exact moment of lift showing superhuman strength
21-22s: VIOLENT SLAM SHOT  camera positioned ground-level looking upward as goon is SLAMMED onto concrete. IMPACT slow-motion, cracks SPREAD like spiderwebs across ground, dust ERUPTS upward
22-24s: THROW SEQUENCE  camera tracks throw trajectory. Goon FLIES through wooden crates, structures BEND and SHATTER, camera follows impact (tracking shot from side)
24-26s: INTENSE FINAL FIGHT EXCHANGE with scarred leader. Rapid multi-angle cuts showing:
Low-angle shot of fighter's punch
High-angle overhead of counter-attack
Close-up on scarred goon's face showing desperation
Metal railings BENDING in background from force
26-27s: EXTREME CLOSE-UP on fighter's fist as it CHARGES energy. Golden-blue glow INTENSIFIES, electricity CRACKLING violently around fist. Camera macro-level, glow filling entire frame
27-28s: SLOW-MOTION FINAL PUNCH setup. Camera positioned LOW-ANGLE BEHIND punch trajectory. Fist PULLS BACK with godly force visible (air distorting around fist)
28-29s: CATACLYSMIC IMPACT SLOW-MOTION. Camera positioned to capture scarred goon's face as punch connects. Eyes go WIDE in SHOCK, body CONTORTS from impact force, entire body LAUNCHED backward with EARTH-SHATTERING velocity
29-30s: PILLAR DESTRUCTION SHOT camera positioned wide to show goon CRASHES through concrete pillar like PAPER, pillar EXPLODES into massive chunks, structure COLLAPSES, debris MUSHROOMS into air, dust cloud engulfs entire area. Final frame: TIGHT CLOSE-UP on fighter's face from straight-on angle. Eyes still BLAZING with power. Breathing HEAVILY, chest HEAVING. Energy aura SLOWLY FADES. Cold MERCILESS confidence in stare. Fade to black.

STORY BEATS:

Second goon attempts RAPID KICK COMBO  fighter PARRIES with BLINDING speed. Each block CRASHES with SONIC booms. GRAB  he SLAMS goon down VIOLENTLY onto concrete, CRACKS spread like spiderwebs. THROW goon FLIES through wooden boxes, metal structures BEND and SHATTER from impact force.

Third goon  scarred leader, last hope  steps forward DESPERATELY. This is BRUTAL WARFARE. EXPLOSIVE hand-to-hand combat: PUNCH blocked, COUNTERATTACK devastating, SPINNING KICK with BONE-BREAKING force, GRAPPLE with SUPERHUMAN pressure. Ground SHATTERS beneath them. Metal railings BEND and SNAP. Every collision sends SHOCKWAVES across street.

FINAL MOMENT  fighter CHARGES energy into fist. Fist GLOWS BLINDING GOLD-BLUE. Pulls back with GODLY FORCE. Unleashes CATACLYSMIC POWERED PUNCH.

SLOW-MOTION IMPACT  scarred goon's body CONTORTS, eyes WIDE in SHOCK, LAUNCHED backward with EARTH-SHATTERING velocity, CRASHES THROUGH concrete pillar like PAPER, pillar EXPLODES into massive chunks, entire structure COLLAPSES, dust MUSHROOMS into air.

Fighter stands alone in TOTAL DEVASTATION. Breathing HEAVILY, chest HEAVING, eyes still BLAZING. Energy aura SLOWLY FADES. Stares DIRECTLY at camera with COLD MERCILESS confidence.
```

</details>

<sub>Source: <a href="https://x.com/itsshara_ai/status/2082892924694712509">https://x.com/itsshara_ai/status/2082892924694712509</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 38 · Cyberpunk Ice-Blue Character Awakening

<sub>astro &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1280×720 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2082830892209221921.jpg" alt="Cyberpunk Ice-Blue Character Awakening" width="100%">](https://x.com/ainextastro/status/2082830892209221921)

<sub><b>▶ <a href="https://x.com/ainextastro/status/2082830892209221921">Watch the clip on the creator's post on X (@astro)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>An H3 output for Cyberpunk Ice-Blue Character Awakening. This page retains the original X source link. The public Prompt is preserved verbatim without translation, rewriting, or completion. Hosted-video output: 15s · 1280×720.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,975 characters)</summary>

```text
Use the uploaded image as the exact source image and first frame. Preserve the original character design, composition, face, pale skin, glowing icy blue eyes, braided black hair, cybernetic head implants, exposed mechanical neck and chest structure, white and cobalt-blue jacket, blue serpentine mechanical creatures, labels, symbols, and the clean white background. Keep the result extremely faithful to the original illustration. The animation should feel like the original artwork has come alive, not been redesigned.  Create a premium, stylish, high-end anime animation with a refined cyberpunk aesthetic. The overall impression should be elegant, cold, hypnotic, dangerous, and visually luxurious. Emphasize precise Japanese anime craftsmanship: crisp linework, beautiful cel shading, highly detailed mechanical rendering, controlled highlights, graceful motion, and strong temporal consistency. The animation should look polished, expensive, and intentional.  The central character remains calm, dominant, and nearly still. She faces forward and maintains an unwavering, piercing gaze directly into the camera. Her expression is cool, emotionless, intelligent, and slightly predatory. Avoid exaggerated acting. Only subtle micro-movements are allowed in her eyelids, breathing, neck posture, and facial tension. Her presence should feel powerful even in stillness.  The main animated elements are the multiple blue mechanical serpents surrounding her. They move with smooth, layered, snake-like elegance. Each serpent has slightly different timing, path, and rhythm, so the movement feels organic and sophisticated rather than synchronized. Their bodies undulate in natural S-curves with believable weight, inertia, and continuous motion. Some serpents slowly raise their heads, some glide across her shoulders and around her face, some tighten or loosen their coils, and some subtly cross behind or in front of the composition to reshape the frame. Their movement should feel alive, hypnotic, and controlled, never frantic. Preserve the segmentation, scale texture, metallic fittings, joints, and cable-like details. Small articulated components should shift with delicate mechanical precision.  Her long green tongue moves like a real serpent tongue but remains elegant and stylized. It slowly extends, retracts, and sways with controlled, organic softness. The forked tip performs subtle tasting-the-air flicks. The tongue should feel eerie, sensual, and mesmerizing, never comedic. The tongue motion should complement the serpents’ motion, acting like a focal accent that draws attention toward her mouth and face.  Add subtle secondary motion throughout the scene. Her shoulders and upper torso rise and fall gently with slow breathing. Tiny motions should ripple through the hood, jacket folds, loose blue fabric, fine cables, and a few hair details. The exposed mechanical chest and neck assembly should feel alive through micro-movements: slight cable tension shifts, minute piston adjustments, tiny joint rotations, and restrained vibration. These details must remain subtle and tasteful, never distracting from the face and serpents.  Lighting should remain clean and striking. Preserve the white background and the strong graphic contrast between the white, cobalt blue, black mechanical detailing, and neon green tongue. Let reflections glide softly across the blue serpents’ scales and metallic joints. Metallic parts in the neck and chest may shimmer subtly. The green tongue should remain a vivid accent with slight wet gloss or faint luminous emphasis. Maintain a polished illustration-like finish while introducing dimensionality through moving highlights and soft shadow transitions.  The camera should perform an extremely slow and smooth frontal dolly-in over the full 15 seconds. The framing begins as a stable medium close-up and gradually becomes slightly tighter and more intense. The camera should never move abruptly. No shake, no tilt, no sudden zoom, no spinning, and no dramatic reframing. The face, eyes, and tongue should become increasingly dominant as the sequence progresses, while the surrounding serpents continue to frame the composition. The movement of the camera should feel cinematic and hypnotic, reinforcing tension through slow approach.  Structure the motion over the 15-second duration with deliberate pacing:  Seconds 0–3: begin in near stillness. Only the faintest breathing, tiny hood and cable motion, and a barely perceptible serpent twitch. Establish tension and the character’s unwavering blue-eyed stare.  Seconds 3–6: the serpents begin to awaken. One or two serpents slowly lift their heads and start gentle undulating motion. Reflections start traveling across their blue surfaces. The tongue begins a slight side-to-side sway.  Seconds 6–9: more serpents join the motion. The body language of the serpents becomes richer and more layered, circling her shoulders and face with elegant S-curve motion. The tongue extends a little farther and retracts slowly, with subtle fork-tip flicks. The camera continues its slow push inward.  Seconds 9–12: reach the most hypnotic phase. The serpents are now fully active but still graceful and controlled, framing her face dynamically. Their movement should feel luxurious and predatory. The tongue performs its most visually striking serpent-like motion here, synchronized with the heightened tension. Highlights glide across scales and metal details. Her gaze remains locked and emotionally unreadable.  Seconds 12–15: sustain and slightly resolve the intensity. The serpents continue moving but begin to feel more settled, as if entering a poised equilibrium. The camera reaches its closest framing, emphasizing her eyes and green tongue while still preserving enough serpents in frame for visual impact. End on a powerful, composed, hypnotic final moment that feels elegant and complete.  The emotional tone should be futuristic, eerie, sensual, intelligent, and luxurious. The final result should resemble a high-budget anime opening shot or a premium animated key visual. Prioritize elegance, polish, and controlled visual storytelling over excessive motion. Every motion should feel deliberate and aesthetically composed.  Maintain strict model fidelity and visual stability. Do not alter the character’s face shape, eye design, hairstyle, skin tone, clothing, mechanical anatomy, serpent design, or color palette. Do not add new objects, extra serpents, extra tongues, extra limbs, or background elements. Do not morph the face or let the eyes drift. Do not let the serpents fuse together unnaturally or intersect in broken ways. Do not allow clipping through the body or clothing. Do not change the jacket symbols or graphic details. Do not shift into 3D, live action, or a different illustration style. Avoid flicker, line wobble, perspective drift, detail melting, unstable anatomy, scale inconsistency, random deformation, abrupt motion, or composition changes.
```

</details>

<sub>Source: <a href="https://x.com/ainextastro/status/2082830892209221921">https://x.com/ainextastro/status/2082830892209221921</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 39 · Manga Characters Race Through Dense Motion Graphics

<sub>goldwing &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 17 &nbsp;·&nbsp; 864×480 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2092385200420647307.jpg" alt="Manga Characters Race Through Dense Motion Graphics" width="100%">](https://x.com/goldwing_zoome/status/2092385200420647307)

<sub><b>▶ <a href="https://x.com/goldwing_zoome/status/2092385200420647307">Watch the clip on the creator's post on X (@goldwing)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>Manga figures, motorcycles, silhouettes, and oversized English typography stack at high speed in a visual opener with a mid-2000s feel. Native-video output: 17s · 864×480. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (7,603 characters)</summary>

```text
Create a fast-paced 19-second motion-graphics video inspired very closely by the visual structure, editing rhythm, composition.

Overall style:
High-energy Japanese music-video / motion-graphics aesthetic from the mid-2000s.
A mixture of graphic design, manga-style comic illustrations, anime-style character art, silhouettes, photographic textures, particles, and bold typography.
The video must feel like a professionally edited promotional opening rather than a normal narrative scene.

Use the entire screen continuously.
Avoid static shots.
Every few moments, the composition must transform, rotate, slide, zoom, blur, or transition into the next composition.

IMPORTANT CHARACTER STYLE:
All male and female characters must appear as clearly illustrated comic / manga characters.
Do not use photorealistic humans.
Use expressive manga/anime-style faces, strong line art, dynamic poses, slightly exaggerated proportions, and graphic shading.
Characters may appear as full body silhouettes, medium shots, or extreme close-ups.
Show both male and female characters throughout the video.

IMPORTANT TEXT RULE:
Never generate random letters, fake words, unreadable pseudo-text, distorted paragraphs, or meaningless symbols.
Do NOT fill the screen with fake text.
Only use a very small number of clean, readable words:
"ARE YOU READY?"
"LIVE"
"MUSIC"
"COMING SOON"
All typography must be large, clean, correctly spelled, and intentionally designed.
If accurate text cannot be rendered, omit the text instead of generating gibberish.

0.0–2.0 seconds:
Begin with a dark navy and black graphic background.
Thin technical lines, transparent rectangles, subtle grids, and small comic-image fragments appear rapidly.
A manga-style female character appears briefly inside a rectangular graphic frame.
The camera pushes forward rapidly through several overlapping graphic layers.
Use diagonal composition and strong depth.
The scene should immediately feel like a music-video opening.

2.0–4.0 seconds:
Hard transition into a powerful dark-blue graphic composition.
A large white manga-style male silhouette moves dynamically across the screen.
Behind him, enormous abstract circular graphic elements rotate.
Large clean typography reading "MUSIC" appears briefly, integrated into the composition.
The typography moves diagonally while the character and circular elements move independently.
Camera sweeps rapidly from left to right and slightly rotates.

4.0–6.0 seconds:
Transition through a fast radial zoom.
A dark red and black ornamental background appears with circular patterns and glowing highlights.
A comic-style female face briefly emerges from the darkness.
Her eyes and hair move subtly.
The camera rotates around the graphic center while the background pattern continuously rotates in the opposite direction.
A clean "COMING SOON" title appears briefly and then is swept away by motion blur.

6.0–8.0 seconds:
Extreme close-up of a colorful manga-style female character.
Bright orange, red, purple, and green colors.
Strong expressive eye.
Hair moves dynamically as if hit by wind.
The camera rapidly moves sideways across her face, then zooms extremely close into the eye.
The eye becomes a transition point into the next scene.
Use motion blur and fast directional movement.

8.0–10.0 seconds:
Break the image into multiple manga comic panels.
Show several different comic-style male and female characters in separate panels:
a male character standing,
a female character looking toward the camera,
a group of young comic characters,
and a dynamic musician-like character.
The panels slide, overlap, rotate slightly, and rapidly change size.
Do not make the panels static.
Camera travels diagonally across the entire composition.
Use white backgrounds, black manga line art, and occasional red accent graphics.

10.0–12.0 seconds:
Suddenly switch to a high-contrast white manga illustration.
A comic-style male character and female character appear together in a dramatic pose.
Use strong black ink outlines and halftone manga shading.
The camera rapidly zooms toward the characters.
Then rotate the entire comic panel approximately 20–30 degrees while additional graphic fragments fly past the camera.
Create the feeling of flipping through a manga at extremely high speed.

12.0–14.0 seconds:
Cut into a dark blue and black particle field.
Thousands of small bright particles move toward and past the camera.
The camera travels forward through the particles.
Occasionally reveal faint silhouettes of manga characters inside the particle cloud.
The particles accelerate strongly toward the end of the shot.
Use depth, parallax, and cinematic motion blur.

14.0–16.0 seconds:
Transition into a clean blue graphic composition.
Show a white silhouette of a motorcycle with a comic-style rider.
The motorcycle moves from left to right.
The rider's body and hair/clothing move naturally.
Large clean text "ARE YOU READY?" appears briefly near the motorcycle.
The camera tracks sideways with the motorcycle, then overtakes it with a fast lateral camera move.
Use flat graphic design mixed with subtle depth.

16.0–17.5 seconds:
Rapid montage of comic-style musicians and characters.
Show a male vocalist, a female character, a guitarist, and several comic-style people in dynamic poses.
They should move independently: head movement, hair movement, arms, body movement, instruments moving.
Use a white background with black manga line art.
Quick zooms and diagonal wipes connect each character.
Do not make the characters look like frozen illustrations.

17.5–19.0 seconds:
Everything rapidly collapses into a dark background.
Graphic fragments and particles fly toward the center.
A clean white logo-like title appears:
"LIVE"
Then the title rapidly becomes smaller while the camera pulls backward.
Finish on a clean black screen with a subtle glow and a professional music-promo ending.
No random text.
No meaningless symbols.

CAMERA AND EDITING:
Extremely active camera throughout the entire 19 seconds.
Use rapid push-ins, pull-backs, left-to-right tracking, right-to-left tracking, diagonal movement, orbital rotation, Dutch angles, whip-pan transitions, rotational transitions, and extreme zooms.
Do not rely mainly on forward/backward camera movement.
Frequently change camera direction.
Characters and graphic objects must also move independently from the camera.
Use strong parallax between foreground, middle ground, and background.
Use motion blur during transitions.
Use occasional sharp freeze-like moments lasting only a fraction of a second before immediately transitioning again.

VISUAL LANGUAGE:
Mid-2000s Japanese music promotion / experimental motion graphics.
Manga panels mixed with modern graphic design.
Bold black-and-white comic artwork contrasted with dark navy, deep red, white, orange, purple, and electric blue.
Layered compositions.
Diagonal typography.
Circular graphic motifs.
Halftone manga textures.
Film grain.
Light streaks.
Particle effects.
Fast zooms.
Graphic wipes.
High contrast.

Most important:
The video must feel like one continuous, highly energetic graphic sequence.
Do not create a normal story.
Do not create long running scenes.
Do not leave characters standing still.
Do not use meaningless text.
Do not use photorealistic people.
Do not use generic corporate motion graphics.
Keep the visual density high from beginning to end.
Match the reference video's rapid montage feeling, graphic layering, manga imagery, strong silhouettes, extreme close-ups, particles, motorcycle imagery, and aggressive camera movement while creating original artwork.
```

</details>

<sub>Source: <a href="https://x.com/goldwing_zoome/status/2092385200420647307">https://x.com/goldwing_zoome/status/2092385200420647307</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

### 40 · A Yamanba Gal Transformation That Keeps Escalating

<sub>すーさん &nbsp;·&nbsp; T2VA &nbsp;·&nbsp; 15 &nbsp;·&nbsp; 1344×768 &nbsp;·&nbsp; landscape</sub>

[<img src="https://raw.githubusercontent.com/callirra-ai/minimax-h3-video-atlas/main/assets/community/x-2092371886961578401.jpg" alt="A Yamanba Gal Transformation That Keeps Escalating" width="100%">](https://x.com/su_nagomi/status/2092371886961578401)

<sub><b>▶ <a href="https://x.com/su_nagomi/status/2092371886961578401">Watch the clip on the creator's post on X (@すーさん)</a></b> — the video stays on the creator's own post; it is not re-hosted here.</sub>

<sub>A character layers hair color, makeup, accessories, and platform boots onto a simple Y2K look before landing in a dense Japanese-typography fashion spot. Native-video output: 15s · 1344×768. The creator published the complete prompt, preserved here verbatim.</sub>

<details>
<summary><b>Prompt</b> — published by the creator, reproduced verbatim (6,460 characters)</summary>

```text
# 『YAMANBA TRANSFORM』15秒 詳細台本  尺：15秒｜画角：9:16縦型｜1080×1920｜スタイル：実写ファッションCM／平成ギャル／ヤマンバギャル／Y2K／変身シークエンス／巨大タイポグラフィ／高速モーショングラフィック｜テーマ：「足す。足す。まだ足す。」｜サブテーマ：「MORE IS MORE.」｜主人公：20代女性。同一人物固定。開始時はシンプルなY2Kストリートルック。変身後は濃い日焼け肌、白く強調した目元と鼻筋、淡い白〜ピンク系リップ、ハイトーン金髪＋白・ピンクメッシュ、大量ヘアアクセ、長いデコネイル、白ファー、レオパード、チェーン、ミニスカート、巨大厚底ブーツを組み合わせたヤマンバギャル。奇抜さは強調するが、常にハイファッション広告として美しく見せる。｜音楽：平成ユーロビート×Hyperpop×Fashion Club Electro、BPM154〜158。4つ打ちキック、クラップ、明るいシンセリード、Bubblegum Bass、デジタルボイスチョップ、カメラシャッター音。0〜8秒は段階的に音を増やし、8.6秒で一瞬ブレイク、9.8秒からフルビートで限界突破、13.2秒以降はエンドカード用の大きな2ヒット。 CUT01｜0.0–1.2秒｜BEFORE「足りない。」 Visuals：完全な白背景。主人公が中央に正面立ち。髪は明るいブラウン〜金髪だが装飾は少なく、メイクも控えめ。シンプルなY2Kトップス＋ミニスカート＋普通のスニーカー。画面右側には縦長の全身ミラー。主人公が鏡の中の自分を一瞬見てからカメラへ視線を戻す。画面上部の余白に巨大日本語「足りない。」が出現。 Camera：50mm、胸上から開始。0.0〜0.6秒はほぼ固定、0.6秒から顔へ約8％だけ静かにドリーイン。 Motion：主人公は片眉をわずかに上げ、鏡を見て「違う」と感じるような表情。身体はほぼ静止。 Lighting：クリーンな白色ビューティーライト。影は非常に浅い。広告撮影のビフォー状態として美しく見せる。 VFX：ほぼ無し。文字出現時だけごく薄い黒のスキャンライン。 SFX：小さなヒール／靴音「コツ」→音楽開始直前の低いベース。 Text/Telop：「足りない。」 Emotion：違和感、物足りなさ、変身前の静けさ。 Transition：主人公が指を鳴らす瞬間に白フラッシュ。 CUT02｜1.2–2.5秒｜HAIR「もっと。」 Visuals：白フラッシュ後、顔の超接写。主人公の髪が一気にハイトーン金髪へ変化し、白メッシュ、ピンクメッシュが走る。左右から星、ハート、蝶、カラフルなクリップ、ビーズ、ミニリボンが高速で飛び込み、髪へ次々装着される。髪のボリュームも一段大きくなる。 Camera：85mm顔接写から開始。0.2秒で35mm相当まで急激にプルバックし、髪全体を見せる。最後に約10°だけ右ロール。 Motion：主人公が頭を左から右へ振る。髪の動きと逆方向からアクセサリーが飛び込む。 Lighting：白キー＋ピンクとシアンの細いリムライト。髪の艶を強調。 VFX：アクセサリー装着時に小さな星形フラッシュ。印刷ズレ、微細なクロマティックオフセット。 SFX：パパパパッ→キラッ→ドン。 Text/Telop：巨大「HAIR!」＋小さく「もっと。」 Emotion：最初の変化による爽快感。 Transition：巨大ヘアクリップがレンズ前を横切る。 CUT03｜2.5–3.8秒｜MAKE「まだ。」 Visuals：主人公の顔を真正面から接写。メイクブラシがレンズ前を横切るたびに変身が進む。1回目で日焼け肌が深くなる。2回目で目元が白く強調。3回目で鼻筋に白いハイライト。4回目でラメと強いアイライン。最後に淡い白〜ピンク系リップが完成。 Camera：70mm、顔の正面。ブラシの動きに合わせて左右へ短い3〜5cmのスライド。最後の0.2秒だけ軽くプッシュイン。 Motion：主人公はほぼ静止し、目線だけブラシを追い、最後に正面を見る。 Lighting：硬めのビューティーキー。白い目元・鼻筋・ラメに明確なスペキュラーを作る。 VFX：ブラシの軌跡が白、ピンク、シルバーのグラフィックストロークへ変化。 SFX：サッ！サッ！サッ！→パッ。 Text/Telop：「MAKE!」＋小さく「まだ。」 Emotion：変身が明確に加速する。 Transition：最後の白ブラシストロークが全面を塗りつぶす。 CUT04｜3.8–5.0秒｜NAILS「盛る。」 Visuals：指先の超マクロ。最初は普通の短いネイル。主人公が指を広げる瞬間、ネイルが物理的に伸び、ピンク、白、シルバーの超ロングネイルへ変化。ハート、ラインストーン、星、チェーン、小さな立体パーツが「カチッ、カチッ」と追加される。背景は黒に切り替わり、指先だけが明るく浮かぶ。 Camera：100mm macro。左手の小指から親指へ横スライドし、そのまま右手へ短いウィップ移動。 Motion：主人公が指を広げる→ネイルが伸びる→最後に両手で顔の横をフレーミングする。 Lighting：爪の艶を最大化する細いトップライト＋小さなリム光。 VFX：ラインストーン装着時に極小のスパーク。背景に細いゼブラ柄ラインが一瞬だけ出現。 SFX：カチッ、カチッ、カチッ→キラッ。 Text/Telop：巨大「盛る。」 Emotion：過剰さを楽しむ。 Transition：両手がレンズを一瞬完全に覆う。 CUT05｜5.0–6.3秒｜ACCESSORIES「MORE! MORE! MORE!」 Visuals：両手が開くと、主人公は胸上ショット。首、耳、手首、腰へアクセサリーがビートに合わせて連続装着される。巨大ピアス、複数ネックレス、ブレスレット、大ぶりリング、サングラス、デコ携帯、チェーンベルト。背景はピンク×ブラックのチェッカー。 Camera：35mm。最初は胸上。アクセが装着されるたびにカメラ位置も3段階で変化し、正面→斜め左→斜め右へ高速ジャンプ。 Motion：主人公は肩を振る→サングラスを上げる→デコ携帯を持ち上げる。各動作を音楽の強拍に合わせる。 Lighting：ハードフラッシュ系。アクセサリーの金属とプラスチックに強い反射。 VFX：ステッカーバースト、プリクラ風ハート、ゼブラ柄、レオパード柄が0.2秒単位で切り替わる。 SFX：MORE!の各ヒットに「ドン！ドン！ドン！」 Text/Telop：「MORE!」→「MORE!」→「MORE!」 Emotion：映像も主人公も一気に過剰になる。 Transition：3つ目の「MORE!」が巨大化して全面ワイプ。 CUT06｜6.3–7.5秒｜FASHION「もっと派手に。」 Visuals：全身。衣装がレイヤー式に変身する。シンプルなY2K衣装の上へ黒×ピンクのトップス、レオパード柄、白ファー、チェーン、ミニスカート、大型ベルトが高速で重なっていく。最後にヤマンバらしい派手なシルエットが完成。 Camera：28mm。主人公の周囲を約100°左方向へ高速オービット。主人公自身は右方向へ回転し、カメラと逆方向の相対運動を作る。 Motion：主人公が両腕を広げて1回転。回転中に衣装が段階的に増える。最後に片脚を前へ出して停止。 Lighting：白キー＋マゼンタとライムのリムライト。ファーとチェーンの質感を強調。 VFX：衣装の切り替えごとに紙コラージュ的なリップル。背景グラフィックがストライプ→レオパード→ハートへ変化。 SFX：シュッ→バサッ→ジャラッ→ドン。 Text/Telop：「もっと派手に。」 Emotion：完成が近いと思わせる高揚感。 Transition：カメラが足元へ高速ティルトダウン。 CUT07｜7.5–8.6秒｜PLATFORM BOOTS「まだ足りない。」 Visuals：足元の接写。普通のスニーカーが映る。0.3秒だけ音楽が薄くなる。画面下部に「まだ足りない。」。次の瞬間、靴が巨大な白×シルバーの厚底ブーツへ一気に変形。主人公が強く踏み込むと、床のチェッカー柄が波紋状に外へ広がる。 Camera：35mmローアングル。靴へ高速プッシュインし、着地と同時に少しだけ上へ跳ねるような衝撃カメラ。 Motion：足を上げる→厚底に変化→「ドン」と着地。 Lighting：ブーツに白いトップライト。床面にはピンクの反射。 VFX：床の衝撃波、薄い星形スパーク、チェック柄の歪み。 SFX：一瞬無音→「ドォン！」。 Text/Telop：「まだ足りない。」 Emotion：最大の変身前フック。 Transition：着地衝撃で画面が一瞬ブラックアウト。 CUT08｜8.6–9.8秒｜QUESTION「完成？」 Visuals：黒背景。完成したように見える主人公が中央に全身で立つ。白いリムライトだけで輪郭を強調。巨大白文字「完成？」が画面中央に出現。主人公のサングラスが光を反射する。 Camera：50mm、完全正面。0.5秒だけごくゆっくり4％プッシュイン。 Motion：主人公は静止。0.4秒後にサングラスを少しだけ下げ、目だけカメラを見る。口角がわずかに上がる。 Lighting：超ローキー。ピンクと白の細いリムだけ。 VFX：ほぼ無し。文字にだけ軽いCRTちらつき。 SFX：音楽をほぼ止める。低いベース1音。 Text/Telop：「完成？」 Emotion：間、期待、次への溜め。 Transition：主人公が小さく首を傾けた瞬間に文字が消える。 CUT09｜9.8–11.3秒｜FINAL OVERLOAD「……まだ。」 Visuals：主人公の顔アップ。画面左に小さく「……まだ。」。直後、ショッキングピンクの背景が爆発的に出現。髪飾りがさらに倍増、ネックレス追加、ネイルに追加パーツ、サングラスがさらに派手な形へ。背景にはプリクラ、ゼブラ、レオパード、ハート、星、デコ携帯、ステッカー、巨大「MAX!」が次々飛び込む。画面全体まで“盛られていく”。 Camera：85mm顔アップから18mm超広角まで1秒で急速プルバック。主人公の周囲に広がった巨大なヤマンバ世界全体を見せる。 Motion：主人公は髪を大きく振り、最後に両腕を広げる。背景オブジェクトは人物と逆方向へ放射状に飛ぶ。 Lighting：白キー＋ピンク、シアン、ライムの多色リム。ただし顔色は自然に保つ。 VFX：プリクラ爆発、ハート、星、紙コラージュ、クロマティックズレ、2フレームフラッシュ。 SFX：フルビート復帰→MAX! MAX! MAX!の3ヒット。 Text/Telop：「……まだ。」→「MAX!」「MAX!」「MAX!」→最後に「YAMANBA!」 Emotion：限界突破、圧倒的な変身完成。 Transition：巨大「YAMANBA!」の文字の中をカメラが突き抜ける。 CUT10｜11.3–13.2秒｜HERO WALK「誰のためでもない。」 Visuals：真っ白なランウェイへ急変。完成したヤマンバギャルの主人公が一人、奥から真正面へ歩いてくる。前カットの情報量を大幅に落とし、メイク、髪、アクセ、衣装、厚底の完成形を見せる。左右の余白には何も置かない。 Camera：24mmローアングル。主人公が前進する速度と同じ速度でカメラが後退。最後0.4秒でややローから35mm相当の腰上へ軽くティルトアップ。 Motion：主人公は堂々と3歩。腕を大きく振らず、モデルウォーク。最後に中央で停止。 Lighting：クリーンなハイファッション照明。肌、白メイク、ファー、金属、厚底すべてが明確に読める。 VFX：ほぼ無し。髪と衣装の自然な揺れのみ。 SFX：ビートを少し薄くし、厚底のステップ音「ドン、ドン、ドン」を明瞭にする。 Text/Telop：小さく「誰のためでもない。」 Emotion：奇抜さから自己表現へ意味を転換。 Transition：3歩目の着地で床からショッキングピンクが上へせり上がる。 CUT11｜13.2–15.0秒｜END CARD Visuals：ショッキングピンク背景。主人公は画面中央やや下に全身で立つ。背後に巨大な白い円。上部に小さく「MORE IS MORE.」。中央に画面幅いっぱいの巨大「YAMANBA TRANSFORM」。下部に日本語「盛りすぎくらいが、ちょうどいい。」。右上に小さく「2000 → 2026」。余計な装飾は減らし、文字と主人公を主役にする。 Camera：基本固定。13.2〜13.7秒だけ約4％プッシュイン。その後完全ホールド。 Motion：主人公がサングラスを上げ、最後にカメラへ笑う。「YAMANBA TRANSFORM」が一度だけ着地バウンス。 Lighting：フラットな広告照明。白い円が髪の輪郭を分離。 VFX：最後に星形フラッシュ1回。14.7秒以降は完全静止。 SFX：ドン！→低いベースヒット→カシャッ！ Text/Telop：「MORE IS MORE.」「YAMANBA TRANSFORM」「盛りすぎくらいが、ちょうどいい。」「2000 → 2026」 Emotion：変身の爽快感と自己表現の強さを同時に残す。 Transition：15.0秒終了。 【変身の連続性ルール】主人公の顔、骨格、髪の長さ、体型は全カットで同一人物として維持する。CUT01からCUT09へ向けて、変身要素を必ず積み上げ式に追加する。前のカットで装着された髪色、メイク、ネイル、アクセ、衣装が次カットで消失しない。CUT09が最大装飾量、CUT10とCUT11はその完成形をそのまま維持する。 【ヤマンバ表現ルール】日焼け肌、白く強調した目元・鼻筋、強いアイメイク、ハイトーン髪、大量アクセ、長いネイル、厚底などを特徴として扱うが、笑いもの・ホラー・怪物・汚れた表現にはしない。常に2000年代ギャル文化を現代のファッション広告として再構築したプレミアムな実写表現にする。 【カメラワークルール】毎カット同じドリーインを使わない。顔接写、プルバック、横スライド、マクロ追従、オービット、ティルトダウン、ローアングル、クラッシュアウト、トラッキングを分散する。人物とカメラを同方向に動かし続けず、相対運動を作る。激しい手ブレ、高速360°回転、顔が読めなくなるモーションブラーは禁止。 【タイポグラフィルール】使用する主要文字は「足りない。」「HAIR!」「もっと。」「MAKE!」「まだ。」「盛る。」「MORE!」「もっと派手に。」「まだ足りない。」「完成？」「……まだ。」「MAX!」「YAMANBA!」「誰のためでもない。」「MORE IS MORE.」「YAMANBA TRANSFORM」「盛りすぎくらいが、ちょうどいい。」「2000 → 2026」のみ。意味不明な日本語、文字化け、重複文字、余計なブランド名、ロゴ、透かしを生成しない。文字は字幕ではなく、画面の主役オブジェクトとして衣装やカメラの動きと連動させる。 【演出の核】この映像の見せ場は「完成形」ではなく「まだ足りない」を繰り返しながら限界まで盛っていくプロセス。0.0〜8.6秒は段階的変身、8.6〜9.8秒で一度完全に溜め、9.8〜11.3秒で最大爆発、11.3秒以降は完成した姿を静かに見せる。全編を騒がしくせず、静→増加→静止→爆発→静かなヒーローショットという強弱を明確にする。
```

</details>

<sub>Source: <a href="https://x.com/su_nagomi/status/2092371886961578401">https://x.com/su_nagomi/status/2092371886961578401</a> &nbsp;·&nbsp; prompt provenance: <code>creator-verbatim</code></sub>

---

## The size comparison

The same prompt rendered at three sizes. This is the question a gallery should
answer and almost none do: **what does the extra money actually buy?**

| | 480P | 768P | 1080P |
|---|---|---|---|
| Measured output | **864 × 480** | **1344 × 768** | **1920 × 1056** |
| Cost of a 6 s clip | ¥0.18 | ¥0.24 | ¥0.60 |
| Wall time | ~70 s | ~150 s | ~475 s |
| In this repository | 480P drafts | [01 Lantern on a Canal](showcase/01-lantern-canal/) | [03 One Stroke of Ink](showcase/03-ink-1080p/) |

**`1080P` is 1920 × 1056, not 1920 × 1080.** The model converges on a pixel budget rather
than a height, and the square tier is **1056 × 1056**, not 1080 × 1080. If you are cutting
into a 1080p timeline the height will not match.

**1080P costs roughly seven times the wall time of 480P** for the same six seconds — not
2.5×, which is what the price ratio suggests. In a batch that dominates everything else.

---

## What we measured

Fourteen probes, each checked against the MP4 that came back.

**[The full request matrix →](docs/what-we-measured.md)**

- **Every clip carries a native audio track** — 32 kHz stereo, generated in the same pass as
  the picture. There is **no parameter to turn it off**.
- **Requested duration is not delivered duration.** 5 s returns 5.167 s; 1 s returns
  1.625 s. The model snaps to a 17k+5 frame grid at 24 fps.
- **The tier enum is closed.** Asking for a resolution the workflow does not publish
  returns an error, never a silent fallback.

## What breaks

**[What breaks, and what to do instead →](docs/what-breaks.md)**

The one to read first: **faces in wide shots degrade regardless of input resolution.** The
fix is the shot list, not the prompt — put the identity read in a close-up and keep the wide
for backs and scenery. The rest of the page covers the audio layer (the least reliable part
of the model), the dead bracket syntax, and what a >15 s take does to continuity.

---

## How to use a case

1. **Watch the clip.** The line under it is the measured output, not the request.
2. **Copy the prompt** from `prompt.txt`. It is complete and filled; the field names are
   deliberate.
3. **Change one thing at a time.** If you change the camera *and* the lighting *and* the
   duration you will not know which one broke it.
4. **Draft at 480P, deliver at 768P.** A 480P test costs a fifth of a 1080P render and takes
   a fifth of the time. Look at the motion before paying for the take.

## Sizes and what comes back

| Requested | Measured output |
|---|---|
| 480P landscape · portrait · square | 864×480 · 480×864 · 480×480 |
| 768P landscape · portrait · square | 1344×768 · 768×1344 · 768×768 |
| 1080P landscape · portrait · square | 1920×1056 · 1056×1920 · 1056×1056 |
| 2K | 2560×1440 |
Every clip came back as **H.264 at 24 fps with an AAC stereo track at 32 kHz**, regardless
of size. Anything less than 4 seconds rounds up — the model snaps to a 17k+5 frame grid.

**Video-to-video is a different door.** H3 supports it through references, but the reference
path takes images and audio in the workflows we render with; driving a clip through the
model as an edit source needs the multimodal endpoint, where a reference video is one of the
accepted inputs alongside the images.

## Repository layout

```
README.md              this page
CATALOG.md             all 40 community cases as a plain table, no media
showcase/              our own clips: prompt, preview loop, poster, MP4, generation record
assets/community/      posters for the community gallery
docs/
  prompt-format.md     the documented field structure and vocabulary
  what-we-measured.md  the request matrix and the size comparison
  what-breaks.md       failure modes and the fixes
```

## Contributing

Clips and prompts are welcome. A community entry must arrive with **the creator's own
published prompt** and a link to their post — see [CONTRIBUTING.md](CONTRIBUTING.md).

## Credits and licence

Prompts and documentation in this repository: **CC BY 4.0**. Our clips: CC BY 4.0.
**Community prompts and videos remain the property of their creators** — each entry links to
its source, and the poster is stored here only so the gallery does not break when a
third-party host goes away. To request a removal, open an issue.

The community index this gallery is curated from is
[SkyNotSilent/awesome-MiniMax-H3-cases](https://github.com/SkyNotSilent/awesome-MiniMax-H3-cases),
which records the provenance of every prompt it publishes.

This is an independent resource. It is not affiliated with, endorsed by, or sponsored by
MiniMax.

**On the model licence:** the H3 weights ship under the
[MiniMax H3 Community License Agreement](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/LICENSE) —
**not** Apache-2.0 or MIT — and it defines **Excluded Territories: the European Union, the
United Kingdom, the Republic of Korea and the United States of America**. That governs the
weights, not the clips here, but read it before self-hosting.

---

<div align="center">

**If this saved you a render, a star helps other people find it.**

<img src="https://img.shields.io/github/stars/callirra-ai/minimax-h3-video-atlas?style=for-the-badge&label=%E2%AD%90%20Star%20this%20repo&color=bf8700" alt="Star this repo">

</div>
