---
name: build-a-course
description: Plans and builds courses, units, pages and exercises in ESLStudeo through the ESLStudeo connector, in the ESLStudeo house style. Use this skill when the person asks to create, make, write, design or build a course, a unit, a lesson, a page, an exercise, a quiz, a test, homework or a diagnostic in ESLStudeo, or to turn their own material (a syllabus, notes, a PDF, a textbook chapter, a worksheet) into one, for example "make a ten-unit course for my evening group", "add a unit on fractions", "write a reading lesson with a quiz" or "turn this worksheet into a unit".
---

# Building a course in ESLStudeo

Work as a careful course author for the person, who is the teacher and decides. Build finished,
classroom-ready material, in small steps the person can see in ESLStudeo as it grows.

## Before writing anything

1. If the ESLStudeo tools are missing, follow the connect-eslstudeo skill first.
2. Call `what_can_this_builder_do` (part "all") once in the conversation, before authoring. It is
   generated from the builder itself, and it is the only reliable source for the exercise types,
   the shape of their items, page fields, unit settings and limits. Author from it, never from memory.
3. Call `list_my_courses`. Use an existing course when the person names one; otherwise create one.
   If a course takes proposals, tell the person that every change will wait for the course owner to
   accept it.

## Agree the brief

Ask only for what is not already known, in one message:
- Who the learners are: their age, their level, what they need the course for, how many they are.
- The size: how many units, how long each lesson is, in class or at home or both.
- What the course calls a unit: Unit, Week, Lesson, Module, Chapter, or no word at all.
- Whether each lesson needs matching homework. If so, use a section split into a Student Book and a
  Workbook.
- Any material to build from: a syllabus, a textbook chapter, notes, a PDF, pictures.

Then propose an outline: the sections; the units, each with a title and a one-line aim; and, for the
first unit, its pages (heading, title, the page's one job, the exercise types). Build once the person
agrees or adjusts it. For a single page or a single unit, a short plan in one message is enough.

## Build in small steps

1. `create_course` with a real title, the unit word and a one-sentence description. Keep the builder
   link it returns and give it to the person.
2. `add_section`, then `read_course` to get the section's id. New items receive their ids from
   ESLStudeo when they are saved: always read them back, never invent one.
3. `add_unit` in the section, then `read_course` for the unit's id.
4. `add_page` one page at a time, in teaching order. Put the exercises in the page's `ia` field, or
   add them afterwards with `set_exercises`.
5. After each unit, `read_unit` to confirm what exists. Then tell the person the unit is ready to
   look at in the Course builder, with **Edit / Preview** and then **As student**. For a long course,
   build one unit per reply and wait for comments before the next, unless the person asks you to
   continue without stopping.
6. For each open question that a teacher marks, call `set_marking_guidance`: what it is marked out
   of, the criteria, a short guide to the bands and a model answer. `read_page` shows the question's
   key.
7. At the end, run `check_course`. Fix every problem it lists, run it again, and report the result
   with the builder link.

## Rules ESLStudeo enforces

- Ids are permanent, and learners' saved work is filed against them. Never invent, reuse or change
  an id.
- A refused write comes back with the reason. Fix exactly what it names and try again. Never work
  around a refusal, for example by pasting an exercise into the page's content as plain text.
- Pictures, recordings and documents must be stored in ESLStudeo. Upload them first, with
  `upload_image` for a picture (up to 6 MB) or `upload_file` for a document or a recording (up to
  20 MB), then use the address that comes back. A link to another website is removed when the course
  is saved. A video is uploaded by the person in the Course builder itself. Use only pictures the
  person supplied or has the right to use.
- A page with `hidden` set to 1 is a draft: learners never see it; staff see it, marked as hidden.
- Dates belong to classes. Leave opening dates and deadlines off the course; the person sets them for
  each class in ESLStudeo, under **My classes**.
- If ESLStudeo answers that somebody else is editing the course, wait a moment, read the course
  again, and repeat the one change.

## The house style, on every page

1. **One job per page.** A page that teaches ten things teaches none. Two unrelated exercises on one
   screen read as a worksheet, not a lesson.
2. **A heading and a title.** The heading is the small line that names the stage, for example
   "READING · FIRST LOOK"; the title says what the page is about.
3. **Instructions as short numbered steps**, never a paragraph. Keep the instructions simpler than
   the content they introduce.
4. **Recognition before production.** Learners meet and choose before they must produce: matching
   and choosing come before typing and writing.
5. **A poll is for opinion, never for testing knowledge.** A poll has no right answer.
6. **Every exercise has a title a learner can read as a task**, for example "Match each word to its
   meaning", not "Exercise 2".

Read `references/page-design.md` before writing a unit. It covers the order of pages in a unit,
which exercise type suits which difficulty, how to write items whose answers cannot be guessed, open
questions, card decks, discussions, role-plays, levels (tiers) and teacher notes.

Read `references/unit-and-course-settings.md` when deciding how a unit is delivered (practice,
homework, test, diagnostic), what the course calls a unit, its home page, or its certificate.

## Finish

Report in a few lines: what was built (sections, units, pages), what `check_course` said, the builder
link, and what the person should look at first. Do not paste the content back into the chat unless
the person asks for it.
