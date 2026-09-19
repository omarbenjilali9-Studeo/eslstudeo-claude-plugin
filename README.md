# ESLStudeo for Claude

The ESLStudeo plugin lets you build courses and run classes in [ESLStudeo](https://eslstudeo.com) by
talking to Claude. ESLStudeo is a platform for building courses and teaching classes, in any subject.

With the plugin, Claude can:
- design a course with Claude as an expert colleague: it asks the questions that change the design,
  recommends an approach, agrees an outline with you, then builds one unit at a time, in small steps
  you can see in ESLStudeo as it grows;
- turn a paper placement test (photos or a document) into an online one — it works out the settings
  that reproduce your test and asks you to approve them — following the rules that keep a level
  trustworthy, and send each candidate their own single-use link, with an email draft per
  person; then read the results and record the level you decide;
- bring in pictures, recordings and videos from a Google Drive folder;
- find and change wording across a course, rename, reorder, copy, hide and remove things, and put a
  course back to an earlier version;
- review a course's quality page by page and propose exact fixes;
- run your classes: change a class's name, dates and settings, open or close units for some learners
  or the whole class, set attempts and exam resits, and add, move or remove learners;
- tell you how a class and each learner are getting on, and find the learners who have or have not
  done something;
- propose marks and feedback from each question's own criteria, and save the ones you confirm;
- answer discussion posts and what learners write to you with **Message my teacher**;
- write to learners: a notice inside ESLStudeo, which reaches every learner, or, if your email is
  connected to Claude, one email draft per learner for you to check and send.

## What it contains

- **The ESLStudeo connector** (`https://eslstudeo.com/mcp`). You approve it on an ESLStudeo page;
  your password never reaches Claude.
- **Seven skills**, the instructions Claude reads when a task needs them: `build-a-course`,
  `edit-a-course`, `review-a-course`, `placement-tests`, `run-a-class`, `mark-and-reply` and
  `connect-eslstudeo`.

The plugin itself is in [`plugins/eslstudeo`](plugins/eslstudeo).

## Install

**In Claude (web or desktop):** Customize → Plugins → Add → **Add marketplace**, and paste this
repository's address, `https://github.com/omarbenjilali9-Studeo/eslstudeo-claude-plugin`. Then
install **ESLStudeo** from the list.

**In Claude Code:**

```
/plugin marketplace add https://github.com/omarbenjilali9-Studeo/eslstudeo-claude-plugin.git
/plugin install eslstudeo@eslstudeo
```

Then connect: Customize → Connectors → **ESLStudeo** → **Connect**. Sign in on the ESLStudeo page. If
you want Claude to work with your classes and learners as well as your courses, switch on **Also let
it into your classes** (it starts off). Then press **Allow**.

You need an ESLStudeo account ([eslstudeo.com](https://eslstudeo.com)).

## Permissions and privacy

| Permission | What Claude may do | Granted |
|---|---|---|
| See courses | Read the courses and placement tests you may edit, everything written in them, and ESLStudeo’s design approaches | When you press Allow |
| Change courses | Create courses and placement tests; write their sections, units, pages, exercises and questions; bring in pictures, documents, recordings and videos from a web address such as a Google Drive link | When you press Allow |
| See classes and learners | Read your classes and learners: names, marks, written work and messages, what each learner has and has not done, and email addresses where they exist; placement sittings and results | Only if you switch on **Also let it into your classes** |
| Run classes | Create classes and change their dates and settings; open or close units, set attempts and resits; add, move or remove learners; mark work; answer posts and messages; write to learners inside ESLStudeo; create placement links and record levels | Only if you switch on **Also let it into your classes** |

- Claude acts only as you, and only in courses and classes you can already reach in ESLStudeo, under
  the same rules as ESLStudeo's own screens.
- Deleting, replacing text across a course, restoring an earlier version, ending a class and removing
  a learner each need your explicit yes. Claude shows you what it will write before anything reaches
  a learner. ESLStudeo sends no email on your behalf.
- Every tool is labelled as reading or changing, so Claude's Tool permissions page can, for example,
  let reads run freely while every change asks first.
- Whatever Claude reads from ESLStudeo is sent to Anthropic and handled under Anthropic's terms. With
  the class permissions, that includes your learners' names, marks and email addresses. Leave the
  switch off to keep them out.
- To end the connection: in ESLStudeo, ⚙ → **Connected apps**; or disconnect it in Claude.

© ESLStudeo. All rights reserved.
