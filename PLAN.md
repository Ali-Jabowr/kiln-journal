# Kiln — the plan

Settled in a grilling session on 2026-10-02. This file is the plan. When something changes, change it here.

## What this is

A plan I keep for the long run, with **Go as the foundation** and every other engineering skill built on top of it: system design, Kubernetes, architecture, AI. It continues whatever job I have. Most of the time I work at set times, and I can also pick it up any free hour or day off and carry on from where I stopped.

**Goal:** get hired by a strong company, Go backend at big tech (Yandex / Ozon / Avito), by becoming really good, not by collecting certificates.

## Core rules

1. **Learn by building.** I read theory only when the code in front of me needs it.
2. **I type every line of Go.** AI is my senior advisor and Go teacher: it explains, reviews after I've written the code, and gives hints. It never writes the solution.
3. **Theory rule:** when I'm stuck, I get a ≤10-min lesson on my own code plus **one** source to go deeper. I read only one book at a time, and only the chapters I need now.
4. **Learned means used.** A concept goes into `LEARNED.md` only with a link to the file or commit where I used it.
5. **There is one system: Kiln.** Every other tool either gets called by it or is archived.

## Time

- 6–8 h/week for now, and it can go up or down.
- The split between projects and algorithms changes week to week; there is no fixed ratio. Projects come first for now.
- **Reminder:** if algorithms or projects get 0 sittings for 14 days, the resume card says so once. It reminds me and never blocks me.

## A sitting

- **Open (≤2 min):** the resume card shows my last step, my next step and one recall question.
- **Work, sized to the time I have:**
  - ~25 min: one algorithm problem or one re-solve.
  - 60–90 min: one project slice.
  - A day off: several slices, plus 30 min reading a real codebase.
- **Close (mandatory, 2 min):** one line in `LOG.md`, plus **the next step in my own words**. Without this line, the next pickup breaks.

## Go milestones ("comfortable/advanced" means these)

1. From an empty folder, with no AI, I build a CLI tool and an HTTP+JSON API, with tests.
2. A Postgres-backed service with migrations, sensible error handling and a clean package layout.
3. A concurrent pipeline using goroutines, channels, `context` cancellation and `errgroup`, with no warnings from the race detector.
4. Profiling and speeding up real code with `pprof` and benchmarks.
5. Explaining out loud, at interview level, how goroutine scheduling, interfaces, slice/map internals and the GC work.
6. About 100 LeetCode problems solved in Go.

## Algorithms track (serious, in Go)

- Work one pattern at a time: two pointers → sliding window → hashing → stack → binary search → trees → graphs → DP…
- **Spaced re-solves:** a problem I needed a hint for comes back after 3, 7 and 21 days, solved from a blank file.
- Every problem ends with a commit to `go-learning-log`.

## Project track

- A ladder of about 6–8 projects, then one flagship.
- The projects must be **real, modern systems** that would catch a big-tech reviewer's eye, not small Go exercises.
- They are designed in a **separate grilling session (2026-10-02, tonight)** and recorded in `LADDER.md`.
- System design, Kubernetes and observability come in because the projects need them.

**Project structure ritual (every project):**
1. Write 10 lines on what it does before writing any code.
2. Build a walking skeleton: `main.go` first, then the thinnest path that works end to end, then grow it.
3. Add packages (`cmd/`, `internal/`, …) only when the code forces it.
4. Mentor support fades along the ladder:
   - Projects 1–2: the mentor walks every step and explains why.
   - Projects 3–5: I decide and the mentor reviews.
   - Projects 6+: I work alone and the mentor reviews afterwards.
5. Read one good open-source Go codebase per project (30 min, guided) and compare it with my own structure.

**AI does not scaffold the Go projects.** Creating `go.mod` and deciding where `main.go` lives *is* the lesson.

## Kiln, the platform

- Atlas, reshaped and renamed. **AI builds all of it; I don't touch the platform code.**
- **This repo (`kiln-journal`) is the truth.** Kiln is a view over these files, plus buttons that write back to them. If Kiln is down, `/kiln` in Claude Code reads the same files.

**v1 scope:**
1. **Resume screen:** last step, next step, a recall question, Start.
2. **Ladder:** projects, slices with ✓, and the milestones each one proves.
3. **Drill:** Atlas's Go problem ladder, plus the spaced re-solve queue.
4. **Learned:** concepts linked to where I used them.
5. **Rhythm:** sittings per week, project time against algorithm time, streak. Facts only, no guilt.

**Later (not before v1 is in daily use):** resources library, theory notes, guided codebase reading, an in-app mentor.

**Build rule:** v1 is built the weekend of 2026-10-03/04 and then frozen. After that, changes go into one weekly session of ≤1 h, and only to fix friction from real use. No new features. Anything not built that weekend goes on the later list.

## Repos

- `kiln`: the platform code (Atlas renamed, history kept).
- `kiln-journal`: this repo. It holds `PLAN.md`, `LADDER.md`, `LOG.md`, `LEARNED.md` and notes.
- One GitHub repo per ladder project, so they're visible on my profile.
- `go-learning-log`: the algorithms.

## Old systems

- **Atlas:** becomes Kiln. Its theory nodes are frozen, and `/atlas` is replaced by `/kiln`.
- **Road to Seniority vault, AI-Builder Layer, Brain V2 learning paths/curriculum:** archived as superseded. They stay readable but are no longer the plan.
- **Own:** kept only for job code, i.e. learning the izicontrol codebase.
- **Teach (Hermes):** kept as the tool for "stuck → short lesson", feeding `LEARNED.md`.
- **Hermes `#atlas`:** renamed `#kiln`.

## Timeline

- **2026-10-02 (tonight):** projects grilling session → `LADDER.md`.
- **2026-10-03/04:** AI builds Kiln v1. I prepare for the izicontrol demo on my own; the demo comes before everything.
- **Monday:** izicontrol demo.
- **Tuesday:** first sitting. I write the first line of Go.
