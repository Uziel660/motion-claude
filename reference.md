# reference.md — learning from a film the user likes

"Make it like this." You cannot play the video: everything you know about it comes from numbers you measure and
pictures you extract and look at. Measure first, then look, and say which is which. Take the craft, never the
content.

## Get the film

- A file the user gives you: study it where it is (never move or edit their original).
- A link: ask before downloading anything (what, from where, how large). If it will not download or play, say so and
  ask for the file. Never describe a film you could not open.
- Stills or screenshots give palette, type and layout, not motion: ask whether a moving reference exists.
- Several references: give each one job ("type and palette from A, the pacing of B"), and do not mix looks just to use
  every reference.

## Measure

```bash
mo study ref.mp4                      # → study/ref/: study.md, study.json, contact sheets, shots/, cuts/
mo study ref.mp4 --at 3.2,7.5         # + 12 consecutive frames from each time: an entrance, a landing
mo study ref.mp4 --at 7.8 --span 3    # + 20 frames over 3 s: typing, a text stream, a pull-back (longer than 12 frames)
```

**Trust the file over the brief.** The study's first line is the real size, frame rate and length. A copy from a
social post is often 640×360: every size you read off it is in its pixels, so write the factor to your frame once
(640 → 1920 is ×3) and convert as you go. If the reference moves in steps (held frames, animating on twos), note its
real rate; render at it when the stepping is part of the look.

`study.md` gives: format; shots, with hard cuts, soft cuts (a subject swapped on the same ground) and transitions that
replace the frame; shot lengths and cuts a minute; moves between holds, their ease shape (ease-out, ease-in,
ease-in-out, steady) and, for a pan, how far the content travels; the share of time the picture holds; palette and
tone; whether it loops; loudness, tempo and how many cuts and move starts sit on a beat.

A motion-graphics film often changes scene without replacing the frame (new type on the same ground): there are no cuts
to find, so read its rhythm from the moves and the sheet. Tempo from a listen is a guess; the measured one is the
number (a model "hearing" 120 BPM in a 128 BPM track is common).

## Look, in this order

1. **The sheets**: the whole film at once. What changes from tile to tile: type, layout, camera, colour?
2. **`shots/`** at 960 wide: the type (family class, weight, width, case, size against the frame height), margins,
   alignment, the grid. The frame that stands for a shot is its last before the cut, not the one you like best.
3. **`cuts/`**: how each cut or wipe works, frame by frame. "A square wipe" seen at sheet speed is often eight bars
   falling in turn, each with a bounce.
4. **`--at` strips** around the moments the brief cares about: what enters, in what order (product, then headline
   +0.1 s, then label +0.25 s), how far it travels, whether it overshoots, how long it holds before the next thing.
5. **Inside each shot**: what keeps moving while the shot "holds" (a glint, a drift, a counter). Missing this is how a
   remake becomes still pictures with transitions between them.

## Name its grammar before its timings

Say which kind of film it is from the strips, because the kind decides what to copy first:

- **Tweened**: things travel and ease. Copy curves, distances and stagger.
- **Stepped**: things appear, swap or jump on held frames. Copy the step rate and what changes per step; easing it
  would lose the look.
- **Camera-led**: one ground, a crop that pulls back, pans or pushes in. Copy the framing at each stop and the move
  between.
- **Interface film**: a product used on screen. Its grammar is a list to check, not a feeling: scenes joined by a
  short dissolve (0.15–0.2 s; a fade out then in leaves a blank), a "working" state after a send, text that streams in
  and speeds up, a cropped view that pulls back to the whole, a click only after an edit ends, the same words before
  and after sending, an end dot or wordmark.

The study reads typing, streaming text and a scroll as moves or soft shots. Look at each one on a `--span` strip
before you copy it as a move.

## The event timeline, and how its times map onto yours

List what happens, in order, each with its time and how you know it:

```text
 0.00  title words appear 0.19 s apart, a dot rides the last word                [measured: at-0.20s]
 4.10  request typed, 31 characters in 1.6 s                                     [measured: at-4.00s --span 3]
 7.80  answer streams in, box widens 565 → 613 px, speeding up                   [measured]
16.50  panel shown cropped, pulls back to the whole in about 1 s, ease-in-out      [measured]
22.30  hard cut to the thread                                                    [estimated: sheet-1]
```

If your film is a different length, decide once which you keep: **the shares** (every event at reference time × your
length ÷ its length; `mo study --pair` prints the factor) or **the absolute timings** of single actions (a 0.45 s
collapse stays 0.45 s). Usually both: events sit at their share, and each action keeps its own duration. Write the
choice down; without it the frames of the two films will not line up and nothing can be compared.

## Count what "busy" and "big" mean

Words like "small labels" and "large dots" drift when you build. Count on the frames:

- how many marks, labels or blocks are on screen in each scene, and how many change a second;
- the size of the main mark, word or dot as a share of the frame height;
- how much of the frame the largest element covers.

Keep the size and the count; change what a mark stands for if your numbers are larger ("one dot = 20 people", said on
screen). 60 large discs redrawn as 1,000 small dots are faithful to the data and lose the film.

## What will not transfer, decided before you build

