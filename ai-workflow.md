# How these projects are built — with Claude Code

## In short

Both projects are built with **[Claude Code](https://claude.com/claude-code)**, Anthropic's AI coding assistant,
working directly on my PC. Claude Code wrote practically all of the source code, all automated tests, the
measurement and evaluation scripts and the drafts of the documentation, and it ran most of the tests and
measurements. I did not write the code by hand.

I decide what gets built and whether it is good enough: goals and requirements, the rules Claude Code has to
follow, the test data for fundstelle, approval of every plan, the choice between measured options, checks on real
hardware, acceptance of each stage, and Git.

"Built with AI" alone says little, so this page shows how the work is split, steered and checked.

## Who does what

| Task | Me | Claude Code |
|---|---|---|
| Ideas, goals, target users | decide | asks questions, points out risks and gaps |
| Requirements and architecture documents | set the direction, approve | writes and maintains them |
| Rules for the assistant (`CLAUDE.md`) | set them | follows them |
| Plan for each stage, with acceptance criteria | approve or change | proposes |
| Source code and automated tests | — | writes them |
| Test documents and questions (fundstelle) | chose the documents, provided the 25 questions | adds automatic evidence checks |
| Measurement and evaluation scripts | — | writes them |
| Measurement runs | approve; run them on other computers | runs them on my PC on request |
| Choosing between options | decide; a few choices delegated on purpose and documented as such | lays out options with numbers, recommends one |
| Checks in the real program | real launches, tests on other PCs, final judgement | window checks when I delegate them |
| Accepting a stage | ✔ | — |
| Git: commits and pushes | ✔ | only when I ask for that specific commit or push |
| These showcase pages | review and publish | wrote them from the project documentation |

## How a stage runs

1. **Plan.** Claude Code writes a short plan with acceptance criteria: tests, measurement targets, what is out of
   scope. Nothing is built before I approve it.
2. **Build.** One checkable step at a time, each with automated tests.
3. **Measure.** The fixed test set runs before and after the change. Results go into a measurement log — only
   numbers from real runs, never estimates.
4. **Decide.** If there are options, Claude Code lays them out with numbers and a recommendation; I choose.
5. **Check and accept.** I check the result in the real program (or delegate a specific check) and accept the
   stage.
6. **Commit.** Claude Code points out a good moment for a commit; I run Git myself or ask it to make that one
   commit. Commits name Claude as co-author with a `Co-Authored-By` line. The earliest commits of both projects
   lack it, but everything on this page applies to them as well.

## Rules Claude Code works under

Each project has a `CLAUDE.md` file that Claude Code reads at the start of every session. The key rules:

- Plan first, wait for approval, one checkable step at a time.
- No Git commands unless I ask for that specific task.
- No sub-agents, plugins, extra tool servers, downloads or package installs without asking; every new dependency
  gets a licence check before it is added.
- Only synthetic or public test data; my real document folder is outside Claude Code's working area.
- No secrets in code or output, no open ports, the local model server only on 127.0.0.1.
- No invented numbers: every measurement comes from a run.

Claude Code works with Anthropic's cloud models, so the code and documentation it works on are sent to Anthropic
during development. The software being built is different: at run time, fundstelle and pc-agent only talk to the
local model.

## Memory between sessions

An AI session forgets. Three documents carry each project from one session to the next: `requirements.md` (what and
why), `architecture.md` (every decision with its reason and status) and a log of measurements and decisions. Claude
Code keeps them up to date; for me they are also the easiest way to follow and check what was done.

## Example: how pc-agent started

pc-agent began as a question of mine during work on fundstelle: could the AI do everything I can do on my PC, not
just search PDFs? Claude Code pointed out what an AI with all of my user rights could do wrong. My answer was to
separate that risk: an agent of its own for a limited set of everyday actions — copy this, prepare that mail, open
YouTube. I set the goals (Windows, Linux and macOS; AMD and NVIDIA; one program that sets everything up with
confirmations), and the safety model was worked out before the first line of code.

## What works well, and what needs care

**Works well**

- Speed: pc-agent went from the first commit to a tested Windows program with setup and installer in two days.
- Thoroughness: tests and measurements are cheap to write, so there are many of them — more than 1,100 automated
  tests across both projects.
- Honest numbers: measuring before and after each change keeps both of us from fooling ourselves. For example, a
  plausible verification step changed nothing until it was restructured.

**Needs care**

- AI writes convincing code and text whether it is right or not. Tests, measurements and checks in the real program
  decide; several problems only showed up when someone used the real window.
- Rules are not self-enforcing. Claude Code occasionally slipped (once it ran a read-only Git command without
  asking); I point it out, and the rule is reinforced in the project memory.
- I steer, read and judge the work, but I did not write it line by line — which is why the tests, the measurements
  and the documented decisions matter so much.
- Legal questions around AI-written code (copyright, licensing) are still open and part of the licence decision.

---

[← Back to the overview](README.md)
