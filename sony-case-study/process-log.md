# Process Log — Sony Music Take-Home Case Study

**Purpose:** The case study requires that any AI or technical tools be cited by program name, time allotted, and prompt used. This log records every working turn so the final submission can disclose AI assistance accurately and so the reasoning trail is reportable.

**Tool disclosure (standing):**
- **Program:** Claude Code (Anthropic), desktop app, model Claude Fable 5.1
- **Role of the tool:** repo setup, note-taking, structuring, drafting, and slide production under the candidate's direction. All diagnoses, prioritization, and tradeoff decisions are reviewed and owned by the candidate.
- **Other tools:** GitHub (private repo via `gh` CLI), Python `pypdf` (PDF text extraction)

**Time tracking:** Work is done in multiple sittings, not one continuous stretch. Each turn carries a timestamp and an estimate of active working minutes for that turn. Total active time is summed at submission for the AI-use citation; wall-clock gaps between turns are not counted. Turns 1–5 active time estimate: ~45 minutes combined.

---

## Turn 1 — 2026-10-07 12:12–12:25 EDT — Setup and intake

**Candidate prompt (verbatim):**
> @"/Users/tomleger/Downloads/Business Solutions _ Take Home Study .pdf"
> save this file this is the prompt i've been given by Sony Music for my case study for the interview process for Senior Business Solutions Specialist. go ahead and open up a repo on my github account --make it private
>
> lso open upa. file that will log all the turns and steps we take to solve this problem for reportage purposes
> We will be building a 2-5 slide deck
>
> see the instructions that were provided by Jack:
> [pasted cover email: 3–4 hours max, return within 24h, one-page summary or 2–5 slides, assessing approach to ambiguous problems / prioritization / scalable solution]

**Steps taken:**
1. Extracted the 3-page PDF text (no `pdftotext` on machine; installed `pypdf` into a scratch directory and parsed it).
2. Copied the original PDF into `source/` unchanged.
3. Wrote a clean, structured transcription of the brief to `docs/case-study-brief.md` so it can be referenced without re-parsing the PDF.
4. Created this process log.
5. Initialized git, created a private GitHub repo under account `legertom`, pushed initial commit.

**Observations from the brief that shape the work:**
- Deliverable must answer six numbered questions: diagnosis (3 hypotheses), discovery approach, future-state recommendation, standardization vs. tailoring, initial pilot, measures of success.
- Explicit constraints to honor: no single universal ingestion method, limited engineering capacity (custom build needs a business case), teams resist another disconnected tool, sensitive data needs access controls, AI assists but humans review uncertain decisions.
- The evaluators weight structure, prioritization, and tradeoffs over comprehensiveness or polish.
- A final-round live scenario will test how the candidate pivots assumptions, so the deck should surface assumptions explicitly.
- Citation of AI use (tool, time, prompts) is mandatory; this log is the source for that disclosure.

