# Workshop Runbook — Copy-Paste Prompt Playbook
## Claude for PMs: From Messy Inputs to Shippable Decisions
### Terraloom scenario — facilitator copy

---

> **How to use this doc**
> Every prompt below is ready to copy and paste directly into Claude. Run them in order in a single Claude Project session that has company.md, product.md, and personas.md already loaded. Prompts are numbered by module. Facilitator notes appear above each prompt in italics. Timing targets are in the section headers.

---

## Pre-session setup (before attendees join)

*Do this before the workshop starts. Takes about 5 minutes.*

**Step 1:** Create a new Claude Project. Name it: `Terraloom PM Workshop — [Date]`

**Step 2:** Upload these three files into the Project knowledge:
- `company.md`
- `product.md`
- `personas.md`

**Step 3:** Load the four input files into a folder you can access during the session:
- `leadership-memo.md`
- `support-tickets.md`
- `posthog-data.md`

**Step 4:** Open this runbook in a separate window. During the workshop, you will copy prompts from here and paste them into Claude.

**Step 5:** Test that context is loaded by running this warm-up check:

---

### SETUP — Context warm-up check

*Run this before the session opens. Confirms the project context is live.*

```
You have three context files loaded for this session: company.md, product.md, and personas.md. Before we begin any analysis, confirm you have access to all three by returning:

1. Company name and current strategic focus (from company.md)
2. The single most important tech constraint affecting PM decisions today (from product.md)
3. The names of all three personas and one sentence on each persona's biggest frustration (from personas.md)

If any file is missing or unclear, tell me now before we proceed.
```

---

---

# MODULE 1 — Build the context pack
## 0:08 – 0:23 | 15 minutes

---

### M1-1 — Context quality check

*Run this live while participants are writing their own context files. Show the output and walk through what Claude flags.*

```
I have loaded three context files into this Claude Project: company.md, product.md, and personas.md. They describe Terraloom, a B2B SaaS platform for architecture and construction project management.

Before we use these files for any analysis, audit each one for quality:

For company.md:
- Is the strategic focus specific enough to make a prioritization decision from?
- Is the NOT-doing list concrete or vague?
- Would a new team member reading this know exactly what is out of scope?

For product.md:
- Are the known pain points honest and specific, or sanitized?
- Are the tech constraints actionable for a PM making a scoping decision?
- Are the open questions real questions or safe ones?

For personas.md:
- Is each JTBD specific enough to anchor a feature decision?
- Is the biggest frustration concrete or generic?
- Would an engineer reading this know who they're building for?

Return a health score for each file: Strong / Acceptable / Needs work
Then flag the single most important gap across all three files — the one that would most hurt our analysis if we don't address it.
```

---

### M1-2 — Sharpen a weak area (use if M1-1 flags something)

*Only run this if the quality check surfaces a real gap. Good to show live — demonstrates the iteration loop.*

```
You flagged that the personas file has a weak JTBD for Devon, the field superintendent. His current JTBD is too focused on drawing access and doesn't capture the downstream consequence of getting the wrong drawing on-site.

Rewrite Devon's JTBD using this additional context: Devon's core risk is not that he can't find drawings — it's that he acts on the wrong drawing without knowing it. By the time he finds out, work has already been done incorrectly. The cost is measured in rework, material waste, and inspection failures — not in inconvenience.

Rewrite the JTBD to capture that consequence. Keep the format: When [situation], I want to [motivation], so I can [outcome].

Then rewrite his "biggest frustration" and "what success looks like" to match the revised JTBD. Be specific and honest.
```

---

---

# MODULE 2 — Synthesize the inputs
## 0:23 – 0:43 | 20 minutes

*This is the core module. You will paste all three input sources into Claude in sequence. Keep the session open — context compounds.*

---

### M2-0 — Prompt comparison demo

*Before running the real synthesis, show this contrast. Paste the weak prompt first, let it run, then paste the strong prompt. The difference in output sells the module.*

**Weak prompt (show this first):**

