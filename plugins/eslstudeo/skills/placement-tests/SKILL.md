---
name: placement-tests
description: Builds and delivers ESLStudeo placement tests through the ESLStudeo connector, by turning a paper test (photos or a document) or a brief into a placement test with parts, questions, levels and score rules that follow the measurement rules keeping a level trustworthy; publishing it; creating one single-use link per candidate for people taking it remotely, with an email draft per candidate in the teacher's own email; and reading the results and recording the level the teacher decides. Use this skill when the person asks about a placement test, a level test, a level check, a diagnostic or placing new students in ESLStudeo, for example "turn these photos of our paper test into a placement test", "make a placement test for adults from A1 to B2", "send the placement test to these twenty people", "who has finished the placement test?" or "place Sara at Intermediate".
---

# Placement tests in ESLStudeo

A placement test answers one question: what level is this person, on evidence. It is not an
achievement test. A question is good if it separates two levels, and useless if everybody gets it
right, however well it is written.

Before anything else, call `what_can_this_builder_do` with part "placement": it gives the exact format
of parts, questions, score rules, levels and settings, and the evidence rules the engine applies.

## Who may do what

- Building a test needs the course permissions. Links, sittings and results carry candidates' personal
  information, so they need the classes switch (**Also let it into your classes**) on the ESLStudeo
  approval page; if `create_placement_links` is missing, follow the connect-eslstudeo skill.
- In a school, owners and administrators build and decide; a teacher does so only when made a proctor
  on ESLStudeo's Placement screen. An independent teacher does everything on their own tests.
- A test bought from the marketplace keeps its questions, levels and score rules locked, because its
  levels are tuned to exactly those questions. Its name, settings and delivery are the buyer's.

## Build from a paper test (photos or a document)

1. Read every page. Transcribe the questions and their order faithfully; do not improve them silently.
2. Find the answer key. If it is not in the photos, ask for it; never guess a key.
3. Ask for the scoring chart: which levels the test places into, and at what scores. If the paper test
   has none, say that the cut-offs will have to be set and checked (see below), rather than inventing
   them as if they were known.
4. Tag every question with its CEFR band (`cefr`), from its own difficulty — how frequent its words are
   and how complex its structure — not from the part's average. Say which tags you are unsure of.
5. Point out, without changing anything, the questions that break the rules below (an absurd option,
   the answer always the longest option, a band with fewer than six questions), and ask which to fix.
6. Build it: `create_placement_test`, then `set_placement_levels` (levels lowest first, each with its
   CEFR band), then one `set_placement_section` per part, then `read_placement_test` to see the problems
   left, then `publish_placement_test`.
7. Pictures and recordings in the paper test come in through `upload_placement_media` from a web
   address — see "Pictures and recordings" below.

## Build a new test from a brief

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
