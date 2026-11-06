# Day chapter record

A day chapter is one dated text file for one date, written by the knowledge expert from verified NAS results only.

## Format

- Title line: the date, for example `2026-11-15`.
- One short section per source type: photos, videos, documents, notes.
- Each entry names the real file it came from and the time it was made.
- One closing line: what was filed, and what was missing.

## Rules

- A chapter is appended as a new file. An existing chapter file is never overwritten, edited, or deleted by this Skill.
- If a later close-out covers the same date, it writes a second chapter file for that date, dated with its own creation time, and says it is a second pass.
- If a source cannot be read, the chapter says so for that source instead of guessing.
- Nothing in a chapter is presented as fact unless it came from a verified NAS result in the same run.
