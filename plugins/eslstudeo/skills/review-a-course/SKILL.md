---
name: review-a-course
description: Reviews the quality of an ESLStudeo course, unit or page (correct answer keys, answers that cannot be guessed, page design, the order of learning, level, settings and support for teachers) and proposes exact fixes, changing nothing until the person chooses which to apply. Use this skill when the person asks to check, review, audit, proofread, evaluate or improve a course, a unit, a page, a quiz or a test in ESLStudeo, for example "check my course before term starts", "is Unit 2 any good?", "find the mistakes in my quiz" or "how can I make this unit better?".
---

# Reviewing an ESLStudeo course

Judge the course as an experienced colleague would, from what is really written, and change nothing
until the person decides. If the ESLStudeo tools are missing, follow the connect-eslstudeo skill
first.

## Steps

1. Run `check_course`: the problems ESLStudeo itself detects. Note them.
2. Read what is in scope: `read_course`, then `read_unit` for each unit, then `read_page` for every
   page. Judge the words and the items as authored, never a summary of them.
3. Check each page against `references/checklist.md`.
4. Report, grouped by unit and page (the unit's word and number, and the page title, so the person
   can find it). For each problem give:
   - the problem, in one sentence;
   - what it does to a learner, for example "a learner who always picks the longest option scores
     without reading";
   - the fix, with the exact new wording or item.
5. Order the findings. First, what is wrong or cannot be answered: wrong answer keys, two right
   options, mistakes in items, missing pictures or recordings. Then the learning design. Then polish.
   Say in one line what works well; do not list everything that is fine. For a long course, report
   unit by unit.
6. Ask which fixes to apply. Apply only those, one at a time, reading each change back, as the
   edit-a-course skill describes. Never send a confirmation word ("delete", "replace", "restore")
   without the person's yes to that specific change.
