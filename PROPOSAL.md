# UGREEN Hackathon 2026 — Project Proposal: day-chapter

## 1. What does your Skill do?
day-chapter closes out one day on a UGREEN NAS as a single chapter: it gathers that day's photos, videos, documents and notes, writes one dated chapter summary, and creates one album.

## 2. Target user and problem
Families who store years of photos, videos and documents on a NAS and never look at them again. The day's material lands in scattered folders, the story of the day is lost, and nobody files it.

## 3. Solution
One request — "close out today" — files the whole day into a dated record that is appended and never overwritten, so the life record stays one click away instead of buried in folders.

## 4. Main user flow
The user names a date (today by default). The Skill finds that day's photos, videos and files, reads the documents, transcribes any recordings, writes the chapter file, and creates the album. Only after confirmation, it moves the files into the dated folder, then reports the chapter path, album name, and what was filed.

## 5. What makes it different?
Photo apps sort by face or date and stop there; chatbots summarise whatever you paste and forget it. day-chapter files the day itself, across photos, video, documents and notes at once, and its record is append-only: a later pass writes a second chapter, never rewrites the first.

## 6. UGREEN AI NAS features used
Photo search and album creation (ug-photo) find the day's pictures and build the album. File find and move (ug-filesystem, ug-filemgr, file-workflow) locate and file the day's files. Document extraction (ug-document) reads the documents. Subtitle search (ug-video) covers video. Knowledge transcription and saving (ug-knowledge) write the chapter.

## 7. Technical approach
A Markdown orchestration Skill under the Uliya Standard: SKILL.md plus one linked reference for the chapter format. It delegates in order — photo-agent, file-agent, document-agent, media-agent, knowledge-agent, then photo-agent and file-agent again — each step passing only its verified real result to the next. Input is the date, plus an optional person, place or topic. Moves, saves and album creation need user confirmation. It uses the NAS's own AI through the supported CLIs. Data stays on the NAS, and the Skill contains no scripts or binaries.

## 8. Built so far, and what needs a NAS
Built: the full SKILL.md workflow and chapter-format reference, checked with UGREEN's official checker — static-pass, 0 errors, 0 warnings, catalog 2.0.0. Still needs a NAS: the full run on real data, confirmation prompts, and the album and folder results as the user sees them.

## 9. Finalist testing
Core case 1: a normal day with photos, a video and a document — the chapter lists all three, the album holds the photos, the files land in the dated folder. Core case 2: a day with one photo only — the chapter files it and says the rest was empty. Edge case: a date with nothing — the Skill reports it empty and creates nothing.

## 10. Limits, risks, outside dependencies
The Skill can only use capabilities in the UGREEN catalog, so a source type with no supported CLI cannot be filed. It depends on the NAS's experts behaving as the catalog describes, and on file dates and metadata being right. It does not verify what a document says, only that it was filed.

---
Third-party components: none. No third-party libraries, components or external services are used. AI tools used: Muse (Meta) as a coding assistant to draft SKILL.md and this proposal, from the author's own idea and wording.
