# ESLStudeo plugin for Claude

Build courses and run classes in ESLStudeo by talking to Claude.

## What the plugin contains

- **The ESLStudeo connector** (`https://eslstudeo.com/mcp`). It gives Claude the same 34 tools, under
  the same four permissions, as adding the connector by hand. You approve it on an ESLStudeo page, and
  your password never reaches Claude.
- **Five skills.** A skill is a set of instructions that Claude reads when a task needs it.
  - **build-a-course**: plans and builds courses, units, pages and exercises in the ESLStudeo house
    style.
  - **edit-a-course**: finds and changes wording, renames, moves, copies, hides, removes, and undoes
    changes.
  - **review-a-course**: checks a course's quality page by page and proposes exact fixes.
  - **run-a-class**: creates classes, reports how a class is getting on, finds who has not done what,
    and sends learners a notice inside ESLStudeo.
  - **connect-eslstudeo**: connecting, the four permissions, what is shared, and ending the connection.

## Install

1. In Claude, open **Customize → Plugins → Add → Upload plugin**, and choose the plugin's zip file.
2. Open **Customize → Connectors → ESLStudeo** and press **Connect**. Sign in on the ESLStudeo page.
   If you want Claude to work with your classes and learners too, switch on **Also let it into your
   classes** (it starts off). Then press **Allow**.
3. If you had already added ESLStudeo as a connector by hand, remove that one, so that only one
   ESLStudeo connection remains.

Then ask, for example: "Make a six-unit course for my Saturday group" or "Who hasn't finished
Unit 2?". You can also type `/` to pick a skill by name.

## The four permissions

| Permission | What Claude may do | Granted |
|---|---|---|
| See courses | Read the courses you may edit, and everything written in them | When you press Allow |
| Change courses | Create courses; write sections, units, pages and exercises; upload pictures and documents | When you press Allow |
| See classes and learners | Read your classes and learners: names, marks, what each learner has and has not done, and email addresses where they exist | Only if you switch on **Also let it into your classes** |
| Act in classes | Create classes, and send learners notices inside ESLStudeo | Only if you switch on **Also let it into your classes** |

Claude acts only as you, and only in courses and classes you can already reach in ESLStudeo. Deleting,
replacing text across a course and restoring an earlier version each need your explicit yes.
ESLStudeo sends no email on your behalf.

ESLStudeo labels every tool as reading or changing, so Claude's **Tool permissions** page
(**Customize → Connectors → ESLStudeo**) groups them. You can, for example, let the reading tools run
without asking and make every change ask first.

## What leaves ESLStudeo

Whatever Claude reads from ESLStudeo is sent to Anthropic and handled under Anthropic's terms. With the
class permissions, this includes your learners' names, marks and email addresses. To build courses
without sharing any learner information, leave **Also let it into your classes** off. On a connection
that already has it, you can instead set the seven class tools to **Blocked** in
**Customize → Connectors → ESLStudeo → Tool permissions**.

## Ending the connection

In ESLStudeo, **⚙ → Connected apps** ends it at once. In Claude, disconnect ESLStudeo under
**Customize → Connectors**, or remove the plugin.
