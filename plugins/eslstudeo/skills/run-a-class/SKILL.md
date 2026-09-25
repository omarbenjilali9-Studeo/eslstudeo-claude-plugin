---
name: run-a-class
description: Helps a teacher run their ESLStudeo classes through the ESLStudeo connector, by creating a class and giving its class code; changing a class's name, dates, joining, class board, grade weighting or certificate rule; ending or reopening a class; opening or closing units, setting a class's unit dates, attempts and exam resits; adding, moving or removing learners; showing how a class and each learner are getting on; finding who has or has not done something; and writing to learners with a notice, an announcement or email drafts. Use this skill when the person asks about their classes, students or learners in ESLStudeo, for example "how is my Tuesday class doing?", "who hasn't finished Unit 3?", "give Sara a resit of the mid-term", "open Unit 4 for the whole class until Friday", "move Ali to the Thursday group", "draft emails to the ones who scored below 50%" or "create a class for the new group".
---

# Running a class in ESLStudeo

Marking written work, discussions and learners' messages are in the mark-and-reply skill.

## Before reading anything about learners

- If `list_classes` is not available, the connection lacks the class permissions. Follow the
  connect-eslstudeo skill: the person connects again and switches on **Also let it into your
  classes** on the ESLStudeo page.
- Everything these tools return, including learners' names, marks and email addresses, is sent to
  Anthropic. Read only what the question needs: prefer `find_students` with filters to reading a
  whole class, and ask for unit-by-unit figures (`perUnit`) only when the question is about units.
  Do not repeat personal details the person did not ask for, and do not copy them anywhere else
  unless the person asks.
- The tools act with the person's own rights in ESLStudeo. A teacher reaches their own classes; the
  heads of an organization reach its classes, and some changes (a class's name, dates, joining,
  weighting and certificate) belong to the class's own teacher alone. A refusal says why: pass it on
  in plain words.

## Find the class

Call `list_my_courses`, then `list_classes` for the course. A course can have several classes. When
the person's words fit more than one class, ask which. Without a class id, the reading tools cover
every class of the course that the person may see. Before changing a class, read it with
`class_details`: its name, dates, whether it has ended, joining and its class code, the class board,
the grade weighting, the certificate rule, and how its units are delivered where that differs from the
course.

## Create a class

Call `create_class` with the class name (the group, the day or the time; learners see it), the start
day (`startsAt`, today if left out) and the end day (`endsAt`, required). A class runs for at most one
year, and never past the course's licence. Give the person the class code that comes back: learners
open ESLStudeo, choose **Join a class** and type the code.

## Change a class

