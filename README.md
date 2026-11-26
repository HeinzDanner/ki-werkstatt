# KI-Werkstatt

**Two local-AI projects in development — running on my own PC, built with Claude Code.**

*KI-Werkstatt is German for "AI workshop": the place where things are still being built.*

> [!NOTE]
> **Status, November 2026: work in progress.** Both projects run and are tested on my PC, but neither is a
> finished product. The source code is private for now; this repository describes what the projects do, how they
> are designed and what has been measured so far.

## The projects

| Project | What it does | Where it stands |
|---|---|---|
| **[fundstelle](fundstelle/)** | Answers questions about your own PDF documents with a local language model. Every answer comes with file, page and a checked quote — or with a clear "the documents do not say". | Import, search and answers done (stages 1–3 of 4); a simple web interface is next |
| **[pc-agent](pc-agent/)** | Does everyday PC tasks from one German sentence ("Kopiere Rechnung.pdf in den Ordner Steuer 2026.") — using only tools the user has switched on, and asking before it changes or sends anything. | Windows program with setup, window and installer works; voice input in testing; Linux and macOS open |

## What both projects have in common

- **Local first.** The language model (Qwen3 8B in [Ollama](https://ollama.com)) runs on my own graphics card.
  Documents, commands and answers stay on the computer; pc-agent even refuses a model server that is not on the
  same machine.
- **The program checks, the model suggests.** A small local model makes mistakes, so everything that matters is
  checked in ordinary code: quotes against the stored text (fundstelle), every action against the user's
  permissions, with a confirmation the program writes itself (pc-agent).
- **"I don't know" is a good answer.** fundstelle declines when it finds no evidence; pc-agent asks back instead of
  guessing a file, a folder or a recipient.
- **Measured, not guessed.** Each project has a fixed test set (questions or commands). Every larger change is
  measured before and after, and every number on these pages comes from such a run.
- **Small, approved steps.** Each stage starts with a written plan and acceptance criteria, and ends with tests,
  measurements and my acceptance.

## Hardware and stack

| | |
|---|---|
| PC | Windows 11, AMD Ryzen 5 7500F, 32 GB RAM, AMD Radeon RX 6800 (16 GB) |
| Model runtime | Ollama with the Vulkan backend (ROCm does not support this card on Windows), listening on 127.0.0.1 only |
| Model | `qwen3:8b` (Q4_K_M, Apache-2.0), 4096-token context, thinking mode off |
| GPU check | 67 tokens/s on the GPU vs. 11 on the CPU; a 30-minute stability run without a single failed request |
| Code | Python 3.14 and pytest; SQLite FTS5 and FastAPI (fundstelle); pydantic, Tkinter, PyInstaller, NSIS and whisper.cpp (pc-agent) |

## How these projects are built

Short and honest: **Claude Code, Anthropic's AI coding assistant, wrote practically all of the code, the tests,
the measurement scripts and the drafts of the documentation.** I did not write the code by hand.

My part is direction and control: the ideas, goals and requirements, the rules the assistant has to follow, the
test documents and questions for fundstelle, approving every plan, choosing between measured options, checking the
programs on my PC and on other computers, accepting each stage, and Git.

→ Who does what, how a stage runs, and what works well or needs care: **[ai-workflow.md](ai-workflow.md)**

## Timeline (2026)

| When | What |
|---|---|
| 6 Nov | fundstelle started; GPU check passed; PDF import and full-text search |
| 13–14 Nov | pc-agent: from the first commit to a tested Windows program with setup and installer |
| 15 Nov | pc-agent: two tool packages, a check on an NVIDIA PC, a first version of voice input |
| 17 Nov | fundstelle: better context for the model, then answers with checked quotes (stage 3) |
| 26 Nov | both projects on GitHub (private); this showcase |

## Kurz auf Deutsch

Die KI-Werkstatt zeigt zwei Projekte, die gerade entstehen. **fundstelle** beantwortet Fragen zu eigenen
PDF-Dokumenten, immer mit Datei, Seite und geprüftem Zitat. **pc-agent** erledigt alltägliche Aufgaben am PC mit
einem Satz, aber nur mit freigegebenen Werkzeugen und nach einer Bestätigung. Beides läuft vollständig lokal auf der
eigenen Grafikkarte. Den Code hat praktisch vollständig Claude Code geschrieben; Ziele, Regeln, Testdaten,
Entscheidungen, Prüfungen auf echter Hardware und Abnahmen liegen bei mir. Beide Projekte sind in Entwicklung, der
Quellcode ist vorerst privat.

## Thanks

To **Kevin**, coach at [neue fische](https://www.neuefische.de), who led the AI day of my training course there and
shared his `CLAUDE.md` template. It became the starting point for the rules Claude Code follows in both projects.

---

© 2026 Heinz Danner. No licence has been chosen yet, so normal copyright applies.
The texts in this repository were drafted by Claude Code from the project documentation and reviewed by me.
