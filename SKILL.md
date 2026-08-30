---
name: j-user-readiness
description: >-
  Visual and comprehension review of a screen or a set of screens — the sibling
  of j-QA, asking the opposite question. j-QA asks "does it work and is it
  true?"; this asks "can somebody who has never seen this screen understand it
  in ten seconds, and would you put it in front of a buyer?" Measures the real
  type sizes, widths, grouping and state markers from the source rather than
  judging by eye, fills every form with realistic values before scoring (an
  empty form hides the problem), hunts the cross-cutting root cause before
  proposing per-screen patches, and ends in one published before/after artifact
  plus a handover message a build agent can act on. Invoke when the user says
  "how does this look", "make it demo-ready", "the screen is confusing", "review
  the UI design", "j-user-readiness", or asks for fonts / sections / colours /
  spacing / panel width to be improved.
---

# j-user-readiness — is this screen ready for a human?

`j-QA` proves a feature **works and tells the truth**. It is deliberately
function-over-form. This skill is its sibling and asks the opposite question:

> **Can somebody who has never seen this screen understand it in ten seconds,
> and would you be happy showing it to a buyer?**

A screen can pass every j-QA rung and fail every item here.

---

## The one rule

**Measure, don't vibe.** "Feels cramped" is not actionable and cannot be argued
with. "The panel's only heading style is 10px at 60% opacity, and it is shared
by the title" is a finding somebody can fix. Read the actual classes and
computed sizes out of the source. Most polish defects are **a token applied at
the wrong level**, not a matter of taste — and saying so is what makes the
review land instead of sounding like an opinion.

## Three habits that produce most of the value

**1. Fill every form with realistic values before you judge it.**
An empty form hides its own problem. Values reveal the hierarchy: which text is
actually biggest, where a real string truncates, which rows waste space on one
short value, and whether you can tell what you have changed. Use *real* data
from the running product — a real record, real names, real amounts — not
"Lorem" and not "Test 1".

**2. Look for the root cause across screens before proposing per-screen fixes.**
Score every screen, then put the measurements side by side in one table. The
pattern usually names itself: one caption-size token used as the default for
labels; no shared scale so each file invents its own; panel widths chosen
independently. **When the root cause is systemic, the first task is not a
screen — it is the shared thing.** Fixing one screen in isolation leaves it
looking unlike its neighbours, and makes the remaining screens *more* expensive,
not less.

**3. Say what is already good, with the same evidence standard.**
A report of only defects invites somebody to rebuild a working screen. Name the
healthiest screen measured and the components that are doing their job.

---

## The 24 checks

Each gets **PASS / WEAK / FAIL** plus one line of evidence — a measured number
(px, count, scroll depth) wherever a number is possible.

### A · Typography & hierarchy (1–6)
1. **The screen names itself prominently.** The title of what you are editing is
   the most, not least, prominent text. Fails if the title shares a class with
   minor labels.
2. **Three distinct levels exist** — title / section heading / field label —
   different in size *and* weight, not weight alone.
3. **Body and label text is ≥13px.** 12px is a caption size; a surface a
   professional uses daily should not be built on it. Count the distinct sizes:
   more than four is noise, fewer than three is flat.
4. **Nothing load-bearing sits below 12px.** 10px uppercase muted is decoration,
   not instruction.
5. **Contrast is sufficient on anything you must read.** Muted-at-60%-opacity is
   for hints, never headings or values.
6. **Sentence case for headings**, ALL-CAPS reserved for short eyebrow labels.

🔴 **Check the direction of the hierarchy, not just its existence.** Shared form
primitives often render *values* larger than the labels and headings authored
around them — so the most disposable text (a value the user just chose) ends up
loudest and the orienting text faintest. **This inversion is invisible on an
empty form** and is the single most common finding this skill produces.

### B · Grouping & structure (7–12)
7. **Controls are grouped into named sections** of 3–5, not one flat stack.
8. **The groups match how a user thinks** — *who decides · how long they get ·
   what if nobody acts · special cases* — not the order the fields were built in.
9. **Related controls sit together.** A setting expressed as a percentage of
   another must be adjacent to it.
10. **Progressive disclosure earns its place.** If "More" hides two things while
    eight sit above it, the split is in the wrong place.
11. **Reading order matches doing order** — identity, main decision, refinements.
12. **Section boundaries are visible** — a rule, a card, or real whitespace.