- `update_class` changes only what is sent: `title`, `startsAt` and `endsAt`, `joining` ("open" or
  "closed": whether new learners can join with the class code), `classBoard` (true lets the class's
  learners see each other's names and progress), `continuousShare` (0 to 100: the final grade becomes
  continuous work × that share + the exam × the rest; null goes back to one pooled score),
  `certificate` (this class's own certificate conditions, or null for the course's) and `delivery`
  (how this class's units are delivered, below). Say what will change before changing it, and read the
  result back.
- `end_class` ends a class: its learners lose access to the course, joining closes, and every record,
  mark and certificate is kept. It refuses unless `confirm` is the word "end". Ask first, naming the
  class and how many learners it has.
- `reopen_class` brings an ended class back with its learners and records. If its end date has
  passed, set a new one with `update_class` straight after.

## Units: order, access, dates, attempts and resits

The course sets the rules for every class (whether a unit waits for the previous one, its number of
attempts, exam mode); changing them with `set_unit_delivery` (the edit-a-course skill) changes every
class. For one class, or for particular learners, use these instead:
- `update_class` with `delivery` changes, for THIS class only, six of the course's settings for every
  unit: `order` ("wait": each unit waits until the previous one is finished; "open": none waits),
  `mode` ("sequence": pages open one after another; "free"), `feedback` ("check": right or wrong at
  each Check; "end": at the end of the unit; "none": never shown), `back` ("allowed" or "locked": no
  going back to an earlier page), `time` ("none": no time limits; "1.25", "1.5" or "2": the course's
  limits multiplied) and `finish` ("list": name what is missing, then let them finish; "complete":
  only when every piece of work is handed in; "direct": at once). Send only the keys to change; "course" puts one back to the course's setting,
  and `delivery: null` all of them. Exam units always keep the course's settings. The class's teacher
  or a manager of the course may change it; `class_details` reads it back in words.
- `unit_access` shows, for each unit and each learner, whether it is finished, open or locked and
  why, and the exceptions already made. With `classId`, it also gives the class's own dates. Read it
  before changing access, and narrow it with `unitId` or `studentId` when the class is large.
- `set_unit_dates` sets a class's calendar, unit by unit, in `units`: `opensAt` (locked before),
  `deadline`, and `afterDeadline` ("review" leaves the unit readable without submitting; "locked"
  shuts it). Units not named keep their dates. Unit ids come from `read_course`. Read the dates back
  in plain words, in the person's time zone.
- `set_unit_access` makes an exception, with `action`:
  - "open": open the unit now, keeping the course's order of activities; with `until`, only until
    that moment (a personal deadline).
  - "open-any-order": open it, with its activities in any order. Never for an exam.
  - "close": close it now.
  - "attempts": the learners' own number of attempts (`attempts`; 0 = unlimited; left out, back to
    the course's number). Never for an exam, which is one sitting.
  - "resit": one more sitting of an exam, for named learners who have already sat it, never for a
    whole class. The new sitting's score replaces the first, and ESLStudeo's **Progress (beta)**
    marks it "resit". Each "resit" gives one more sitting.
  - "resit-cancel": withdraws a resit that has not been used yet.
  Name the learners in `studentIds` (from `class_roster` or `find_students`). Leave `studentIds` out,
  with `classId`, to act on the whole class (never for a resit). The latest action wins over the
  unit's dates and rules.
- After changing access or dates, offer to tell the learners concerned what changed, with
  `send_notice`.

## Learners in a class

- `class_roster` lists a class's learners, with their username and their email address where they
  have one.
- `manage_learner` with `action`:
  - "add": puts a learner who already has an ESLStudeo account into the class, by their exact
    `username`. A school's class takes only that school's learners; anybody else joins with the class
    code.
  - "move": moves a learner (`studentId`) of this course into this class from another class of the
    same course.
  - "remove": takes a learner out of the class. Their account and work are kept, but they lose access
    to the course. It refuses unless `confirm` is the word "remove": ask first, naming the learner.
  New accounts and passwords are made in ESLStudeo itself (**🔑 Student accounts**), never through
  the chat.
- `set_read_aloud` answers a learner's request to have the course read aloud to them, an
  accessibility aid: `decision` "approved", "declined" or "reset" (they can ask again).

## How a class is getting on

`class_progress` gives, for each learner: when they were last in the course, how much work they have
handed in, their scores on continuous work and on exams, the final grade where the class has a
weighting, the units they have finished, and what is waiting to be marked. Summarize in a few
sentences: how the class is doing overall, who needs attention, and why. Show a table only if the
person asks for one.

For one learner, `learner_record` gives everything the teacher's screens show: time in the course,
each unit's status, attempts used and whether a score comes from a resit, scores, work handed in and
missing, marks waiting, access exceptions and the final grade. With `unitId` and `writtenAnswers`
true, it adds their written answers in that unit.

## Who has or has not done something

`find_students` answers "who has not …" in one call. It needs at least one filter. Filters combine,
and a learner must match all of them to be listed:
- `notStarted`: has never opened the course;
- `notSeenForDays`: has not been in the course for that many days;
- `awaitingMark`: has written work waiting for the teacher's mark;
- `missingWork`: has not handed in everything (with `inUnitId`, in that unit);
- `unfinished`: has not finished a unit (with `inUnitId`, that unit);
- `scoreBelow`: scored below that percentage (with `inUnitId`, in that unit);
- `scoreAtLeast`: scored that percentage or more (with `inUnitId`, in that unit), for example to
  congratulate the best results;
- `scoreOf` chooses the score that `scoreBelow` and `scoreAtLeast` read: "overall" (the default),
  "continuous", "exam" or "final" (the class's weighted grade);
- `didNotPostIn`: has not posted in the discussion on that page.

Unit and page ids come from `read_course`, `read_unit` or `find_in_course`.

## Writing to learners

- Many learners sign in with a username and have no email address. Every list of learners says how
  many have none, and who. ESLStudeo itself sends no email.
- `send_notice` reaches every learner named: a private notice on each one's class feed, marked
  "For you". Nobody sees who else received it.
- `announce_to_class` posts one notice on a class's feed, for every learner of that class: a change
  of time, a reminder, something to bring.
- Learners can read a notice the moment it is sent. Follow these steps:
  1. Find the learners with `find_students` or `class_roster`.
  2. Draft the notice in the teacher's voice: a short title, who it is from, what to do, and by when.
  3. Show the person the names and the draft.
  4. Send after the person says yes to this list and this text. When the person has already given
     both the exact recipients and the exact words, send without asking again.
  5. Report who received it.

### Email drafts

When the person wants email, and Claude can reach the person's own email through a connector that
saves drafts (Gmail's does):
1. Find the learners, as above. Only the learners with an email address can receive one.
2. Write one draft per learner, addressed to that learner alone, never one email to the group: a
   shared email would show every learner's address to the others. Use the learner's name, and their
   own figures when the email is about their results.
3. Save the drafts in the person's email and do not send them. The person reads and sends them.
   Send only if the person explicitly asks for the emails to be sent, after seeing the recipients and
   the text.
4. Report how many drafts were saved, and name the learners who have no email address. Offer them
   the same message as a notice with `send_notice`, which reaches them inside ESLStudeo.

If no email connector is available, say so, and offer a notice instead, or the texts in the chat for
the person to send themselves.
