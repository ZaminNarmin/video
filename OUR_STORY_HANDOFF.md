# OUR STORY — Production Handoff for the 2-minute engagement film

**For:** the next AI model (Claude Fable 5.2 or similar) that will build the full film.
**From:** the previous working session (12–23 Nov 2026). Everything below was learned by doing it, not guessed.
**Film:** "Our Story", ~2:00, 16:9, shown at the engagement (Nişan) on **27.12.2026**. The real proposal footage plays straight after it.

---

## 0. Read this first (the 12 things that matter most)

1. **The user wants REAL VIDEO, not animated photos.** In the first attempt, real photos were animated with tiny motion and 55 short clips were joined with dissolves. The user rejected it: *"Your last video is just animated photos not full normal video!!!"* Section 2 defines "real video" and how to test for it before showing anything.
2. **The faces must be the real faces from the user's photos in every shot.** The user said: *"We need same exact face for each moment in video so it will not look like generated but as real recording video."* Use only the photos the user sends. **Never** take faces from a reference video.
3. **The method that finally worked** (approved 25-second "Where it all began" result) is: a real full-motion video, then an identity-lock pass with **Higgsfield Genjutsu `hf_mult_replace_object`** using the face photos. Section 6 has the exact recipe.
4. **For the full film the user wants the videos made directly from their photos** so the faces are right from the first attempt. Section 7 explains how to do that: build each moving shot from the real photos, then always run the identity-lock pass.
5. **Keep the full PDF scenario** ("Our Story – AI video scenario, Draft 9", 6 chapters, 59 shots). Appendix B has every shot in full. Only the faces and the motion approach change.
6. **Ask the user questions with options for every 2 seconds of the film** (60 segments) before generating. Section 9 is the protocol. Appendix A is a pre-filled draft of all 60 segments built from the PDF.
7. **Her look:** long, straight, dark-brown hair, worn **down** (the user explicitly wanted her hair changed from an updo to long and down). **His look:** his face must look **slimmer, "not fat"** (user's words). He must still clearly be him.
8. **Modest film:** no kissing or hugging, no added touch (only touch that exists in their real photos), modest necklines, families and guests will watch.
9. **No numbers, years or dates on screen**, ever. The only allowed words are a few place names or a chapter feeling line.
10. **Ask before spending credits.** Show the plan and the cost, and get an OK before every paid batch. The balance was **570 credits** on 14 Nov 2026 (Higgsfield Ultra plan). The full film needs roughly 2,500–5,000 credits (Section 10).
11. **The user writes short messages from a phone.** Answer in short key points, under about 1,000 characters, and send no links. Use option questions (AskUserQuestion), not open essays.
12. Keep a **manifest file** of every job ID and file. Sessions restart and jobs take 5–35 minutes.

---

## 1. Goal and deliverable

- **One finished video file:** 1920×1080, 16:9, 24 fps, H.264 (CRF ≈17), AAC audio, **exactly about 2:00** (60 segments × 2 s).
- **Six chapters in PDF order:** University → Studying abroad → New Year together → Graduations and home → Army → Asking for her hand.
- It must look like it was **filmed**: people move, walk, turn, talk and laugh, and the camera moves with real parallax, in continuous takes with normal film editing.
- The faces of the couple must be **recognisably the real people in every shot**, including close-ups and side views.
- **The end:** the last AI shot (6.06, the tea glass) fades to soft white (6.07) and the real proposal footage follows. That footage is edited in separately and is not part of the 2:00.

---

## 2. What "real video" means (acceptance tests)

### 2.1 What the user rejected (do NOT do this)
- Real photo used as start frame **and** end frame, with "very subtle motion" and a "slow push-in": the people just breathe and smile in place, like a photo with a breeze.
- Each clip trimmed to its first ~2 s (because faces drifted later) and then 55 such clips joined with cross-dissolves. The result is a slideshow.
- Widening portrait photos to 16:9 and animating them while the people stay frozen in their photo poses.

### 2.2 What the user approved
The 25-second "Where it all began" result (ask the user to attach `where-it-all-began-v2.mp4` as the quality bar). It has continuous action across several shots: she packs her bag and stands up, walks down a corridor, a man walks toward camera, close-up shy smile with a hand gesture, they pass each other, he looks back over his shoulder and smiles. The camera moves, the editing has real cuts, and the faces belong to the real couple.

### 2.3 Hard acceptance tests for every shot (run before showing the user)
| Test | Pass condition |
|---|---|
| **Action** | In every 2-second segment, a person visibly changes pose or position (walks, turns the head more than ~30°, gestures, sits or stands, laughs), **or** the camera moves with parallax (dolly, track, orbit, handheld). Breathing, blinking or hair in the wind alone = FAIL. |
| **No frozen photo** | The first and last frame of a clip must not be near-identical. Grab them (`ffmpeg -i clip.mp4 -frames:v 1 first.png`; `ffmpeg -sseof -0.1 -i clip.mp4 -frames:v 1 last.png`) and compare (`ffmpeg -i first.png -i last.png -lavfi ssim -f null -`). SSIM > 0.90 between the first and last frame of a 5 s clip = FAIL (too static). Never use start_image = end_image. |
| **Faces** | Pull 3 frames per clip (start, middle, end). Put each face crop next to the user's reference photos. Both people must be clearly recognisable, from the front **and** in profile. If not, re-run the identity-lock pass (Section 7.5). |
| **Continuity** | Same outfit, hair and props across all shots of one scene. Her hair stays long and down unless the user chose otherwise for that scene. |
| **Rules** | No text or numbers, no added touching, modest clothes (Section 5). |
| **Editing** | Shots are 2–6 s continuous takes cut like a film (wide → medium → close, shot/reverse-shot). Use dissolves only between chapters or where the user asks. |

---

## 3. Inputs: what to ask the user to attach, and what already exists

### 3.1 Files the user should attach to the new chat
1. **This handoff file.**
2. **The PDF:** "Our Story – AI video scenario (draft 9)" (39 pages). It contains all real photos (C1_…–C6_… files), embedded. Extract them with `pdfimages -j -png file.pdf outdir/`. Each shot's photo names are listed in Appendix B.
3. **Her face photos (7):** 5 car selfies (`IMG_0180`–`IMG_0184`: three front views, one three-quarter glance, one near profile) and 2 side views in a red-and-white striped sweater (`IMG_0217` facing left, `IMG_0218` facing right).
4. **His face photos (7):** `IMG_0210`–`IMG_0216`: front, two three-quarter views, chin-up (do not use, it makes the face look heavier), front smile, profile facing right, profile facing left.
5. **Optional:** the couple photo (her in a red dress with pink roses, him in a navy suit). It is good for proportions and height, but **do not let his suit leak into other scenes** (see failures).
6. **Quality reference:** the 25 s source video the user sent (`VIDEO-2026-11-12-16-20-21.mp4`, someone else's AI clip of chapter 1) and the approved result `where-it-all-began-v2.mp4`.

### 3.2 Already uploaded to the user's Higgsfield account (reuse these media IDs; re-upload if one does not resolve)
**HER (use all 7 together):**
| Photo | Media ID | Use for |
|---|---|---|
| Car selfie, front 1 | `2da05287-989d-4f73-b422-123034fd0218` | main front reference |
| Car selfie, front 2 (chin up) | `4daf1276-2811-4e8e-8aea-9d3003c2718a` | front |
| Car selfie, front 3 (head tilted, soft smile) | `41f5b68e-08e0-4801-8486-e564395d1b53` | front / smile |
| Car selfie, three-quarter (glancing left) | `b89ff7c1-7b8b-43a9-bb17-3014e2bd273b` | 3/4 shots |
| Car selfie, near profile (looking right) | `db1e4ae2-24ae-4e80-a0b2-afc5122c317d` | profile shots |
| Side view, facing left (head crop) | `8a72e9e6-8d08-478a-b1b0-c4344f25d235` | profile shots |
| Side view, facing right (head crop) | `f3d0d9f1-aad8-4e70-8d8e-12238d42abd9` | profile shots |

**HIM:**
| Photo | Media ID | Use for |
|---|---|---|
| Front (real, head crop) | `4c8cf164-b48f-4b32-b69f-7f1dc5a90c39` | reference |
| 3/4 looking image-left (real) | `107953f7-ce5d-40f9-bb11-52ae3a904be9` | reference |
| 3/4 looking image-right (real) | `8609eba7-72f1-4b14-8e8f-bff3a031e109` | reference |
| Front smile (real) | `313af5fa-96e5-4bff-ad2f-1d1b642b509d` | reference |
| Profile facing right (real) | `558ca02d-4e66-4b31-96c8-e75c0837b833` | profile shots (use real profiles) |
| Profile facing left (real) | `74a8f324-e758-4241-9259-c926dfe4cdcc` | profile shots (use real profiles) |
| **Slim** front, navy crew-neck, beige wall (FLUX edit of the real front) | job `9c080945-8f51-4994-95a7-5f055dad4441` | **preferred identity ref** |
| **Slim** 3/4, navy crew-neck | job `346a172a-3e4e-470a-9ea3-3cb9f8365843` | **preferred identity ref** |
| **Slim** front smile, navy crew-neck | job `1c86ba92-c4b3-48b5-8fa5-b39d08b01582` | **preferred identity ref** |

The slim versions were approved in use: they made his face slimmer while keeping him recognisable. A slim *profile* edit (`d5b03454…`) was **rejected** because it changed his skin tone, so use the real profiles for side views. Job IDs of finished generations can be passed as `image_references` values directly.

**Old, weaker references (do not use as primary):** the garden portrait `15fe45e0…` (retouched; pulls the face toward a generic beauty face), small crops of him from the PDF photos (`c8c4e371…`, `78a1935c…`, `7df35b69…`, `96f5cb95…`, `bc544a8c…`), the Kling element "her-face" `f04d8979…` (made from the old references).

**Location photos already uploaded:** classroom `89867713-1b70-4801-85c9-99daf1dc5902`, corridor `d6918dfa-e718-40cd-92a9-a40b7574919e`, café `68cd9113-fbf4-4209-96fb-b9ef624eb032`, library `a0fb082b-17f8-498b-81ad-082cd7b06af0`, park bridge `a7f88443-1736-491e-ba06-eff428c4ad20`, airport terminal `e137404c-b47c-49ed-9648-29d78bca7386`, MSU building `9ac4bc04-f9fd-4cbf-8d0c-8583bcbb872b`, real serving-tea photo `79246d22-79d5-4a25-9086-35ecffb8a389`, Thames at night (16:9) `545612f8-abc8-4032-8dd8-0c56f872253c`, campus at dusk (16:9 widened) `44c60663-a114-44f3-8431-0f33f2e323d7`.

**Cleaned real photos (originals, years and watermarks removed):** 1.09 `8becebc3-647c-450c-af89-b2886722a2a7` · 1.10 `39ba888b-62e2-46f3-ba9c-25275ab9f080` · 1.11 `9e302a6d-4832-45d2-8b0a-7cb19b49cb0e` · 1.12 `0c36a0ea-ee86-482c-afaa-b4911f6f03ea` · 2.09 `49ad0831-f612-481f-9665-3b55f620b75f` · 2.10 `d4c55fc4-70d9-418b-9e51-e0e83a769188` · 3.03 `c38e70ed-b0db-4cda-9f0c-02fb94c311c9` · 3.05 `f90861da-6cac-4cbb-b441-1bbf6536c15a` · 3.07 `b43980eb-058f-4e7b-8e11-1008d6feeca4` · 4.01b `cd5e2fc2-5f97-46e7-b5e8-f9e9df3bdb17` · 4.02 `26692df3-b771-4d17-9ba0-4bb774ebc842` · 4.03 `4e6275b8-77f1-4ed2-bbcd-c491f2e1b8b1` · 6.01 `e9abbd5b-09f4-4be6-b1b8-f2e4e945972b` · 6.04 `46964ded-e4ad-48a8-a1a5-b7927a19ee10`.
**16:9 versions of those (real photo pasted back in the centre, AI-painted sides):** 1.10 `4a513be5-5b8b-4232-a174-18cef9088a50` · 1.11 `95fe9d91-ce54-4e08-bb5d-224c4cf8436f` · 1.12 `3d8614ce-898c-4b54-9a01-f4abba1c42a1` · 2.09 `a568a748-fbd5-4793-b9ee-a2a692662109` · 2.10 `64006f1f-97f3-422a-9f91-d158f1c35942` · 3.03 `99e9ca6d-81df-402e-af3a-5a0fdc6eb2c7` · 3.05 `e08a51f8-d596-40b9-8d3d-4434bbad83e2` · 3.07 `cbd5fc8a-0783-45cb-ab22-1b2a805e4076` · 4.01b `2ae4ab0c-d926-43f5-adbd-84ba152a28fe` · 6.04 `eb8f3642-0d9a-4f35-b8e8-f8b52e5626a4`.

**25 s reference video:** full clip `64ad9f18-5501-42dd-9f6f-a64752182587`.

---

## 4. Identity kit (how they look, and the rules for faces)

### HER
- Long, straight, glossy **dark-brown** hair with a centre part, **worn down** past the shoulders (default for every scene; ask if a scene should differ, e.g. graduation cap or the low bun in 6.05).
- Fair skin; round face with **full cheeks**; **thick, dark, defined eyebrows**; dark-brown eyes with long lashes and soft winged liner; **full lips** with a glossy nude-pink colour; soft natural makeup with a warm glow; small gold hoop earrings and a thin gold necklace often.
- When a generated face drifts, it usually becomes thinner and more "model-like" with a narrower jaw and smaller lips. That is wrong: keep her **round, full face**.

### HIM
- Tall, broad-shouldered. Short dark-brown hair, short on the sides, with a **receding hairline at the temples**. Straight dark eyebrows, brown eyes, slightly rounded nose, light stubble (the PDF says clean-shaven; his photos show light stubble, so ask the user).
- **Make his face slimmer** than in his photos: less fullness in the cheeks and under the chin, a more defined jawline. He must still be clearly himself and not look gaunt. Use the three *slim* references as primary identity refs and his real profiles for side views.
- When a generated face drifts, it becomes heavier, with a double chin and a different hairline. That is wrong.

### Rules that apply to both
- Every shot with the couple goes through the identity-lock pass (Section 7.5), even if the first attempt looks fine.
- References must be **head and shoulders only**, or in the **same outfit** as the target shot. Otherwise the model copies the clothes from the photo (his suit appeared in a shot where he wore a sweater).
- In the prompt, say **which reference images belong to whom, by order**, e.g. "the woman from the first seven reference photos … the man from the last six reference photos".
- Include **profile references** whenever the shot shows a face from the side.

---

## 5. Rules (from the PDF and from the user)

1. **Look:** real life, filmed like a movie, never cartoon or animation. Warm soft light, natural skin, light film grain.
   - PDF style line for every prompt: *"Photorealistic, cinematic, shot on 35mm film, natural skin texture, soft warm light, shallow depth of field, subtle film grain, slow gentle camera movement."* Keep "cinematic camera movement", but **replace "slow gentle" with real, motivated moves** (dolly, tracking, handheld) when the scene has action.
   - PDF negative prompt: *"cartoon, anime, illustration, 3D render, CGI look, plastic skin, distorted face, deformed hands, extra fingers, text, letters, numbers, logos, watermark."*
2. **Pace:** gentle and warm, with slow motion on emotional moments. The PDF asks for soft cross-dissolves between shots. Use them between scenes and chapters; inside a scene use real cuts (ask the user in Round 0).
3. **Frame:** 16:9, 1920×1080.
4. **No years, no dates, no numbers** anywhere, including phones, chat bubbles, signs, buses, number plates and shop names. Remove "2024" from photos. Time passing is shown only through outfits, seasons and light.
5. **Modest affection:** looks, smiles, standing close. Keep touch **only** as it is in their real photos. **Never** add kissing, hugging, a head on a shoulder or holding hands unless the real photo shows it. (A generated 3.06 shot added her head on his shoulder; it had to be cut.) Many guests and family will watch.
6. **Modest clothing:** high, closed necklines for her (crew neck, high collar, scarf). Generated outfits drifted to low necklines twice and had to be redone.
7. **On-screen text:** very little. At most one short line per chapter (place or feeling), added in the edit, never generated by AI. The PDF suggests: "Where it all began" (1.01), "Edinburgh" / "Michigan" (2.03), "Chicago" (2.10), "London" (3.02), "Baku" (4.05 globe).
8. **Signs with letters** (e.g. 6.01 "Hə Almağa Gəlmişik") must not change. Keep the real photo and only move the camera and light.
9. **Guests' faces** must never be visible in 6.05 (blurred dark suits only).
10. **Faces come only from the user's photos.** Never from a reference video or a generic generated face.
11. **Split screens** (a/b shots): her on the left half, him on the right half, looking toward each other, with matched light.
12. **Sound:** in the 25 s piece the original audio was kept. For the full film, ask in Round 0 (music track from the user, no sound, or AI music).

---

## 6. The method that produced the approved result (exact recipe)

**Task it solved:** keep a real-motion 25 s video exactly (shots, timing, clothes, movement, background, sound) and change only both faces and her hair.

| Step | What | Tool and settings | Cost and time |
|---|---|---|---|
| 1 | Find the cuts in the source: `ffmpeg -i src.mp4 -vf "select='gt(scene,0.25)',showinfo" -f null -` | ffmpeg | free |
| 2 | Cut it into **groups of two shots, 4–30 s each** (Genjutsu needs 4–30 s). Shots without the couple (aerial, atrium, wide hall) stay original. Upscale those with `upscale_video` provider `topaz`, 1080p. | ffmpeg; Higgsfield `upscale_video` | small |
| 3 | **Hair and outfit pass:** `generate_video` model `kling4_0`, `mode: "video-edit"`, `resolution: 1080p`, `duration` = group length, `medias`: `video_references` = group clip, `image_references` = her selfies. Prompt: "Edit the input video and change only … her long, straight dark-brown hair worn down … keep everything else exactly as in the input video: every shot and cut, timing, camera, body movement, expressions, clothes, background, lighting and all other people." | Kling 4.0 video-edit | **4 credits/s**; ~5–10 min. A whole 25 s clip **failed**; groups of ≤6 s worked. |
| 4 | **Identity lock:** `generate_video` model `hf_mult_replace_object` (Higgsfield Genjutsu), `resolution: 1080p`, `medias`: `video_references` = **the Kling-edited job ID** from step 3, `image_references` = her 7 refs + his slim refs + his real profiles. Prompt names each person by reference order and says: "Both keep exactly the clothes they wear in the source video … Keep their movements and expressions, both shots and the cut, the camera, the backgrounds and all other people exactly as in the source video." | Genjutsu | **~20 credits/s at 1080p** (120 per ~6 s); ~7 credits/s at 720p (42 per ~6 s). **15–35 min** per job. |
| 5 | **Check** faces next to the references (Section 2.3). Re-run any group that failed, with corrected references. | ffmpeg + OpenCV crops | — |
| 6 | **Assemble:** detect the cut inside each result, **retime each shot to the exact original shot length** (outputs come back 5.7–6.04 s for 5.9 s sources), concatenate, mux the **original audio**, 1920×1080, 24 fps, CRF 17. | ffmpeg (`assemble.py`, Appendix C) | free |

Total cost was about **40 credits per second** of final video.

**Why it worked:** the source already had real human motion. Kling video-edit can change hair and outfits while keeping motion, but it does **not** change faces. Genjutsu does change faces (and keeps motion, cuts and gestures) when it gets good references.

---

## 7. Production pipeline for the 2-minute film ("directly from the photos")

The user's answer: *"if possible just make videos directly from this current images so faces will be real and accurate from first attempt."*
So every shot starts from the user's real photos (real face pixels in the start frame, real faces as references), is generated with **full motion**, and then always goes through the identity lock.

### 7.0 First: one test scene before the big run (about 110 credits with a 720p lock, about 240 with a 1080p lock; ask first)
Run Route A on **1.01–1.03** (class ends → corridor look → shy smile), 8–10 s. Show the user a 3-frame sheet and the clip. Proceed only when the user says the faces and motion are right. Also test there whether `kling4_0` **`mode: "reference-to-video"`** with the face photos plus the location photo as `image_references` (or `kling_element_ids` from elements made with `show_reference_elements` / `manage_reference_elements` from the 7+7 photos) already gives correct faces in one pass. That was **not tested** in the previous session. If it does, the lock pass can be lighter. If not, use the A1–A4 chain below.

### 7.1 Route A: acted moments with no real photo (PDF "Create a start frame"; ≈52 s of the film)
- **A1 Start frame from the real face:** `generate_image` model **`flux_3_image`** (2k, 16:9). Edit a **real selfie** of her and/or a real photo of him into the scene: change only the background (use the location photo as a second reference), the outfit and the framing, with "keep the face exactly, do not retouch, beautify or slim". FLUX 3 keeps the real face; **Nano Banana redraws faces into generic ones, so do not use it for people.** About 3 credits. Optional: paste the real face pixels back (`facepaste.py` idea: SIFT-align the selfie to the edited frame, blend the inner-face ellipse, tone-match).
- **A2 Real motion:** `kling4_0`, `mode: "image-to-video"`, `start_image` = A1 frame, **no end_image**, `duration` 8–10 s, 1080p, 16:9. Write the prompt as **timed beats that match the user's 2-second answers** (e.g. "0–2 s she closes the notebook; 2–4 s she stands and swings the bag onto her shoulder; 4–6 s she walks toward the door, camera tracks with her; 6–8 s …"). Ask for real camera moves and say "her face, features, hair stay exactly as in the first frame". **Do not** put face photos in `image_references` in this mode: Kling cut away to those photos inside the video. About 3.25 credits/s at 1080p.
- **A3 Identity lock:** Genjutsu on the A2 clip (Section 7.5). Always.
- **A4 Check:** Section 2.3. Two-person shots need both faces locked in the same pass (list both people's refs, by order).

### 7.2 Route B: moments that have a real photo (PDF "Animate a real photo"; ≈46 s)
The real photo gives the true place, outfits and group. **It must become a real moment, not a moving photo.**
- **B1 Prepare:** clean the photo (remove "2024", watermarks, sign lettering; see Appendix B notes). Make it 16:9. Crop landscape photos. For portrait photos, widen with the **masked-inpaint method**: build a 16:9 canvas with the photo in the centre (`widen_prep.py`), then `nano_banana_2_1` with `is_inpaint: true` and the mask (paint only the sides). Then paste the real photo back over the centre and tone-match the seams (`composite.py … tone`). **Never** use `outpaint_image` on people (it repaints faces and changes their size).
- **B2 Real motion:** `kling4_0` image-to-video, `start_image` = B1 frame, **no end_image**, 8–10 s. Prompt the **story action around the photo moment**: e.g. 1.11 "they turn to each other, laugh, walk out from under the canopy toward camera, camera tracks backward"; 3.05 "they walk along the riverside railing, a boat passes, the camera cranes up to reveal Tower Bridge". The photo pose should be only one beat of the clip.
- **B3 Identity lock** for the couple (Section 7.5). **Family members:** the user has no face references for them, so large motion will change their faces. Ask the user (Round 0) whether to keep the families at medium/wide distance with gentle action, or whether they can send face photos of family members for a lock.
- **B4 Check.**

### 7.3 Route N: no identity needed (≈18 s): 1.08 campus dusk, 1.09 ceremony crowd, 2.04 two planes, 3.02 London street, 3.09 fireworks, 4.02 McEwan dome, 4.03 pipers, 6.01 sign, 6.02 table
`kling4_0` image-to-video from the photo with real camera and scene motion (time-lapse clouds, traffic, fireworks, crane or dolly moves). For 6.01 the letters must not change: use the real photo with a slow push-in done in the edit (ffmpeg zoompan or an OpenCV script; `extras.py sign` did this), or a careful light-only animation.

### 7.4 Route E: made in the edit (≈4 s)
- **2.07 chat bubbles:** phone-style panel over a blurred background; her castle photo, then his campus photo, then his Chicago photo slide in as white rounded bubbles; no names, times or dates (`extras.py chat1/chat2`).
- **4.05 night globe:** realistic night Earth with city lights; two glowing arcs from Michigan (42.73 N, −84.48 E) and Edinburgh (55.95 N, −3.19 E) meet over Baku (40.41 N, 49.87 E) with a soft flash; only the word "Baku" appears (`globe.py`, ready-made; 3.6 s; uses `global-land-mask` and `geonamescache`).
- **6.07:** fade the last frame of 6.06 to soft white over about 1 s, then the real proposal footage follows. Grade the AI film's end to match the colour of the real footage.

### 7.5 Identity-lock pass (Genjutsu, `hf_mult_replace_object`): exact rules
- Source = the generated motion clip (job ID works directly), **4–30 s long**. Lock a whole continuous take, not a 2-second piece.
- `image_references`: her 7 refs (3 front, 1 three-quarter, 3 profile) and his 3 slim + 2 real profiles (+ real 3/4 if needed). Up to 30 are allowed. Head and shoulders only, or the same outfit as the shot.
- Prompt template:
  > Replace the young woman in the [outfit] with the woman from the first N reference photos (front and side views of the same woman): her real face from every angle (round face, full cheeks, thick dark eyebrows, brown eyes, full lips, her real side profile), keeping her long, straight dark-brown hair worn down. Replace the young man in the [outfit] with the man from the last M reference photos: his real slim face with a defined jawline, short dark hair with his real hairline. Both keep exactly the clothes they wear in the source video: she keeps the [outfit], he keeps the [outfit]. Keep their movements and expressions, every shot and cut, the camera, the backgrounds and all other people exactly as in the source video.
- Resolution: 1080p for close-ups and key shots. 720p plus a Topaz upscale is the cheaper option for wides.
- Output length differs slightly from the source. Retime it in the edit.
- If one person is not replaced in a run (it happened once), re-run with that person's references listed first and their outfit named exactly.

### 7.6 QA gate before showing the user
For each shot, make a sheet with the reference photo next to start, middle and end frame crops of each face, plus a full-frame strip (the `review.py` and `sheets.sh` idea). Look at it yourself, fix failures, then show the user the clip and one sheet per scene.

### 7.7 Assembly
- Put the shots on the **2-second grid** from the user's answers. Continuous takes can span several segments.
- Split screens: two 958 px wide crops side by side with a thin white divider (crop offsets chosen so the faces sit centred and look toward the divider).
- Chapter changes: about 0.6 s soft dissolve. Inside a scene: straight cuts, or 0.3 s dissolves if the user wants softer.
- Fade in from black at the start; fade to white at the end (6.07).
- Add sound as chosen in Round 0. Export 1920×1080, 24 fps, H.264 CRF 17, AAC 192k, `+faststart`.

### 7.8 Example prompts (copy the pattern)

**A2 motion prompt for 1.01–1.03 (one continuous 10 s take, then cut points in the edit):**
> A bright modern university lecture hall with curved light-wood desks and grey mesh chairs, soft daylight; class has just ended and students around her stand up, chat and pack their bags. 0–2 s: the young woman in a pink crew-neck sweater and blue jeans, long straight dark-brown hair worn down, closes her notebook and slides it into her cream canvas backpack. 2–4 s: she stands up, swings the backpack onto her right shoulder and tucks her hair behind her ear. 4–6 s: she turns and walks toward the door; the camera tracks beside her at shoulder height. 6–8 s: she steps out into the bright corridor; across the corridor a tall young man in a navy crew-neck sweater stops and looks at her. 8–10 s: she notices him, a small shy smile, she lowers her eyes. Her face, features and hair stay exactly as in the first frame. Real-time natural movement, handheld cinematic camera, no zoom-in on faces, no text. Photorealistic, shot on 35mm film, natural skin texture, soft warm light, shallow depth of field, subtle film grain.

**B2 motion prompt for 1.11 (graduation, the two of us):**
> Start exactly from this photo: the young woman in a white dress and the young man in a white shirt stand together under a wooden canopy, sunlight flickering through the slats. 0–2 s: they turn to each other and laugh. 2–4 s: they walk forward out from under the canopy toward the camera, side by side, not touching. 4–6 s: he says something and she laughs, looking at him; the camera dollies backward in front of them. 6–8 s: they stop in the sunlight and look around the courtyard, smiling. Both faces stay exactly as in the first frame. Real-time natural movement, cinematic camera, no text, no numbers.

**Lock prompt (Genjutsu) for the same take:** use the template in 7.5 with outfits "white dress" / "white shirt".

---

## 8. What failed (do not repeat)

| # | What was tried | What happened | Do instead |
|---|---|---|---|
| 1 | Animate real photos with start = end frame, "very subtle motion", slow push-in | Looked like animated photos; user rejected the whole 2-min film | Real action, 8–10 s, no end frame; lock faces afterwards |
| 2 | 55 two-second clips joined with dissolves | Slideshow | Continuous takes, film editing |
| 3 | Kling "slow push-in" | Strong zoom; after 2–3 s it invented close-up faces | Name the exact camera move; keep subject distance; lock faces |
| 4 | Larger motion with no lock pass | Faces drifted away from the real people | Always run the Genjutsu lock |
| 5 | Nano Banana 2.1 stills from face references | Generic, beautified face; user: "Face … should be more similar to images" | FLUX 3 edit of a real selfie; then lock |
| 6 | Garden portrait as a main reference | Pulled her face toward a retouched, generic look | Car selfies and side views only |
| 7 | Face photos as `image_references` in Kling **image-to-video** | Video cut away to the reference photos mid-clip | Face refs only in the lock pass (or test reference-to-video mode) |
| 8 | `outpaint_image` to widen photos | Repainted the whole image; faces and sizes changed | Masked inpaint of the sides only plus paste the real photo back, tone-match seams |
| 9 | Kling 4.0 **video-edit** to replace faces | Changed hair and outfits but kept the original actors' faces | Use it only for hair and outfit; faces via Genjutsu |
| 10 | Kling video-edit on a whole 25 s clip | Job failed (no reason) | Groups of ≤6–10 s |
| 11 | Genjutsu with a reference of him in a **suit** | His sweater became the suit, and her face was not changed in that run | Head-only or same-outfit refs; "keep exactly the clothes" |
| 12 | AI "slim" edit of his **profile** | Skin tone changed | Real profiles; slim edits only for front and 3/4 |
| 13 | Small crops of him from group photos | Soft, approximate face | The 7 clear photos (`IMG_0210`–`IMG_0216`) |
| 14 | Generated outfits for her | Low necklines appeared | Name a high, closed neckline in every prompt |
| 15 | Generated 3.06 | Added her head on his shoulder (not in the real photo) | Prompt "they do not touch" or "touch only as in the photo"; cut if added |
| 16 | Generated families in big motion | Family faces changed (no refs) | Keep families at distance or ask for their photos |
| 17 | Assuming the user means "animate my photos" | Wrong deliverable | When the user says "video", they mean filmed-looking full motion |

---

## 9. Question protocol (ask with options for every 2 seconds)

Use the **AskUserQuestion** tool: 1–4 questions per call, 2–4 options each (the tool adds "Other" automatically). Put the **PDF version first, marked "(Recommended)"**. Keep the wording short and simple; the user reads on a phone.

### Round 0: global settings (one call, before the segments)
1. **Sound:** user's music track / no sound / AI-generated soft music / keep as decided later.
2. **Editing feel:** straight cuts inside scenes and dissolves between chapters (recommended) / soft dissolves everywhere (as the PDF says) / mostly continuous long takes.
3. **Families in group shots:** keep at medium/wide distance with gentle action (recommended) / user sends family face photos / remove families from moving shots.
4. **Her hair in special scenes:** always long and down / follow each real photo (graduation cap, bun in 6.05) / ask per scene.
(A second call can confirm: his stubble vs clean-shaven; on-screen text lines; slow-motion amount.)

### Rounds 1–60: one call per 2-second segment (Appendix A has the defaults)
Header every call with the segment number and time, e.g. "Seg 07 · 0:12–0:14 · 1.05 The café".
- **Q1 What happens** (action in these 2 s): options = PDF action (Recommended) / 2–3 concrete alternatives (different gesture, more movement, a reaction) / "continue the previous action".
- **Q2 Camera:** shot size + move, e.g. "Medium, slow dolly in (Recommended)" / "Wide, tracking beside them" / "Close-up, handheld" / "Over the shoulder".
- **Q3 Faces and emotion:** who is visible and where they look, e.g. "She laughs and looks at him (Recommended)" / "Both look at each other, shy smiles" / "Only her face clear, him from behind".
- **Q4 Look and details** (ask only when something can change, otherwise "same as previous segment"): outfit, hair, props, light, time of day, weather.

Practical rules:
- Show a one-line summary of the last 2–3 decisions every 5 segments, and a small table per chapter at the chapter end. Ask "OK?" before moving on.
- If the user answers "Other" with free text, follow it exactly and repeat it back in one line.
- Never generate before the user approves the chapter's segment plan **and** the cost.
- After all 60 segments, write the **shot plan** (takes, beats per 2 s, references per take, route, cost) and get one final OK.

### 9.1 Example question call for one segment (AskUserQuestion)
```json
{"questions": [
 {"header": "Seg 07 action", "multiSelect": false,
  "question": "Seg 07 (0:12–0:14), 1.05 The café: what happens in these 2 seconds?",
  "options": [
   {"label": "He jokes, she laughs (Recommended)", "description": "PDF: at the window table with coffee, he says something funny and she laughs."},
   {"label": "She tells a story", "description": "She talks with her hands, he listens and smiles."},
   {"label": "They clink cups", "description": "They lift their coffee cups and smile at each other."},
   {"label": "Continue previous", "description": "Keep the action from segment 06 going."}]},
 {"header": "Camera", "multiSelect": false,
  "question": "Seg 07: how is it filmed?",
  "options": [
   {"label": "Medium, slow arc (Recommended)", "description": "PDF: the camera slowly arcs around the table."},
   {"label": "Close on her laugh", "description": "Close-up of her face, him blurred in the foreground."},
   {"label": "Wide through window", "description": "From outside the glass, the café and lawn around them."}]},
 {"header": "Faces", "multiSelect": false,
  "question": "Seg 07: who is clear on screen and where do they look?",
  "options": [
   {"label": "Both, at each other (Recommended)", "description": "Both faces clear, looking at each other."},
   {"label": "Mainly her", "description": "Her face clear, him in profile."},
   {"label": "Mainly him", "description": "His face clear, her from the side."}]},
 {"header": "Details", "multiSelect": false,
  "question": "Seg 07: outfits and light?",
  "options": [
   {"label": "PDF outfits, daylight (Recommended)", "description": "Her cream knit sweater (high neck), him dark jacket; bright daylight."},
   {"label": "Same as segment 06", "description": "Keep everything from the previous segment."},
   {"label": "Autumn look", "description": "Warmer clothes and golden autumn light (time passing)."}]}
]}
```

---

## 10. Tools, costs and environment facts (verified Nov 2026)

**Higgsfield MCP connector ("video" tools):**
| Model / tool | Use | Cost (credits) | Notes |
|---|---|---|---|
| `kling4_0` image-to-video | real motion from a start frame | 3.25/s at 1080p (16.25 per 5 s), 2.25/s at 720p | 3–30 s; roles `start_image`, `end_image`, `image_references`, `video_references`; modes `text-to-video`, `image-to-video`, `reference-to-video`, `video-edit`; param `kling_element_ids` (≤7) |
| `kling4_0` video-edit | change hair or outfits in an existing video | 4/s at 1080p | does not change faces |
| `hf_mult_replace_object` (Genjutsu) | **identity lock / face replace** in a video | ~20/s at 1080p, ~7/s at 720p | source 4–30 s, 1–30 image refs; 15–35 min |
| `hf_mult_motion_control` / `motion_control` (Kling 3.0) | transfer motion from a driving video onto a person image | — | option if a clip needs a very specific action |
| `flux_3_image` | edit a real photo into a scene, keeps the face | 3 per 2k image | best for start frames |
| `nano_banana_2_1` | masked inpaint (widening the sides) | 2 | never for faces |
| `upscale_video` (topaz) | upscale to 1080p | small | used for the 640×360 opening |
| `outpaint_image` | — | 2 | do not use on people |
| Seedance 2.5 | — | — | blocks uploads of real faces |
- **Upload flow:** `media_upload` → curl PUT to the returned `upload_url` → `media_confirm`. The network must allow `upload.higgsfield.ai` (uploads) and `d8j0ntlcm91z4.cloudfront.net` (result downloads). In the previous cloud session this needed a custom environment (named "video") with those hosts.
- **Waiting:** `jobs_wait` waits at most 15 s per call. Kling takes 5–10 min; Genjutsu 15–35 min. Schedule a check rather than polling.
- **Free or "unlimited" generations** are not available from Claude Code (only in the Claude chat, Cowork and ChatGPT connectors).
- **Balance:** 570 credits on 14 Nov 2026 (Ultra plan, 3,000 credits per month). Check with `balance` first.
- **Estimate for the full 2:00:** Route A ≈52 s and Route B ≈46 s of screen time, generated about 2× for choice, plus locking about 1.5× → **≈2,500 credits** (720p lock + upscale) to **≈5,000 credits** (1080p lock everywhere), including about 30% retries. Tell the user before starting; they will probably need more credits.

---

## 11. Session hygiene
- Keep `manifest.txt` with every media ID, job ID, file name and decision. Write to it after every submit and download.
- Jobs keep running if the session restarts. Recover them by job ID with `jobs_wait`.
- Download every result right away (`curl` the `result_url`) and keep the originals.
- Before every paid batch, send a short message with what will be made, the cost, and the current balance.

## 12. How to talk to this user
- Short answers in key points, under about 1,000 characters, no links.
- Ask questions with options before starting anything new or paid.
- Send finished files with SendUserFile (video renders inline).
- Do not over-promise. If a face is close but not exact, say so and offer a fix.

---

## Appendix A — Draft 60-segment timeline (from the PDF; the user's answers override it)

How it was made: every PDF moment gets one 2-second segment; the 8 key or emotional moments get two (1.02, 1.03, 2.02, 2.14, 3.06, 4.06, 5.02, 6.05); split-screen pairs (a/b) share their segments; 6.07 (fade to white) sits in the last second of 6.06. Chapter lengths: Ch1 30 s · Ch2 32 s · Ch3 20 s · Ch4 14 s · Ch5 10 s · Ch6 14 s = 2:00.
Routes: **A** acted, made from the face photos (≈52 s) · **B** real photo turned into real video (≈46 s) · **N** no identity needed (≈18 s) · **E** made in the edit (≈4 s). One continuous take may cover several segments.

| Seg | Time | Ch | PDF shot | What happens (PDF default) | On screen | Route |
|---|---|---|---|---|---|---|
| 01 | 0:00–0:02 | 1 | 1.01 Class ends | Class has just ended. Students stand and pack up. She closes her notebook, puts her bag on her shoulder and heads for the door. | her | A (acted, from face photos) |
| 02 | 0:02–0:04 | 1 | 1.02 (part 1/2) The look | She steps into the corridor. Across from her, he comes out of another classroom and sees her. He looks at her, and she notices. | both | A (acted, from face photos) |
| 03 | 0:04–0:06 | 1 | 1.02 (part 2/2) The look | She steps into the corridor. Across from her, he comes out of another classroom and sees her. He looks at her, and she notices. | both | A (acted, from face photos) |
| 04 | 0:06–0:08 | 1 | 1.03 (part 1/2) Her shy smile | Close-up. She smiles shyly, tucks her hair behind her ear and lowers her eyes. | her (close-up) | A (acted, from face photos) |
| 05 | 0:08–0:10 | 1 | 1.03 (part 2/2) Her shy smile | Close-up. She smiles shyly, tucks her hair behind her ear and lowers her eyes. | her (close-up) | A (acted, from face photos) |
| 06 | 0:10–0:12 | 1 | 1.04 His smile | Close-up. He smiles back, a little embarrassed, glances away and back again. | him (close-up) | A (acted, from face photos) |
| 07 | 0:12–0:14 | 1 | 1.05 The café | They sit at a table by the window with coffee and something to eat. He says something funny and she laughs. | both | A (acted, from face photos) |
| 08 | 0:14–0:16 | 1 | 1.06 The library | They study side by side on their laptops at the front table. He points at something on her screen, she looks up at him and they share a quiet smile. | both | A (acted, from face photos) |
| 09 | 0:16–0:18 | 1 | 1.07 The park | They walk side by side across the red bridge at golden hour, talking. She laughs and looks at him. | both (from behind) | A (acted, from face photos) |
| 10 | 0:18–0:20 | 1 | 1.08 Time passes | The campus at dusk. Windows light up, leaves fall, clouds drift. This shows time passing without any dates. | none | N (no identity needed) |
| 11 | 0:20–0:22 | 1 | 1.09 Graduation day | The outdoor ceremony: the choir sings on stage while graduates in caps and gowns look on. | crowd only | N (no identity needed) |
| 12 | 0:22–0:24 | 1 | 1.10 With our families | Graduation evening at ADA. The two of them in their gowns with their diplomas, family around them. She holds red roses. | both + family | B (real photo -> real video) |
| 13 | 0:24–0:26 | 1 | 1.11 The two of us | Graduation day, just the two of them. They turn to each other and smile. | both | B (real photo -> real video) |
| 14 | 0:26–0:28 | 1 | 1.12 The prom, Zağulba Palace | The red carpet at the graduation prom. Camera flashes, she smiles and leans toward him. | both | B (real photo -> real video) |
| 15 | 0:28–0:30 | 1 | 1.13 The dance | She dances and laughs, he turns toward her, warm lights behind. The chapter ends on a soft glow. | both + guests | B (real photo -> real video) |
| 16 | 0:30–0:32 | 2 | 2.01 Leaving together | At the airport in Baku. They walk side by side through the terminal, each pulling a suitcase. | both | A (acted, from face photos) |
| 17 | 0:32–0:34 | 2 | 2.02 (part 1/2) Two directions | The terminal’s twin escalators. She rides up the left one, he rides up the right one. Halfway up, both turn and look back at each other across the tree. | both (small, wide) | A (acted, from face photos) |
| 18 | 0:34–0:36 | 2 | 2.02 (part 2/2) Two directions | The terminal’s twin escalators. She rides up the left one, he rides up the right one. Halfway up, both turn and look back at each other across the tree. | both (small, wide) | A (acted, from face photos) |
| 19 | 0:36–0:38 | 2 | 2.03 Her window + His window | No photo of this moment. Use the face references on page 3. On her plane. She sits by the window and looks out at the clouds, missing him. ‖ On his plane. He sits by the window, looking out and thinking of her. No photo of this moment. Use the face references. | her | him (split) | A (acted, from face photos) |
| 20 | 0:38–0:40 | 2 | 2.04 Two skies | No photo needed. There are no people in this shot. High above the clouds, two planes that were flying together turn away from each other. Their trails split apart. | none | N (no identity needed) |
| 21 | 0:40–0:42 | 2 | 2.05 Arriving: Edinburgh + Arriving: Michigan State | She arrives at the University of Edinburgh’s Old College. The wind catches her hair; she looks around the courtyard and smiles. ‖ He arrives at Michigan State and stands by the Spartan statue. He looks around the campus and smiles. | her | him (split) | B (real photo -> real video) |
| 22 | 0:42–0:44 | 2 | 2.06 A photo for him | Exploring Edinburgh. By the fountain below the castle, she takes a photo of the view to send him. | her | B (real photo -> real video) |
| 23 | 0:44–0:46 | 2 | 2.07 Photos back and forth | Their chat on a phone screen. The photos they send each other pop up in message bubbles. | none (graphics) | E (edit graphics) |
| 24 | 0:46–0:48 | 2 | 2.08 His reply | On campus in Michigan he gets her photo, smiles, and photographs his campus to send back. | him | A (acted, from face photos) |
| 25 | 0:48–0:50 | 2 | 2.09 Michigan life | A street fair in Lansing. He poses with the Spartan mascot, who flexes; he laughs and flexes back. | him + mascot | B (real photo -> real video) |
| 26 | 0:50–0:52 | 2 | 2.10 Chicago | A trip to Chicago. At night on the river he poses for a photo, then takes one of the lit-up skyline to send her. | him | B (real photo -> real video) |
| 27 | 0:52–0:54 | 2 | 2.11 “Wow” | In a sunny Edinburgh park she opens his photo and lights up. | her | A (acted, from face photos) |
| 28 | 0:54–0:56 | 2 | 2.12 Studying: Edinburgh + Studying: Michigan State | The term begins. She studies inside an old stone university building, autumn trees outside. ‖ He studies at Michigan State, by the tall windows of the International Center. | her | him (split) | A (acted, from face photos) |
| 29 | 0:56–0:58 | 2 | 2.13 Winter: Edinburgh + Winter: Michigan | Winter arrives. Under grey skies she walks to university in a warm coat and scarf, the castle above her. ‖ Deep snow in Michigan. The same building from the summer shot, now buried in snow; he walks past in a thick jacket. | her | him (split) | A (acted, from face photos) |
| 30 | 0:58–1:00 | 2 | 2.14 (part 1/2) The call: her + The call: him | No photo of this moment. Use the face references on page 3. An evening video call. In her room in Edinburgh she talks to him on her laptop, smiling and encouraging him. ‖ In his room in Michigan, snow outside. He turns his laptop to the window to show her the snow, and they both laugh. No photo of this moment. Use the face references on page 3. | her | him (split) | A (acted, from face photos) |
| 31 | 1:00–1:02 | 2 | 2.14 (part 2/2) The call: her + The call: him | No photo of this moment. Use the face references on page 3. An evening video call. In her room in Edinburgh she talks to him on her laptop, smiling and encouraging him. ‖ In his room in Michigan, snow outside. He turns his laptop to the window to show her the snow, and they both laugh. No photo of this moment. Use the face references on page 3. | her | him (split) | A (acted, from face photos) |
| 32 | 1:02–1:04 | 3 | 3.01 Together again | Edinburgh Castle on a bright winter day. Both families stand together on the esplanade: his mother and brother, her mother, and the two of them. | both + family | B (real photo -> real video) |
| 33 | 1:04–1:06 | 3 | 3.02 London lights | London at Christmas: golden lights strung across the street, black cabs and red buses passing. | none (street) | N (no identity needed) |
| 34 | 1:06–1:08 | 3 | 3.03 Under the Christmas arch | Both families together under a big Christmas arch of greenery and red bows. | both + family | B (real photo -> real video) |
| 35 | 1:08–1:10 | 3 | 3.04 The winter fair | Night at the Christmas fair. The two of them and his brother laugh and make peace signs among the bright stalls. | both + his brother | B (real photo -> real video) |
| 36 | 1:10–1:12 | 3 | 3.05 Tower Bridge | Both families by the river at night, Tower Bridge glowing behind them in the fog. | both + family | B (real photo -> real video) |
| 37 | 1:12–1:14 | 3 | 3.06 (part 1/2) By the tree | Just the two of them, by a big Christmas tree, city lights in the window behind. | both | B (real photo -> real video) |
| 38 | 1:14–1:16 | 3 | 3.06 (part 2/2) By the tree | Just the two of them, by a big Christmas tree, city lights in the window behind. | both | B (real photo -> real video) |
| 39 | 1:16–1:18 | 3 | 3.07 New Year’s Eve | New Year’s Eve. Everyone dressed up at the top of the hotel staircase before dinner. | both + family | B (real photo -> real video) |
| 40 | 1:18–1:20 | 3 | 3.08 The dinner | At the New Year’s Eve dinner, the two of them at their table under the hanging greenery. | both | B (real photo -> real video) |
| 41 | 1:20–1:22 | 3 | 3.09 Midnight | Midnight. Fireworks burst over the Thames and the city lights. | none | N (no identity needed) |
| 42 | 1:22–1:24 | 4 | 4.01 Her graduation + His graduation | In front of McEwan Hall in her gown, she lifts her cap and smiles over her shoulder. ‖ At Michigan State, in cap and gown with his diploma, his sister beside him. | her | him + his sister (split) | B (real photo -> real video) |
| 43 | 1:24–1:26 | 4 | 4.02 McEwan Hall | Inside the hall: the painted, gilded dome above the families in the galleries. | none (hall, crowd) | N (no identity needed) |
| 44 | 1:26–1:28 | 4 | 4.03 The pipers | Outside, a piper and a drummer play as the graduates come out. | piper, drummer, strangers | N (no identity needed) |
| 45 | 1:28–1:30 | 4 | 4.04 Flowers | She holds a big bouquet with her family around her, low sun on the old buildings. | her + family | B (real photo -> real video) |
| 46 | 1:30–1:32 | 4 | 4.05 Flying home | A globe at night. Two glowing flight paths, one from Michigan and one from Edinburgh, arc across the world and meet in Baku. No photo needed. | none (graphics) | E (edit graphics) |
| 47 | 1:32–1:34 | 4 | 4.06 (part 1/2) Home | Back at the airport in Baku, at the same twin escalators from shot 2.02. Now they ride down from either side and meet in the middle by the tree. | both (wide) | A (acted, from face photos) |
| 48 | 1:34–1:36 | 4 | 4.06 (part 2/2) Home | Back at the airport in Baku, at the same twin escalators from shot 2.02. Now they ride down from either side and meet in the middle by the tree. | both (wide) | A (acted, from face photos) |
| 49 | 1:36–1:38 | 5 | 5.01 In uniform | He stands at the base in his uniform, ready for his service. | him | B (real photo -> real video) |
| 50 | 1:38–1:40 | 5 | 5.02 (part 1/2) Watching him go | Close on her face as she watches him walk away toward the base gate. She tries to smile, but her eyes are sad. | her (close) + him from behind | A (acted, from face photos) |
| 51 | 1:40–1:42 | 5 | 5.02 (part 2/2) Watching him go | Close on her face as she watches him walk away toward the base gate. She tries to smile, but her eyes are sad. | her (close) + him from behind | A (acted, from face photos) |
| 52 | 1:42–1:44 | 5 | 5.03 Waiting | No photo of this moment. Use the face references on page 3. She waits. By her window in Baku she looks at his photo on her phone while the seasons change outside. | her | A (acted, from face photos) |
| 53 | 1:44–1:46 | 5 | 5.04 Visiting day | Visiting day at the base. She and the families stand with him in front of the gate. | both + families | B (real photo -> real video) |
| 54 | 1:46–1:48 | 6 | 6.01 Hə Almağa Gəlmişik | The sign among white and blue flowers and crystal favours: “Hə Almağa Gəlmişik”. Guests know straight away what day this is. | none (sign) | N (no identity needed) |
| 55 | 1:48–1:50 | 6 | 6.02 The table is set | The long table laid in white and gold, candles lit, waiting for the guests. | none (table) | N (no identity needed) |
| 56 | 1:50–1:52 | 6 | 6.03 Waiting to come in | In the next room she waits in white, a calla lily in her hand, and smiles to herself. | her | B (real photo -> real video) |
| 57 | 1:52–1:54 | 6 | 6.04 The tea | She holds the tray of tea in armudu glasses, ready to take it in. | her | B (real photo -> real video) |
| 58 | 1:54–1:56 | 6 | 6.05 (part 1/2) Serving the tea | At the table she leans in and sets a glass of tea down. Only she is seen clearly. The guests at the table stay out of focus, with no faces visible. | her (guests blurred, no faces) | A (acted, from face photos) |
| 59 | 1:56–1:58 | 6 | 6.05 (part 2/2) Serving the tea | At the table she leans in and sets a glass of tea down. Only she is seen clearly. The guests at the table stay out of focus, with no faces visible. | her (guests blurred, no faces) | A (acted, from face photos) |
| 60 | 1:58–2:00 | 6 | 6.06 “Hə” | She holds one glass of tea and smiles. The camera moves in slowly on the glass. Last ~1 s: fade to soft white (6.07), then the real proposal footage follows. | her | B (real photo -> real video) |

---

## Appendix B — Full PDF scenario, all 59 shots (Draft 9, kept complete)

**Chapter summaries from the PDF**
- **1 University:** The story begins at ADA University in Baku. One ordinary day a class ends, and in the corridor outside two students notice each other. He looks at her, she catches it, smiles and looks away, a little shy. Then small everyday moments: coffee and laughter in the university café, studying side by side in the library, walks across the red bridge in the university park. The seasons change. Then graduation day, with both families there, and the graduation prom at Zağulba Palace. *Feeling:* light and warm, shy at the start, growing into ease and joy. *Text:* optional "Where it all began" over 1.01.
- **2 Studying abroad:** After graduation their paths split for a while. He goes to Michigan State University (USA); she goes to the University of Edinburgh (Scotland). They set off from Heydar Aliyev International Airport in Baku. In the terminal they go two different ways, and on two different planes each looks out of the window, missing the other. They arrive, she at the University of Edinburgh's Old College, he at Michigan State beside the Spartan statue. The screen stays split. In quick loose cuts they explore and share: she photographs the castle and sends it; he answers with his campus and later the Chicago skyline, and she lights up at each one. Then the term gets serious: they study, winter arrives (grey and wet in Edinburgh, deep snow in Michigan), and in the evenings they video call. *Feeling:* bittersweet at the airport, then curious and warm. *Text:* "Edinburgh" and "Michigan" over the first split screen (2.03); optionally "Chicago" on 2.10, added in the edit.
- **3 New Year together:** Both families fly to the UK (his mother and brother, and her mother); he comes over from Michigan too. Together they see Edinburgh, then London for the holidays: streets strung with Christmas lights, the winter fair, Tower Bridge at night. On New Year's Eve everyone dresses up for dinner, and at midnight the sky over the Thames lights up. *Feeling:* warm and festive, the two families together for the first time. *Text:* none, optionally "London" over 3.02.
- **4 Graduations and home:** He graduates at Michigan State. She graduates at the University of Edinburgh in McEwan Hall, with a choir inside, pipers outside and family there. Then they both fly home: two flight paths, from America and Scotland, meet in Baku. At the same airport where they once went separate ways, they come back down the escalators and meet in the middle. *Feeling:* proud and joyful, then the relief of coming home. *Text:* optionally "Baku" on the globe (4.05).
- **5 Army:** Back in Baku, he leaves for his military service with the Naval Forces. She sees him off and watches him go, trying to smile. Then she waits while the seasons turn. On visiting days she and the families visit him at the base. *Feeling:* quiet and tender, sad to part, steady while waiting, proud of him.
- **6 Asking for her hand:** As tradition goes, his family comes to her family's home to take the "hə" (the family's yes). The table is set; the sign by the flowers says "Hə Almağa Gəlmişik". She waits in the next room in white, a calla lily in her hand, then carries in the tea in armudu glasses and serves it at the table. The AI film ends here; the real footage of his proposal follows. *Feeling:* warm, respectful and joyful, two families becoming one. Their names and 27.12.2026 can close the whole film **after** the proposal footage (in the edit only).

**PDF "How to use" notes (original approach, kept for reference):** each shot was generated at 5 s and trimmed to its "use" length; "Animate a real photo" = photo as start frame; "Create a start frame" = make a still from face refs plus location photo, then animate; split-screen a/b = her left, him right; "Made in the edit" = graphics, not AI. **This handoff replaces the "animate with small motion" part with the real-video method of Section 7 (see the "New approach" line under each shot). All story, place, outfit and rule details below still apply.**


### Chapter 1 University

#### 1.01 — Class ends
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C1_classroom.jpg`  
**What happens:** Class has just ended. Students stand and pack up. She closes her notebook, puts her bag on her shoulder and heads for the door.  
**PDF prompt:** A modern university lecture hall with curved light-wood desks, grey mesh chairs and warm beige walls, soft daylight. The class has just ended and students stand up and pack their bags. In the foreground the young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), wearing a pink sweater and blue jeans, closes her notebook, slips it into her bag, puts the bag on her shoulder and walks toward the door. The camera slowly pushes in from the back rows.  
**Notes:** Her outfit: pink sweater, blue jeans, hair down. Keep this outfit for shots 1.02 and 1.03.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.02 — The look
*Create a start frame · use ~4 s*  
Photos in the PDF pack: `C1_corridor.jpg`, `C1_corridoratrium.jpg`  
**What happens:** She steps into the corridor. Across from her, he comes out of another classroom and sees her. He looks at her, and she notices.  
**PDF prompt:** A bright university corridor with warm beige wall panels, glass classroom walls on one side, a pale stone floor, long linear ceiling lights and a low green bench, students passing by. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a pink sweater and blue jeans, steps out of a classroom. Across the corridor the young man (tall, short dark hair, fair skin, clean-shaven), in a navy sweater and dark jeans, steps out of another classroom and stops when he sees her. He keeps looking at her and she notices. Over-the-shoulder shot from behind her, focused on him, passing students softly blurred.  
**Notes:** Corridor: use C1_corridor.jpg as the setting; the atrium photo shows the wider building. His outfit: navy sweater and dark jeans.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.03 — Her shy smile
*Create a start frame · KEY SHOT · use ~3 s*  
Photos in the PDF pack: `C1_corridor.jpg`  
**What happens:** Close-up. She smiles shyly, tucks her hair behind her ear and lowers her eyes.  
**PDF prompt:** Close-up of the young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup) in a pink sweater in a bright university corridor. She catches someone’s gaze, smiles shyly, tucks a strand of hair behind her ear and lowers her eyes, cheeks slightly flushed. Soft window light on her face, background softly blurred, slow motion.  
**Notes:** The key moment of the chapter. Use her face references (page 3); the corridor is only the soft background. Worth generating several versions and choosing the best.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.04 — His smile
*Create a start frame · use ~2 s*  
Photos in the PDF pack: `C1_corridor.jpg`  
**What happens:** Close-up. He smiles back, a little embarrassed, glances away and back again.  
**PDF prompt:** Close-up of the young man (tall, short dark hair, fair skin, clean-shaven) in a navy sweater in a bright university corridor. He smiles back, a little embarrassed, glances away and then looks back at her. Soft window light, background softly blurred, slow motion.  
**Notes:** Use his face references (page 3); the corridor is only the soft background. First shot to cut if the chapter runs long.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.05 — The café
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C1_cafe-atrium.jpg`  
**What happens:** They sit at a table by the window with coffee and something to eat. He says something funny and she laughs.  
**PDF prompt:** A bright university atrium café with round white tables, red chairs and floor-to-ceiling windows overlooking a green lawn. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup) in a cream knit sweater and the young man (tall, short dark hair, fair skin, clean-shaven) in a dark jacket sit across from each other at a table by the window, with coffee cups and a small snack. He says something funny and she laughs; they talk easily. The camera slowly arcs around the table. Natural daylight.  
**Notes:** New outfits from here on show that time is passing.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.06 — The library
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C1_library.jpg`  
**What happens:** They study side by side on their laptops at the front table. He points at something on her screen, she looks up at him and they share a quiet smile.  
**PDF prompt:** A modern university library with light-wood study tables and chairs, tall light-wood bookshelves, square ceiling lights and tall windows with white blinds, soft warm light. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup) and the young man (tall, short dark hair, fair skin, clean-shaven) sit side by side at the front table, each with an open laptop and a notebook, studying. He points at something on her laptop screen; she nods, looks up at him and they share a quiet smile. The camera slowly pushes in.  
**Notes:** Use this exact library: place the two of them at the front table in C1_library.jpg, keep the room as it is. Make the still first, check faces, then animate.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.07 — The park
*Create a start frame · use ~4 s*  
Photos in the PDF pack: `C1_park-red-bridge.jpg`, `C1_park-lake.jpg`  
**What happens:** They walk side by side across the red bridge at golden hour, talking. She laughs and looks at him.  
**PDF prompt:** A university park with tall pine trees and a calm green pond crossed by a red footbridge, golden-hour sunlight. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup) in a light coat and the young man (tall, short dark hair, fair skin, clean-shaven) in a casual jacket walk side by side across the red bridge, talking; she laughs and looks at him. The camera follows slowly from behind, then rises gently. Warm sunlight through the pine trees.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 1.08 — Time passes
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C1_campus-dusk.jpg`  
**What happens:** The campus at dusk. Windows light up, leaves fall, clouds drift. This shows time passing without any dates.  
**PDF prompt:** Animate this photo: a university campus at dusk. The library windows glow warm yellow, a few students walk up the steps, leaves drift down from the tree and clouds move across the lavender sky in a gentle time-lapse. Very slow push-in.  
**Notes:** No people close to the camera, so this one is easy to generate.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 1.09 — Graduation day
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C1_graduation-ceremony.jpg`  
**What happens:** The outdoor ceremony: the choir sings on stage while graduates in caps and gowns look on.  
**PDF prompt:** Animate this photo: an outdoor university graduation ceremony at dusk. A student choir sings on stage while graduates in caps and gowns watch; a woman in the front raises her phone to film. Gentle movement in the crowd, slow push-in toward the stage.  
**Notes:** Make sure no year is visible on the stage banner.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 1.10 — With our families
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C1_graduation-families.jpg`  
**What happens:** Graduation evening at ADA. The two of them in their gowns with their diplomas, family around them. She holds red roses. Fix the photo first: This file is small (572 × 763). Upscale it with an AI upscaler before animating.  
**PDF prompt:** Animate this photo: five people stand together on a cobbled courtyard outside a modern university building on a summer evening. A young woman in a black graduation gown over a white dress holds red roses and her diploma, a young man in a graduation gown holds his diploma folder, and between them stand two women and a young woman in white. Everyone smiles; a light breeze moves hair and fabric. Very subtle motion, slow push-in.  
**Notes:** Keep motion very small so every face stays true.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 1.11 — The two of us
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C1_graduation-couple.jpg`  
**What happens:** Graduation day, just the two of them. They turn to each other and smile. Fix the photo first: Remove the “Commencement 2024” banner reflected in the glass behind them.  
**PDF prompt:** Animate this photo: the young woman in a white dress and the young man in a white shirt stand together under a wooden canopy, sunlight flickering through the slats. They turn toward each other and smile. Slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 1.12 — The prom, Zağulba Palace
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C1_prom-portrait.jpg`, `C1_prom-redcarpet.jpg`  
**What happens:** The red carpet at the graduation prom. Camera flashes, she smiles and leans toward him. Fix the photo first: Remove “PROM 2024” and the photographer’s watermark (bottom left). If using the red-carpet photo instead, remove the large “2024”.  
**PDF prompt:** Animate this photo: a couple at an elegant evening party, standing on a red carpet in front of a glowing white neon sign. Camera flashes go off; she smiles and leans slightly toward him, and he relaxes into a smile. Subtle motion, slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 1.13 — The dance
*Animate a real photo · use ~4 s*  
Photos in the PDF pack: `C1_prom-dance.jpg`  
**What happens:** She dances and laughs, he turns toward her, warm lights behind. The chapter ends on a soft glow. Fix the photo first: Remove the photographer’s watermark (bottom left).  
**PDF prompt:** Animate this photo: an evening party in a palace ballroom, warm golden string lights in the background. The young woman in a champagne off-shoulder gown dances and laughs; the young man in a dark suit turns toward her. Other guests dance around them, softly blurred. Slow motion, gentle camera drift, ending on warm glowing light.  
**Notes:** Ends the chapter. Fade through the warm light into chapter 2.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  


### Chapter 2 Studying abroad

#### 2.01 — Leaving together
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C2_airport-terminal.jpg`  
**What happens:** At the airport in Baku. They walk side by side through the terminal, each pulling a suitcase.  
**PDF prompt:** A bright modern airport terminal with a white lattice ceiling, glass balconies and a polished pale floor. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a beige trench coat over a light knit, and the young man (tall, short dark hair, fair skin, clean-shaven), in a dark jacket and jeans, walk side by side toward the camera, each pulling a suitcase, talking quietly. The camera moves slowly backward in front of them.  
**Notes:** Travel outfits are a suggestion. Change them if you have a photo from that day. Keep the same outfits through 2.03.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.02 — Two directions
*Create a start frame · KEY SHOT · use ~4 s*  
Photos in the PDF pack: `C2_airport-terminal.jpg`  
**What happens:** The terminal’s twin escalators. She rides up the left one, he rides up the right one. Halfway up, both turn and look back at each other across the tree.  
**PDF prompt:** Symmetrical wide shot of an airport terminal hall with two escalators rising on either side of a tall green tree in the centre. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a beige trench coat, stands on the left escalator with her suitcase, and the young man (tall, short dark hair, fair skin, clean-shaven), in a dark jacket, stands on the right escalator with his, both rising slowly. Halfway up they turn and look back at each other across the tree, a little sad. The camera holds centred and pushes in very slowly.  
**Notes:** Use this exact view of the terminal (Heydar Aliyev International Airport). Its symmetry shows them going two different ways. If the signs warp, soften them.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.03a — Her window
*Create a start frame · use ~4 s*  
**What happens:** No photo of this moment. Use the face references on page 3. On her plane. She sits by the window and looks out at the clouds, missing him.  
**PDF prompt:** Inside a passenger plane, daytime. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a light knit, sits in a window seat on the right side of the frame, her face turned toward the oval window. She looks out at the clouds below, thoughtful and a little sad, then lowers her eyes. Soft daylight from the window on her face, slow push-in.  
**Notes:** Split screen with 2.03b: her on the left half of the screen, facing right, toward him.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.03b — His window
*Create a start frame · use ~4 s · side by side with 2.03a (her left, him right)*  
**What happens:** On his plane. He sits by the window, looking out and thinking of her. No photo of this moment. Use the face references.  
**PDF prompt:** Inside a passenger plane, daytime. The young man (tall, short dark hair, fair skin, clean-shaven), in a dark jacket, sits in a window seat on the left side of the frame, his face turned toward the oval window. He looks out at the clouds below, thoughtful and a little sad, then rests his head back against the seat. Soft daylight from the window on his face, slow push-in.  
**Notes:** Split screen with 2.03a: him on the right half, facing left, so they seem to look toward each other across the line. Match the light in both clips.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.04 — Two skies
*Create a start frame · use ~3 s*  
**What happens:** No photo needed. There are no people in this shot. High above the clouds, two planes that were flying together turn away from each other. Their trails split apart.  
**PDF prompt:** Wide aerial view high above the clouds at golden hour. Two passenger jets flying side by side slowly turn away from each other, their white contrails splitting into a wide V across the sky. Calm and cinematic, slow camera drift.  
**Notes:** No people, so this one is quick to generate. It closes the departure.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 2.05a — Arriving: Edinburgh
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C2_edinburgh-old-college-her.jpg`  
**What happens:** She arrives at the University of Edinburgh’s Old College. The wind catches her hair; she looks around the courtyard and smiles.  
**PDF prompt:** Animate this photo: a young woman in a green hoodie and jeans stands on the lawn of a grand old stone university courtyard under a bright sky. A breeze lifts her long hair; she looks up at the buildings around her, then back toward the camera with a happy smile. Clouds drift. Slow push-in.  
**Notes:** Split screen with 2.05b: her on the left, him on the right, as in 2.03.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 2.05b — Arriving: Michigan State
*Animate a real photo · use ~3 s · side by side with 2.05a (her left, him right)*  
Photos in the PDF pack: `C2_msu-sparty-him.jpg`  
**What happens:** He arrives at Michigan State and stands by the Spartan statue. He looks around the campus and smiles.  
**PDF prompt:** Animate this photo: a young man in a green T-shirt and jeans stands in front of a large bronze statue on a redbrick plinth, campus lawn and trees behind. He takes his hands out of his pockets, looks around the campus and smiles. Clouds drift and the trees move in the breeze. Slow push-in.  
**Notes:** The statue must stay completely still; only he, the trees and the sky move.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 2.06 — A photo for him
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C2_edinburgh-fountain-her.jpg`  
**What happens:** Exploring Edinburgh. By the fountain below the castle, she takes a photo of the view to send him.  
**PDF prompt:** Animate this photo: a young woman with long dark hair in a beige knit top and a plaid skirt stands in a garden in front of an ornate blue-and-gold fountain, a castle on the rock behind her. She smiles, lifts her phone and takes a photo of the castle. Water flows from the fountain and clouds drift. Slow push-in.  
**Notes:** The montage starts here: loose, quick cuts of about 2 seconds each, through 2.11.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 2.07 — Photos back and forth
*Made in the edit · use ~2 s*  
Photos in the PDF pack: `C2_edinburgh-castle.jpg`, `C2_msu-building.jpg`, `C2_chicago-him.jpg`  
**What happens:** Their chat on a phone screen. The photos they send each other pop up in message bubbles.  
**PDF prompt / how to make it:** A simple phone chat drawn in the edit. Her photo of the castle slides in as a message bubble, then his photo of the campus answers it. Later his Chicago photo arrives the same way. Clean white bubbles, no names, no timestamps, no dates. The bubbles can float over shots 2.06 to 2.11.  
**Notes:** No times or dates anywhere in the chat; they would give the year away.  
**New approach (this handoff):** Route E (Section 7.4): made in the edit, not AI.  

#### 2.08 — His reply
*Create a start frame · use ~2 s*  
Photos in the PDF pack: `C2_msu-building.jpg`  
**What happens:** On campus in Michigan he gets her photo, smiles, and photographs his campus to send back.  
**PDF prompt:** A sunny university campus with a curved red-brick building with tall glass windows, big oak trees and a green lawn. The young man (tall, short dark hair, fair skin, clean-shaven), in a green T-shirt and jeans, stops on the path, looks at his phone and smiles, then holds the phone up and takes a photo of the building. Dappled sunlight through the leaves, slow push-in.  
**Notes:** His photo from 2.05b is a good extra reference for his look in this chapter.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.09 — Michigan life
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C2_lansing-mascot-him.jpg`  
**What happens:** A street fair in Lansing. He poses with the Spartan mascot, who flexes; he laughs and flexes back.  
**PDF prompt:** Animate this photo: a sunny street festival in a city centre, red-brick buildings and inflatable games behind. A young man in a white T-shirt and grey jeans stands next to a costumed Spartan mascot. The mascot flexes its arm; the young man laughs and flexes his arm too. People stroll in the background. Slow push-in.  
**Notes:** A light, funny beat in the montage. If the street signs warp, soften them.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 2.10 — Chicago
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C2_chicago-him.jpg`  
**What happens:** A trip to Chicago. At night on the river he poses for a photo, then takes one of the lit-up skyline to send her. Fix the photo first: Remove the large lit lettering on the tower behind him (top right). Lettering warps in AI video and pulls the eye.  
**PDF prompt:** Animate this photo: night in Chicago, a young man in a cream fleece jacket stands at a stone balustrade above the river, skyscraper lights reflected in the water and a tour boat gliding past. He smiles, takes his hands out of his pockets, then turns and photographs the skyline with his phone. The water shimmers. Slow push-in.  
**Notes:** This photo can also be the one he sends her in the chat (2.07).  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 2.11 — “Wow”
*Create a start frame · use ~2 s*  
Photos in the PDF pack: `C2_edinburgh-meadows.jpg`  
**What happens:** In a sunny Edinburgh park she opens his photo and lights up.  
**PDF prompt:** A wide green park in Edinburgh on a sunny day, big trees and students relaxing on the grass. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a light knit top and jeans, sits on the grass and looks at her phone; her eyes widen and she breaks into a delighted smile, a hand over her mouth. Soft sunlight, slow push-in.  
**Notes:** Her photos from 2.05a and 2.06 are good extra references for her look in this chapter.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.12a — Studying: Edinburgh
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C2_edinburgh-uni-building.jpg`  
**What happens:** The term begins. She studies inside an old stone university building, autumn trees outside.  
**PDF prompt:** Inside an old stone University of Edinburgh building: a quiet study room with tall white sash windows and autumn trees outside. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a cosy knit sweater, sits at a wooden desk with her laptop and notebooks, typing, then pauses and looks out of the window. Soft afternoon light, slow push-in.  
**Notes:** Split screen with 2.12b. The photo shows the outside of the building for style.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.12b — Studying: Michigan State
*Create a start frame · use ~3 s · side by side with 2.12a (her left, him right)*  
Photos in the PDF pack: `C2_msu-international-center.jpg`  
**What happens:** He studies at Michigan State, by the tall windows of the International Center.  
**PDF prompt:** A bright university hall with tall windows looking onto red-brick buildings and trees, a staircase and a metal globe sculpture. The young man (tall, short dark hair, fair skin, clean-shaven), in a hoodie, sits at a table by the windows with his laptop and books, studying, then rubs his eyes and stretches. Soft daylight, slow push-in.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.13a — Winter: Edinburgh
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C2_edinburgh-castle.jpg`  
**What happens:** Winter arrives. Under grey skies she walks to university in a warm coat and scarf, the castle above her.  
**PDF prompt:** A cold grey winter day in Edinburgh, the castle on its rock above bare trees, wind and light drizzle. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a long camel wool coat and a cream scarf, walks along the path below with her hands in her pockets, the wind in her hair. Slow tracking shot.  
**Notes:** Split screen with 2.13b.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.13b — Winter: Michigan
*Create a start frame · use ~3 s · side by side with 2.13a (her left, him right)*  
Photos in the PDF pack: `C2_msu-building.jpg`  
**What happens:** Deep snow in Michigan. The same building from the summer shot, now buried in snow; he walks past in a thick jacket.  
**PDF prompt:** The same curved red-brick university building with tall glass windows, now in deep winter: snow covers the lawn, the paths and the bare oak branches, and snow is falling. The young man (tall, short dark hair, fair skin, clean-shaven), in a dark puffer jacket, beanie and scarf, walks along the snowy path, his breath visible in the cold. Soft grey light, slow push-in.  
**Notes:** First make a winter version of the summer photo (same view, deep snow), then animate it. The same place in summer and then in winter shows time passing without any dates.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.14a — The call: her
*Create a start frame · KEY SHOT · use ~4 s*  
**What happens:** No photo of this moment. Use the face references on page 3. An evening video call. In her room in Edinburgh she talks to him on her laptop, smiling and encouraging him.  
**PDF prompt:** A cosy student room in Edinburgh in the evening, a warm desk lamp and rain on the dark window. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a soft oversized sweater, sits at her desk facing her laptop on a video call, smiling and talking warmly, then laughs at something on the screen. Warm light on her face, slow push-in.  
**Notes:** Split screen with 2.14b: her on the left, him on the right, as if they look at each other through their screens. Keep the laptop screens soft or out of view.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 2.14b — The call: him
*Create a start frame · use ~4 s · side by side with 2.14a (her left, him right)*  
**What happens:** In his room in Michigan, snow outside. He turns his laptop to the window to show her the snow, and they both laugh. No photo of this moment. Use the face references on page 3.  
**PDF prompt:** A student room in Michigan in the evening, heavy snow falling outside the window. The young man (tall, short dark hair, fair skin, clean-shaven), in a hoodie, sits at his desk on a video call on his laptop, smiling. He turns the laptop toward the window to show the snow, then turns it back and laughs. Warm lamp light inside, cold blue light from the window, slow push-in.  
**Notes:** Closes this part of the chapter. The New Year comes next.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  


### Chapter 3 New Year together

#### 3.01 — Together again
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C3_edinburgh-castle-families.jpg`  
**What happens:** Edinburgh Castle on a bright winter day. Both families stand together on the esplanade: his mother and brother, her mother, and the two of them. Fix the photo first: Soften or remove the lettering on the trailers at the left.  
**PDF prompt:** Animate this photo: five people in warm winter coats and hats stand together on a wide wet esplanade in front of a stone castle, bright low winter sun and long shadows. They smile; the young woman in a burgundy coat and cream scarf leans slightly toward the young man in a grey puffer jacket. Visitors stroll past behind them. Slow push-in.  
**Notes:** Keep motion small so every face stays true.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.02 — London lights
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C3_london-street-lights.jpg`, `C3_london-admiralty.jpg`, `C3_trafalgar-tree.jpg`  
**What happens:** London at Christmas: golden lights strung across the street, black cabs and red buses passing. Fix the photo first: Shop names and number plates will warp. Soften them.  
**PDF prompt:** Animate this photo: a London shopping street at dusk with golden branch-shaped Christmas lights strung across it. Black cabs and a red double-decker bus drive through, people cross the road and the lights twinkle. Slow push-in.  
**Notes:** Two more London cutaways in the pack: the red bus at dusk and the Trafalgar Square tree (C3_london-admiralty.jpg, C3_trafalgar-tree.jpg).  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 3.03 — Under the Christmas arch
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C3_christmas-arch-families.jpg`  
**What happens:** Both families together under a big Christmas arch of greenery and red bows.  
**PDF prompt:** Animate this photo: five people in winter jackets stand together in front of a large Christmas arch of greenery, red bows and baubles at a grand entrance, olive trees in stone planters on either side. They smile and lean in closer; a light breeze moves the ribbons. Slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.04 — The winter fair
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C3_winter-wonderland.jpg`, `C3_ice-kingdom.jpg`  
**What happens:** Night at the Christmas fair. The two of them and his brother laugh and make peace signs among the bright stalls. Fix the photo first: Stall signs will warp. Soften them.  
**PDF prompt:** Animate this photo: night at a bright Christmas funfair with glowing candy-cane stalls and fairground lights. A young woman in a grey beanie and black puffer jacket, a tall young man in a grey puffer jacket and a boy in glasses laugh and make peace signs at the camera; the lights twinkle and people walk past. Slow push-in.  
**Notes:** The lit castle (C3_ice-kingdom.jpg) works as a one-second cutaway before this shot.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.05 — Tower Bridge
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C3_tower-bridge-families.jpg`  
**What happens:** Both families by the river at night, Tower Bridge glowing behind them in the fog. Fix the photo first: Remove the shopping-bag advert at the bottom right.  
**PDF prompt:** Animate this photo: five people in winter coats stand at a riverside railing at night with Tower Bridge lit up behind them in light fog. They smile, a boat glides past on the river and the bridge lights glow. Slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.06 — By the tree
*Animate a real photo · KEY SHOT · use ~3 s*  
Photos in the PDF pack: `C3_hotel-tree-couple.jpg`  
**What happens:** Just the two of them, by a big Christmas tree, city lights in the window behind.  
**PDF prompt:** Animate this photo: a young couple stands beside a tall Christmas tree decorated with red and gold baubles in a hotel lounge, a large window behind them full of twinkling city lights. She smiles softly and tilts her head toward him; he smiles. The tree lights twinkle. Slow push-in.  
**Notes:** The quiet moment of the chapter. Keep it slow.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.07 — New Year’s Eve
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C3_new-year-families.jpg`  
**What happens:** New Year’s Eve. Everyone dressed up at the top of the hotel staircase before dinner.  
**PDF prompt:** Animate this photo: five people dressed up for an evening out stand together at the top of a grand hotel staircase, warm light and decorated Christmas trees behind them. They smile; the young woman in a long white knit dress turns slightly toward the young man in a dark suit. Subtle motion, slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.08 — The dinner
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C3_new-year-dinner.jpg`  
**What happens:** At the New Year’s Eve dinner, the two of them at their table under the hanging greenery.  
**PDF prompt:** Animate this photo: a young couple sits at a dinner table in an elegant hotel restaurant, greenery and fairy lights hanging from the balcony above, gold Christmas crackers on the table. She smiles and turns to look at him; he smiles back. A waiter moves softly in the background. Slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 3.09 — Midnight
*Create a start frame · use ~3 s*  
Photos in the PDF pack: `C3_thames-night.jpg`  
**What happens:** Midnight. Fireworks burst over the Thames and the city lights.  
**PDF prompt:** New Year’s midnight in London: fireworks burst over the River Thames, the lit city skyline and the river reflecting every colour, crowds on the riverbank cheering. Wide shot, slow push-in.  
**Notes:** No countdown numbers and no year anywhere. The photo shows the real river view from that night.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  


### Chapter 4 Graduations and home

#### 4.01a — Her graduation
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C4_graduation-her-cap-raised.jpg`, `C4_graduation-hercap-on.jpg`  
**What happens:** In front of McEwan Hall in her gown, she lifts her cap and smiles over her shoulder.  
**PDF prompt:** Animate this photo: a young woman in a black graduation gown over a long white dress stands on a wet stone square in front of a grand domed sandstone hall in golden lateafternoon light. She lifts her graduation cap higher and smiles over her shoulder; other graduates move in the background and clouds drift. Slow push-in.  
**Notes:** Split screen with 4.01b: her on the left, him on the right. Alternative photo: C4_graduation-her-cap-on.jpg.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 4.01b — His graduation
*Animate a real photo · use ~3 s · side by side with 4.01a (her left, him right)*  
Photos in the PDF pack: `C4_graduation-him-msu.jpg`  
**What happens:** At Michigan State, in cap and gown with his diploma, his sister beside him. Fix the photo first: Soften the “No bags” signs.  
**PDF prompt:** Animate this photo: a young man in a black graduation cap and gown holds a rolled diploma outside a modern glass arena on an overcast spring day, a young woman in a brown blazer holding his arm. They smile; he lifts the diploma slightly while people mingle in the background. Slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 4.02 — McEwan Hall
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C4_mcewan-dome.jpg`, `C4_mcewan-choir.jpg`  
**What happens:** Inside the hall: the painted, gilded dome above the families in the galleries.  
**PDF prompt:** Animate this photo: looking up at the gilded, painted dome of a grand circular hall, arched windows and columns below, families watching from the galleries. Warm light, a very slow upward tilt.  
**Notes:** The choir photo works as a short cutaway, but it has many faces, so keep its motion very small.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 4.03 — The pipers
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C4_pipers.jpg`  
**What happens:** Outside, a piper and a drummer play as the graduates come out.  
**PDF prompt:** Animate this photo: outside a sandstone hall at dusk, a Scottish piper in full Highland dress plays the bagpipes and a drummer in a kilt plays a snare drum, graduates in gowns walking past under a lit street lamp. Slow push-in.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 4.04 — Flowers
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C4_graduation-her-family.jpg`  
**What happens:** She holds a big bouquet with her family around her, low sun on the old buildings.  
**PDF prompt:** Animate this photo: a young woman in a graduation gown over a white dress holds a large bouquet of flowers, standing with two women in long coats and a boy in a cream sweater on a wet stone square in front of a grand sandstone hall, low golden sunlight. They smile and lean together. Subtle motion, slow push-in.  
**Notes:** Keep motion small so every face stays true.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 4.05 — Flying home
*Made in the edit · use ~3 s*  
**What happens:** A globe at night. Two glowing flight paths, one from Michigan and one from Edinburgh, arc across the world and meet in Baku. No photo needed.  
**PDF prompt / how to make it:** Best made as a 3D globe animation in the edit, so the geography is right. A realistic Earth at night seen from space, city lights glowing. One glowing line rises from Michigan, USA, and one from Edinburgh, Scotland; both arc east and meet over Baku with a soft flash of light. Only the word “Baku” may appear on screen. No dates.  
**Notes:** If made with AI instead, check that the lines start and end in the right places. AI often gets maps wrong.  
**New approach (this handoff):** Route E (Section 7.4): made in the edit, not AI.  

#### 4.06 — Home
*Create a start frame · KEY SHOT · use ~4 s*  
Photos in the PDF pack: `C2_airport-terminal.jpg`  
**What happens:** Back at the airport in Baku, at the same twin escalators from shot 2.02. Now they ride down from either side and meet in the middle by the tree.  
**PDF prompt:** Symmetrical wide shot of an airport terminal hall with two escalators on either side of a tall green tree in the centre. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a light coat, rides down the left escalator with her suitcase, and the young man (tall, short dark hair, fair skin, clean-shaven), in a dark jacket, rides down the right one with his. At the bottom they walk toward each other and meet by the tree, smiling. The camera holds centred and pushes in slowly.  
**Notes:** Mirrors shot 2.02, where they went separate ways from this same spot. Frame it exactly the same way.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  


### Chapter 5 Army

#### 5.01 — In uniform
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C5_him-uniform.jpg`  
**What happens:** He stands at the base in his uniform, ready for his service.  
**PDF prompt:** Animate this photo: a young man in a green digital-camouflage military uniform and matching cap stands on a wide sunlit concrete square in front of a long brick building, a fence with anchor emblems behind him. He straightens, gives a small calm smile, then turns his head toward the building. A light breeze, clouds drift. Slow push-in.  
**Notes:** This photo is also the reference for his uniform in 5.02. Match it exactly.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 5.02 — Watching him go
*Create a start frame · KEY SHOT · use ~3 s*  
Photos in the PDF pack: `C5_him-uniform.jpg`, `C5_visitfamilies.jpg`  
**What happens:** Close on her face as she watches him walk away toward the base gate. She tries to smile, but her eyes are sad.  
**PDF prompt:** Close-up of the young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), in a cream coat, standing on a wide concrete square on a grey day. In the soft-focus background the young man (tall, short dark hair, fair skin, clean-shaven), in a green digital-camouflage military uniform and matching cap, walks away toward a stone gate arch. She watches him go, tries to smile, and her eyes glisten. Shallow depth of field, slow motion, very slow push-in.  
**Notes:** Keep the gate lettering out of focus so it doesn’t warp. Her face references are on page 3.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 5.03 — Waiting
*Create a start frame · use ~3 s*  
**What happens:** No photo of this moment. Use the face references on page 3. She waits. By her window in Baku she looks at his photo on her phone while the seasons change outside.  
**PDF prompt:** A bedroom window in Baku overlooking the city and the Caspian Sea. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup) sits on the window seat holding her phone, looking at a photo of him, then looks out at the city. Outside, the seasons change in a slow time-lapse from summer to autumn to winter and into spring. Soft light, very slow push-in.  
**Notes:** No calendar, clock or date anywhere. The seasons alone show the time.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 5.04 — Visiting day
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C5_visit-families.jpg`  
**What happens:** Visiting day at the base. She and the families stand with him in front of the gate. Fix the photo first: Blur the car number plates on the left. Keep the gate lettering unchanged, or soften it if it warps.  
**PDF prompt:** Animate this photo: a group of family members stand on a wide concrete square in front of a stone gate arch, a young man in a green digital-camouflage military uniform and matching cap in the middle with a young woman in white beside him. They smile; a light breeze moves hair and coats while people walk in the background. Subtle motion, slow push-in.  
**Notes:** Many faces here, so keep motion very small.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  


### Chapter 6 Asking for her hand

#### 6.01 — Hə Almağa Gəlmişik
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C6_he-almaga-sign.jpg`  
**What happens:** The sign among white and blue flowers and crystal favours: “Hə Almağa Gəlmişik”. Guests know straight away what day this is. Fix the photo first: The letters must not change. Keep all motion on the light and flowers. If the letters warp, use the still photo with a slow zoom instead.  
**PDF prompt:** Animate this photo: a clear arched sign standing among white roses, calla lilies and pale blue flowers, rows of small crystal favours tied with ribbon in front of it. Soft light glints across the crystal and the petals stir slightly. Very slow push-in.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 6.02 — The table is set
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C6_table-set.jpg`  
**What happens:** The long table laid in white and gold, candles lit, waiting for the guests. Fix the photo first: Turn off the TV on the left (make the screen plain black) so its words and menu don’t show.  
**PDF prompt:** Animate this photo: a long mirrored dining table laid with white and gold plates, crystal glasses, tall white candles and white flowers, white chairs on both sides and soft daylight through the curtains. The candle flames flicker and light moves across the crystal. Slow push-in along the table.  
**Notes:** No people in this shot.  
**New approach (this handoff):** Route N (Section 7.3): real camera/scene motion from the photo; no identity lock needed.  

#### 6.03 — Waiting to come in
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C6_her-waiting-calla.jpg`  
**What happens:** In the next room she waits in white, a calla lily in her hand, and smiles to herself.  
**PDF prompt:** Animate this photo: a young woman in an elegant white outfit with pearl buttons, her dark hair in a low bun, stands in profile holding a single white calla lily beside a table of white and blue flowers and sweets. She lowers her eyes and smiles softly to herself, a little shy. Very subtle motion, slow push-in.  
**Notes:** Echoes her shy smile in the corridor (1.03), where the story began.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 6.04 — The tea
*Animate a real photo · use ~2 s*  
Photos in the PDF pack: `C6_her-tea-tray.jpg`  
**What happens:** She holds the tray of tea in armudu glasses, ready to take it in. Fix the photo first: Keep the sign behind her exactly as it is, or soften it if the letters warp.  
**PDF prompt:** Animate this photo: a young woman in an elegant white outfit holds a gold mirrored tray of pear-shaped armudu tea glasses decorated with tiny white flowers, white and blue flower arrangements behind her. She takes a small breath, smiles and steps forward with the tray; steam rises gently from the tea. Slow push-in.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 6.05 — Serving the tea
*Create a start frame · KEY SHOT · use ~3 s*  
Photos in the PDF pack: `C6_serving-tea.jpg`, `C6_table-set.jpg`  
**What happens:** At the table she leans in and sets a glass of tea down. Only she is seen clearly. The guests at the table stay out of focus, with no faces visible.  
**PDF prompt:** Close shot at a long table laid with white and gold plates, crystal glasses and a tall white candle. The young woman (long dark-brown hair, fair skin, dark eyes, soft natural makeup), her dark hair in a low bun, in an elegant white outfit with a high embroidered collar and pearl-buttoned cuffs, leans in and gently sets an armudu glass of tea on its saucer at a place setting, with a soft smile. The seated guests are only blurred dark suits at the edge of the frame, their faces never visible. Shallow depth of field, focus on her and the tea, slow push-in.  
**Notes:** Do not animate the real photo: the guests’ faces must not appear. Use it only as a reference for her dress, hair and the table, and make a new start frame without anyone else’s face.  
**New approach (this handoff):** Route A (Section 7.1): FLUX 3 start frame from her/his real photo + location photo -> Kling 4.0 image-to-video with REAL action and camera moves (8–10 s, no end frame) -> Genjutsu identity lock -> QA.  

#### 6.06 — “Hə”
*Animate a real photo · use ~3 s*  
Photos in the PDF pack: `C6_her-tea-glass.jpg`  
**What happens:** She holds one glass of tea and smiles. The camera moves in slowly on the glass.  
**PDF prompt:** Animate this photo: a young woman in an elegant white outfit holds a single armudu glass of tea on a crystal saucer and smiles warmly at the camera. Steam rises from the tea. The camera pushes in slowly until the glass of tea fills the frame.  
**Notes:** The last AI image. Lead straight into the fade in 6.07.  
**New approach (this handoff):** Route B (Section 7.2): clean + 16:9 the real photo -> Kling 4.0 image-to-video where the photo moment becomes a real moving scene (8–10 s, no end frame) -> Genjutsu identity lock for the couple -> QA. Any PDF wording like 'very subtle motion' / 'keep motion small' is SUPERSEDED.  

#### 6.07 — Into the real footage
*Made in the edit · use ~1 s*  
**What happens:** A soft fade to white leads straight into the real footage of his proposal. No photo needed.  
**PDF prompt / how to make it:** Fade the last frame of 6.06 to soft white over about one second, then cut to the real proposal footage. Grade the end of the AI film to match the colour of the real footage so the change feels natural.  
**Notes:** Their names and 27.12.2026 can close the whole film after the proposal footage. End of the AI film. The real proposal footage follows.  
**New approach (this handoff):** Route E (Section 7.4): made in the edit, not AI.  

---

## Appendix C — Helper scripts from the previous session (Python 3 + OpenCV + ffmpeg)

Paths inside them point to the old session's scratch folder; change `S` / paths before use.

### `widen_prep.py`

```python
"""Make a 16:9 canvas with the real photo untouched in the centre, plus a mask
of the two side areas that need painting (white = paint, black = keep).

usage: widen_prep.py ORIGINAL OUT_CANVAS OUT_MASK
"""
import sys

import cv2
import numpy as np

orig = cv2.imread(sys.argv[1])
h, w = orig.shape[:2]
W = int(round(h * 16 / 9 / 2)) * 2
x0 = (W - w) // 2
# sides start as a blurred mirror of the photo so the tones are already right
pad = cv2.copyMakeBorder(orig, 0, 0, x0, W - w - x0, cv2.BORDER_REFLECT_101)
blur = cv2.GaussianBlur(pad, (0, 0), 25)
canvas = blur.copy()
canvas[:, x0:x0 + w] = orig
mask = np.full((h, W), 255, np.uint8)
mask[:, x0 + 12:x0 + w - 12] = 0
cv2.imwrite(sys.argv[2], canvas)
cv2.imwrite(sys.argv[3], mask)
print(sys.argv[1], "->", W, "x", h, "photo at x =", x0)
```

### `composite.py`

```python
"""Paste the real photo back over the centre of an AI-widened frame.

The widening tool repaints the whole picture, which changes faces. This keeps
only its new left/right sides and restores the original pixels in the middle,
with a soft seam so the join is not visible.

usage: composite.py ORIGINAL WIDENED OUT [feather_px]
"""
import sys

import cv2
import numpy as np

orig_path, wide_path, out_path = sys.argv[1:4]
feather = int(sys.argv[4]) if len(sys.argv) > 4 else 48

orig = cv2.imread(orig_path)
wide = cv2.imread(wide_path)
oh, ow = orig.shape[:2]

# Work at the original photo's pixel scale so real faces are never upscaled.
scale = oh / wide.shape[0]
wide_s = cv2.resize(wide, (round(wide.shape[1] * scale), oh), interpolation=cv2.INTER_AREA)
ch, cw = wide_s.shape[:2]

# Find where the original sits inside the widened frame.
sift = cv2.SIFT_create(6000)
k1, d1 = sift.detectAndCompute(cv2.cvtColor(orig, cv2.COLOR_BGR2GRAY), None)
k2, d2 = sift.detectAndCompute(cv2.cvtColor(wide_s, cv2.COLOR_BGR2GRAY), None)
matches = cv2.BFMatcher().knnMatch(d1, d2, k=2)
good = [m for m, n in matches if m.distance < 0.7 * n.distance]
src = np.float32([k1[m.queryIdx].pt for m in good])
dst = np.float32([k2[m.trainIdx].pt for m in good])
M, inl = cv2.estimateAffinePartial2D(src, dst, method=cv2.RANSAC, ransacReprojThreshold=2.0)
s = float(np.hypot(M[0, 0], M[1, 0]))
print(f"matches={len(good)} inliers={int(inl.sum())} scale={s:.4f} "
      f"rot={np.degrees(np.arctan2(M[1, 0], M[0, 0])):.3f}deg tx={M[0, 2]:.1f} ty={M[1, 2]:.1f} "
      f"(expected tx~{(cw - ow) / 2:.1f}, ty~0)")

warped = cv2.warpAffine(orig, M, (cw, ch), flags=cv2.INTER_LANCZOS4)
mask = cv2.warpAffine(np.full((oh, ow), 255, np.uint8), M, (cw, ch), flags=cv2.INTER_LINEAR)

# The widening tool often shifts brightness and colour. Pull its sides back to
# the real photo's tones, measured where the two overlap, so the sky and walls
# do not change shade at the join.
inside = mask > 250
wf = wide_s.astype(np.float32)
for c in range(3):
    a = wf[..., c][inside]
    b = warped[..., c][inside].astype(np.float32)
    gain = float(np.clip(b.std() / max(a.std(), 1e-3), 0.7, 1.4))
    wf[..., c] = (wf[..., c] - a.mean()) * gain + b.mean()
wide_s = np.clip(wf, 0, 255).astype(np.uint8)

# Soft seam on the left and right edges only; keep full strength at top/bottom
# where the original already reaches the frame edge.
cols = np.where(mask.max(axis=0) > 250)[0]
x0, x1 = int(cols.min()), int(cols.max())

# Optional: pull each painted side to the exposure of the photo right at the
# seam (row by row, heavily smoothed), for sides that came out brighter or
# darker than the real photo.
if len(sys.argv) > 5 and sys.argv[5] == "tone":
    S = 110
    wf = wide_s.astype(np.float32)
    mid = (x0 + x1) // 2
    for side in ("L", "R"):
        if side == "L":
            ins = warped[:, x0 + 6:x0 + 6 + S].astype(np.float32)
            outs = wf[:, max(0, x0 - 6 - S):max(1, x0 - 6)]
            sl = slice(0, mid)
        else:
            ins = warped[:, x1 - 6 - S:x1 - 6].astype(np.float32)
            outs = wf[:, x1 + 6:x1 + 6 + S]
            sl = slice(mid, cw)
        if outs.shape[1] < 8:
            continue
        g = (np.median(ins, axis=1) + 4.0) / (np.median(outs, axis=1) + 4.0)   # rows x 3
        g = cv2.GaussianBlur(g.astype(np.float32), (1, 0), sigmaX=0.01, sigmaY=140)
        g = np.clip(g, 0.5, 1.5)
        wf[:, sl] *= g[:, None, :]
        print(f"tone {side}: gain mean {g.mean(axis=0).round(2)}")
    wide_s = np.clip(wf, 0, 255).astype(np.uint8)
ramp = np.ones(cw, np.float32)
ramp[:x0] = 0
ramp[x1 + 1:] = 0
ramp[x0:x0 + feather] = np.linspace(0, 1, feather)
ramp[x1 - feather + 1:x1 + 1] = np.linspace(1, 0, feather)
alpha = (mask.astype(np.float32) / 255.0) * ramp[None, :]
# Where the warped photo does not reach the top/bottom (tiny shifts), fall back to the widened frame.
alpha = alpha[..., None]
out = (warped.astype(np.float32) * alpha + wide_s.astype(np.float32) * (1 - alpha)).round().astype(np.uint8)

# Crop to exact 16:9, centred on the original photo.
tw = round(ch * 16 / 9)
if cw > tw:
    cx = (x0 + x1) / 2
    left = int(round(min(max(cx - tw / 2, 0), cw - tw)))
    out = out[:, left:left + tw]
    print(f"cropped to {tw}x{ch} from x={left}; original spans x={x0 - left}..{x1 - left}")
cv2.imwrite(out_path, out)
print("wrote", out_path, out.shape[1], "x", out.shape[0])
```

### `assemble.py`

```python
"""Rebuild the 25 s reference video from the face-replaced scenes.

Opening (no main faces) + three face-replaced scene groups, each fitted back
to the exact length of its source so every cut lands where it did in the
reference, then the reference's own sound is laid back on top.

usage: assemble.py OPENING.mp4 G1.mp4 G2.mp4 G3.mp4 OUT.mp4
"""
import subprocess
import sys

S = "/tmp/claude-0/-home-user-video/689a70ff-c76b-5997-9a9b-e67cdbc87305/scratchpad/"
REF = "/root/.claude/uploads/689a70ff-c76b-5997-9a9b-e67cdbc87305/bfab53d5-VIDEO-2026-11-12-16-20-21.mp4"
FPS = 24
# (source group, start in reference, end in reference, cut inside the group)
PARTS = [("g0", 0.0, 8.1333, None), ("g1", 8.1333, 14.05, 2.9167), ("g2", 14.05, 19.8833, 3.0833),
         ("g3", 19.8833, 25.0167, 1.8334)]


def dur(p):
    return float(subprocess.run(["ffprobe", "-v", "error", "-show_entries", "format=duration", "-of", "csv=p=0", p],
                                capture_output=True, text=True).stdout)


def cut_of(p):
    out = subprocess.run(["ffmpeg", "-i", p, "-vf", "select='gt(scene,0.25)',showinfo", "-f", "null", "-"],
                         capture_output=True, text=True).stderr
    ts = [float(x.split(":")[1]) for x in out.split() if x.startswith("pts_time:")]
    return ts


inputs = sys.argv[1:5]
out = sys.argv[5]
pieces = []
for (name, a, b, cut), spec in zip(PARTS, inputs):
    want = b - a
    # "A.mp4" uses one clip for the whole group; "A.mp4,B.mp4" takes the first
    # shot from A and the second shot from B (best result per shot).
    srcs = spec.split(",")
    segs = []
    if cut is None:
        segs = [(srcs[0], 0.0, dur(srcs[0]), want)]
    else:
        for k, path in enumerate(srcs if len(srcs) == 2 else [srcs[0], srcs[0]]):
            d = dur(path)
            c = min(cut_of(path), key=lambda x: abs(x - cut * d / want))
            # fit each shot to its own source length so the cut lands exactly
            segs.append((path, 0.0, c, cut) if k == 0 else (path, c, d, want - cut))
    for i, (path, s, e, w) in enumerate(segs):
        p = f"{S}swap/out/_piece_{name}_{i}.mp4"
        n = round(w * FPS)
        factor = w / (e - s)
        vf = (f"trim={s}:{e},setpts=(PTS-STARTPTS)*{factor:.6f},fps={FPS},"
              f"scale=1920:1080:flags=lanczos,setsar=1,format=yuv420p")
        subprocess.run(["ffmpeg", "-v", "error", "-y", "-i", path, "-vf", vf, "-frames:v", str(n), "-an",
                        "-c:v", "libx264", "-crf", "14", "-preset", "fast", p], check=True)
        pieces.append(p)
        print(f"{name}[{i}] src {s:.3f}-{e:.3f} -> {w:.3f}s (x{factor:.3f}) frames {n}")
lst = S + "swap/out/_list.txt"
open(lst, "w").write("".join(f"file '{p}'\n" for p in pieces))
subprocess.run(["ffmpeg", "-v", "error", "-y", "-f", "concat", "-safe", "0", "-i", lst, "-i", REF,
                "-map", "0:v", "-map", "1:a", "-c:v", "libx264", "-crf", "17", "-preset", "medium",
                "-pix_fmt", "yuv420p", "-c:a", "aac", "-b:a", "192k", "-shortest", "-movflags", "+faststart", out],
               check=True)
print("wrote", out, f"{dur(out):.2f}s")
```

### `review.py`

```python
"""Contact sheet: three frames (start, middle, end) per clip, one row each.
usage: review.py OUT.jpg CLIP [CLIP ...]"""
import os, subprocess, sys
import cv2, numpy as np
rows = []
for c in sys.argv[2:]:
    fr = []
    for t in (0.3, 2.6, 4.6):
        p = f"/tmp/_rv_{os.getpid()}.png"
        subprocess.run(["ffmpeg", "-v", "error", "-y", "-ss", str(t), "-i", c, "-frames:v", "1", "-vf", "scale=480:270", p])
        fr.append(cv2.imread(p)); os.remove(p)
    r = np.hstack(fr); cv2.putText(r, os.path.basename(c)[:-4], (8, 28), 0, 0.9, (0, 255, 255), 2); rows.append(r)
cv2.imwrite(sys.argv[1], np.vstack(rows))
```

### `globe.py`

```python
"""4.05 Flying home: a night globe with two glowing flight paths (Michigan and
Edinburgh) meeting over Baku. Made in the edit so the geography is right.

usage: globe.py OUT.mp4
"""
import subprocess
import sys

import cv2
import numpy as np
from geonamescache import GeonamesCache
from global_land_mask import globe

W, H, FPS, DUR = 1920, 1080, 24, 3.6
N = int(FPS * DUR)
R = 470                      # globe radius in px
CX, CY = W // 2, H // 2 + 20

A = (42.73, -84.48)          # East Lansing, Michigan
B = (55.95, -3.19)           # Edinburgh
C = (40.41, 49.87)           # Baku


def vec(lat, lon):
    la, lo = np.radians(lat), np.radians(lon)
    return np.array([np.cos(la) * np.cos(lo), np.cos(la) * np.sin(lo), np.sin(la)])


def arc(p, q, n=200):
    a, b = vec(*p), vec(*q)
    om = np.arccos(np.clip(a @ b, -1, 1))
    t = np.linspace(0, 1, n)[:, None]
    return (np.sin((1 - t) * om) * a + np.sin(t * om) * b) / np.sin(om)


def basis(lat0, lon0):
    """Camera looking at (lat0, lon0): returns east, north, out unit vectors."""
    out = vec(lat0, lon0)
    east = np.array([-np.sin(np.radians(lon0)), np.cos(np.radians(lon0)), 0.0])
    north = np.cross(out, east)
    return east, north, out


cities = [(c["latitude"], c["longitude"], c["population"]) for c in GeonamesCache().get_cities().values()
          if c["population"] > 60000]
cv_ = np.array([vec(la, lo) for la, lo, _ in cities])
cp = np.array([p for _, _, p in cities], np.float32)

yy, xx = np.mgrid[0:H, 0:W].astype(np.float32)
sx, sy = (xx - CX) / R, -(yy - CY) / R
rr = sx * sx + sy * sy
inside = rr <= 1.0
sz = np.sqrt(np.clip(1.0 - rr, 0, 1))

rng = np.random.default_rng(3)
stars = np.zeros((H, W), np.float32)
ys, xs = rng.integers(0, H, 900), rng.integers(0, W, 900)
stars[ys, xs] = rng.uniform(0.2, 1.0, 900)
stars = cv2.GaussianBlur(stars, (0, 0), 0.8) * 2.2

arcA, arcB = arc(A, C), arc(B, C)
ff = subprocess.Popen(["ffmpeg", "-v", "error", "-y", "-f", "rawvideo", "-pix_fmt", "bgr24", "-s", f"{W}x{H}",
                       "-r", str(FPS), "-i", "-", "-c:v", "libx264", "-crf", "15", "-pix_fmt", "yuv420p", sys.argv[1]],
                      stdin=subprocess.PIPE)
for i in range(N):
    u = i / (N - 1)
    e = u * u * (3 - 2 * u)
    lon0 = -38 + e * 62          # drift east from the Atlantic toward the Caucasus
    lat0 = 44 - e * 2
    east, north, out = basis(lat0, lon0)
    # screen -> sphere -> lat/lon
    P = sx[..., None] * east + sy[..., None] * north + sz[..., None] * out
    lat = np.degrees(np.arcsin(np.clip(P[..., 2], -1, 1)))
    lon = np.degrees(np.arctan2(P[..., 1], P[..., 0]))
    land = np.zeros((H, W), np.float32)
    land[inside] = globe.is_land(lat[inside], lon[inside]).astype(np.float32)
    land = cv2.GaussianBlur(land, (0, 0), 1.2)
    shade = (0.35 + 0.65 * sz) * inside                       # limb darkening
    img = np.zeros((H, W, 3), np.float32)
    ocean = np.array([38, 16, 6], np.float32)                 # BGR
    ground = np.array([62, 44, 30], np.float32)
    img += (ocean + (ground - ocean) * land[..., None]) * shade[..., None]
    # city lights
    d = cv_ @ out
    vis = d > 0.02
    px = (CX + R * (cv_[vis] @ east)).astype(int)
    py = (CY - R * (cv_[vis] @ north)).astype(int)
    lights = np.zeros((H, W), np.float32)
    np.add.at(lights, (py.clip(0, H - 1), px.clip(0, W - 1)), np.clip(np.log10(cp[vis]) - 4.4, 0.15, 2.5) * d[vis])
    glow = cv2.GaussianBlur(lights, (0, 0), 1.1) * 2.6 + cv2.GaussianBlur(lights, (0, 0), 5) * 2.0
    img += glow[..., None] * np.array([120, 200, 255], np.float32)
    # atmosphere rim
    rim = np.clip(1.0 - np.abs(np.sqrt(rr) - 1.0) * 28, 0, 1) ** 2
    img += rim[..., None] * np.array([150, 90, 40], np.float32) * 0.55
    img += (stars * (~inside))[..., None] * 160
    # flight paths
    prog = np.clip((u - 0.08) / 0.72, 0, 1)
    prog = prog * prog * (3 - 2 * prog)
    line = np.zeros((H, W), np.float32)
    for pts in (arcA, arcB):
        k = max(2, int(len(pts) * prog))
        seg = pts[:k]
        zz = seg @ out
        q = np.stack([CX + R * (seg @ east) * (1 + 0.0), CY - R * (seg @ north)], 1)
        for j in range(1, k):
            if zz[j] > 0 and zz[j - 1] > 0:
                cv2.line(line, tuple(q[j - 1].astype(int)), tuple(q[j].astype(int)), 1.0, 3, cv2.LINE_AA)
        if zz[k - 1] > 0 and prog < 1:
            cv2.circle(line, tuple(q[k - 1].astype(int)), 6, 2.0, -1, cv2.LINE_AA)
    lg = line + cv2.GaussianBlur(line, (0, 0), 6) * 1.6 + cv2.GaussianBlur(line, (0, 0), 18) * 1.2
    img += lg[..., None] * np.array([150, 215, 255], np.float32)
    # meeting flash and the one allowed word
    cz = vec(*C) @ out
    bx, by = int(CX + R * (vec(*C) @ east)), int(CY - R * (vec(*C) @ north))
    if prog >= 1 and cz > 0:
        fl = np.clip((u - 0.80) / 0.12, 0, 1)
        flash = np.zeros((H, W), np.float32)
        cv2.circle(flash, (bx, by), 10, 1.0, -1, cv2.LINE_AA)
        fg = cv2.GaussianBlur(flash, (0, 0), 26) * 30 * (1.2 - 0.5 * fl) + cv2.GaussianBlur(flash, (0, 0), 6) * 6
        img += fg[..., None] * np.array([170, 225, 255], np.float32) * fl
        t8 = np.zeros((H, W), np.uint8)
        cv2.putText(t8, "Baku", (bx + 34, by + 12), cv2.FONT_HERSHEY_DUPLEX, 1.25, 255, 2, cv2.LINE_AA)
        txt = t8.astype(np.float32) / 255.0
        img += (txt + cv2.GaussianBlur(txt, (0, 0), 4) * 0.6)[..., None] * 235 * fl
    ff.stdin.write(np.clip(img, 0, 255).astype(np.uint8).tobytes())
ff.stdin.close()
ff.wait()
print("wrote", sys.argv[1])
```

### `extras.py`

```python
"""Edit-only shots: the chat bubbles (2.07) and the sign (6.01).

usage: extras.py chat1|chat2|sign OUT.mp4
"""
import subprocess
import sys

import cv2
import numpy as np

W, H, FPS = 1920, 1080, 24
S = "/tmp/claude-0/-home-user-video/689a70ff-c76b-5997-9a9b-e67cdbc87305/scratchpad/"


def writer(path):
    return subprocess.Popen(["ffmpeg", "-v", "error", "-y", "-f", "rawvideo", "-pix_fmt", "bgr24", "-s", f"{W}x{H}",
                             "-r", str(FPS), "-i", "-", "-c:v", "libx264", "-crf", "15", "-pix_fmt", "yuv420p", path],
                            stdin=subprocess.PIPE)


def frame_of(clip, t):
    tmp = "/tmp/_ex_frame.png"
    subprocess.run(["ffmpeg", "-v", "error", "-y", "-ss", str(t), "-i", clip, "-frames:v", "1", "-vf",
                    f"scale={W}:{H}", tmp])
    return cv2.imread(tmp)


def rounded(img, r):
    h, w = img.shape[:2]
    m = np.zeros((h, w), np.uint8)
    cv2.rectangle(m, (r, 0), (w - r, h), 255, -1)
    cv2.rectangle(m, (0, r), (w, h - r), 255, -1)
    for cx, cy in ((r, r), (w - r, r), (r, h - r), (w - r, h - r)):
        cv2.circle(m, (cx, cy), r, 255, -1, cv2.LINE_AA)
    return cv2.GaussianBlur(m, (0, 0), 0.8).astype(np.float32) / 255.0


def paste(canvas, img, alpha, x, y):
    h, w = img.shape[:2]
    x0, y0, x1, y1 = max(x, 0), max(y, 0), min(x + w, W), min(y + h, H)
    if x1 <= x0 or y1 <= y0:
        return
    a = alpha[y0 - y:y1 - y, x0 - x:x1 - x, None]
    canvas[y0:y1, x0:x1] = canvas[y0:y1, x0:x1] * (1 - a) + img[y0 - y:y1 - y, x0 - x:x1 - x] * a


def bubble(photo, w=470, pad=14):
    """A white rounded message bubble holding one photo."""
    ph = cv2.imread(photo)
    h0, w0 = ph.shape[:2]
    side = min(h0, w0 * 3 // 4 * 1)
    ch = min(h0, int(w0 * 0.72))
    y0 = max(0, (h0 - ch) // 3)
    ph = ph[y0:y0 + ch]
    iw = w - 2 * pad
    ih = int(iw * ph.shape[0] / ph.shape[1])
    ph = cv2.resize(ph, (iw, ih), interpolation=cv2.INTER_AREA).astype(np.float32)
    b = np.full((ih + 2 * pad, w, 3), 252, np.float32)
    ia = rounded(ph, 22)
    b[pad:pad + ih, pad:pad + iw] = b[pad:pad + ih, pad:pad + iw] * (1 - ia[..., None]) + ph * ia[..., None]
    return b, rounded(b, 34)


def ease(u):
    u = float(np.clip(u, 0, 1))
    return 1 - (1 - u) ** 3


def chat(out, bg_clip, bg_t, items, dur):
    bg = frame_of(bg_clip, bg_t).astype(np.float32)
    bg = cv2.GaussianBlur(bg, (0, 0), 28) * 0.62
    # soft phone-shaped panel in the middle
    bubs0 = [bubble(S + p_, w=560) for p_, _, _ in items]
    pw = 720
    ph_ = 70 + sum(b.shape[0] + 26 for b, _ in bubs0) + 44
    px, py = (W - pw) // 2, (H - ph_) // 2
    panel = np.full((ph_, pw, 3), 236, np.float32)
    pa = rounded(panel, 64)
    sh = np.zeros((H, W), np.float32)
    sh[py + 14:py + ph_ + 14, px:px + pw] = 1
    sh = cv2.GaussianBlur(sh, (0, 0), 30)[..., None]
    bubs = [(bb, side, t0) for bb, (p_, side, t0) in zip(bubs0, items)]
    ff = writer(out)
    n = int(dur * FPS)
    for i in range(n):
        t = i / FPS
        f = bg * (1 - 0.45 * sh)
        f = f * (1.0 + 0.02 * t)
        paste(f, panel, pa * 0.97, px, py)
        y = py + 70
        for (b, ba), side, t0 in bubs:
            e = ease((t - t0) / 0.38)
            bx = px + 34 if side == "L" else px + pw - 34 - b.shape[1]
            if e > 0:
                paste(f, b, ba * e, bx, int(y + (1 - e) * 46))
            y += b.shape[0] + 26
        ff.stdin.write(np.clip(f, 0, 255).astype(np.uint8).tobytes())
    ff.stdin.close()
    ff.wait()


def sign(out, dur=3.0):
    o = cv2.imread(S + "film/orig/6.01.jpg")
    h0, w0 = o.shape[:2]
    ff = writer(out)
    n = int(dur * FPS)
    for i in range(n):
        u = i / (n - 1)
        z = 1.0 + 0.06 * u                       # very slow push-in, letters untouched
        fh = int(H * z)
        fg = cv2.resize(o, (int(w0 * fh / h0), fh), interpolation=cv2.INTER_LANCZOS4)
        bgs = 1.15 + 0.03 * u
        bw = int(W * bgs)
        bgim = cv2.resize(o, (bw, int(h0 * bw / w0)), interpolation=cv2.INTER_LINEAR)
        by = int((bgim.shape[0] - H) * 0.30)
        bx = (bw - W) // 2
        f = cv2.GaussianBlur(bgim[by:by + H, bx:bx + W], (0, 0), 30).astype(np.float32) * 0.80
        y0 = (fh - H) // 3
        fg = fg[y0:y0 + H]
        x = (W - fg.shape[1]) // 2
        a = np.ones(fg.shape[:2], np.float32)
        k = 36
        ramp = np.linspace(0, 1, k)
        a[:, :k] *= ramp[None]
        a[:, -k:] *= ramp[::-1][None]
        paste(f, fg.astype(np.float32), a, x, 0)
        ff.stdin.write(np.clip(f, 0, 255).astype(np.uint8).tobytes())
    ff.stdin.close()
    ff.wait()


kind, out = sys.argv[1], sys.argv[2]
if kind == "chat1":
    chat(out, S + "out1/2-06.mp4", 3.6, [("film/src/pg20-000.jpg", "R", 0.20), ("film/src/pg17-000.jpg", "L", 1.05)], 2.5)
elif kind == "chat2":
    chat(out, S + "out3/2-10.mp4", 4.4, [("film/orig/2.10.jpg", "L", 0.20)], 1.7)
else:
    sign(out)
print("wrote", out)
```

