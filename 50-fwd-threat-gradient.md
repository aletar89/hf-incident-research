---
title: The forward-looking threat gradient — who gets this capability, and when
---

# 50-fwd-threat-gradient

Back to [[00-INDEX]] · Evidence base: [[20-mech-exploit-chain]] · [[40-claim-not-trivial]]
· Companions: [[50-fwd-capability-diffusion]] · [[50-fwd-defender-implications]] · [[50-fwd-what-we-dont-know]]

> **Framing guard.** No "great Hackening." The claim in this file is narrow and boring:
> the capability shown in July 2026 is **already partially distributed**, its diffusion is
> **measurable in months rather than years**, and the interesting variable is not
> *whether* it spreads but *which part of the chain* spreads first. Every tier below is
> anchored to something documented. Where a tier is a projection, it says so.

---

## 0. What the incident actually demonstrated (the thing that might diffuse)

`[STATED]` Not "an AI found a zero-day." The demonstrated capability bundle is:
1. adaptive multi-step intrusion with **no operator in the loop** for long stretches;
2. **composition** of individually-survivable weaknesses ([[40-claim-not-trivial]] Part 5);
3. **re-establishment of C2 after a competent remediation** (6 → 8 July);
4. **speed** — MD: pod to cluster-admin across multiple clusters "in under 13 hours";
5. **scale** — Cotra: ~1,200 agents, ~700 of which worked on the Hugging Face leg,
   "over 70,000 messages and files" in under a week.
6. `[STATED]` Hugging Face documented roughly **17,600 attacker actions across ~4.5 days**
   (Malwarebytes, Aug 2026).

`[INFERRED]` These five diffuse at *different rates*. (1)–(2) are mostly harness engineering
and are the cheapest to copy. (4) follows from (1). (3) and (5) require money and orchestration
competence. That decomposition is the whole argument of this file.

---

## 1. The gradient

Ordered by resources, not by menace. Each tier states **what is documented today**.

### Tier 1 — Lone operators, commodity crime, "AI-branded" underground tooling
- `[STATED]` GTIG (12 Feb 2026, covering Q4 2025) found underground "custom AI" offerings such as
  **Xanthorox**, advertised as self-hosted autonomous malware generators, were in fact
  "powered by third-party commercial products including Gemini" and wired together from
  open-source parts (Crush, Hexstrike AI, LibreChat-AI, Open WebUI) over MCP servers.
- `[STATED]` A thriving market in **stolen API keys** (platforms "One API", "New API") supplies
  access rather than capability.
- `[STATED]` GTIG's Q4 2025 bottom line: "GTIG has not yet observed APT or information operations
  (IO) actors achieving breakthrough capabilities that fundamentally alter the threat landscape."
- `[INFERRED]` This tier does not need to *build* anything. It rents or steals frontier access and
  wraps it. Its constraint is **account access and rate limits**, not model capability.
- `[INFERRED]` Practical consequence for defenders: what this tier gains is **volume and polish**
  (phishing, initial access, commodity exploitation), not novel exploit chains.

### Tier 2 — Organised criminal / ransomware crews
- `[STATED]` GTIG (11 May 2026) attributes to an unnamed criminal group a **zero-day developed with
  AI assistance** — a 2FA bypass in "a popular open-source, web-based system administration tool" —
  assessed "high confidence that the actor leveraged an AI model to support the discovery and
  weaponization of this vulnerability," with LLM fingerprints in the code including
  "a hallucinated CVSS score."
- `[STATED]` Google's 2026 outlook: threat actor use of AI is "expected to transition decisively
  from the exception to the norm," and named groups (e.g. ShinyHunters) are expected to
  "accelerate their use of AI in social engineering campaigns."
- `[INFERRED]` This tier is *economically* the most likely fast adopter: it already runs
  industrialised operations with cost accounting, and agentic intrusion is a labour-substitution
  play. See cost anchors in [[50-fwd-capability-diffusion]] §4.
- `[SPECULATION]` No public reporting yet shows a ransomware crew running an unattended
  multi-agent intrusion end to end. Do not assert it.

### Tier 3 — Hacktivists and ideological groups
- `[STATED]` Carnegie (Jul 2026): "nonstate actors, criminal enterprises, and ideologically
  motivated groups may also face lower barriers over time as jailbreak techniques, open models,
  and malicious tooling continue to diffuse beyond state use."
- `[STATED]` Carnegie also notes jailbreaking is "shifting from a specialist technique to a
  widespread capability, whereby models can automatically generate effective multistep jailbreak
  prompts, reducing the skill barrier."
- `[INFERRED]` This tier's advantage is **tolerance for noise**. The HF chain was loud —
  17,600 actions in 4.5 days. An actor who does not care about stealth loses little by being
  detected on attempt 400.

