# OUR STORY — Scenario Handoff v2 (final shot plan, approved by the user)

**For:** the video-maker AI (Claude with the Higgsfield "video" MCP connector) that will make the full film.
**Built from:** `OUR_STORY_HANDOFF.md` (the production handoff, read in full) plus the user's answers to Round 0 and to every 2-second segment of the film. The raw answers, including the user's own words, are in `SCENARIO_ANSWERS.md`.
**Film:** "Our Story", about **2:02**, 16:9, 1920×1080, 24 fps. It plays at the engagement (Nişan) on **27.12.2026**, and the real proposal footage follows straight after it.

---

## 0. Read this first

1. **This file is the shot plan.** It replaces Appendix A (timeline) and the per-shot prompts of Appendix B in `OUR_STORY_HANDOFF.md`. **Everything else in that file still applies and is not repeated here in full:** what "real video" means and its acceptance tests (§2), the identity kit (§4), the rules (§5), the method that worked (§6–7), what failed (§8), tools and costs (§10), session hygiene (§11), how to talk to the user (§12), and the helper scripts (Appendix C). Attach and read both files.
2. **Names:** she is **Narmin**, he is **Zamin**. Use the names only in planning text. In model prompts write "the young woman" / "the young man". Names never appear on screen, except on the closing card **after** the real proposal footage (§12.7).
3. **Length:** 61 segments × 2 s = **2:02**. The user agreed the film may run longer than 2:00 so that no scene is lost. One continuous take (T04, Seg 04–05) may need up to 2 s more; that is allowed (final length 2:02–2:04).
4. **Everything must look filmed:** real action, real camera moves, real cuts. Never the rejected "animated photo" look. Every take below is written as timed beats with a named camera move.
5. **Faces only from the user's photos**, and every take with the couple (or the curly-haired friend) goes through the **Genjutsu identity lock** (`hf_mult_replace_object`). No exceptions, even when the first result looks fine.
6. **First production step = the whole of chapter 1 (Seg 01–16, 32 s).** Make it, assemble it with sound, run QA, and show it to the user. **Do not start chapter 2 before the user says OK.** (§3)
7. **Ask before spending.** Check the balance, show the cost of the batch, and get an OK before every paid batch. The estimate for the full film is in §15.
8. **The user writes short messages from a phone.** Keep replies short (key points, under ~1,000 characters, no links) and ask with option questions (AskUserQuestion).
9. Keep `manifest.txt` with every media ID, job ID, file name and decision. Sessions restart; Kling takes 5–10 min and Genjutsu 15–35 min per job.

### 0.1 What the user changed compared with the PDF (all already built into the takes below)
| Where | PDF draft | User's decision |
|---|---|---|
| 1.01 opening | 3 s, she packs and leaves | **8 s, 4 beats** with cuts between angles: wide dolly-in → she finishes writing and packs → a **curly-haired female friend** jokes and she laughs → she stands, waves goodbye, walks out. **The friend is a real person: the user will send her photo.** |
| 1.01 → 1.02 | cut | **No cut:** the camera follows her from a diagonal rear angle through the doorway into the corridor. |
| 1.02 | he steps out of a classroom | **He walks toward her looking at his phone, then looks up** and sees her; over her shoulder, focus pulls to him. Then reverse shot on her: **their eyes meet, she gives a small smile and her eyes stay on him.** |
| 1.03 shy smile | separate close-up, she lowers her eyes and tucks her hair | **Removed.** The small smile lives inside Seg 06. **She does not lower her eyes and does not touch her hair.** |
| 1.04 his smile | separate close-up | **Merged** into one slow-motion side shot: they pass each other without stopping, a **shared smile**, no look-back, no nod. Then a **match cut on the smile** into the café. |
| 1.06 library | he points at her screen | **She explains** something in her notebook, he nods and smiles. |
| 1.07 park | light coat / casual jacket | **Coffees in hand.** Her **short burgundy long-sleeve winter dress, long tailored coat worn open, knee-high boots**; him a casual winter jacket, sweater and trousers. Sunny winter day. |
| 2.01–2.03 travel | trench coat / dark jacket | Her **grey sweater + matching grey sweatpants**; him **blue sweater + matching blue sweatpants**. |
| 2.02 escalators | look back | Look back with a **small wave** across the tree. |
| 2.06 fountain | photo of the castle | She **walks up**, then photographs the castle; filmed **from behind her shoulder**. |
| 2.07 chat | bubbles on a phone | **Split screen: the photos fly across the divider** between her half and his half, with a soft "ping". |
| 2.09 mascot | both flex | **They pose for a photo**, then he laughs. |
| 2.10 Chicago | photographs the skyline | **He walks along the river.** |
| 2.11 "Wow" | hand over mouth | **No hand over the mouth**; eyes widen, delighted smile. |
| 2.12 studying | type / stretch | **Both busy writing notes.** |
| 2.13 winter | her camel coat | Her **long burgundy coat** and cream scarf. |
| 3.04 winter fair | peace signs | **They walk through the fair**, then turn for the peace-sign photo. |
| 3.06 by the tree | head tilt | They **walk up to the tree**; **she hangs a gold bauble**; they look at each other. No added touch. |
| 3.07 NYE | pose | They **arrive at the top** of the staircase and turn for the photo. |
| 4.06 home | light coat / dark jacket, ride down | **Summer outfits**; they are **already at the bottom** and turn to each other, then meet by the tree. |
| 6.02 table | candles flicker | **Hands (no face) place the last plate and light a candle**; the TV is **cropped out**. |
| 6.03 calla | lowers her eyes | Soft shy smile, **eyes stay up**. |
| 6.04 tea tray | steps forward | She **lifts the tray and turns to the door**. |
| 6.07 end | fade to white | **Fade through the tea steam** to soft white. |
| Closing card | names + date | **"Zamin & Narmin"** and **27.12.2026**, only after the real footage. |

---

## 1. Global settings (Round 0 answers)

| Setting | Decision |
|---|---|
| Production stack | Claude + Higgsfield: FLUX 3 start frames → Kling 4.0 motion → Genjutsu identity lock → ffmpeg edit |
| Question depth | Every 2 s (done; this plan is the result) |
| Sound | **Music + soft real sounds** (steps, chatter, café, wind, choir, bagpipes, fireworks, tea glasses). Music source still to confirm (§17). |
| Editing | **Real cuts inside scenes; soft dissolves only between chapters.** One match cut (Seg 07→08). |
| Families (no face refs) | **Medium/wide distance, gentle action.** Lock only the couple. |
| Her hair | **Follow the real photos:** long, straight, dark-brown and **down** by default; as in the photos at graduations (cap) and on the engagement day (**low bun**, Seg 57–61). |
| His face | **Light stubble**, face **slimmer** than in his photos with a defined jawline, still clearly him. |
| On-screen words | Only the PDF lines, added in the edit: "Where it all began", "Edinburgh" / "Michigan", "Chicago", "London", "Baku". Closing card after the real footage. |
| Modesty | No kissing, hugging, head on shoulder or hand-holding unless the real photo shows it. High closed necklines for her in generated outfits. Real photo outfits stay as they are (the user approved her real off-shoulder prom gown). |
| Text in the picture | No numbers, years, dates, clocks or readable signs anywhere. |

---

## 2. Inputs

### 2.1 Files to attach to the new chat
1. `OUR_STORY_HANDOFF.md`, `SCENARIO_HANDOFF.md` (this file), `SCENARIO_ANSWERS.md`.
2. The PDF "Our Story – AI video scenario (Draft 9)" — all real photos are embedded. Extract with `pdfimages -j -png file.pdf outdir/` and match them to the `C1_…`–`C6_…` names listed in each take.
3. Her 7 face photos (`IMG_0180`–`IMG_0184`, `IMG_0217`, `IMG_0218`) and his 7 (`IMG_0210`–`IMG_0216`).
4. **NEW — the curly-haired friend's photo** (the user promised to send it). Needed for T01, T03, T04. Ask for it in the first message if it is not attached. Head-and-shoulders crop, front or 3/4.
5. Quality bar: `where-it-all-began-v2.mp4`.

### 2.2 Reference sets (Higgsfield IDs; re-upload any that do not resolve)
Use these short names everywhere below.

**HER7** — lock order, always all seven:
| Ref | ID | View |
|---|---|---|
| H1 | `2da05287-989d-4f73-b422-123034fd0218` | front 1 (main) |
| H2 | `4daf1276-2811-4e8e-8aea-9d3003c2718a` | front 2 |
| H3 | `41f5b68e-08e0-4801-8486-e564395d1b53` | front, head tilted, soft smile |
| H4 | `b89ff7c1-7b8b-43a9-bb17-3014e2bd273b` | three-quarter |
| H5 | `db1e4ae2-24ae-4e80-a0b2-afc5122c317d` | near profile |
| H6 | `8a72e9e6-8d08-478a-b1b0-c4344f25d235` | side view facing left |
| H7 | `f3d0d9f1-aad8-4e70-8d8e-12238d42abd9` | side view facing right |

**HERBUN** (chapter 6 only, make them first): head-and-shoulders crops of her from `C6_her-waiting-calla.jpg` (profile) and `C6_her-tea-glass.jpg` (front), low bun, white outfit. Upload as **H8** and **H9**. They are "same outfit" refs, so they are safe for Seg 57–61.

**HIM5** — lock order:
| Ref | ID | View |
|---|---|---|
| Z1 | job `9c080945-8f51-4994-95a7-5f055dad4441` | **slim** front (preferred) |
| Z2 | job `346a172a-3e4e-470a-9ea3-3cb9f8365843` | **slim** three-quarter |
| Z3 | job `1c86ba92-c4b3-48b5-8fa5-b39d08b01582` | **slim** front smile |
| Z4 | `558ca02d-4e66-4b31-96c8-e75c0837b833` | real profile facing right |
| Z5 | `74a8f324-e758-4241-9259-c926dfe4cdcc` | real profile facing left |
| (Z6) | `107953f7-ce5d-40f9-bb11-52ae3a904be9` | real 3/4 image-left (add only if 3/4 drifts) |
| (Z7) | `8609eba7-72f1-4b14-8e8f-bff3a031e109` | real 3/4 image-right (add only if 3/4 drifts) |

Never use his chin-up photo, the slim **profile** edit (`d5b03454…`, skin tone changed), any photo of him in a suit as an identity ref, or the old weak refs listed in `OUR_STORY_HANDOFF.md` §3.2.

**FRIEND** — **F1** (and F2 if the user sends two): the curly-haired friend.

**Locations (uploaded):**
| Name | ID |
|---|---|
| LOC-classroom | `89867713-1b70-4801-85c9-99daf1dc5902` |
| LOC-corridor | `d6918dfa-e718-40cd-92a9-a40b7574919e` |
| LOC-cafe | `68cd9113-fbf4-4209-96fb-b9ef624eb032` |
| LOC-library | `a0fb082b-17f8-498b-81ad-082cd7b06af0` |
| LOC-bridge | `a7f88443-1736-491e-ba06-eff428c4ad20` |
| LOC-airport | `e137404c-b47c-49ed-9648-29d78bca7386` |
| LOC-msu | `9ac4bc04-f9fd-4cbf-8d0c-8583bcbb872b` |
| LOC-thames (16:9) | `545612f8-abc8-4032-8dd8-0c56f872253c` |
| LOC-dusk (16:9) | `44c60663-a114-44f3-8431-0f33f2e323d7` |

