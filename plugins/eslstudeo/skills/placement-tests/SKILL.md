---
name: placement-tests
description: Builds and delivers ESLStudeo placement tests through the ESLStudeo connector — replicating a paper test (photos or a document) by proposing the settings that reproduce it for the teacher's approval, or designing a new test with them from the rules that keep a level trustworthy; publishing it; creating one single-use link per candidate for people taking it remotely, each batch with its own time limit, listening plays and support language, and an email draft per candidate in the teacher's own email; and reading the results and recording the level the teacher decides. Use this skill when the person asks about a placement test, a level test, a level check, a diagnostic or placing new students in ESLStudeo, for example "turn these photos of our paper test into a placement test", "make a placement test for adults from A1 to B2", "send the placement test to these twenty people", "who has finished the placement test?" or "place Sara at Intermediate".
---

# Placement tests in ESLStudeo

A placement test answers one question: what level is this person, on evidence. It is not an
achievement test. A question is good if it separates two levels, and useless if everybody gets it
right, however well it is written.

Before anything else:
- `what_can_this_builder_do` with part "placement": the exact format of parts, questions, score rules,
  levels and settings, and the evidence rules the engine applies.
- `design_approaches` with approach "placement-and-diagnostics": how to work with the teacher, and the
  measurement principles behind the rules below.

## Who may do what

- Building a test needs the course permissions. Links, sittings and results carry candidates' personal
  information, so they need the classes switch (**Also let it into your classes**) on the ESLStudeo
  approval page; if `create_placement_links` is missing, follow the connect-eslstudeo skill.
- In a school, owners and administrators build and decide; a teacher does so only when made a proctor
  on ESLStudeo's Placement screen. An independent teacher does everything on their own tests.
- A test bought from the marketplace keeps its questions, levels and score rules locked, because its
  levels are tuned to exactly those questions. Its name, settings and delivery are the buyer's.

## Which kind of request is this?

- **"Put our test online"** — the teacher has a paper test that works and wants the same test on the
  platform. Keep it simple: follow "Replicate a paper test" below. Do not walk them through the
  engine's options; work out the settings that reproduce their test and put them up for approval.
- **"Make us a placement test"** — there is no paper test, or the teacher wants a new one. Follow
  "Design a new test" below, and show them what the engine can do so they can choose.

## Replicate a paper test (photos or a document)

1. Say briefly what the online test will do — two or three sentences, not a tour: each candidate opens
   their own link on a phone or a computer; ESLStudeo asks the questions in the paper's order, marks
   them, and reads the score against the chart; the teacher sees every result with the level the
   questions suggest, and confirms it.
2. Read every page. Transcribe the questions and their order faithfully; do not improve them silently.
3. Ask only what the paper does not tell you: the answer key (never guess one), the score chart —
   which levels, at what scores — and the names of the levels. If the paper test has no chart, say that
   the cut-offs will have to be set and checked, rather than inventing them as if they were known.
4. Work out the settings that reproduce the paper test, and put them to the teacher as a short list to
   approve:
   - every part in the paper's order, every question kept, nothing drawn at random;
   - one chart at the end, read on the running total of the whole test (`gateBasis` "cumulative"); each
     earlier part simply sends the candidate on;
   - the paper's time limit, or untimed;
   - the plays the listening instructions allow (two unless the paper says otherwise);
   - a support language only if the paper's own instructions have one;
   - the spoken interview and the writing task only if the paper has them;
   - adaptive off and the confirmation questions off, so a candidate answers exactly the paper's
     questions;
   - candidates do not see their level: each result waits for the teacher's decision;
   - links last seven days, and each works once.

   Add one line: any of this can be changed later, and one batch of links can be sent out with its own
   time limit, plays and support language without changing the test.
5. Turn the chart into score rules. A rule places a candidate at or below a percentage, so convert each
   cut-off to a percentage of the test's total points, and set the value half a point above the band's
   top score, so that no whole score lands on the wrong side: a level whose top score is 15 out of 60
   becomes `upTo` (15 + 0.5) ÷ 60 × 100 = 25.8. The last rule must be 100. Check first that the online
   total matches the paper's total: `read_placement_test` gives `totalPoints` and the points of each
   part, and a matching question scores one point per pair, a gap-fill one point per gap.
