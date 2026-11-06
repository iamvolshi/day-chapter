# day-chapter

Close out one day on your UGREEN NAS as a single chapter.

Say "close out today" (or name a date) and the Skill gathers that day's photos, videos, documents and notes, writes one dated chapter summary as a new file, and creates one album for the day's photos. Nothing already filed is overwritten. It asks before saving the chapter, creating the album, or moving any file.

Inspired by the idea behind [Curator](https://github.com/iamvolshi/curator) — a life filed chapter by chapter, the full record one click away — rebuilt as a small, new UGOS Skill for the UGREEN Hackathon 2026 on AI NAS. No Curator code or materials are reused; the Skill, its workflow and its chapter format were written new for UGREEN AI NAS.

**Track:** Life — Understand Your Life.

## The Skill

The Skill package is in [`day-chapter/`](day-chapter/) — `SKILL.md` plus `references/day-chapter-record.md`. It is a Markdown orchestration Skill under the Uliya Skill Development Standard, checked with UGREEN's official checker: **static-pass, 0 errors, 0 warnings** (catalog 2.0.0).

It delegates in order — photo-agent, file-agent, document-agent, media-agent, knowledge-agent, then photo-agent and file-agent again — each step passing only its verified real result to the next, using only supported NAS capabilities: `ug-photo`, `ug-filesystem`, `ug-filemgr`, `file-workflow`, `ug-document`, `ug-video`, `ug-knowledge`.

## Proposal

The Round 1 proposal is in [`PROPOSAL.md`](PROPOSAL.md) and [`day-chapter-proposal.pdf`](day-chapter-proposal.pdf) — 492 words, under the 500-word limit, answering all ten required items.

## Status

Round 1 entry, submitted to the UGREEN Hackathon 2026 on AI NAS (Devpost). The full run on a real UGREEN AI NAS is still untested — that is the finalist round.
