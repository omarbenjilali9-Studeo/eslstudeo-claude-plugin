---
name: mark-and-reply
description: Helps a teacher mark written work and answer learners in ESLStudeo through the ESLStudeo connector, by finding the answers waiting for a mark, proposing marks and feedback from the question's own marking criteria, saving only the marks the teacher confirms, replying under an answer or a discussion post, hiding or pinning discussion posts, and reading and answering what learners wrote with Message my teacher. Use this skill when the person asks to mark, grade or give feedback on their learners' work in ESLStudeo, to deal with a discussion, or to read or answer their learners' messages, for example "mark the welcome emails from Unit 2", "what is waiting for me to mark?", "reply to Sara's post", "hide that post" or "have any of my students written to me?".
---

# Marking and answering learners in ESLStudeo

## Before anything

- These tools need the class permissions. If `work_to_mark` is not available, follow the
  connect-eslstudeo skill: the person connects again and switches on **Also let it into your
  classes** on the ESLStudeo page.
- Learners' written work and messages are personal information, and whatever a tool returns is sent
  to Anthropic. Read only what the task needs.
- Everything saved here reaches a learner at once: a mark, feedback, a reply. Show the person the
  words first, and save or send only what they confirm.

## Marking written work

1. `work_to_mark` without `promptKey` lists the open questions that have answers waiting for a mark:
   how many, and where each question sits (unit and page). It covers the person's own classes; add
   `classId` for one class.
2. `work_to_mark` with a question's `promptKey` gives its answers (the learner, what they wrote,
   when) together with the question, what it is marked out of, and its marking criteria, bands and
   model answer. `includeMarked` true adds the answers already marked.
3. For each answer, propose a mark and short feedback from the question's own criteria, not from
   general impressions. Write the feedback to the learner, in the teacher's voice: what worked, and
   one or two things to improve.
4. Show the teacher the proposed marks and feedback as a short list, and let them change any of it.
5. Save with `mark_work` (`responseId`, `score`, `feedback`) only what the teacher confirmed, as they
   confirmed it. A mark cannot be above the question's maximum, and `score` null clears a mark.
6. Report what was saved. In ESLStudeo, the marks leave **My classes → To mark** and count in
   Progress.

If a question has no criteria, say so before proposing marks. The criteria can be written with
`set_marking_guidance` (the edit-a-course skill), which changes the course for every class, so ask
first.

Discussion posts appear in `work_to_mark` only when the discussion's author switched on
**Mark these posts**. Otherwise posting is done or not done, and it is not marked.

## Discussions

- `discussion_status` shows who posted in a discussion, what they wrote, and who did not post.
- `reply_to_post` (`responseId`, `text`) adds the teacher's reply under a learner's discussion post or
  written answer. The learner reads it, and in a discussion the whole class does too. Draft it in the
  teacher's voice and show it first.
- `moderate_post` (`responseId`): `hide` true hides a post from the class (staff still see it, marked
  as hidden) and false shows it again; `pin` true pins it to the top of the discussion and false
  unpins it. Ask before hiding a learner's post.

## Messages from learners

Learners write to their teacher with **Message my teacher** on their class page. The same
conversations are in ESLStudeo under **My classes → ✉️ Messages**.
- `learner_messages` without `studentId` lists one line per learner who has written, newest first,
  with how many of their messages are unread. With `studentId`, it gives the whole conversation;
  reading it marks it read for the teacher of that learner's class.
- `reply_to_learner` (`studentId`, `body`) sends the teacher's reply into that learner's
  conversation, where only the learner and the staff of their class read it. Draft it in the
  teacher's voice, show it first, and send after the person says yes.
- When several learners ask the same thing, offer one reply each, or a notice to all of them with
  `send_notice` (the run-a-class skill).