```
Here are some support tickets from Terraloom. Can you summarize what customers are saying?

[paste first 10 rows of support-tickets.md]
```

**Strong prompt (run this immediately after):**

```
Ignore the previous summary. We are starting the real synthesis now.

I am going to give you three sources of input about Terraloom's product problems. I will paste them one at a time. Do not analyze anything until I say "BEGIN SYNTHESIS." Confirm you understand and are ready for the first input.
```

---

### M2-1 — Load source 1: Support tickets

*Paste this prompt, then paste the full contents of support-tickets.md into Claude.*

```
Here is Source 1: 41 support tickets from July 1–8, 2025.

[PASTE FULL CONTENTS OF support-tickets.md HERE]

You have received Source 1. Do not analyze yet. Confirm receipt and wait for Source 2.
```

---

### M2-2 — Load source 2: PostHog data

*Paste this prompt, then paste the full contents of posthog-data.md.*

```
Here is Source 2: PostHog product analytics covering the last 90 days.

[PASTE FULL CONTENTS OF posthog-data.md HERE]

You have received Source 2. Do not analyze yet. Confirm receipt and wait for Source 3.
```

---

### M2-3 — Load source 3: Leadership memo

*Paste this prompt, then paste the full contents of leadership-memo.md.*

```
Here is Source 3: A memo from Rob Callahan, CEO, dated July 8, 2025.

[PASTE FULL CONTENTS OF leadership-memo.md HERE]

You have received Source 3. You now have all inputs. Wait for the BEGIN SYNTHESIS command.
```

---

### M2-4 — BEGIN SYNTHESIS

*This is the main event. Run it after all three sources are loaded. While Claude generates, narrate what each clause in the prompt is doing.*

```
BEGIN SYNTHESIS.

You have three sources: 41 support tickets, 90 days of PostHog analytics, and a leadership memo from the CEO. Each source is telling a different story about what Terraloom should prioritize.

Using the context from company.md, product.md, and personas.md:

1. Identify 5–7 recurring themes across all three sources. For each theme return:
   - Theme name (3–5 words, specific not generic)
   - Which source(s) surfaced it: tickets / PostHog / leadership / multiple
   - Signal count or data point that supports it
   - One verbatim quote or specific data reference
   - Confidence level: High / Medium / Low
   - Any signal from a DIFFERENT source that contradicts or complicates this theme

2. After the themes table, add a "Source conflicts" section:
   - Where does the CEO memo point in a different direction than the ticket data?
   - Where does PostHog data surface a problem that tickets have NOT caught yet?
   - Where do tickets surface urgency that the PostHog data does NOT show?

3. Final line: "The single most dangerous assumption in this analysis: [one sentence]"

Return the themes as a markdown table. Return the source conflicts as numbered prose.
```

---

### M2-5 — Contradiction deep-dive

*Run this after the synthesis output lands. Pick the most interesting contradiction the room is debating.*

```
You surfaced a conflict between the CEO's reporting request and the mobile drawing sync failures from the ticket data.

Go deeper on this specific tension:

- The CEO is responding to one account ($340K ARR, 45-day renewal). How many field superintendent tickets this week describe consequences — rework, wrong materials, safety incidents — that are arguably higher severity than losing that renewal?
- What type of PM reasoning would lead someone to prioritize the reporting dashboard? What would they have to believe about churn risk, relationship leverage, and engineering cost?
- What type of PM reasoning would lead someone to prioritize mobile sync? What would they have to believe about the same variables?
- What single data point, if you had it, would make this decision obvious?

Do not tell me which to prioritize. Show me the sharpest version of both arguments.
```

---

### M2-6 — Surface the silent bomb

*Run this to make the PostHog dependency bug land with the room. This is the "nobody filed a ticket because they don't know" moment.*