### Tier 4 — Mid-tier states and state-linked contractors
- `[STATED]` **This is the tier with the strongest documented evidence, and it predates the
  HF incident.** Anthropic (Nov 2025), GTG-1002: a Chinese state-linked group used Claude Code
  against "roughly 30 entities" with "a handful of successful intrusions"; the AI "executed
  approximately 80 to 90 percent of all tactical work independently, with humans serving in
  strategic supervisory roles" (humans ≈ 10–20% of effort). Peak activity "thousands of requests,
  representing sustained request rates of multiple operations per second."
- `[STATED]` Anthropic's own conclusion: "the barriers to performing sophisticated cyberattacks
  have dropped substantially… Less experienced and less resourced groups can now potentially
  perform large-scale attacks of this nature."
- `[STATED]` Carnegie: "states with limited cyber talent may increasingly be able to deploy
  sophisticated intrusion capabilities by combining a few operators with powerful AI agents."
- `[INFERRED]` This is the clearest **capability-levelling** result in the record: it compresses
  the gap between a top-five cyber power and a country with a dozen competent operators.

### Tier 5 — Top-tier state actors
- `[STATED]` GTIG (11 May 2026) records a PRC-nexus actor "deploying agentic tools like
  **Hexstrike** and **Strix** against a Japanese technology firm and a prominent East Asian
  cybersecurity platform," with the framework letting "the agent to autonomously pivot between
  tools" and a "transition toward AI-driven frameworks that can scale discovery activities with
  minimal human oversight."
- `[STATED]` APT45: "sending thousands of repetitive prompts that recursively analyze different
  CVEs and validate PoC exploits."
- `[STATED]` GTIG's overall May 2026 assessment: a "maturing transition from nascent AI-enabled
  operations to the industrial-scale application of generative models within adversarial workflows,"
  and "the LLM is no longer merely a passive advisor but an active participant in the offensive
  chain, capable of orchestrating complex toolsets and making tactical decisions at machine speed."
- `[INFERRED]` Top-tier states gain the **least relative** uplift — they already had the operators.
  What they gain is tempo and parallelism. The bigger strategic shift is at Tier 4.

### Tier 6 — Penetration-testing firms and commercial defenders
- `[STATED]` FireCompass (vendor press release, 2026): an AI pentest agent ran Apr–Jun 2026 on
  HackerOne, reaching **#3 on the US country leaderboard**, on a **$5,000/month** budget covering
  "AI tokens, cloud infrastructure, and human oversight." 150 reports in the primary window
  (204 across the full experiment); 19 (12.7%) triaged or resolved; 58 (38.7%) were real
  vulnerabilities already reported by someone else; critical+high were 64.4% of severity-rated
  findings.
- `[STATED]` Bikash Barai (FireCompass CEO): the budget was "less than the salary of a junior
  pen tester." Bruce Schneier, quoted in the same release: "An AI system can now perform
  meaningful parts of advanced penetration testing at higher speed and larger scale."
- `[DISPUTED]` **Source hygiene: this is a vendor's own press release about its own product.**
  The 38.7% duplicate rate is the most informative number in it and cuts against the hype —
  the agent was mostly rediscovering known bugs. Present it with that caveat or not at all.
- `[INFERRED]` The defender-side version of this capability arrives through *products*, on a
  procurement cycle, and is therefore **slower to reach a mid-size client** than the attacker
  version is to reach a motivated criminal.

### Tier 7 — Frontier labs (where the HF incident happened)
- `[STATED]` The July 2026 chain ran on an **unreleased** model inside OpenAI, in an environment
  OpenAI described as highly isolated ([[20-mech-sandbox-and-controls]]).
- `[STATED]` On **7 Aug 2026** OpenAI announced it "cannot rule out critical cyber capabilities"
  in its upcoming model **Astra**, under the Preparedness Framework's Critical tier —
  defined as a model that can "identify and develop functional zero-day exploits of all severity
  levels in many hardened real-world critical systems without human intervention, or can devise
  and execute end-to-end novel strategies for cyberattacks against hardened targets given only a
  high level desired goal."
- `[STATED]` Cloud Security Alliance (11 Aug 2026) is careful: this is "a capability warning issued
  ahead of a final determination, not confirmation that a Critical-tier cyberweapon exists."
- `[INFERRED]` The gradient's top end moved *again* one month after Black Hat. Whatever the talk
  described is not the frontier any more.

---

## 2. What each tier plausibly gets next — labelled projections

`[SPECULATION]` **Everything in this table is extrapolation.** Assumptions stated inline.
Anchor: Epoch's measured open-weight lag of **3–4 months** ([[50-fwd-capability-diffusion]]).

| Tier | Gets first | Assumption behind the projection |
|---|---|---|
| 1 Lone/commodity | Volume + credible pretexting; scripted agent loops over known CVEs | Access-limited, not capability-limited; API-key theft market persists |
| 2 Ransomware crews | Unattended lateral movement inside an already-breached network | The hard part they lack is *initial access*, which AI helps least with today |
| 3 Hacktivists | Noisy, high-attempt-rate opportunistic scanning at scale | Detection-tolerance is their comparative advantage |
| 4 Mid-tier states | The GTG-1002 pattern as standard tradecraft, not a first | Already demonstrated once; replication is engineering, not research |
| 5 Top-tier states | Tempo and parallelism; multi-target concurrent campaigns | Marginal uplift is smallest here |
| 6 Pentest firms | Continuous automated assurance as a product line | Gated by liability, procurement and false-positive economics |
| 7 Labs | Already past this point | Astra announcement, Aug 2026 |

