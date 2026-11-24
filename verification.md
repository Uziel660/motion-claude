# Verification and rework

Machines answer what can be measured: does the file decode completely, is the frame count right, are the length
and frame size right, does seeking to the same time give the same frame, are fonts or files missing. Frame checks
cover the key text, the caption area and the landing points of motion; where no automatic detector exists, name the
time windows you checked by hand and do not claim everything was checked.

An independent reviewer gets only: the original request, the final MP4, the chosen direction, the rhythm sheet
(`treatment.md`), the sources table for on-screen text (`sources.md`: which screenshot or page each caption or
UI string came from) and the facts that must be verified. It does not read the maker's explanations first. Without
the sources table, a reviewer mistakes the official site's own sentences for "invented copy". The review must ask
"where does attention start to drift, where does it go flat?" — a review that only checks right and wrong misses
boredom, which is what users reject most often. The report names timecodes, the defect, its severity, how much was
watched and the limits, and is tied to the final file's SHA. Tell apart: not explained, logic error, unreadable
text, rough craft, rhythm flat or out of control, unmotivated camera, technical fault. Check still-frame craft and
continuous motion separately (visual-direction.md): which detail does not hold up close, which stretch does not
move the information forward.

Review is not about chasing one high score. Fix what blocks understanding and use, then verify the original defect
and the seams next to it. A trade-off the user accepted is not reopened without new evidence; when the user says
stop, finish as asked and state the limits of what was verified.

The chosen version keeps its code, timeline, asset references, sound and the identity of the render. Rework starts
from the version actually delivered last and accounts for the patches of earlier rounds. After an export, check that
the target window changed as intended and that nothing else changed by accident; treat encoding differences and
content differences separately.

Checking only screenshots cannot claim the motion was reviewed; running only audio metrics cannot claim a listening
review; converting only a spec cannot claim a new subject's film passed. Confirm a test tool catches a deliberately
broken input, so "all green" does not come from a check that never ran.

Record engineering acceptance and creative acceptance separately. Frame-exact matches prove only the edit's
boundary or determinism, and the number of tests only says which counter-examples are covered; neither proves it
looks good. A sample the user explicitly rejected becomes a technical regression case, with the rejected dimension
noted. After changing a skill, only an independent agent making a real film on an unfamiliar subject counts as a
transfer test; the author simulating two answers in the same context does not.

## Working economically

A film costs the user minutes and tokens; spend them where they change the film. Measured on six example films,
most of both went to full renders after every small fix and to looking at many full-size frames.

- **Between fixes, look without rendering.** `mo check`, then `mo still film --sheet` (the whole film as one small
  image, a frame a second, in seconds) or `mo still film --at <the times the fix touched>`. A full `mo render` is for
  a review round and for delivery, not for each fix. A narration change is heard with `mo voice --check`; the cues
  come from the voice, so its timing needs no render either.
- **Look small first.** Judge layout, rhythm and continuity on the sheet. Open a full-size frame only where you must
  read text or a number or check an edge, and each such frame once.
- **Read each file once.** Do not reread a reference, a source or a script already read in this session; note what
  you need from it the first time.

## Before delivery: a review by someone who did not make it

The agent that made a film is the worst judge of it: it sees what it meant, not the frames. So before delivering:

1. `mo render film`, then `mo review film`. It writes `film/review/`: the film as delivered (and its sha256), contact
   sheets two frames a second, a frame after each scene starts and the last, what whisper hears with times, the
   loudness every second, `mo qa`'s measurements, the request, plan and `sources.md`, and `brief.md` — the reviewer's
   instructions: the six criteria (clear to a stranger, only about this subject, rhythm, craft up close, sound with
   picture, truth), findings as JSON with severity (blocking, major, minor) and timecodes. What lives outside the
   film's folder goes in with `--add <file>` (repeatable): always the user's request in their words, and the material
   the film quotes or shows (a spec, reviews, a data file, a session); `mo review` warns when the kit has no request.
2. Give that folder, and nothing else, to a fresh agent: "Read brief.md in <folder> and do what it says." In Claude
   Code, the Agent tool with a new general-purpose agent — never a fork, which inherits this session and its bias; in
   Codex, `codex exec --sandbox read-only` from that folder. A reviewer of another model family than the maker sees
   other things; say which model reviewed. With no way to start a fresh agent, say so and hand the folder to the user.