```
The PostHog data shows a task dependency corruption pattern — tasks are silently deleted when a parent task is marked complete. 201 active users are affected. The data estimates 1,400–1,800 tasks have been silently lost in 90 days.

Cross-reference this with the ticket data:

- How many tickets explicitly reference task disappearance?
- What does the language in those tickets tell you about whether users understand WHY tasks are disappearing?
- If a user doesn't know tasks are disappearing silently, what behavior would you expect to see — and does the ticket data show that behavior?
- How many of the 201 affected users have filed any ticket at all?

Then answer: why is a bug that has deleted 1,400+ tasks generating only 31 support tickets? What does that tell us about the true scope of the problem versus what support data alone would show?
```

---

*Deliverable checkpoint — say this to the room:*
> "What you just built is Artifact 02 — a themes table with evidence, confidence levels, and source conflicts. Screenshot the output or copy it. We will use it in the next module."

---

---

# MODULE 3 — From signal to solution
## 0:43 – 1:03 | 20 minutes

*Stay in the same Claude session. The context from Module 2 is still live.*

---

### M3-1 — Quick rank

*Run this first. While it generates, tell the room: "Claude is about to rank these. Your job is to override at least one ranking and write one sentence explaining why."*

```
Based on the synthesis we just completed, here are the three candidate initiatives:

1. Cross-project reporting dashboard (CEO request — Meridian Group renewal, $340K ARR, 45 days)
2. Mobile drawing sync fix (Support tickets — 6 critical escalations, field safety incidents, stale drawing rate 19–51% depending on conditions)
3. Task dependency data integrity fix (PostHog — silent task deletion, 201 affected users, 1,400–1,800 tasks lost, mostly invisible to users)

Rank these three using this framework:
- Strategic fit: how directly does this address our stated focus — retention and NRR in the 150–300 seat tier?
- Revenue exposure: what ARR is at risk if we don't act, and how certain is that estimate?
- User impact severity: how bad is the consequence for the user when this problem occurs?
- Engineering cost signal: based on what product.md tells us about our tech constraints, what is the relative complexity of each?

Return a ranked table with one sentence of rationale per initiative. Then add: "My least confident ranking is [X] because [reason]."
```

---

### M3-2 — PM override

*After the ranking lands, run this. Have the room suggest which ranking to override and why. Type their reasoning into the prompt.*

```
I am overriding your ranking. Here is my decision and rationale:

I am moving the mobile drawing sync fix to #1. Rationale: The PostHog stale rate (19% overall, 51% on Android cellular) combined with 6 critical ticket escalations in 7 days — including a field superintendent who used a draft drawing for a concrete pour — represents active safety risk and active churn signal. The CEO's reporting request is real but serves one account. The mobile fix serves every field superintendent in our mid-market segment, which is our growth tier.

Acknowledge this override. Then: given my reasoning, what assumption am I making that could be wrong? Give me one specific data point I could get within 30 days that would tell me if that assumption is correct or incorrect.
```

---

### M3-3 — Stress-test the top bet

*This is the most important prompt in Module 3. Run it on whatever the room decides is #1. Read the output aloud.*

```
My top-ranked initiative is: Fix mobile drawing sync — specifically, the stale version problem where the mobile app serves cached drawings that are not the current published version, with a 19% average stale rate and 51% stale rate on Android cellular in low-signal environments.

Argue against prioritizing this now. Specifically:

- What in the support ticket data actually cuts against making this the top priority?
- Is there any signal that field superintendents are adapting workarounds that reduce the urgency of a platform fix?
- What would have to be true about engineering complexity (based on product.md's tech constraints) for this to be the wrong bet?
- What is the strongest argument for doing the task dependency fix first instead — and whose interests does that argument serve?
- If we ship the mobile sync fix and it doesn't improve field adoption, what did we miss?

Do not soften this. Give me the strongest version of the counter-argument.
```

---

### M3-4 — Write the solution brief

*Run this after the stress-test. Tell the room: "Notice the structure — every section requires evidence. No unsupported claims."*

