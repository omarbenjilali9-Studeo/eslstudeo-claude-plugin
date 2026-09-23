# ESLStudeo plugin for Claude

Build courses and run classes in ESLStudeo by talking to Claude.

## What the plugin contains

- **The ESLStudeo connector** (`https://eslstudeo.com/mcp`). It gives Claude the same 71 tools, under
  the same four permissions, as adding the connector by hand. You approve it on an ESLStudeo page, and
  your password never reaches Claude.
- **Seven skills.** A skill is a set of instructions that Claude reads when a task needs it.
  - **build-a-course**: designs and builds courses with you as an expert would — the questions that
    change the design, a recommended approach, an outline you agree, then unit by unit in the
    ESLStudeo house style.
  - **edit-a-course**: finds and changes wording, renames, moves, copies, hides, removes, and undoes
    changes.
  - **review-a-course**: checks a course's quality page by page and proposes exact fixes.
  - **run-a-class**: creates and changes classes; sets a class's unit dates, access, attempts and
    exam resits; adds, moves or removes learners; reports how a class and each learner are getting
    on; finds who has or has not done something; and writes to learners with a notice inside
    ESLStudeo, or with email drafts in your own email.
  - **placement-tests**: puts your paper test online — it works out the settings that reproduce it and
    asks you to approve them — or designs a new test with you, following the rules that keep a level
    trustworthy; creates one link per candidate for people far away, each batch with its own time
    limit, listening plays and support language, with email drafts; reads the results and records the
    level you decide.
  - **mark-and-reply**: proposes marks and feedback from each question's criteria and saves the ones
    you confirm; answers discussion posts, hides or pins them; reads and answers what learners write
    with **Message my teacher**.
  - **connect-eslstudeo**: connecting, the four permissions, what is shared, and ending the connection.

## Install

1. In Claude, open **Customize → Plugins → Add → Upload plugin**, and choose the plugin's zip file.
2. Open **Customize → Connectors → ESLStudeo** and press **Connect**. Sign in on the ESLStudeo page.
   If you want Claude to work with your classes and learners too, switch on **Also let it into your
   classes** (it starts off). Then press **Allow**.
3. If you had already added ESLStudeo as a connector by hand, remove that one, so that only one
   ESLStudeo connection remains.
4. If your account has several workspaces (your own, and one per organization you belong to), the
   connection works in the workspace you were in when you pressed **Allow**. To work in another
   one, switch to it in ESLStudeo, then disconnect and connect again.

Then ask, for example: "Make a six-unit course for my Saturday group", "Who hasn't finished
Unit 2?", "Give Sara a resit of the mid-term" or "Mark the welcome emails from Unit 2". You can also type `/` to pick a skill by name.

## The four permissions

| Permission | What Claude may do | Granted |
|---|---|---|
| See courses | Read the courses and placement tests you may edit, everything written in them, and ESLStudeo’s design approaches | When you press Allow |
| Change courses | Create courses and placement tests; write their sections, units, pages, exercises and questions; bring in pictures, documents, recordings and videos from a web address such as a Google Drive link | When you press Allow |
| See classes and learners | Read your classes and learners: names, marks, written work and messages, what each learner has and has not done, and email addresses where they exist; placement sittings and results | Only if you switch on **Also let it into your classes** |
| Run classes | Create classes and change their dates and settings; open or close units, set attempts and resits; add, move or remove learners; mark work; answer posts and messages; write to learners inside ESLStudeo; create placement links and record levels | Only if you switch on **Also let it into your classes** |

Claude acts only as you, and only in courses and classes you can already reach in ESLStudeo, under
the same rules as ESLStudeo's own screens. Deleting, replacing text across a course, restoring an
earlier version, ending a class and removing a learner each need your explicit yes. ESLStudeo sends
no email on your behalf; if your email is connected to Claude, Claude can save drafts in it for you to
check and send.

ESLStudeo labels every tool as reading or changing, so Claude's **Tool permissions** page
(**Customize → Connectors → ESLStudeo**) groups them. You can, for example, let the reading tools run
without asking and make every change ask first.

## Pictures, recordings and videos

Claude cannot pass on a file you drop into the chat. Put your files in a Google Drive folder, share it with
"Anyone with the link", and connect Google Drive to Claude: it can then bring in one file or a whole folder.
ESLStudeo keeps its own copy, so you can stop sharing afterwards.

## What leaves ESLStudeo

Whatever Claude reads from ESLStudeo is sent to Anthropic and handled under Anthropic's terms. With the
class permissions, this includes your learners' names, marks and email addresses. To build courses
without sharing any learner information, leave **Also let it into your classes** off. On a connection
that already has it, you can connect again with the switch off, or set the 30 class tools to
**Blocked** in **Customize → Connectors → ESLStudeo → Tool permissions**.

## Ending the connection

In ESLStudeo, **⚙ → Connected apps** ends it at once. In Claude, disconnect ESLStudeo under
**Customize → Connectors**, or remove the plugin.
