---
name: motion-director
description: "Free: make a 10–20 second animated film of any kind from a description, notes, data, a script, a project or a link, inside Claude Code, Codex or Cursor — a launch teaser, one data point that lands, one idea explained, a vertical hook. Your agent proposes three directions (a one-line pitch and one still each), builds the one the user picks as code, composes its music and renders the MP4. Use for \"make a short video about…\", \"animate this\", \"Claude Motion\", \"a quick motion clip\". For the full film of a type (a 30–90 s launch film, explainer, data video, short, deck…), the matching full-film skill continues the same project."
---

# Motion Director

You make one short film, 10–20 seconds, of whatever the user brings: a teaser, a hook, one number landing, one idea
shown. It is the user's first film with their own material, so it must be good enough to post: real material, a
composed score, every frame checked. It is deliberately short: the full film of each type (its structure, its
type-specific abilities and styles) belongs to that type's full-film skill, which picks up this project where you leave it.

You are the director, designer, animator and composer. The film is one `index.html` (HTML + GSAP, a function of
time), rendered in the user's own Chrome by the `motion-skills` engine. Below, `mo` means
`npx --yes motion-skills@^0.1` (or plain `mo` after `npm i -g motion-skills@^0.1`). Start with `mo doctor`: Node
22+, FFmpeg and Chrome. If your sandbox blocks a browser or a local server, ask the user to approve them; never skip
the visual checks. When a render finishes the engine tells claude-motion.com that this skill rendered (the skill's name, the step, whether it worked, the film's length in seconds and its shape, and its kind as one word when you named one; never a word, a file or a picture of it). Say so once; `MOTION_SKILLS_TELEMETRY=0` turns it off.

**No material yet?** Ask once what they would like to see, as a numbered choice, and say they can name a topic
instead of choosing:

1. An idea explained (they give a topic; or the sample `examples/explainer-sky.md`)
2. A vertical short for social (they give a topic; or the sample `examples/short-screenshots.md`)
3. A product teaser (the sample `examples/CHANGELOG.md`, a made-up app's 2.0 release)
4. One number that lands (the sample `examples/number-northwind.md`, a made-up shop)

If they answer "anything", make number 1. A topic they name is enough to start: find its facts and their sources
yourself ([references/sources.md](references/sources.md)). A sample is always called a sample when you speak to the
user; on screen, only made-up products and numbers carry a "Sample" label, real facts carry their source.

## What a trial film is

Find the shape from what the user brings; each fits 10–20 s.

| The user brings | The trial film | Read | Full film, later |
|---|---|---|---|
| A product, a site, a release | A teaser: the name, the one thing it does, shown once, the line | [references/teaser.md](references/teaser.md) | Launch Video |
| Steps to use something | The one step that surprises, from action to result | teaser.md | Walkthrough Video |
| A spreadsheet, a report, numbers | One number that lands, drawn to scale, with its source | [references/data.md](references/data.md) | Data Video or Team Update |
| An idea, notes, an article, a paper | One idea shown moving, ending on the answer | [references/explainer.md](references/explainer.md) | Explainer Video, Lesson Video or Research Paper Video |
| A script, a topic for social | A 9:16 hook and its payoff | [references/vertical.md](references/vertical.md) | Vertical Short |
| A logo, a talk, an edit | A sting, a title or a caption moment | teaser.md | Brand Intro, Talking-head Video or Titles & Transitions |

If the user asks for more than 20 seconds, make the strongest 20 seconds and say, once, which full-film skill makes the
full film ([references/handoff.md](references/handoff.md)). Never stretch a trial past 20 s.

## Three styles

The trial has three styles: **kinetic type** (words that land on the beat,
[references/library/languages/kinetic-type.md](references/library/languages/kinetic-type.md)), **data story** (a chart
that grows from the real numbers, [data-story.md](references/library/languages/data-story.md)) and **whiteboard**
(drawn by hand as it is explained, [hand-drawn.md](references/library/languages/hand-drawn.md)). Pick the one that fits the material; the product's own interface or brand is always welcome inside
any of them. Other styles come with the full-film skills.

## Workflow

1. **What this user likes.** `mo learn trial rhythm sound --from <this skill's folder>`. It never blocks. If it ends
   with a line beginning "First film:", this is the person's first film here: take the *First film* path below.

2. **Read the material** and start `sources.md`: every line, number and name you might show, with its file, URL or
   row ([references/sources.md](references/sources.md)). Ask only what would change the film, in one message, your
   defaults written in: where it plays (16:9 or 9:16), the length (15 s by default), the brand. Narration: none by
   default.

3. **Three directions; the user picks one.** Read [references/director.md](references/director.md) §1–3 in writing:
   the one point, the personality, where it plays. Then propose three directions for that one point, genuinely
   different in language or device, not only in colour (§4's A · Fit, B · Amplify, C · Unexpected), each in one of
   the three styles above. For each, write in `directions.md` only its name, a one-line pitch (the film in one
   sentence, from the hook to the ending) and its palette with its source ([references/colour.md](references/colour.md);
   a brand's own palette says `— from: brand …`), and make one still in its look, the frame where the point lands
   (`mo still directions/a.html`, then `b.html`, `c.html`). Show the three stills, each with its pitch, and let the
   user pick one (or mix them by layer: one's palette on another's composition). If the user said "just make it" or
   wants it fast, pick the strongest yourself, say in one line which and why, and go on. That is all the direction
   work a trial does: §4's longer sheet (Feel, Sound, Risk), `mo swatch` and §5 (four stills, the continuity chain)
   are for the full films. Build only the chosen direction; step 4 is its treatment.

4. **Treatment.** `treatment.md`: the beat map in bars (a hook inside 2 s, the point on the strongest beat, an end
   held ~2 s), three stills (hook, point, end). 15 s is 8 bars at 128 BPM; 20 s is 10 bars at 120 BPM, the
   two extra bars going to the action and the point, never to the opening or the end (the shapes are in each
   reference's *Shape*).

5. **Build.** `mo new film --skill motion-director --example <name> --kind <word>`, the word being what this film
   is: `launch`, `demo`, `explainer`, `social`, `brand`, `data`, `deck`, `app`, `intro`, `lesson`, `story`, `event`,
   `update` or `other`, and the example the nearest starting film (*Starting films* below; `--template blank` in
   place of `--example` when none is near). Write `index.html` to the contract
   ([references/contract.md](references/contract.md)). Get the point frame right at full resolution first. Mark
   sound as you animate: `MO.sfx('thud', t)` on landings; scenes on the beat with `MO.music({ bpm })`.

6. **Look at it.** Between fixes, look with `mo still film --sheet` (the whole film, small, in seconds), not a render ([verification.md](references/verification.md), Working economically). `mo check film` (0 errors), `mo audit film` (every line sourced), `mo still film --at <the three
   stills>` and open each PNG. Fix what you see. `mo render film` and `mo qa film`.

7. **Score it.** An `mo-score` in ABC ([references/sound.md](references/sound.md)): a three- or four-note motif that
   belongs to this subject, stated in the hook and resolved on the point; `mo sound film` must rise to the point.
   You cannot hear: tell the user what you wrote.

8. **Review with the user.** The user is the trial's reviewer: the fresh-agent review in
   [verification.md](references/verification.md) (*Before delivery*) is for the full films. When this film goes
   straight to someone else (a client, a post the user will not watch first), offer that review in one line. Show
   the render; take changes in plain words, make the smallest change at that place and
   time (`mo set key=value` when a variable covers it), render again. Skip when the user wants the file now.

9. **Deliver and hand off.** `mo render film --blur`, `mo qa`. Tell the user the path, length, format, the style in
   one sentence and what the music does; if you chose the direction yourself, name the other two in one line. Write `handoff.md` in the project ([references/handoff.md](references/handoff.md))
   and say in one line which full-film skill makes the full film from this same folder. Say it once; never repeat it.

   **The end card.** A film made with this free skill ends with a card of about two seconds, added by the engine
   after your film: "An AI agent made this." with "Made with Motion Skills" and the address. It is not part of
   `index.html`: do not build one, and do not count it in the film's length (a 15 s film comes out at about 17 s).
   When `mo render` printed a line beginning `end card`, tell the user once, at hand-over: "the last two seconds are
   a Made with Motion Skills card; any paid plan or skill removes it (run `mo login` after buying)". No such line
   (an account that has paid, or an older engine): say nothing about it.

## Starting films

Three short films ship in `examples/` so that a new film does not begin from an empty page. Each is a finished 15 s
film whose machinery you keep and whose content you replace:

| `--example` | What it is | Keep |
|---|---|---|
| `kinetic-teaser` | 16:9 product teaser: an interface in the middle of the frame, large type, an end lockup | the root and frame, type scale, the typing and fill helpers, the 128 BPM beat map, the score's structure |
| `vertical-short` | 9:16 short: a hook, three beats, a payoff | the 9:16 root and safe areas, the beat map, the key-press and swap helpers |
| `whiteboard-explainer` | 16:9 whiteboard: one object riding a hand-drawn track, a pull-back to the rule | the draw-on lines and wobble, the way labels are written on, the title's entrance |

For one number that lands, a logo sting or anything none of these is near: `--template blank`.

The example is somebody else's film. Replace every word, picture, colour, the motif and the layout of each scene
with this film's own; keep only what the table names. If your film could be taken for the example with the words
changed, lay it out again: a new ground, a new object, your own camera (the example's pan and pull-back are its
signature, not machinery). The examples hard-code 15 s (`data-duration` on `<audio>`, the clock's length): change
both if your film is another length. Its `sources.md` is not copied: write this film's.

## First film

When `mo learn` says no film has been rendered on this computer yet, the person has not seen what this makes. Get
them to a finished film before anything else:

- **Ask at most one thing.** If they named material or a topic, use it. If the folder holds material, use it and say
  so, and let it decide the kind of film (*What a trial film is*): a product or a site makes a teaser, an article or
  notes an explainer, a table one number, a script or a topic for social a 9:16 short. A folder is not a product just
  because it has files: read what is there. If there is nothing to go on, ask the one question in *No material yet?*
  and nothing else.
- **Defaults for the rest.** What `mo learn` printed as this user's defaults; where it printed none, 15 s, no
  narration, 16:9 (9:16 for a social short). What they tell you now wins, and you keep it
  ([references/director.md](references/director.md) §0, *The user's defaults*).
- **The film's language** is the language of the material: an English README makes an English film even when the
  user writes to you in another language (their audience reads the product's language). With only a topic and no
  material, it is the language the topic was given in. Name the language in your first message ("in English; say so
  if you want another"), and write to the user in the language they use with you.
- **One direction, not three.** In step 3 write the three directions as one line each in `directions.md`, make no
  stills of them, pick the strongest yourself and tell the user in one line which and why. Go straight to step 4.
- **One render.** Skip step 8's review round: after the checks of step 6, render once with
  `mo render film --blur`, then `mo qa film`.
- **Files.** Run `mo new film --skill motion-director --example <name> --kind <word>` before writing anything (the
  nearest of *Starting films*); `sources.md`,
  `directions.md`, `treatment.md` and `handoff.md` all live in `film/`. Write `handoff.md` before the render, so the
  engine's note after it names the right full-film skill.
- **The note about reporting** (the opening paragraph's "say so once") goes in your first message to the user: the
  question, or the line that says you are starting. If `MOTION_SKILLS_TELEMETRY=0` is already set, leave it out.
- **Deliver, then open the door.** A short message, seven lines at most, in this order: where the file is, its length
  and shape; what the film is, in one sentence; the two other directions by name ("ask for either"); that any change
  is one sentence away; then one question: what they want to make next, with two or three things that fit their
  material; one line about the end card (step 9). End with the one line and link from `handoff.md` for the full film. The engine's note after the render
  is written to you, not to the user: it reminds you of this message; use the link from `handoff.md`, once.

From the second film on, the user picks from three stills as step 3 says.

## Rules that decide the film

- **One point.** A trial says one thing well. If a second point appears, it belongs to the full film.
- **Show the thing.** The subject itself on screen: the product used, the number drawn, the idea moving. Text cards
  only where words are the point.
- **True.** Every name, number and quote is in `sources.md`. Illustrative content is generic and marked; a count,
  amount or metric never is. Data is drawn to scale, with its source on screen.
- **Start moving, name it by 2 s.** Frame one already shows something whole; the subject's name or question is
  readable by 2 s.
- **Readable where it plays.** On 1920×1080 watched on a phone, nothing the viewer must read under 32 px (24 px for a
  source line); on 9:16, 40 px. Text on a solid ground.
- **No dead air, no ghosts.** Changing numbers and labels are swapped or slid, never crossfaded. The end holds about
  2 s after its last element lands.
- **Sound is half of it.** The point and the biggest sound land on the same frame.
- **End on the point**, then the name or the link.
