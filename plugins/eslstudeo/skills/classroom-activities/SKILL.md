---
name: classroom-activities
description: Makes single classroom activities in a teacher's own Classroom Activities in ESLStudeo through the ESLStudeo connector, by writing a printable activity (a board game, speaking cards, a find someone who, role-play cards, a jigsaw and others) or a spinning wheel of discussion topics for the classroom screen, adding a ready file from a Google Drive link, listing what is already there, changing an activity made earlier and filing activities in folders. Use this skill when the person wants one activity for a lesson rather than a whole course, for example "make a board game to review Unit 5", "a spinning wheel with twelve topics on health for my B1 class", "add this worksheet to my activities", "what is in my Classroom Activities" or "put these in a folder for Intermediate 3".
---

# Making classroom activities in ESLStudeo

Classroom Activities is each teacher's own bank of ready activities: files they uploaded, printable
activities that ESLStudeo lays out as a board, cards or a handout, and wheels shown on the classroom
screen. It is separate from courses. Use it when the person wants one activity for a lesson. When
they want lessons that learners work through online, with marks, use the `build-a-course` skill
instead.

Everything this skill makes is saved in the person's own bank and is private. The person shares an
activity with their team from ESLStudeo if they wish. No other person's bank can be read or changed.

## Before anything

1. If the ESLStudeo tools are missing, or a call is refused for lack of permission, use the
   `connect-eslstudeo` skill. Reading the bank needs **See courses**; adding to it needs **Change
   courses**.
2. Call `what_can_this_builder_do` with `part` set to `activities`. It returns every printable type
   with what it is for and how many items it takes, the exact shape of a spinning wheel, and the
   files the bank accepts. Follow those shapes exactly.
3. Call `list_activities` to see what the person already has and which folders they use, so you
   file the new activity where they would look for it and do not make a second copy.

## Ask only what changes the activity

Three things decide the content: the class level (in the teacher's own words, or a CEFR band), the
unit or theme, and the language to practise (the target words or the grammar point). If the person
gave them, start. If one is missing, ask for it in one short question. Do not ask about layout:
ESLStudeo lays the activity out.

## A printable activity

Use `create_activity` with the `type`, a `title`, the `level`, the `unit` and `items`.

- `items` is a list of strings. Each item is one prompt exactly as students should read it. Do not
  number the items and do not add markup.
- Write at the class's level. A prompt a student cannot read cannot be discussed.
- Vary the prompts: personal experience, opinion, a choice between two things, a short task. A list
  of twelve questions of one form is tiring to play.
- A board game takes 22 to 30 squares. The other types take 6 to 12 items. For a Reading, the first
  item is the passage and each further item is one comprehension task.
- `instructions` is how the teacher uses the activity in class, in two or three sentences. Leave it
  out to use the standard text for the type.
- A Listening activity is not made here, because it needs a recording. Tell the person that Create
  activity in ESLStudeo makes those.

## A spinning wheel

A spinning wheel is shown on the classroom screen. The class spins it; the topic under the pointer
opens a card with a discussion question, a follow-up question and the target words to use. A word
bank under the wheel holds every target word, and the teacher taps a word when a student uses it.

Use `create_activity` with `type` set to `Spinning wheel` and a `wheel`:

- `topics`: 10 to 16 is best (2 at least, 24 at most). Each topic has a `label` of two to four
  words for the wheel, a `question`, a `followUp` and the `words` to use.
- A `question` asks for an opinion, an experience or a choice. It has no single right answer, and
  a pair can talk about it for three minutes.
- Wrap each target word in two asterisks inside the question and the follow-up, like `**this**`.
  The screen shows it in bold, the way a textbook marks its target words.
- `groups` is optional: the names of the lessons or themes the topics belong to, up to four. Each
  group has its own colour on the wheel and its own column in the word bank. Give each topic the
  `group` name it belongs to. Use groups when a unit has two lessons; leave them out otherwise.
- `subtitle` is one line under the title that says what the class does.

Tell the person how to use it: they open it under **Classroom Activities** and press **Present** to
show the wheel on the whole screen.

## A ready file

Use `upload_activity_file` with the file's web address in `url`, and a `title`, `level` and `unit`.

- You cannot hand a file over yourself. Ask for a Google Drive share link, with the file shared with
  **Anyone with the link**. A Google Doc or Slides file arrives as a Word or PowerPoint file.
- The bank takes PDF, Word and PowerPoint files, pictures and text files, up to 60 MB.
- Give the file the title, level and unit a teacher would look for it under, and one or two
  sentences in `description` on what it is useful for.

## Folders

`folder` on `create_activity` and `upload_activity_file` is the name of one of the person's folders;
a folder that does not exist yet is made. `set_activity_folder` moves an activity made earlier, or
takes it out of its folder when `folder` is empty. Many teachers keep one folder for each level they
teach. Follow the folders `list_activities` shows, and ask before starting a new way of grouping.

## Changing an activity

`update_activity` replaces the title, level, unit, items or wheel of an activity the person made
earlier. Send only what changes; the rest stays. The items or the wheel are replaced whole, so send
the complete new list. Say what you are about to change and get a yes first. An uploaded file cannot
be rewritten: add the new file instead.

## After each activity

Say in one or two lines what you made, where it is filed, and how the person uses it. Offer one
useful next step, such as a second activity for the same unit or the same activity one level easier.