**Cleaned real photos (years/watermarks removed) and their 16:9 versions:**
| Shot | Cleaned original | 16:9 (real photo in the centre) |
|---|---|---|
| 1.09 ceremony | `8becebc3-647c-450c-af89-b2886722a2a7` | — (crop to 16:9) |
| 1.10 families | `39ba888b-62e2-46f3-ba9c-25275ab9f080` | `4a513be5-5b8b-4232-a174-18cef9088a50` |
| 1.11 two of us | `9e302a6d-4832-45d2-8b0a-7cb19b49cb0e` | `95fe9d91-ce54-4e08-bb5d-224c4cf8436f` |
| 1.12 prom | `0c36a0ea-ee86-482c-afaa-b4911f6f03ea` | `3d8614ce-898c-4b54-9a01-f4abba1c42a1` |
| 2.09 mascot | `49ad0831-f612-481f-9665-3b55f620b75f` | `a568a748-fbd5-4793-b9ee-a2a692662109` |
| 2.10 Chicago | `d4c55fc4-70d9-418b-9e51-e0e83a769188` | `64006f1f-97f3-422a-9f91-d158f1c35942` |
| 3.03 arch | `c38e70ed-b0db-4cda-9f0c-02fb94c311c9` | `99e9ca6d-81df-402e-af3a-5a0fdc6eb2c7` |
| 3.05 Tower Bridge | `f90861da-6cac-4cbb-b441-1bbf6536c15a` | `e08a51f8-d596-40b9-8d3d-4434bbad83e2` |
| 3.07 NYE | `b43980eb-058f-4e7b-8e11-1008d6feeca4` | `cbd5fc8a-0783-45cb-ab22-1b2a805e4076` |
| 4.01b his graduation | `cd5e2fc2-5f97-46e7-b5e8-f9e9df3bdb17` | `2ae4ab0c-d926-43f5-adbd-84ba152a28fe` |
| 4.02 dome | `26692df3-b771-4d17-9ba0-4bb774ebc842` | — (crop) |
| 4.03 pipers | `4e6275b8-77f1-4ed2-bbcd-c491f2e1b8b1` | — (crop) |
| 6.01 sign | `e9abbd5b-09f4-4be6-b1b8-f2e4e945972b` | — (edit only) |
| 6.04 tea tray | `46964ded-e4ad-48a8-a1a5-b7927a19ee10` | `eb8f3642-0d9a-4f35-b8e8-f8b52e5626a4` |
| real serving-tea photo | `79246d22-79d5-4a25-9086-35ecffb8a389` | reference only (guests' faces: never animate) |

**Photos still only in the PDF (extract, clean, make 16:9, upload):** `C1_prom-dance` (remove watermark), `C2_edinburgh-old-college-her`, `C2_msu-sparty-him`, `C2_edinburgh-fountain-her`, `C2_edinburgh-castle`, `C2_msu-building` (same place as LOC-msu), `C2_edinburgh-meadows`, `C2_edinburgh-uni-building`, `C2_msu-international-center`, `C3_edinburgh-castle-families` (soften trailer lettering), `C3_london-street-lights` (soften shop names and plates), `C3_winter-wonderland` (soften stall signs), `C3_hotel-tree-couple`, `C3_new-year-dinner`, `C4_graduation-her-cap-raised`, `C4_graduation-her-family`, `C5_him-uniform`, `C5_visit-families` (blur car plates), `C6_her-waiting-calla`, `C6_table-set`, `C6_her-tea-glass`.
Widening portrait photos: masked inpaint of the sides only (`widen_prep.py` → `nano_banana_2_1` with `is_inpaint: true` → `composite.py … tone`). **Never** `outpaint_image` on people. For split-screen halves (958×1080) a portrait photo often needs no widening at all: generate in the photo's own aspect if the model allows it, otherwise widen.

---

## 3. Production order and approval gates

1. **Before anything paid:** check `balance`; ask the user the open questions in §17 (music source, lock resolution and budget, friend photo). Show the chapter 1 cost (§15) and get an OK.
2. **Chapter 1 = the test (Seg 01–16, takes T01–T15).** Make start frames → motion → lock → QA (§16) → assemble the 32 s with sound, the title and the dissolve out. Send the user the clip (SendUserFile) and one face sheet per scene. Ask with options: faces right? motion right? anything to change? **Proceed only on an explicit OK.** Fix what the user asks first.
3. **Chapters 2–6:** for each chapter: short plan + cost → OK → generate → QA → show the chapter cut → OK.
4. **Final assembly** (§12–13): all 61 segments, transitions, text, music and sound, colour match of the end to the real proposal footage, export.
5. Always generate **2 versions** of the key shots (T05, T06, T17, T32/T33, T39, T48, T57) and let QA pick.

### 3.1 How each route works (short; details in `OUR_STORY_HANDOFF.md` §7)
- **Route A (acted, from the face photos):** A1 `flux_3_image` start frame (2k, 16:9) from a real face photo + location photo → A2 `kling4_0` `mode: "image-to-video"`, `start_image` = A1 frame, **no face photos in `image_references`**, 1080p, 16:9 → A3 Genjutsu lock → A4 QA.
- **Route B (real photo → real moving scene):** B1 clean + 16:9 → B2 `kling4_0` image-to-video from the photo with real action (the photo pose is one beat, not the whole clip) → B3 lock the couple → B4 QA.
- **Route N (no identity):** Kling from the photo with real camera/scene motion. No lock.
- **Route E (made in the edit):** scripts, no AI.
- **"Ends on the real photo" takes** (the user often chose "they settle into the photo pose"): Kling starts from a frame, so use one of these and say which in the manifest:
  - **R (reverse):** start from the real photo and prompt the *opposite* action and the *opposite* camera move (e.g. "they relax out of the pose and drift a little apart; the camera cranes slowly up"). Play the result **reversed** in the edit. Good for gathering/settling with small motion. Check that nothing reads backwards (walking, steam, smoke, water, hair falling, people in the background walking). If it does, use E.
  - **E (end frame):** `start_image` = a FLUX start frame of the moment before (made from the face refs + the photo as place/outfit reference), `end_image` = the real photo (a *different* frame, so this is allowed). Good for walking-into-the-photo takes.
  - If neither works, start from the photo and play the action forward (pose first, then the action), and tell the user in one line.

---

## 4. Universal prompt blocks (paste these where a take says so)

**[STYLE]**
> Photorealistic, cinematic, shot on 35mm film, natural skin texture, soft warm light, shallow depth of field, subtle film grain, real-time natural human movement, motivated cinematic camera movement, no cuts inside the shot, no text, no letters, no numbers.

**[NEG]** (negative prompt, every generation)
> cartoon, anime, illustration, 3D render, CGI look, plastic skin, airbrushed face, beautified face, distorted face, face morphing, changing face, deformed hands, extra fingers, text, letters, numbers, subtitles, logos, watermark, low neckline, cleavage, kissing, hugging, holding hands, head on shoulder, frozen photo, still image, slideshow, zoom-in on faces

**[HER]** (description of her, for FLUX frames and Kling motion prompts)
> the young woman: fair skin, round face with full cheeks, thick dark defined eyebrows, dark-brown eyes with long lashes and soft winged liner, full lips with a glossy nude-pink colour, soft natural makeup with a warm glow, long straight glossy dark-brown hair with a centre part worn down past her shoulders, small gold hoop earrings

**[HIM]**
> the young man: tall and broad-shouldered, a slim face with a defined jawline, short dark-brown hair that is short on the sides with a receding hairline at the temples, straight dark eyebrows, brown eyes, slightly rounded nose, light stubble

**[KEEPFACE]** (end of every FLUX start-frame prompt)
> Keep every real face exactly as in its reference image: same features, same skin, same proportions. Do not retouch, beautify, slim, smooth or redraw the faces. Only the place, clothes, pose and framing change.

**[KEEPMOTION]** (end of every Kling motion prompt with people)
> Their faces, features and hair stay exactly as in the first frame throughout. Real-time natural movement.

### 4.1 Lock prompt templates (Genjutsu `hf_mult_replace_object`, `video_references` = the Kling job ID)
Refs go in **exactly this order** in `image_references`. Fill the [outfit] fields from the take.

**[LOCK-BOTH]** — refs: HER7, then HIM5 (12 refs)
> Replace the young woman in the [her outfit] with the woman from the first seven reference photos (front and side views of the same woman): her real face from every angle — round face, full cheeks, thick dark eyebrows, brown eyes, full lips, her real side profile — keeping her [hair: long, straight dark-brown hair worn down]. Replace the young man in the [his outfit] with the man from the last five reference photos: his real slim face with a defined jawline, light stubble, short dark hair with his real hairline, his real side profile. Both keep exactly the clothes they wear in the source video: she keeps the [her outfit], he keeps the [his outfit]. Keep their movements, expressions, eye direction, every shot, the camera, the background and all other people exactly as in the source video.

**[LOCK-HER]** — refs: HER7 (+ H8, H9 in chapter 6)
> Replace the young woman in the [her outfit] with the woman from the reference photos (front and side views of the same woman): her real face from every angle — round face, full cheeks, thick dark eyebrows, brown eyes, full lips, her real side profile — keeping her [hair]. She keeps exactly the clothes she wears in the source video: the [her outfit]. Keep her movements, expressions, eye direction, the camera, the background and all other people exactly as in the source video.

**[LOCK-HIM]** — refs: HIM5 (+ Z6/Z7 if 3/4 views drift)
> Replace the young man in the [his outfit] with the man from the reference photos: his real slim face with a defined jawline, light stubble, short dark hair with his real hairline, his real side profile. He keeps exactly the clothes he wears in the source video: the [his outfit]. Keep his movements, expressions, eye direction, the camera, the background and all other people exactly as in the source video.

**[LOCK-HER+FRIEND]** — refs: HER7, then F1(–F2)
> Replace the young woman in the [her outfit] with the woman from the first seven reference photos … (as LOCK-HER) … Replace the young woman with curly brown hair in the [friend outfit] with the woman from the last [1–2] reference photo(s): her real face and her naturally curly brown hair. Both keep exactly the clothes they wear in the source video. Keep their movements, expressions, eye direction, the camera, the background and all other people exactly as in the source video.

**[LOCK-THREE]** — refs: HER7, HIM5, F1(–F2): combine the three sentences in that order ("first seven …", "next five …", "last [1–2] …").

**Lock rules:** source 4–30 s (all takes here are 5–10 s). 1080p for close-ups and key shots, 720p + Topaz `upscale_video` for wides (column "Lock" in each take). If one person is not replaced, re-run with that person's refs listed first and their outfit named exactly. Retime each locked result back to its source length in the edit.

---

## 5. How to read a take sheet

Each take = one generation that covers one or more 2-second segments.
- **Route** A / B / N / E (§3.1); R or E method for "ends on the real photo" takes.
- **Gen:** length and resolution to generate with `kling4_0` (always 16:9, no end frame unless the sheet says so).
- **A1 refs / A1 prompt:** `flux_3_image`, 2k, 16:9; images in the listed order; the prompt says which image is whom.
- **Motion prompt:** paste into `kling4_0` `image-to-video` with `start_image` = the A1 frame (Route A) or the prepared real photo (Route B/N). Expand the [BLOCKS] from §4. Negative prompt = [NEG].
- **Lock:** which template from §4.1, which outfits to fill in, and the resolution.
- **Use:** which seconds of the (retimed) take go into the film. Times are approximate; pick the best 2 s that contain the named beat.
- **Edit / Sound / QA:** what to do in the cut, what we hear, what to check.

Times in the headers are on the 2-second grid. If T04 runs 2 s longer (allowed), every later time shifts by +2 s.

---

## 6. Take sheets — Chapter 1: University (Seg 01–16, 0:00–0:32)

Chapter outfits: **her** pink crew-neck sweater, blue jeans, cream canvas backpack, hair down (Seg 01–07); **him** navy crew-neck sweater, dark jeans, light stubble (Seg 04–07); **friend** naturally curly brown hair, modest olive-green knit sweater and jeans (default; change it if the user's photo suggests another look).

### T01 · Seg 01 · 0:00–0:02 · 1.01 Class ends — the wide
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER, 720p + Topaz | ≈1.0–3.0 s (students up, dolly moving) |

**A1 refs:** H4, LOC-classroom
**A1 prompt:**
> The first image shows the young woman's face; the second image shows the place. A wide shot from the back rows of the university lecture hall in the second image: curved light-wood desks, grey mesh chairs, warm beige walls, soft daylight from the windows. In the middle rows sits [HER], wearing a pink crew-neck sweater and blue jeans, a cream canvas backpack on the desk beside her; she is writing in a notebook, eyes down, her face in three-quarter view toward the camera. Around her the class has just ended: several students are standing up, putting notebooks into bags and chatting; two students walk toward the door on the right. Everyday, lively but relaxed. [KEEPFACE]

**Motion prompt:**
> A wide shot of a bright university lecture hall just as the class ends, soft daylight. 0–1.5 s: all around the hall students stand up from their seats, close their notebooks, gather their things and talk casually; a few walk toward the door. 1.5–3.5 s: the camera dollies slowly and smoothly forward from the back rows down the aisle toward the young woman in the pink crew-neck sweater, who is still seated, writing in her notebook, eyes down. 3.5–5 s: the camera keeps gliding closer; students cross between her and the camera; she keeps writing, calm and relaxed. [KEEPMOTION] [STYLE]

**Lock fill:** her outfit "pink crew-neck sweater and blue jeans"; hair "long, straight dark-brown hair worn down".
**Edit:** the film opens with a 0.5 s fade from black. Title **"Where it all began"** (§12.5) from 0:00.8 to 0:03.4, crossing the cut into Seg 02. Then a hard cut.
**Sound:** music starts from silence; classroom ambience — chairs scraping, bags zipping, soft chatter.
**QA:** her face clear in three-quarter view, eyes down; real dolly parallax (desks pass the lens).

### T02 · Seg 02 · 0:02–0:04 · 1.01 — medium close-up, notebook
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER, 1080p | ≈0.6–2.6 s (notebook closes and goes into the bag) |

**A1 refs:** H4, LOC-classroom
**A1 prompt:**
> The first image shows the young woman's face; the second image shows the place. Medium close-up at desk height in the lecture hall from the second image, background softly blurred with students standing up. [HER] in a pink crew-neck sweater sits at her desk writing the last line in an open notebook with a pen, eyes down, face in three-quarter view; an open cream canvas backpack sits on the desk. Soft daylight from the side. [KEEPFACE]

**Motion prompt:**
> Medium close-up. 0–1.5 s: she writes the last word, puts the pen down and gently closes the notebook. 1.5–3.5 s: she picks the notebook up with both hands and slides it into the open cream canvas backpack. 3.5–5 s: she drops her pen and phone into the bag while turning her head slightly to the side as if listening to a friend standing next to her, with a relaxed small smile. Natural, unhurried movements; cheerful and unaware of what the day will bring. Camera: slight handheld drift at desk height, shallow depth of field, students moving in the soft background. [KEEPMOTION] [STYLE]

**Lock fill:** as T01.
**Sound:** notebook closing, pen on the desk, chatter.

### T03 · Seg 03 · 0:04–0:06 · 1.01 — the friend's joke, her laugh
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER+FRIEND, 1080p | ≈1.2–3.2 s (the laugh) |

**A1 refs:** H4, F1, LOC-classroom
**A1 prompt:**
> The first image shows the young woman's face, the second image shows her friend's face, the third image shows the place. Medium two-shot from across the desk in the lecture hall from the third image. [HER] sits at her desk in a pink crew-neck sweater, packing her cream canvas backpack. Standing beside her desk, leaning in casually, is her friend — the young woman from the second image, with naturally curly brown hair, in a modest olive-green knit sweater and jeans. Students in the soft background. [KEEPFACE]

**Motion prompt:**
> Medium two-shot. 0–1.5 s: the curly-haired friend standing beside the desk says something funny with a playful little hand gesture. 1.5–3.5 s: the seated young woman turns her head toward her friend, makes eye contact and breaks into a genuine, spontaneous laugh — her eyes narrow as she smiles and her shoulders move slightly with the laughter. 3.5–5 s: both keep laughing softly; the friend grins. An authentic everyday moment between two friends, not staged. Camera: slow gentle arc from the front of the desk, shallow depth of field. [KEEPMOTION] [STYLE]

**Lock fill:** her "pink crew-neck sweater and blue jeans"; friend "olive-green knit sweater and jeans".
**If the friend's photo has not arrived:** generate anyway, keep the friend side-on and softer in focus, lock only her (LOCK-HER), and re-lock with LOCK-HER+FRIEND when the photo comes.
**Sound:** her real laugh audible under the music.

### T04 · Seg 04–05 · 0:06–0:10 (may stretch to 0:12) · 1.01 → 1.02 — wave, follow through the doorway, he looks up
One continuous take, **no cut** (user's instruction).
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 7 s, 1080p | LOCK-THREE, 1080p | from the wave to the moment he looks up, ≈0.0–6.0 s (4–6 s on the grid) |

**A1 refs:** H1, F1, LOC-classroom
**A1 prompt:**
> The first image shows the young woman's face, the second image shows her friend's face, the third image shows the place. Medium shot in the lecture hall from the third image, the open classroom door visible a few steps behind her. [HER], in a pink crew-neck sweater and blue jeans, has just stood up beside her desk and is lifting her cream canvas backpack onto her right shoulder; her curly-haired friend (olive-green knit sweater) stands on the other side of the desk smiling at her. Students move toward the door in the background. The camera is slightly behind and to the side of her. [KEEPFACE]

**A1b (end frame, only if needed) refs:** H6, Z1, LOC-corridor
> The first image shows the back and side of the young woman's head, the second image shows the young man's face, the third image shows the place. Over-the-shoulder shot from just behind the young woman's right shoulder (pink crew-neck sweater, long dark-brown hair down, cream backpack) in the bright corridor from the third image: warm beige wall panels, glass classroom walls, pale stone floor, long linear ceiling lights, a low green bench, students passing softly blurred. In focus a few metres ahead, [HIM], in a navy crew-neck sweater and dark jeans, walks toward her with his phone in his hand and has just looked up from it. [KEEPFACE]

**Motion prompt:**
> One continuous shot, no cuts. 0–1 s: the young woman settles the cream backpack on her right shoulder, looks at her curly-haired friend with a warm smile and gives a small casual wave goodbye; the friend smiles and waves back. 1–2.5 s: she turns and walks to the classroom door past other students; the camera follows her smoothly from a slightly diagonal rear angle at shoulder height. 2.5–4 s: without any cut the camera follows her through the doorway into a bright corridor with warm beige wall panels, glass classroom walls, a pale stone floor and long linear ceiling lights; the light shifts gradually from the warm classroom to the brighter corridor. 4–5.5 s: the camera stays just behind her right shoulder; ahead of her a tall young man in a navy crew-neck sweater and dark jeans walks toward her along the corridor, looking down at his phone. 5.5–7 s: he looks up from his phone and sees her; the focus pulls gently from her hair to his face; he slows down. Natural walking pace. Smooth, understated camera movement like a professionally filmed romantic movie; no morphing, no sudden change of perspective, no exaggerated camera moves. [KEEPMOTION] [STYLE]

**If** the corridor does not look like the real one, or he does not appear: regenerate with `end_image` = the A1b frame.
**Lock fill:** her "pink crew-neck sweater and blue jeans"; him "navy crew-neck sweater and dark jeans"; friend "olive-green knit sweater and jeans".
**Edit:** the whole piece plays uncut. If it needs 6 s, the film becomes 2:04 (approved). **Never speed it up.**
**Sound:** classroom chatter fades as she passes the door; corridor footsteps and a lighter, airier room tone.
**QA:** no morphing at the doorway; his face appears only at the end, in focus, in the pull.

### T05 · Seg 06 · 0:10–0:12 · 1.02 — reverse on her: their eyes meet, a small smile (KEY SHOT, make 2 versions)
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER, 1080p | ≈1.8–3.8 s (eyes lift → smile) |

**A1 refs:** H4, LOC-corridor
**A1 prompt:**
> The first image shows the young woman's face; the second image shows the place. Medium close-up in the bright corridor from the second image (warm beige panels, glass classroom walls, long linear ceiling lights, students softly blurred behind). [HER] in a pink crew-neck sweater, the cream backpack on her right shoulder, walks slowly toward the camera, face in three-quarter view, eyes slightly lowered. Soft window light on her face. [KEEPFACE]

**Motion prompt:**
> Medium close-up, slight slow motion. 0–1.5 s: she walks slowly forward, eyes slightly down; the camera moves backward in front of her at her pace. 1.5–3 s: she senses someone looking at her, lifts her eyes and looks just to the right of the camera lens, at the young man off-screen. 3–5 s: their eyes meet; a small, soft smile appears and her eyes stay on him — she does not look down and does not touch her hair. Shallow depth of field, soft window light. [KEEPMOTION] [STYLE]

**Lock fill:** as T01.
**Sound:** corridor chatter softens and drops away; the music rises.
**QA (user's rules):** eyes stay up; **no** hair-behind-ear; smile small and natural.

### T06 · Seg 07 · 0:12–0:14 · 1.04 merged — they pass, a shared smile (KEY SHOT, make 2 versions)
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-BOTH, 1080p | ≈1.2–3.2 s, ending on the shared smile as they cross |

**A1 refs:** H5, Z5, LOC-corridor
**A1 prompt:**
> The first image shows the young woman's face in profile, the second image shows the young man's face in profile, the third image shows the place. Medium side view across the bright corridor from the third image (warm beige panels, glass classroom walls, linear ceiling lights). On the left, [HER], seen in profile facing right, walks to the right: pink crew-neck sweater, blue jeans, cream backpack on her shoulder, long dark-brown hair down. On the right, [HIM], seen in profile facing left, walks to the left: navy crew-neck sweater, dark jeans, phone lowered in his hand. They are two steps apart, about to pass each other, looking at each other with the beginning of a smile. Students blurred in the foreground and background. [KEEPFACE]

**Motion prompt:**
> Slow motion, medium side view. 0–2 s: they walk toward each other along the corridor, eyes on each other, students passing blurred in the foreground. 2–3.5 s: they pass each other at arm's length without stopping, both with a shared, slightly shy smile; his smile is a little embarrassed. 3.5–5 s: they keep walking apart, the smile still on their faces. Neither stops, looks back, nods or makes any gesture; for a brief moment their attention is entirely on each other. They do not touch. Camera: slow lateral tracking shot at chest height. [KEEPMOTION] [STYLE]

**Lock fill:** her "pink crew-neck sweater and blue jeans"; him "navy crew-neck sweater and dark jeans".
**Edit:** **MATCH CUT** on the smile straight into Seg 08 (she is laughing in the café). The music carries on through the cut.
**QA:** no look-back, no nod, no stop; both profiles must be the real profiles (check against H5/H6/H7 and Z4/Z5).

### T07 · Seg 08 · 0:14–0:16 · 1.05 The café
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-BOTH, 1080p | ≈0.9–2.9 s (start ON her laugh for the match cut) |

**A1 refs:** H3, Z2, LOC-cafe
**A1 prompt:**
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place. Medium shot in the bright atrium café from the third image: round white tables, red chairs, floor-to-ceiling windows onto a green lawn. [HER], in a cream knit sweater with a high neck and her hair down, and [HIM], in a dark jacket over a plain dark tee, sit across from each other at a table by the window, two coffee cups and a small pastry between them; both faces visible in three-quarter view, smiling. Natural daylight. [KEEPFACE]

**Motion prompt:**
> Medium shot. 0–1 s: he leans in a little and says something funny with a small hand gesture. 1–3 s: she bursts into a natural laugh, eyes narrowing, her hand near her coffee cup. 3–5 s: they keep talking easily, both smiling. Camera: slow arc around the window table from her side toward his side. Natural daylight, a few students far behind. [KEEPMOTION] [STYLE]

**Lock fill:** her "cream high-neck knit sweater"; him "dark jacket over a dark tee".
**Sound:** café murmur, a cup set on a saucer.

### T08 · Seg 09 · 0:16–0:18 · 1.06 The library
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-BOTH, 1080p | ≈1.8–3.8 s (he nods → she turns to him) |

**A1 refs:** H4, Z1, LOC-library
**A1 prompt:**
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place. Front view of the front study table in the library from the third image — keep the room exactly as it is (light-wood tables and shelves, square ceiling lights, tall windows with white blinds). [HER], in a soft beige turtleneck sweater with her hair down, and [HIM], in a grey crew-neck sweater, sit side by side with open laptops and notebooks; she points with a pen at her notebook, he leans slightly toward her. Warm lamp light. [KEEPFACE]

**Motion prompt:**
> Medium shot from the front of the table. 0–2 s: she points at a line in her notebook with her pen and explains it to him quietly, with small hand movements. 2–3.5 s: he leans closer to look, then nods and smiles. 3.5–5 s: she turns from her notes to look at him, and they share a quiet smile. Camera: slow push-in. Warm lamp light, a few students in the background. [KEEPMOTION] [STYLE]

**Lock fill:** her "beige turtleneck sweater"; him "grey crew-neck sweater".
**Sound:** quiet library room tone, a page turning.

### T09 · Seg 10 · 0:18–0:20 · 1.07 The park, red bridge, coffees
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | ≈1.6–3.6 s (she turns and laughs, camera starts rising) |

**A1 refs:** H5, Z5, LOC-bridge
**A1 prompt:**
> The first image shows the young woman's face in profile, the second image shows the young man's face in profile, the third image shows the place. From behind and slightly to the left, in soft golden winter sunlight: [HER] and [HIM] walk side by side across the red footbridge in the university park from the third image (tall pine trees, a calm green pond). She is on the left, he is on the right; each holds a takeaway coffee cup; she turns her face toward him (her profile visible) and he smiles at her (his profile visible). She wears an elegant short burgundy winter dress with long sleeves and a high closed neckline, a long tailored coat worn open so the dress shows, and knee-high boots; her long dark-brown hair is down. He wears a stylish casual winter jacket over a coordinated sweater and trousers that complement her outfit without looking matched. [KEEPFACE]

**Motion prompt:**
> 0–2 s: they walk side by side across the red footbridge away from the camera, each holding a takeaway coffee, talking; her hair moves gently as she walks. 2–3.5 s: she turns her face toward him and laughs; he smiles at her. 3.5–5 s: the camera, which has been following behind them, rises gently above the bridge and reveals the green pond and the pines in warm winter sunlight. A sunny winter day; romantic, sophisticated and effortlessly natural, like a scene from a real romantic film. [KEEPMOTION] [STYLE]

**Lock fill:** her "short burgundy long-sleeve winter dress, long open tailored coat, knee-high boots"; him "casual winter jacket, sweater and trousers".
**Sound:** footsteps on the wooden bridge, birds, soft wind in the pines.
**QA:** the dress neckline stays high and closed.

### T10 · Seg 11 · 0:20–0:22 · 1.08 Time passes
| Route | Gen | Lock | Use |
|---|---|---|---|
| N | 5 s, 1080p, start = LOC-dusk | — | ≈1.5–3.5 s |

**Motion prompt:**
> Animate this photo as real footage: a university campus at dusk. The library windows switch on one by one and glow warm yellow, clouds move quickly across the lavender sky in a time-lapse, a few small students walk up the steps far away, leaves drift down from the tree. The camera cranes slowly upward. [STYLE]

**Sound:** music only.

### T11 · Seg 12 · 0:22–0:24 · 1.09 Graduation day
| Route | Gen | Lock | Use |
|---|---|---|---|
| N | 5 s, 1080p, start = `8becebc3…` cropped to 16:9 | — | ≈1.0–3.0 s |

**Motion prompt:**
> Animate this photo as real footage: an outdoor university graduation ceremony at dusk. The student choir on stage sings, mouths and bodies moving with the song; graduates in caps and gowns watch and sway gently; a woman at the front holds up her phone to film. The camera pushes slowly forward through the crowd toward the stage. No readable text on the stage or banners. [STYLE]

**Sound:** soft choir voices blended into the music.
**QA:** no year on any banner.

### T12 · Seg 13 · 0:24–0:26 · 1.10 With our families (method R)
| Route | Gen | Lock | Use |
|---|---|---|---|
| B + R | 5 s, 1080p, start = `4a513be5…` (upscale it first with `upscale_image`; the source is only 572×763) | LOCK-BOTH, 720p + Topaz | the **last 2 s of the reversed clip** (it must end exactly on the real photo) |

**Motion prompt (generated forward, played reversed):**
> Start exactly from this photo: five people on a cobbled courtyard outside a modern university building on a summer evening — the young woman in a black graduation gown over a white dress holding red roses and her diploma, the young man in a graduation gown holding his diploma folder, and between them two women and a young woman in white. 0–2 s: they relax out of the photo pose, their smiles soften and they start to chat. 2–5 s: the family members drift half a step outward from the couple and turn to talk to each other; the young woman lowers her roses slightly. The camera arcs slowly to the left. Everyone in sharp focus (deep focus), gentle natural movement, medium-wide framing, no one walks. [KEEPMOTION] [STYLE]

Played reversed, this reads as: the family gathers and settles into the photo pose while the camera arcs to the right.
**Lock fill:** her "black graduation gown over a white dress"; him "black graduation gown". Lock **before** reversing.
**QA:** nothing reads backwards (hair, fabric, background people); family faces stay true at the end (the last frame is the real photo).
**Sound:** soft evening voices, a little laughter.

### T13 · Seg 14 · 0:26–0:28 · 1.11 The two of us
| Route | Gen | Lock | Use |
|---|---|---|---|
| B | 5 s, 1080p, start = `95fe9d91…` | LOCK-BOTH, 1080p | ≈0.6–2.6 s (turn, laugh, first steps) |

**Motion prompt:**
> Start exactly from this photo: the young woman in a white dress and the young man in a white shirt stand together under a wooden canopy, sunlight flickering through the slats. 0–1.5 s: they turn to each other and laugh. 1.5–3.5 s: they walk forward out from under the canopy toward the camera, side by side, not touching. 3.5–5 s: he says something and she laughs, looking at him; the sunlight flickers across them. The camera dollies backward in front of them at their pace. [KEEPMOTION] [STYLE]

**Lock fill:** her "white dress"; him "white shirt".
**Sound:** footsteps, light courtyard ambience.

### T14 · Seg 15 · 0:28–0:30 · 1.12 The prom, Zağulba Palace
| Route | Gen | Lock | Use |
|---|---|---|---|
| B | 5 s, 1080p, start = `3d8614ce…` (portrait photo, "PROM" and watermark removed) | LOCK-BOTH, 1080p | ≈1.0–3.0 s |

**Motion prompt:**
> Start exactly from this photo: a couple at an elegant evening party on a red carpet in front of a glowing white neon sign (the sign shows no readable letters). 0–1.5 s: camera flashes go off from photographers in front of them, lighting their faces. 1.5–3.5 s: she smiles and leans slightly toward him — only as close as in the photo, no added touch — and he relaxes into a smile. 3.5–5 s: more flashes; they hold their smiles. The camera pushes in slowly. [KEEPMOTION] [STYLE]

**Lock fill:** her and his outfits exactly as in the photo (name them after extraction, e.g. "her evening gown", "his dark suit").
**Sound:** camera shutter clicks and soft flash pops under the music.
**QA:** touch exactly as in the real photo; no letters on the neon sign.

### T15 · Seg 16 · 0:30–0:32 · 1.13 The dance (last shot of chapter 1)
| Route | Gen | Lock | Use |
|---|---|---|---|
| B | 5 s, 1080p, start = `C1_prom-dance` (remove the watermark, widen to 16:9) | LOCK-BOTH, 1080p | ≈1.0–3.0 s, the last 0.6 s glowing for the dissolve |

**Motion prompt:**
> Start exactly from this photo: an evening party in a palace ballroom with warm golden string lights. The young woman in a champagne off-shoulder gown dances and laughs, moving naturally to the music; the young man in a dark suit turns toward her and smiles; other guests dance around them, softly blurred. Slow motion. The camera drifts gently to the side and slightly upward, and in the last second rises into the warm golden string lights, which glow and flare softly. [KEEPMOTION] [STYLE]

**Lock fill:** her "champagne off-shoulder gown" (kept exactly as in her real photo — user approved); him "dark suit".
**Edit:** chapter end: **0.6 s soft dissolve through the glowing string lights** into Seg 17.
**Sound:** party ambience under the music, which swells into the dissolve.

---

## 7. Take sheets — Chapter 2: Studying abroad (Seg 17–32, 0:32–1:04)

Travel outfits (Seg 17–20): **her** comfortable grey sweater (high crew neck) with matching grey sweatpants, hair down; **him** blue sweater with matching blue sweatpants. Suitcases: hers beige hard-shell, his dark grey (default).
Split screens: **her left, him right**, each half 958×1080, 4 px white divider, matched light, both halves cut at the same moment (§12.1).

### T16 · Seg 17 · 0:32–0:34 · 2.01 Leaving together
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | ≈1.0–3.0 s |

**A1 refs:** H1, Z1, LOC-airport
**A1 prompt:**
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place. Medium-wide shot in the bright modern airport terminal from the third image (white lattice ceiling, glass balconies, polished pale floor). [HER] and [HIM] walk side by side toward the camera, each pulling a suitcase (hers beige hard-shell, his dark grey). She wears a comfortable grey sweater with matching grey sweatpants, hair down; he wears a blue sweater with matching blue sweatpants — casual, comfortable and stylish travel outfits. Faces in three-quarter view, talking. Travellers in the background. [KEEPFACE]

**Motion prompt:**
> Medium-wide shot. 0–5 s: they walk side by side toward the camera through the bright terminal, each pulling a suitcase, talking quietly; at about 2 s she glances at him and he answers with a small smile; travellers pass behind them. The camera moves backward in front of them at walking pace. A relaxed couple travelling together, a little quiet. [KEEPMOTION] [STYLE]

**Lock fill:** her "grey sweater and matching grey sweatpants"; him "blue sweater and matching blue sweatpants".
**Edit:** enters through the 0.6 s chapter dissolve from Seg 16.
**Sound:** terminal ambience, suitcase wheels on the polished floor.

### T17 · Seg 18–19 · 0:34–0:38 · 2.02 Two directions (KEY SHOT, make 2 versions)
One continuous symmetrical take.
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | ≈0.2–4.2 s, uncut |

**A1 refs:** H1, Z1, LOC-airport (if LOC-airport is not the twin-escalator view, extract `C2_airport-terminal` from the PDF — the PDF asks for "this exact view")
**A1 prompt:**
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place. A perfectly symmetrical, centred wide shot of the airport terminal hall from the third image: two escalators rise on either side of a tall green tree in the centre. At the bottom, between the two escalators and in front of the tree, [HER] (grey sweater set) and [HIM] (blue sweater set) stand facing each other, each with a suitcase. They are small in the frame. [KEEPFACE]

**Motion prompt:**
> A perfectly symmetrical centred wide shot; the camera very slowly pushes in the whole time; no cuts. 0–1 s: at the bottom between the two escalators they look at each other for a moment. 1–2 s: she turns and steps onto the LEFT escalator with her suitcase; he steps onto the RIGHT escalator with his. 2–3 s: both rise slowly on either side of the tall green tree, facing forward, a little sad. 3–4.5 s: a few metres up, both turn back and give a small wave to each other across the tree — sad, with a small brave smile. 4.5–5 s: they keep rising. [KEEPMOTION] [STYLE]

**Lock fill:** as T16.
**Edit:** keep this exact framing; T48 must copy it for the homecoming (save the A1 frame as "ESC-FRAME").
**Sound:** soft echoing hall, suitcase wheels, the escalator hum; music.
**QA:** symmetry holds; signs soft and unreadable.

### T18 + T19 · Seg 20 · 0:38–0:40 · 2.03 Window seats (split screen)
| Take | Route | Gen | Lock | Use |
|---|---|---|---|---|
| T18 her (left half) | A | 5 s, 1080p | LOCK-HER, 1080p | ≈2.0–4.0 s |
| T19 him (right half) | A | 5 s, 1080p | LOCK-HIM, 1080p | ≈2.0–4.0 s |

**T18 A1 refs:** H5
> The image shows the young woman's face. Inside a passenger plane in soft daylight. [HER] sits in a window seat; the oval window is on the RIGHT side of the frame and she faces right toward it, her face in three-quarter profile, lit by the daylight from the window. She wears her grey high-neck sweater, hair down. Clouds outside the window. [KEEPFACE]

**T18 motion prompt:**
> Close-medium shot. 0–2 s: she looks out of the oval window at the clouds below, thoughtful and a little sad. 2–3.5 s: she lowers her eyes for a moment. 3.5–5 s: she looks back out of the window, missing him. Soft daylight on her face; clouds drift past outside. The camera pushes in slowly. [KEEPMOTION] [STYLE]

**T19 A1 refs:** Z5, Z2
> The first image shows the young man's face in profile, the second image in three-quarter view. Inside a passenger plane in soft daylight. [HIM] sits in a window seat; the oval window is on the LEFT side of the frame and he faces left toward it, his face in three-quarter profile, lit by the daylight from the window. He wears his blue sweater. Clouds outside. [KEEPFACE]

**T19 motion prompt:**
> Close-medium shot. 0–2 s: he looks out of the oval window at the clouds below, thinking of her. 2–3.5 s: he rests his head back against the seat. 3.5–5 s: he keeps looking out, a little sad. Soft daylight on his face; clouds drift past outside. The camera pushes in slowly. [KEEPMOTION] [STYLE]

**Edit:** split screen, her left facing right, him right facing left, so they seem to look toward each other across the divider. Match brightness and colour. Text: **"Edinburgh"** on her half, **"Michigan"** on his half (§12.5).
**Sound:** soft cabin hum under the music.

### T20 · Seg 21 · 0:40–0:42 · 2.04 Two skies
| Route | Gen | Lock | Use |
|---|---|---|---|
| N | 5 s, 1080p, `text-to-video` | — | ≈1.5–3.5 s |

**Motion prompt:**
> Wide aerial view high above a sea of clouds at golden hour. Two passenger jets flying side by side slowly bank away from each other; their white contrails split into a wide V across the golden sky. Calm and cinematic, slow camera drift. No text, no airline logos or lettering. [STYLE]

**Sound:** soft high-altitude wind under the music.

### T21 + T22 · Seg 22 · 0:42–0:44 · 2.05 Arriving (split screen)
| Take | Route | Gen | Lock | Use |
|---|---|---|---|---|
| T21 her (left) | B, start = `C2_edinburgh-old-college-her` | 5 s, 1080p | LOCK-HER, 1080p | ≈2.0–4.0 s |
| T22 him (right) | B, start = `C2_msu-sparty-him` | 5 s, 1080p | LOCK-HIM, 1080p | ≈2.0–4.0 s |

**T21 motion prompt:**
> Start exactly from this photo: the young woman in a green hoodie and jeans stands on the lawn of a grand old stone university courtyard under a bright sky. 0–2 s: a breeze lifts her long hair; she looks up and around at the buildings. 2–3.5 s: she turns back toward the camera. 3.5–5 s: she breaks into a happy smile. Clouds drift. The camera slowly orbits a little around her. [KEEPMOTION] [STYLE]

**T22 motion prompt:**
> Start exactly from this photo: the young man in a green T-shirt and jeans stands in front of a large bronze statue on a red-brick plinth, campus lawn and trees behind. 0–1.5 s: he takes his hands out of his pockets. 1.5–3.5 s: he looks around the campus. 3.5–5 s: he smiles. The trees move in the breeze and clouds drift; the bronze statue stays completely still and unchanged. The camera slowly orbits a little around him. [KEEPMOTION] [STYLE]

**Lock fill:** her "green hoodie and jeans"; him "green T-shirt and jeans".
**Sound:** her side wind and distant city; his side birds and campus voices.
**QA:** the statue does not move or melt.

### T23 · Seg 23 · 0:44–0:46 · 2.06 A photo for him (Route A, because the camera is behind her)
| Route | Gen | Lock | Use |
|---|---|---|---|
| A (place + outfit from `C2_edinburgh-fountain-her`) | 5 s, 1080p | LOCK-HER, 1080p | ≈1.5–3.5 s (stops, lifts the phone, castle on the screen) |

**A1 refs:** H6, H5, `C2_edinburgh-fountain-her`
> The first two images show the young woman's head from the side; the third image shows the place and her outfit. From just behind her right shoulder in the garden from the third image (an ornate blue-and-gold fountain, the castle on its rock behind): [HER] walks along the path toward the fountain, seen from behind and slightly to the side, her profile just visible. She wears the beige knit top and plaid skirt exactly as in the third image, long dark-brown hair down. [KEEPFACE]

**Motion prompt:**
> 0–2 s: she walks up the garden path toward the ornate blue-and-gold fountain, the castle on its rock beyond; the camera follows just behind her right shoulder. 2–3.5 s: she stops, lifts her phone and frames the castle — the castle appears on her phone screen (no app interface, no text) and in real life behind it. 3.5–5 s: she takes the photo and lowers the phone with a smile, her profile visible. The fountain's water flows, clouds drift. [KEEPMOTION] [STYLE]

**Lock fill:** her "beige knit top and plaid skirt".
**Edit:** montage pace from here to Seg 28: quick 2 s cuts. The tail of this take (she lowers the phone, ≈3.5–5.0 s) is also the **left half of Seg 24**.
**Sound:** fountain water, a soft phone-camera click.

### Seg 24 · 0:46–0:48 · 2.07 Photos fly between the halves — made in the edit
See §12.2. Left half = T23 tail; right half = T24 head (he looks at his phone). Two soft "pings".

### T24 · Seg 25 · 0:48–0:50 · 2.08 His reply
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HIM, 1080p | ≈1.0–3.0 s (smile → raises the phone); ≈0.0–2.0 s also feeds Seg 24's right half |

**A1 refs:** Z2, LOC-msu
> The first image shows the young man's face; the second image shows the place. Medium shot on the sunny campus from the second image: the curved red-brick building with tall glass windows, big oak trees, a green lawn, dappled sunlight. [HIM], in a green T-shirt and jeans, has just stopped on the path and looks down at his phone, face in three-quarter view. [KEEPFACE]

**Motion prompt:**
> Medium shot. 0–1.5 s: he looks at the photo on his phone and smiles. 1.5–3 s: he raises the phone and frames the building. 3–5 s: he takes a photo of the curved red-brick building; the camera arcs slowly from his face round toward the building. Dappled sunlight through the oaks. [KEEPMOTION] [STYLE]

**Lock fill:** him "green T-shirt and jeans".
**Sound:** birds, leaves, a phone-camera click.

### T25 · Seg 26 · 0:50–0:52 · 2.09 Michigan life
| Route | Gen | Lock | Use |
|---|---|---|---|
| B | 5 s, 1080p, start = `a568a748…` | LOCK-HIM, 1080p | ≈1.0–3.0 s (pose → laugh) |

**Motion prompt:**
> Start exactly from this photo: a sunny street festival in a city centre, red-brick buildings and inflatable games behind; the young man in a white T-shirt and grey jeans stands next to a costumed Spartan mascot. 0–2 s: they hold their pose for a friend's phone off-camera, both flexing an arm, smiling. 2–3.5 s: he breaks into a big laugh and drops his arm. 3.5–5 s: the mascot gives a thumbs-up; he laughs again and turns toward the street. People stroll in the background. Light handheld camera, like a friend filming at the fair. Shop signs and street signs stay soft and unreadable. [KEEPMOTION] [STYLE]

**Lock fill:** him "white T-shirt and grey jeans".
**Sound:** festival crowd, distant music from the fair.

### T26 · Seg 27 · 0:52–0:54 · 2.10 Chicago
| Route | Gen | Lock | Use |
|---|---|---|---|
| B | 5 s, 1080p, start = `64006f1f…` | LOCK-HIM, 1080p | ≈1.5–3.5 s (walking along the river) |

**Motion prompt:**
> Start exactly from this photo: night in Chicago; the young man in a cream fleece jacket stands at a stone balustrade above the river. 0–1.5 s: he smiles, takes his hands out of his pockets and starts to walk along the riverside path. 1.5–5 s: he walks slowly along the balustrade, looking at the city lights; skyscraper lights reflect and shimmer in the water and a tour boat glides past. The camera orbits slowly from him round toward the skyline. No lettering on any building. [KEEPMOTION] [STYLE]

**Lock fill:** him "cream fleece jacket".
**Edit:** small **"Chicago"** (§12.5).
**Sound:** water lapping, the distant city, a boat engine.
**QA:** face holds up in low light; no tower lettering.

### T27 · Seg 28 · 0:54–0:56 · 2.11 "Wow"
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER, 1080p | ≈1.8–3.8 s (eyes widen → delighted smile) |

**A1 refs:** H3, `C2_edinburgh-meadows`
> The first image shows the young woman's face; the second image shows the place. Medium shot in the sunny park from the second image (a wide lawn, big trees, students relaxing far behind). [HER] sits on the grass in a light high-neck knit top and jeans, hair down, looking down at her phone, face in three-quarter view. [KEEPFACE]

**Motion prompt:**
> Medium shot. 0–2 s: she sits on the grass looking at her phone. 2–3 s: her eyes widen. 3–5 s: she breaks into a delighted smile, still looking at the phone. She does not put her hand over her mouth. The camera pushes in slowly toward her face. Soft sunlight. [KEEPMOTION] [STYLE]

**Lock fill:** her "light high-neck knit top and jeans".
**QA (user's rule):** no hand over the mouth.

### T28 + T29 · Seg 29 · 0:56–0:58 · 2.12 Studying (split screen)
| Take | Route | Gen | Lock | Use |
|---|---|---|---|---|
| T28 her (left) | A | 5 s, 1080p | LOCK-HER, 1080p | ≈1.5–3.5 s |
| T29 him (right) | A | 5 s, 1080p | LOCK-HIM, 1080p | ≈1.5–3.5 s |

**T28 A1 refs:** H4, `C2_edinburgh-uni-building` (style of the building)
> The first image shows the young woman's face; the second image shows the style of the building. Inside an old stone University of Edinburgh building in the style of the second image: a quiet study room with tall white sash windows and autumn trees outside. [HER] sits at a wooden desk, books and notebooks open around her, writing notes quickly with a pen, focused, face in three-quarter view. She wears a cosy high-neck knit sweater, hair down. Soft afternoon light. [KEEPFACE]

**T28 motion prompt:**
> 0–5 s: she writes notes fast in her notebook, focused; at about 2 s she glances at an open textbook beside her, then keeps writing quickly and turns a page. The camera pushes in slowly. Soft afternoon light, autumn trees moving outside the window. [KEEPMOTION] [STYLE]

**T29 A1 refs:** Z2, `C2_msu-international-center`
> The first image shows the young man's face; the second image shows the place. The bright university hall from the second image: tall windows looking onto red-brick buildings and trees, a staircase and a metal globe sculpture. [HIM], in a hoodie, sits at a table by the windows, a laptop and lots of open books in front of him, writing notes quickly, focused, face in three-quarter view. Soft daylight. [KEEPFACE]

**T29 motion prompt:**
> 0–5 s: he writes notes fast in his notebook, focused; at about 2 s he checks a line in an open book, then keeps writing quickly. The camera pushes in slowly. Soft daylight. [KEEPMOTION] [STYLE]

**Lock fill:** her "cosy high-neck knit sweater"; him "hoodie".
**Sound:** pens on paper, pages turning.

### T30 + T31 · Seg 30 · 0:58–1:00 · 2.13 Winter (split screen)
| Take | Route | Gen | Lock | Use |
|---|---|---|---|---|
| T30 her (left) | A | 5 s, 1080p | LOCK-HER, 1080p | ≈1.5–3.5 s |
| T31 him (right) | A | 5 s, 1080p | LOCK-HIM, 1080p | ≈1.5–3.5 s |

**First make WINTER-MSU** (`flux_3_image`, image: LOC-msu):
> The same view of this curved red-brick university building with tall glass windows, now in deep winter: snow covers the lawn, the paths and the bare oak branches, and snow is falling; soft grey light. Keep the building, its windows and the camera position exactly the same.

**T30 A1 refs:** H4, `C2_edinburgh-castle`
> The first image shows the young woman's face; the second image shows the place. A cold grey winter day in Edinburgh: the castle on its rock (as in the second image) above bare trees, wind and light drizzle. [HER] walks along the path below in a long burgundy coat and a cream scarf, hands in her pockets, the wind in her hair, face in three-quarter view. [KEEPFACE]

**T30 motion prompt:**
> 0–5 s: she walks along the path below the castle, hands in her coat pockets, the wind moving her hair and scarf, light drizzle falling; she glances up at the castle once. The camera tracks beside her at her pace. [KEEPMOTION] [STYLE]

**T31 A1 refs:** Z2, WINTER-MSU
> The first image shows the young man's face; the second image shows the place. [HIM] walks along the snowy path in front of the snow-covered red-brick building from the second image, in a dark puffer jacket, a beanie and a scarf, his breath visible in the cold air, face in three-quarter view. Snow is falling. [KEEPFACE]

**T31 motion prompt:**
> 0–5 s: he walks along the snowy path past the building, snow falling, his breath visible; he pulls his scarf up a little. The camera tracks beside him at his pace. [KEEPMOTION] [STYLE]

**Lock fill:** her "long burgundy coat and cream scarf"; him "dark puffer jacket, beanie and scarf".
**Sound:** her side wind and drizzle; his side the crunch of snow.
**Note:** the same building in summer (Seg 25) and in deep snow (Seg 30) shows time passing without any date.

### T32 + T33 · Seg 31–32 · 1:00–1:04 · 2.14 The call (split screen, KEY SHOT, make 2 versions of each)
One continuous take per half.
| Take | Route | Gen | Lock | Use |
|---|---|---|---|---|
| T32 her (left) | A | 6 s, 1080p | LOCK-HER, 1080p | ≈1.0–5.0 s, uncut |
| T33 him (right) | A | 6 s, 1080p | LOCK-HIM, 1080p | ≈1.0–5.0 s, uncut |

**T32 A1 refs:** H4
> The image shows the young woman's face. A cosy student room in Edinburgh in the evening: a warm desk lamp, rain on the dark window behind her. [HER] sits at her desk facing an open laptop (its screen turned away from the camera), on a video call, smiling and talking. Seen from beside the laptop, her face in three-quarter view lit by the lamp. She wears a soft oversized high-neck sweater, hair down. [KEEPFACE]

**T32 motion prompt:**
> Camera beside the laptop, slow push-in, no cuts. 0–2.5 s: she talks warmly to the laptop on a video call, smiling and encouraging him, with small hand gestures. 2.5–4 s: she watches the screen as he shows her something; her eyes widen. 4–6 s: she laughs. The laptop screen is never readable. Rain runs down the dark window behind her. [KEEPMOTION] [STYLE]

**T33 A1 refs:** Z2
> The image shows the young man's face. A student room in Michigan in the evening: heavy snow falling outside the window, warm lamp light inside and cold blue light from the window. [HIM], in a hoodie, sits at his desk on a video call on his laptop (screen turned away from the camera), smiling, face in three-quarter view. [KEEPFACE]

**T33 motion prompt:**
> Camera beside the laptop, slow push-in, no cuts. 0–2.5 s: he listens and smiles, nodding. 2.5–4 s: he turns the laptop toward the snowy window to show her the snow, then turns it back. 4–6 s: he laughs. The laptop screen is never readable. [KEEPMOTION] [STYLE]

**Lock fill:** her "soft oversized high-neck sweater"; him "hoodie".
**Edit:** sync the halves so his laptop turn and her widening eyes happen together, then both laugh. Chapter end: **0.6 s soft dissolve — his snowy window melts into Edinburgh Castle on a bright winter day** (Seg 33).
**Sound:** her rain on the window; his muffled snow wind; both laughs audible, soft.

---

## 8. Take sheets — Chapter 3: New Year together (Seg 33–42, 1:04–1:24)

Families stay at medium/wide distance with gentle motion. Only the couple is locked. His brother (no face reference) stays at medium distance, mostly side-on.

### T34 · Seg 33 · 1:04–1:06 · 3.01 Together again (method R)
| Route | Gen | Lock | Use |
|---|---|---|---|
| B + R, start = `C3_edinburgh-castle-families` (trailer lettering softened, 16:9) | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | the last 2 s of the reversed clip, ending on the photo |

**Motion prompt (generated forward, played reversed):**
> Start exactly from this photo: five people in warm winter coats and hats on a wide wet esplanade in front of a stone castle, bright low winter sun and long shadows; the young woman in a burgundy coat and cream scarf, the young man in a grey puffer jacket. 0–2 s: they relax out of the photo pose, their smiles soften and they start chatting. 2–5 s: they drift slightly apart, turning to each other. Visitors in the far background stand still, looking at the castle. The camera cranes slowly UP from the group toward the castle walls. Gentle natural movement; everyone stays at a wide distance; no one walks. [KEEPMOTION] [STYLE]

Played reversed: the camera cranes down from the castle walls to the group, which settles into the photo pose.
**Lock fill:** her "burgundy coat and cream scarf"; him "grey puffer jacket". Closeness only as in the real photo.
**Edit:** enters through the chapter dissolve from Seg 32.
**Sound:** wind on the esplanade, distant city murmur, gulls.

### T35 · Seg 34 · 1:06–1:08 · 3.02 London lights
| Route | Gen | Lock | Use |
|---|---|---|---|
| N, start = `C3_london-street-lights` (shop names and plates softened, 16:9) | 5 s, 1080p | — | ≈1.0–3.0 s |

**Motion prompt:**
> Animate this photo as real footage: a London shopping street at dusk with golden branch-shaped Christmas lights strung across it. Black cabs and a red double-decker bus drive through, people cross the road, the lights twinkle. The camera glides slowly forward down the street under the lights. Shop names and number plates stay soft and unreadable. [STYLE]

**Edit:** small **"London"** (§12.5).
**Sound:** traffic, a bus passing, street crowd.

### T36 · Seg 35 · 1:08–1:10 · 3.03 Under the Christmas arch (method R)
| Route | Gen | Lock | Use |
|---|---|---|---|
| B + R, start = `99e9ca6d…` | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | the last 2 s of the reversed clip, ending on the photo |

**Motion prompt (generated forward, played reversed):**
> Start exactly from this photo: five people in winter jackets in front of a large Christmas arch of greenery, red bows and baubles at a grand entrance, olive trees in stone planters on either side. 0–2 s: they relax out of the pose and lean a little apart from each other, still smiling; the ribbons stir in the breeze. 2–5 s: they chat quietly; the camera tilts slowly UP from the group to the red bows and greenery of the arch. Everyone in sharp focus; gentle motion; no one walks. [KEEPMOTION] [STYLE]

Played reversed: the camera tilts down from the arch, and they lean in closer and smile into the photo pose.
**Lock fill:** outfits as in the photo.
**QA:** ribbons may move either way; check no person reads backwards.

### T37 · Seg 36 · 1:10–1:12 · 3.04 The winter fair (method E: end frame = the real photo)
| Route | Gen | Lock | Use |
|---|---|---|---|
| A start + B end | 5 s, 1080p, `start_image` = A1 frame, `end_image` = `C3_winter-wonderland` (stall signs softened, 16:9) | LOCK-BOTH, 720p + Topaz | ≈3.0–5.0 s (stop → peace signs) |

**A1 refs:** H4, Z2, `C3_winter-wonderland`
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place, the outfits and his younger brother. Night at the bright Christmas funfair from the third image, glowing candy-cane stalls and fairground lights. [HER] in a grey beanie and black puffer jacket, [HIM] in a grey puffer jacket, and his younger brother (the boy in glasses from the third image, same clothes, seen side-on) walk side by side toward the camera between the stalls, laughing, a few metres before the spot where the third image was taken. [KEEPFACE]

**Motion prompt:**
> 0–3 s: the three walk between the glowing stalls toward the camera, laughing and talking; the young man says something and his brother laughs. 3–5 s: they stop, turn to the camera and make peace signs with big smiles, ending exactly in the pose of the last frame. Fairground lights twinkle; people walk past behind. Light handheld camera, festive. [KEEPMOTION] [STYLE]

**Lock fill:** her "grey beanie and black puffer jacket"; him "grey puffer jacket".
**QA:** the brother's face matches the real photo by the final pose; keep his motion gentle.
**Sound:** fairground music far off, crowd, laughter.

### T38 · Seg 37 · 1:12–1:14 · 3.05 Tower Bridge
| Route | Gen | Lock | Use |
|---|---|---|---|
| B, start = `e08a51f8…` (shopping-bag advert painted out) | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | ≈1.5–3.5 s |

**Motion prompt:**
> Start exactly from this photo: five people in winter coats at a riverside railing at night, Tower Bridge lit up behind them in light fog. 0–2 s: they smile; a boat glides past on the river behind them, its lights reflected in the water. 2–5 s: the camera cranes slowly up over the group to reveal Tower Bridge glowing in the fog. [KEEPMOTION] [STYLE]

**Lock fill:** outfits as in the photo.
**Sound:** the river, a boat horn far away.

### T39 · Seg 38–39 · 1:14–1:18 · 3.06 By the tree (KEY SHOT, make 2 versions)
Route A with the real photo as place and outfit reference, because the take starts before the photo moment.
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 6 s, 1080p | LOCK-BOTH, 1080p | ≈1.0–5.0 s, uncut (may stretch to 5 s on the grid) |

**A1 refs:** H4, Z2, `C3_hotel-tree-couple`
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place and their outfits. In the hotel lounge from the third image: a tall Christmas tree with red and gold baubles, a large window full of twinkling city lights behind. [HER] and [HIM], in exactly the outfits they wear in the third image, walk side by side toward the tree from a few steps away, looking up at the decorations, talking softly; there is a little space between them. [KEEPFACE]

**Motion prompt:**
> Slight slow motion; the camera arcs slowly around them with the tree lights as soft bokeh in the foreground; no cuts. 0–1.5 s: they walk up to the tree side by side, looking at the decorations and talking softly. 1.5–3 s: she takes a small gold bauble and hangs it on a branch. 3–4.5 s: he watches her and smiles. 4.5–6 s: they turn and look at each other, smiling. They do not touch: no head on the shoulder, no hug, no holding hands. [KEEPMOTION] [STYLE]

**Lock fill:** outfits as in the photo.
**QA (failure #15 in the old handoff):** cut any version that adds her head on his shoulder or any touch.
**Sound:** soft lounge ambience, a bauble's tiny clink; the music is at its quietest and warmest here.

### T40 · Seg 40 · 1:18–1:20 · 3.07 New Year's Eve (method E)
| Route | Gen | Lock | Use |
|---|---|---|---|
| A start + B end | 5 s, 1080p, `start_image` = A1 frame, `end_image` = `cbd5fc8a…` | LOCK-BOTH, 720p + Topaz | ≈3.0–5.0 s (arrive at the top → turn for the photo) |

**A1 refs:** H4, Z2, `cbd5fc8a…`
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the place, the outfits and the family. A low angle from the bottom of the grand hotel staircase in the third image, warm light and decorated Christmas trees at the top: the five people from the third image, dressed up exactly as in it (the young woman in a long white knit dress, the young man in a dark suit), climb the last steps toward the top, seen from slightly below and behind. [KEEPFACE]

**Motion prompt:**
> 0–2.5 s: the five walk up the last steps of the grand staircase toward the warm light and the decorated Christmas trees; the camera starts low at the bottom of the stairs and rises slowly. 2.5–5 s: they reach the top, turn around to face the camera and settle into a group pose, smiling; she turns slightly toward him — ending exactly as in the last frame. [KEEPMOTION] [STYLE]

**Lock fill:** her "long white knit dress"; him "dark suit".
**Sound:** soft hotel lobby, dresses rustling, distant piano.

### T41 · Seg 41 · 1:20–1:22 · 3.08 The dinner
| Route | Gen | Lock | Use |
|---|---|---|---|
| B, start = `C3_new-year-dinner` (16:9) | 5 s, 1080p | LOCK-BOTH, 1080p | ≈1.5–3.5 s |

**Motion prompt:**
> Start exactly from this photo: a young couple at a dinner table in an elegant hotel restaurant, greenery and fairy lights hanging from the balcony above, gold Christmas crackers on the table. 0–1.5 s: they sit as in the photo. 1.5–3.5 s: she smiles and turns to look at him; he smiles back at her. 3.5–5 s: they share the smile; a waiter moves softly through the blurred background. The camera pushes in slowly. [KEEPMOTION] [STYLE]

**Lock fill:** outfits as in the photo.
**Sound:** restaurant murmur, glasses, cutlery.

### T42 · Seg 42 · 1:22–1:24 · 3.09 Midnight (last shot of chapter 3)
| Route | Gen | Lock | Use |
|---|---|---|---|
| N, start = LOC-thames `545612f8…` | 5 s, 1080p | — | ≈1.5–3.5 s, ending on a big bright burst |

**Motion prompt:**
> Animate this photo as real footage: New Year's midnight in London; fireworks burst over the River Thames in many colours above the lit city skyline; every colour reflects in the river; small crowds on the riverbank cheer far away. Wide shot; the camera pushes slowly forward over the river. No countdown numbers, no year, no text anywhere. [STYLE]

**Edit:** chapter end: a bright white-gold burst → **0.6 s flash dissolve** into the sunlit McEwan Hall (Seg 43).
**Sound:** soft, muffled booms and distant cheers under the music. No countdown voices.

---

## 9. Take sheets — Chapter 4: Graduations and home (Seg 43–49, 1:24–1:38)

### T43 + T44 · Seg 43 · 1:24–1:26 · 4.01 Graduations (split screen)
| Take | Route | Gen | Lock | Use |
|---|---|---|---|---|
| T43 her (left) | B, start = `C4_graduation-her-cap-raised` | 5 s, 1080p | LOCK-HER, 1080p | ≈1.5–3.5 s |
| T44 him (right) | B, start = `2ae4ab0c…` (or `cd5e2fc2…` cropped for the half) | 5 s, 1080p | LOCK-HIM, 1080p | ≈1.5–3.5 s |

**T43 motion prompt:**
> Start exactly from this photo: a young woman in a black graduation gown over a long white dress stands on a wet stone square in front of a grand domed sandstone hall in golden late-afternoon light, holding her graduation cap raised. 0–2 s: she lifts the cap a little higher. 2–3.5 s: she smiles over her shoulder toward the camera. 3.5–5 s: she laughs softly; other graduates move in the background; clouds drift. The camera slowly orbits a little around her. [KEEPMOTION] [STYLE]

**T44 motion prompt:**
> Start exactly from this photo: a young man in a black graduation cap and gown holds a rolled diploma outside a modern glass arena on an overcast spring day; a young woman in a brown blazer (his sister) holds his arm, exactly as in the photo. 0–2 s: they smile. 2–3.5 s: he lifts the diploma slightly with a proud smile. 3.5–5 s: his sister laughs; people mingle in the background. All signs stay soft and unreadable. The camera slowly orbits a little around them. [KEEPMOTION] [STYLE]

**Lock fill:** her "black graduation gown over a long white dress" (hair as in the photo); him "black graduation cap and gown". His sister is not locked: keep her motion gentle.
**Edit:** enters through the firework flash dissolve. Split screen, matched orbit direction (both clockwise).
**Sound:** her side a choir echo from the hall; his side applause far off.

### T45 · Seg 44 · 1:26–1:28 · 4.02 McEwan Hall
| Route | Gen | Lock | Use |
|---|---|---|---|
| N, start = `26692df3…` cropped to 16:9 | 5 s, 1080p | — | ≈1.0–3.0 s |

**Motion prompt:**
> Animate this photo as real footage: looking up at the gilded, painted dome of a grand circular hall, arched windows and columns below, families watching from the galleries. Warm light; the camera tilts very slowly upward. [STYLE]

**Sound:** a soft choir echoing under the dome, blended into the music.

### T46 · Seg 45 · 1:28–1:30 · 4.03 The pipers
| Route | Gen | Lock | Use |
|---|---|---|---|
| N, start = `4e6275b8…` cropped to 16:9 | 5 s, 1080p | — | ≈1.0–3.0 s |

**Motion prompt:**
> Animate this photo as real footage: outside a sandstone hall at dusk, a Scottish piper in full Highland dress plays the bagpipes, fingers moving on the chanter, and a drummer in a kilt plays the snare drum; graduates in gowns walk past under a lit street lamp. The camera tracks slowly sideways past the pipers. [STYLE]

**Sound:** **real bagpipes and snare drum rise over the music** for these 2 s, then hand back to the music.

### T47 · Seg 46 · 1:30–1:32 · 4.04 Flowers (method R)
| Route | Gen | Lock | Use |
|---|---|---|---|
| B + R, start = `C4_graduation-her-family` (16:9) | 5 s, 1080p | LOCK-HER, 720p + Topaz (re-lock at 1080p if her face is soft) | the last 2 s of the reversed clip, ending on the photo |

**Motion prompt (generated forward, played reversed):**
> Start exactly from this photo: a young woman in a graduation gown over a white dress holds a large bouquet, standing with two women in long coats and a boy in a cream sweater on a wet stone square in front of a grand sandstone hall, low golden sunlight. 0–2 s: they relax out of the pose; the young woman hands the bouquet to the older woman beside her (her mother), who takes it with both hands. 2–5 s: they stand half a step apart, chatting and smiling. The camera arcs slowly to the left. Everyone in sharp focus, gentle motion, medium-wide; background people stand still; no one walks. [KEEPMOTION] [STYLE]

Played reversed: her mother hands her the bouquet, she smiles, they settle into the photo pose, the camera arcs right.
**Lock fill:** her "graduation gown over a white dress".
**Sound:** soft voices, paper of the bouquet rustling.

### Seg 47 · 1:32–1:34 · 4.05 Flying home — made in the edit
`globe.py` (old handoff, Appendix C) with `DUR = 2.0` (or render the 3.6 s version and speed it up ×1.8). Night Earth with city lights; arcs from Michigan and Edinburgh meet over Baku with a soft flash; only the word "Baku". **Sound:** a soft whoosh along the arcs and a soft chime at the flash.

### T48 · Seg 48–49 · 1:34–1:38 · 4.06 Home (KEY SHOT, make 2 versions)
One continuous take, framed **exactly** like T17 (the goodbye).
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 6 s, 1080p | LOCK-BOTH, 720p + Topaz | ≈1.0–5.0 s, uncut, ending as they meet (may stretch to 5 s on the grid) |

**A1 refs:** H1, Z1, ESC-FRAME (the T17 A1 frame, for the exact composition), LOC-airport
> The first image shows the young woman's face, the second image shows the young man's face, the third image shows the exact framing to copy, the fourth image shows the place. Exactly the same perfectly symmetrical wide framing as the third image: the two escalators on either side of the tall green tree in the terminal. [HER] has just stepped off the bottom of the LEFT escalator and [HIM] off the RIGHT one, at the same moment, each with a suitcase. Summer outfits: she wears a long, flowing white-cream summer dress with a high neckline and short sleeves, hair down; he wears a light-blue linen shirt and beige chinos. They are small in the frame. [KEEPFACE]

**Motion prompt:**
> A perfectly symmetrical centred wide shot; the camera very slowly pushes in; no cuts. 0–1.5 s: both step off the bottom of the escalators at the same moment on either side of the tree and turn toward each other. 1.5–2.5 s: they see each other and smile. 2.5–5 s: they leave their suitcases and walk toward each other, meeting in the middle in front of the tree. 5–6 s: they stand face to face, close, smiling — no hug, no touch. [KEEPMOTION] [STYLE]

**Lock fill:** her "long white-cream summer dress with a high neckline"; him "light-blue linen shirt and beige chinos".
**Edit:** cut it so it mirrors Seg 18–19. Chapter end: **0.6 s soft dissolve** into Seg 50.
**Sound:** the same echoing hall as the goodbye; the music resolves into relief.

---

## 10. Take sheets — Chapter 5: Army (Seg 50–54, 1:38–1:48)

Music mood: quieter and tender, turning gently proud at the visit.

### T49 · Seg 50 · 1:38–1:40 · 5.01 In uniform
| Route | Gen | Lock | Use |
|---|---|---|---|
| B, start = `C5_him-uniform` (16:9) | 5 s, 1080p | LOCK-HIM, 1080p | ≈1.0–3.0 s |

**Motion prompt:**
> Start exactly from this photo: a young man in a green digital-camouflage military uniform and matching cap stands on a wide sunlit concrete square in front of a long brick building, a fence with anchor emblems behind him. 0–1.5 s: he straightens. 1.5–3 s: he gives a small, calm smile. 3–5 s: he turns his head toward the building. A light breeze; clouds drift. Slightly low camera angle, slow push-in. [KEEPMOTION] [STYLE]

**Lock fill:** him "green digital-camouflage uniform and matching cap".
**Sound:** wind across the square, a distant flag rope tapping.

### T50 · Seg 51 · 1:40–1:42 · 5.02 Watching him go (KEY SHOT, make 2 versions)
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER, 1080p | ≈1.5–3.5 s |

**A1 refs:** H4, `C5_visit-families` (the square and the stone gate), `C5_him-uniform` (his uniform, from behind)
> The first image shows the young woman's face, the second image shows the place, the third image shows the young man's uniform. Close-up of [HER] on a wide concrete square on a grey day, in a cream coat with a high collar, hair down, face in three-quarter view. In the soft-focus background, the young man in the green digital-camouflage uniform and cap from the third image walks away from the camera toward the stone gate arch from the second image (seen from behind). Shallow depth of field; the gate lettering is out of focus. [KEEPFACE]

**Motion prompt:**
> Slow motion, close-up, shallow depth of field. 0–5 s: she watches him walk away toward the stone gate arch in the soft background; she tries to smile, takes a small breath, and her eyes glisten. The camera pushes in very slowly. [KEEPMOTION] [STYLE]

**Lock fill:** her "cream coat".
**Sound:** almost nothing but the music and the wind.

### T51 · Seg 52 · 1:42–1:44 · 5.02 — at the gate he turns and waves
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HIM, 1080p | ≈1.2–3.2 s |

**A1 refs:** Z1, `C5_him-uniform`, `C5_visit-families`
> The first image shows the young man's face, the second image shows his uniform, the third image shows the place. Medium shot at the stone gate arch from the third image (lettering out of focus): [HIM], in the green digital-camouflage uniform and cap from the second image, stands at the gate turning back toward the square, face in three-quarter view. Far behind him on the wide concrete square stands the young woman in a cream coat, very small. Grey day. [KEEPFACE]

**Motion prompt:**
> 0–1.5 s: he stops at the gate and turns back toward the square. 1.5–3.5 s: he gives one small wave and a calm smile. 3.5–5 s: far away, small, she waves back. The gate lettering stays soft and out of focus. Slow push-in. [KEEPMOTION] [STYLE]

**Lock fill:** him "green digital-camouflage uniform and cap". She is tiny: no lock.

### T52 · Seg 53 · 1:44–1:46 · 5.03 Waiting
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 5 s, 1080p | LOCK-HER, 1080p | ≈1.5–3.5 s |

**A1 refs:** H4
> The image shows the young woman's face. A bedroom window in Baku overlooking the city and the Caspian Sea. [HER] sits on the window seat in a cosy high-neck sweater, hair down, holding her phone (its screen a soft glow, nothing readable), face in three-quarter view, the window beside her. Soft light. [KEEPFACE]

**Motion prompt:**
> 0–2 s: she looks at a photo on her phone (the screen is only a soft glow, nothing readable). 2–5 s: she looks up and out of the window at the city; outside, the seasons change in a fast time-lapse — summer sun, autumn colours, winter grey, spring green — while she stays still and calm. No clock, calendar or date anywhere. The camera pushes in slowly. [KEEPMOTION] [STYLE]

**Fallback** if Kling cannot change the seasons behind her: generate her take with a plain bright window; make a 5 s time-lapse plate of the Baku view (Route N, from a FLUX still of the city and the sea, prompt the seasons changing); composite it into the window in the edit with a mask.
**Lock fill:** her "cosy high-neck sweater".
**Sound:** quiet room tone; the seasons pass only in the music.

### T53 · Seg 54 · 1:46–1:48 · 5.04 Visiting day (method R, last shot of chapter 5)
| Route | Gen | Lock | Use |
|---|---|---|---|
| B + R, start = `C5_visit-families` (car plates blurred, gate lettering unchanged, 16:9) | 5 s, 1080p | LOCK-BOTH, 720p + Topaz | the last 2 s of the reversed clip, ending on the photo |

**Motion prompt (generated forward, played reversed):**
> Start exactly from this photo: family members on a wide concrete square in front of a stone gate arch; the young man in a green digital-camouflage uniform and cap in the middle, the young woman in white beside him. 0–2 s: they relax out of the photo pose, smiles softening; a light breeze moves hair and coats. 2–5 s: they turn a little to each other and chat; background people stand still. The camera pulls slowly back. Very gentle motion, everyone at a wide distance, no one walks. The gate lettering does not change. [KEEPMOTION] [STYLE]

Played reversed: the camera pushes in slowly while the families gather and settle into the photo, smiling.
**Lock fill:** her "white outfit"; him "green digital-camouflage uniform and cap".
**Edit:** chapter end: **0.6 s soft dissolve** into Seg 55.
**Sound:** soft voices of the families; the music lifts, proud.

---

## 11. Take sheets — Chapter 6: Asking for her hand (Seg 55–61, 1:48–2:02)

Her look: elegant white outfit (pearl buttons, high embroidered collar), dark hair in a **low bun** (as in the real photos). Use H8 + H9 with HER7 in every lock of this chapter.
Sound for the chapter: warmer music, soft family voices and tea glasses clinking in the background.

### Seg 55 · 1:48–1:50 · 6.01 Hə Almağa Gəlmişik — made in the edit
`extras.py sign` (old handoff, Appendix C) with `dur = 2.0`, source = `e9abbd5b…`. A very slow push-in on the real photo; the letters are never animated or redrawn. Enters through the chapter dissolve.

### T54 · Seg 56 · 1:50–1:52 · 6.02 The table is set
| Route | Gen | Lock | Use |
|---|---|---|---|
| N, start = `C6_table-set` cropped so the TV is out of frame (16:9) | 5 s, 1080p | — | ≈1.0–3.0 s (plate set → candle lit) |

**Motion prompt:**
> Animate this photo as real footage: a long mirrored dining table laid with white and gold plates, crystal glasses, tall white candles and white flowers, white chairs on both sides, soft daylight through the curtains. 0–2 s: a pair of hands in modest white sleeves (no face, no body visible) enters the frame and places the last white-and-gold plate at a setting. 2–4 s: the hands light a tall white candle with a long match. 4–5 s: the flame flickers and light glints across the crystal. The camera glides slowly along the table. [STYLE]

**Sound:** a plate set down softly, a match striking.

### T55 · Seg 57 · 1:52–1:54 · 6.03 Waiting to come in
| Route | Gen | Lock | Use |
|---|---|---|---|
| B, start = `C6_her-waiting-calla` (16:9) | 5 s, 1080p | LOCK-HER (+H8, H9), 1080p | ≈2.5–4.5 s |

**Motion prompt:**
> Start exactly from this photo: the young woman in an elegant white outfit with pearl buttons, her dark hair in a low bun, stands in profile holding a single white calla lily beside a table of white and blue flowers and sweets. 0–2 s: she stands holding the lily, listening to voices from the next room. 2–5 s: she smiles softly to herself, a little shy; her eyes stay up — she does not look down. The camera arcs slowly from her profile toward a three-quarter view of her face. [KEEPMOTION] [STYLE]

**Lock fill:** her "elegant white outfit with pearl buttons"; hair "dark hair in a low bun".
**QA (user's rule):** eyes stay up. This echoes the corridor smile of Seg 06.
**Sound:** muffled family voices from the next room.

### T56 · Seg 58 · 1:54–1:56 · 6.04 The tea
| Route | Gen | Lock | Use |
|---|---|---|---|
| B, start = `eb8f3642…` | 5 s, 1080p | LOCK-HER (+H8, H9), 1080p | ≈1.0–3.0 s (lifts the tray → turns to the door) |

**Motion prompt:**
> Start exactly from this photo: the young woman in an elegant white outfit holds a gold mirrored tray of pear-shaped armudu tea glasses decorated with tiny white flowers, white and blue flower arrangements behind her. 0–1.5 s: she lifts the tray a little higher from the side table where it rested; steam rises from the tea. 1.5–3 s: she turns toward the door. 3–5 s: she steps forward with the tray, a small smile. The camera moves backward in front of her. The sign behind her stays exactly as it is. [KEEPMOTION] [STYLE]

**Lock fill:** as T55.
**QA:** the sign letters do not change (soften the sign only if they warp).
**Sound:** tea glasses clinking softly on the tray.

### T57 · Seg 59–60 · 1:56–2:00 · 6.05 Serving the tea (KEY SHOT, make 2 versions)
Route A — **never animate the real serving photo** (guests' faces). Use it only as a reference for her dress, hair and the table.
| Route | Gen | Lock | Use |
|---|---|---|---|
| A | 8 s, 1080p | LOCK-HER (+H8, H9), 1080p | Seg 59 ≈0.5–2.5 s (walks in); Seg 60 ≈4.6–6.6 s (sets the glass) — a real cut inside the scene |

**A1 refs:** H9, H4, `C6_table-set`, `79246d22…`
> The first two images show the young woman's face (in the first one her hair is in a low bun, as it must be here), the third image shows the room and the table, the fourth image shows her outfit only. From just behind her right shoulder at the doorway: [HER], her dark hair in a low bun, in the elegant white outfit with a high embroidered collar and pearl-buttoned cuffs from the fourth image, holds a gold tray of armudu tea glasses and is about to walk toward the long table from the third image (white and gold plates, crystal glasses, tall white candles). The seated guests at the table are only dark suits, out of focus, cut by the frame edges or turned away — no faces visible anywhere. [KEEPFACE]

**Motion prompt:**
> No cuts. 0–3 s: the camera follows just behind her right shoulder as she walks into the room carrying the tray toward the long table; the seated guests are only blurred dark suits at the edges of the frame, their faces never visible. 3–4.5 s: she reaches a place setting; the camera moves round to her side. 4.5–6.5 s: a close shot: she leans in and gently sets one armudu glass of tea on its saucer, with a soft smile; her face and the glass are sharp, everything else is soft. 6.5–8 s: she straightens, still smiling softly. Shallow depth of field. No face other than hers is ever visible. [KEEPMOTION] [STYLE]

**Lock fill:** her "elegant white outfit with a high embroidered collar and pearl-buttoned cuffs"; hair "dark hair in a low bun".
**He is not seen** (the real proposal footage shows him afterwards).
**QA:** zero guest faces in any frame, including blurred ones; if one appears, crop or regenerate.
**Sound:** a glass set on a saucer, soft voices, a hush.

### T58 · Seg 61 · 2:00–2:02 · 6.06 "Hə" → 6.07 fade through the steam
| Route | Gen | Lock | Use |
|---|---|---|---|
| B, start = `C6_her-tea-glass` (widen to 16:9) | 5 s, 1080p | LOCK-HER (+H8, H9), 1080p | ≈0.6–2.6 s; the last 1.0 s is the steam fade |

**Motion prompt:**
> Start exactly from this photo: the young woman in an elegant white outfit, her hair in a low bun, holds a single armudu glass of tea on a crystal saucer and smiles warmly at the camera. 0–1 s: she smiles warmly; steam rises gently from the tea. 1–3 s: the camera pushes in slowly until the tea glass fills the frame. 3–5 s: the steam rises thicker toward the lens and glows softly in the light. [KEEPMOTION] [STYLE]

**Lock fill:** as T55. Lock before the fade is added.
**Edit:** §12.6 — fade **through the steam** to soft white over the last ~1 s; the real proposal footage follows. Grade the end to match the real footage.
**Sound:** the music lands its final warm note on the white; leave a short breath before the real footage's own sound.

---

## 12. Edit-only work and assembly rules

### 12.1 Split screens (Seg 20, 22, 29, 30, 31–32, 43, and the background of 24)
- Canvas 1920×1080. **Left half = her** (x 0–957), **4 px white divider** (x 958–961), **right half = him** (x 962–1919). Each half is a 958×1080 crop of its own 1080p take, chosen so the face sits about one third in from the divider and **looks toward the divider** (her facing right, him facing left).
- Match exposure and colour between the halves (grade both to the same warm look).
- Both halves start and end on the same frame; the cut in and out is shared.
- In Seg 31–32 sync the beats: his laptop turn and her widening eyes at the same moment, then the shared laugh.

### 12.2 Seg 24 — the photos fly between the halves (write a small `fly.py`, OpenCV + ffmpeg, 2.0 s, 24 fps)
- Background: split screen. Left = T23 tail (≈3.5–5.0 s: she lowers her phone). Right = T24 head (≈0.0–2.0 s: he looks at his phone). Darken both by ~15% so the cards read.
- **Card 1 — her castle photo** (`C2_edinburgh-castle`): white-bordered rounded card, 420 px wide, 14 px white border, 22 px corner radius, soft drop shadow. 0.00–0.20 s: appears near her phone on the left half, scaling 0.6→1.0. 0.20–0.90 s: flies on a gentle upward arc across the divider to the right half (ease-in-out), rotating −4°→+3°. 0.90 s: lands near his phone with a tiny bounce and a soft **"ping"**. 0.90–1.10 s: fades out.
- **Card 2 — his campus photo** (`C2_msu-building`): 1.00–1.20 s appears on the right; 1.20–1.85 s flies back across to the left half; 1.85 s lands with a second soft **"ping"**; holds to 2.0 s.
- No names, no times, no dates, no text, no app interface. Cards stay modest in size; faces in the halves stay visible.

### 12.3 Seg 47 — globe
`globe.py` with `DUR = 2.0` (or speed the 3.6 s render ×1.8 with `setpts=PTS/1.8`). Check that the arcs start at East Lansing and Edinburgh and meet over Baku. The only word is "Baku".

### 12.4 Seg 55 — the sign
`extras.py sign` with `dur = 2.0` from `e9abbd5b…`. The letters are never animated.

### 12.5 On-screen words (edit only; never generated)
| Word | Where | When | Style |
|---|---|---|---|
| Where it all began | centred, slightly below the middle | 0:00.8–0:03.4 (over Seg 01–02) | thin elegant serif (e.g. Cormorant Garamond Light), white, 68 px, letter-spacing +2%, soft shadow (black 30%, blur 8 px), 0.4 s fade in/out |
| Edinburgh / Michigan | lower third of each half, centred in the half | Seg 20, 0.3–1.7 s into the segment | same serif, 48 px |
| Chicago | lower left | Seg 27, 0.3–1.7 s in | same, 48 px |
| London | lower left | Seg 34, 0.3–1.7 s in | same, 48 px |
| Baku | inside the globe (globe.py) | Seg 47 | as rendered |
No other words, numbers or dates anywhere in the 2:02.

### 12.6 The ending — 6.07, fade through the steam
- In the last ~1.0 s of Seg 61 the steam over the tea glass thickens toward the lens. Build a luminance key from the steam, brighten it, and ramp a soft warm-white (≈#FBF7F0) overlay from 0% to 100% over 1.0 s with an ease-in curve, so the white seems to grow **out of the steam**.
- Hold full white 2–3 frames, then the real proposal footage starts (it is not part of the 2:02).
- Grade the last 3–4 shots toward the colour of the real proposal footage so the change feels natural. Ask the user to attach that footage for the final step.

### 12.7 Closing card (after the real proposal footage only)
Soft cream/white background (or a softly blurred still from the real footage). **"Zamin & Narmin"** in the same serif, 88 px, and below it **"27.12.2026"**, 48 px. Fade in 1.0 s, hold 4 s, fade out 1.5 s. This is the only place in the whole film where names or a date appear.

### 12.8 Transitions
| Where | Transition |
|---|---|
| Start | 0.5 s fade in from black |
| Inside every scene | straight cuts (real film cuts) |
| Seg 07 → 08 | **match cut** on the smile → her laugh; music continuous |
| Ch 1 → 2 (Seg 16 → 17) | 0.6 s dissolve **through the glowing string lights** |
| Ch 2 → 3 (Seg 32 → 33) | 0.6 s dissolve: **his snowy window melts into Edinburgh Castle** |
| Ch 3 → 4 (Seg 42 → 43) | a bright firework burst → 0.6 s **flash dissolve** into the sunlit McEwan Hall |
| Ch 4 → 5 (Seg 49 → 50) | 0.6 s soft dissolve |
| Ch 5 → 6 (Seg 54 → 55) | 0.6 s soft dissolve |
| End (Seg 61) | fade through the steam to soft white (§12.6), then the real footage |

### 12.9 Retime, grade, export
- Retime every locked result back to its source length (Genjutsu returns ~5.7–6.04 s for a 5.9 s source; see `assemble.py`). For R-method takes, lock first, then reverse (`reverse` filter), then trim.
- Put each piece on the 2-second grid of §13. Continuous takes span their segments uncut.
- One warm, soft, consistent grade across the film; light film grain added in the edit; skin tones natural.
- Export: 1920×1080, 24 fps, H.264 CRF 17, `yuv420p`, AAC 192k, `-movflags +faststart`. Keep a ProRes or CRF 12 master as well.

---

## 13. Master timeline (2-second grid; the user's answers)

If T04 or T39/T48 stretch (allowed), shift every later row by the same amount.

| Seg | Time | Ch | Shot | Take · use | Route | What we see | Words | Out |
|---|---|---|---|---|---|---|---|---|
| 01 | 0:00–0:02 | 1 | 1.01 | T01 ≈1.0–3.0 | A | wide hall, class ends, dolly toward her writing | Where it all began | cut |
| 02 | 0:02–0:04 | 1 | 1.01 | T02 ≈0.6–2.6 | A | MCU: she closes the notebook, packs | (title ends 0:03.4) | cut |
| 03 | 0:04–0:06 | 1 | 1.01 | T03 ≈1.2–3.2 | A | curly-haired friend jokes; she laughs | — | cut |
| 04 | 0:06–0:08 | 1 | 1.01 | T04 (uncut, 04–05) | A | wave goodbye, walk, through the doorway | — | continuous |
| 05 | 0:08–0:10 | 1 | 1.02 | T04 | A | over her shoulder: he looks up from his phone | — | cut |
| 06 | 0:10–0:12 | 1 | 1.02 | T05 ≈1.8–3.8 | A | her face: eyes meet, small smile, eyes stay up | — | cut |
| 07 | 0:12–0:14 | 1 | 1.03+1.04 | T06 ≈1.2–3.2 | A | side view, slow-mo: they pass, shared smile | — | **match cut** |
| 08 | 0:14–0:16 | 1 | 1.05 | T07 ≈0.9–2.9 | A | café: she laughs at his joke | — | cut |
| 09 | 0:16–0:18 | 1 | 1.06 | T08 ≈1.8–3.8 | A | library: she explains, he nods, a quiet smile | — | cut |
| 10 | 0:18–0:20 | 1 | 1.07 | T09 ≈1.6–3.6 | A | red bridge with coffees, she laughs, camera rises | — | cut |
| 11 | 0:20–0:22 | 1 | 1.08 | T10 ≈1.5–3.5 | N | campus dusk time-lapse, crane up | — | cut |
| 12 | 0:22–0:24 | 1 | 1.09 | T11 ≈1.0–3.0 | N | ceremony, choir, push toward the stage | — | cut |
| 13 | 0:24–0:26 | 1 | 1.10 | T12 reversed, last 2 s | B+R | families gather into the photo | — | cut |
| 14 | 0:26–0:28 | 1 | 1.11 | T13 ≈0.6–2.6 | B | they laugh and walk out from the canopy | — | cut |
| 15 | 0:28–0:30 | 1 | 1.12 | T14 ≈1.0–3.0 | B | red carpet, flashes, she leans in | — | cut |
| 16 | 0:30–0:32 | 1 | 1.13 | T15 ≈1.0–3.0 | B | she dances, he turns; up into the lights | — | **dissolve (lights)** |
| 17 | 0:32–0:34 | 2 | 2.01 | T16 ≈1.0–3.0 | A | airport walk, grey and blue sweater sets | — | cut |
| 18 | 0:34–0:36 | 2 | 2.02 | T17 (uncut, 18–19) | A | symmetrical escalators: they part | — | continuous |
| 19 | 0:36–0:38 | 2 | 2.02 | T17 | A | halfway up: a small wave across the tree | — | cut |
| 20 | 0:38–0:40 | 2 | 2.03 | T18 + T19 split | A | plane windows, missing each other | Edinburgh / Michigan | cut |
| 21 | 0:40–0:42 | 2 | 2.04 | T20 ≈1.5–3.5 | N | two jets turn apart, golden hour | — | cut |
| 22 | 0:42–0:44 | 2 | 2.05 | T21 + T22 split | B | arrivals: look around, smile | — | cut |
| 23 | 0:44–0:46 | 2 | 2.06 | T23 ≈1.5–3.5 | A | fountain: she photographs the castle | — | cut |
| 24 | 0:46–0:48 | 2 | 2.07 | E (§12.2) | E | photos fly between the halves, two pings | — | cut |
| 25 | 0:48–0:50 | 2 | 2.08 | T24 ≈1.0–3.0 | A | he smiles at her photo, photographs the building | — | cut |
| 26 | 0:50–0:52 | 2 | 2.09 | T25 ≈1.0–3.0 | B | mascot photo pose, he laughs | — | cut |
| 27 | 0:52–0:54 | 2 | 2.10 | T26 ≈1.5–3.5 | B | Chicago at night, he walks by the river | Chicago | cut |
| 28 | 0:54–0:56 | 2 | 2.11 | T27 ≈1.8–3.8 | A | Meadows: her eyes widen, delighted smile | — | cut |
| 29 | 0:56–0:58 | 2 | 2.12 | T28 + T29 split | A | both busy writing notes | — | cut |
| 30 | 0:58–1:00 | 2 | 2.13 | T30 + T31 split | A | winter walks: drizzle and castle / deep snow | — | cut |
| 31 | 1:00–1:02 | 2 | 2.14 | T32 + T33 split (uncut, 31–32) | A | evening video call, talking, smiling | — | continuous |
| 32 | 1:02–1:04 | 2 | 2.14 | T32 + T33 | A | he shows the snow; both laugh | — | **dissolve (window → castle)** |
| 33 | 1:04–1:06 | 3 | 3.01 | T34 reversed, last 2 s | B+R | crane down: families settle at the castle | — | cut |
| 34 | 1:06–1:08 | 3 | 3.02 | T35 ≈1.0–3.0 | N | London Christmas street, cabs and a red bus | London | cut |
| 35 | 1:08–1:10 | 3 | 3.03 | T36 reversed, last 2 s | B+R | tilt down from the arch; they lean in | — | cut |
| 36 | 1:10–1:12 | 3 | 3.04 | T37 ≈3.0–5.0 | A→B (E) | winter fair: walk, then peace signs | — | cut |
| 37 | 1:12–1:14 | 3 | 3.05 | T38 ≈1.5–3.5 | B | Tower Bridge, boat passes, crane up | — | cut |
| 38 | 1:14–1:16 | 3 | 3.06 | T39 (uncut, 38–39) | A | they walk up to the tree | — | continuous |
| 39 | 1:16–1:18 | 3 | 3.06 | T39 | A | she hangs a bauble; they look at each other | — | cut |
| 40 | 1:18–1:20 | 3 | 3.07 | T40 ≈3.0–5.0 | A→B (E) | arrive at the top of the staircase, turn for the photo | — | cut |
| 41 | 1:20–1:22 | 3 | 3.08 | T41 ≈1.5–3.5 | B | dinner: she turns to him and smiles | — | cut |
| 42 | 1:22–1:24 | 3 | 3.09 | T42 ≈1.5–3.5 | N | fireworks over the Thames | — | **flash dissolve** |
| 43 | 1:24–1:26 | 4 | 4.01 | T43 + T44 split | B | her cap up / his diploma up | — | cut |
| 44 | 1:26–1:28 | 4 | 4.02 | T45 ≈1.0–3.0 | N | McEwan dome, tilt up | — | cut |
| 45 | 1:28–1:30 | 4 | 4.03 | T46 ≈1.0–3.0 | N | pipers and drummer | — | cut |
| 46 | 1:30–1:32 | 4 | 4.04 | T47 reversed, last 2 s | B+R | her mother hands her the bouquet | — | cut |
| 47 | 1:32–1:34 | 4 | 4.05 | E globe | E | two arcs meet over Baku | Baku | cut |
| 48 | 1:34–1:36 | 4 | 4.06 | T48 (uncut, 48–49) | A | summer outfits: they step off and turn | — | continuous |
| 49 | 1:36–1:38 | 4 | 4.06 | T48 | A | they meet by the tree, smiling, no touch | — | **dissolve** |
| 50 | 1:38–1:40 | 5 | 5.01 | T49 ≈1.0–3.0 | B | him in uniform, calm smile | — | cut |
| 51 | 1:40–1:42 | 5 | 5.02 | T50 ≈1.5–3.5 | A | close on her, he walks to the gate behind | — | cut |
| 52 | 1:42–1:44 | 5 | 5.02 | T51 ≈1.2–3.2 | A | at the gate he turns and waves | — | cut |
| 53 | 1:44–1:46 | 5 | 5.03 | T52 ≈1.5–3.5 | A | window in Baku, seasons change | — | cut |
| 54 | 1:46–1:48 | 5 | 5.04 | T53 reversed, last 2 s | B+R | visiting day, families settle | — | **dissolve** |
| 55 | 1:48–1:50 | 6 | 6.01 | E sign | E | the sign, slow push-in | (real sign) | cut |
| 56 | 1:50–1:52 | 6 | 6.02 | T54 ≈1.0–3.0 | N | hands place the plate, light a candle | — | cut |
| 57 | 1:52–1:54 | 6 | 6.03 | T55 ≈2.5–4.5 | B | calla lily, soft smile, eyes up | — | cut |
| 58 | 1:54–1:56 | 6 | 6.04 | T56 ≈1.0–3.0 | B | she lifts the tray, turns to the door | — | cut |
| 59 | 1:56–1:58 | 6 | 6.05 | T57 ≈0.5–2.5 | A | she walks in with the tray | — | cut |
| 60 | 1:58–2:00 | 6 | 6.05 | T57 ≈4.6–6.6 | A | she sets a glass of tea, soft smile | — | cut |
| 61 | 2:00–2:02 | 6 | 6.06 + 6.07 | T58 ≈0.6–2.6 | B | smile → glass fills the frame → steam to white | — | **steam fade → real footage** |

Chapter lengths: Ch1 32 s · Ch2 32 s · Ch3 20 s · Ch4 14 s · Ch5 10 s · Ch6 14 s = **2:02**.

---

## 14. Sound plan

**Music:** one continuous piece for the whole 2:02 (source still to confirm, §17). If AI-made (`generate_audio`), prompt:
> Gentle cinematic romantic score, about 2 minutes 5 seconds, solo piano with soft warm strings, around 72 bpm, no vocals. Starts from silence, light and warm; a gentle rise at 0:10–0:14; playful and warm until 0:24; a fuller swell at 0:24–0:32; thinner and bittersweet at 0:34–0:42; curious and warm with a light pulse from 0:42 to 1:00; tender at 1:00–1:04; festive and bright with soft bells from 1:04 to 1:14; at its quietest and warmest at 1:14–1:18; a lift at 1:22–1:24; proud and full at 1:24–1:38; quiet and tender at 1:38–1:46 with a small proud lift at 1:46; warm and full from 1:48, resolving on one final warm note at 2:01–2:02.
If the user sends a song: cut it to 2:02–2:04 so its ending lands on the steam fade; keep cuts on the beat where possible.

**Real sounds** (`search_sound_effects` / `download_sound_effect`), always under the music (about −10 dB), never voices with words that can be understood:
| Segments | Sounds |
|---|---|
| 01–03 | classroom chatter, chairs, a bag zipping, notebook closing; her laugh in Seg 03 audible |
| 04–05 | chatter fading at the door, corridor footsteps, airier room tone |
| 06–07 | corridor sound drops away; music rises (no effects) |
| 08–09 | café murmur, a cup on a saucer; quiet library, a page turning |
| 10 | footsteps on the wooden bridge, birds, wind in the pines |
| 11 | music only |
| 12 | soft choir blended in |
| 13–15 | evening voices; footsteps; shutter clicks and flash pops |
| 16 | party ambience swelling into the dissolve |
| 17–19 | terminal ambience, suitcase wheels, echoing hall, escalator hum |
| 20–21 | cabin hum; high-altitude wind |
| 22–28 | wind / campus birds; fountain water and a phone-camera click; two soft "pings" (Seg 24); a click (Seg 25); festival crowd; river water and a boat; park birds |
| 29–30 | pens and pages; drizzle and wind / snow crunch |
| 31–32 | rain on her window, muffled snow wind on his; both laughs soft |
| 33–37 | esplanade wind and gulls; London traffic and a bus; breeze; fairground and laughter; river and a far boat horn |
| 38–41 | soft lounge ambience and a bauble's clink; hotel lobby and distant piano; restaurant murmur, glasses |
| 42 | soft muffled firework booms and distant cheers (no countdown) |
| 43–45 | choir echo / far applause; choir under the dome; **bagpipes and drum up front for Seg 45** |
| 46–47 | voices and bouquet paper; soft whoosh and a chime on the globe |
| 48–49 | the same echoing hall as the goodbye |
| 50–54 | wind across the square; near silence for her; family voices at the visit |
| 55–61 | warm room tone, soft family voices from the next room, a plate set down, a match, tea glasses clinking, a glass on a saucer; silence under the final note |

Mix: music about −16 LUFS integrated for the film; keep the end clean so the real footage's own sound starts fresh.

---

## 15. Cost estimate (Higgsfield credits; verify with `estimate_video_cost` before each batch — prices change)

Prices used (from `OUR_STORY_HANDOFF.md` §10): Kling 4.0 1080p 3.25/s; Genjutsu lock ~7/s at 720p, ~20/s at 1080p; FLUX 3 start frame ~3; Nano Banana inpaint ~2. Totals include 2 versions of the key shots and the prep, **plus 30% for retries**.

| Chapter | Generated s | Locked s | All locks 720p + Topaz | Locks at 1080p as marked |
|---|---|---|---|---|
| 1 (the test) | 77 | 67 | ≈ 1,050 | ≈ 1,900 |
| 2 | 92 | 87 | ≈ 1,350 | ≈ 2,600 |
| 3 | 46 | 36 | ≈ 600 | ≈ 770 |
| 4 | 31 | 21 | ≈ 380 | ≈ 530 |
| 5 | 25 | 25 | ≈ 390 | ≈ 710 |
| 6 | 28 | 23 | ≈ 400 | ≈ 770 |
| **Film** | **≈ 300** | **≈ 260** | **≈ 4,200** | **≈ 7,300** |
Without retries: ≈ 3,200 (all 720p) / ≈ 5,600 (as marked). Music, sound effects and Topaz upscales are small extras.

**Recommendation to offer the user:** lock everything at 720p, upscale with Topaz, and re-lock at 1080p only the shots where a face looks soft after the upscale (usually the close-ups: T05, T06, T27, T50, T55, T57, T58). This should land near the lower column plus a few hundred credits.
The balance was **570 credits on 14 Nov 2026** (Ultra plan, 3,000/month). The user will very likely need more credits; say so with the numbers before starting.

---

## 16. QA checklist (in addition to `OUR_STORY_HANDOFF.md` §2.3)

Make a face sheet per take (reference crops next to start/middle/end face crops) and a full-frame strip. Look at it yourself before showing anything.
- [ ] **Action** in every 2 s; camera moves with real parallax; nothing looks like an animated photo.
- [ ] **First vs last frame SSIM < 0.90** for every 5 s take (never start = end image).
- [ ] **Her face** = the real face from the front and in profile (round face, full cheeks, thick brows, full lips); not thinner or "model-like".
- [ ] **His face** = him, slimmer, defined jaw, light stubble, real hairline; not heavier, no double chin.
- [ ] **Friend's face** (T01, T03, T04) = the friend's photo.
- [ ] **Outfits and hair** continuous inside each scene; her hair down except caps (graduation) and the low bun (chapter 6).
- [ ] **User-specific rules:** Seg 06 and Seg 57 eyes stay up, no hair tuck in Seg 06; Seg 07 no stop, look-back or nod; Seg 28 no hand over the mouth; Seg 38–39 and all couple shots no added touch; the prom gown stays as in her real photo.
- [ ] **Necklines** high and closed in every generated outfit (burgundy dress, summer dress, sweaters).
- [ ] **No text, numbers or dates** anywhere: screens soft, signs soft, no countdown, no clock, no plates; the real 6.01 sign unchanged; the 6.04 sign unchanged.
- [ ] **Families** at medium/wide distance; no family face changes noticeably; R-method takes do not read backwards.
- [ ] **Seg 59–60:** zero guest faces.
- [ ] **Split screens:** her left, him right, looking toward the divider, matched light.
- [ ] **Statue** (Seg 22) and the **escalator framing** (Seg 18–19 = Seg 48–49) are right.
- [ ] **Edit:** cuts, the one match cut, five chapter dissolves, the steam ending; words only as in §12.5.

---

## 17. Open items — ask the user these first (options, short)

1. **Music:** "Your own song (send it) / AI soft piano and strings (§14) / decide later."
2. **Credits and quality:** show the balance and §15; options "720p locks + upscale, re-lock close-ups (Recommended) / 1080p locks as marked / test chapter 1 first and decide."
3. **The friend's photo** (needed for T01, T03, T04) and, if they like, her outfit (default olive-green knit sweater and jeans).
4. **The real proposal footage** — needed only at the end, to match the colour and check the steam fade into it.
5. Remind them that T04 (and T39/T48) may each add up to 2 s; the film may end at about 2:04–2:06. They already agreed the film can run longer.

---

## 18. Manifest template (`manifest.txt`, one line per event)

```
date-time | take | step (A1/A2/A3/B1/B2/B3/N/E/edit) | model | input IDs (refs in order) | job ID | result file | duration | resolution | credits | status (ok/retry/rejected) | note
```
Example:
```
2026-12-01 10:12 | T05 | A1 | flux_3_image | H4, LOC-corridor | <job> | t05_a1.png | — | 2k | 3 | ok | face matches H4
2026-12-01 10:20 | T05 | A2 | kling4_0 i2v | start=<T05 A1 job> | <job> | t05_a2_v1.mp4 | 5.0 s | 1080p | 16.25 | ok | eyes stay up ✓
2026-12-01 10:48 | T05 | A3 | hf_mult_replace_object | src=<T05 A2 job>; H1–H7 | <job> | t05_lock.mp4 | 5.9 s | 1080p | ~100 | ok | profile ✓
```

---

*End of the scenario handoff. Everything the user decided is in this file; their exact words are in `SCENARIO_ANSWERS.md`.*