```
Write a one-page solution brief for the mobile drawing sync fix.

Use this exact structure:

**Problem statement:** One sentence, present tense, anchored to Devon (field superintendent persona from personas.md). Do not use passive voice.

**Evidence:**
- Ticket data: specific count, severity, and one verbatim quote with ticket ID
- PostHog data: the stale rate numbers by platform and network condition
- Business consequence: what the data shows about churn correlation after a stale drawing event

**Target persona:** Devon. One sentence on why we are solving for him first and what that means for Marcus (PM persona) as a secondary beneficiary.

**Proposed approach:** Plain language. What are we actually fixing — the cache invalidation logic, the sync trigger, the version hash check, or all three? Do not use jargon. If you don't have enough technical detail to be specific, say so and flag it as an open question.

**What we are NOT building in this release:**
- List at least three explicit exclusions
- Include one exclusion that someone on the team will definitely ask for

**Key risks:**
- The two most likely technical failure modes based on product.md constraints
- The one user behavior assumption that could make the fix irrelevant

**Definition of done:** What would make this a clear win, measurable within 60 days of ship?

No unsupported claims. Every evidence point must trace back to a specific ticket ID, PostHog metric, or context file section.
```

---

### M3-5 — Constraint pass

*Inject a real engineering constraint. This shows compounding context — Claude redesigns using everything from the session.*

```
New constraint from the engineering lead: the Android sync issue is rooted in how the mobile app handles version hash checks — and the mobile app is a separate React Native codebase. Any fix to the Android stale rate requires a dedicated mobile sprint and cannot be parallelized with web work. We have one mobile engineer available this quarter.

Given this constraint, redesign the solution brief:

- Does the problem statement change?
- Does the scope change — should we ship an iOS-first fix and follow with Android, or is that worse for the persona?
- Does the definition of done change?
- What new risks does this constraint introduce that weren't in the original brief?
- Is there anything in the brief that is now impossible this quarter?

Return a revised brief. Mark every section that changed with [REVISED]. Flag anything that is now uncertain that was previously settled.
```

---

*Deliverable checkpoint:*
> "Artifact 03 is your ranked shortlist with PM rationale. Artifact 04 is your solution brief v2 — the one that survived the constraint pass. Both came from the same session, no copy-paste between tools."

---

---

# MODULE 4 — Flat screens for engineering
## 1:03 – 1:13 | 10 minutes

*This module is a live demo. You drive. Participants watch and take notes. The teaching moment is the contrast between what a prototype gives an engineer versus what a flat screen artifact gives them.*

---

### M4-1 — Generate the flat screen artifact

*Run this. While it generates, say: "We're asking for four screens — the states any engineer needs to build against. Static HTML. No interactivity. No aesthetics. Just clarity."*

```
Based on the solution brief for the mobile drawing sync fix, generate a flat screen HTML artifact for the key user journey.

This artifact will be handed directly to the engineering team. Design for handoff clarity, not visual polish.

Requirements:
- Single HTML file, no external dependencies, no JavaScript, no CSS frameworks
- Four screens, each as a clearly labeled section with a visible screen name as a heading
- Screens to include:

  Screen 1 — Drawing list (current state, synced)
  The field superintendent opens the Terraloom mobile app on a project. All drawings are current. Show: project name, list of drawing sets with version number and "Last updated" timestamp, a visible sync status indicator (green, "Up to date — synced 4 min ago"), and a primary CTA to open a drawing.

  Screen 2 — Drawing list (stale state — the broken experience)
  Same view, but the app is serving a cached version that does not match the current published version. Show: the same drawing list, but the sync indicator is amber with the text "Last synced 3 days ago — tap to refresh." Add a banner: "Some drawings may not be current. Tap any drawing to verify before use." Show a visible version mismatch warning on one drawing set.

  Screen 3 — Drawing open (version conflict detected)
  The superintendent taps a drawing. The system detects that the cached version does not match the current published hash. Show: a full-screen modal that says "This drawing has been updated since you last synced. You are viewing version 4 of 6. Download current version before use?" with two buttons: "Download current" (primary) and "View cached version" (secondary, with warning text: "Version 4 — may not reflect current approved details").

  Screen 4 — Sync error (no connection)
  The superintendent attempts to sync on a low-signal cellular connection and the sync fails. Show: an error state with the message "Sync failed — no connection. You are viewing drawings from [date]. Verify with your project manager before use." Include a retry button and a "View offline drawings" secondary option.

For each screen, include inline annotations — small bracketed notes next to key elements explaining: what the element does, why it is there, and what the engineer needs to know about the logic behind it.

At the top of the file, add a "For engineering" section that lists:
- Which screen maps to which acceptance criteria
- The specific version hash check behavior that screens 2 and 3 depend on
- Known edge cases the engineer needs to handle that are not visible in the UI
```

