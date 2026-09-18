# Designing pages and units

The exact shape of every exercise comes from `what_can_this_builder_do`. This file says how to
choose and write them.

## The shape of a unit

A unit moves learners from meeting something new to using it without help. Adapt this order to the
subject, but keep its direction.

1. **Start.** One page that connects the topic to the learners: a question, a picture, or a poll about
   their own experience (opinion only).
2. **Meet it.** The new material on the page itself: a text, a dialogue, a worked example, a diagram,
   a recording. Follow it with a quick check of understanding (`mc`, `truefalse`).
3. **Understand it.** Recognition exercises: `matching` (a term to its meaning), `mc`, `dropdown`,
   `click-error` (spot the mistake), `ordering` (the steps of a process, the lines of a dialogue).
4. **Practise it with support.** Production with help: `wordbank`, then `gap-fill`, then
   `fix-error`; `form` for a real document completed field by field.
5. **Use it freely.** Open questions the teacher marks (`prompts`), a role-play, a discussion, a
   performance task.
6. **Check and keep it.** A short mixed check, then a summary page with the key points and
   "I can …" statements.

Practice pages use a new situation, not the one on the "Meet it" page: different people, numbers,
places or details, testing the same content. Otherwise learners answer from their memory of the text
instead of using what they learned.

Choose the exercise type by what makes the content difficult:
- Familiar content: recognition (`mc`, `matching`, `truefalse`).
- Difficult meaning: learners infer it from context with choices (`mc`, `dropdown`), and a later page
  confirms it.
- Difficult form (a spelling, a formula, a grammar pattern, the order of a procedure): `gap-fill`,
  `fix-error`, `ordering`.

## Items whose answers cannot be guessed

- `mc` shows the options in the order they are written. Put the right answer in different positions
  across the items, and never make it the longest or the most detailed option.
- Every wrong option must be plausible to a learner who has not understood. No joke options.
- Comprehension questions paraphrase the text. Never copy the sentence the answer comes from, or
  learners match words instead of understanding them.
- Matching pairs must not share a word, or a form of the same word, that gives the pair away.
- A `truefalse` statement is clearly true or clearly false from the text. Avoid "always" and "never",
  which signal a false statement.
- One gap tests one thing, and the sentence around it makes the answer decidable. List every
  acceptable answer with a pipe: `[[colour|color]]`.
- Each error-correction marker holds one real, typical mistake, written as the learner will see it:
  `[[go>goes]]`.
- `dropdown` choices list only the wrong options; ESLStudeo adds the right one and shuffles them.
- Check every answer key before saving. A wrong key marks a right answer wrong.

## Open questions (`prompts`)

Use open questions for writing or speaking that the teacher marks by hand. Each has a `key` that is
unique in the course and never changes. After adding them, set the marking guidance of each with
`set_marking_guidance`: the maximum score (10 unless there is a reason to change it), the criteria, a
short guide to the bands, and a model answer. The guidance also steers the mark that ESLStudeo
suggests to the teacher.

## Card decks, discussions, role-plays, performance

- **Cards** (`cards`) split a deck across the class, so that each learner takes a share. They suit
  information-gap and jigsaw tasks. Eight cards or fewer is advised. `cardsRequired` sets how many
  cards each learner completes; `soloThread` gives the alternative for a learner working alone.
- **A discussion** (`discussion`) turns a page into a thread. Posting is participation: it is done or
  not done, and it is not marked. An author who wants the posts marked switches on "Mark these
  posts" for that discussion in the Course builder.
- **A role-play** (`roleplay`) is a scripted exchange; `answerMode` is "type" or "record".
- **A performance task** (`perform`) is judged live in class.

## Mixed classes and teacher support

- `tier` on a page or a unit ("easy", "core" or "challenge") serves it only to those learners. Leave
  it off for everyone.
- `teacherNotes` on a page hold the aim, the traps and the answers to watch for. Only staff see them.
  Write them wherever a teacher might wonder why a page is built as it is.
- `linkTo` and `linkTo2` point to an earlier page the learner may need again; a button takes the
  learner there and back. A page holds two links at most.