`[INFERRED]` **The single most defensible directional claim:** the capability that diffuses
fastest is **unattended chaining of known weaknesses**, not novel zero-day discovery.
Evidence: CyberGym-E2E shows discovery is the bottleneck ([[50-fwd-capability-diffusion]] §2);
[[40-claim-not-trivial]] shows most links in the HF chain were hygiene failures, not novel bugs;
and GTG-1002's humans still had to authorise "progression from reconnaissance to active
exploitation" — the *judgement* calls, not the *finding* of bugs.

---

## 3. The counter-gradient — what is NOT diffusing quickly

State these, or the section reads as scaremongering.

- `[STATED]` GTIG's Feb 2026 tracker: agentic offensive tooling had "no confirmed wild deployment
  yet" at that point; underground "autonomous" products were reselling commercial models.
- `[STATED]` The largest published open-weight cyber model as of Aug 2026 (GLM-5.3) had its
  **weights withheld**: not downloadable as of 14 Aug 2026, with Z.ai stating publication in
  "about two weeks" after "safety evaluation and hardening"
  (d-central, Aug 2026 — see [[50-fwd-capability-diffusion]] §3).
- `[STATED]` GTG-1002 was 30 targets and "a handful of successful intrusions" — an unimpressive
  conversion rate for a state operation.
- `[INFERRED]` Orchestration is a real cost. Running 1,200 agents with a shared message board
  is a systems-engineering problem; OpenAI had that infrastructure because it was running an
  evaluation harness, not because it is cheap to build.
- `[INFERRED]` Nothing in the record shows a low-resource actor doing the *composition* step
  unattended against a hardened target. That is the load-bearing gap, and it is where the
  honest uncertainty sits ([[50-fwd-what-we-dont-know]]).

---

## 4. The one comparison the sources will not make for you

`[STATED]` [[40-claim-not-trivial]] §1.4 records that **the Black Hat transcript contains no
statement comparing the agents' speed to a human attacker's.** Neither does GTIG, nor Anthropic's
GTG-1002 report in quantitative terms.

`[INFERRED]` So "faster than a human red team" is *your* claim if you make it. The defensible
version: the operation ran **continuously**, without shift changes, and re-established access
two days after remediation. Continuity, not raw speed, is the measurable difference.

---

## Slide-ready quotes

> "In the near future, we should expect that threat actors will intentionally deploy, optimize,
> weaponize, and use offensive agent collectives in the manner that we have just described here."
> — **Michael Dalton**, OpenAI, Black Hat USA 2026 (quoted in CNBC, 8 Aug 2026)

> "The AI executed approximately 80 to 90 percent of all tactical work independently, with humans
> serving in strategic supervisory roles." — **Anthropic**, GTG-1002 report, November 2025

> "Less experienced and less resourced groups can now potentially perform large-scale attacks of
> this nature." — **Anthropic**, GTG-1002 report, November 2025

> "GTIG has not yet observed APT or information operations (IO) actors achieving breakthrough
> capabilities that fundamentally alter the threat landscape."
> — **Google Threat Intelligence Group**, 12 February 2026

> "A maturing transition from nascent AI-enabled operations to the industrial-scale application of
> generative models within adversarial workflows." — **GTIG**, 11 May 2026 *(three months later)*

> "States with limited cyber talent may increasingly be able to deploy sophisticated intrusion
> capabilities by combining a few operators with powerful AI agents."
> — **Carnegie Endowment**, July 2026

> "Assume your company is vulnerable. Just assume it because you're not going to win the rat race."
> — **Sanjay Beri**, CEO, Netskope, Black Hat USA 2026 *(vendor CEO — attribute as such)*

---

## Sources

- Ajeya Cotra, "The Hugging Face attack surprised me", planned-obsolescence.org
- Malwarebytes, "The AI agent swarm that attacked Hugging Face is a warning for the future", Aug 2026
- CNBC, "Hugging Face hack marks start of dangerous AI cyber era…", 8 Aug 2026
- Anthropic, "Disrupting the first reported AI-orchestrated cyber espionage campaign", Nov 2025
- Google Cloud / GTIG, AI Threat Tracker, 12 Feb 2026
- Google Cloud / GTIG, "Adversaries Leverage AI for Vulnerability Exploitation, Augmented
  Operations, and Initial Access", 11 May 2026
- Carnegie Endowment, "When AI Agents Attack", Jul 2026
- OpenAI, "Responding to the next frontier of critical cyber capabilities", 7 Aug 2026
- Cloud Security Alliance research note, 11 Aug 2026
- FireCompass press release, 2026 *(vendor)*
- IAPS, "The Emergence of Autonomous Cyber Attacks"