---

### M4-2 — Engineer-perspective review

*Run this immediately after the artifact generates. This is the QA pass — and often the most valuable moment in the module.*

```
Review the flat screen artifact you just generated as if you are the engineer receiving this for the first time.

You have never been in a product meeting. You have not read the solution brief. This artifact is your primary context for implementation.

Flag:
- Any screen where the expected behavior is ambiguous — where you would have to guess what should happen
- Any state that is missing that you would have to invent on your own to ship something coherent
- Any annotation that is too vague to write an acceptance criteria test against
- Any element where it is unclear whether the logic lives in the frontend, backend, or native app layer
- Any edge case that is implied by the design but not explicitly called out

Then return a "Handoff readiness" score:
- Ready to ticket
- Ready with one revision
- Missing critical detail — do not ticket yet

Include the single most important thing to fix before this goes to engineering.
```

---

### M4-3 — Generate a specific edge state (if time allows)

*Only run this if you have 3+ minutes remaining in the module. Good for showing iteration speed.*

```
Add a fifth screen to the artifact:

Screen 5 — Partial sync (some drawings current, some stale)
The superintendent opens the drawing list and the sync has completed for some drawing sets but not others — for example, because a large drawing file timed out on a slow connection. Show: the drawing list with a mixed state — some drawing sets show a green "Current" badge, others show an amber "Sync pending" badge. Include a section-level banner: "3 of 7 drawing sets are not current. Tap to retry." Add an "Impact on AC" note explaining how this state changes the acceptance criteria for the sync logic.
```

---

*Deliverable checkpoint:*
> "Artifact 05 is your flat screen artifact. Engineering gets this file, not a Figma link. Notice how short the acceptance criteria just got — because the screen says most of it."

---

---

# MODULE 5 — Tickets for engineering handoff
## 1:13 – 1:21 | 8 minutes

*Stay in the same session. The brief and flat screens are in context.*

---

### M5-1 — Generate the ticket set

*Run this. Tell the room: "Every field in these tickets traces back to something we built in the last hour."*

```
Convert the solution brief and flat screen artifact into implementation-ready engineering tickets for the mobile drawing sync fix.

For each ticket, use this exact structure:

**Title:** [Action verb] + [specific object] — no vague titles like "Fix sync issue"
**Context:** Why this ticket exists. Reference the specific brief section and the PostHog stale rate data that motivated it.
**Acceptance criteria:** Specific and testable. Reference flat screen states by name (e.g., "matches Screen 2 stale state"). No acceptance criteria that use the word "correctly" or "properly."
**Dependencies:** What must ship first or be resolved before this ticket can be completed. Name them explicitly.
**Edge cases to handle:** Pull from the flat screen annotations and the engineering review.
**Out of scope for this ticket:** At least one explicit exclusion.
**Estimated size:** S / M / L. If L, flag it and propose a split before returning.

Generate tickets for:
1. Version hash check — the logic that detects whether the cached drawing matches the current published version
2. Stale state UI — the amber sync indicator, the banner, and the per-drawing version mismatch warning (Screen 2)
3. Version conflict modal — the full-screen modal when a superintendent opens a stale drawing (Screen 3)
4. Sync failure error state — the no-connection error and offline fallback (Screen 4)
5. Push notification trigger — the notification that fires when a drawing is updated and the user has that drawing cached

If any ticket is estimated L, split it before returning. Return the split tickets as separate entries with clear sequencing.
```

