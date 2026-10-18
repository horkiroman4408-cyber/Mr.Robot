# Mr. Robot

**[ ENG ](./README.md)** | **[ RUS ](./README.ru.md)**

A working prototype for warehouse file work — a single HTML file that makes
routine tasks faster than Excel macros and manual copy-paste.

It's not a finished product, but it's not a mockup either. Everything described
here runs, and you can try it right now in your browser.

It's shared for two reasons: so other people building similar tools can take
ideas from it, and so anyone who sees a better way can send feedback or code
back.

If this helps you — good. If you want to help it grow — also good.

![status](https://img.shields.io/badge/status-working%20prototype-success)
![version](https://img.shields.io/badge/version-3.6.4-blue)
![Auto-update](https://img.shields.io/badge/auto--update-enabled-brightgreen?style=flat-square)
![runs in](https://img.shields.io/badge/runs%20in-your%20browser-0a84ff)
![offline](https://img.shields.io/badge/offline-ready-success)
![single file](https://img.shields.io/badge/single--file-HTML-orange)
![vue](https://img.shields.io/badge/vue-3-42b883)
![Privacy](https://img.shields.io/badge/privacy-100%25_local-blue?style=flat-square)

> **Try it now:** [open the live version](https://horkiroman4408-cyber.github.io/Mr.Robot/) — it runs entirely in your browser, no install, no sign-up.


## Contents

- [What it is](#what-it-is)
- [Try it](#try-it)
- [Why it exists](#why-it-exists)
- [Speed](#speed)
- [Modules](#modules)
- [How it's built](#how-its-built)
- [Running it](#running-it)
- [Helping each other](#helping-each-other)
- [What's next](#whats-next)
- [Credit](#credit)
- [Author](#author)


## What it is

Mr. Robot is a browser app that does warehouse file work — parsing reports,
comparing two big spreadsheets, filtering locations, calculating KPIs, exporting
clean results.

It's a working prototype. Not a concept, not a slide deck. You can open it
right now and use it on real files.

It's one file. No install, no server, no build step. You open `index.html` and
it works. Everything runs on your machine; nothing is uploaded anywhere. Files
you load stay in your browser, and they're still there after a page reload.

The point isn't that it's the biggest or most polished tool. The point is that
it's the kind of thing one person can put together in a browser today, and that
this changes what a "quick internal tool" can look like.


## Try it

Live version — runs entirely in your browser, no install, no account needed:

**[Open Mr. Robot](https://horkiroman4408-cyber.github.io/Mr.Robot/)**

You can also download `index.html` and open it locally. It works offline.


## Why it exists

If you've worked with warehouse reports, you know the pattern. A file arrives
as `.xlsx`. Someone opens it in Excel, applies filters, copies columns into
another file, runs a VBA macro — until the macro breaks after an Excel update.
Then everyone does it slightly differently, and no two people get the same
numbers.

I wanted to see what happens if that whole loop lives in a browser instead.
What if parsing 50k rows took under a second? What if the filters were defined
once, in code, so everyone got the same result? What if a daily routine that
takes half an hour could be done in one click?

That's what this prototype tries to answer. It's not a replacement for a real
production system — it's a working sketch of what one might look like.

### Open by design

This isn't a closed internal tool. It's shared so it can grow both ways — from
what other people know, and towards what other people need. If you've solved
a similar problem in a smarter way, I'd like to hear about it. If something
here saves you a week of trial and error, just take it — no credit needed.


## Speed

This is the part that matters most.

### What usually slows people down

| Task | The usual way |
|------|---------------|
| Open a 50 000-row `.xlsx` | 10–30 seconds, sometimes freezes |
| Apply filters and remap columns | Done by hand, error-prone |
| Compare two large files | Copy-paste, VLOOKUP, waiting |
| Produce a clean export | Reformatted manually every time |
| Repeat it tomorrow | Same amount of time again |

### What this prototype does instead

| Task | Mr. Robot |
|------|-----------|
| Open a 50 000-row `.xlsx` | Parsed off the main thread — the UI stays responsive |
| Filters and column mapping | Defined once in code — always the same result |
| Compare two large files | In-memory hash maps — linear-time lookups |
| Produce a clean export | One click → styled `.xlsx` or `.csv` |
| Repeat it tomorrow | Filters and files are remembered |

### Rough numbers

Not exact benchmarks — just the general scale of difference seen while
building this:

- Parsing large Excel files: seconds → well under a second, and without
  freezing the page.
- Cross-referencing two 100k-row files: minutes of VLOOKUP → instant.
- A daily routine (open → filter → export): around 15–30 minutes → around
  30 seconds.
- Reproducibility: manual steps replaced with deterministic code, so
  copy-paste errors stop happening.

The claim isn't "this is the fastest tool ever". The claim is that a browser
can already do this — in one file, offline, with no install — and that alone
changes what a small internal tool can be.


## Modules

The app is a hub with four sections. Each one replaces a recurring task.

### KPI Norms — employee performance

Load `.xlsx` reports by drag and drop, combine them with a schedule file,
filter by group, process or shift, and read the numbers.

Sub-modules:

- **Audyt** — KPI and INFO breakdown
- **Scalanie** — KPI for merging / picking
- **Rozkładanie** — KPI for distribution, with RSORT and Returns detection
- **NADWE / VAS** — KPI with two rows per login
- **Statistics** — one view across all processes: rankings, efficiency,
  median, average

What it does well:

- Norm thresholds based on the median, adjustable per process
- Top-3 / Top-5 / Top-10 rankings
- Coloured Excel export with conditional formatting
- Filters built from the schedule file (group, process, shift)

### RS — Tote Finder

Compares two large databases in memory.

Sub-modules:

- **MP → RS Tote Finder** — matches EANs from MP to TOTE locations in RS
- **Search totes by EAN** — paste a list, get TOTE and inventory quantity
- **AUDYT GEEK** — reads a Stocktake order file and reports on it without
  exporting anything

Details that matter:

- Median or minimum-quantity strategy when picking a TOTE
- Multi-tote detection and filtering
- 2×2 pop-tote awareness
- Copy to clipboard and Excel export

### MP — Audit and merging

Sub-modules:

- **AL_AUDYT** — KPI and INFO from an audit report
- **FORMATKA_59** — quality control format with its own metrics
- **GODZINY_MDT** — MDT analysis, shelf 1/1, location lists
- **STOCK** — location reports grouped by receiving hours
- **Scalanie** — filter locations by shelf, ABC, SKU range
- **Konsolidacja** — find small locations worth consolidating

Notes:

- Where a VBA macro already existed, the logic is matched to it, so the
  numbers line up with what people were used to.
- Clipboard copy is there so results can be pasted straight into Excel or a
  WMS.
- CSV files are exported with the exact filenames downstream tools expect.

### Other

- **Analiza_Przestojów** — downtime analysis per USER ID, 8 to 300 minutes
- **ARTLTT** — paste product names, get LTT files as CSV
- **TH Reports** — report generation and parsing (in progress)


## How it's built

A few decisions that make it fast:

- Everything ships in one file. Vue, Tailwind, SheetJS and the Web Workers
  are all inlined. No CDN, no build step, no runtime dependencies.
- Excel parsing runs in a Web Worker, so the interface doesn't freeze on
  large files.
- Cross-referencing uses hash maps, which turns repeated lookups into
  linear-time work.
- State is reactive in memory, and files are persisted to IndexedDB so a
  reload doesn't lose context.
- The logic is deterministic — same input, same output, for anyone who uses
  it.


## Running it

Live version:

**[Open Mr. Robot](https://horkiroman4408-cyber.github.io/Mr.Robot/)**

Or run it yourself:

1. Download `index.html`.
2. Double-click it, or drag it into a browser.
3. That's it.

To host it yourself, fork the repo and turn on GitHub Pages in
**Settings → Pages**.

Needs a modern browser — Chrome, Edge, Safari or Firefox. Nothing else.


## Helping each other

This repo is a prototype, shared openly. It can go both ways.

### What this might give you

If you're building something for warehouse or inventory work, here are the
ideas most worth taking:

- A single `index.html` that anyone can run beats a repo that needs Node,
  Docker and CI for a tool used by five people.
- Parsing `.xlsx` is CPU-heavy. Moving it into a Web Worker keeps the UI
  smooth on huge files.
- Two large files joined in memory beat every VLOOKUP you'll ever write.
- IndexedDB makes a page reload feel like nothing happened.
- Filters and formulas in code mean every person gets the same numbers.
- If a routine takes twenty clicks, everyone will do it differently. If it
  takes one, everyone does it the same way.

Use them, adapt them, rewrite them in your own stack. If any of this ends up
in something you build — a note, a link back, or just a message saying hello
would be genuinely appreciated. It's not required, but it does make the work
feel worth sharing.

### What would help this project

If you'd like to help it grow, here's what's genuinely useful:

- **Ideas.** A smarter way to filter, a module that's missing, a workflow
  this doesn't cover yet.
- **Bug reports.** A file that doesn't parse right, a KPI that looks off, an
  edge case that breaks something.
- **Pull requests.** Small fixes, new filters, or an entirely new
  sub-module.
- **Feedback on the design.** What feels confusing, what feels slow, what
  feels wrong.
- **Other languages.** The UI is in Polish and English. More are welcome.
- **Real data.** The prototype works best when it's pushed by real files
  from real warehouses.

If you're working on something similar, open an issue and say hi. I'd rather
compare notes than work in isolation.


## What's next

Done so far:

- [x] KPI dashboard with statistics and rankings
- [x] Multi-file cross-referencing (Tote Finder)
- [x] In-app audit analysis without exporting to Excel
- [x] Persistent file storage with IndexedDB
- [x] Off-thread Excel parsing with Web Workers

Planned or under consideration:

- [ ] TH Reports module
- [ ] PDF export
- [ ] Batch processing of multiple files
- [ ] User-defined formulas and filters
- [ ] Optional cloud sync (opt-in)


## Credit

This prototype is free to read, learn from and build on. There's no license
gate and no legal requirement to mention the author.

That said — if you take code, ideas or whole modules from here and put them
into something of your own, it would be really nice if you left a small credit
somewhere (a link, a name, a mention in your README). Not because it's owed,
but because it's how small open projects stay motivated to keep sharing.

If you'd rather just say hello and tell me what you built with it, that works
too. Open an issue or reach out — I'd like to see it.


## Author

Raman Horki

> If you do the same thing twice — automate it.

Open to feedback and collaboration. If you have thoughts, open an issue in
this repository.


© 2026 Mr. Robot · Made by Raman Horki

A working prototype — shared with two wishes: that it helps someone, and that
someone helps it grow. If you build on it, a small credit back is always
appreciated — never required.
