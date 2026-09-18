# ESLStudeo for Claude

The ESLStudeo plugin lets you build courses and run classes in [ESLStudeo](https://eslstudeo.com) by
talking to Claude. ESLStudeo is a platform for building courses and teaching classes, in any subject.

With the plugin, Claude can:
- plan and build a course, a unit, a lesson, a quiz or homework, in small steps you can see in
  ESLStudeo as it grows;
- find and change wording across a course, rename, reorder, copy, hide and remove things, and put a
  course back to an earlier version;
- review a course's quality page by page and propose exact fixes;
- tell you how a class is getting on, find the learners who have not done something, and send them a
  notice inside ESLStudeo.

## What it contains

- **The ESLStudeo connector** (`https://eslstudeo.com/mcp`). You approve it on an ESLStudeo page;
  your password never reaches Claude.
- **Five skills**, the instructions Claude reads when a task needs them: `build-a-course`,
  `edit-a-course`, `review-a-course`, `run-a-class` and `connect-eslstudeo`.

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
| See courses | Read the courses you may edit, and everything written in them | When you press Allow |
| Change courses | Create courses; write sections, units, pages and exercises; upload pictures and documents | When you press Allow |
| See classes and learners | Read your classes and learners: names, marks, what each learner has and has not done, and email addresses where they exist | Only if you switch on **Also let it into your classes** |
| Act in classes | Create classes, and send learners notices inside ESLStudeo | Only if you switch on **Also let it into your classes** |

- Claude acts only as you, and only in courses and classes you can already reach in ESLStudeo.
- Deleting, replacing text across a course and restoring an earlier version each need your explicit
  yes. ESLStudeo sends no email on your behalf.
- Every tool is labelled as reading or changing, so Claude's Tool permissions page can, for example,
  let reads run freely while every change asks first.
- Whatever Claude reads from ESLStudeo is sent to Anthropic and handled under Anthropic's terms. With
  the class permissions, that includes your learners' names, marks and email addresses. Leave the
  switch off to keep them out.
- To end the connection: in ESLStudeo, ⚙ → **Connected apps**; or disconnect it in Claude.

© ESLStudeo. All rights reserved.