*Before proposing a restructure, check whether the structure already exists in
the markup and is merely invisible. Headings styled into oblivion are common,
and "make the existing headings visible" is a far cheaper, lower-risk fix than
"reorganise the panel".*

### C · Colour, state & emphasis (13–17)
13. **Overridden-vs-inherited is visible at a glance.** On any settings surface
    with defaults, this is the single most valuable marker: *this one is not the
    default*.
14. **Consequential settings look different from cosmetic ones.** Anything that
    can move money or act automatically should not look like a label change.
15. **Colour carries meaning consistently** and never alone — pair with an icon
    or text.
16. **Errors appear where the offending control is**, not only in a panel
    elsewhere. If a validation summary names an item, that item should show it.
17. **The primary action is visually primary**, and disabled states say why.

### D · Space, density & scroll (18–21)
18. **Everything needed for the common task fits without scrolling** at
    1366×768. Measure the depth at which the last essential control sits.
19. **Container width suits its densest row.** If a control is clipped or
    squeezed, the container is too narrow — widening beats truncating. Check
    whether it has already been widened once; that is evidence, not coincidence.
20. **Short fields share a row.** A number and a percentage each taking a full
    row spends vertical space that scroll then has to pay for.
21. **No horizontal scrolling**, and no value clipped by layout — test with the
    longest *real* option string, not the placeholder.

### E · Language & explanation (22–24)
22. **Every label is plain English** — no internal jargon, no API field names.
23. **Explanation is visible, not hover-only.** Load-bearing help hidden in a
    tooltip means the screen reads as unexplained until probed.
24. **Empty and first-run states teach.** A brand-new item shows what to do
    next, not an empty form. A verb with no object ("Escalate") should name the
    object ("Escalate to the next level up").

---

## How to run it

**Phase 0 — scope and measure.** List the screens. For each, read from source:
the distribution of font sizes, the count of section headings, container widths,
the number of controls. Put them in one table. **This table is the deliverable
that decides the order of work.**

**Phase 1 — open the real screens.** Log in, navigate, and look. Fill the forms
with real values. Where a screenshot is awkward, the accessibility tree plus the
source classes is enough to reconstruct faithfully.

**Phase 2 — score against the 24.** Evidence per item. Never score from memory
of how a framework usually looks — read this codebase's own primitives, since
the shared Input/Select/Label sizes set the baseline everything else fights.

**Phase 3 — one artifact, not one per screen.** Publish a single page:
- a faithful **before** of one exemplar screen, rendered at the sizes the code
  actually specifies (reproduce them; never caricature — the critique dies the
  moment somebody spots an exaggeration), beside a **proposed** version;
- for the remaining screens, the **specific changes** with the measurement
  behind each. No mockup per screen — the pattern is established by the exemplar.
- state plainly, near the top, that **nothing has been built** and which changes
  need new state versus pure styling.

**Phase 4 — a prioritised work list**, ordered by (systemic first) → (worst
measurements, cheapest fix) → (highest demo value) → (most careful work last).
Mark each item small/medium. Separate any item needing information the screen
does not already render; it can ship as its own later phase without blocking
the rest.

**Phase 5 — the handover message.** A pasteable block carrying: the artifact
link, the root-cause finding with its table, the decisions the owner has made,
the ordered list, and a short "things not to lose" section naming what already
works. Ask the owner any question whose answer changes the work list **before**
writing it — width and phasing decisions are the usual two.

---

## Working with the owner

- **Show, don't describe.** A side-by-side at real sizes settles in five seconds
  what three paragraphs cannot.
- **Ask about anything that changes the plan**, not about anything else: one
  width or several? does the item needing new state ship now or later?
- **Correct yourself in public when the measurement contradicts your first
  read.** Discovering that the sections already exist, or that the values are
  larger than the labels, makes the finding sharper and the fix cheaper — both
  are better news than the original complaint.

## Relationship to the other skills
- **`j-QA`** — does it work, is it true, does it persist, did it land in the
  backend. Run that first; a screen that lies is not a polish problem.
- **`adversarial-review` / `feature-impact-sweep`** — read the code for defects.
  This skill reads the code only for *sizes, widths and structure*.
- Findings here are **design proposals**, not defects. File them where the
  project files design decisions, and never in the defect log as though they
  were bugs.
