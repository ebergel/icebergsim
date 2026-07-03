---
id: map
title: The IcebergSim Program in Plain Words
isbrs: program
kind: map
status: draft
version: 0.4.0
date: 2026-07-03
updated: 2026-07-03
tags: [isbrs/program]
---

# MAP.md — The IcebergSim Program in Plain Words

**DRAFT v0.3 — work in progress. History: the umbrella repo's changelog.**

**The rule of this document:** everything here must be understandable by a
smart reader who knows nothing about the project. If a section cannot be
written simply, the thinking behind it is not finished yet. This document is
that test, applied to the whole program. When the map and reality disagree,
reality wins and the map gets updated.

---

## 1. The names

**People:**

- **EB** — Eduardo Bergel. Statistician and epidemiologist. Author of the
  program.
- **DS** — David Sackett. Co-developer of the original simulator. Deceased.
  A founding figure of this work.
- **Claude** — the AI collaborator in conversation: design, critique,
  documents.
- **CCd** — Claude Code: the same AI working inside codebases:
  implementation. Two roles, one model.

**Software registry:**

| Handle | Plain description | Built by | Status |
|---|---|---|---|
| **ISM_RCT_W** | The original IcebergSim: a Microsoft Windows application that simulates randomized clinical trials. | EB + DS, with an international consortium | Historical. The ancestor. No longer developed. |
| **ISM_RCT_R** | The modern rebuild of ISM_RCT_W: a Python engine with a React web interface, public on GitHub, regenerated from a written specification (spec version 2.0.0-alpha.1). | EB + CCd | Live and public. |
| **ISM_LD_alfa** | The first working lie detector for trial data. Steps 1–6 of a 12-step plan built; 101 tests passing; one planted tampering caught at p ≈ 0.0006. Commit `cf694b1`. | EB + Claude + CCd | Proof of concept. Freezes as the sealed museum specimen once its quarry is extracted (the benchmark lie + test ideas). |
| **ISM_LD_beta** | The second lie detector, built fresh — not ported — under a two-page constitution (CONSTITUTION-LD.md): a hard shell around the core principles, declared freedom everywhere else. Carries the matured ideas that alfa predates. | EB + Claude + CCd | In construction. The active codebase. |
| **ISM_LD_PNX** | Reserved name: the future Phoenix consolidation of the lie detector — specification extracted, code regenerated and proven — once beta has stabilized into an instrument with a validated soul, exactly as ISM_RCT_R's was. | EB + Claude + CCd | Reserved. Not started, deliberately. |

**Naming rules:**

1. Pattern: `ISM_{lineage}_{variant}`. Lineages so far: **RCT** (the trial
   simulator) and **LD** (the lie detector). New lineages get short codes
   when they become real code — not before.
2. Handles name **artifacts** — things you can point at. Identity and
   version numbers live in **specifications** (example: the detector's spec
   will carry its own version line, proposed `LIESPEC 0.1.0-alpha.1`). So
   future releases of the rebuilt detector stay ISM_LD_PNX with new spec
   versions; we do not mint a new handle per release.
3. The variant slot is practical, not taxonomic: it records whatever most
   distinguishes the artifact (W/R = platform; alfa/PNX = development
   method). The spelling *alfa* is deliberate — it names the hand-grown
   specimen, and keeps it distinct from version words like "alpha.1".
4. ISM_LD_alfa freezes forever at `cf694b1` once its quarry is extracted.
   Handles are never reused; PNX waits for the consolidation it names.
5. Translation from older documents: "ICEBERGSIM v2" = **ISM_RCT_R**;
   "Stage 1" = **ISM_LD_alfa**; "the regenerated implementation" =
   **ISM_LD_PNX**; "the fresh build" = **ISM_LD_beta**.
