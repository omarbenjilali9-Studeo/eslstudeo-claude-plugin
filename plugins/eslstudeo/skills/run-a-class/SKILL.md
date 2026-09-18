---
name: run-a-class
description: Helps a teacher run their ESLStudeo classes through the ESLStudeo connector, by creating a class and giving its class code, showing who is in a class and how each learner is getting on, finding the learners who have not done something, showing who posted in a discussion, and sending chosen learners a notice inside ESLStudeo. Use this skill when the person asks about their classes, students or learners in ESLStudeo, for example "how is my Tuesday class doing?", "who hasn't finished Unit 3?", "remind the ones who haven't started", "who didn't post in the discussion?" or "create a class for the new group".
---

# Running a class in ESLStudeo

## Before reading anything about learners

- If `list_classes` is not available, the connection lacks the class permissions. Follow the
  connect-eslstudeo skill: the person connects again and switches on **Also let it into your
  classes** on the ESLStudeo page.
- Everything these tools return, including learners' names, marks and email addresses, is sent to
  Anthropic. Read only what the question needs: prefer `find_students` with filters to reading a
  whole class, and ask for unit-by-unit figures (`perUnit`) only when the question is about units.
  Do not repeat personal details the person did not ask for, and do not copy them anywhere else
  unless the person asks.

## Find the class

Call `list_my_courses`, then `list_classes` for the course. A course can have several classes. When
the person's words fit more than one class, ask which. Without a class id, the tools cover every
class of the course that the person may see.

## Create a class

Call `create_class` with the class name (the group, the day or the time; learners see it) and the
start and end dates. Give the person the class code that comes back: learners open ESLStudeo, choose
**Join a class** and type the code. Deadlines, opening dates and exceptions for the class are set in
ESLStudeo, under **My classes**, not through Claude.

## How a class is getting on

`class_progress` gives, for each learner: when they were last in the course, how much work they have
handed in, their scores on continuous work and on exams, the units they have finished, and what is
waiting to be marked. Summarize in a few sentences: how the class is doing overall, who needs
attention, and why. Show a table only if the person asks for one.

## Who has not done something

`find_students` answers "who has not …" in one call. It needs at least one filter. Filters combine,
and a learner must match all of them to be listed:
- `notStarted`: has never opened the course;
- `notSeenForDays`: has not been in the course for that many days;
- `awaitingMark`: has written work waiting for the teacher's mark;
- `missingWork`: has not handed in everything (with `inUnitId`, in that unit);
- `unfinished`: has not finished a unit (with `inUnitId`, that unit);
- `scoreBelow`: scored below that percentage (with `inUnitId`, in that unit);
- `didNotPostIn`: has not posted in the discussion on that page.

Unit and page ids come from `read_course`, `read_unit` or `find_in_course`.

Work waiting for a mark is the teacher's task, not the learners': point the person to
**My classes → To mark**. Claude does not mark work through the connector; it can set how an open
question is marked with `set_marking_guidance`.

## Discussions

`discussion_status` shows who posted, what they wrote, and who did not post. Posting is
participation: it is done or not done, and it is not marked unless the course's author switched on
"Mark these posts" for that discussion.

## Contacting learners

- Many learners sign in with a username and have no email address. Every list of learners says how
  many have none, and who. ESLStudeo sends no email on anyone's behalf.
- `send_notice` reaches every learner: a private notice on each named learner's class feed, marked
  "For you". Nobody sees who else received it.
- Learners can read a notice the moment it is sent. Follow these steps:
  1. Find the learners with `find_students` or `class_roster`.
  2. Draft the notice in the teacher's voice: a short title, who it is from, what to do, and by when.
  3. Show the person the names and the draft.
  4. Send after the person says yes to this list and this text. When the person has already given
     both the exact recipients and the exact words, send without asking again.
  5. Report who received it.
- If the person prefers email, name the learners who have no email address and would not receive
  it, and offer a notice for them.
