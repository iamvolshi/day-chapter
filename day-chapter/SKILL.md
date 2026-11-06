---
name: day-chapter
description: A dated chapter of one day on the NAS, with its photos, videos, documents and notes filed together and nothing overwritten, when a user asks to close out a day or asks what happened on a date.
---

# Goal

Close out one day on the NAS as a single chapter: gather the photos, videos, documents and notes from that date, write one dated chapter summary that is appended and never overwritten, and create one album for the day's photos. The chapter is a record of what happened, not a rewrite of it. See [references/day-chapter-record.md](references/day-chapter-record.md) for the chapter format.

# Required input

Collect only the date to close out (default: today) and, if the user gives one, a single focus such as a person, place or topic. Do not pre-collect private parameters owned by a child expert, such as file paths, album IDs or document IDs.

# Generation-time capability evidence

- `ug-photo` → `photo-agent`
- `ug-filesystem` → `file-agent`
- `ug-filemgr` → `file-agent`
- `file-workflow` → `file-agent`
- `ug-document` → `document-agent`
- `ug-knowledge` → `knowledge-agent`
- `ug-video` → `media-agent`

# Orchestration

Delegate in this order. Each step passes only its real result to the next step, and downstream steps use only the upstream real result. The parent Skill uses only `delegate`; it does not directly execute any CLI call.

1. Delegate to `photo-agent` with `delegate --target photo-agent --instruction 'Find the photos and videos from the requested date on the NAS, grouped by time, and report the verified photo and video results with their real file paths. If no photos or videos exist for that date, report that empty result and stop the album step.'`
2. Delegate to `file-agent` with `delegate --target file-agent --instruction 'Find the files and documents created or modified on the requested date on the NAS and report the verified file results with their real file paths. If no files exist for that date, report that empty result and stop the document step.'`
3. Delegate to `document-agent` with `delegate --target document-agent --instruction 'Read only the verified document paths passed from the file step. Extract the key facts from each document and report the verified extracted facts. If a document cannot be read, report that failure for that document and continue with the remaining documents.'`
4. Delegate to `media-agent` with `delegate --target media-agent --instruction 'Search only the verified video paths passed from the photo step for subtitles and report the verified subtitle results. If no subtitles exist, report that empty result.'`
5. Delegate to `knowledge-agent` with `delegate --target knowledge-agent --instruction 'Transcribe only the verified audio recordings passed from the file step, then save one dated chapter summary as a new text file using the verified photo, video, document, subtitle and transcription results. The chapter file is appended as a new file and must never overwrite an existing chapter file. Ask for user confirmation before saving the chapter file.'`
6. Delegate to `photo-agent` with `delegate --target photo-agent --instruction 'Create one album for the requested date using only the verified photos passed from the first step. Ask for user confirmation before creating the album. If the photo step returned no photos, do not create an album.'`
7. Delegate to `file-agent` with `delegate --target file-agent --instruction 'Move the verified files from the requested date into the dated chapter folder only after user confirmation, and report the verified moved results. If the user does not confirm, leave every file where it is.'`

# Completion and failure

- `completed`: Report the chapter file path, the album name, and a short list of what was filed, only after the delegated expert returns `completed` for each step.
- `failed`: Report the failed step and which result is missing. Stop dependent steps when their required result is unavailable. Preserve partial results and say plainly what was filed and what was not.
- `cancelled`: Stop all remaining steps at once and report what was already filed before the cancellation.
- `waiting_user`: Ask the user for the missing date or focus, then wait. Do not guess a date and do not substitute a different date.
- `waiting_approval`: Wait for the user to confirm the chapter save, the album creation, or the file move. Do not save, create, move, delete or overwrite anything while waiting for approval.
- If no photos, videos, documents or files exist for the requested date, say so clearly and stop. Do not invent content, do not substitute results from a different date, and do not create an empty chapter or an empty album.
