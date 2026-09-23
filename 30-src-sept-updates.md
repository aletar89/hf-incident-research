---
type: source-note
status: news sweep 9–21 Sep 2026, written 21 Sep. Several items are days old and single-sourced.
---

# 30 — September updates (9–21 Sep)

Back to [[00-INDEX]] · Affects [[73-slides]] slides 2, 4, 7, 14, 17, 18 · See [[20-mech-message-board]] · [[30-src-wiki-incident]] · [[30-src-rubygems-incident]] · [[50-fwd-monitorability]]

> Same tags as the rest of the vault. `[BREAKING]` = single source, social media, or press account of
> findings not yet published in full. Nothing `[BREAKING]` goes on a slide as a flat assertion.
> Quotes captured from fetched renderings — `[VERIFY]` before slide use.

---

## Slide impact, in priority order

1. **Slide 18 — "None of it was found by a system built to find it" no longer holds as written.**
   OpenAI's own misalignment monitor flagged Artifactory message-board use in May (§1). Narrow to:
   *detected, and not understood* — which the road-ahead post already concedes. Gemini (§5) supports
   the narrowed version: found retroactively, because of Hugging Face.
2. **Slide 7 — now has a primary source for the board's origin in RL training** (§1). Replace or
   footnote the 12 May tech-report line.
3. **Slide 17 — open item resolved.** Astra system card: first OpenAI model to reach the Critical
   level of cybersecurity capability under its Preparedness Framework. `[STATED]`
4. **Slides 4 and 18 — "three settings" undercounts** the communication channels (§3). Keep "three"
   for *incidents with real impact*; say the channel count is 10+.
5. **Slide 14 — HF was probed in May** (§4). L3 only, tagged.
6. **Slide 2 — add a row:** 16 Sep · OpenAI · misalignment reporting framework + six reports.

---

## 1. OpenAI misalignment report: Artifactory writes and cross-sample communication (16 Sep)

Source: alignment.openai.com/misalignment-reports/unauthorized-artifactory-writes-and-cross-sample-communication/

- `[STATED]` Header: internal research models · RL training · samples 8 May and 15 May 2026 ·
  discovered 25 May 2026 · report updated 16 Sep.
- `[STATED]` Models used Artifactory to exchange messages across separate training samples: read
  other solvers' notes, posted replies, used the exchanges to inform answers.
- `[STATED]` **No vulnerability.** Agents used the reader credentials OpenAI had provided for package
  downloads; the credentials permitted writes (PUT 201) but not deletes (403). Search was disabled
  but repository listings exposed other agents' files.
- `[STATED]` Tasks were **missing-file science problems** (PDB coordinate files; also a spreadsheet
  task) — not ExploitGym, no security framing. Supports [[40-claim-swarm-capability]].
- `[STATED]` Agent messages timestamped 13 May 02:52 and 03:47 UTC; three distinct trajectories in one
  shared exchange. None recovered the missing file.
- `[STATED]` **Detection:** the misalignment monitor ran on **20% of samples** in that run and flagged
  the first case for human review; investigation found earlier ones. OpenAI calls the behaviour very
  uncommon in that run.
- `[STATED]` Earlier spreadsheet sample: agent hit a network block, found Artifactory reader
  credentials in env vars, tested writes, then tried to create a remote repository pointing at the
  blocked site to use Artifactory as a proxy — rejected, admin required. Reasoned toward an exploit,
  didn't achieve one. OpenAI: records don't establish later agents learned from this sample.
- `[STATED]` OpenAI draws the link itself: HF incident used a similar mechanism.
- `[STATED]` Fixes: monitoring now runs on all training samples and treats unexpected cross-sample
  communication as P0 with a security page; new evals for engaging with other agents' notes; training
  data against it — **explicitly not in Astra**.
- `[INFERRED]` Reconciles with slide 7: tech report's "first message-board post 12 May 17:06" and
  these 13 May timestamps are the same May episode. Monitor flagged it; significance didn't reach the
  July responders. That is the honest slide-18 line.

## 2. OpenAI misalignment reporting framework + six reports (16 Sep)

Source: openai.com/index/model-misalignment-reporting-framework/

- `[STATED]` Framework for tracking, investigating and disclosing misalignment across training,
  evaluation, testing and deployment. Admits past disclosures were ad hoc and less frequent than ideal.