3. Fix every blocking and major finding (do not argue one away; when a finding is wrong, say why in the delivery
   note). **One review round.** Check the fixes yourself with `mo still --sheet` and `--at` the times they touched,
   then render once for delivery. A second round, with `mo review` again and a new reviewer, only when the first
   found a blocking problem (a false claim, something unreadable, a broken frame), to see that its fix worked; or
   when the user asks for more. Three at most. (Measured on a launch film: the first round found most of what three
   rounds found, and the second and third roughly doubled the film's tokens.)
4. **The delivery note is part of the film's truth.** It is written for the user, in their words: what was made,
   what was changed from the request and why (first, when it matters; of several changes, the one that changes what
   the viewer sees or believes comes first, in its own sentence), what they must check or decide. Every figure
   in it — length, words, words a minute, loudness — is one you measured on the delivered file (a count of words or
   pages is counted by a script, never estimated; every file you name — `review.md`, a caption file — is delivered),
   and a check you did not make is not claimed ("whisper heard every line" only if the transcript of this render matches the script word for word, names and
   any stray syllable included; otherwise say which words it heard differently). A claim about a whole source ("the book never names Newton",
   "nowhere in the report") is made only of what you read: "not on the pages I had". A claim that a source does not say something ("does not
   mention any rules", "gives no cause") is searched for in the whole text first (its notes and footnotes too) and
   worded as narrowly as the search: "gives no cause for the rise" when it names the directive elsewhere. No tool names or skill
   rules: say what is true of the film, not how it was made; one line says it was reviewed (item 6).
5. **The floor:** never deliver with a blocking finding open — a wrong number, name, date or quotation, a claim the
   sources do not support, something unreadable. If it cannot be fixed, it goes to the user as the first line of the
   delivery note.
6. Beside the film, `review.md`: who reviewed (the model), the scores, what was found and what changed, and anything
   left as it was and why. The delivery note says it in one line, in these words, filled in truly: "Reviewed by N
   fresh agent(s) (<model>); the final render was / was not reviewed again; what was left as it was is in
   review.md." Nothing stronger ("every finding fixed", "independent") unless it is exactly so.
7. A word about quality in the note — "loops cleanly", "seamless", "slow", "readable on a phone" — is a claim like a
   number: make it only when you measured it on the delivered file (the level either side of a loop seam, the pace
   page by page, the type size), and say what you measured.

8. **What was checked, in three words.** The delivery note ends with the checks, each marked **pass**, **fail** or
   **not run**; a check that was not run is written "not run", never left out and never worded around ("should be
   fine", "looks good"):

   | Check | How |
   |---|---|
   | The page and its rules | `mo check`: 0 errors |
   | Every line and number has a source | `mo audit` |
   | The rendered file | `mo qa` on the file delivered |
   | Frames looked at | the sheet and the stills you opened, from the delivered render |
   | Reviewed by someone who did not make it | item 2; "not run" when no fresh agent could be started |
   | Heard by a person | you cannot listen: "not run" unless the user did |
   | Watched at normal speed by a person | "not run" unless the user did |

   A film is **a draft** until it is rendered, **rendered** until `mo qa` passes on that file, **checked** when the
   rows above that you can run are pass, and **reviewed** when item 2 was done on the delivered render. Say which.

## A second request on a finished film

When the user comes back to a film that exists, do the size of work they asked for, not the whole workflow again.
Say in one line which of these it is before starting:

| They ask for | Do | Run again |
|---|---|---|
| A change at one place or time ("the title larger", "hold the end longer") | the smallest edit there (`mo set key=value` when a variable covers it) | `mo check`, the still at that moment, one render, `mo qa` |
| Other words or numbers | the edit, and `sources.md` for anything new | `mo audit`, then as above |
| Sound only (other music, quieter, a hit moved) | the score or the cue; the picture is not touched | `mo sound`, one render, `mo qa` |
| Another size, place or format | a version of its own (below: A version for another place); `mo render --format` for a file type | the checks on the new project or file only |
| The file again, nothing changed | point to the latest render, or render once | nothing else |
| An opinion ("is this good?", "review it") | look and report; change nothing | `mo review` when they want a second pair of eyes |
| Another film from the same material | a new project folder and the workflow from its start | everything |

A change to the story, the look or the structure is a new direction: go back to the step that decides it, and say so.
Keep what the user already approved: an edit to scene 3 does not restyle scene 1. The delivery note covers what
changed and the checks you ran this time.

## A version for another place

A film made for one place is not finished for another by cropping it. When the user asks for one ("a vertical one for
Reels", "a short one for 小红书"), or names in the brief more than one place it will be posted, make each version its
own project and leave the first film as it is.

| For | Frame to start from | What changes besides the frame |
|---|---|---|
| TikTok, Reels, Shorts, 抖音, 视频号 | 9:16, 1080 × 1920 | everything read inside y 250–1450 and clear of the right-hand 130 px (the app's buttons and caption cover the rest); the point said in the first two seconds (the proof still lands on the music's strongest moment); captions on, since many watch muted (a film whose words are already on screen has them) |
| 小红书 | 3:4 or 9:16 | as above; the first frame also serves as the cover, so it carries the title |
| X, LinkedIn feed | 16:9 or 1:1 | plays muted at first: the point readable without sound; 1:1 takes more of a phone's feed |
| YouTube, Bilibili, a site, a deck | 16:9, 1920 × 1080 | nothing by default |

These are starting points for the edit, not the platforms' upload rules: lengths and limits change, so check the
platform's own page when a limit matters, and never state one from memory.

1. `mo fork <film> <film>-<place> --size <w>x<h>` copies the project into the new frame and leaves the re-layout as a
   comment in the new project's inbox. The first project and its renders are not touched.
2. Lay it out again for that frame: the subject as large as the frame allows, text sizes checked again (what was
   32 px on a wide frame is rarely enough on a tall one), nothing important in the bands above. A wide chart or
   screen is cut to its point or stacked, not shrunk to fit.
3. **A shorter version** keeps whole beats: the hook, the one strongest proof, the end. Cut on the music's bars and
   score it again for the new length (`mo sound`); never speed the film up, and never fade out mid-phrase. Narration
   is cut at sentences and timed again (`mo voice`).
4. Run the checks on the new project only (`mo check`, `mo audit` when words changed, stills of every scene, one
   render, `mo qa`), and say in the delivery note which version is which and what was left out.

Offer it once, at the end of a delivery, only when the brief named more than one place or the film's shape does not
fit the place the user named: one line, not a list of platforms.


After latent-variable/shipshow's critic loop (MIT: a fresh critic per round, never the builder; findings by severity;
a floor no cap lowers) and Vincentwei1021/mg-styles-15's review prompt (MIT: frames and measurements first, fixes in
order of impact).