---

### M5-2 — Scope check

*Run this immediately. Read any gap aloud to the room.*

```
Review this ticket set for gaps and scope problems.

- Is any ticket doing more than one thing?
- Is there anything in the solution brief that is not covered by any ticket?
- Are there dependencies between tickets that are not surfaced?
- Does the set, taken together, fully ship what the solution brief defines as the definition of done?
- Is there anything the PostHog data flagged — specifically the Android vs iOS differential — that the tickets do not address?

Return a gap analysis in three bullets or fewer. Then return a revised ticket list if any changes are needed.
```

---

### M5-3 — Split a large ticket (if needed)

*Only run if M5-1 flagged an L ticket.*

```
The push notification trigger ticket is estimated L. Split it into smaller tickets that:
- Can each be tested independently
- Have clear sequencing — which ships first, which is blocked by what
- Do not duplicate acceptance criteria

The split should reflect what product.md tells us about the notification system: it is event-driven but not user-preference-aware. Any notification work that requires rebuilding the preference layer is out of scope for this sprint.

Return the split tickets in the same format as the original set.
```

---

*Deliverable checkpoint:*
> "Artifact 06 is your ticket set. Note that every AC references a specific screen state. That's because Artifact 05 existed first."

---

---

# MODULE 6 — Automate the loop + evals + team handoff
## 1:21 – 1:30 | 9 minutes

*The shift: you just ran this manually. Now you'll write the recipe that makes it run every month without starting from scratch.*

---

### M6-1 — Build the trigger file

*Run this first. While it generates, say: "This file is the 'start here' doc. Anyone on the team can pick this up next month without having been in this room."*

```
Based on the synthesis workflow we just completed, write a trigger file called run-synthesis.md.

This file will be used next month to run the same synthesis with fresh data. Write it so that a PM who was not in today's workshop could pick it up and run the full workflow correctly.

It should include:

1. What inputs to load before starting (list file names, expected format, and where to get each one)
2. Which context files to verify are current before running (and what "current" means — if product.md hasn't been updated in 60+ days, flag it before running)
3. The synthesis prompt to run, verbatim and ready to copy-paste, with placeholders clearly marked: {{DATE_RANGE}}, {{TICKET_COUNT}}, {{PRODUCT_AREA}}
4. What confidence threshold should trigger a human PM review before acting on output (define this concretely — not "low confidence" but a specific condition)
5. The format the output should return in (reference the output template)

Write it as a markdown file. Plain, clear, no jargon. This is an SOP, not a design doc.
```

---

### M6-2 — Build the standing prompt

*Run immediately after M6-1.*

```
Template the synthesis prompt we ran in Module 2 into a reusable monthly prompt.

Replace these values with placeholders:
- The date range → {{DATE_RANGE}}
- The number of tickets → {{TICKET_COUNT}}
- The product area → {{PRODUCT_AREA}} (default: pull from product.md)
- The current quarter focus → {{QUARTER_FOCUS}} (default: pull from product.md)

Add an instruction block at the top:
"Before running this prompt: (1) update all placeholders above, (2) confirm company.md, product.md, and personas.md are loaded in the Claude Project, (3) load all three input sources and confirm receipt before running BEGIN SYNTHESIS."

Return the full templated prompt, ready to copy-paste next month.
```

---

### M6-3 — Build the output template

*Run immediately after M6-2.*

```
Create a structured output template called synthesis-output-template.md.

Claude should return results in this exact format every time the monthly synthesis runs:

---
## Monthly Synthesis — {{PRODUCT_AREA}} — {{DATE_RANGE}}

### Themes table
| Theme | Source(s) | Signal count / data point | Confidence | Representative quote or metric | Contradicting evidence |
|-------|-----------|--------------------------|------------|-------------------------------|------------------------|

### Source conflicts
[Numbered list — where do the three input sources disagree? One conflict per line.]

### Top 3 signals this month
[The three things a PM most needs to act on — ordered by urgency, not importance]

### Silent risks
[Signals in the data that most users haven't noticed yet — the PostHog-type findings]

### Recommended bet
[One sentence — the initiative most supported by this month's combined evidence]
**PM action required:** Confirm / Override / Needs more data

### What changed since last month
[Only fill in on second run and beyond]

---

Add a note at the top: "If Claude's output does not match this structure, ask it to reformat before using the output."
```