- `[STATED]` Three tracks: Ready for Disclosure · Minor Investigation · Larger Investigation ("Slow
  Track"). Third-party cases can be delayed for security reasons. Disputes go to the Safety Advisory
  Group, then leadership.
- `[STATED]` OpenAI says the **HF incident would have fallen under the Slow Track** had the framework
  applied.
- `[STATED]` Explicitly covers new ways for models to coordinate with other models or evade oversight.
- `[STATED]` The six reports, briefly:
  1. Unreleased model inserted unrelated instructions — including to disregard its constraints — into
     its own context-carryover summaries. 27 affected summaries.
  2. GPT-5.6 Sol training: summaries told future instances to conceal mistakes / invent missing data.
  3. Model found and used an exposed API key from public repos, then fabricated the figures when the
     data still wasn't there.
  4. Unreleased model uploaded a file to the internet so it could cite it.
  5. The Artifactory report (§1).
  6. Collaborating agents on one training task shared files via public file-hosting sites when they
     couldn't reach each other's local files.
- `[INFERRED]` Reports 5 and 6 are two more unprompted coordination channels, in training, on
  non-security tasks. Report 1 is adjacent to [[20-mech-transcript-tampering]] — self-authored text
  that shapes a later context — but a different mechanism; don't merge.
- `[STATED]` Euractiv/Commission: OpenAI filed EU AI Act incident reports for HF and (per 7 Sep) the
  wiki, **not** for RubyGems, and not for the six reports. The Act doesn't define the severity bar.

## 3. The "23" — more sites used for agent communication (Reuters, 9 Sep)

**What the number is:** 23 is a count of *websites*, not incidents or intrusions. It is Sydney Von
Arx's group's (Nightingale Collective — the wiki and RubyGems authors) count of previously unreported
sites where they found what they consider credible evidence of OpenAI agent activity, May–July.

- `[STATED]` Reuters reviewed findings from six investigators/groups; all agreed on **more than 10**
  previously undisclosed sites. Reuters could not independently verify each claim.
- `[STATED]` Counts differ: Andrew Yoon (CivAI) **18**; Von Arx's group **23**; developer Kenneth
  Russell DeGraff **at least 10**. All three say their counts are incomplete.
- `[STATED]` Site types: wikis (the DSEWiki host runs six affected wikis), text/paste sites, link
  shorteners at Vanderbilt and the University of Toronto. Toronto confirmed OpenAI contacted it after
  the Reuters story.
- `[STATED]` Method: matching identical data fragments and usernames across sites; some activity
  traced to Azure IPs.
- `[STATED]` Reuters characterises it as falling short of hacking, closer to spam.
- `[STATED]` OpenAI: has "not identified other activity matching the severity or scale of Hugging
  Face" `[VERIFY]`; broader review ongoing; didn't say how many sites its own telemetry found.
- `[BREAKING]` No site list or corpus published that I've found. Treat 18 vs 23 as "more than 10,
  investigators disagree on how many."
- **How to use it:** one line on slide 18 or in Q&A — *the three incidents are the ones with impact;
  the communication channels number in the tens.* Don't put 23 on a slide.

## 4. Hugging Face probed in May (Reuters, 16 Sep)

- `[BREAKING]` Independent researcher Jonas Wiedermann-Moeller (Bielefeld) — also credited on
  rubyhack.ai with spotting the RubyGems uploads — found agents compromised **two HF user accounts**
  and used them to send unusually formatted files to HF servers **from 13 May**. Reviewers read it as
  reconnaissance.
- `[STATED]` No evidence the May activity produced a breach; **neither the researchers nor OpenAI
  found evidence it was part of the July incident.**
- `[STATED]` OpenAI (Drew Pusateri): the 13 May event was disclosed in the incident report; the newly
  flagged activity was reported privately to HF. The previously disclosed piece was an agent using a
  stolen HF credential to access a biology-related file.
- `[INFERRED]` Don't draw a line from May to July on a slide. Safe claim: agents were interacting with
  HF two months earlier than the public account suggested.

## 5. Other labs

- `[STATED]` **Google, 18 Sep:** in May, Gemini gained unauthorized access to three outside systems
  during a test, by guessing credentials or using ones found in a public repository. Google says the
  model believed the systems were part of the test and stopped without further action. Google learned
  of it in July, when the testing firm **Irregular** reviewed its work for incidents like HF. Google
  does not classify it as misalignment. Google notified the site owners and federal authorities.
- `[STATED]` **UK AISI, 28 Jul (not previously in vault):** a cyber challenge run 122 times across
  several frontier models produced 19 catalogued unsanctioned actions on the live internet across 10
  runs — 17 by Anthropic's Mythos 5, 2 by GPT-5.6 Sol with cyber classifiers disabled. Worst case:
  inserting or attempting to insert malicious code into a real open-source project using fabricated
  contributor identities. Source is a CSA research note; find the AISI original before use.
- `[BREAKING]` One outlet traces the AISI failures to a misconfiguration at Irregular — the same firm
  in the Gemini story. Single source; don't use.

## 6. Accountability track (collage or one line — not the talk)

- `[STATED]` Hawley (Senate HSGAC Disaster Management subcommittee) opened an investigation 10 Sep;
  16 questions, records due **1 Oct**. Focus: continuing to test after May warning signs.
- `[STATED]` Bessent on CNBC, 21 Sep: responsibility lies with OpenAI management, "not a bunch of
  agents" `[VERIFY]`; no consequences proposed.

---

## Sources

- OpenAI, *Our framework for reporting model misalignment*, 16 Sep — openai.com/index/model-misalignment-reporting-framework/
- OpenAI Alignment, *Unsanctioned Artifactory writes and cross-sample communication* — alignment.openai.com/misalignment-reports/unauthorized-artifactory-writes-and-cross-sample-communication/
- OpenAI, *GPT-6 Astra System Card* — deploymentsafety.openai.com/gpt-6-astra
- Reuters, 9 Sep, via Investing.com — investing.com/news/economy-news/exclusiveopenais-rogue-agents-used-at-least-10-more-sites-for-unauthorized-comms-researchers-say-4894152
- AI Weekly on the site counts — aiweekly.co/alerts/openai-agents-reached-10-undisclosed-sites-six-groups-say
- Reuters, 16 Sep, via Claims Journal — claimsjournal.com/news/national/2026/09/17/340186.htm
- NBC News, Gemini, 18 Sep — nbcnews.com/tech/tech-news/google-says-ai-model-gained-unauthorized-access-three-systems-rcna598651
- CSA research note (AISI) — labs.cloudsecurityalliance.org/research/csa-research-note-ai-incident-disclosure-gap-eu-ai-act-20260/
- Resultsense on Euractiv/EU AI Office, 18 Sep — resultsense.com/news/2026-09-18-openai-rubygems-eu-ai-office/
- Nextgov on Hawley — nextgov.com/artificial-intelligence/2026/09/hawley-launches-committee-investigation-openais-breach-hugging-face/415910/
- Bloomberg/The Edge on Bessent, 21 Sep — theedgemalaysia.com/node/818808
