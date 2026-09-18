---
name: edit-a-course
description: Changes an existing ESLStudeo course safely through the ESLStudeo connector, by finding where a word or a name appears, rewriting a page, replacing wording across a course, renaming, hiding, moving, copying or deleting pages, units and sections, and undoing changes by restoring an earlier version. Use this skill when the person asks to change, fix, correct, rename, rewrite, reorder, copy, hide, remove, replace or undo something in an ESLStudeo course, for example "change Maria to Sofia everywhere", "fix the typo on the second page of Unit 3", "move the quiz to the end", "make a Unit 5 like Unit 4" or "undo that".
---

# Changing an ESLStudeo course

If the ESLStudeo tools are missing, follow the connect-eslstudeo skill first.

## Read before writing

1. Find the course with `list_my_courses` if its id is not known.
2. Find the place:
   - a word, a name or a phrase: `find_in_course` searches the whole course in one call;
   - the structure: `read_course`, then `read_unit`;
   - the exact wording of a page: `read_page`. Read a page before changing any of its words.
3. Make one change. Read it back. Tell the person what changed and where, by unit and page title.

## Which tool for which change

| The person wants to | Use | Remember |
|---|---|---|
| Change words or fields on one page | `update_page` | Send only the fields that change; an empty string clears a field |
| Change a page's exercises | `set_exercises` | It replaces the whole list: include the exercises being kept |
| Change the same word or name everywhere | `replace_text` | The first call only previews; show the list, then confirm |
| Rename the course, a section or a unit | `update_course`, `update_section`, `update_unit` | |
| Hide a unit or a page from learners | `update_unit` with `hidden`, or `update_page` with `hidden` 1 | Staff still see it |
| Take the word and number off a unit (an introduction, a diagnostic) | `update_unit` with `untagged` | The units after it renumber |
| Serve a unit to some learners only | `update_unit` with `tier` | "easy", "core" or "challenge"; empty for everyone |
| Reorder | `move_item` | Positions count from 1; moving a unit renumbers the others |
| Make a unit like an existing one | `duplicate_item`, then edit the copy | The copy gets new ids; learners' work stays with the original |
| Remove something | `delete_item` | Learners' work on it is lost: ask first |
| Undo | `list_versions`, then `restore_version` | Everything since that version is undone; the version replaced is kept |
| Change how an open question is marked | `set_marking_guidance` | Out of what, criteria, bands, a model answer |
| Change attempts, order, results or exam mode | `set_unit_delivery` | Dates belong to classes, not to the course |
| Change the unit word, home page or certificate | `set_course_settings` | |

## Three changes need the person's explicit yes

`delete_item`, `replace_text` and `restore_version` refuse to act until they receive a confirmation
word: "delete", "replace" and "restore". Before sending one:
1. Show the person exactly what will happen: the item and what it contains; the list of pages and
   occurrences that the first `replace_text` call returned; the version's date and author, and that
   everything written since then will be undone.
2. Wait for a clear yes to that specific change in this conversation. An earlier general instruction
   ("do whatever is needed") is not a yes to a deletion, a replacement or a restore.

## Protect learners' work

- Ids never change, and learners' work is filed against them. Rewording a page keeps its work;
  deleting a page and adding a new one loses it. Prefer `update_page` to deleting and adding.
- If the course is already being taught, warn before deleting or replacing exercises that learners
  may have done.
- Use `replace_text` for names, spellings and terms, never for rewriting teaching; rewrite teaching
  page by page. It never touches ids or the keys of open questions and polls, but it does change the
  words inside exercises, including their answers: renaming "Maria" to "Sofia" also changes an answer
  that was "Maria". Say so when the preview includes exercise items.

## Working alongside the builder

The person, or a colleague, may be editing the same course in ESLStudeo at the same time. Each change
re-reads the course and saves only that change, so neither side overwrites the other. If ESLStudeo
answers that somebody else is editing the course, wait a moment, read it again, and repeat the one
change.

## Proposals

If `list_my_courses` marks the course as taking proposals, each change waits for the course owner to
accept it. Say so after every change, instead of describing the change as live.