6. GitHub and the domain: **the domain names the program; repos name
   lineages; handles name stages.** `icebergsim.com` points at the umbrella
   repo `ebergel/icebergsim`, whose face is this map — the program's front
   door. Living lineages get marked repos: `icebergsim-rct` (the
   simulator), `icebergsim-integrity` (the detector, hosting ISM_LD_beta
   and later ISM_LD_PNX in one history). Museums are GitHub-Archived
   side-vaults, read-only with the banner on: `icebergsim-classic`
   (ISM_RCT_W); optionally `icebergsim-integrity-alfa`. Repo
   **descriptions stay in plain language** — the shop window for
   strangers, no internal handles (the repo's name already sits right
   above them). The handle lives instead in one README line per repo
   ("Part of the IcebergSim program · handle: ISM_…"), maintained in the
   repo layer so nobody has to remember a Settings field; the canonical
   handle→repo registry is this map. Public names avoid
   verdict-shaped words: the detector's repo says *integrity*, never *lie
   detector*. Renames are free only until first share — publication is the
   one-way door for names too, so the renaming happens before any link
   leaves the house.
7. Live demos run on **lineage subdomains**: `rct.icebergsim.com` serves
   the simulator app and its embeddable chart widgets;
   `integrity.icebergsim.com` is reserved and stays empty until the
   constitution's no-claims-before-calibration law allows a public demo.
   The front door stays static. An embedded widget URL freezes — host,
   path, and parameters together — the moment any external page publishes
   it.
8. Documents carry **manifests**: every markdown file in the program opens
   with a small metadata block (its id, lineage, kind, status, version or
   date — schema in SOP-DOCS.md), so the whole paperwork can be poured
   into tables and queried like data. Ids never change; artifacts get
   version numbers, events get dates; history lives in changelogs and in
   git, never in headers. The Obsidian vault sees the repos through a
   window (`70 Repos/`), never through copies.

---

## 2. What we have done

**The simulator (years ago).** EB and DS built ISM_RCT_W: a flight
simulator for clinical trials. Before running a real trial — years of work,
millions of dollars, patients' lives — you simulate thousands of versions of
it and watch what your design choices do: how many patients you need, how
often chance alone would produce a false positive, what happens when
patients drop out, switch treatments, or get lost along the way.

**The rebuild, and the method (2026).** EB and CCd rebuilt the simulator as
ISM_RCT_R, now public on GitHub. The product matters less than the method
used to build it, which we call the **Phoenix**:

1. Write the rules of the program in documents, precisely.
2. Turn every important behavior into a test with a known answer.
3. Generate code until every test passes.
4. The proof: delete the code, regenerate it from the documents alone, and
   every test must pass again.

The documents are the permanent thing; code is a print-out. ISM_RCT_R passed
this proof, which certified two things at once: the method works, and we now
own a machine that can produce unlimited *honest* simulated trials — which
the lie detector will need (§4, step 1).

**The lie detector (in parallel).** ISM_LD_alfa examines the data of a
randomized trial and asks one question: *does this data look like it came
from the trial that was declared — or has someone tampered with it?* Three
ideas make it work:

- **The committed seed.** Random assignment in a trial comes from a random
  number generator, which starts from a seed. If that seed is published
  before the trial starts — like a sealed, dated envelope — then afterwards
  anyone can regenerate the exact assignment sequence and check that it
  matches what the trial reports. If the allocation was tampered with, the
  check fails. Not "probably fails": fails. One cheap habit turns a whole
  class of fraud from deniable into impossible to hide.
- **Two independent detectors.** Detector A checks the *consequences of the
  design*: given how patients were assigned, certain patterns must hold, and
  A hunts for violations. Discriminator B ignores the design and reads the
  *texture of the numbers*: real clinical data has a texture that fabricated
  data struggles to fake. They look at different things, so a lie must fool
  both at once.
- **A lie generator.** To measure a detector you need lies with known
  answers. The generator plants realistic tampering into simulated trials —
  subverted allocation, deleted patients, reclassified outcomes — so we can
  measure exactly what gets caught and what slips through.

Status: Steps 1–6 of 12 built; 101 tests pass; the detector caught a planted
allocation tampering with a signal that honest data would produce about six
times in ten thousand (p ≈ 0.0006).