- **Photos, footage, drawings with real texture** (an engraving, a photographed object, people's avatars): you cannot
  use the reference's, and a thin outline drawn in SVG does not stand in for a shaded drawing. Decide the substitute
  now: the user's own pictures, a licensed or public-domain source, a generated picture if the user agrees, or the
  material built in code (shading, grain, a torn edge, brush texture, a lit 3D object: these can be built, and are
  tried in full before anything simpler). A simpler device is the last choice and is honest about being simpler.
  Say which in `reference.md`.
- **The reference's product**: its interface, its chrome, its control names. A remake shows the user's own product.
  Renaming the reference's composer bar is copying its interface.
- **Its signature**: the one picture people would recognise the film by (four letters gathering into a square, a logo
  built a particular way). Take the idea's job ("the name assembles at the end") and design your own picture for it.
- **Its sound**: take the tempo, the loudness shape and where the hits fall, never the recording.

## Write it down: `reference.md` in the film's folder

One line per finding, each labelled:

```text
Source: ref.mp4, 1920×1080, 30 fps, 22.4 s, with sound.
Shots      14, median 1.4 s, 38 a minute; 9 of 13 cuts within 0.07 s of a beat (122 BPM).           [measured]
Entrance   3.20–3.70 s: card from y+60, opacity 0→1, scale 0.96→1.0, a slight overshoot.           [measured: at-3.20s]
Order      product → headline (+0.10 s) → label (+0.25 s).                                           [measured]
Hold       readable 3.85–6.10 s before the next move pulls the eye.                                  [measured]
Type       a grotesk, heavy, all caps, cap height about 1/9 of the frame.                            [estimated: shots/004]
Our film   our report screen enters the same way and holds 2.2 s.                                    [creative choice]
```

Measured is what `mo study` or a frame shows; estimated is what you judge from a picture (name the frame that would
settle it); a creative choice is yours. Then turn it into rules for this film, one line each.

## Take the craft, never the content

| Take (match it closely) | Never take |
|---|---|
| Palette relations: ground, ink, accent, contrast, saturation | Its logos, brand names, characters, mascots |
| Type feel: class, weight, width, case, tracking, scale | Its words, claims, numbers |
| Layout, margins, where the eye goes | Its footage, photos, drawings, 3D models |
| Motion: curves, durations, stagger, overshoot | Its music, voice or sound effects |
| Pacing, cut rhythm, transitions, camera language | Its frames, in the film or anywhere you deliver |
| Texture and finish: grain, blur, glow, animating on twos | |
| Sound energy: tempo, density of hits, loudness shape | |

When the film is for a made-up product or uses example numbers, `mo audit` needs them marked from the start: in
`sources.md` the row's source says "sample company detail" (or app, shop, event), and the film shows a "Sample data"
label a viewer can read on a phone for as long as those numbers are on screen. A number on screen is a claim;
unmarked, the audit refuses it.

Map the palette by lightness and saturation as well as by role: an accent much darker or greyer than the reference's
changes the film even when it sits in the same place.

With the user's own brand, map the reference's roles onto it (its accent becomes their accent) unless they ask for the
reference's palette. The reference is studied, never shipped: the `study/` folder stays out of what you deliver.

## Check yours against it

```bash
mo study film --pair ref.mp4 --draft  # one picture: reference left, your page right, at the same shares of each length
mo study film --pair ref.mp4          # the same from your latest render
mo study film --compare ref.mp4       # your latest render and the reference, side by side in numbers
```

**The pair picture is the main check, and it starts before the first line of code.** First look at
the reference's own frames at the shares you will compare (one for every part of its timeline, and one for the moment
it turns on) and design your frame for each of those moments.
Then, after every round of fixes, `--pair --draft` (no render) and compare row by row: the scale of the main element,
how busy the frame is, where the eye goes, how far along the action is. With `--pair`, `--at` takes shares of the
length (0.08,0.36,0.9), not seconds; give enough that every part of the film gets a row. The numbers can agree while
the frames do not.

**Follow the system, compose the frames.** A film whose blocks cover the reference's blocks one for one is a tracing
with the colours changed. Keep the grid, the margins, the main element's size, the count of things on screen and the
kinds of element; decide yourself where each one sits. Lay one of your frames over the reference's at the same share:
if they coincide, recompose.

**When the house checks disagree with the reference, the reference wins, and you say so.** `mo qa` may call a pause the
reference holds on purpose "blank"; the rhythm method snaps scenes to the beat where the reference cuts off it (count
its cuts on a beat: 20 % is a target, not a fault); `mo sound` may call a flat contour flat when the reference's is
flat. Keep what the reference measurably does, and write it in `reference.md` as a creative choice with the number
beside it. A check that fails for any other reason is still a fault.

**Ease shares** come from how things move, not from the easing name: many small staggered reveals read as steady.
To match a reference that is mostly ease-out, move whole figures (scale, translate) and let them settle.

**Sound, when you cannot listen:** compare the loudness curve in two-second steps, the tempo and where the loudest
moment falls against the picture. Say plainly that nobody listened.

Shot length, cuts a minute, the share of time holding, ease shapes, tone, palette, loudness, tempo and cuts on the beat,
in two columns. A difference you meant is a creative choice; one you did not is the next fix. Then look at the same
moments of both, frame for frame.