---

### M6-4 — Self-eval: score this output before you act on it

*This is the evals moment. Run it against the themes table from Module 2. Read the score table aloud.*

```
Score the synthesis output we produced in Module 2 on these four dimensions. Return a table with: dimension, score (1–5), and one-sentence rationale.

Scoring dimensions:

1. Theme clarity — Are the themes specific enough to act on, or so broad they could mean anything?
   1 = theme name could describe any product / 5 = theme name maps directly to a specific engineering decision

2. Evidence quality — Is each theme backed by specific quotes, ticket IDs, or PostHog metrics — or just paraphrasing?
   1 = all assertions, no citations / 5 = every theme has a verbatim quote or specific metric

3. Contradiction coverage — Did the analysis find at least one signal that challenges or complicates each major theme?
   1 = no contradictions surfaced / 5 = every theme has at least one counter-signal named

4. Recommendation confidence — Is the recommended bet traceable to specific evidence, or is it a generalization?
   1 = "we should probably focus on X" / 5 = "PostHog stale rate + 6 critical tickets + churn correlation = mobile sync is #1"

Do not inflate scores. 3 means acceptable. 4 means good. 5 means you could defend this in a board meeting.

After the table: "If any dimension scored below 3, identify which prompt produced the weak output and suggest one specific change to the prompt that would improve the score on the next run."
```

---

### M6-5 — Build the eval rubric file

*Run this to create the reusable quality standard file.*

```
Create a file called eval-rubric.md.

This file is the quality standard for all Claude synthesis outputs on Terraloom. It will be pinned in the Claude Project so every team member references the same standard.

Include:

1. The four evaluation dimensions (theme clarity, evidence quality, contradiction coverage, recommendation confidence), each with:
   - A one-sentence definition
   - What a score of 1 looks like — use a specific bad example from today's session if possible
   - What a score of 5 looks like — use a specific good example from today's session if possible
   - The minimum acceptable score before a PM should act on the output (set this yourself — do not default to 3 for everything)

2. A "When to re-run" section: three specific conditions where the PM should discard the output and re-run synthesis rather than manually fix it

3. A "When to update context files" section: conditions where the output suggests company.md, product.md, or personas.md needs updating before the next run — for example, themes that don't map to any existing persona, or contradictions that suggest the strategic focus has shifted

Write it as plain markdown. No jargon.
```

---

### M6-6 — Team handoff SOP

*Only run if you have 3+ minutes left. Strong close — participants leave with something they can send to a teammate today.*

```
Write a one-page onboarding SOP called team-handoff.md for a PM joining the Terraloom Claude Project for the first time.

They are a strong PM but have never used Claude for synthesis work. They were not in today's workshop.

Cover:
1. What this project contains and what each file does (context files, prompt library, trigger file, output template, eval rubric)
2. How to run the monthly synthesis — step by step, with file names and prompt references
3. How to interpret the output — what to act on immediately, what to flag for discussion, what score triggers a re-run
4. How to know when the context files are stale and what to do about it
5. The one habit that matters most: run the eval rubric before acting on any output

Length: one page. Tone: direct, no fluff. Assume the reader is smart and short on time.
```

---

---

# WRAP — 1:28 – 1:30

*Read the artifact list on the final slide. Then say:*

> "Every one of these came from the same Claude session, the same fictional company, the same 90 minutes. This isn't seven separate tasks. It's one workflow — and it runs again next month by you or anyone on your team."