**The decision (July 2, 2026).** ISM_LD_alfa grew by hand and by
conversation. Good enough to prove the idea; not good enough to be trusted
as an integrity instrument. A tool that audits other people's data must
survive an audit itself. So: rebuild it under the Phoenix, exactly as the
simulator was rebuilt. Two documents were written to govern that:

- **INTENT.md** — the constitution. It states what the detector is
  *supposed* to be and why, in numbered clauses, each tagged by how sure we
  are of it (anchored / inferred / open). It binds nothing until EB ratifies
  it clause by clause — because it was compressed from memory of design
  conversations, and memory is lossy.
- **PHOENIX-PORT-PROMPT.md** — the operating instructions for CCd. Step by
  step: verify the original first; freeze the p ≈ 0.0006 catch as test case
  zero; write the specification; classify all 101 tests; seal off the
  original code; rebuild from the specification alone; prove the rebuild
  behaves identically, bit for bit. With hard stop rules, so the loop halts
  and asks instead of improvising. Wherever the code disagrees with the
  constitution, it files a numbered "drift" item for EB to decide — it never
  decides alone.

**The premortem and the turn (July 3, 2026).** Before firing, a
high-altitude review asked how the plan could fail — and the plan failed the
review. The Phoenix consolidates finished things: it worked for ISM_RCT_W
because years of use and expert validation had given that program a soul
worth extracting; writing its specification was collecting a receipt for
validation already paid. Alfa holds no such receipt — it is an
exploration-stage prototype, six steps of twelve, whose ideas we have since
outgrown. Porting it would have preserved a larva. Decision: do not port.
Build fresh — **ISM_LD_beta** — with Claude Code at full speed inside a
short, hard constitution. The two port documents are shelved, not wasted:
INTENT.md's confirmed clauses were compressed into the constitution, and
PHOENIX-PORT-PROMPT.md waits as the kit for the eventual PNX consolidation.
The map records the road, including the turns.

---

## 3. What we are doing now

**Building ISM_LD_beta.** In order:

1. **Extract the quarry from alfa** (about an hour): the exact recipe of
   the planted tampering behind the p ≈ 0.0006 catch — kept as the
   **benchmark lie** that beta must also catch, reporting its own calibrated
   number — plus alfa's 101 tests as a mine of ideas for new test cases.
   Ideas are ported; code is not. Then alfa seals at `cf694b1`.
2. **EB signs CONSTITUTION-LD.md** — a short constitution: thirteen laws
   (regimes always labeled; no verdicts; every statistic passes a
   null-calibration gate before merging; no p-value quoted deeper than
   calibration reaches; the seed kernel held sacred; full reproducibility;
   no power claims before false-alarm rates; messy-honest calibration; the
   ancestor pristine; real data behind glass; everything the system does
   pours into tables anyone can explore by eye; a mathematical core of pure
   functions, testable atom by atom; real datasets enter only through a
   sealing procedure, and exposure is a one-way street), exactly three
   human gates, three stop rules, and the freedoms declared as loudly as
   the laws.
3. **Claude Code builds, with high autonomy.** EB supervises by feedback
   loop, not pre-approval, except at the three gates. Failing fast is
   policy, inside the shell.

The north star that scores every decision: **time to the first false-alarm
rate** — the first honest number of the form "on N messy-but-honest
simulated trials, the instrument flags X%." Everything is either on the
critical path to that number or it is ceremony.

---

## 4. The road ahead (for ISM_LD_beta, in order)

1. **Count the false alarms** — the north star. Run the detector over
   thousands of honest
   simulated trials from ISM_RCT_R — especially *messy* honest ones, with
   dropouts, non-compliance, crossovers — and measure how often it flags
   innocence. Real trials are messy, and mess mimics fraud. A detector that
   cannot tell mess from tampering is an accusation machine, and its errors
   cost reputations. No claim about detection power is allowed before this
   number exists.