6. Tag every question with its CEFR band (`cefr`), from its own difficulty — how frequent its words are
   and how complex its structure — and map each level to a band (`levelCefr`), so ESLStudeo can report
   what a candidate can do and can flag a result its own evidence disagrees with (see "What the engine
   adds to the chart"). Say which tags you are unsure of. If the teacher's levels do not correspond to
   CEFR bands, leave the mapping out: the chart alone then decides.
7. Build it: `create_placement_test`, then `set_placement_levels` (levels lowest first), then one
   `set_placement_section` per part, then `read_placement_test` to see the problems left, then
   `publish_placement_test`.
8. Keep the review light. Say plainly when something cannot work — a key that contradicts its question,
   two right options, a missing picture or recording, a level whose band has fewer than six questions —
   and ask what to do about it. Do not redesign their test, or list what you would have done
   differently, unless they ask.
9. Pictures and recordings from the paper come in through `upload_placement_media` — see "Pictures and
   recordings" below.

## Design a new test

Decide five things with the person before writing a question:
1. **Floor and ceiling**, from who takes the test, not from ambition: a group of beginners needs
   Pre-A1 and A1 questions and nothing much above B1; an adult intake may run to C1. Without a floor the
   test cannot tell "A1" from "cannot yet read".
2. **The bands to report, and at least six questions for each.** Below six, a level is not reliable
   enough to act on; the engine itself refuses to trust a band with less evidence. Roughly ten per band
   is comfortable.
3. **A band tag on every question**, by its own difficulty.
4. **Rising difficulty**: parts rise, and questions rise inside each part. Tell the candidate in the
   instructions that the later parts are meant to be hard, so they keep going.
5. **What the test does not measure**, stated in "About this test" (`update_placement_test`). A test
   taken at home cannot guarantee a recording plays; a spoken answer is collected, never scored.

Show them what the engine can do, in plain words, and say what you would choose: parts in a fixed
order, or adaptive questions chosen as the candidate answers; extra questions at the deciding level
when the evidence is thin; a time limit, and how many times a recording may be played; a first
language beside the instructions; read-aloud for young children; a spoken interview, or a written
task after the questions; whether a candidate is told their own level; how many days a link lasts.

Then write the questions easiest first:
- Three options, all plausible and from the same category; the right answer is never the longest
  (fix a length giveaway by making a wrong option longer, not by shortening the key); spread the right
  answer across positions.
- Difficulty comes first from word frequency: the most common thousand words for Pre-A1 and A1, the
  second thousand from A2, less common and abstract words from B1.
- Reading texts grow with the band (about 60–80 words at A2, 100–130 at B1), and a reading set asks for
  different things: a detail, a reason, the main idea, an inference, what a word refers to.
- A candidate reaches a band when they get about two thirds of its questions right, with the bands
  below it also at two thirds.

## Check it, then let the teacher decide

`check_placement_test` looks at a finished test through a candidate's eyes and names what would go wrong:
a question whose options cannot be answered as written; a key that is always the longest, or always in
the same place; a level with too little evidence behind it; a score chart with a hole; a description
promising a skill nothing measures; a passage far from its band's usual length; a clock too fast for the
number of questions. Run it when a test is built, and again after a batch of edits.

- **It advises; it does not gate.** Nothing is changed and nothing is refused: the test still publishes
  and still goes out. Put a finding in terms of the person sitting the test — what a candidate could do
  without reading, what a level would rest on — then let the teacher choose. A teacher who says no gets
  the test they asked for, and the matter is closed.
- **Ask what standard they place people by** — their own chart and level names, the CEFR, or nothing
  formal. All three are legitimate. Say once that the checks and the CEFR mapping are available, then
  work the way they want to work.
- **It does not judge everything.** Nothing it reports touches whether the content is accurate, up to
  date, fair or worth asking — a person reads for that, and a real sitting shows the rest. Tell the
  teacher what was looked at, so a quiet report is not mistaken for a clean bill of health.

## What a level means, in CEFR words

`cefr_bands` holds the can-do statements ESLStudeo prints its reports from. Use them to draft "What each
level means" — then check the draft against the test itself: which skills its parts cover, how many
questions sit at each band, whether writing or speaking is collected at all. Where the words go further than the test
does, say so plainly and put two roads in front of the teacher: build the missing questions, or describe
the level by what this test really shows and name the gap. A can-do statement is never pasted in as a
description on its own.

## Score rules and levels

- Each part's `gate` lists score rules, lowest first: a candidate at or below `upTo` percent is placed
  at `place`, or goes on with "__continue__". The last part's final rule must reach 100%.
- `gateBasis` "cumulative" judges the running total of all parts so far — the usual choice for a long
  test with one chart.
- Cut-offs from a real paper chart stay valid only if the questions and the number per part stay the
  same. New cut-offs must be checked: tell the person to run **Analyse** on the test in ESLStudeo
  (Placement → the test), which simulates hundreds of sittings, before relying on it.
- `set_placement_levels` refuses to remove or rename a level that a score rule or a prompt still
  names; change those first.

### What the engine adds to the chart

Once every level has a CEFR band and the questions are tagged, ESLStudeo checks the chart's answer
against the candidate's performance on the questions of that band itself. It moves the result one level
down when at least ten questions of the awarded level's band were answered and fewer than two thirds
were right, and one level up when a higher level's own band was mastered and the total was within one
standard error of that level's cut-off. Either way the result is flagged for the teacher, beside the
chart's own answer, and the teacher decides. With the confirmation setting on, the engine serves a few
more questions at the deciding band before it settles a result the sitting has not evidenced.

## Pictures and recordings

You cannot pass on a file the person dropped into the chat. Files come in by their web address:
1. Ask the person to put the pictures and recordings in one Google Drive folder, named clearly
   (for example "part3-q2-kitchen.jpg", "part4-dialogue1.mp3"), and to share the folder with
   "Anyone with the link" as Viewer.
2. With Claude's Google Drive connection (Customize → Connectors → Google Drive), list the folder. You
   can look at the pictures to match them to questions; you cannot listen to a recording, so match
   recordings by their names.
3. For each file, `upload_placement_media` with its Drive link (kind "picture" or "recording"); a
   file's link can also be written from its id as https://drive.google.com/open?id=THE_ID.
4. Put the address that comes back in the question's `imageUrl` or `audio`.
5. Tell the person that ESLStudeo keeps its own copy, so the folder's sharing can be switched off.
ESLStudeo's generated pictures and voices are made on the ESLStudeo screen, not through Claude.

## Deliver it to people who are far away

1. The test must be published.
2. Collect the list: each person's name, and their email address when there is one; the age is
   required for the Children test.
3. Show the person the list and the choices, and get a yes:
   - `days`: how long the links last, 1 to 30 (7 unless they say otherwise); each link works once.
   - `showLevel`: whether each candidate sees their level at the end. Off by default: the teacher
     decides each level from the results. Never offered for the Children test, whose level is never
     shown to a child or a parent, nor with the interview.
   - This batch's own conditions, when they differ from the test's: `timeLimitMin` (0 for untimed),
     `audioPlays` (0 for as many as they like), `supportLang` ("fr", "ar", or "" for English only) and
     `readAloud`. They apply to these links alone and change nothing in the test — for an invigilated
     room, a candidate who needs longer, or a group who share a first language.
4. `create_placement_links` makes one link per person (up to 200 at a time).
5. Offer one email per candidate. When the person's email is connected to Claude and can save drafts
   (Gmail's can), write one draft per candidate, addressed to that person alone, with their own link,
   what the test is, roughly how long it takes, that it works once, and until when. Save the drafts;
   do not send them unless the person explicitly asks for the emails to be sent, after seeing the
   recipients and the text.
6. Name the candidates without an email address, so the person can send those links another way.
   ESLStudeo's Placement screen also prints the QR codes and downloads the whole list.

## Results and decisions

- `placement_results` lists the sittings: in progress, waiting for a decision, placed, or finished with
  the level shown to the candidate. With `sessionId`, one sitting in full: the part scores, the level
  the questions suggest, whether it is borderline, and with `answers` true every answer.
- Show the teacher the suggestion and the evidence, and let them decide. `decide_placement` records
  only the level the teacher chose, one of the test's own levels, with their note.
- A borderline result, a sitting with very fast answers, or a level that disagrees with the teacher's
  impression is worth a short spoken check before deciding; say so rather than deciding for them.
