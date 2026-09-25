# Unit and course settings

The exact names and ranges come from `what_can_this_builder_do` (parts "delivery" and "course").
This file says which to choose.

## How a unit is delivered (`set_unit_delivery`)

| The unit is | Settings |
|---|---|
| Practice (the usual case) | `feedback` "check" (results as learners go), `attempts` 0 (as often as they like), `mode` "free" |
| A lesson to follow in order | `mode` "sequence"; add `lockBack` 1 only if going back would spoil the task |
| Homework | `feedback` "check" or "end". The deadline is set for each class in ESLStudeo, not here |
| A test or an exam | `exam` 1 (one sitting; the score goes to the Exam column), `feedback` "end" or "none", `timeLimitMin` if it is timed, usually `mode` "sequence" |
| A diagnostic ("Where are you now?") | An untagged unit (no word, no number), `feedback` "none" (the work is recorded and no score is shown), `attempts` 1 |
| Outside the grades | `grading` "none" (it still counts for Handed in) |

- `adaptive` 1 switches differentiation on for the unit: the easy and challenge tiers start working,
  measured on that unit's core exercises (`adaptiveThreshold`, the percentage right that counts as
  strong, and `adaptiveMin`, how many core items must be answered first). Without it a tier does
  nothing, and it never runs on a unit whose `feedback` is "none". See "One class, several levels"
  in `references/page-design.md`.
- `requiresPrev` 1 keeps a unit locked until the previous unit is finished.
- `finish` says what the Finish button does. "list" (the usual case) names the pieces of work with no
  answer yet and lets the learner finish anyway; "complete" refuses to finish until every piece is
  handed in, which suits homework that must be done in full (a timed unit still finishes when its time
  runs out, and with `lockBack` 1 each page is checked before Next); "direct" finishes at once, for a
  unit where skipping is expected. A piece a learner cannot do alone (a recorded role-play on a device
  without a microphone, a pair activity) would hold a "complete" unit up, so say so before choosing it.
- A class, or a single learner, can be given a different number of attempts, and a learner who has
  sat an exam can be given a resit (`set_unit_access`, in the run-a-class skill). That number wins
  over the unit's setting.
- Leave `opensAt` and `deadline` off. Dates set on a class override them, and each class runs on its
  own calendar (`set_unit_dates`, in the run-a-class skill).

## The course as a whole (`set_course_settings`)

- `unitWord`: what every unit is called (Unit, Week, Lesson, Module, Chapter). An empty word removes
  it. A single unit can instead be left untagged with `update_unit`, for an introduction or a
  diagnostic; the units after it keep counting.
- `landing`: the course's home page. `eyebrow` is the small line above the title, `headline` the
  headline, `subhead` the sentence beneath it, `cue` the nudge at the foot (for example "Start with
  Unit 1 ↓"), and `heroPhoto` the picture across the top, uploaded first.
- `theme`: the background.
- `certificate`: released when its conditions are met: `requireCompletion`, `minScore` and
  `minCoverage` (percentages), `scoreScope` ("quiz" for every unit with questions, "exam" for the
  exam units only), `title`, `subtitle`, and `email` to send it out. At least one condition is
  required. A class's teacher can replace the conditions for their own class.

## Sections

A section holds units. Split a section into a Student Book and a Workbook (`add_section` with
`split` set to true) when every lesson has matching homework. Each unit then goes into `book`
"student" or "workbook".