2. **Map the blind spots.** Which kinds of tampering, at what size, in
   trials of what scale, can it see — and not see? Publish the blind spots
   along with the catches. That map is honest science whichever way it comes
   out.
3. **Teach both tools stepped-wedge trials.** The Mozambique trial (step 6)
   used a stepped-wedge design — treatment rolled out to clusters in a
   randomized order over time — which neither tool reads yet. Without this,
   the real test cannot happen.
4. **Sharpen against an adaptive adversary.** Let the lie generator see the
   detectors and learn to evade them — with the committed seed always out of
   its reach, because in the real world the seed is protected by publication,
   not by trust. Caution recorded: this sharpens the instrument but can
   never certify it. Self-testing is self-graded homework.
5. **External fire.** Someone who is not us plants a hidden number of lies
   across many datasets; the detector must call them; the sealed answer key
   opens only afterwards.
6. **The real trial.** Mozambique: a very large real trial EB led (published
   in *The Lancet*, 2018; about 218,000 clinic visits). In strict order:
   first check that our simulated honesty matches the texture of real
   honesty; then plant known lies inside the real data (locally, privately)
   and measure detection amid true operational noise; and only then run the
   detector, untouched, on the real trial — with the rules for interpreting
   whatever it flags **written down before anyone looks**. The detector will
   probably flag something innocent in real data. What we do about that must
   be decided in advance, or the exercise is theater.

---

## 5. The long-term objective

Medicine learns what is true from randomized trials. Today the integrity of
a trial rests mostly on **trust**: reputation, peer review, institutions.
Those are all forms of opinion, and opinion can be flattered, pressured, or
fooled.

The long-term objective is to move part of that weight from trust onto
**verification**: checks that give the same answer no matter who runs them,
and no matter how important the author is.

Concretely:

- A public, calibrated, audited instrument that can **verify** a trial's
  allocation outright when a committed seed exists, and put honest numbers
  on the evidence of tampering when one does not — with known false-alarm
  rates and published blind spots.
- A policy argument made undeniable by working code: **committing the
  randomization seed should become standard, near-zero-cost trial
  infrastructure**, the way trial registration became standard. Adopted
  widely, it makes one entire class of fraud mechanically impossible to
  hide.
- The instrument held to the standard it imposes: rebuilt from open
  documents, reproducible by strangers, tested by adversaries, and pointed
  at its author's own trial first.

**What it will never do:** deliver verdicts. It flags anomalies and attaches
the numbers; judgment stays with humans — investigators, editors,
regulators. A flag is a reason to look, never a finding.

One more branch belongs on the long-term map, separate from the lie
detector: a new statistical test (working name: the *unified-asymmetry
test*) that judges a trial by its whole pattern of outcomes at once, instead
of the convention of a single "primary outcome." It exists as mathematics
and design, not yet as code. It gets a handle (ISM_UA_…) when it becomes
real. Mozambique is its natural first target too.

---

## 6. The documents

- **MAP.md** — this file. The plain-language map of the program.
- **CONSTITUTION-LD.md** — the governing document for ISM_LD_beta:
  thirteen laws, three gates, three stop rules, and the freedoms. Short.
  Binding once EB signs.
- **SOP-DATA.md** — the standard procedure for sealing every real dataset
  that enters the program: vault on GitHub, pin by hash, codebook, declared
  role (exam or calibration), exposure log, registry. Born from the
  Mozambique seal; applies to all that follow.
- **ANC-SEAL.md** — the first seal: the Mozambique trial pinned by commit
  and hash, role EXAM, blind. The reference implementation of the SOP.
- **INTENT.md** — shelved. Its confirmed clauses live on inside the
  constitution; the full document waits as source material for the PNX
  consolidation.
- **PHOENIX-PORT-PROMPT.md** — shelved. The kit for the eventual PNX
  consolidation, once beta has a soul worth extracting.
- The **specifications** live with their code: ISM_RCT_R's `spec/` is
  public on GitHub; ISM_LD_beta's constitutional tests will live in its
  repo; ISM_LD_PNX's `spec/` will be born at consolidation.