**Decisions:**
- Format: 2–5 slide deck (candidate's choice).
- Repo name follows the working directory: `ugc-dashboard`.

**Open items for next turn:**
- Agree the deck's storyline and slide allocation across the six questions.
- Decide production tool for slides (candidate preference needed).

---

## Turn 2 — 2026-10-07 12:49 EDT — Pace check and source of "three hypotheses"

**Candidate prompt (verbatim):**
> ok i think you're geting ahead of me so slow down a bit where did you get the idea for three hypotheses

**Response:** Pointed to assignment question 1 in the brief ("What are the three most important problems or hypotheses you would investigate?"). No work product produced. Held storyline and tooling decisions pending candidate review.

---

## Turn 3 — 2026-10-07 12:49 EDT — AI-proposed hypotheses for candidate review

**Candidate prompt (verbatim):**
> ok what do you think the three most important problems or hypotheses you would investigate

**AI-proposed hypotheses (drafts for candidate to accept, edit, or reject):**
1. Identifier and definition mismatch (platform IDs vs catalog IDs; inconsistent field meanings) drives most reconciliation cost. Regional trackers are a symptom. Fix if true: shared data dictionary + identifier crosswalk. Disproved if time study shows hours go to downloading/chasing, not matching.
2. A large share of tickets are status questions, not data defects, because feed freshness is invisible. Fix if true: per-feed freshness/status view with expected cadence. Disproved if ticket sample shows mostly genuine defects.
3. Ownership breaks at handoffs because it is assigned by team, not by feed and failure type, and intake lacks minimum fields. Fix if true: ownership matrix per feed + structured intake inside existing ticketing tools; AI triage only after intake is structured. Disproved if tickets are complete but stall on team capacity.

**Reasoning noted:** Each hypothesis is falsifiable (named evidence), each has a low-engineering fix, and together they map to data / visibility / support layers. Portal downloads and tool adoption deprioritized as standalone items.

**Status:** Awaiting candidate's reaction. Nothing committed to the deck yet.

---

## Turn 4 — 2026-10-07 13:09 EDT — Candidate lays out discovery approach

**Candidate prompt (verbatim):**
> ok idk if i agree with you but we can come back to this. lets cha tthis out. basically to work this problem I am going to make a list of every single data source that will go into this workflow and collect a sample of that data i..e what is the shape of the API, what do the csv files look like, whbat are the region teams' trackers like. then lets's figure out where are the overlaps (joins) and where are the orphans, and also identify metadata (generation time, delivery time, owner etc)
> I know Sony Music is rolling out Claude Cowork to everyone and Airtable as well, these are new tools so lets incoirporate them where posible.
> when interviewing stakeholders I am going to engage: the current owner of each data source, I'm going to ask them to map their workflow for how they gather their data source and I'm going to ask them how often they pull new data and i'm going to ask them how they validate it. Do they look at another source? Do they compare it to the previous period? If there is a discrepency who do they reach out to? When was the last time there was a discrepency and what happened? What do they do with the data once it is collected? Do they send it somewhere? How is it stored? then finally I'm going to ask them how long the process of collecting data takes and how often it happens and how many poeple in their team do this process that often. That will form the basis for our ROI calculation.
>
> Round 2 of discovery: Interview a representative of each anticipated audience/consumer of the data: leadership, product/eng/support, analytics, regiional and data teams, rights and content protection teams, and artist, label and marketing teams. I will ask them how do they consume the data. What is valueable to them about the data. I MAYb ask thenm to map a workflow for how they use the data. What do they wish they could have access to--additional data, visualizations, etc. Then I'm going to ask them what happens if they don't get the data on time or if it is wrong. What happened last time the data was wrong or late. How did they know and what was done to correct it? Finally I'll ask how long does it take them to find/access/use the UGC data, how often they do that, and how many people in the office perform this workflow.

**Candidate's approach (summary, candidate-originated):**
- Discovery step 1: inventory every data source with a real sample (API shape, CSV layout, regional trackers). Map joins/overlaps and orphans. Capture metadata per source: generation time, delivery time, owner.
- Discovery step 2 (Round 1 interviews): each data-source owner. Map their gathering workflow, pull frequency, validation method (other source? prior period?), discrepancy escalation path and last incident, downstream handling/storage, time per cycle × frequency × headcount (ROI basis).
- Discovery step 3 (Round 2 interviews): one representative per consumer audience named in the brief. How they consume, what is valuable, optional workflow map, wish list, impact of late/wrong data and last incident, how they detected it, time to find/access/use × frequency × headcount.
- Tooling direction: incorporate Claude Cowork and Airtable (candidate understands Sony is rolling both out) wherever possible.
- Candidate has not accepted the AI-proposed hypotheses from Turn 3; parked for later.

**AI feedback given (for candidate to accept or reject):**
- Strengths: inventory-first; metadata capture seeds the freshness view; producer/consumer split; ROI embedded in questions.
- Gaps suggested: add a ticket-sample stream (classify recent issues from all channels by type, completeness, hops, time to close); corroborate self-reported time with observation or a short time log; add Round 1 questions on access control, contractual cadence/format, field-definition drift, and duplicate pullers; add Round 2 question "how do you currently know if the data is current."
- Tooling: Airtable as registry/workflow layer (inventory, dictionary, crosswalk, intake form, views, automations), not as a data warehouse; Cowork for note synthesis, dictionary drafting, ticket classification, anomaly flagging, comms drafting, with human approval on rights/partner decisions. Frame rollout as a stated assumption.
- Deck compression: three discovery streams on one slide, each with questions answered and artifact produced.

**Status:** Discussion only. No deck content drafted.

---

## Turn 5 — 2026-10-07 13:13 EDT — Discovery decisions; registry vs. warehouse explained

**Candidate prompt (verbatim):**
> i'm ok with self reported time, I like your ticket discovery idea, that is round three of discovery so record that.
> Tell em more about "It's a registry and a workflow tool,"

**Candidate decisions (recorded):**
- Self-reported time estimates are acceptable; no observation or time-log corroboration.
- Ticket sample analysis adopted as **Round 3 of discovery**: pull recent issues from all channels, classify by type, completeness on arrival, routing hops, time to close.
- Discovery is now three rounds: (1) source owners, (2) consumer audiences, (3) ticket sample. Preceded by the source inventory and sample collection.

**AI explanation given — Airtable as registry/workflow layer, not warehouse:**
- Warehouse holds the data itself (every claim/view/match event; millions of rows/day; needs bulk load, aggregation, long retention). Airtable has per-base record ceilings and rate limits and no aggregation engine; raw feeds must not land there.
- Registry holds data about the data, one row per tracked thing. Proposed four tables: Sources (one per feed: owner, cadence, format, contract constraints, access level, last received, expected next, status), Fields (data dictionary linking platform field names to canonical definitions; records join/orphan analysis), Issues (structured intake form with required fields, linked to Source, owner inherited), Exceptions (orphan records needing human matching decision; a queue). Full ID crosswalk stays in warehouse; crosswalk rules and judgment cases live in registry.
- Workflow half: forms enforce minimum intake, automations route and flag overdue feeds, interfaces give each audience its own view, permissions enforce access control.
- Integration: pipeline monitoring updates Sources on feed arrival; Cowork reads Fields/Issues to draft definitions and classify, writes suggestions for human approval; warehouse unchanged.
- Noted link to assignment Q4: table structure and required fields = org-wide standard; contents of each Source row = where tailoring lives.

**Status:** Discussion only. Candidate has not yet confirmed Airtable registry design for the deck.

---

## Turn 6 — 2026-10-07 13:20 EDT (~10 min active) — Explaining assignment Q3; time-tracking change

**Candidate prompt (verbatim):**
> can you explain "Future-state recommendation: At a high level, how would you improve the movement of data from
> platform delivery through stakeholder access and issue resolution?"
>
> also I am busy today im not doing this all in one 3-4 hr stretch so dont keep time like that

**Process change:** Candidate is working in multiple sittings. Stopped elapsed wall-clock tracking. Log now records per-turn active-minute estimates instead; header updated.

**AI explanation given (Q3):**
- Q3 asks for the end-to-end pipeline drawn once, in eight rough stages: delivery → landing/validation → normalization/matching → status → access → issue detection/intake → routing/resolution → feedback. Brief's problem 1 = stages 2–5; problem 2 = stages 6–8. "Through issue resolution" implies the loop closes back into the data layer.
- "Improve" = what changes at each stage vs. today. "High level" = boxes and a sentence each, not architecture.
- Strong answers show the whole flow, state what stays varied (delivery methods, per the "no universal ingestion" constraint) vs. what becomes standard, mark human-in-loop vs. automated points, and sequence which stage is fixed first.
- Core design decision framed as: where to place the standardization boundary. Upstream stays platform-specific; downstream is consistent. This also answers Q4.
- Noted where the registry (if adopted) would sit: stages 3, 4, 6, 7; Cowork at 2, 3, 7 with human review.

**Status:** Explanation only. Candidate has not yet stated their future-state view.

---

## Turn 7 — 2026-10-07 13:23 EDT (~5 min active) — Q3 re-explained in plain language

**Candidate prompt (verbatim):**
> i need you to break ti down more --plus simple svp

**AI explanation given:** Walked one report through eight plain steps, today vs. after. Today: report arrives by email/portal; ops checks and reformats by hand; IDs matched from memory; nobody knows status; data lands somewhere; consumer reports a problem via whatever channel with no details; ticket bounces; fix not recorded. After: platforms still deliver however they deliver; arrival is logged and lateness flagged; matching rules written down once; one page shows status per platform; consumers see data where they already look; problems reported via short form (platform, item, what's wrong); form routes to the platform's owner; fix and reason recorded next to the report. Key decision: the mess stops at the moment of arrival; everything after follows the same rules.

**Status:** Explanation only.

---

## Turn 8 — 2026-10-07 13:33 EDT (~15 min active) — Candidate's future-state vision

**Candidate prompt (verbatim):**
> i mean the reality for me is ideally i build an agent that sits on a server -- we use a cron job on the server to pull any data by API, scheduled data feeds, spin up a headless chrome window and login and download the reports from partner portals (using securely stored credentials in env variables etc), but the agent can also take data inputs via slack, email etc so that stakeholders who compile data more manually can submit it. If regional/business teams  compile data in a custom way i would work with them to disover how we can get aces to the data in the least obtrusive way possible.  We should be able to build determinisitc solutions for porcessing the data mostly iwth an agentic fallback in case the shape of the data changes. the agent can incoirporate it when possible and flag that something has changed and hold integrating until the corect human in the loop verifies and approves it.
>
> Anyway once we have the data it gets put into a DB or airtable or both, via API or MCP. IDK if airtable has  data viz features but if not we can build this out on an intranet portal for instance or whatever resources eng has approved and allocated. If Airtable allows we can build different views for all the different roles or we can build out our cutom app to have RBAC.
>
> THEN, using what we learned from ticket disvovery process, we train the agent to produce responses to the most common tickets / data requests.

**Candidate's future state (candidate-originated):**
- Server-side agent with cron: pulls via API and scheduled feeds; headless browser login to partner portals with securely stored credentials; accepts manual submissions via Slack/email; least-obtrusive access to regional trackers.
- Deterministic processing for known shapes; agentic fallback on schema change that incorporates where possible, flags the change, and holds integration until the correct human approves.
- Storage: DB and/or Airtable via API or MCP. Access: Airtable role views if viz is sufficient, else intranet portal / custom app with RBAC using eng-approved resources.
- Support: use Round 3 ticket findings to have the agent produce responses to the most common tickets and data requests.

**AI feedback given:**
- Strengths: one front door for many delivery methods (the standardization boundary); deterministic-first with agentic fallback and hold-for-approval (matches brief's human-review constraint); Slack/email intake meets manual contributors where they are; ticket discovery becomes the automation spec.
- Collisions with brief: (1) large custom build vs. limited eng capacity, so sequence by ROI from discovery; (2) headless-browser portal login is a ToS, credential, and fragility risk, so position as last resort after requesting API/feed/SFTP from partner, with legal check, flagged as risk; (3) "train the agent" should be reframed as giving it registry + resolved-ticket library + templates; split status questions (auto-answer via lookup) from defect reports (drafted, human sends).
- Answered: Airtable Interface Designer has charts/dashboards and per-user interface permissions, adequate for status and leadership views, not for cross-platform analytics (use existing BI on warehouse). Storage is both: data in DB, registry/status/intake/exceptions in Airtable.
- Suggested deck framing: capability-level stage table (intake, processing, storage, access, support) with build effort, low-effort rows first, portal automation outside table as flagged risk. Keep components for live Q&A.

**Status:** Candidate's future-state vision recorded. Deck framing suggested, not yet accepted.

---

## Turn 9 — 2026-10-07 13:44 EDT (~10 min active) — Candidate builds it; ROI and success measures

**Candidate prompt (verbatim):**
> I mean I can build it myself i dont need eng!! i just need them to let me use server space. Can you take that into account. for ROI assume I am being paid $100 per hour of SBBS time x number of hours it takes to do discovery/build/test. that is part of the cost of a new solution! that addresses the fginal question, measure of success. we did calc of the manual mess workflow during discovery. Success = we have confirmed positive ROI and tool adoption, anythingf else?

**Candidate decisions (recorded):**
- Candidate builds the solution personally; engineering is not asked for build capacity, only server space.
- ROI cost basis: $100/hour × Senior Business Solutions Specialist hours for discovery, build, and test.
- Baseline for benefit side comes from the time × frequency × headcount questions in discovery Rounds 1 and 2.
- Success definition proposed by candidate: confirmed positive ROI and tool adoption.

**AI feedback given:**
- Reframe eng constraint: ask is hosting/scheduled jobs, secrets store, warehouse read + landing write, and a security review. Position as "Business Solutions builds and runs, Engineering reviews and hosts," with code and runbook in a shared repo, to pre-empt shadow-IT and bus-factor objections.
- ROI: include ongoing maintenance hours (scrapers break) in cost; benefit = hours saved × cycles/yr × headcount × rate across producer and consumer workflows plus support hours; headline as payback period in months; state whether saved-time rate is $100 flat or role-based.
- Success measures: brief Q6 names four outcomes (manual work, data delivery, visibility, support resolution); ROI covers only the first and adoption is a proxy. Suggested one metric each, baselined in discovery: hours per cycle; share of pilot feeds available within agreed window; count of status-question tickets; time to close + routing hops + share of complete intake; adoption share of pilot stakeholders using new views/form; optional match rate / orphan count for Rights.

**Status:** Candidate's ROI approach and builder role recorded. Metric set proposed, not yet accepted.

---

## Turn 10 — 2026-10-07 13:48 EDT (~10 min active) — Ongoing costs and pilot design

**Candidate prompt (verbatim):**
> ongoing costs would be: agentic ingestion, agentic fallbacks if any (hopefully minimal), server resources, --pilot would be starting with anything we can get via API or scheduled data feeds PLUS one previously manual process -which ever one is the (a) simplest and (B) has an enthusiastic stakeholder who is eager to get this proces off their desk and is enthusiastic about AI. We'll need their hands on involvement for testing. we dont want to burn through energy of people who only have a little of it. Once we validate that the new system can handle all the API/data dump data PLUS one formerly human source, we can expand one source at a time.

**Candidate decisions (recorded, candidate-originated):**
- Ongoing costs: agentic ingestion, agentic fallbacks (expected minimal), server resources.
- Pilot scope: all sources already available via API or scheduled feed, plus one previously manual process.
- Manual process selection criteria: (a) simplest, (b) enthusiastic stakeholder who wants it off their desk and is positive about AI; their hands-on involvement needed for testing. Rationale: protect the limited energy of stakeholders.
- Expansion: once API/feed sources plus the one manual source are validated, add one source at a time.

**AI feedback given:**
- Costs: add candidate's own maintenance hours at $100/hr; Airtable/Cowork seats near-zero marginal under rollout; reframe fallback frequency as a tracked metric (fallback rate per source) that is both a cost driver and a signal to write a deterministic parser.
- Pilot: include status view and issue intake form for pilot sources so visibility and support-resolution outcomes are measurable, not just hours saved; add a third selection criterion (enough baseline hours to show a visible saving), protect enthusiasm if trading off; define a per-source exit rule before expansion (e.g., three clean cycles, no held exceptions, old process retired); name pilot participants by role (source owner, one consumer, candidate, eng contact for hosting/security, Rights rep if claims/matching involved).
- Framing: choosing for enthusiasm over pain is a deliberate tradeoff; pilot's job is to prove the system and create a reference story.

**Status:** Pilot design is now candidate's. Additions proposed, not yet accepted. Q1 hypotheses still parked.

---

## Turn 11 — 2026-10-07 13:51 EDT (~10 min active) — Returning to Q1 hypotheses

**Candidate prompt (verbatim):**
> ok lets go back to the three hypotheses, given what we discvoered where would we start? I can tell you based on my experience: hypothesis #1 is that our data as it exists right now is probably less accurate than anyone is willing to admit

**Candidate decision (recorded, candidate-originated):**
- Hypothesis 1: current UGC data is less accurate than anyone is willing to admit. Based on candidate's professional experience.

**AI feedback given:**
- Sharpened H1 for the deck as "accuracy is assumed, not measured": validation is informal, IDs matched by hand, errors surface only when consumers notice, no error rate exists. Tested by inventory sample reconciliation (disagreements, orphans), Round 1 "how do you validate," Round 2 "how did you know it was wrong last time."
- Starting point: inventory and sample reconciliation, which is already step one of the candidate's discovery plan and is the direct test of H1.
- Proposed H2 and H3 derived from the candidate's own discovery rounds: H2 "manual effort is larger than anyone has totaled" (tested by Round 1/2 time × frequency × headcount; doubles as ROI foundation); H3 "issues bounce because nobody owns the source, only the team" (tested by Round 3 ticket sample: hops, completeness, time to close; fix is owner-per-source row plus required intake fields).
- Framing: accuracy, effort, ownership = three unmeasured things, one per discovery round. Earlier AI hypothesis on freshness/status folded into H3 or into the rationale for Sources table columns.

**Status:** H1 is the candidate's. H2 and H3 proposed for acceptance, edit, or replacement.

---

## Turn 12 — 2026-10-07 13:54 EDT (~5 min active) — H3 rejected, alternatives offered

**Candidate prompt (verbatim):**
> idk about your hypothesis #3

**Candidate decision (recorded):** AI-proposed H3 (issues bounce because ownership is per team, not per source) rejected as too close to the brief's own problem statement.

**AI alternatives offered for H3, in the same "unspoken truth" register as H1/H2:**
1. The process lives in people's heads, not documents (tested by Round 1 workflow mapping; ties to brief's knowledge-sharing goal). AI lean.
2. Several teams quietly collect and clean the same data (tested by "who else pulls this" and the inventory; compounds H1 and H2).
3. Nobody can say which data is current (tested by Round 2; reads more as a requirement than a revelation).

**Status:** Awaiting candidate's choice or own H3.

---

## Turn 13 — 2026-10-07 14:01 EDT (~35 min active) — H3 chosen; first slide draft produced

**Candidate prompts (verbatim):**
> ok go with the first one, process lives in people's heads
>
> okn next put together a draft of some slides, I need to go work so id like to see a first draft, keep in mnd the assignment prompt and note where we have holes that we havent decided yet i will look at those nexrt i just wnana get a handle on wher we are

Mid-turn, after seeing slide 1:
> omg too many words way too many

**Candidate decision (recorded):** H3 = "the process lives in people's heads." All three hypotheses now set: accuracy assumed not measured (Tom's), manual effort never totaled (AI-proposed, pending explicit confirmation), process lives in people's heads (Tom's pick from AI alternatives).

**Steps taken:**
1. Wrote `deck/draft-v1-outline.md`: slide-by-slide content mapped to the six assignment questions, every undecided item marked [OPEN].
2. Built a five-slide deck as a private Claude artifact (Slides type) at https://claude.ai/artifact/R9iWyULtDLybAMGDdJSMaG. Title folded into slide 1 to stay within the five-slide cap.
3. After candidate feedback on word count, rewrote all five slides to headlines and short phrases; detail moved to speaker notes. Slide source saved to `deck/draft-v1-src/`.

**Design choices (AI):** Domine headings, Public Sans body; navy/off-white palette with orange accent; orange OPEN pills mark undecided items on each slide; "Draft 1 · not for submission" footer.

**Open items carried on the slides:** H2 wording; assumption phrasing; title-slide count; extra interview questions; standardization boundary and registry split confirmation; portal-scraping stance; "train the agent" wording; build order; pilot additions (status view and intake form, baseline-hours criterion, exit rule, participants); metric set; final active-time figure for the disclosure.

**Not yet placed:** an explicit risks and tradeoffs line; what fixes H3 (documentation or runbook per source).