**Artifacts built today:**
1. Context Pack — 3 files loaded into a Claude Project
2. Themes Table — evidence, confidence, source conflicts
3. Ranked Shortlist — PM rationale on the top bet
4. Solution Brief v2 — survived the constraint pass
5. Flat Screen Artifact — 4 annotated states for engineering
6. Ticket Set — implementation-ready, referencing flat screens
7. Automation Recipe — trigger file, standing prompt, output template, eval rubric

**Take-homes to distribute:**
- This runbook (workshop-runbook.md)
- The prompt library (full set including team and eval prompts)
- The three context file templates (blank versions for their own company)
- The eval rubric template

---

---

# BONUS PROMPTS — use anytime after the workshop

*These are not part of the 90-minute session. Share in the take-home prompt library.*

---

### BONUS-1 — Stakeholder update: exec (3 sentences)

```
Write a 3-sentence exec update on the mobile drawing sync fix for Rob Callahan, CEO.

Lead with business impact, not product detail. Reference the PostHog stale rate and the critical ticket escalations — but translate them into business language. End with what you need from leadership, if anything. No implementation language.
```

---

### BONUS-2 — Stakeholder update: GTM and sales

```
Rewrite the mobile drawing sync brief as a 3–4 sentence update for the sales and customer success team.

Focus on what changes for the customer — specifically for field superintendent users and the project managers who manage them. No technical detail. No internal framing. Write in the customer's language: what stops going wrong, what they can count on that they couldn't before.
```

---

### BONUS-3 — Stakeholder update: engineering kickoff

```
Write an engineering kickoff summary for the mobile drawing sync fix.

Cover: what we're building and why (reference the PostHog stale rate and the 6 critical ticket escalations), the constraints that shaped the design (React Native separate codebase, one mobile engineer available, Android cellular as the primary failure condition), open questions engineering needs to answer before starting, and where to find the flat screen artifact and ticket set.

Length: half a page. Tone: direct. Assume the engineering lead has read the tickets but not the brief.
```

---

### BONUS-4 — Address the CEO's request without building the dashboard

```
Rob's memo asked for a cross-project reporting dashboard. We have decided not to prioritize it this quarter. Write a response to Rob that:

1. Acknowledges the Meridian Group commercial situation directly
2. Explains what we are prioritizing instead and why — using the PostHog data and ticket severity as evidence
3. Proposes a specific interim action that addresses Meridian's immediate need without requiring engineering (for example, a manual CSV export workflow the CSM can run, or a dedicated customer success touchpoint before the renewal conversation)
4. Sets a concrete timeline for when reporting could realistically be resourced

Tone: direct, transparent, respectful of the commercial pressure. Rob does not want to be managed — he wants to understand the tradeoff. Write accordingly.
```

---

### BONUS-5 — Address the dependency bug proactively

```
The task dependency data corruption issue is currently invisible to most affected users — they don't know tasks are being silently deleted. We have decided to triage this as a follow-on fix after mobile sync.

Write a proactive outreach message to send to the 201 affected accounts. The message should:

1. Acknowledge the issue without alarming language — these users don't know there's a problem yet
2. Tell them what happened in plain language (parent task completion triggered deletion of dependent tasks)
3. Tell them what to do right now to assess their projects (check project timelines for unexpected gaps)
4. Set a timeline for the fix
5. Offer a direct support contact for accounts who want to audit their data

Tone: transparent, calm, accountable. This should read like a message from a PM who respects the customer's time, not a legal-reviewed incident notice.
```

---

### BONUS-6 — Update context files after the session

```
Today's workshop surfaced several things about Terraloom's current state that should update our context files.

Based on what we learned in synthesis today:
- The mobile drawing sync issue is now a known critical problem with a defined fix in progress
- The task dependency bug is a known issue being triaged
- The CEO's reporting request has been acknowledged and deferred with a proposed interim action

Update product.md to reflect:
1. The mobile sync fix as the current top engineering priority with a one-sentence description of the fix
2. The dependency bug as a known issue in the backlog
3. A revised "open questions" section that removes any questions we answered today and adds any new ones surfaced

Flag anything in the current product.md that is now stale or contradicted by what we learned. Return the full updated file.
```

