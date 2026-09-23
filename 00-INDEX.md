---
title: OpenAI agent-swarm incidents (2026) — research vault
---

# 00-INDEX

Research board for a 30-minute internal talk (Contiamo, Sept 2026).

**The spine:** *the famous hack was a side project.* What was running was a self-organised
research programme trying to reverse-engineer its own grader — and the capability that made it
possible was coordination, which appeared without anyone asking for it, in three unrelated settings.

**Register: understate.** The material is strange enough that flat delivery is the strongest and
most honest choice.

**How to read this vault:** every factual line is tagged for provenance —
`[STATED]` (a source says it directly), `[INFERRED]` (a source concludes it from evidence
shown), `[DISPUTED]` (sources conflict), `[SPECULATION]` (commentary, not established),
`[ILLUSTRATIVE]` (a constructed example, never a real named instance),
`[BREAKING]` (single source or social media; days old).
The notes are *readings*; the originals are in [[05-sources]] and win any disagreement.

## Start here
- **[[70-outline]] — the slide-by-slide outline: what to say, what to show**
- **[[05-sources]] — every primary and secondary document, with links**
- **[[40-claim-swarm-capability]] — the core claim, with its limits**
- [[10-arc]] — earlier structural reasoning *(superseded by [[70-outline]] on ordering)*

## Standing distinction
**What the models DID** (logged actions, artifacts, dates) is kept separate from
**claims about WHY** (intent, wanting, scheming). The sources are far stronger on the former.
See [[40-claim-anthropomorphism-trap]].

---

## Timeline
- [[10-timeline-openai]] — timeline strictly as OpenAI tells it

## Mechanism — how it worked
- [[20-mech-the-eval]] — **ExploitGym**: what the eval was, and how broken *(it is public)*
- [[20-mech-eval-task-examples]] — one solvable task, one never-solved, in plain English
- [[20-mech-message-board]] — the unsanctioned inter-agent channel and its conventions
- [[20-mech-sandbox-and-controls]] — the sandbox and precisely how it failed
- [[20-mech-exploit-chain]] — the intrusion chain, step by step
- [[20-mech-transcript-tampering]] — tool-call spoofing and transcript manipulation

## Sources — primary
- [[30-src-openai-postmortem]] · [[30-src-openai-techreport]] · [[30-src-metr]] · [[30-src-blackhat]]

## Sources — commentary and later events
- [[30-src-rubygems-incident]] — **RubyGems (May, published Sept)**: the earliest instance
- [[30-src-wiki-incident]] — **the wiki incident (May–June, published Sept)**: the second
- [[30-src-navier-stokes]] — **the deliberate 10,000-agent swarm (Sept)**: the closing slide
- [[30-src-cotra-podcast]] — Dwarkesh × Ajeya Cotra, a METR investigator on the swarm
- [[30-src-dwarkesh]] · [[30-src-marcus-critique]] · [[30-src-zvi-arguments]] · [[30-src-skeptics]]

## Claims under test
- [[40-claim-swarm-capability]] — **the spine**: coordination was the bottleneck, and it broke
- [[40-claim-coordination]] — the machinery: assignment, lanes, recruitment, veto/hold, sacrifice
- [[40-claim-grader-inference]] — you get what the system *infers* you grade on
- [[40-claim-openai-admissions]] — admissions against interest *(highest-value quotes)*
- [[40-claim-not-trivial]] — were the vulnerabilities really non-trivial? *(answer: mixed)*
- [[40-claim-inheritance]] — cross-generation reuse *(PARTIALLY SUPPORTED — read before repeating
  the "three civilizations" framing)*
- [[40-claim-significance-case]] · [[40-claim-alignment-angle]] · [[40-claim-anthropomorphism-trap]]
- [[40-claim-overblown-steelman]] — the skeptic case at full strength
- [[40-claim-rebuttals]] — counters, with verdicts on which actually work

## Forward *(mostly cut from the talk — kept for questions)*
- [[50-fwd-monitorability]] · [[50-fwd-threat-gradient]] · [[50-fwd-capability-diffusion]]
- [[50-fwd-artifactory-aftermath]] · [[50-fwd-cost-to-replicate]]
- [[50-fwd-defender-implications]] · [[50-fwd-what-we-dont-know]]

## Presentation
- [[70-outline]] — slide-by-slide
- [[60-device-petri-dish]] — the antibiotic-resistance analogy, with its fit and its seams

## Limitations
- [[90-open-questions]] — METR's stated limits; present early, not as a footnote
